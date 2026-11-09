# Levantamiento de Requerimientos - Nómina Fácil

## 1. Visión general

Este proyecto busca desarrollar una plataforma para pequeñas y medianas empresas (PYMEs) que permita gestionar remuneraciones, cotizaciones previsionales, licencias médicas y cuentas bancarias de los trabajadores, además de ofrecer un portal seguro para que cada empleado consulte su información laboral y financiera.

La solución debe desarrollarse con Node.js como backend y React + TypeScript como frontend, integrados mediante API REST/JSON, con Tailwind CSS para el diseño de interfaces, ORM para persistencia y despliegue con Docker.

## 2. Objetivo del sistema

### Objetivo general
Crear un sistema de gestión de nómina y portal del trabajador que permita:
- registrar y realizar sueldos
- gestionar cotizaciones previsionales
- controlar licencias médicas
- administrar cuentas bancarias para pagos
- ofrecer acceso seguro a la información del trabajador
- cumplir con la normativa laboral y de protección de datos
- Gestionar Permisos
- gestionar Atrasos
- gestionar Contrataciones
- gestionar finiquitos
- registro de entrada y salida laboral
- gestion de vacaciones
- gestion de horas extra

### Objetivos específicos
- automatizar procesos de remuneración
- reducir errores manuales en la liquidación
- Automatizar procesos de contratacion y finiquitos
- Automatizar procesos de calculos de ingresos y egresos 
- mantener historial de pagos y cambios
- permitir consulta de información a trabajadores con acceso controlado
- asegurar confidencialidad, integridad y disponibilidad de los datos

## 3. Proceso DevOps y DevSecOps del equipo
Enfoque DevOps y DevSecOps

El proyecto Nómina Fácil adoptará un enfoque DevOps y DevSecOps con el propósito de integrar el desarrollo, las pruebas, la seguridad y las operaciones durante todo el ciclo de vida de la aplicación.

El enfoque DevSecOps resulta especialmente relevante para Nómina Fácil debido a que el sistema contempla información sensible de los trabajadores, incluyendo datos personales, remuneraciones, cotizaciones previsionales, información bancaria y documentación médica.

Como referencia para la planificación de seguridad se utilizarán principalmente:

-NIST Secure Software Development Framework (SSDF) SP 800-218, que establece prácticas de desarrollo seguro que pueden integrarse en diferentes modelos de ciclo de vida del software. Su objetivo incluye reducir vulnerabilidades en el software publicado y abordar sus causas para evitar recurrencias.
-OWASP Application Security Verification Standard (ASVS), que proporciona una base para definir y verificar controles técnicos de seguridad en aplicaciones web. OWASP ASVS contempla áreas como autenticación, sesiones, autorización, criptografía, comunicaciones, protección de datos, configuración y registro de eventos.
-ISO/IEC 27001, como referencia para la gestión de riesgos asociados a la seguridad de la información.

Para integrar ambos enfoques, el equipo considerará seguridad en las fases de planificación, programación, construcción, pruebas, publicación, despliegue, operación y monitorización.
### 3.1Planificar

Durante la fase de planificación se definirán los requerimientos funcionales, no funcionales y de seguridad de Nómina Fácil, además de los usuarios, roles, arquitectura y riesgos relevantes del sistema.

Debido a que la aplicación gestionará información salarial, bancaria, previsional y médica, el equipo efectuará un análisis de amenazas sobre los componentes que gestionen estos datos.

- Prácticas de seguridad planificadas
- Identificación de activos sensibles.
- Clasificación de información.
- Definición de requisitos de seguridad.
- Aplicación del principio de mínimo privilegio.
- Modelado de amenazas mediante STRIDE.
- Análisis de riesgos.
- Incorporación de tareas de seguridad al backlog.

Estándares de referencia: NIST SSDF, OWASP ASVS e ISO/IEC 27001.

Evidencias previstas:

- matriz STRIDE;
- requisitos de seguridad;
- backlog en Azure Boards;
- diagrama de arquitectura;
- matriz de riesgos.

El NIST SSDF establece que las prácticas de desarrollo seguro deben incorporarse al ciclo de vida del software, en lugar de tratar la seguridad como una actividad separada.

### 3.2 Programar

Durante la fase de programación se desarrollarán las funcionalidades de frontend y backend definidas para Nómina Fácil.

Según el diseño tecnológico planteado actualmente, se contempla React con TypeScript para frontend, Node.js para backend y una API REST/JSON para la comunicación entre componentes.

Cada funcionalidad será desarrollada procurando aplicar controles de seguridad desde el código.

