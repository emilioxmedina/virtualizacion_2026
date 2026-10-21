# Assessment: Monitoreo y Centralización de Logs

**Estudiante:** Emilio Xavier Medina Mencos
**Namespace:** monitoring-exmm

## Descripción
Implementación de un stack de observabilidad completo en Kubernetes (Minikube) utilizando Prometheus para métricas y la pila Loki/Promtail para la centralización de logs. La visualización se realiza a través de Grafana, expuesto vía Traefik y MetalLB.

## Configuración Realizada
1. **Loki y Promtail:** Instalados vía Helm. Promtail se configuró como DaemonSet para extraer los logs de los contenedores (incluyendo las aplicaciones de `parcial-exmm` y Traefik) hacia Loki.
2. **Prometheus:** Desplegado mediante Helm, optimizando recursos (desactivando Alertmanager y Pushgateway) pero manteniendo el node-exporter y kube-state-metrics.
3. **Grafana e IaC (Provisioning):** Se utilizó un archivo `values.yaml` para aprovisionar automáticamente como código las fuentes de datos (Prometheus y Loki) y un dashboard base de métricas del clúster, sin requerir configuración manual.
4. **Exposición (Ingress y DNS):** Se crearon recursos Ingress para Grafana y Prometheus. Se modificó el archivo `/etc/hosts` de Windows apuntando los dominios `grafana.local` y `prometheus.local` a la IP de Traefik gestionada por MetalLB.

## Evidencias

### 1. Prometheus - Targets en estado UP
Visualización de los endpoints principales en estado activo, accediendo desde el dominio local.
![alt text](image-1.png)
### 2. Grafana - Dashboard de Métricas
Dashboard provisionado como código mostrando el porcentaje de uso de CPU y Memoria del clúster.
![alt text](image.png)
### 3. Grafana - Dashboard de Logs (Loki)
Panel configurado utilizando LogQL para extraer y visualizar los registros en texto de Traefik y los contenedores.
![alt text](image-2.png)