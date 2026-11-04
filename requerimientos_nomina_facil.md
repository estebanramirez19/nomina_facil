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

## 3. Alcance funcional

### 3.1 Administración de empleados
- datos personales
- RUT y contacto
- cargo y contrato
- jornada laboral
- centro de costos
- cuenta bancaria asociada
- estado laboral

### 3.2 Gestión de remuneraciones
- sueldo base
- ingresos y salidas
- horas extra
- bonos
- descuentos
- asignaciones y beneficios
- descuentos previsionales
- liquidación de sueldos por periodo
- historial de pagos


### 3.3 Cotizaciones previsionales
- cotizaciones de salud
- cotizaciones AFP
- AFC
- impuesto de segunda categoria
- prestamos
- registro por periodo
- historial y conciliación

### 3.4 Licencias médicas
- registro de licencias médicas
- carga de certificados médicos
- cálculo de días de licencia
- validación por periodo
- vinculaciones con el área de RR.HH

### 3.5 Cuentas bancarias
- registro de cuenta de pago
- actualización de cuenta y validación
- historial de cambios
- control de autorizaciones

### 3.6 Portal del trabajador
- consulta de sueldos
- historial de liquidaciones
- acceso a cotizaciones previsionales
- consulta de licencias médicas
- estado de cuenta y datos bancarios
- descarga de comprobantes asociados
- tiempo en la empresa
- renuncia voluntaria
- denuncias

### 3.7 Administración y seguridad
- roles y permisos por perfil
- registro de auditoría
- trazabilidad de cambios
- control de sesiones
- gestión de accesos y revocación

## 4. Usuarios y roles

### 4.1 Administrador de RR.HH o Nómina
- gestiona empleados
- registra pagos y liquidaciones
- valida licencias
- configura parámetros de nómina
- valida ingreso y salida trabajador
- gestionar renuncias y despidos
- gestion de contratos

### 4.2 Administrador de empresa o gerencia
- revisa reportes
- administra cuentas
- administrar datos del negocio
- analiza indicadores de nómina
- aprueba cambios importantes

### 4.3 Trabajador
- consulta sus datos personales
- revisa su sueldo y liquidaciones
- revisa cotizaciones y licencias
- actualiza sus datos autorizados

### 4.4 Soporte / Seguridad / Auditoría
- revisa logs y eventos
- valida accesos y permisos
- gestiona incidentes de seguridad
- gestiona trazabilidades

## 5. Requisitos funcionales

### 5.1 Requisitos de negocio
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

### 5.2 Requisitos de información
- La información sensible debe clasificarse y protegerse.
- Los datos deben mantenerse auditables.
- Debe existir control de retención de información.
- Cada registro debe relacionarse con empresa, empleado y periodo.

### 5.3 Requisitos de usuario
- inicio de sesión seguro con MFA
- autenticación con credenciales robustas
- control de sesiones
- permisos por perfil
- recuperación de credenciales segura

## 6. Requisitos legales y normativos

### 6.1 Código del Trabajo
El sistema debe contemplar, al menos, lo siguiente:
- liquidación de remuneraciones
- pagos de sueldo conforme a la legislación
- licencias médicas y permisos
- horas extra y remuneraciones legales
- descuentos legales
- registro de contratos y condiciones laborales
- respaldo documental y auditoría

### 6.2 Ley 21.719
La plataforma debe cumplir los principios de protección de datos personales, especialmente:
- finalidad específica y legítima del tratamiento
- minimización de datos
- limitación de acceso
- seguridad adecuada
- consentimiento según corresponda
- derechos de los titulares sobre su información
- notificación de incidentes frente a la autoridad correspondiente
- tratamiento responsable de datos sensibles

### 6.3 Requisitos de privacidad y seguridad
- política de privacidad accesible
- consentimiento claro para tratamiento de datos
- registro de tratamiento de datos
- manejo seguro de documentos médicos y financieros
- control de accesos por perfil y necesidad de conocer

## 7. Requisitos de seguridad según ISO 27002

### 7.1 Control de acceso
- asignación de roles y permisos
- mínimo privilegio
- revisión periódica de accesos
- autenticación multifactor para accesos sensibles
- revocación de accesos ante cambios de personal

### 7.2 Seguridad de activos
- clasificación de datos por sensibilidad
- cifrado en tránsito y en reposo
- manejo seguro de secretos y variables de entorno
- copias de seguridad cifradas

### 7.3 Criptografía
- TLS para conexiones web
- hash seguro para contraseñas
- protección de archivos sensibles
- gestión segura de claves y certificados

### 7.4 Seguridad operativa
- monitorización y registro de eventos
- alertas por actividad anómala
- actualizaciones periódicas de dependencias
- gestión de parches y revisión de vulnerabilidades

### 7.5 Auditoría y trazabilidad
- registro de accesos e interacciones sensibles
- historial de cambios en nómina y cuentas bancarias
- bitácora de actividad por usuario y módulo

