# Entendimiento de Frappe / ERPNEXT
Documento de entendimiento de frappe.

## ¿Qué es Frappe?
Frappe es un framework full stack escrito en python y javascript para desarrollar soluciones empresariales bajo el enfoque de ERP. Que además permite desarrollar y agregar al sistema aplicaciones (módulos) personalizados dependiendo de los requerimientos especificos del negocio. A su vez, Frappe es una aplicación dentro de la caja de Frappe.

### ¿Qué es un ERP?
El término ERP se refiere a Enterprise Resource Planning, que significa “sistema de planificación de recursos empresariales”. Estos programas se hacen cargo de distintas operaciones internas de una empresa, desde producción a distribución o incluso recursos humanos.

### ¿Qué es una aplicación de frappe?
Una aplicación frappe vive dentro de la caja de frappe y este soporta múltiples aplicaciones, se pueden ver como módulos de un software que se construye en base a estos, el primer ejemplo es Frappe, el segundo es ERPNEXT.

## ¿Qué es ErpNEXT?
Erpnext es una aplicación de frappe (módulo) que incluye lo básico de un erp, como por ejemplo:
- Clientes
- Productos
- Inventario
- etc

## ¿Qué es bench?
Bench es la interfaz de lineas de comando (cli) que nos permite trabajar con frappe.

## Cosas que debes tener en cuenta al trabajar con Frappe
- Frappe maneja la base de datos de un modo algo peculiar, las claves primarias de las tablas son los nombres (name) de estas.
- Las tablas en base de datos que corresponden a los Doctypes tienen la siguiente estructura <code>tabDoctypeName</code>, donde DoctypeName es el nombre del doctype.
- Funciona con un paradigma excentrico el cual se puede ver como un tipo de MVC, pero cambiando un poco la terminología y el uso de las vistas. Los modelos serían Doctypes, los registros docs. Las vistas no se escriben, solo se configuran con los archivos JS de cada Doctype, las vistas se contruyen de manera estandar con esta configuración.
- Los Doctypes se crean desde la interfaz de Frappe o desde el código (Mucho más sencillo hacerlo desde la inmterfaz).
- Frappe permite proveer un website a los clientes que visiten el sitio y esta cara funciona diferente al resto del framework, es un poco complicado de personalizar sin cambiar las aplicaciones core (Frappe y ERPNEXT).

## Flujo de trabajo normal
Al trabajar con Frappe existen dos maneras adecuadas de hacerlo.

1. Se debe intentar siempre trabajar en aplicaciones fuera de Frappe y ERPNEXT, es decir, crerar aplicaciones y agregar los doctypes y la lógica de negocio específica.
Se debe trabajar en tu entorno local, luego subir los cambios al respositorio (merge request aprobado y mergeado), para finalmente jalar los cambios en el sevidor, pero al jalar los cambios estos deben ser aplicados con el bench.
- Si se hacen cambios en la estructura de los doctypes, se debe correr la migración <code>bench migrate</code>
- Si se hacen cambios en los archivos de javascript, se debe correr la construcción de los assets <code>bench build</code>

2. La otra manera que solemos emplear en casos muy extremos, donde no es posible agregar la logica de negocio en una aplicación a parte, es modificar el core de ERPNEXT o Frappe y crear un repositorio privado para guardar y mantener estos cambios y manejar las actualizaciones.
- Esta debe ser siempre la última opción.
- Se debe asignar el repositorio privado como origin y el de Frappe/ERPNEXT como upstream, para guardar en el origin nustra version y mantenerla actualizada jalando desde upstream (para esto se debe tener sumo cuidado)
- Se debe agregar al readme los archivos que se están modificando en esta version customizada de la aplicación.