Prácticas de seguridad planificadas
- Validación de datos recibidos por el backend.
- Control de autorización.
- Protección de rutas sensibles.
- Manejo seguro de errores.
- Evitar contraseñas, tokens o claves directamente en el código.
- Uso de variables de entorno para configuración sensible.
- Revisión del código mediante Pull Request antes de su integración.

Referencia: OWASP ASVS y NIST SSDF.

OWASP ASVS incluye categorías específicas relacionadas con validación, autenticación, gestión de sesiones, autorización, servicios web, criptografía, comunicaciones y protección de datos, todas relevantes para la aplicación.

Evidencias previstas:

- ramas de desarrollo;
- Pull Requests;
- revisiones de código;
- commits;
- pruebas asociadas.


### 3.3 Construir

En esta etapa los diferentes componentes del sistema serán preparados para generar una versión ejecutable y reproducible del software.

El proyecto contempla actualmente el uso de Docker para sus entornos, por lo que la construcción de la aplicación deberá considerar las dependencias necesarias para el frontend y backend sin incorporar información secreta dentro de los artefactos generados.

Prácticas de seguridad planificadas
Comprobación de dependencias utilizadas por el proyecto.
Control de versiones de dependencias.
Exclusión de archivos con credenciales.
Uso de .gitignore.
Gestión de secretos mediante variables de entorno.
Análisis de dependencias y componentes cuando se configure el pipeline.

Referencia: NIST SSDF y OWASP.

Evidencias previstas:

Dockerfile;
### 3.4 Probar

Las pruebas permitirán comprobar tanto las funcionalidades como los controles de seguridad implementados en Nómina Fácil.

El equipo contempla pruebas unitarias y de integración dentro de los requisitos actuales del proyecto.

Además, los requisitos de seguridad deberán disponer de alguna forma de comprobación.

Pruebas de seguridad previstas

Entre los escenarios que se pretende verificar se encuentran:

- Un trabajador no puede consultar información perteneciente a otro trabajador.
- Un trabajador no puede acceder a funciones destinadas exclusivamente a RR.HH.
- Una sesión cerrada no puede continuar utilizándose.
- Los datos introducidos en formularios son validados.
- Los errores no muestran información técnica o datos sensibles.
- Los cambios críticos quedan registrados cuando corresponda.
- Las credenciales y secretos no forman parte del código fuente.

Referencia: OWASP ASVS.

OWASP ASVS proporciona precisamente una base para probar los controles técnicos de seguridad utilizados para proteger aplicaciones web.

Evidencias previstas:

- resultados de pruebas;
- ejecución del pipeline;
- resultado de pruebas de autorización;
- capturas o registros de ejecución.
### 3.5 Publicar

Antes de considerar una versión como candidata para publicación, deberá verificarse que los controles y pruebas definidos para dicha versión hayan sido ejecutados satisfactoriamente.

Prácticas de seguridad planificadas
Verificar que las pruebas definidas se ejecuten correctamente.
Revisar las dependencias utilizadas.
Evitar credenciales en los artefactos.
Identificar claramente las versiones publicadas.
Mantener trazabilidad entre los cambios de código y los elementos de trabajo correspondientes.

Referencia: NIST SSDF.

Esta fase busca evitar que una nueva versión se considere preparada para despliegue sin haber pasado previamente por los controles acordados por el equipo.

Evidencias previstas:

- resultado satisfactorio del pipeline;
- Pull Request aprobado;
- registro de versión;
- artefacto o imagen resultante, cuando corresponda.

  
### 3.6 Desplegar

En la etapa de despliegue se instalará la versión validada de Nómina Fácil en el entorno definido por el equipo.

En vuestro documento existe actualmente una propuesta que contempla Docker, Supabase y Vercel. Antes de la entrega final deberá definirse claramente qué componente será desplegado en cada plataforma.

Prácticas de seguridad planificadas
Separación entre código y secretos.
Variables de entorno para configuración sensible.
Uso de comunicaciones protegidas en entornos publicados.
Configuración segura del entorno.
Restricción de accesos administrativos.
Evitar credenciales directamente en imágenes de contenedor o repositorios.

Referencias: OWASP ASVS y NIST SSDF.

Evidencias previstas:

configuración del entorno;
variables configuradas de manera segura;
Dockerfile;
ejecución del despliegue;
comprobación de la aplicación desplegada. 

### 3.7 Operar

Durante la operación se buscará mantener el sistema disponible y proteger los datos gestionados por Nómina Fácil.

