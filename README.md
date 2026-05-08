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

```mermaid
graph TD
    subgraph GitHub_Actions [Automatización]
        A[Git Push / Manual Trigger] --> B[Playbook de Ansible]
    end

    subgraph Security_Layer [Capa de Seguridad]
        B --> C{Certificados TLS}
        C -->|Firma CA| D[Nodos Blindados]
    end

    subgraph Infrastructure [Nodos en Docker]
        D --> Node1[Master: 10.0.0.10]
        D --> Node2[Worker 1: 10.0.0.11]
        D --> Node3[Worker 2: 10.0.0.12]
    end

    subgraph Networking [CNI Calico]
        Node1 <--> Node2
        Node2 <--> Node3
        Node3 <--> Node1
    end

    style GitHub_Actions fill:#0d1117,stroke:#22d3ee,stroke-width:2px
    style Infrastructure fill:#0d1117,stroke:#22d3ee,stroke-width:2px
    style Networking fill:#0d1117,stroke:#22d3ee,stroke-width:4px
