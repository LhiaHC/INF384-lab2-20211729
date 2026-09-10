# diagnostico
# Los cuatro defectos
- El defecto es que usa el archivo "requirements.txt" en lugar de "requirements.lock". Se encuentra en el archivo "pipeline.yml" en las líneas 23–26 y 53–56 y la consecuencia es que se pierde la reproducibilidad de dependencias. 
- El defecto es que no usa caché de dependencias. Se encuentra en el archivo "pipeline.yml", pasos de Python/instalación y la consecuencia es que se pierde eficiencia y el pipeline demora más.                      
- El defecto es que Sonar analiza, pero el Quality Gate no bloquea. Se encuentra en el archivo "pipeline.yml" en las líneas 31–39 y la consecuencias es que se pierde la garantía de detener código que no cumple calidad.      
- El defecto es que "publicar" no depende de "validar", no restringe "main" y usa nombre fijo. Se encuentra en el archivo "pipeline.yml" en las líneas 41–66 y la consecuencia es que se pierde la garantía de publicar solo código validado y versionado. 

# El defecto que explica la duración
La principal razón es la falta de caché, ya que las dependencias se descargan nuevamente en cada ejecución. La línea base medida es en promedio 55 s. La caché busca reducir ese tiempo.

# El vínculo con su caso

El defecto relacionado con nuestro caso es la falta de integración continua, porque ataca la restricción del tiempo de espera para integrar cambios. 

# La métrica DORA
Las métricas DORA que se esperan mover son Lead Time for changes y Chane Failure Rate.

Las dos métricas que podemos aproximar sin despliegue son Lead Time for Changes y Change Failure Rate. Elegimos Lead Time for Changes, ya que buscamos reducir el tiempo del pipeline.


# Proxy
Lo que se va a medir y usaremos como proxy será la duración promedio del workflow.
Proxy = tiempo promedio de las ejecuciones -> 55 s (actual o la foto del "antes")
Compararemos el tiempo antes vs dsp de la correción.