Esta fase adquiere especial importancia debido a que el sistema contempla datos personales, salariales, financieros y médicos.

Prácticas de seguridad planificadas
Control de acceso basado en roles.
Aplicación de mínimo privilegio.
Gestión y revocación de accesos.
Copias de seguridad.
Actualización de dependencias.
Gestión de incidentes.
Separación de funciones administrativas.

Referencias: ISO/IEC 27001 y OWASP ASVS.

Evidencias previstas:

configuración de roles;
procedimiento de respaldo;
procedimiento de recuperación;
registros de operación.

### 3.8 Monitorizar

La fase de monitorización permitirá detectar eventos importantes relacionados tanto con el funcionamiento como con la seguridad del sistema.

Nómina Fácil ya contempla dentro de sus requisitos actuales el registro de auditoría, trazabilidad, monitorización y registro de eventos.

Eventos previstos para monitorización
intentos de autenticación relevantes;
fallos de autorización;
modificaciones de información crítica;
cambios en información bancaria;
operaciones administrativas relevantes;
eventos de seguridad;
errores del sistema.

También deberá evitarse almacenar contraseñas, tokens u otros datos sensibles innecesarios en los registros.

OWASP indica que el registro de eventos de aplicación resulta útil para seguridad, auditoría, investigación de incidentes y monitorización, y señala además la necesidad de evitar determinados datos sensibles en los logs.

Evidencias previstas:

logs de aplicación;
registros de auditoría;
eventos de autenticación;
registros de modificaciones críticas.
- archivos de dependencias;
- gitignore;
- resultado del proceso de construcción;
- ejecución del workflow cuando se encuentre implementado.




## 4. Alcance funcional

### 4.1 Administración de empleados
- datos personales
- RUT y contacto
- cargo y contrato
- jornada laboral
- centro de costos
- cuenta bancaria asociada
- estado laboral

### 4.2 Gestión de remuneraciones
- sueldo base
- ingresos y salidas
- horas extra
- bonos
- descuentos
- asignaciones y beneficios
- descuentos previsionales
- liquidación de sueldos por periodo
- historial de pagos


### 4.3 Cotizaciones previsionales
- cotizaciones de salud
- cotizaciones AFP
- AFC
- impuesto de segunda categoria
- prestamos
- registro por periodo
- historial y conciliación

### 4.4 Licencias médicas
- registro de licencias médicas
- carga de certificados médicos
- cálculo de días de licencia
- validación por periodo
- vinculaciones con el área de RR.HH

### 4.5 Cuentas bancarias
- registro de cuenta de pago
- actualización de cuenta y validación
- historial de cambios
- control de autorizaciones

### 4.6 Portal del trabajador
- consulta de sueldos
- historial de liquidaciones
- acceso a cotizaciones previsionales
- consulta de licencias médicas
- estado de cuenta y datos bancarios
- descarga de comprobantes asociados
- tiempo en la empresa
- renuncia voluntaria
- denuncias

### 4.7 Administración y seguridad
- roles y permisos por perfil
- registro de auditoría
- trazabilidad de cambios
- control de sesiones
- gestión de accesos y revocación

## 5. Usuarios y roles

### 5.1 Administrador de RR.HH o Nómina
- gestiona empleados
- registra pagos y liquidaciones
- valida licencias
- configura parámetros de nómina
- valida ingreso y salida trabajador
- gestionar renuncias y despidos
- gestion de contratos

### 5.2 Administrador de empresa o gerencia
- revisa reportes
- administra cuentas
- administrar datos del negocio
- analiza indicadores de nómina
- aprueba cambios importantes

### 5.3 Trabajador
- consulta sus datos personales
- revisa su sueldo y liquidaciones
- revisa cotizaciones y licencias
- actualiza sus datos autorizados

### 5.4 Soporte / Seguridad / Auditoría
- revisa logs y eventos
- valida accesos y permisos
- gestiona incidentes de seguridad
- gestiona trazabilidades
  
## 6. Requisitos funcionales

### 6.1 Requisitos de negocio
- El sistema debe permitir realizar remuneraciones conforme a la normativa laboral vigentes.
- Debe registrar contratos, finiquitos, despidos, renuncias voluntarias.
- Debe registrar el horario de ingreso y salida del trabajador.
- Debe gestionar calculos de impuestos de segunda categoria.
- Debe gestionar descuentos de cajas de compensacion.
- Debe permitir administrar anticipos, horas extras, bonos, gratificaciones, asignaciones.
- Debe registrar cotizaciones previsionales, APV, salud, AFC asociadas al trabajador.
- Debe permitir administrar licencias médicas con soporte documental.
- Debe mantener una relación segura y trazable entre trabajador y cuenta bancaria de pago.
- El portal del trabajador debe mostrar información de forma limitada y segura.
- El administrador no puede acceder a informacion confidencial de licencias medicas.

