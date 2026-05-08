# 🏗️ Cluster Lab: Kubernetes Industrial con Kubespray

Este proyecto implementa un clúster de Kubernetes completo utilizando **Kubespray** (Ansible). A diferencia de soluciones ligeras, este método ofrece un control absoluto sobre la red y los certificados del sistema.

---

## 🗺️ Esquema Visual del Despliegue

```mermaid
graph TD
    subgraph GitHub_Actions [CI/CD Pipeline]
        A[Git Push] --> B[Playbook de Ansible]
    end

    subgraph Security_Layer [Capa de Seguridad]
        B --> C{Certificados TLS}
        C -->|Firma CA| D[Nodos Blindados]
    end

    subgraph Infrastructure [Nodos Docker]
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

---

## 🛠️ Guía de Implementación por Fases

> [!IMPORTANT]
> Haz clic en cada fase para ver el detalle técnico y la lógica detrás de cada paso.

<br/>

### 🟦 FASE 1: Aprovisionamiento de Infraestructura
<details>
<summary><b>▶️ Detalles de Infraestructura (Nodos Inmutables)</b></summary>

Para este laboratorio, simulamos servidores reales usando contenedores Docker con soporte de `systemd`. Esto garantiza que los servicios de Kubernetes (kubelet, containerd) puedan correr como demonios reales.

**Configuración clave:**
* **Imagen:** `jrei/systemd-ubuntu:22.04`
* **Modo:** Privilegiado (`privileged: true`)
* **Red:** Bridge con IPs estáticas asignadas.

---
</details>

<br/>

### 🟦 FASE 2: Diseño del Inventario (IaC)
<details>
<summary><b>▶️ Detalles de Configuración (Mapa del Clúster)</b></summary>

Definimos los roles de cada nodo en un archivo YAML declarativo. Esto permite que el despliegue sea **idempotente** (puedes ejecutarlo 100 veces y el resultado será el mismo).

**Lógica del Inventario:**
* **kube_control_plane:** Nodo que contiene el API Server.
* **etcd:** Base de datos del clúster (instalada en el Master).
* **kube_node:** Nodos de trabajo (Workers).

---
</details>

<br/>

### 🟦 FASE 3: Ejecución del Despliegue
<details>
<summary><b>▶️ Detalles de Ejecución (Ansible Playbook)</b></summary>

Es la fase crítica donde Ansible entra por SSH y realiza:
1. Generación de certificados TLS autofirmados.
2. Instalación de **Containerd** como runtime.
3. Despliegue de binarios de Kubernetes.
4. Configuración del **kubelet**.

```bash
# Comando de despliegue profesional
ansible-playbook -i inventory/mycluster/hosts.yml --become cluster.yml

---
</details>

<br/>

### 🟦 FASE 4: Networking y Calico
<details>
<summary><b>▶️ Detalles de Red (CNI de Capa 3)</b></summary>

Se ha seleccionado **Calico** como plugin de red.
* **¿Qué es?** Es el encargado de que los Pods se comuniquen entre sí.
* **¿Por qué?** Usa enrutamiento nativo (BGP), lo que lo hace el CNI más rápido y escalable del mercado.
* **Seguridad:** Permite crear *Network Policies* (Firewalls internos para tus contenedores).

---
</details>

---

## 🧪 Pruebas de Salud (Health Check)
Una vez terminado el proceso, verificamos el estado con:
```bash
kubectl get nodes -o wide

### 💡 Valor Profesional
Este proyecto demuestra que no solo sabes usar Kubernetes, sino que **sabes cómo construirlo**. Dominas el manejo de certificados TLS, redes de Capa 3 y automatización compleja con Ansible.

¡Tu repositorio con este diseño se verá espectacular! ¿Hay algo más que quieras ajustar o ya estás listo para publicarlo?
