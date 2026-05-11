# ☸️ Cluster Builder: Kubernetes Industrial con Kubespray

Este proyecto demuestra la implementación de un clúster de Kubernetes de grado industrial, gestionado íntegramente como **Infraestructura como Código (IaC)**. Utilizando **Kubespray**, se ha automatizado el despliegue sobre nodos inmutables, garantizando un entorno seguro, escalable y profesional.

---

## 📋 Resumen del Proyecto
El objetivo es transformar nodos Linux aislados en un clúster de orquestación coordinado. A diferencia de soluciones automáticas o ligeras (como k3s o minikube), este método permite un control total sobre la red, los certificados y los componentes internos del sistema.

* **Arquitectura:** 1 Nodo Master (Control Plane) + 2 Nodos Workers.
* **Motor de Despliegue:** Ansible (Kubespray Playbooks).
* **Networking:** Red Overlay gestionada por **Calico (Capa 3)**.
* **Runtime de Contenedores:** **Containerd**.

---

## 🗺️ Esquema Visual del Despliegue

https://github.com/user-attachments/assets/e76fd8a2-1154-4735-9c37-56651065119a