### 6.2 Requisitos de información
- La información sensible debe clasificarse y protegerse.
- Los datos deben mantenerse auditables.
- Debe existir control de retención de información.
- Cada registro debe relacionarse con empresa, empleado y periodo.

### 6.3 Requisitos de usuario
- inicio de sesión seguro con MFA
- autenticación con credenciales robustas
- control de sesiones
- permisos por perfil
- recuperación de credenciales segura

### 6.4 Historias de usuario y criterios de aceptación

#### HU-01: Registro y mantenimiento de empleados
Como RR.HH, quiero registrar y actualizar los datos del trabajador, para mantener un historial laboral completo y confiable.

Criterios de aceptación:
- El sistema permite crear, consultar, actualizar y desactivar empleados.
- Se registran nombre, RUT, contacto, cargo, contrato, estado laboral y centro de costos.
- No se permite duplicar un RUT activo dentro del sistema.
- Cada cambio relevante queda registrado en auditoría.

#### HU-02: Liquidación de remuneraciones
Como RR.HH, quiero calcular y gestionar la liquidación de sueldo de cada trabajador, para asegurar pagos correctos y cumplir con la normativa laboral.

Criterios de aceptación:
- El sistema calcula sueldo base, bonos, horas extra, descuentos y cotizaciones asociadas.
- Cada liquidación queda asociada a un empleado y a un período específico.
- Se genera un historial de pagos y liquidaciones por trabajador.
- El cálculo exige validación de reglas de negocio y condiciones legales.

#### HU-03: Gestión de licencias médicas
Como RR.HH, quiero registrar licencias médicas y sus respaldos documentales, para controlar ausencias y validar permisos médicos.

Criterios de aceptación:
- Se permite registrar licencias con fecha de inicio, fin y tipo de licencia.
- Se admite carga de certificados y documentos médicos.
- El sistema calcula días de licencia y su estado.
- El acceso a los documentos médicos está restringido a perfiles autorizados.

#### HU-04: Administración de cuentas bancarias
Como RR.HH, quiero registrar y actualizar la cuenta de pago del trabajador, para garantizar que el abono se realice en la cuenta autorizada.

Criterios de aceptación:
- El trabajador puede tener una cuenta asociada activa.
- Todo cambio de cuenta genera historial y trazabilidad.
- La modificación requiere autorización según el flujo definido.
- No se puede cambiar la cuenta sin validación del proceso de negocio.

#### HU-05: Portal del trabajador
Como trabajador, quiero consultar mi información laboral y financiera de manera segura, para revisar mi nómina, licencias y cotizaciones sin riesgo de exposición indebida.

Criterios de aceptación:
- El trabajador puede acceder solo a su información personal y laboral.
- Puede consultar su sueldo, liquidaciones, cotizaciones y licencias.
- No puede visualizar información de otros empleados ni documentos de terceros.
- La sesión requiere autenticación vigente y permisos válidos.

#### HU-06: Control de roles y permisos
Como administrador, quiero definir roles y permisos por perfil, para limitar el acceso a la información sensible según la responsabilidad del usuario.

Criterios de aceptación:
- Existen roles como RR.HH, gerencia, trabajador, soporte y auditor.
- Cada operación crítica valida permisos en backend.
- Un usuario sin autorización no puede acceder a datos salariales, bancarios o médicos.
- Los cambios de permisos quedan registrados en auditoría.

#### HU-07: Auditoría y trazabilidad
Como soporte o auditor, quiero revisar accesos, cambios y eventos críticos, para detectar incidentes y mantener trazabilidad del sistema.

Criterios de aceptación:
- Se registran accesos, cambios de cuenta, modificaciones salariales y licencias.
- La auditoría incluye usuario, acción, módulo, entidad, fecha y datos relevantes.
- Los eventos críticos quedan disponibles para revisión y análisis.
- No se permite eliminar evidencia crítica sin control.

### 6.5 Requisitos no funcionales

#### RNF-01: Disponibilidad y continuidad
- El sistema debe operar con alta disponibilidad durante los procesos diarios de nómina y consultas del trabajador.
- Debe existir respaldo y recuperación ante fallos de infraestructura o datos.

