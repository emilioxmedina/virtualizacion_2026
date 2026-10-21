# Assessment 06: Implementación de GitOps con Argo CD
## Descripción
Este repositorio contiene la evidencia y los manifiestos de Kubernetes para la implementación de un flujo de trabajo GitOps utilizando Argo CD en un clúster local (Minikube). El objetivo es automatizar el despliegue y la sincronización de aplicaciones directamente desde un repositorio de GitHub.

---

## 1. Instalación y Exposición del Servicio
Argo CD fue instalado en el namespace personalizado `argocd-exmm`. Para el acceso a la interfaz web, se configuró Traefik como Ingress Controller, exponiendo el servicio a través del dominio `argocd.local` mediante un túnel de Minikube y modificando la resolución DNS local.

![Captura 1: Interfaz inicial de Argo CD](image.png)

---

## 2. Creación y Sincronización de Aplicaciones
Se definieron dos aplicaciones (`app-primera` y `app-segunda`) configuradas para desplegarse en el namespace `parcial-exmm`. Se resolvieron los permisos de RBAC (ClusterRoleBindings) para que el controlador pudiera acceder a los recursos, logrando que Argo CD leyera los manifiestos desde GitHub y desplegara los pods de Nginx exitosamente.

![Captura 2: Aplicaciones Sincronizadas](image-1.png)

---

## 3. Prueba de Automatización GitOps
Para validar la sincronización automática, se editó el archivo `deployment.yaml` de la `app-primera`, escalando la configuración de 1 a 3 réplicas. Al hacer el push a GitHub, Argo CD detectó el cambio automáticamente y actualizó el estado del clúster (Self-Heal y Prune habilitados) creando los pods adicionales sin necesidad de ejecutar comandos de `kubectl`.

![Captura 3: Escalabilidad Automática](image-2.png)