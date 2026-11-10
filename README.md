# Nómina Fácil
### Sistema de Gestión de Remuneraciones y Portal del Trabajador

**Proyecto académico | Desarrollo Seguro (CI3V64) | INACAP Santiago Sur**

**Estado del proyecto:** Planificación y diseño de arquitectura.

## 1. Descripción del proyecto

**Nómina Fácil** es una plataforma web orientada a pequeñas y medianas empresas (PYMEs) chilenas, cuyo propósito es centralizar, simplificar y automatizar la gestión de remuneraciones y los principales procesos administrativos relacionados con sus trabajadores.

La solución busca facilitar la administración de información laboral, cálculos de remuneraciones, cotizaciones previsionales, contratos, licencias médicas y registros de asistencia.

También contempla un **portal del trabajador**, mediante el cual cada empleado podrá consultar su información laboral y financiera de forma segura, según los permisos asignados.

El proyecto se desarrolla bajo un enfoque **DevSecOps**, integrando prácticas de seguridad durante todo el ciclo de vida del software, desde el levantamiento de requerimientos hasta las pruebas, el despliegue y la monitorización.

## 2. Objetivos

### Objetivo general

Desarrollar una plataforma web de gestión de remuneraciones y administración laboral para PYMEs, incorporando controles de seguridad que permitan proteger la confidencialidad, integridad y disponibilidad de la información.

### Objetivos específicos

- Automatizar procesos de cálculo y gestión de remuneraciones.
- Centralizar la información contractual y administrativa de los trabajadores.
- Facilitar la administración de cotizaciones, licencias, vacaciones y asistencia.
- Proporcionar un portal seguro de consulta para los trabajadores.
- Implementar autenticación, autorización y control de acceso según roles.
- Mantener trazabilidad de modificaciones y operaciones críticas.
- Integrar prácticas DevSecOps en el desarrollo y mantenimiento del sistema.
- Considerar la normativa laboral y de protección de datos personales aplicable en Chile.

## 3. Funcionalidades contempladas

El alcance funcional se organiza en los siguientes módulos:

| Módulo | Funcionalidades previstas |
|---|---|
| Gestión de empleados | Registro, actualización, estado laboral y datos contractuales. |
| Remuneraciones | Sueldo base, bonos, descuentos, horas extras y generación de liquidaciones. |
| Cotizaciones | Administración de AFP, salud, AFC y otros descuentos aplicables. |
| Contratos y finiquitos | Gestión documental de contratación y término de la relación laboral. |
| Asistencia | Registro de entradas, salidas y atrasos. |
| Vacaciones y permisos | Administración de solicitudes y registros de ausencias. |
| Licencias médicas | Registro, seguimiento y protección de documentación médica. |
| Cuentas bancarias | Administración de datos para pago de remuneraciones y seguimiento de modificaciones. |
| Portal del trabajador | Consulta de liquidaciones, cotizaciones y antecedentes personales autorizados. |
| Seguridad y auditoría | Control de acceso, gestión de sesiones, monitoreo y trazabilidad. |

**Nota:** Estas funcionalidades corresponden al alcance previsto y no representan módulos que ya se encuentren implementados. Su desarrollo será priorizado progresivamente.

## 4. Tecnologías y arquitectura propuesta

La solución contempla una arquitectura web modular, con separación de responsabilidades entre frontend, backend y persistencia de datos.

| Componente | Tecnología propuesta |
|---|---|
| Frontend | React, TypeScript, Vite y Tailwind CSS |
| Backend | Node.js y TypeScript |
| Framework backend | NestJS o Express, pendiente de decisión definitiva |
| API | REST con intercambio de datos JSON |
| Base de datos | PostgreSQL mediante Supabase |
| ORM | Prisma |
| Contenedores | Docker y Docker Compose |
| Control de versiones | Git y GitHub |
| Gestión del proyecto | GitHub Projects y GitHub Issues |
| Integración continua | GitHub Actions, previsto |
| Despliegue frontend | Vercel, previsto |
| Despliegue backend | Servicio independiente, pendiente de selección |

