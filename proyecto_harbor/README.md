## Estructura del Proyecto Ansible para Instalar Harbor

proyecto_harbor/
├── inventory/
│   └── hosts.yml
├── roles/
│   └── harbor/
│       ├── tasks/
│       │   └── main.yml
│       ├── handlers/
│       │   └── main.yml
│       ├── defaults/
│       │   └── main.yml
│       ├── vars/
│       │   └── main.yml
│       └── templates/
│           └── config.yml.j2
├── playbooks/
│   └── instalar_harbor.yml
├── group_vars/
│   └── all.yml
└── host_vars/
└── localhost.yml

### Descripción de los archivos

-   **`inventory/hosts.yml`**

    -   Define el host `localhost` donde se instalará Harbor.
    -   Utiliza `ansible_connection=local` para indicar la conexión local.

-   **`roles/harbor/tasks/main.yml`**

    -   Contiene las tareas principales para instalar Harbor usando Helm.
    -   Utiliza variables para mayor flexibilidad y reutilización.

-   **`playbooks/instalar_harbor.yml`**

    -   Playbook principal que invoca el rol `harbor`.
    -   Ejecuta las tareas con privilegios de administrador (`become: yes`).

-   **`roles/harbor/defaults/main.yml`**

    -   Define los valores por defecto para las variables del rol `harbor`.
    -   Puedes personalizar estos valores según tus necesidades.

-   **`roles/harbor/vars/main.yml`, `group_vars/all.yml`, `host_vars/localhost.yml`**

    -   Permiten sobreescribir los valores por defecto de las variables a nivel de rol, grupo de hosts o host individual.

-   **`roles/harbor/handlers/main.yml`**

    -   (Opcional) Define manejadores de eventos para el rol `harbor`.

-   **`roles/harbor/templates/config.yml.j2`**

    -   (Opcional) Contiene plantillas Jinja2 para generar archivos de configuración dinámicamente.

**¡Importante!**

-   Los archivos `handlers/main.yml` y `templates/config.yml.j2` son opcionales.
-   Ajusta los nombres de las variables y la ubicación de los archivos según tus convenciones.

**Cómo usar este proyecto**

1. Clona este repositorio.
2. Configura las variables en los archivos correspondientes.
3. Ejecuta el playbook `instalar_harbor.yml` con Ansible.

**Ejemplo de ejecución**

```bash
ansible-playbook playbooks/instalar_harbor.yml
```
