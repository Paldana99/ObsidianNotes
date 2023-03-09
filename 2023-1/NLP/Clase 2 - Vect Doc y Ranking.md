
Cada documento es una sentencia, para poder vectorizarla
![[Pasted image 20230309153515.png]]

## BM25

Tf => Frecuencia del termino en el documento
Factor idf => Frecuencia inversa de documentos

![[Pasted image 20230309154008.png]]

Se utiliza para saber que tan relevante es un termino en el documento. Pero gracias al Idf puesto que es una frecuencia inversa, si el termino esta en muchos documentos a lo largo del corpus, entonces se vuelve menos relevante. 

## Ranking

Es hacerle una consulta y obtener un listado de documentos ordenados. Para esto es necesario contar con un score 

$$Q \rightarrow {d, ...}$$
![[Pasted image 20230309154451.png]]

Para crear una estructura de datos, usamos un indice invertido
Es invertido ya que ingresamos una palabra y este nos da el ID del documento en donde aparece. 
Podemos hacer un ordenamiento por orden alfabético para hacer búsqueda binaria.

Existe la busqueda conjuntiva, en donde se va a buscar los documentos existentes en cada termino, y hacer una interseccion para obtener los doc que tienen todas las palabras.
Pero hoy en dia se prefiere usar **union** y clasificar con ranking.


Para mejorar las consultas hoy en dia, se hace una query expansion, la cual preprocesa la consulta para enriquecerla. hace un parafrasis del query.