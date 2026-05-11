<img width="800" height="650" alt="gemini-svg" src="https://github.com/user-attachments/assets/9c3c1ae0-328e-4aba-ab76-3a5cfd0dc82a" /># ☸️ Cluster Builder: Kubernetes Industrial con Kubespray

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
![Uploading g<svg width="800" height="650" viewBox="0 0 800 650" xmlns="http://www.w3.org/2000/svg">
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Urbanist:wght@600;700&amp;display=swap');
    text { font-family: 'Urbanist', sans-serif; fill: white; text-anchor: middle; }
    .node { fill: #0f172a; stroke: #38bdf8; stroke-width: 2; rx: 12; }
    
    /* Deployer / Ansible Diamond - Más ancho para que quepa el texto */
    .deployer-bg { fill: #1e293b; stroke: #fbbf24; stroke-width: 3; filter: drop-shadow(0 0 10px rgba(251, 191, 36, 0.2)); }
    .ansible-pulse { fill: none; stroke: #fbbf24; stroke-width: 2; }
    
    /* Animación Ansible */
    @keyframes pulse-ring {
      0% { r: 10; opacity: 1; stroke-width: 4; }
      100% { r: 70; opacity: 0; stroke-width: 1; }
    }
    .pulse-effect { animation: pulse-ring 2.5s cubic-bezier(0.21, 0.61, 0.35, 1) infinite; }

    /* Líneas SSH (Rojo) */
    .ssh-line { stroke: #ef4444; stroke-width: 2; stroke-dasharray: 10 6; fill: none; opacity: 0.8; }
    @keyframes flow-ssh { to { stroke-dashoffset: -32; } }
    .ssh-anim { animation: flow-ssh 0.8s linear infinite; }

    /* Calico Flow (Verde) */
    .calico-line { stroke: #22c55e; stroke-width: 3; fill: none; opacity: 0.3; }
    .packet { fill: #4ade80; filter: drop-shadow(0 0 4px #4ade80); }

    /* Kubernetes Border Breathing */
    .k8s-border { 
      fill: none; stroke: #0ea5e9; stroke-width: 2.5; opacity: 0.4;
      animation: breathe 4s ease-in-out infinite;
    }
    @keyframes breathe {
      0%, 100% { opacity: 0.2; stroke-width: 2.5; }
      50% { opacity: 0.6; stroke-width: 4.5; }
    }
  </style>

  <rect width="800" height="650" fill="#020617" />

  <rect x="50" y="220" width="700" height="380" class="k8s-border" rx="30" />
  <text x="400" y="255" font-size="16" font-weight="700" opacity="0.4" letter-spacing="6">KUBERNETES INFRASTRUCTURE</text>

  <path d="M400 130 L400 300" class="ssh-line ssh-anim" />
  <path d="M400 130 L180 460" class="ssh-line ssh-anim" />
  <path d="M400 130 L620 460" class="ssh-line ssh-anim" />

  <path id="c1" d="M400 330 L180 460" class="calico-line" />
  <path id="c2" d="M400 330 L620 460" class="calico-line" />
  <path id="c3" d="M180 495 L620 495" class="calico-line" />

  <circle r="5" class="packet"><animateMotion dur="3s" repeatCount="indefinite" path="M400 330 L180 460" /></circle>
  <circle r="5" class="packet"><animateMotion dur="3s" begin="1.5s" repeatCount="indefinite" path="M180 495 L620 495" /></circle>
  <circle r="5" class="packet"><animateMotion dur="3s" begin="0.7s" repeatCount="indefinite" path="M620 460 L400 330" /></circle>

  <g transform="translate(400, 90)">
    <circle r="10" class="ansible-pulse pulse-effect" />
    <circle r="20" class="ansible-pulse pulse-effect" style="animation-delay: 0.8s" />
    <path d="M0 -75 L100 0 L0 75 L-100 0 Z" class="deployer-bg" />
    <text y="-15" font-size="14" fill="#fbbf24" font-weight="bold" letter-spacing="2">KUBESPRAY</text>
    <text y="12" font-size="22" font-weight="bold">ANSIBLE</text>
    <text y="35" font-size="10" opacity="0.6" letter-spacing="1">DEPLOYER NODE</text>
  </g>

  <g transform="translate(310, 300)">
    <rect width="180" height="75" class="node" />
    <text x="90" y="32" font-weight="bold" font-size="16">MASTER</text>
    <text x="90" y="55" font-size="12" opacity="0.7">10.0.0.10</text>
  </g>

  <g transform="translate(90, 460)">
    <rect width="180" height="85" class="node" />
    <text x="90" y="35" font-weight="bold" font-size="16">WORKER 1</text>
    <text x="90" y="60" font-size="12" opacity="0.7">10.0.0.11</text>
  </g>

  <g transform="translate(530, 460)">
    <rect width="180" height="85" class="node" />
    <text x="90" y="35" font-weight="bold" font-size="16">WORKER 2</text>
    <text x="90" y="60" font-size="12" opacity="0.7">10.0.0.12</text>
  </g>
</svg>
emini-svg.svg…]()
