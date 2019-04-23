# specs-reqs
Propuesta de apoyo para revision de facturas _**Xml**_ Semi-Automaticamente

## Resumen:
Descripcion de propuesta para la implementacion de revision de los archivos _**Xml**_   que envian los proveedores via email al departamento de Adquisiciones del [Poder Judicial del Estado de Sonora](http://stjsonora.gob.mx/) .

## Contenido
1. Archivos del Proveedor:

   * `Archivo Excel` [pathprov.xlsx](https://github.com/jr-acosta/specs-reqs) `para`  direccionamiento del alacenamiento xml en Outlook `Office365` de la plataforma
   * `Archivo Excel` [xmlproveedor1.xlsx](https://github.com/jr-acosta/specs-reqs) `para` especificar que facturas se deben de extraer de Outlook `Office365`

2. Arhivos UI y acciones a seguir :

   * `Revision inicial` [Rev1.jpg](https://github.com/jr-acosta/specs-reqs) `para` verificar si el archivo del proveedor es valido en las facturas que decalra enviar a Outlook. 
   * `Validacion` [Rev2.jpg](https://github.com/jr-acosta/specs-reqs) `para` hacer revision exhaustiva a cada xml que el proveedor entrega con las reglas especificadas. 
   * `Actualizar Status` [Rev3.jpg](https://github.com/jr-acosta/specs-reqs) `para` actualizar la base de datos para posteriores revisiones futuras.

3. Reporte de Acciones :

   * `Reporte de outlook` [xml_outlook.md](https://github.com/jr-acosta/specs-reqs) `para`  detectar que facturas no han sido enviadas por parte del proveedor.
   * `Reporte de Incidencias en Validacion` [rev_incidencias.md](https://github.com/jr-acosta/specs-reqs) `para` filtrar todas las facturas que no se ajusten a las reglas de validacion especificadas.

4. Reglas de Validacion :

   * `Archivo con las reglas especificas` [rev_validar.md](https://github.com/jr-acosta/specs-reqs)  que estan bajo un concenso jurisdiccional, apropiadas para el procedimiento de trabajo que se realiza en el depto. Adquicisiones.


## Descripcion de Contenido
1. Archivos del Proveedor:

   * `Archivo Excel` [pathprov.xlsx](https://github.com/jr-acosta/specs-reqs) 

   ![Exel pathprov](/files/pathprov.JPG)
      ```sh
   En este archivo se especifica la estructura de folders dentro de outlook, la forma y manera de
   almacenar los archivos  "Xml"  y  "PDF"  de cada factura y que corresponda a su especifico
   proovedor organizado por meses y años. En este archivo tambien debe señalar opcionalmente su email.
   ```

   * `Archivo Excel` [xmlproveedor1.xlsx](https://github.com/jr-acosta/specs-reqs) 

   ![Exel xmlproveedor](/files/xmlproveedor1.JPG)
      ```sh
   Archivo con al relacion especifica de las facturas que el proveedor reclama para su pronto pago, en la
   imagen se puede visualizar que es de importancia especificar en la primera columna el "RFC" del 
   proveedor para que pueda ser localizado y procesado adecuadamente, todas las busquedas de sus facturas
   seran cotejadas por este dato de su  "RFC" ya que otros proveeedores pueden manejar similares 
   numeraciones y con este dato bien especificado podemos evitar errores en la busqueda de los archivos.
   ```

2. Arhivos UI y acciones a seguir :

   * `Revision inicial` [Rev1.jpg](https://github.com/jr-acosta/specs-reqs/files/Rev1.jpg)
   
   ![REV1](/files/Rev1.jpg)
   ```sh
   La revision inicial consiste en revisar el archivo de excel que envia el proveedor donde se especifica
   que facturas son mencionadas para exigir el pago por parte de esta institucion. si la factura que el
   proveedor menciona en su archivo no es encontrada en la bandeja de entrada de outlook, esta factura
   sera omitida por el sistema y las revisiones siguientes, esperando se incluya para los proximos lotes
   que el proveedor reclame.
   ```

   * `Validacion` [Rev2.jpg](https://github.com/jr-acosta/specs-reqs/files/Rev2.jpg) 

   ![REV2](/files/Rev2.jpg)
   ```sh
   En esta opcion se ejecutara de forma automatica la revision de las facturas que fueron encontradas
   en la bandeja de entrada de outlook, la revision incluye de forma automatica las reglas de revision.
   En este punto el operador/usuario no interviene solo espera el resultado.
   ```

   * `Actualizar Status` [rev3.jpg](https://github.com/jr-acosta/specs-reqs/files/Rev3.jpg) 

   ![REV3](/files/Rev3.jpg)
   ```sh
   En esta opcion se enviaran (a la base de datos para actualizar status) las facturas que fueron
   revisadas y cumplieron con las reglas de validacion tanto de forma automatica como de forma manual
   fisicamente por el operador, las facturas que no cumplieron con alguna regla seran separadas y se
   informara a proveedor el motivo.
   ```



3. Reporte de Acciones :

    * `Reporte de outlook` [xml_outlook.md](https://github.com/jr-acosta/specs-reqs/reportes/xml_outlook.md) 
   
   ```sh
   La finalidad de este reporte es cotejar las facturas que el proveedor señala en su "Archivo Excel"
   (xmlproveedor1.xlsx) que envio a outlook para que no falte algun archivo en su revision, en caso
   que falte un xml quedara fuera de revision.
   ```

   * `Reporte de Incidencias en Validacion` [rev_incidencias.md](https://github.com/jr-acosta/specs-reqsreportes/rev_incidencias.md)

   ```sh
   Este es el reporte mas imoprtante, con este  reporte se visualizara las facturas revisadas automaticamente
   separando todas aquellas facturas que no se ajusten a las reglas de validacion especificadas, cada factura
   que en su descripcion no alcanze un 82% de similitud contra la requisicion pasara a revision fisica manual,
   asi  se asegurara que el algoritmo de revision esta trabajando acorde a lo señalado en las reglas, una vez
   que el operador revisa fisicamente la factura podra señalarle al programa que integre la factura al
   siguiente proceso, de no ser asi sera rechazada.
   ```



4. Reglas de Validacion :

   * `Archivo con las reglas especificas` [rev_validar.md](https://github.com/jr-acosta/specs-reqs/validaciones/rev_validar.md)  
   
| Validacion                        | Descripcion de Validacion          |
| --------------------------------- | ---------------------------------- |
|Req-No.-Año| Revision del formato en archivo xml 5 digitos /diagonal Año en 4 digitos, esta validacion servira para posteriormente buscar la req. en bd|
|Repetido en Lote|Revisar que ninguna factura del lote del proveedor o otros proveedores tengan no. de requisicion repetida (que no se intente referenciar a una requisicion por parte de 2 facturas o mas en el proceso de revision) |
|Rev-Historial Status Rev-XML| Filtro de revision, que la requisicion no este en Status "Rev-Xml" , solo aceptar Status "entregada" y quiza otro status mas ya que el usuario tarda en modificar este status y el pago de la factura no debe detenerse por este motivo|
|No.de-Items Factura|Validar que la factura tenga el no. de items igual a la requisicion excluyendo los casos que se señalen por parte del depto. de requisiciones|
|Cantidades Mayores en Item|Validacion de las cantidades por Item en factura, el cual debe ser menor o igual al campo de cantidad autorizada en req.|
|Unidad de Medida Item|Verificar la unidad de medida por item, debe ser igual a la especificada en req., la cual se buscara standarizar en acuerdo con el proveedor|
|Parser en Descripcion Item mayor a 82%| Validacion de la descripcion del articulo, que debe ser igual a la requisicion o catalogo de licitacion, en los casos que difiera deben existir 2 filtros uno mayor al 65% de coinciencia y otro mayor al 82% , esto con el fin de ir ajustando estos porcentajes para minimizar el proceso manual de revision| 
|Verificar Catalogo de Licitacion |Con la validacion de la descripcion se revisara el catalogo de la licitacion donde se revisaran todos los articulos mayores a un 82% de coincidencia para validar el precio pactado del año en curso por parte de los proveedores en la revision|
|Historial Paso final |Modificar historial en BD requisiciones aceptadas automaticamente y manualmente , poner la requisicion en Status "Rev-Xml" para que no se pueda volver a referenciar la misma requisicion 2 veces en posteriores revisiones y validaciones|


xx ["Installation"] yy [The Book].

["Installation"]: https://github.com/jr-acosta/specs-reqs
[Book]: https://github.com/jr-acosta/specs-reqs