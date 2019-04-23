# Validaciones para el proceso de Verificacion Facturas Xml  

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
 
