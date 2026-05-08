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
graph TB
    %% Definición de Estilos Neón
    classDef master fill:#1e293b,stroke:#22d3ee,stroke-width:4px,color:#fff,rx:10,ry:10;
    classDef worker fill:#1e293b,stroke:#818cf8,stroke-width:2px,color:#fff,rx:10,ry:10;
    classDef ansible fill:#0f172a,stroke:#fbbf24,stroke-width:2px,color:#fbbf24,stroke-dasharray: 5 5;

    subgraph Control_Plane [Estación de Control]
        A((fa:fa-terminal Ansible Control)):::ansible
    end

    subgraph Cluster [Kubernetes Cluster]
        direction LR
        M[fa:fa-brain Master Node<br/>10.0.0.10]:::master
        W1[fa:fa-gears Worker 1<br/>10.0.0.11]:::worker
        W2[fa:fa-gears Worker 2<br/>10.0.0.12]:::worker
    end

    %% Conexiones de Despliegue
    A -- "SSH + Kubespray" --> M
    A -- "SSH + Kubespray" --> W1
    A -- "SSH + Kubespray" --> W2

    %% Red Interna Calico
    M <--> |Calico BGP| W1
    W1 <--> |Calico BGP| W2
    W2 <--> |Calico BGP| M

    linkStyle 0,1,2 stroke:#fbbf24,stroke-width:2px;
    linkStyle 3,4,5 stroke:#22d3ee,stroke-width:3px;
    style Infrastructure fill:#0d1117,stroke:#22d3ee,stroke-width:2px
    style Networking fill:#0d1117,stroke:#22d3ee,stroke-width:4px