#### RNF-02: Rendimiento
- Las consultas de nómina, reportes y portal del trabajador deben responder en tiempos aceptables para uso diario.
- El sistema debe soportar la carga esperada de empleados y transacciones sin degradación crítica.

#### RNF-03: Mantenibilidad
- El proyecto debe mantenerse modular y escalable, con separación clara entre frontend, backend y base de datos.
- La implementación debe seguir patrones de capas, servicios y repositorios.

#### RNF-04: Auditoría y trazabilidad
- Toda operación crítica debe quedar registrada con metadata suficiente para investigación y cumplimiento.
- La trazabilidad debe ser observable por RR.HH, soporte y auditoría.

#### RNF-05: Cumplimiento legal y de privacidad
- El sistema debe cumplir con la normativa laboral vigente y la Ley 21.719.
- Debe existir tratamiento mínimo indispensable, retención definida y control de acceso por necesidad de conocer.

#### RNF-06: Compatibilidad y despliegue
- La solución debe funcionar con React + TypeScript en frontend y Node.js + TypeScript en backend.
- Debe ser desplegable en entornos de desarrollo, staging y producción con configuración segura.

### 6.6 Requisitos de seguridad

#### RSEG-01: Autenticación segura
- El sistema debe exigir autenticación robusta con credenciales válidas.
- Los perfiles sensibles deben requerir MFA.
- Las sesiones deben expirar y reutilizarse con políticas de seguridad definidas.

#### RSEG-02: Autorización por rol y mínimo privilegio
- El acceso a información salarial, médica o bancaria debe validarse por backend.
- El principio de mínimo privilegio debe aplicarse en usuarios, roles y permisos.
- Un trabajador no puede acceder a información de otros empleados.

#### RSEG-03: Protección de datos sensibles
- Los datos salariales, bancarios, previsionales y médicos deben protegerse con cifrado en tránsito y en reposo.
- Los archivos adjuntos sensibles deben almacenarse de forma segura.
- Los registros de auditoría no deben exponer secretos ni información confidencial.

#### RSEG-04: Prevención de vulnerabilidades comunes
- El sistema debe protegerse contra SQL Injection, XSS, CSRF, IDOR y exposición de secretos.
- Se debe validar la entrada de datos en backend y controlar los errores para no revelar información técnica.
- Las dependencias deben mantenerse actualizadas y revisadas.

#### RSEG-05: Auditoría y monitoreo
- El sistema debe registrar intentos fallidos de autenticación, cambios de permisos, accesos sensibles y modificaciones críticas.
- Los eventos de seguridad deben ser revisables por auditoría y soporte.
- Se deben activar alertas para actividades sospechosas o accesos no autorizados.

#### RSEG-06: Seguridad de despliegue
- No se deben registrar credenciales ni secretos en repositorios ni logs.
- Las variables de entorno deben manejarse a través de un mecanismo seguro.
- El despliegue debe ejecutarse sobre conexiones HTTPS/TLS con configuración segura.

## 7. Requisitos legales y normativos

### 7.1 Código del Trabajo
El sistema debe contemplar, al menos, lo siguiente:
- liquidación de remuneraciones
- pagos de sueldo conforme a la legislación
- licencias médicas y permisos
- horas extra y remuneraciones legales
- descuentos legales
- registro de contratos y condiciones laborales
- respaldo documental y auditoría

### 7.2 Ley 21.719
La plataforma debe cumplir los principios de protección de datos personales, especialmente:
- finalidad específica y legítima del tratamiento
- minimización de datos
- limitación de acceso
- seguridad adecuada
- consentimiento según corresponda
- derechos de los titulares sobre su información
- notificación de incidentes frente a la autoridad correspondiente
- tratamiento responsable de datos sensibles

### 7.3 Requisitos de privacidad y seguridad
- política de privacidad accesible
- consentimiento claro para tratamiento de datos
- registro de tratamiento de datos
- manejo seguro de documentos médicos y financieros
- control de accesos por perfil y necesidad de conocer

## 8. Requisitos de seguridad según ISO 27002

### 8.1 Control de acceso
- asignación de roles y permisos
- mínimo privilegio
- revisión periódica de accesos
- autenticación multifactor para accesos sensibles
- revocación de accesos ante cambios de personal

### 8.2 Seguridad de activos
- clasificación de datos por sensibilidad
- cifrado en tránsito y en reposo
- manejo seguro de secretos y variables de entorno
- copias de seguridad cifradas

### 8.3 Criptografía
- TLS para conexiones web
- hash seguro para contraseñas
- protección de archivos sensibles
- gestión segura de claves y certificados

