## Despliegue de kube-prometheus-stack con Ansible

Este proyecto Ansible te permite desplegar `kube-prometheus-stack` en tu clúster Kubernetes de forma sencilla y automatizada.

### Estructura del Proyecto

proyecto_kube_prometheus/
├── inventory/
│   └── hosts.yml  # Define tus hosts (localhost en este caso)
├── roles/
│   └── kube_prometheus_stack/
│       ├── tasks/
│       │   └── main.yml  # Tareas para instalar kube-prometheus-stack
│       ├── handlers/
│       │   └── main.yml  # Manejadores de eventos (si es necesario)
│       ├── defaults/
│       │   └── main.yml  # Valores por defecto para variables
│       ├── vars/
│       │   └── main.yml  # Variables específicas del rol
│       └── templates/
│           └── config.yml.j2  # Plantillas Jinja2 para configuración (si aplica)
├── playbooks/
│   └── instalar_kube_prometheus.yml  # Playbook principal para desplegar
├── group_vars/
│   └── all.yml  # Variables comunes a todos los hosts
└── host_vars/
└── localhost.yml  # Variables específicas para localhost

### Descripción de los archivos

-   **`inventory/hosts.yml`**

    -   Define el host `localhost` donde se instalará `kube-prometheus-stack`.
    -   Utiliza `ansible_connection=local` para indicar la conexión local.

-   **`roles/kube_prometheus_stack/tasks/main.yml`**

    -   Contiene las tareas principales para instalar `kube-prometheus-stack` usando Helm.
    -   Agrega el repositorio de Prometheus Community.
    -   Instala el chart en el namespace `monitoring`.
    -   Espera a que Prometheus y Grafana estén listos.
    -   Puedes usar un archivo `values.yaml` para personalizar la instalación.

-   **`playbooks/instalar_kube_prometheus.yml`**

    -   Playbook principal que invoca el rol `kube_prometheus_stack`.

-   **`roles/kube_prometheus_stack/defaults/main.yml`**

    -   (Opcional) Define los valores por defecto para las variables del rol.

-   **`roles/kube_prometheus_stack/vars/main.yml`, `group_vars/all.yml`, `host_vars/localhost.yml`**

    -   (Opcional) Permiten sobreescribir los valores por defecto de las variables.

-   **`roles/kube_prometheus_stack/handlers/main.yml` y `roles/kube_prometheus_stack/templates/config.yml.j2`**

    -   (Opcional) Se utilizan para manejadores de eventos y plantillas de configuración, respectivamente.

### Requisitos

-   **Ansible:** Asegúrate de tener Ansible instalado en tu sistema.
-   **Helm:** Necesitarás tener Helm instalado para gestionar los charts.
-   **Kubernetes:** Debes tener un clúster Kubernetes en funcionamiento (en este caso, en `localhost`).

### Cómo usar este proyecto

1. **Clona este repositorio:**

    ```bash
    git clone <URL_DEL_REPOSITORIO>
    ```

2. **Configura las variables (opcional):**

    - Si necesitas personalizar la instalación, modifica los valores en los archivos `defaults/main.yml`, `vars/main.yml`, `group_vars/all.yml` o `host_vars/localhost.yml`.
    - Si utilizas un archivo `values.yaml`, colócalo en el directorio raíz del proyecto.

3. **Ejecuta el playbook:**

    ```bash
    ansible-playbook playbooks/instalar_kube_prometheus.yml
    ```

¡Y eso es todo! Ansible se encargará de desplegar `kube-prometheus-stack` en tu clúster Kubernetes.

**¡Importante!**

-   Consulta la documentación oficial de `kube-prometheus-stack` para obtener información detallada sobre la configuración y personalización.
-   Asegúrate de entender las implicaciones de seguridad al exponer Prometheus y Grafana en tu clúster.
