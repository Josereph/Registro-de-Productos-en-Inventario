# Registro-de-Productos-en-Inventario

Aplicación de escritorio en **Java Swing** para registrar, listar, editar y eliminar productos de inventario.  
Incluye validaciones básicas, control de duplicados por **código de entrada** y persistencia en memoria mediante un arreglo gestionado por `GestionEmpleados`.

> Nota: El nombre de la clase `Empleado` se usa como “entrada de inventario / producto”. Puede renombrarse a `Producto` más adelante.

---

## ✨ Características

- Alta de productos con: código, nombre, observaciones, cantidad, estado (buen estado/dañado), unidad de medida, ubicación, fecha y número de lote.
- Edición in-place desde la tabla (modo edición).
- Eliminación con confirmación.
- Validaciones:
  - Código y nombre obligatorios.
  - Lote numérico.
  - Fecha y ubicación requeridas.
  - Evita duplicados por **código** al insertar.
- Tabla con las columnas:  
  `Código | Nombre | Observaciones | Cantidad | Estado | Unidad de Medida | Ubicación | Fecha | Lote`

---

## 📦 Requisitos

- **Java 8+** (JDK 1.8 o superior).
- **NetBeans 12+** (recomendado) o cualquier IDE compatible con Swing.
- **Librería JCalendar / JDateChooser** de Toedter para el selector de fecha:
  - Grupo: `com.toedter`
  - Artefacto: `jcalendar`
  - Si usas jar: `jcalendar-x.x.x.jar` (añadir al classpath)

---

## 🗂️ Estructura del proyecto

```

├── build/                → Carpeta generada automáticamente por NetBeans al compilar
│   └── classes/          → Contiene los .class (archivos bytecode compilados)
│       ├── clases/       → .class de tus modelos (Empleado, GestionEmpleados…)
│       ├── Main/         → .class del paquete Main (si tienes clase con main aquí)
│       └── vista/        → .class de tus formularios Swing (Diseño)
│
├── nbproject/            → Configuración interna de NetBeans (no tocar mucho)
│   └── private/          → Ajustes locales del IDE (paths, usuario, etc.)
│
├── src/                  → 📌 Código fuente en Java
│   ├── clases/           → Modelo y lógica de negocio
│   │    ├── Empleado.java
│   │    └── GestionEmpleados.java
│   ├── Main/             → Clase principal con `public static void main` (si existe)
│   └── vista/            → Interfaz gráfica (Diseño.java y otros formularios)
│
└── test/                 → Código de pruebas unitarias (JUnit, opcional)

```

## ⚙️ Configuración y ejecución

### Opción A: NetBeans (recomendada)
1. Importa el proyecto en NetBeans.
2. Asegúrate de añadir la librería **JCalendar/JDateChooser** al proyecto:
   - Project > Properties > Libraries > Add JAR/Folder > selecciona `jcalendar-x.x.x.jar`.
3. Establece `vista.Diseño` como **Main Class** (si no lo hace automático).
4. Ejecuta con **Run** ▶️.

### Opción B: Consola (javac/java)
1. Coloca el jar de `jcalendar` en una carpeta `lib/`.
2. Compila:

   ```bash
   javac -cp .;lib/jcalendar-x.x.x.jar src/clases/*.java src/vista/*.java -d bin


    java -cp bin;lib/jcalendar-x.x.x.jar vista.Diseño


🧭 Uso básico

Abre la aplicación.
Completa los campos.
Haz clic en Guardar para insertar.
Usa Editar para modificar un registro seleccionado.
Usa Borrar para eliminar un registro seleccionado.

🧱 Modelo de datos (Empleado)
String  codigoEntrada;
String  nombreProducto;
String  estado;          // "Buen Estado" | "Dañado"
int     cantidad;
String  fechaRecibido;
String  unidadMedida;
int     nLote;
String  ubicacion;
String  observaciones;

🧠 Lógica de negocio (GestionEmpleados)
Arreglo fijo de 100 elementos (Empleado[]) con contador.
Métodos disponibles:
agregarEmpleado(Empleado e)
obtenerEmpleados()
eliminarEmpleado(String codigo)
buscarEmpleado(String codigo)
existeCodigo(String codigo)
actualizarEmpleado(Empleado e)

🧩 Notas de UI (Diseño)
JDateChooser (Toedter) para la selección de fecha.
ButtonGroup para estado.
DefaultTableModel para la tabla.
Validaciones antes de guardar.
Modo edición vs. modo inserción.

🗺️ Roadmap / Mejoras futuras
Renombrar clase Empleado → Producto.
Persistencia en archivo/BD (SQLite/H2).
Migrar a ArrayList en lugar de arrays fijos.
Exportar tabla a CSV/Excel.
Tests unitarios.

📄 Licencia
Este proyecto se distribuye bajo la licencia MIT (ver LICENSE).
---
## 📜 CHANGELOG.md  
```markdown
# Changelog

## [1.0.0] - 2025-08-29
### Added
- Primera versión estable de la aplicación Swing.
- Clase `Empleado` como modelo de producto en inventario.
- Clase `GestionEmpleados` con CRUD básico (array de 100).
- Vista `Diseño` con interfaz Swing (tabla, formularios y botones).

### Fixed
- Corrección de `dgvregistro()` para usar getters correctos (`getCodigoEntrada()`, `getNombreProducto()`, etc.).
- Manejo adecuado de edición con `modoEdicion` y `filaEditando`.
- Confirmaciones de borrado con `showConfirmDialog` y mensajes con `showMessageDialog`.
- Validaciones de campos antes de guardar: código obligatorio, lote numérico, fecha y ubicación requeridas.

### Changed
- `observaciones` pasó de `double` a `String`.
- Mensajes de error más descriptivos en `btnguardarActionPerformed`.
- Método `actualizarEmpleadoEnGestion` ahora usa `gestion.actualizarEmpleado(...)` para persistir.

---

MIT License

Copyright (c) 2025  

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