### 8.4 Seguridad operativa
- monitorización y registro de eventos
- alertas por actividad anómala
- actualizaciones periódicas de dependencias
- gestión de parches y revisión de vulnerabilidades

### 8.5 Auditoría y trazabilidad
- registro de accesos e interacciones sensibles
- historial de cambios en nómina y cuentas bancarias
- bitácora de actividad por usuario y módulo

### 8.6 Gestión de terceros
- evaluación de proveedores de infraestructura y servicios
- políticas de seguridad para integración con terceros
- cubrimiento contractual en tratamiento de datos

## 9. Requisitos según ISO 27005

La ISO 27005 guía la gestión de riesgos. El proyecto debe incluir:
- identificación de activos críticos
- evaluación de amenazas y vulnerabilidades
- valoración de impacto y probabilidad
- tratamiento del riesgo
- seguimiento y revisión continua

### 9.1 Activos críticos
- base de datos de trabajadores
- liquidaciones y remuneraciones
- información previsional y de salud
- cuentas bancarias
- documentos médicos
- registros de auditoría
- infraestructura de despliegue

### 9.2 Riesgos principales
- filtración de datos salariales
- acceso no autorizado a información personal
- manipulación de nómina o pagos
- cambio fraudulento de cuenta bancaria
- ataques a autenticación y sesiones
- fallos en disponibilidad o servicio

### 9.3 Tratamiento del riesgo
- mitigación por control técnico y organizacional
- separación de funciones
- políticas de acceso
- auditoría continua
- planes de recuperación y continuidad

## 10. Vulnerabilidades comunes en este tipo de sistemas

### 10.1 SQL Injection
Manipulación de consultas para acceder o modificar información de nómina o trabajadores.

### 10.2 XSS (Cross-Site Scripting)
Ejecutar scripts maliciosos en el portal del trabajador o módulo administrativo.

### 10.3 IDOR / Broken Access Control
Acceso a sueldo, licencias o datos bancarios de otros empleados.

### 10.4 Fuga de información sensible
Exposición de datos de salud, remuneración o cuentas bancarias.

### 10.5 Autenticación débil
Contraseñas frágiles, sesiones reutilizadas o falta de MFA.

### 10.6 CSRF
Solicitudes no autorizadas que alteran pagos o ajustes en datos.

### 10.7 Exposición de secretos
Credenciales, claves y tokens en archivos de configuración o logs.

### 10.8 Falta de auditoría
No se registran cambios críticos ni accesos a información sensible.

### 10.9 Dependencias vulnerables
Bibliotecas con fallas conocidas y actualizaciones pendientes.

## 11. Análisis de vulnerabilidades del caso

### Riesgos críticos del negocio
- filtración de sueldos y remuneraciones
- acceso a datos médicos sin autorización
- desvío de pagos por modificación de cuentas bancarias
- manipulación de liquidaciones de nómina
- exposición de información a terceros no autorizados

### Severidad esperada
|---------------------------------------|---------|--------------|-----------|
| Riesgo                                | Impacto | Probabilidad | Severidad |
|---------------------------------------|---------|--------------|-----------|
| manipulación de nómina                | crítico | media        | crítico   |
| acceso a información médica           | crítico | media        | crítico   |
| cambio fraudulento de cuenta bancaria | crítico | media        | crítico   |
| filtración de sueldos                 | alto    | media        | crítico   |
| robo de sesión                        | alto    | media        | crítico   |
| falta de trazabilidad                 | alto    | alta         | alto      |
| credenciales expuestas                | alto    | media        | alto      |
| XSS y CSRF                            | alto    | media        | alto      |
|---------------------------------------|---------|--------------|-----------|

### Conclusión
La mayor amenaza no es solo la pérdida técnica, sino la pérdida de confianza del trabajador, la empresa y la posible responsabilidad legal asociada a un tratamiento indebido de datos sensibles.

## 12. Requisitos no funcionales

### 12.1 Seguridad
- cifrado de datos sensibles
- autenticación robusta en frontend y backend
- control de acceso granular por rol y permisos
- tokens seguros o sesiones con validación reforzada
- registro de auditoría de acciones críticas
- políticas de contraseñas y MFA para accesos sensibles
- prevención contra OWASP Top 10 en API y frontend
- validación de tokens y manejo seguro de CORS/CSRF

### 12.2 Rendimiento
- consultas optimizadas para reportes y liquidaciones
- respuesta rápida para consultas del trabajador
- manejo eficiente de grandes volúmenes de datos por periodo

