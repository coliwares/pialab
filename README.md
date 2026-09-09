# QA Dashboard · Rindegastos

Dashboard de métricas de QA para proyectos de Rindegastos, con datos provenientes del consolidado de Google Sheets.

## Estructura

```
qa-dashboard/
├── index.html              # Dashboard principal (todo en un archivo)
└── .github/
    └── workflows/
        └── deploy.yml      # Deploy automático a GitHub Pages
```

## Cómo publicar en GitHub Pages

### 1. Crear el repositorio

1. Ir a [github.com/new](https://github.com/new)
2. Nombre sugerido: `qa-dashboard` (o `rindegastos-qa`)
3. Visibilidad: **Public** (necesario para GitHub Pages gratis) o **Private** con GitHub Pro
4. No inicializar con README (ya tenemos uno)

### 2. Subir los archivos

```bash
cd qa-dashboard
git init
git add .
git commit -m "Initial: QA Dashboard Rindegastos"
git remote add origin https://github.com/TU_USUARIO/qa-dashboard.git
git push -u origin main
```

### 3. Activar GitHub Pages

1. Ir al repositorio → **Settings** → **Pages**
2. En **Source**: seleccionar **"GitHub Actions"**
3. El workflow se ejecutará automáticamente en el próximo push

### 4. Acceder al dashboard

La URL pública quedará en:
```
https://TU_USUARIO.github.io/qa-dashboard/
```

Aparece en Settings → Pages después del primer deploy exitoso (tarda ~1 min).

---

## Actualización de datos

El dashboard carga datos **embebidos** (en el HTML). Para actualizar:

### Opción A — Editar el HTML directamente
Modificar el array `ALL_PROJECTS` en `index.html` con los datos del nuevo período y hacer push.

### Opción B — Actualizar desde Google Sheets (con hoja publicada)
1. En Google Sheets: **Archivo → Compartir → Publicar en la web** → seleccionar la hoja de detalle → CSV
2. En el dashboard, hacer clic en **"↻ Actualizar"** para cargar los datos en vivo

---

## Filtros disponibles

| Filtro | Descripción |
|--------|-------------|
| **Período** | Últimos 4 trimestres **cerrados** (se calculan solos según la fecha actual) |
| **Todos** | Todos los proyectos del período |
| **Web** | Proyectos de tipo Web |
| **Mobile** | Proyectos Mobile (no releases) |
| **Release** | Builds de release versionados (Release X.X.X) |
| **Incremental** | Mejoras incrementales post-release |
| **Revisión general** | Revisiones generales de app |

### Período (trimestres)

Los botones de período **no están fijos en el código**: se recalculan cada vez que se abre el dashboard, tomando los **4 últimos trimestres ya cerrados** respecto a la fecha real del dispositivo. El trimestre en curso (aún no cerrado) nunca se muestra, y los trimestres más antiguos que esos 4 quedan ocultos.

Ejemplo: si hoy es **Q3 2026** (en curso, sin cerrar), los pills muestran **Q3 2025, Q4 2025, Q1 2026, Q2 2026**, y el dashboard abre por defecto en **Q2 2026** (el último cerrado).

El cierre de un proyecto en un trimestre lo define la columna **`qFin`** de sus datos — desde ahí se calculan todas las métricas del período.

---

*Tipografía: Nunito Sans · Chart.js 4.4.1 · Datos embebidos + fetch CSV opcional*
