# AEE.-Bit-cora-III.-UD06y7T04-Conexiones-Empresariales.

# Operación Escudo: Fundamentos de Seguridad y Auditoría

Este repositorio contiene la investigación y documentación técnica correspondiente a la **Fase de Investigación: Comprendiendo el corazón del sistema**, desarrollada para la asignatura de Sistemas Informáticos.

**Estudiante:** José Luis Segura Fernández  
**Asignatura:** Sistemas Informáticos  
**Profesor:** Willman Acosta  
**Fecha:** 17 de abril de 2026

---

## 📋 Índice
1. [Anatomía de Syslog y Clasificación](#1-anatomía-de-syslog-y-clasificación)
2. [Seguridad en el Registro de Autenticación](#2-seguridad-en-el-registro-de-autenticación)
3. [Diferenciación de Intentos de Acceso (SSH vs Local)](#3-diferenciación-de-intentos-de-acceso-ssh-vs-local)
4. [Log Management y Cumplimiento Legal (RGPD)](#4-log-management-y-cumplimiento-legal-rgpd)
5. [Referencias](#5-referencias)

---

## 1. Anatomía de Syslog y Clasificación
Syslog es el estándar en sistemas Linux para la gestión y clasificación de eventos de registro. [cite_start]El sistema organiza cada mensaje mediante un valor numérico de **prioridad (PRI)**, el cual se obtiene cruzando la **Facilidad** (el origen del mensaje) y la **Severidad**.

De acuerdo con el estándar, la severidad se clasifica en 8 niveles críticos:

| Nivel | Severidad | Descripción |
| :---: | :--- | :--- |
| **0** | Emergency | El sistema no se puede usar. |
| **1** | Alert | Se necesita acción inmediata del usuario. |
| **2** | Critical | Condiciones críticas del sistema. |
| **3** | Error | Condiciones de error en procesos. |
| **4** | Warning | Advertencias preventivas. |
| **5** | Notice | Evento normal pero significativo. |
| **6** | Informational | Mensajes meramente informativos. |
| **7** | Debug | Mensajes detallados para depuración. |

---

## 2. Seguridad en el Registro de Autenticación
La configuración de permisos en el archivo `/var/log/auth.log` es un pilar crítico de la seguridad. Se considera una **negligencia grave** permitir permisos de lectura a usuarios no privilegiados debido a:

* **Exposición de Información Sensible:** El archivo contiene nombres de usuarios válidos, intentos de inicio de sesión, direcciones IP y actividad detallada del comando `sudo`.
* **Enumeración de Usuarios:** Un atacante local podría identificar qué cuentas existen en el sistema para dirigir ataques de fuerza bruta dirigidos.

---

## 3. Diferenciación de Intentos de Acceso (SSH vs Local)
Es fundamental distinguir el origen de un fallo de autenticación para determinar si la amenaza es externa o física:

### A. Conexión Remota (SSH)
* **Proceso:** Identificado bajo el demonio `sshd`. Cada conexión genera un subproceso con un **PID único**.
* **Identificador de Red:** Siempre incluye la **IP de origen** y el puerto remoto. 
* *Ejemplo de log:* `from 192.168.1.45 port 54321 ssh2`.

### B. Acceso Local
* **Proceso:** Identificado por procesos de sistema como `login`, o gestores de entorno gráfico como `gdm` o `lightdm`.
* **Identificador Físico:** Al no existir una dirección IP, el registro muestra el identificador de la **TTY** o terminal física.
* *Ejemplo de log:* `on tty1` o `on /dev/tty2`.

---

## 4. Log Management y Cumplimiento Legal (RGPD)
La gestión centralizada transforma los registros de simples archivos de texto en **evidencia digital íntegra**.

### Ventajas de Seguridad
* **Custodia Externa:** Al enviar logs en tiempo real a un servidor externo, un atacante que comprometa la máquina local pierde el control sobre la evidencia, impidiendo que borre sus huellas.
* **Correlación de Eventos:** Facilita la detección de ataques distribuidos; si múltiples servidores reportan fallos desde una misma IP simultáneamente, se dispara una alerta global.

### Cumplimiento Legal (RGPD)
El Reglamento General de Protección de Datos (RGPD) exige a las empresas demostrar la trazabilidad de los datos personales (quién accedió, cuándo y desde dónde). La centralización de logs asegura que estos registros sean inalterables y estén disponibles para auditorías legales en cumplimiento con la normativa española vigente.

---

## 5. Referencias
* [1] J. L. Segura Fernández, *Bitácora III. Conexiones Empresariales: Taller Técnico Operación Escudo*, Sevilla, 2026[cite: 1, 2, 5].
* [2] R. Gerardi, *Hands-on System Programming con Go*, Packt Publishing, 2019 (Ref. conceptual sobre estándares Syslog y RFC 5424).
