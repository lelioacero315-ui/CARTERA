# Conciliador — Conciliación bancaria y gestión de cartera

Aplicación web para el área de cartera: concilia el movimiento bancario contra el libro auxiliar, hace seguimiento de la cartera y genera los informes en Excel.

**Versión actual: 3.8**

**Abrir la aplicación:** https://lelioacero315-ui.github.io/CARTERA/

\---

## Módulos

### 🏦 Bancos

* **Entradas (conciliación diaria):** cruza el extracto bancario (PDF, Excel o CSV) con el libro auxiliar de recibos de caja.
* **Salidas (proveedores)** y **Notas crédito**.

### 📂 Cartera

* **Proyección semanal:** se carga el informe de cartera del sistema una sola vez y se obtiene el recaudo esperado por semana (lunes a domingo) y por línea de negocio. Cada factura se puede marcar como *Cancelada* o *Abono parcial* con su fecha de pago, y el cuadro se actualiza solo.
* **Control de asesores:** cartera de cada canal de venta frente a su condición de pago (contado, crediexpress, crédito), con la lista de cobro de las facturas fuera de condición.
* **Movimiento mensual:** cartera inicial + ventas − recaudo − notas crédito = cartera teórica, frente a la real.
* **Estado y edades**, **Análisis financiero** y **Gestión y cruce 1305**.

### 🏥 Módulo EPS

Seguimiento de la cartera de una EPS con tratamiento especial.

### 📊 Reportes

Panel de reportes e informe semanal.

### ⚙️ Configuración

Seguridad y respaldos, bitácora y el manual **"Cómo funciona"**.

\---

## Cómo concilia

Cada partida queda con un color:

|Color|Significado|
|-|-|
|🔵 Azul|Conciliado: el banco y el libro coinciden|
|🟠 Naranja|Está en el banco, pendiente de aplicar en libros|
|🟣 Morado|Está en libros, sin movimiento bancario: revisar|

La app intenta los cruces en este orden, y siempre sobre lo que quedó pendiente:

1. **Exacto:** mismo valor y fecha cercana. La fecha del pago también se lee del detalle del recibo ("AGOSTO 04", "AGO 04", "4 DE AGOSTO", "04/08").
2. **Por nombre:** el cliente se busca en el tercero y en el detalle, aunque el banco corte el nombre.
3. **Equivalencias de pagador:** cuando quien paga no es el cliente (por ejemplo, un giro directo). Se configuran en la app.
4. **Un pago, varios recibos:** un solo movimiento del banco que es exactamente la suma de varios recibos del mismo cliente.
5. **Pagos con tarjeta por pasarela:** el banco recibe menos que el recibo por las retenciones y la comisión. Estos cruces quedan marcados **VERIFICAR**, con el porcentaje y el valor descontado.

Además:

* **Conciliar a mano:** se seleccionan partidas naranja y morado y se unen. Si hay diferencia, la app exige escribir el motivo.
* **Deshacer:** cualquier cruce se puede revertir con el botón ↩.
* **Sin duplicados:** lo ya conciliado queda bloqueado. Si se vuelve a cargar el mismo extracto, no se repite.
* Todo queda registrado en la **bitácora**.
* **Excel de conciliación:** una hoja de entradas, salidas y gastos por banco. La columna Estado muestra los mismos tres resultados de la app: CONCILIADO, NO CONCILIADO y REVISAR (en salidas, PENDIENTE DE PAGO); las partidas anuladas por nota crédito dicen ANULADO.

\---

## Seguridad y datos

* **Los datos viven en el navegador del equipo donde se usa la app**, cifrados con **AES-GCM de 256 bits**. La clave se deriva de la contraseña con PBKDF2 (150.000 iteraciones).
* **Nada se envía a un servidor.** La única conexión que hace la app es consultar su propia página para avisar si hay una versión nueva.
* Acceso con **contraseña** y **código de recuperación**, más un **modo consulta** de solo lectura.
* **Borrado total:** solo desde Configuración › Seguridad › Zona de peligro, escribiendo ELIMINAR TODO.
* **Respaldos (.eabak):** si se borra el navegador o se cambia de equipo, los datos se pierden. Descargue respaldos con frecuencia y guárdelos fuera del equipo.
* ⚠️ **Este repositorio es público. Nunca suba aquí extractos, auxiliares, informes de cartera ni respaldos.** Solo va el código de la app.

\---

## Cómo actualizar la aplicación

1. Descargar un respaldo `.eabak` desde **Configuración**.
2. En este repositorio: **Add file → Upload files**, arrastrar el nuevo `index.html` y esperar a que llegue al **100 %**.
3. Hacer clic en **Commit changes**.
4. Comprobar que junto a `index.html` aparezca la fecha de hoy. Si muestra una fecha anterior, la subida no se completó.
5. Esperar unos 2 minutos, abrir el enlace con **Ctrl + F5** y confirmar que el encabezado muestre la **versión nueva**.

Los datos no se pierden al actualizar, porque están en el navegador y no en el archivo.

\---

## Aspectos técnicos

* Un solo archivo, `index.html` (unos 5,7 MB), sin servidor ni base de datos. También funciona abriéndolo con doble clic, sin internet.
* Librerías incluidas dentro del archivo: SheetJS 0.18.5 (Excel), ExcelJS 4.4.0 (informes con fórmulas), PDF.js 3.11.174 (extractos en PDF), JSZip 3 (gráficos nativos en Excel) y Chart.js 4.4.1 (gráficos en pantalla).
* Publicación: GitHub Pages.

## Historial de versiones

|Versión|Cambios principales|
|-|-|
|3.8|Navegación en 5 módulos; Proyección semanal de recaudo; Control de asesores; cruces nuevos (uno a varios, pasarela con VERIFICAR, más formatos de fecha); conciliación manual y deshacer; Excel de conciliación con estados correctos (REVISAR, PENDIENTE DE PAGO, ANULADO) y número de CE en salidas; borrado total solo desde la zona protegida; Banco de Occidente en la carga; corrección de botones duplicados; manual "Cómo funciona" actualizado|
|3.7|Versión anterior|

\---

**Eduardo Acero** · Contador Público · Especialista en Gerencia para Empresas de Salud

