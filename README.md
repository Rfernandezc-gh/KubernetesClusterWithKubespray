# ☸️ Cluster Lab: Orquestación de Kubernetes con Kubespray (En proceso)

## 1. Presentación del Proyecto
Este proyecto consiste en el despliegue de un clúster de Kubernetes de grado industrial utilizando **Kubespray**. A diferencia de las soluciones gestionadas o ligeras, Kubespray ofrece un control total sobre la infraestructura, permitiendo configurar cada componente del clúster (etcd, red, certificados y runtime) desde cero.

El objetivo es demostrar la capacidad de gestionar **Infraestructura como Código (IaC)** para levantar un entorno de orquestación reproducible, seguro y escalable.


---

## 2. ¿Qué es Kubespray y por qué usarlo?
**Kubespray** es una composición de **Ansible Playbooks**, inventarios y herramientas de aprovisionamiento orientadas a la implementación de clústeres de Kubernetes en entornos *On-Premise* o nubes privadas.

### Ventajas de este enfoque:
* **Basado en Ansible:** Despliegue sin agentes (*Agentless*) a través de SSH.
* **Altamente personalizable:** Permite elegir el CNI (Calico, Flannel, Cilium), el Runtime (Containerd, Docker) y la topología de red.
* **Idempotencia:** El pipeline de despliegue puede ejecutarse múltiples veces garantizando que el estado final sea siempre el definido en el inventario.

---

## 3. Arquitectura del Laboratorio
Para este laboratorio técnico, se ha simulado un entorno de servidores reales utilizando contenedores Linux con **Systemd** habilitado, organizados de la siguiente manera:

| Nodo | Rol | IP Interna | Componentes Clave |
| :--- | :--- | :--- | :--- |
| **k8s-master** | Control Plane | 10.0.0.10 | kube-apiserver, etcd, scheduler |
| **k8s-worker-1** | Worker | 10.0.0.11 | kubelet, kube-proxy, containerd |
| **k8s-worker-2** | Worker | 10.0.0.12 | kubelet, kube-proxy, containerd |


---

## 4. Despliegue con Ansible (IaC)
El despliegue se realiza de forma declarativa definiendo un inventario en YAML. El proceso automatiza la generación de la **Autoridad de Certificación (CA)**, el firmado de certificados TLS para todos los componentes y la configuración de la red Overlay (Calico).