Las tecnologías indicadas representan las decisiones y alternativas documentadas durante la planificación. Su implementación será confirmada conforme avance el desarrollo.

### Principios de arquitectura

**Frontend**

Responsable de presentar la interfaz de usuario, gestionar formularios, mostrar información autorizada y consumir los servicios del backend.

**Backend**

Responsable de aplicar las reglas de negocio, realizar cálculos de remuneraciones, validar información, administrar sesiones y verificar permisos.

**Persistencia**

Responsable de mantener los datos de trabajadores, contratos, liquidaciones y registros de auditoría, aplicando restricciones de integridad y controles de acceso.

**Seguridad**

Los controles de seguridad deberán validarse principalmente en el servidor. La protección de una ruta visual en el frontend no reemplaza la autorización en el backend.

Para consultar la propuesta detallada:

[Documento de arquitectura](arquitectura_nomina_facil.md)

## 5. Seguridad de la información

Nómina Fácil contempla el tratamiento de información personal y confidencial, incluyendo remuneraciones, datos bancarios, antecedentes laborales y documentación médica.

Por este motivo, la seguridad es un requisito transversal del proyecto.

### Controles de seguridad planificados

1. **Autenticación:** mecanismos seguros para identificar a los usuarios y administrar sus sesiones.
2. **Autorización:** permisos definidos según roles y comprobación de acceso a cada recurso.
3. **Protección de datos:** cifrado y medidas de confidencialidad según la clasificación de la información.
4. **Validación de entradas:** verificación de datos recibidos por las API para prevenir entradas maliciosas o inconsistentes.
5. **Protección de cuentas:** almacenamiento seguro de contraseñas mediante algoritmos de hash adecuados.
6. **Auditoría:** registro de accesos y modificaciones relevantes, especialmente en información salarial y bancaria.
7. **Gestión de secretos:** separación de credenciales, claves y configuraciones sensibles del código fuente.
8. **Seguridad de dependencias:** revisión de bibliotecas y componentes utilizados.
9. **Seguridad de sesiones:** expiración, revocación y protección frente a accesos no autorizados.
10. **Respaldo y recuperación:** mecanismos para proteger la disponibilidad y recuperación de la información.

Estos controles deberán contar con pruebas y evidencias antes de considerarse implementados.

### Principales riesgos identificados

| Riesgo | Consecuencia potencial | Medida de mitigación prevista |
|---|---|---|
| Acceso no autorizado | Exposición de información de trabajadores | Autorización por rol, empresa y recurso |
| Manipulación de remuneraciones | Cálculos o pagos incorrectos | Validación de operaciones y auditoría |
| Modificación indebida de cuentas bancarias | Desvío de remuneraciones | Validación reforzada y trazabilidad |
| Exposición de datos médicos | Vulneración de confidencialidad | Acceso restringido y cifrado |
| Robo de sesiones | Suplantación de usuarios | Gestión segura de sesiones |
| Inyección SQL | Acceso o modificación indebida de datos | Consultas parametrizadas y validación |

El análisis de amenazas se desarrollará considerando la metodología **STRIDE**.

### Marcos y estándares de referencia

- **NIST SP 800-218 (SSDF):** prácticas de desarrollo seguro.
- **OWASP ASVS:** requisitos y verificación de seguridad para aplicaciones web.
- **OWASP Top 10:** referencia para identificar riesgos frecuentes en aplicaciones web.
- **ISO/IEC 27001:** referencia para la gestión de seguridad de la información.
- **ISO/IEC 27002:** buenas prácticas de controles de seguridad.
- **ISO/IEC 27005:** gestión de riesgos de seguridad de la información.

El proyecto también considera el Código del Trabajo de Chile y la normativa de protección de datos personales aplicable, incluyendo la Ley 21.719 según su entrada en vigencia y disposiciones correspondientes.

La utilización de estas referencias no implica certificación ni cumplimiento legal automático.

## 6. Metodología de desarrollo

