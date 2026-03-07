# 🌿 Lupino · Sistema de Punto de Venta

Sistema de ventas web para el local **Lupino** — multi-vendedor, conectado a Google Sheets vía Apps Script, sin instalación, funciona desde el celular.

---

## 📁 Estructura de archivos

```
index.html          → Selector de vendedores (entrada al sistema)
[prefijo]-index.html    → POS de cada vendedor
[prefijo]-reportes.html → Reportes de cada vendedor
```

### Vendedores activos

| Archivo | Vendedor | Prefijo | Reportes |
|---|---|---|---|
| `ne-index.html` | Nali Eggui | NE | `ne-reportes.html` |
| `xx-index.html` | Usuario Prueba | XX | `xx-reportes.html` |

---

## 🗄️ Google Sheets — VENDEDORES LUPINO

Planilla central con una hoja por vendedor:

| Hoja | Descripción |
|---|---|
| `INVENTARIO_NE` | Productos de Nali Eggui |
| `VENTAS_NE` | Ventas de Nali Eggui |
| `INVENTARIO_XX` | Productos usuario prueba |
| `VENTAS_XX` | Ventas usuario prueba |

### Columnas INVENTARIO
`A=Código` `B=Producto` `C=Stock` `D=P.Costo` `E=P.Venta` `F=Proveedor` `G=Categoría` `H=Reservada` `I=Reservada`

### Columnas VENTAS
`A=Fecha` `B=Producto` `C=Cantidad` `D=P.Venta` `E=Modo de pago` `F=Total`

---

## ⚙️ Apps Script — VENDEDORES LUPINO

**URL del deployment:**
```
https://script.google.com/macros/s/AKfycby9UoS5VbPEroBBrFdFMjakKwQ9sEHBaliO007Fcp42OgZWo3OInsaNpwqkO5cQhE__zg/exec
```

### Acciones disponibles

| Acción | Descripción |
|---|---|
| `getProductos` | Devuelve inventario del vendedor |
| `vender` | Registra venta y descuenta stock |
| `ingresarMercaderia` | Suma stock o crea producto nuevo |
| `ajustarStock` | Modifica stock/precio/nombre |
| `getVentas` | Devuelve todas las ventas |
| `getEstadisticas` | Estadísticas del mes |
| `getVentasDiarias` | Ventas por día para el calendario |

Todas las acciones requieren el parámetro `&prefijo=NE` (o el prefijo correspondiente).

---

## 🔑 Protocolo de códigos de producto

Los códigos se generan automáticamente con las **iniciales del vendedor + número correlativo**:

```
NE001, NE002, NE003...  → Nali Eggui
VA001, VA002, VA003...  → Vendedora VA
XX001, XX002, XX003...  → Usuario prueba
```

El script detecta el prefijo más alto existente y genera el siguiente automáticamente al ingresar un producto nuevo.

---

## ➕ Agregar un vendedor nuevo

1. **Google Sheets** → crear hojas `INVENTARIO_VA` y `VENTAS_VA` con los encabezados correspondientes
2. **Copiar** `xx-index.html` → `va-index.html` y cambiar `const PREFIJO = 'XX'` por `const PREFIJO = 'VA'`
3. **Copiar** `xx-reportes.html` → `va-reportes.html` y cambiar el prefijo igual
4. **Actualizar links internos** en ambos archivos (`va-index ↔ va-reportes`)
5. **Agregar tarjeta** en `index.html` en la sección `vendedores-grid`
6. **Subir** los archivos nuevos a Vercel

---

## 💳 Métodos de pago

| Método | Estado |
|---|---|
| 💵 Efectivo | ✅ Activo |
| 🏦 Transferencia | ✅ Activo — QR alias `naturalezailustrada` |
| 💳 Débito / Posnet | ✅ Activo (registro manual) |
| 📱 QR Mercado Pago | ⏳ Pendiente — requiere API token |

---

## 🚀 Deploy

El sistema está deployado en **Vercel**:
```
https://naturalezailustrada.vercel.app
```

Entrada principal:
```
https://naturalezailustrada.vercel.app/index.html
```

---

## 🛠️ Tecnologías

- HTML + CSS + JavaScript vanilla — sin frameworks
- Google Sheets como base de datos
- Google Apps Script como API backend
- QRCode.js para generación de QR
- Vercel para hosting estático
- Fuentes: Playfair Display + DM Sans (Google Fonts)

---

## 📌 Notas importantes

- La planilla **VENDEDORES LUPINO** es la única fuente de verdad — no editar datos directamente salvo correcciones puntuales
- Las **ventas no se borran** — son el registro histórico sagrado del negocio
- El inventario es orientativo, se ajusta con el uso
- Columnas H e I en INVENTARIO están **reservadas** para funcionalidades futuras — no eliminar
- El usuario `XX` es solo para pruebas — sus datos pueden borrarse sin consecuencias

---

*Sistema desarrollado para Lupino · Bariloche, Argentina · 2026*
