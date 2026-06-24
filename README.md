# 🔐 Lab 01 — IPSec IKEv1 — Policy-Based (Crypto Map)

**Estudiante:** Enmanuel Feliz Soto | **Matrícula:** 2025-1402  
**Institución:** Instituto Tecnológico de Las Américas (ITLA)  
**Curso:** Seguridad en Redes | **Sección:** 2-1C  
**Docente:** Jonathan Esteban Rondón Corniel

---

## 📋 Descripción

VPN clásica basada en políticas. El tráfico interesante se define mediante ACL extendida. Usa Crypto Map aplicado en la interfaz WAN.

| Campo | Valor |
|-------|-------|
| **Tipo de VPN** | Site-to-Site |
| **Protocolo** | IKEv1 + IPSec ESP-AES256-SHA256 |
| **Mecanismo** | Crypto Map + ACL Criptográfica |
| **Routing** | Estático + ACL de tráfico interesante |
| **Pre-shared Key** | `Cisco2025-1402!` |

---

## 🗺️ Topología

> 📸 <img width="1472" height="805" alt="Captura de pantalla 2026-06-21 154657" src="https://github.com/user-attachments/assets/d07a1fce-12df-45c7-a935-b2c16b19a5e8" />



<!-- Coloca aquí el screenshot de PNetLab con la topología del Lab 01 -->

**Entorno:** PNetLab — Cisco IOL  
**Peers:** R1-S1 (20.25.1.2) ↔ R4-S2 (20.25.1.6)

### Tabla de Direccionamiento

| Router | Rol | IP WAN | Interfaz WAN | IP LAN | Interfaz LAN |
|--------|-----|--------|--------------|--------|--------------|
| R1-S1 | Peer 1 / Iniciador | 20.25.1.2 | Ethernet0/0 | 10.14.10.0.1/24 | **Ethernet0/3** |
| R4-S2 | Peer 2 / Respondedor | 20.25.1.6 | Ethernet0/1 | 10.14.20.0.1/24 | Ethernet0/0 |

### ISP

| Interfaz ISP | IP | Descripción |
|-------------|-----|-------------|
| Ethernet0/0 | 20.25.1.1/30 | Link to R1-S1 |
| Ethernet0/1 | 20.25.1.5/30 | Link to R4-S2 |







---

## ⚙️ Configuración

El script completo de configuración se encuentra en:  
📄 [`EnmanuelFelizSoto_2025-1402_IPSec_IKEv1_PolicyBased_P3.txt`](./EnmanuelFelizSoto_2025-1402_IPSec_IKEv1_PolicyBased_P3.txt)

### Parámetros IKE/IPSec

| Parámetro | Valor |
|-----------|-------|
| Encryption | AES-256 |
| Hash/Integrity | SHA-256 |
| DH Group | 14 (2048-bit) |
| SA Lifetime (IKE) | 86400 s (24h) |
| SA Lifetime (IPSec) | 3600 s (1h) |
| PFS | Group 14 |
| Auth Method | Pre-Shared Key |

---

## ▶️ Procedimiento de Ejecución

### 1. Cargar configuración en PNetLab
```
# Aplicar configuración en cada dispositivo en el orden:
# 1. ISP → 2. R1-S1 → 3. R4-S2 → 4. R2/Server
```

### 2. Verificar la VPN

```
show crypto ipsec sa
```
```
show crypto isakmp sa
```

### 3. Prueba de conectividad
```
ping 10.14.20.10 source 10.14.10.2
```

---

## 📸 Capturas de Verificación

> 📸 <img width="1571" height="1001" alt="image" src="https://github.com/user-attachments/assets/9fd2891b-b8b6-4f4b-92cc-ea0bba6504e5" />


<!-- Captura mostrando el estado QM_IDLE / ESTABLISHED -->

> 📸 <img width="2004" height="785" alt="image" src="https://github.com/user-attachments/assets/cb3c4ce6-0641-48e5-803a-a661de1ab77e" />


<!-- Captura mostrando pkts encaps/decaps incrementando -->

> 📸 <img width="1397" height="1126" alt="image" src="https://github.com/user-attachments/assets/4edc6e1e-450c-4ae8-9f10-a0b6620e2700" />


<!-- Captura del ping source 10.14.10.0/24 -->

---

## 🔍 Análisis y Comparativa

### Ventajas de este tipo de VPN
- Ver documentación técnica en el informe PDF

### Diferencias con otros labs
- Ver tabla comparativa en el README principal

---

## 📎 Recursos

| Recurso | Enlace |
|---------|--------|
| Repositorio Principal | [Enmafs/NetSec](https://github.com/Enmafs/NetSec) |
| Script de configuración | [`EnmanuelFelizSoto_2025-1402_IPSec_IKEv1_PolicyBased_P3.txt`](./EnmanuelFelizSoto_2025-1402_IPSec_IKEv1_PolicyBased_P3.txt) |
| Video demostración | 🎬 [Aquí](https://youtu.be/_ZKK-srNnZU) |

---

> ⚠️ *Laboratorio realizado en entorno controlado (PNetLab). Fines exclusivamente académicos.*
