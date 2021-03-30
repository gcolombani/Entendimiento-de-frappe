# Entendimiento de Frappe / ERPNEXT
Documento de entendimiento de Frappe.

## ¿Qué es Frappe?
Frappe es un poderoso framework full stack escrito en python y javascript pensado desarrollar soluciones empresariales bajo el enfoque de ERP. Permite desarrollar y agregar al sistema aplicaciones (módulos) personalizadas dependiendo de los requerimientos especificos del negocio. A su vez, Frappe es una aplicación dentro de la caja de Frappe.

### ¿Qué es un ERP?
El término ERP se refiere a Enterprise Resource Planning, que significa “sistema de planificación de recursos empresariales”. Estos programas se hacen cargo de distintas operaciones internas de una empresa, desde producción a distribución o incluso recursos humanos.

### ¿Qué es una aplicación de Frappe?
Una aplicación Frappe vive dentro de la caja de Frappe y este soporta múltiples aplicaciones, se pueden ver como módulos de un software que se construye en base a estos, el primer ejemplo es Frappe, el segundo es ERPNEXT.

## ¿Qué es ERPNEXT?
ERPNEXT es una aplicación de Frappe (módulo) que incluye lo básico de un erp, como por ejemplo:
- Clientes
- Productos
- Inventario
- Entre otros

## ¿Qué es bench?
Bench es la interfaz de lineas de comando (cli) que nos permite trabajar con Frappe.

## ¿Qué es un Doctype?
Un Doctype es la manera en la cual Frappe maneja las entidades, puedes verlo como un modelo si estás acostumbrado al paradigma MVC.

## Cosas que debes tener en cuenta al trabajar con Frappe
- Frappe maneja la base de datos de un modo algo peculiar, las claves primarias de las tablas son los nombres (name) de estas.
- Las tablas en base de datos que corresponden a los Doctypes tienen la siguiente estructura <code>tabDoctypeName</code>, donde doctypeName es el nombre del doctype.
- Funciona con un paradigma excentrico el cual se puede ver como un tipo de MVC, pero cambiando un poco la terminología y el uso de las vistas. Los modelos serían Doctypes, los registros documents. Las vistas no se escriben, solo se configuran con los archivos JS de cada Doctype, las vistas se contruyen de manera estandar con esta configuración.
- Los Doctypes se crean desde la interfaz de Frappe o desde el código (Mucho más sencillo hacerlo desde la inmterfaz).
- Frappe permite proveer un website a los clientes que visiten el sitio y esta cara funciona diferente al resto del framework, es un poco complicado de personalizar sin cambiar las aplicaciones core (Frappe y ERPNEXT).

## Flujo de trabajo normal
Al trabajar con Frappe existen dos maneras adecuadas de hacerlo.

1. Se debe intentar siempre trabajar en aplicaciones fuera de Frappe y ERPNEXT, es decir, crerar aplicaciones y agregar los doctypes y la lógica de negocio específica.
Se debe trabajar en tu entorno local, luego subir los cambios al respositorio (merge request aprobado y mergeado), para finalmente jalar los cambios en el sevidor, pero al jalar los cambios estos deben ser aplicados con el bench.
- Si se hacen cambios en la estructura de los doctypes, se debe correr la migración <code>bench migrate</code>
- Si se hacen cambios en los archivos de javascript, se debe correr la construcción de los assets <code>bench build</code>

2. La otra manera que podemos emplear en casos muy muy extremos, donde no es posible agregar la logica de negocio en una aplicación a parte, es modificar el core de ERPNEXT o Frappe y crear un repositorio privado para guardar y mantener estos cambios y manejar las actualizaciones.
- Esta debe ser siempre la última opción.
- Se debe asignar el repositorio privado como origin y el de Frappe/ERPNEXT como upstream, para guardar en el origin nustra version y mantenerla actualizada jalando desde upstream (para esto se debe tener sumo cuidado)
- Se debe agregar al readme los archivos que se están modificando en esta version customizada de la aplicación.
Es necesario hacer incapie en que la segunda opción es en casos muy extremos, como un ejemplos de un caso que puede parecer extremo pero no lo es y su solución:
- Modificar la logica de js de algun doctype de una aplicación ajena. Para esto debes crear tu propia app y en los js de esta agregar la lógica que desees al modelo ajeno, por ejemplo un nuevo botón con una opción especifica para los productos. En el siguiente ejemplo se modifica la logica de la vista de las facturas pertenecientes a la aplicación de ERPNEXT sin tocar ERPNEXT: https://gitlab.com/rootstack/ERPNEXT-intfiscal/-/blob/master/intfiscal/public/js/account.js (puedes solicitar acceso a Alejandro Oses)
