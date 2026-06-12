# Laboratorio: VLAN Trunking Protocol (VTP) Attack 💥

**Instituto Tecnológico de Las Américas (ITLA)**
* **Materia:** Seguridad de Redes
* **Profesor:** Jonathan Rondón
* **Estudiante:** Anthony De Los Santos
* **Matrícula:** 2025-1335

---

## 🎥 Video Demostrativo
▶️ **Enlace a YouTube:** https://youtu.be/jW5YTvA7--4 

*(El video incluye demostración con cámara, voz, fecha/hora, topología y comprobación de la herramienta).*

---

## 📄 Documentación Técnica

### Objetivo del Laboratorio
Demostrar de forma práctica la explotación y mitigación de vulnerabilidades en protocolos de Capa 2 (VTP) dentro de un entorno virtualizado, evidenciando el impacto de configuraciones por defecto.

### Objetivo de la Herramienta (Yersinia)
Inyectar paquetes VTP manipulados en la red con un número de revisión superior al actual del dominio VTP. El objetivo es forzar a los switches a actualizar su base de datos de VLANs, permitiendo agregar nuevas VLANs o borrar las existentes, provocando una denegación de servicio (DoS) a nivel de capa 2.

### Requisitos para utilizar la herramienta
* Entorno virtualizado (PNETLab / Proxmox).
* Sistema operativo Linux (ej. Pop!_OS / Ubuntu) con entorno gráfico.
* Herramienta `yersinia` instalada (`sudo apt install yersinia`).
* Conexión a un puerto del switch.

### Documentación del Funcionamiento
1. Se ejecuta Yersinia en modo gráfico mediante el comando `yersinia -G` con privilegios de superusuario.
2. Se selecciona la interfaz de red conectada al switch.
3. Se identifica el dominio VTP activo capturado en el tráfico (`LAB_SEGURIDAD`).
4. Se ejecuta el ataque "Adding one VLAN" definiendo el ID y el nombre, o inyectando un Subset Advertisement vacío para el borrado.
5. Yersinia falsifica el paquete incrementando exponencialmente el número de revisión, sobrescribiendo la base de datos `vlan.dat` de la red.

### Topología y Direccionamiento
* **VLAN 35 (Gestión):** `10.25.35.0/24` (Aislada).
* **VLAN 133 (Usuarios/Atacante):** `10.25.133.0/24` (IP Atacante: 10.25.133.12).
* **VLAN 999:** Blackhole / Nativa.

*(Ver documento PDF adjunto en este repositorio para capturas de pantalla de la topología y evidencia de ejecución).*

### Contramedidas (Mitigación)
* **VTP Password:** Configurar una contraseña robusta en el dominio VTP (`vtp password [clave]`).
* **VTP Transparent Mode:** Configurar los switches en modo transparente (`vtp mode transparent`) u `off` si no es necesaria la sincronización dinámica.
* **VTP Version 3:** Utilizar VTPv3 para habilitar autenticación criptográfica mejorada.