El equipo utilizará prácticas DevOps y DevSecOps para integrar seguridad, calidad y colaboración durante el desarrollo.

| Etapa | Actividades planificadas |
|---|---|
| Planificar | Definición de alcance, historias de usuario, riesgos y requisitos de seguridad. |
| Programar | Implementación modular, validaciones y revisión del código. |
| Construir | Gestión de dependencias, contenedores y análisis de componentes. |
| Probar | Pruebas funcionales, de integración y de controles de seguridad. |
| Publicar | Validación de cambios y revisión previa a su integración. |
| Desplegar | Configuración segura de los entornos de ejecución. |
| Operar | Gestión de accesos, actualizaciones y respaldos. |
| Monitorizar | Revisión de errores, registros de auditoría y eventos de seguridad. |

Se utilizará GitHub Projects para dar seguimiento a las actividades y GitHub Issues para documentar tareas, defectos y mejoras.

## 7. Gestión y seguimiento del proyecto

El trabajo del equipo se organiza mediante GitHub Projects, utilizando un tablero Kanban.

**Tablero del proyecto:**

[GitHub Projects — Nómina Fácil](https://github.com/users/estebanramirez19/projects/4/views/1)

### Estados de trabajo

- **Backlog:** actividades pendientes de planificación o desarrollo.
- **Ready:** tareas preparadas para iniciar.
- **In progress:** actividades actualmente en ejecución.
- **In review:** tareas sometidas a revisión.
- **Done:** actividades completadas y validadas.

Cada tarea deberá registrar una descripción clara, responsable, prioridad y criterios de aceptación cuando corresponda.

### Flujo de colaboración propuesto

1. Seleccionar una tarea desde GitHub Projects.
2. Crear una rama de trabajo asociada a la tarea.
3. Realizar los cambios necesarios.
4. Ejecutar las comprobaciones correspondientes.
5. Crear un Pull Request que referencie el Issue.
6. Solicitar revisión de otro integrante.
7. Integrar los cambios una vez aprobados.
8. Actualizar el estado de la tarea.

Se propone utilizar las siguientes convenciones de ramas:

- `feature/numero-descripcion`: nuevas funcionalidades.
- `fix/numero-descripcion`: correcciones.
- `docs/numero-descripcion`: documentación.
- `security/numero-descripcion`: mejoras de seguridad.

Ejemplo de nombre de rama:

`feature/12-modelamiento-empleados`

Este flujo constituye la metodología de colaboración prevista y deberá complementarse con protección de la rama principal y revisiones verificables.

## 8. Organización del repositorio

### Documentación disponible

| Archivo | Descripción |
|---|---|
| `README.md` | Presentación general, tecnologías y organización del proyecto. |
| `requerimientos_nomina_facil.md` | Objetivos, alcance, requerimientos e historias de usuario. |
| `arquitectura_nomina_facil.md` | Arquitectura propuesta, tecnologías, seguridad y despliegue. |

**Documentos del proyecto:**

- [Levantamiento de requerimientos](requerimientos_nomina_facil.md)
- [Arquitectura de software](arquitectura_nomina_facil.md)

### Estructura de código prevista

La arquitectura propone organizar la futura aplicación en un monorepositorio:

```text
nomina_facil/
├── apps/
│   ├── web/            # Aplicación frontend
│   └── api/            # API y lógica de negocio
├── packages/
│   ├── shared/         # Tipos y validaciones comunes
│   └── config/         # Configuración compartida
├── docker/             # Contenedores
├── docs/               # Informes y evidencias
├── README.md
├── requerimientos_nomina_facil.md
└── arquitectura_nomina_facil.md
```

**Esta estructura es referencial y aún no corresponde a una implementación completa del repositorio.**

## 9. Instalación y ejecución

El proyecto se encuentra en fase de planificación y diseño.

Los procedimientos de instalación, configuración de variables de entorno, inicialización de base de datos y ejecución mediante Docker se documentarán una vez implementada la estructura base.

No se recomienda utilizar datos personales reales durante el desarrollo o las pruebas. Se utilizarán datos ficticios o anonimizados según corresponda.

## 10. Pruebas y aseguramiento de calidad

La estrategia de pruebas prevista contempla:

- Pruebas unitarias para reglas de negocio y cálculos.
- Pruebas de integración de API y persistencia.
- Pruebas de autenticación y autorización.
- Pruebas de aislamiento de información entre trabajadores y empresas.
- Validación de entradas en el servidor.
- Análisis estático de seguridad.
- Revisión de dependencias vulnerables.
- Detección de secretos en el repositorio.

Se proyecta integrar estas verificaciones mediante GitHub Actions, de modo que las comprobaciones relevantes puedan utilizarse como condiciones para integrar cambios.

Las pruebas y el pipeline serán documentados junto con sus resultados una vez implementados.

## 11. Equipo de desarrollo

| Integrante | Rol principal | Responsabilidades |
|---|---|---|
| Esteban Ramírez | Scrum Master y coordinación | Planificación, seguimiento de tareas, documentación, coordinación y control de entregables. |
| Alejandro Belvie | Desarrollo de software y seguridad | Diseño técnico, desarrollo de componentes, implementación y revisión de controles de seguridad. |

Las actividades de revisión, pruebas, integración y aseguramiento de calidad requieren colaboración de ambos integrantes.

## 12. Estado y próximas actividades

El proyecto cuenta con documentación de requerimientos, una propuesta inicial de arquitectura y tareas organizadas en GitHub Projects.

### Próximos hitos

- [x] Definir el problema y el alcance general.
- [x] Elaborar el levantamiento de requerimientos.
- [x] Documentar una propuesta de arquitectura.
- [x] Crear el repositorio y organizar las tareas iniciales.
- [ ] Validar definitivamente el stack tecnológico.
- [ ] Modelar las entidades y relaciones de la base de datos.
- [ ] Establecer políticas de ramas y revisión.
- [ ] Inicializar frontend y backend.
- [ ] Configurar la conexión con PostgreSQL/Supabase.
- [ ] Implementar autenticación y autorización.
- [ ] Desarrollar los módulos priorizados.
- [ ] Incorporar pruebas automatizadas y análisis de seguridad.
- [ ] Configurar integración continua y despliegue.
- [ ] Validar las evidencias de seguridad y los requisitos funcionales.

El seguimiento actualizado de estas actividades se realiza en el tablero del proyecto.

## 13. Uso de inteligencia artificial

Durante la planificación y desarrollo se podrán utilizar herramientas de inteligencia artificial como apoyo para el análisis de requerimientos, la documentación, las propuestas de arquitectura y la revisión de alternativas técnicas.

El equipo será responsable de:

- Revisar y comprender los contenidos generados.
- Verificar las recomendaciones técnicas antes de aplicarlas.
- Validar la seguridad y funcionamiento del código.
- Documentar el uso de inteligencia artificial en los informes académicos.
- No incorporar información sensible o credenciales en las consultas.

La inteligencia artificial se considera una herramienta de apoyo y no reemplaza la validación técnica ni las responsabilidades del equipo.

## 14. Alcance académico

Nómina Fácil se desarrolla como parte de la asignatura **Desarrollo Seguro (CI3V64)** de INACAP, sede Santiago Sur.

El objetivo académico es demostrar la aplicación de prácticas de ingeniería de software, gestión de proyectos y seguridad durante el ciclo de vida del desarrollo.

Los avances se respaldarán mediante documentación, historial de cambios, tareas, revisiones de código y resultados de pruebas.

El sistema no debe considerarse apto para procesar remuneraciones reales hasta completar su implementación, validación funcional, evaluación de seguridad y revisión normativa correspondiente.

---

**Nómina Fácil — Desarrollo de software con seguridad desde el diseño.**

**Equipo:** Esteban Ramírez · Alejandro Belvie

**Institución:** INACAP Santiago Sur

**Asignatura:** Desarrollo Seguro · CI3V64
