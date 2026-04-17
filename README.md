# AEE.-Bit-cora-III.-UD06y7T04-Conexiones-Empresariales.
Misión 1: Reto de investigación
Anatomia de Syslog y clasificación
Syslog es el sistema estándar en Linux para gestionar y clasificar eventos de registro (logs). Organiza cada mensaje utilizando un valor numérico de prioridad (PRI) calculado al cruzar la Facilidad, que significa que parte del sistema es generado por el log

El estándar de la prioridad antes mencionada se define en 8 niveles:

0-Emergency: El sistema no se puede usar
1-Alert: Se necesita accion inmediata del usuario
2-Critical: Condiciones críticas
3-Error: Condiciones de error
4-Warning: Son las advertencias
5-Notice: Algo normal pero significativo
6-Informational: Mensajes meramente informativos
7-Debug: Mensajes de depuracion
¿Por qué es una negligencia grave que el archivo /var/log/auth.log tenga permisos de lectura para usuarios no privilegiados?
Es una negligencia grave porque expone información sensible sobre la seguridad del sistema, incluyendo nombres de usuario, intentos de inicio de sesión fallidos, direcciones IP y actividad de sudo.
¿Qué información específica (como PIDs, nombres de usuario o direcciones IP) diferencia un intento fallido de conexión remota SSH de un simple fallo de contraseña de un usuario local frente a la pantalla?
La diferencia es que primero cada conexión entrante en SSH genera un subproceso con un PID único y que en local se verán procesos como login o gdm o lightdm si es entorno gráfico. En SSH siempre aparece la IP de origen y puerto desde el que se intenta la conexión  algo como “from 192.168.1.45 port 54321 ssh2 y en local como no hay direccion ip aparece el identificador de la TTY o terminal física (on tty1 o on /dev/tty2



Log Management, Seguridad y Cumplimiento Legal
	
La gestión centralizada de los registros resumidamente transforma los logs de simples archivos de texto en evidencia digital íntegra.
Ventajas de Seguridad
Custodia Externa: Al enviar logs en tiempo real a un servidor externo seguro, el atacante pierde el control sobre la evidencia. 
Correlación de Eventos: Permite detectar ataques distribuidos. Si diez servidores distintos reportan fallos de autenticación desde la misma IP externa al mismo tiempo, el sistema centralizado disparará una alerta global que un servidor aislado nunca detectará
Cumplimiento Legal (RGPD)
Este es el reglamento general de protección de datos, exige que las empresas demuestren quién, cuándo y desde donde se accedió a datos personales.
	