### 7.6 Gestión de terceros
- evaluación de proveedores de infraestructura y servicios
- políticas de seguridad para integración con terceros
- cubrimiento contractual en tratamiento de datos

## 8. Requisitos según ISO 27005

La ISO 27005 guía la gestión de riesgos. El proyecto debe incluir:
- identificación de activos críticos
- evaluación de amenazas y vulnerabilidades
- valoración de impacto y probabilidad
- tratamiento del riesgo
- seguimiento y revisión continua

### 8.1 Activos críticos
- base de datos de trabajadores
- liquidaciones y remuneraciones
- información previsional y de salud
- cuentas bancarias
- documentos médicos
- registros de auditoría
- infraestructura de despliegue

### 8.2 Riesgos principales
- filtración de datos salariales
- acceso no autorizado a información personal
- manipulación de nómina o pagos
- cambio fraudulento de cuenta bancaria
- ataques a autenticación y sesiones
- fallos en disponibilidad o servicio

### 8.3 Tratamiento del riesgo
- mitigación por control técnico y organizacional
- separación de funciones
- políticas de acceso
- auditoría continua
- planes de recuperación y continuidad

## 9. Vulnerabilidades comunes en este tipo de sistemas

### 9.1 SQL Injection
Manipulación de consultas para acceder o modificar información de nómina o trabajadores.

### 9.2 XSS (Cross-Site Scripting)
Ejecutar scripts maliciosos en el portal del trabajador o módulo administrativo.

### 9.3 IDOR / Broken Access Control
Acceso a sueldo, licencias o datos bancarios de otros empleados.

### 9.4 Fuga de información sensible
Exposición de datos de salud, remuneración o cuentas bancarias.

### 9.5 Autenticación débil
Contraseñas frágiles, sesiones reutilizadas o falta de MFA.

### 9.6 CSRF
Solicitudes no autorizadas que alteran pagos o ajustes en datos.

### 9.7 Exposición de secretos
Credenciales, claves y tokens en archivos de configuración o logs.

### 9.8 Falta de auditoría
No se registran cambios críticos ni accesos a información sensible.

### 9.9 Dependencias vulnerables
Bibliotecas con fallas conocidas y actualizaciones pendientes.

## 10. Análisis de vulnerabilidades del caso

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

## 11. Requisitos no funcionales

### 11.1 Seguridad
- cifrado de datos sensibles
- autenticación robusta en frontend y backend
- control de acceso granular por rol y permisos
- tokens seguros o sesiones con validación reforzada
- registro de auditoría de acciones críticas
- políticas de contraseñas y MFA para accesos sensibles
- prevención contra OWASP Top 10 en API y frontend
- validación de tokens y manejo seguro de CORS/CSRF

### 11.2 Rendimiento
- consultas optimizadas para reportes y liquidaciones
- respuesta rápida para consultas del trabajador
- manejo eficiente de grandes volúmenes de datos por periodo

### 11.3 Disponibilidad
- copias de seguridad periódicas
- recuperación ante fallas
- monitoreo del sistema
- continuidad operativa

### 11.4 Mantenibilidad
- código modular y documentado
- pruebas unitarias y de integración
- despliegue con Vercel
- arquitectura separada por dominio funcional

## 12. Requisitos tecnológicos

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


-------------aqui voy

## 13. Historias de usuario

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

## 14. Recomendaciones para el desarrollo

- usar Node.js con buenas prácticas de seguridad
- limitar permisos por rol
- sanitizar entradas y salidas
- proteger rutas sensibles por permisos
- usar TLS y cifrado en almacenamiento
- implementar registro de auditoría en eventos críticos
- ejecutar análisis de seguridad y actualizaciones de dependencias
- usar Docker con configuración segura y entorno mínimo

## 15. Conclusión

El proyecto de remuneraciones y portal del trabajador para PYMEs requiere un enfoque integral que combine funcionalidad, cumplimiento legal y seguridad de la información. El diseño debe priorizar la protección de los datos salariales, médicos y financieros, considerando la normativa chilena y los estándares internacionales de seguridad.

La propuesta debe desarrollarse con una arquitectura segura, accesos controlados, trazabilidad de eventos y gestión activa de riesgos para reducir la probabilidad de filtración, manipulación o acceso indebido.

## 16. Participantes del proyecto

- Esteban Ramirez - Scrum Master
  - facilita la planificación y seguimiento del proyecto en Azure Boards
  - cuida plazos y acuerdos de trabajo

- Andy Rodriguez - DevOps
  - configura repositorio, políticas de rama, pipelines y pruebas

- Alejandro - Ingeniero de desarrollo
  - diseña e implementa la solución con prácticas de código seguro

## 17. Resumen ejecutivo

Nómina Fácil es una solución orientada a simplificar la administración de remuneraciones y servicios del trabajador para pequeñas y medianas empresas, con foco en seguridad, cumplimiento y experiencia de usuario. Su desarrollo debe tomar en cuenta no solo la eficiencia operativa, sino también los riesgos asociados a la información sensible de los empleados y la obligación legal de protegerla adecuadamente.
