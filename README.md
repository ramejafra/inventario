# 📦 Sistema de Inventario — Negocio Pequeño

Aplicación web autocontenida para gestionar el inventario de un negocio pequeño: registrar productos, entradas (compras), salidas (ventas) y alertas automáticas de existencias bajas. **Bloquea ventas sin stock.**

> No requiere instalación, ni servidor, ni conexión a Internet (después de la primera carga). Todos los datos se guardan en el navegador (`localStorage`).

---

## 🚀 Cómo empezar

1. Abre `index.html` con **doble clic** en cualquier navegador moderno (Chrome, Edge, Firefox, Safari).
2. La primera vez verás un mensaje preguntando si quieres **cargar datos de demostración**. Si aceptas, se crean productos y movimientos de muestra para que veas cómo funciona todo.
3. Si rechazas, empieza desde cero en **Productos → Nuevo producto**.

> **Tip:** crea un acceso directo al archivo en tu escritorio para abrirlo con un solo clic cada día.

---

## 🧭 Secciones

### 📊 Dashboard
Resumen visual: total de productos, valor del inventario (costo × stock), alertas activas y movimientos del día. Incluye un gráfico de los últimos 7 días y un ranking de productos más vendidos.

### 📦 Productos
- Alta, baja y modificación de productos con **SKU, nombre, categoría, unidad (pza, kg, lt…), costo, precio y stock mínimo**.
- Búsqueda por nombre o SKU.
- Filtro por categoría.
- Indicador visual por producto: **OK / Stock bajo / Sin stock**.

### 🚚 Entradas
Registra compras o reabastecimiento. Captura: producto, cantidad, costo unitario, proveedor, número de factura y notas. Calcula el total automáticamente.

### 💵 Salidas (ventas)
- Registra ventas o consumos.
- **Validación en vivo:** al elegir producto y capturar la cantidad, el sistema compara contra el stock disponible.
  - Si la cantidad solicitada **supera el stock**, aparece una alerta roja y el botón de "Registrar salida" se deshabilita.
  - Si el producto está en **0 unidades**, también se bloquea la venta.
- Captura tipo de movimiento (venta, consumo interno, merma, devolución).

### ⚠️ Alertas
- Lista de productos **sin stock** (no se pueden vender).
- Lista de productos **por debajo del mínimo**.
- Sugerencia automática de **cantidad a pedir** (doble del mínimo) y costo estimado del pedido.
- Botón "Crear entrada rápida" para registrar el reabastecimiento sugerido en un clic.

### 🕓 Movimientos
Historial completo con filtros: rango de fechas, tipo de movimiento y totales de entradas/salidas.

### ⚙️ Configuración
- Nombre del negocio, símbolo de moneda, % de impuesto.
- **Exportar respaldo** JSON (para guardar en USB, nube, etc.).
- **Importar respaldo** desde un archivo JSON.
- **Borrar todos los datos** (con doble confirmación).

---

## 💾 Acerca de los datos

- **Persistencia:** los datos se guardan automáticamente en el navegador (`localStorage`). Persisten aunque cierres la pestaña o apagues la computadora.
- **Límite de espacio:** ~5 MB en la mayoría de navegadores. Suficiente para cientos de miles de movimientos.
- **⚠️ Importante:** si borras los datos de navegación del navegador, perderás el inventario. **Usa "Exportar" regularmente** y guarda el archivo JSON en un lugar seguro (USB, OneDrive, Google Drive, etc.).
- **Privacidad total:** nada sale de tu computadora. No hay servidor, no hay cuentas, no hay nube obligatoria.

---

## 🛡️ Cómo funciona la regla "Sin stock = no se vende"

1. Al abrir el formulario de **Salidas**, el sistema calcula el stock actual de cada producto (= Σ entradas − Σ salidas).
2. Al seleccionar un producto, muestra el stock disponible en tiempo real.
3. Si capturas una cantidad mayor al stock, **el botón "Registrar salida" se deshabilita** y aparece una alerta roja explicando el motivo.
4. La validación también se ejecuta al confirmar el formulario (defensa en profundidad).

---

## ⌨️ Atajos

| Acción | Resultado |
|---|---|
| `Esc` | Cierra cualquier ventana modal |
| Doble clic en `index.html` | Abre la aplicación |

---

## 📋 Estructura de datos (referencia)

```js
{
  storeName: "Mi Tienda",
  currency: "$",
  taxRate: 16,
  products: [
    { id, sku, name, category, unit, cost, price, minStock, createdAt }
  ],
  movements: [
    { id, type:'entry'|'output', productId, qty, unitPrice, total, party, reference, notes, date }
  ]
}
```

---

## 🆘 Problemas comunes

**"No se guardan los datos"** → Tu navegador tiene `localStorage` deshabilitado o estás en modo incógnito. Usa una ventana normal.

**"Quiero usar la app en varios equipos"** → Exporta el respaldo en un equipo y use "Importar" en el otro. (Cada navegador guarda su propia copia.)

**"Quiero empezar de cero sin perder el formato"** → Configuración → Borrar todos los datos.

---

## 🧰 Detalles técnicos

- **Stack:** HTML + Tailwind CSS (CDN) + JavaScript puro (sin frameworks, sin build step).
- **Tamaño:** un solo archivo `index.html` (~65 KB).
- **Compatibilidad:** Chrome 90+, Edge 90+, Firefox 88+, Safari 14+.
- **Sin dependencias locales:** solo requiere conexión a Internet la primera vez (para descargar Tailwind/FontAwesome desde CDN). Después se puede usar sin red.

---

**Versión 1.0** — Hecho para negocios pequeños que necesitan control simple, rápido y confiable.