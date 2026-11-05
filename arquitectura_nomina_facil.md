# Arquitectura propuesta para Nómina Fácil

## 1. Objetivo de la arquitectura

Esta guía está pensada para servir como base de implementación del proyecto de nómina y portal del trabajador, tomando como referencia los requisitos de seguridad, cumplimiento legal, separación de frontend/backend, despliegue y stack tecnológico ya definido en `requerimientos_nomina_facil.md`.

El objetivo es construir una solución robusta, modular y segura, con una base tecnológica clara para que el equipo pueda ir desarrollando cada módulo sin mezclar responsabilidades ni comprometer datos sensibles como sueldos, cotizaciones, licencias médicas y cuentas bancarias.

---

## 2. Principios de diseño

1. Separación clara de responsabilidades
   - Frontend: experiencia del usuario, validaciones visuales, consumo de API.
   - Backend: lógica de negocio, seguridad, autorización, cálculo de nómina, reglas fiscales.
   - Base de datos: persistencia centralizada y trazabilidad.

2. Seguridad por defecto
   - mínimo privilegio por rol
   - autenticación segura
   - cifrado en tránsito y reposo
   - auditoría de acciones críticas
   - prevención de OWASP Top 10

3. Escalabilidad y mantenibilidad
   - arquitectura modular
   - uso de patrones de servicios y repositorios
   - código tipado y pruebas
   - configuración por variables de entorno

4. Cumplimiento y trazabilidad
   - log de accesos, cambios y liquidaciones
   - control de autorización por perfil
   - historial de modificaciones de cuentas bancarias, sueldos y licencias

5. Despliegue profesional
   - frontend en Vercel
   - backend en servicio separado
   - entornos: desarrollo, staging, producción

---

## 3. Stack tecnológico sugerido

### Frontend
- React
- TypeScript
- Vite
- Tailwind CSS
- React Router
- Axios o Fetch con cliente centralizado
- React Query / TanStack Query
- Zustand o Context API para estado global
- Zod para validación de formularios y esquemas

### Backend
- Node.js
- TypeScript
- Framework recomendado: NestJS o Express + arquitectura limpia
- Prisma ORM
- PostgreSQL (o Supabase Postgres)
- JWT para autenticación
- Bcrypt para contraseñas
- Helmet, CORS, Express Rate Limit / Nest throttling
- class-validator / Zod para validación
- Swagger / OpenAPI para documentación de API
- Jest + Supertest para pruebas

### Infraestructura y despliegue
- Docker
- Docker Compose para desarrollo/local
- GitHub Actions o Azure DevOps para CI/CD
- Vercel para frontend
- Backend en servicio separado: Render, Railway, Azure App Service, VPS o Vercel Serverless según estrategia
- Supabase o Postgres managed para persistencia

---

## 4. Arquitectura general

### 4.1 Propuesta de estructura

Se recomienda trabajar en monorepo para facilitar la coordinación entre frontend y backend:

```text
nomina-facil/
├── apps/
│   ├── web/               # Frontend React + TypeScript
│   └── api/               # Backend Node.js + TypeScript
├── packages/
│   ├── shared/            # Tipos, enums, validaciones compartidas
│   ├── ui/                # Componentes reutilizables
│   └── config/            # ESLint, TS, archivos de configuración
├── docker/
│   ├── docker-compose.yml
│   └── Dockerfile
├── .env.example
├── .gitignore
├── package.json
├── README.md
└── tsconfig.base.json
```

### 4.2 Modelo de comunicación

- El frontend solo se comunica con el backend a través de API REST/JSON.
- No se debe depender de lógica de negocio dentro del frontend.
- Toda regla fiscal, cálculo de sueldo, cotizaciones, licencias, y permisos deben ejecutarse en backend.
- La autenticación se valida en backend y se emite un token seguro para el cliente.

---

## 5. Separación recomendada entre backend y frontend

### Frontend
Responsabilidades:
- renderizar pantallas y dashboards
- login y sesión del usuario
- validación UX (formateo, reglas visuales)
- consumo de APIs
- gestión de estado de UI
- mostrar permisos por rol y rutas protegidas

No debe:
- calcular nómina directamente
- almacenar secretos
- manejar lógica crítica de negocio
- decidir permisos de acceso sin validación del backend

