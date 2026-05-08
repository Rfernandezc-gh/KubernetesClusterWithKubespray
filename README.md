# ☸️ Cluster Builder: Implementación de Kubernetes con Kubespray

Este proyecto demuestra la implementación de un clúster de Kubernetes de grado industrial, gestionado íntegramente como **Infraestructura como Código (IaC)**. Utilizando **Kubespray**, hemos automatizado el despliegue sobre nodos simulados, garantizando un entorno seguro, escalable y reproducible.

---

## 📋 Resumen del Proyecto
El objetivo principal es transformar nodos Linux aislados en un clúster coordinado. A diferencia de las soluciones automáticas, este método permite un control total sobre la red, los certificados y los componentes internos del sistema.

* **Arquitectura:** 1 Nodo Master (Control Plane) + 2 Nodos Workers.
* **Motor de Despliegue:** Ansible (Kubespray Playbooks).
* **Networking:** Red Overlay gestionada por **Calico**.
* **Runtime de Contenedores:** **Containerd**.

---

## 🛠️ Guía de Implementación por Fases

A continuación, se detalla el proceso técnico dividido en etapas lógicas. Haz clic en cada fase para expandir la información:

<details>
<summary><b>📍 Fase 1: Aprovisionamiento y Preparación de Nodos</b></summary>

### Simulación de Servidores Reales
Para este laboratorio, se han utilizado contenedores Docker optimizados para actuar como servidores físicos.
* **Imagen base:** `jrei/systemd-ubuntu:22.04` (Permite el uso de `systemd` para gestionar los servicios de K8s).
* **Requisitos:** Acceso SSH configurado y Python instalado en los nodos para permitir la ejecución de los módulos de Ansible.

```yaml
# Estructura básica de los nodos en el host
services:
  k8s-master:
    privileged: true
    networks:
      k8s-net: { ipv4_address: 10.0.0.10 }
