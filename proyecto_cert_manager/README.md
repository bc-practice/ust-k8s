# Despliegue de cert-manager con Ansible

Este proyecto Ansible te permite desplegar cert-manager en tu clúster Kubernetes de forma sencilla y automatizada.

## Estructura del Proyecto

proyecto_cert_manager/
├── inventory/
│   └── hosts.yml  # Define tus hosts (localhost en este caso)
├── roles/
│   └── cert_manager/
│       ├── tasks/
│       │   └── main.yml  # Tareas para instalar cert-manager
│       ├── defaults/
│       │   └── main.yml  # Valores por defecto para variables (opcional)
│       ├── vars/
│       │   └── main.yml  # Variables específicas del rol (opcional)
├── playbooks/
│   └── instalar_cert_manager.yml  # Playbook principal para desplegar
├── group_vars/
│   └── all.yml  # Variables comunes a todos los hosts (opcional)
└── host_vars/
└── localhost.yml  # Variables específicas para localhost (opcional)
└── values.yaml  (Opcional, si necesitas personalizar la instalación)

## Descripción de los archivos

-   **`inventory/hosts.yml`**

    -   Define el host `localhost` donde se instalará cert-manager.
    -   Utiliza `ansible_connection=local` para indicar la conexión local.

-   **`roles/cert_manager/tasks/main.yml`**

    -   Contiene las tareas principales para instalar cert-manager usando Helm.
    -   Agrega el repositorio de Jetstack.
    -   Instala el chart `cert-manager` en el namespace `cert-manager`, incluyendo los CRDs necesarios.
    -   Espera a que el despliegue `cert-manager-webhook` esté listo.

-   **`playbooks/instalar_cert_manager.yml`**

    -   Playbook principal que invoca el rol `cert_manager`.

-   **`values.yaml` (Opcional)**

    -   Contiene valores personalizados para la instalación de cert-manager.
    -   Consulta la documentación de cert-manager para las opciones disponibles.

-   **`roles/cert_manager/defaults/main.yml`, `roles/cert_manager/vars/main.yml`, `group_vars/all.yml`, `host_vars/localhost.yml`**

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

    - Si necesitas personalizar la instalación, crea y modifica el archivo `values.yaml` o utiliza los archivos `defaults/main.yml`, `vars/main.yml`, `group_vars/all.yml` o `host_vars/localhost.yml`.

3. **Ejecuta el playbook:**

    ```bash
    ansible-playbook playbooks/instalar_cert_manager.yml
    ```

¡Y eso es todo! Ansible se encargará de desplegar cert-manager en tu clúster Kubernetes.

## ¡Importante!

-   Consulta la documentación oficial de cert-manager para obtener información detallada sobre la configuración y personalización.