### Backend
Responsabilidades:
- validación de datos recibidos
- autenticación y autorización
- cálculo de sueldos, bonos, descuentos, horas extra y cotizaciones
- manejo de documentos médicos y archivos sensibles
- generación de auditoría y trazabilidad
- control de acceso por perfil y módulos
- integración con servicios bancarios, previsionales o reportes

No debe:
- depender de la UI para decisiones críticas
- aceptar datos sin validación de esquema
- exponer información sensible sin control de permisos

---

## 6. Estructura sugerida del backend

### 6.1 Capas recomendadas

```text
apps/api/
├── src/
│   ├── app.module.ts
│   ├── main.ts
│   ├── config/
│   │   ├── env.ts
│   │   └── cors.ts
│   ├── common/
│   │   ├── filters/
│   │   ├── guards/
│   │   ├── decorators/
│   │   ├── interceptors/
│   │   └── utils/
│   ├── auth/
│   │   ├── auth.controller.ts
│   │   ├── auth.service.ts
│   │   ├── dto/
│   │   └── strategies/
│   ├── users/
│   ├── employees/
│   ├── payroll/
│   ├── leaves/
│   ├── contracts/
│   ├── bank-accounts/
│   ├── reports/
│   ├── audit/
│   ├── prisma/
│   │   └── prisma.service.ts
│   └── modules/
│       └── ...
```

### 6.2 Módulos funcionales sugeridos
- autenticación y autorización
- empleados
- cargos y contratos
- nómina y liquidaciones
- licencias médicas
- vacaciones
- horas extra
- cotizaciones previsionales
- cuentas bancarias
- auditoría y logs
- reportes y dashboards

---

## 7. Estructura sugerida del frontend

```text
apps/web/
├── src/
│   ├── app/
│   │   ├── routes/
│   │   ├── layouts/
│   │   └── providers/
│   ├── features/
│   │   ├── auth/
│   │   ├── dashboard/
│   │   ├── employees/
│   │   ├── payroll/
│   │   ├── leaves/
│   │   └── worker-portal/
│   ├── components/
│   │   ├── ui/
│   │   ├── forms/
│   │   └── tables/
│   ├── services/
│   │   └── api/
│   ├── hooks/
│   ├── store/
│   ├── lib/
│   ├── styles/
│   ├── App.tsx
│   └── main.tsx
```

### 7.1 Rutas sugeridas
- /login
- /dashboard
- /empleados
- /nomina
- /licencias
- /contratos
- /reportes
- /portal-trabajador
- /perfil
- /configuracion

### 7.2 Rutas protegidas
- El frontend debe validar roles (UI), pero la decisión final siempre debe estar en backend.
- Se recomienda crear wrappers de autenticación por rol:
  - admin
  - rrhh
  - manager
  - employee
  - support

---

## 8. Modelo de seguridad

### 8.1 Autenticación
- Login con email / RUT + contraseña
- JWT con expiración corta
- Refresh token con almacenamiento seguro (httpOnly, Secure, SameSite)
- renovación automática de sesiones
- bloqueo tras varios intentos fallidos
- MFA para roles sensibles y accesos administrativos

### 8.2 Autorización
- RBAC (Role Based Access Control)
- permisos por módulo y acción
- validación por backend en cada endpoint crítico
- control de acceso por necesidad de conocer

Ejemplo de roles:
- SuperAdmin
- RRHH
- Gerencia
- Trabajador
- Soporte
- Auditor

### 8.3 Protección contra OWASP Top 10
- SQL Injection: Prisma / queries parametrizadas, validación estricta
- XSS: sanitización, escape de contenido, CSP
- CSRF: tokens anti-CSRF, SameSite cookies, validación de origen
- IDOR: validación de ownership y pertenencia de registros
- Deserialización insegura: no aceptar JSON arbitrario sin esquema
- Exposición de secretos: variables de entorno, no hardcodear

### 8.4 Auditoría
Debe registrarse:
- acceso a información salarial
- cambios de cuentas bancarias
-Cambio de estado de empleados
- creación o modificación de liquidaciones
- permisos alterados
- login exitoso / fallido
- eliminación o exportación de datos sensibles

