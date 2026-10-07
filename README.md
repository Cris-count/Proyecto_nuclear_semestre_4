# Mentora

Estructura inicial de Mentora. Esta base separa los clientes y el backend para que los requisitos, cuando estén definidos, puedan incorporarse sin reconstruir la arquitectura.

En esta etapa no hay funcionalidades, entidades, casos de uso ni reglas de negocio.

## Arquitectura

Web y mobile consumen el mismo backend a través de una API REST. La lógica de negocio vivirá en el backend. La persistencia y la base de datos se elegirán cuando el dominio esté definido.

```text
Frontend Web ──┐
               ├── API REST ── Backend ── Persistencia ── Base de datos
Mobile ────────┘
```

## Estructura

```text
mentora/
├── frontend/
│   ├── web/                 Cliente Angular
│   │   └── src/app/
│   │       ├── core/        Piezas transversales del cliente web
│   │       ├── shared/      Piezas reutilizables del cliente web
│   │       └── features/    Requisitos futuros del cliente web
│   └── mobile/              Cliente Angular + Ionic + Capacitor
│       └── src/app/
│           ├── core/        Piezas transversales del cliente móvil
│           ├── shared/      Piezas reutilizables del cliente móvil
│           └── features/    Requisitos futuros del cliente móvil
├── backend/                 API REST (NestJS)
│   └── src/
│       ├── core/            Infraestructura transversal
│       ├── shared/          Utilidades, tipos e interfaces comunes
│       ├── modules/         Módulos de negocio futuros
│       └── config/          Configuración de la aplicación
├── shared/                  Contratos compartidos, cuando haga falta
├── docs/
│   ├── architecture/
│   ├── requirements/
│   ├── design/
│   ├── api/
│   └── decisions/
└── scripts/                 Automatizaciones futuras
```

`shared/` en la raíz queda reservado para elementos que de verdad puedan compartirse entre web, mobile y backend. Cada aplicación mantiene su propio `package.json`.

## Cómo ejecutar

Requisitos: Node.js LTS y npm.

Frontend web, en http://localhost:4200:

```bash
cd frontend/web
npm start
```

Aplicación mobile en el navegador, en http://localhost:8100:

```bash
cd frontend/mobile
npm start -- --port 8100
```

Backend, en http://localhost:3000:

```bash
cd backend
npm run start:dev
```

Los proyectos nativos de Android e iOS se agregan cuando hagan falta. iOS requiere macOS.

```bash
cd frontend/mobile
npx cap add android
npx cap add ios
```
