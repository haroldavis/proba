# Análisis de subvenciones por el Ayuntamiento de Barcelona

1. Descripción

Tenemos una base de datos con información de subvenciones económicas hacia personas que lo solicitan \n
estas subvenciones la otorgan diferentes instituciones de gobierno de Barcelona.

2. Preprocesamiento

Obvervé las siguiente variables:

| Variables |
| ------------------- | 
| Entidad Municipal |
| Organo Gestor |
| Beneficiario |
| NIF_CIF |
| Tipología de Subvención |
| Código de subvención |
| Objeto |
| Fecha de convocatoria |
| Fecha de otorgamiento |
| Importe solicitado |
| Importe Proyectado |
| Importe otorgado inicial |
| Importe Reintegrado|

- Al recorrer las variables, no encontré filas duplicadas,encontré valores nulos, errores ortográficos, valores negativos, outlaiers, fecha sin formato mucha de la información se podría manejar mejor con una feedback del administrador  de los datos, pero al no ser posible, asumí algunos argumentos en base a los datos encontrados.

- Revisando a detalle las varibles _Beneficiario_ y _NIF_CIF_ son variables que puede ser reemplazada por solo una, en este caso la que tiene mejor performance es _NIF_CIF_ ya que la otra variable tiene mucha información repetida, pudiendo causar confusiones en las conclusiones.

- Respecto a las fechas, muchas filas no lo tienen pero la información de cada fila es importante, solo fue sustituída por un **NAT** para poder generar una nueva variable: _Diferencia_de_días_ que es la diferencia desde la _fecha de convocatoria_ hasta la _fecha de otorgamiento_ y así también las de valor negativo se eliminaron, poque no tiene sentido de que otorgen subvención antes de una convocatoria.

- Al observar outlaiers en las varibles numéricas, decidí poner un límite de 10000. perdiendo solo un 4% de datos aprox.

- Después de tener un dataset limpio y coherente, inicié a buscar insights.


3. Preguntas propuestas

    3.1 ¿Que institución recibió más subvenciones, en base a la cantidad de códigos de subvención?(Por entidad municipal y por organo gestor) 
    3.2 ¿ Qué institución recibió mayo suma de dinero? (por entidad municipal y por organo gestor)
    3.3 ¿ Cuántas personas y/o personas jurídicas(empresas,instituciones) solicitaron subvención por organo gestor?
    3.4 ¿ Cuántas personas y/o personas jurídicas(empresas,instituciones) reciben más de un códido de subvención?

    * Preguntas resueltas en el análisis

4. Modelo 

    El problema propuesto es generar un presupuesto  proyectado mas eficiente en base a la información obtenida y futura información anual para así distribuir mejor los recursos.

    El modelo por el que me decanté fue por el de Regresión lineal, pero luego de una competición de modelos, el ganador es Random Forest Regressor. Mi métrica que use para comparar fue el MSE. 