### 12.3 Disponibilidad
- copias de seguridad periódicas
- recuperación ante fallas
- monitoreo del sistema
- continuidad operativa

### 12.4 Mantenibilidad
- código modular y documentado
- pruebas unitarias y de integración
- despliegue con Vercel
- arquitectura separada por dominio funcional

## 13. Requisitos tecnológicos

### Stack propuesto
- Typescript
- Node.js
- React
- Tailwind CSS
- ORM prisma supabase
- Vercel

### Arquitectura sugerida
- backend en Node.js para autenticación, lógica de negocio y servicios de nómina
- frontend en React + TypeScript para experiencia de usuario y dashboards
- API REST/JSON para comunicación entre frontend y backend
- ORM para modelos de negocio y persistencia
- base de datos relacional Supabase
- contenedores para entorno de desarrollo y producción
- variables de entorno para configuración segura
- autenticación JWT o sesiones con node.js según el diseño final

## 14. Historias de usuario

Desde el análisis del proyecto hay que generar el pseudocódigo y expandir las historias de usuario.

### Historia 1: Liquidación de sueldo
Como administrador de RR.HH, quiero realizar el sueldo de los trabajadores para generar pagos correctos.

Criterios de aceptación:
- el sistema genera la nómina por periodo
- se calculan sueldos, descuentos y bonos
- quedan registrados en auditoría
- solo usuarios autorizados pueden generar la liquidación

### Historia 2: Consulta del trabajador
Como trabajador, quiero consultar mi información laboral para conocer mi remuneración y cotizaciones.

Criterios de aceptación:
- el trabajador solo ve sus datos
- el acceso está protegido por autenticación
- la información se muestra con permisos restringidos

### Historia 3: Licencia médica
Como trabajador, quiero registrar y consultar mi licencia médica para mantener mi información actualizada.

Criterios de aceptación:
- la licencia está asociada al empleado correcto
- los documentos se almacenan con acceso restringido
- RR.HH puede revisarla con permisos específicos

### Historia 4: Cambio de cuenta bancaria
Como trabajador, quiero actualizar mi cuenta bancaria para rebicir mi pago.

Criterios de aceptación:
- el sistema valida el cambio
- se registra el historial de modificación
- requiere autorización y auditoría

### Historia 5: Gestión de trabajador

Como administrador de RR.HH.,
 quiero registrar y actualizar la información de los trabajadores,
 para mantener correctamente sus antecedentes personales y laborales.

Criterios de aceptación
- El sistema debe permitir registrar los datos obligatorios del trabajador.
- Debe validar los datos antes de almacenarlos.
- Solo usuarios autorizados pueden crear o modificar trabajadores.
- Los cambios relevantes deben quedar registrados.
- Cada trabajador debe quedar asociado a su información laboral correspondiente.

La administración de empleados ya contempla datos personales, RUT, contacto, cargo, contrato, jornada, centro de costes, cuenta bancaria y estado laboral.

### Historia 6: Gestión de contrato

Como administrador de RR.HH.,
 quiero registrar y gestionar los contratos de los trabajadores,
 para mantener actualizada su información contractual.

Criterios de aceptación
- Cada contrato debe estar asociado a un trabajador.
- Solo usuarios autorizados pueden crear o modificar contratos.
- El sistema debe validar la información obligatoria.
- Las modificaciones relevantes deben quedar registradas.
- La información contractual debe tener acceso restringido.

Los contratos están expresamente considerados dentro de los requisitos del proyecto.

### Historia 7: Registro de asistencia

Como trabajador,
 quiero registrar mi entrada y salida laboral,
 para mantener un control de mi asistencia.

Criterios de aceptación
- El trabajador debe estar identificado en el sistema.
- El sistema debe registrar entrada y salida.
- El registro debe quedar asociado al trabajador correspondiente.
- El trabajador no debe poder modificar la asistencia de otro empleado.
- RR.HH. debe poder consultar los registros según sus permisos.

El registro de entrada y salida está incluido en vuestro objetivo y requisitos funcionales.

### Historia 8: Gestión de horas extraordinarias

Como administrador de RR.HH.,
 quiero gestionar las horas extraordinarias de los trabajadores,
 para incorporarlas correctamente al proceso de remuneración.

Criterios de aceptación
- Las horas extraordinarias deben estar asociadas al trabajador correspondiente.
- Deben estar relacionadas con un periodo.
- Solo usuarios autorizados pueden gestionarlas.
- Las horas correspondientes deben poder considerarse en el proceso de remuneración.
- Las modificaciones deben mantener trazabilidad.

