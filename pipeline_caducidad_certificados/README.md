# Verificación de Certificados Kubernetes

Este proyecto utiliza Bitbucket Pipelines y Ansible para verificar automáticamente la fecha de expiración de los certificados TLS en tus clusters de Kubernetes. La pipeline se ejecuta de forma programada todos los sábados a las 2 AM UTC y te notifica si algún certificado está a punto de expirar.

## Cómo funciona

1. **Bitbucket Pipelines:** Define la pipeline de CI/CD que se ejecuta en la nube de Bitbucket.
2. **Ansible:** Automatiza la tarea de conectarse a tus clusters Kubernetes y obtener información sobre los certificados TLS.
3. **Programación:** La pipeline se ejecuta automáticamente cada sábado a las 2 AM UTC gracias a un disparador cron.
4. **Notificaciones:** (Opcional) Puedes configurar notificaciones por correo electrónico o a través de otras herramientas para recibir alertas sobre certificados próximos a expirar.

## Configuración

1. **Clona este repositorio:** `git clone <URL_de_tu_repositorio>`
2. **Variables de entorno:** Configura las siguientes variables de entorno en la configuración de tu repositorio en Bitbucket:
    - `SSH_USER`: Usuario para conectarte a tus clusters Kubernetes por SSH.
    - `SSH_PRIVATE_KEY`: Clave privada SSH para la autenticación (asegúrate de que sea segura).
    - `CLUSTER1_HOST`: Hostname o IP del primer cluster Kubernetes.
    - `CLUSTER2_HOST`: Hostname o IP del segundo cluster Kubernetes.
3. **Archivo `ansible/hosts.ini`:** Actualiza este archivo con los hostnames o IPs de tus clusters Kubernetes.
4. **Kubeconfig:** Asegúrate de que Ansible tenga acceso a un archivo `kubeconfig` válido para interactuar con tus clusters. Puedes incluirlo en la imagen de Docker o montarlo como un volumen en la pipeline.

## Ejecución

-   La pipeline se ejecutará automáticamente cada sábado a las 2 AM UTC.
-   También puedes ejecutarla manualmente desde la interfaz de Bitbucket Pipelines.