Se recomienda una tabla de auditoría con:
- id
- userId
- action
- module
- entityId
- previousValue
- newValue
- ipAddress
- userAgent
- createdAt

---

## 9. Seguridad de datos y compliance

### 9.1 Datos sensibles que requieren tratamiento especial
- RUT
- remuneraciones
- cotizaciones previsionales
- licencias médicas
- documentos adjuntos
- cuentas bancarias
- información personal y confidencial

### 9.2 Medidas mínimas
- HTTPS obligatorio en producción
- TLS en todas las conexiones
- cifrado de archivos adjuntos y documentos médicos
- copias de seguridad cifradas
- política de retención de datos
- control de acceso por perfil
- registro de consentimiento y tratamiento de datos

### 9.3 Cumplimiento normativo
La arquitectura debe considerar:
- Ley 21.719 y protección de datos personales
- normativa laboral vigente
- trazabilidad de cambios y responsabilidades
- tratamiento mínimo indispensable de datos
- política de privacidad accesible al usuario

---

## 10. Base de datos y persistencia

### Recomendación principal
- PostgreSQL con Supabase o una base relacional administrada

### Por qué PostgreSQL
- robustez transaccional
- soporte de integridad referencial
- adecuado para nómina, reportes y auditoría
- excelente compatibilidad con Prisma

### Entidades principales sugeridas
- users
- roles
- permissions
- employees
- contracts
- salaries
- payrolls
- payroll_items
- leaves
- medical_documents
- bank_accounts
- bank_account_history
- contributions
- audit_logs
- settings

### Reglas de diseño
- cada registro debe tener createdAt y updatedAt
- cada operación crítica debe quedar registrada en auditoría
- cada liquidación debe referenciar periodo, empleado y empresa
- cada cuenta bancaria debe tener historial de cambios
- no se debe eliminar información crítica en “borrado físico”; usar soft delete o auditoría

---

## 11. Dependencias recomendadas por módulo

### Backend (package.json sugerido)
```bash
npm install express cors helmet morgan dotenv zod bcryptjs jsonwebtoken
npm install @prisma/client prisma
npm install @nestjs/core @nestjs/common @nestjs/platform-express
npm install class-validator class-transformer
npm install --save-dev typescript ts-node nodemon jest supertest @types/node @types/express
```

### Frontend (package.json sugerido)
```bash
npm install react react-dom react-router-dom
npm install -D vite @vitejs/plugin-react typescript tailwindcss postcss autoprefixer
npm install @tanstack/react-query axios zod
npm install clsx
```

### Seguridad adicional recomendada
```bash
npm install express-rate-limit helmet csurf cookie-parser
npm install --save-dev eslint prettier eslint-plugin-react eslint-plugin-react-hooks
```

### Herramientas de observabilidad
- Sentry
- LogRocket (opcional)
- Winston o Pino para logs
- Prometheus/Grafana o monitoring ligero para producción

---

## 12. Recomendación de despliegue

### 12.1 Frontend en Vercel
Se recomienda dejar el frontend en Vercel por su simplicidad, velocidad y buena integración con React.

Configuración recomendada:
- proyecto React + Vite
- variable de entorno `VITE_API_URL`
- dominio con HTTPS
- protección de rutas y manejo de sesión en cliente
- uso de middleware de seguridad opcional

### 12.2 Backend separado
Por seguridad y robustez, el backend debe ir separado del frontend, incluso si eventualmente se despliega en Vercel como función serverless.

Opciones válidas:
- Render
- Railway
- Azure App Service
- VPS con Docker
- Vercel Functions para prototipos sencillos

Recomendación fuerte:
- en un proyecto real de nómina, el backend debe estar separado del frontend y no depender de un entorno de cliente para decisiones críticas

### 12.3 Base de datos
- Supabase Postgres o servidor PostgreSQL managed
- backup automatizado
- acceso solo por red privada o puerto restringido
- variables de entorno en servicio seguro

---

## 13. Variables de entorno recomendadas

