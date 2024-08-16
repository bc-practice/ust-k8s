# Despliegue de Loki en modo monolítico con Ansible

Este proyecto Ansible te permite desplegar Loki en modo monolítico, utilizando almacenamiento en el sistema de archivos, de forma sencilla y automatizada.

## Estructura del Proyecto

proyecto_loki/
├── inventory/
│   └── hosts.yml  # Define tus hosts (localhost en este caso)
├── roles/
│   └── loki/
│       ├── tasks/
│       │   └── main.yml  # Tareas para instalar Loki
│       ├── defaults/
│       │   └── main.yml  # Valores por defecto para variables (opcional)
│       ├── vars/
│       │   └── main.yml  # Variables específicas del rol (opcional)
├── playbooks/
│   └── instalar_loki.yml  # Playbook principal para desplegar
├── group_vars/
│   └── all.yml  # Variables comunes a todos los hosts (opcional)
└── host_vars/
└── localhost.yml  # Variables específicas para localhost (opcional)
└── values.yaml # Configuración de Loki

## Descripción de los archivos

-   **`inventory/hosts.yml`**

    -   Define el host `localhost` donde se instalará Loki.
    -   Utiliza `ansible_connection=local` para indicar la conexión local.

-   **`roles/loki/tasks/main.yml`**

    -   Contiene las tareas principales para instalar Loki usando Helm.
    -   Agrega el repositorio de Grafana.
    -   Instala el chart `loki-stack` en el namespace `monitoring` utilizando el archivo `values.yaml`.
    -   Espera a que el componente `distributor` de Loki esté listo.

-   **`playbooks/instalar_loki.yml`**

    -   Playbook principal que invoca el rol `loki`.

-   **`values.yaml`**

    -   Contiene la configuración específica para Loki en modo monolítico con almacenamiento en el sistema de archivos.
    -   Configura `deploymentMode: SingleBinary` y `storage.type: 'filesystem'`.
    -   Ajusta otros parámetros según tus necesidades.

-   **`roles/loki/defaults/main.yml`, `roles/loki/vars/main.yml`, `group_vars/all.yml`, `host_vars/localhost.yml`**

    -   (Opcionales) Permiten definir y sobreescribir variables para personalizar la instalación.

## Requisitos

-   **Ansible:** Asegúrate de tener Ansible instalado en tu sistema.
-   **Helm:** Necesitarás tener Helm instalado para gestionar los charts.
-   **Kubernetes:** Debes tener un clúster Kubernetes en funcionamiento (en este caso, en `localhost`).

## Cómo usar este proyecto

1. **Clona este repositorio:**

    ```bash
    git clone <URL_DEL_REPOSITORIO>
    ```

2. **Configura las variables (opcional):**

    - Si necesitas personalizar la instalación, modifica los valores en `values.yaml` o utiliza los archivos `defaults/main.yml`, `vars/main.yml`, `group_vars/all.yml` o `host_vars/localhost.yml`.

3. **Ejecuta el playbook:**

    ```bash
    ansible-playbook playbooks/instalar_loki.yml
    ```

¡Y eso es todo! Ansible se encargará de desplegar Loki en modo monolítico en tu clúster Kubernetes.

## ¡Importante!

-   El almacenamiento en el sistema de archivos no es persistente. Si necesitas persistencia de datos, considera utilizar un almacenamiento de objetos compatible.
-   Consulta la documentación oficial de Loki para obtener información detallada sobre la configuración y personalización.
