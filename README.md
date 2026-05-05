# 🚀 Hola Mundo con Flask + Nginx desplegado con Ansible

Proyecto de automatización de infraestructura usando **Ansible** para desplegar
una aplicación **Flask** servida a través de **Nginx** como proxy inverso.

## 📁 Estructura del proyecto

\`\`\`
helloworld-ansible-flask-nginx/
├── deploy.yml              # Playbook principal
├── inventory.yml           # Inventario de hosts
├── vars/
│   └── main.yml            # Variables de configuración
├── files/
│   └── app.py              # Aplicación Flask
└── templates/
    └── nginx.conf.j2       # Plantilla de configuración Nginx
    \`\`\`

    ## ⚙️ Requisitos

    - Debian 12/13
    - Ansible 2.9+
    - Acceso sudo en el host destino

    ## 🔧 Variables disponibles

    | Variable | Valor por defecto | Descripción |
    |---|---|---|
    | `flask_port` | `5000` | Puerto en el que escucha Flask |

    ## 🏗️ Qué hace el playbook

    1. **Instala Nginx** como proxy inverso en el puerto 80
    2. **Instala Python 3** y crea un entorno virtual
    3. **Instala Flask** dentro del entorno virtual
    4. **Copia** la aplicación Flask al servidor en `/opt/flask/`
    5. **Configura Nginx** para redirigir el tráfico a Flask
    6. **Crea un servicio systemd** para que Flask arranque automáticamente
    7. **Inicia** ambos servicios

    ## 🚀 Uso

    ### 1. Clona el repositorio

    \`\`\`bash
    git clone git@github.com:Pedro-Sarmiento/helloworld-ansible-flask-nginx.git
    cd helloworld-ansible-flask-nginx
    \`\`\`

    ### 2. Ejecuta el playbook

    \`\`\`bash
    ansible-playbook -i inventory.yml deploy.yml --ask-become-pass
    \`\`\`

    ### 3. Prueba la aplicación

    \`\`\`bash
    curl http://localhost
    \`\`\`

    Deberías ver:

    \`\`\`
    Hola Mundo
    \`\`\`

    ## 🏛️ Arquitectura

    \`\`\`
    Cliente HTTP
         │
              ▼
                Nginx :80
                     │  proxy_pass
                          ▼
                            Flask :5000
                              /opt/flask/venv
                              \`\`\`

                              ## 🛠️ Servicios gestionados

                              | Servicio | Puerto | Gestionado por |
                              |---|---|---|
                              | Nginx | 80 | systemd |
                              | Flask | 5000 | systemd |

                              ## 📝 Licencia

                              MIT
