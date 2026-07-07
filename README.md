# Proyecto: Despliegue de VPN IpSec y Túneles GRE Full-Mesh con Ansible

## Descripción
Este proyecto automatiza la configuración de una topología de red segura (VPN IPSec y túneles GRE Full-Mesh) sobre tres routers Cisco (R1, R2 y R3) utilizando Ansible.

## Estructura del Proyecto
El código está estructurado bajo las mejores prácticas, utilizando **Roles de Ansible** para garantizar la modularidad y escalabilidad:
- `master.yml`: Playbook principal que invoca el rol.
- `inventory/hosts.ini`: Inventario con los datos de conexión de los routers.
- `roles/vpn_router/`: Rol que contiene las tareas de configuración.
- `group_vars/all.yml`: Archivo cifrado con Ansible Vault que protege la contraseña (PSK) de la VPN.

## Requisitos Cumplidos (Fase 1)
1. **Seguridad:** Uso de `ansible-vault` para proteger datos sensibles (ISAKMP Key).
2. **Modularidad:** Implementación de la estructura mediante Roles.
3. **Eficiencia:** Uso de diccionarios y bucles (`loop`) para iterar la creación de los túneles GRE dependiendo del router (`inventory_hostname`).
4. **Resiliencia:** Implementación de manejo de errores (`block`, `rescue`) para evitar caídas abruptas del despliegue.

## Instrucciones de Ejecución
Para desplegar esta configuración, ejecute el siguiente comando en la terminal:

`ansible-playbook -i inventory/hosts.ini master.yml --ask-vault-pass`

*(Se le solicitará la contraseña de la bóveda para desencriptar la clave IPSec).*
