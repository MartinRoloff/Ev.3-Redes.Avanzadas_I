# Evaluación 3 - Redes Avanzadas I: Despliegue CI/CD de Infraestructura Segura

**Institución:** INACAP, Sede Temuco  
**Carrera:** Ingeniería en Telecomunicaciones, Conectividad y Redes  
**Autor:** Martín Roloff  

---

## Descripción del Proyecto
Este proyecto demuestra la implementación de un pipeline de Integración y Entrega Continua (CI/CD) para la automatización de infraestructuras de red. Utilizando principios de **Infraestructura como Código (IaC)**, el repositorio despliega de forma totalmente desatendida una topología de red dinámica y segura sobre equipos Cisco.

El objetivo principal de esta fase es automatizar el enrutamiento y proteger las comunicaciones mediante la creación de túneles VPN, validando que el flujo de trabajo sea capaz de inyectar configuraciones reales sin intervención manual en la terminal de los equipos.

## Topología y Tecnologías Utilizadas

* **Entorno de Simulación:** GNS3
* **Servidor de Automatización (Runner):** Rocky Linux (Configurado como *Self-Hosted Runner* mediante servicio de sistema `systemd`).
* **Orquestador CI/CD:** GitHub Actions
* **Motor de Configuración:** Ansible
* **Protocolos Desplegados:**
    * **Enrutamiento Dinámico:** OSPF (Intercambio de rutas automático).
    * **Seguridad:** IPsec (Fase 1 ISAKMP y Fase 2 IPsec).
    * **Encapsulación:** Túneles GRE (Protocolo 47) para permitir enrutamiento dinámico sobre VPN.

## Estructura del Repositorio

* `.github/workflows/pipeline.yml`: Archivo maestro de GitHub Actions que define los *jobs* y pasos del despliegue automatizado.
* `inventory/hosts.ini`: Inventario de Ansible con las direcciones IP de gestión de los routers R1, R2 y R3.
* `playbooks/`: Contiene los archivos YAML de Ansible encargados de inyectar el direccionamiento IP, declarar las redes en OSPF y levantar la criptografía de IPsec.

## Flujo de Ejecución (Pipeline)

El despliegue está diseñado para operar en piloto automático. El flujo de trabajo se activa ante cualquier cambio en el repositorio (`push`) o mediante ejecución manual:
1.  **GitHub Actions** recibe la orden de despliegue.
2.  El trabajo es capturado por el **Self-Hosted Runner (Rocky Linux)** en la red local.
3.  El Runner ejecuta los *playbooks* de **Ansible**.
4.  Ansible establece conexión SSH con los routers en **GNS3** e inyecta la configuración de interfaces, OSPF e IPsec.

## Evidencias de Éxito (Fase 2)

A continuación, se presentan las pruebas técnicas de la correcta operación de la red tras el despliegue automatizado:

### 1. Enrutamiento OSPF y Adyacencias
Los routers alcanzan el estado `FULL` y aprenden las redes remotas automáticamente.
**<img width="723" height="112" alt="image" src="https://github.com/user-attachments/assets/f4d899dd-395a-43f1-9ef9-6c99e523edfb" />
**
<img width="727" height="346" alt="image" src="https://github.com/user-attachments/assets/8ab5b53d-fdf9-44fb-9714-80fd0a8bed4b" />

### 🎥 Demostración en Video
En el siguiente enlace se encuentra el recorrido completo por la topología y la comprobación de tráfico encriptado en tiempo real:
> **[Enlace al video de YouTube / Google Drive aquí]**