Las horas extra están contempladas en el alcance de remuneraciones junto con sueldo, bonos, descuentos, asignaciones y beneficios.

### Historia 9: Gestión de vacaciones

Como trabajador,
 quiero consultar la información correspondiente a mis vacaciones,
 para conocer mi situación de vacaciones dentro de la empresa.

Criterios de aceptación
- El trabajador debe estar autenticado.
- Solo puede consultar su propia información.
- La información debe estar asociada al trabajador correspondiente.
- RR.HH. puede acceder únicamente según los permisos asignados.
- Las operaciones administrativas deben estar protegidas por autorización.

La gestión de vacaciones aparece dentro del objetivo funcional de vuestro proyecto.


### Historia 10: Gestión de cotizaciones previsionales

Como administrador de RR.HH.,
 quiero registrar las cotizaciones previsionales de los trabajadores,
 para mantener actualizada su información previsional por periodo.

Criterios de aceptación
- Las cotizaciones deben estar asociadas al trabajador correspondiente.
- Deben quedar registradas por periodo.
- Solo usuarios autorizados pueden registrar o modificar información.
- El trabajador solo puede consultar sus propias cotizaciones.
- Los cambios relevantes deben mantener trazabilidad.

Aquí tienes bastante material porque vuestro proyecto contempla salud, AFP, AFC, APV e historial de cotizaciones, entre otros elementos.

### Historia 11: Gestión de finiquito

Como administrador de RR.HH.,
 quiero gestionar el finiquito de un trabajador,
 para registrar adecuadamente el término de su relación laboral.

Criterios de aceptación
- El finiquito debe asociarse al trabajador correcto.
- Solo usuarios autorizados pueden gestionar esta información.
- La operación debe quedar registrada.
- La información debe mantenerse protegida.
- El estado laboral del trabajador debe mantenerse coherente con la operación realizada.

Finiquitos, despidos y renuncias voluntarias están contemplados entre los requisitos funcionales de Nómina Fácil.

### Historia 12: Auditoría y trazabilidad

Esta, en mi opinión, es una de las historias más importantes para vuestro proyecto DevSecOps.

Como usuario de Seguridad/Auditoría,
 quiero consultar los registros de operaciones y eventos relevantes,
 para verificar la trazabilidad de las acciones realizadas en el sistema.

Criterios de aceptación
- Solo usuarios autorizados pueden consultar la información de auditoría.
- Los accesos e interacciones sensibles definidos por el sistema deben quedar registrados.
- Los cambios de nómina y cuentas bancarias deben conservar su historial.
- La actividad debe poder relacionarse con el usuario y módulo correspondiente.
- Los registros deben estar protegidos frente a accesos no autorizados.



## 15. Recomendaciones para el desarrollo

- usar Node.js con buenas prácticas de seguridad
- limitar permisos por rol
- sanitizar entradas y salidas
- proteger rutas sensibles por permisos
- usar TLS y cifrado en almacenamiento
- implementar registro de auditoría en eventos críticos
- ejecutar análisis de seguridad y actualizaciones de dependencias
- usar Vercel con configuración segura y entorno mínimo

## 16. Conclusión

El proyecto de remuneraciones y portal del trabajador para PYMEs requiere un enfoque integral que combine funcionalidad, cumplimiento legal y seguridad de la información. El diseño debe priorizar la protección de los datos salariales, médicos y financieros, considerando la normativa chilena y los estándares internacionales de seguridad.

La propuesta debe desarrollarse con una arquitectura segura, accesos controlados, trazabilidad de eventos y gestión activa de riesgos para reducir la probabilidad de filtración, manipulación o acceso indebido.

## 17. Participantes del proyecto

- Esteban Ramirez - Scrum Master
  - facilita la planificación y seguimiento del proyecto en Azure Boards
  - cuida plazos y acuerdos de trabajo

- Andy Rodriguez - DevOps
  - configura repositorio, políticas de rama, pipelines y pruebas

- Alejandro - Ingeniero de desarrollo
  - diseña e implementa la solución con prácticas de código seguro

## 18. Resumen ejecutivo

Nómina Fácil es una solución orientada a simplificar la administración de remuneraciones y servicios del trabajador para pequeñas y medianas empresas, con foco en seguridad, cumplimiento y experiencia de usuario. Su desarrollo debe tomar en cuenta no solo la eficiencia operativa, sino también los riesgos asociados a la información sensible de los empleados y la obligación legal de protegerla adecuadamente.