```env
NODE_ENV=development
PORT=4000
DATABASE_URL=postgresql://user:password@host:5432/dbname
JWT_SECRET=super_secret_key
JWT_REFRESH_SECRET=super_refresh_secret
JWT_EXPIRES_IN=15m
REFRESH_TOKEN_EXPIRES_IN=7d
FRONTEND_URL=https://tu-frontend.vercel.app
CORS_ORIGIN=https://tu-frontend.vercel.app
SMTP_HOST=smtp.example.com
SMTP_PORT=587
SMTP_USER=mail@example.com
SMTP_PASS=secret
UPLOAD_DIR=./uploads
LOG_LEVEL=info
```

### Buenas prácticas
- nunca commitear `.env`
- usar `.env.example` como plantilla
- rotar secretos periódicamente
- usar secrets manager si la infraestructura lo permite

---

## 14. CI/CD y calidad

### Recomendado
- lint
- type-check
- tests unitarios/integración
- build del frontend
- build del backend
- análisis de vulnerabilidades con dependabot / npm audit / Snyk

### Pipeline sugerida
1. push a rama
2. install dependencies
3. run lint
4. run tests
5. build frontend/backend
6. deploy a entorno de staging
7. smoke tests
8. deploy a producción

---

## 15. Observabilidad y monitoreo

### Elementos clave
- logs estructurados
- metricas de uso por endpoint
- alertas por errores 4xx/5xx
- monitorización de tiempo de respuesta
- trazabilidad de cambios críticos
- reportes de seguridad y accesos sospechosos

### Herramientas sugeridas
- Sentry para errores
- Logtail / Datadog / New Relic (opcional)
- CloudWatch / Azure Monitor según infraestructura
- GitHub Actions para pipelines y alertas

---

## 16. Recomendación de flujo de trabajo de desarrollo

### Fase 1: base del proyecto
- inicializar monorepo
- configurar TypeScript
- crear backend y frontend base
- configurar Prisma y PostgreSQL
- configurar variables de entorno

### Fase 2: autenticación y seguridad
- login/logout
- JWT + refresh tokens
- roles y permisos
- middleware de autorización
- auditoría básica

### Fase 3: módulos de negocio
- empleados
- contratos
- nómina
- licencias
- cotizaciones
- cuentas bancarias

### Fase 4: portal trabajador
- vista personal
- historiales y liquidaciones
- permisos por identidad
- documentos y consultas limitadas

### Fase 5: despliegue y hardening
- Docker
- Vercel frontend
- backend en servicio externo
- protección de endpoints
- pruebas de seguridad
- backups y monitoring

---

## 17. Checklist de arquitectura antes de arrancar el código

- [ ] Definir repositorio o monorepo
- [ ] Separar frontend y backend de forma clara
- [ ] Elegir PostgreSQL + Prisma
- [ ] Definir roles y permisos
- [ ] Definir entidad de auditoría
- [ ] Definir flujo de autenticación JWT + refresh token
- [ ] Definir entorno de despliegue frontend (Vercel)
- [ ] Definir backend host y estrategia de API
- [ ] Configurar variables de entorno
- [ ] Definir estrategia de seguridad y OWASP
- [ ] Preparar estructura de carpetas
- [ ] Definir Módulos de nómina, empleados y licencias
- [ ] Preparar pipelines CI/CD

---

## 18. Conclusión

La arquitectura ideal para Nómina Fácil debe priorizar tres pilares: seguridad, trazabilidad y separación de responsabilidades. El backend debe encargarse de las reglas de negocio, cálculo de nómina y control de acceso; el frontend debe centrarse en la experiencia de usuario; y la infraestructura debe operar con base de datos robusta, despliegue seguro y auditoría constante.

Como proyecto orientado a información sensible y de alto impacto, no basta con una solución funcional: debe construirse con principios de privacidad, control, integridad y disponibilidad. Esta guía sirve como base técnica para comenzar a programar con una arquitectura sólida, segura y escalable.

---

## 19. Siguiente paso recomendado

1. Crear el repositorio o monorepo.
2. Inicializar backend con Node.js + TypeScript + Prisma.
3. Inicializar frontend React + TypeScript + Tailwind.
4. Definir modelos base: usuario, empleado, contrato, nómina, licencias, auditoría.
5. Implementar autenticación y roles.
6. Desarrollar módulos por dominio.
7. Preparar despliegue en Vercel y backend externo.
8. Añadir pruebas y auditoría antes de producción.

