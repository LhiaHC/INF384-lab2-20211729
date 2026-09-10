# Diagnóstico (parte 1)
# Los cuatro defectos
- El defecto es que usa el archivo "requirements.txt" en lugar de "requirements.lock". Se encuentra en el archivo "pipeline.yml" en las líneas 23–26 y 53–56 y la consecuencia es que se pierde la reproducibilidad de dependencias. 
- El defecto es que no usa caché de dependencias. Se encuentra en el archivo "pipeline.yml", pasos de Python/instalación y la consecuencia es que se pierde eficiencia y el pipeline demora más.                      
- El defecto es que Sonar analiza, pero el Quality Gate no bloquea. Se encuentra en el archivo "pipeline.yml" en las líneas 31–39 y la consecuencias es que se pierde la garantía de detener código que no cumple calidad.    
- El defecto es que "publicar" no depende de "validar", no restringe "main" y usa nombre fijo. Se encuentra en el archivo "pipeline.yml" en las líneas 41–66 y la consecuencia es que se pierde la garantía de publicar solo código validado y versionado. 

# El defecto que explica la duración
La principal razón es la falta de caché, ya que las dependencias se descargan nuevamente en cada ejecución. La línea base medida es en promedio 55 s. La caché busca reducir ese tiempo.

# El vínculo con su caso
El defecto relacionado con nuestro caso es la falta de caché de dependencias, porque incrementa el tiempo de validación de los cambios. En el VSM del Caso 1 se identificó una espera promedio de 4 días para acceder al ambiente de staging, evidenciando que los tiempos de espera son una restricción importante del flujo. 

# La métrica DORA
Las métricas DORA que se esperan mover son Lead Time for changes y Chane Failure Rate.
Las dos métricas que podemos aproximar sin despliegue son Lead Time for Changes y Change Failure Rate. Elegimos Lead Time for Changes, ya que buscamos reducir el tiempo del pipeline.

# Proxy
Lo que se va a medir y usaremos como proxy será la duración promedio del workflow.
Proxy = tiempo promedio de las ejecuciones -> 55 s (actual o la foto del "antes")
Compararemos el tiempo antes vs dsp de la correción.

# Cierre
# Medición posterior
La línea base fue de 55 s. Después de los cambios aplicados, el promedio fue de 77 s. El tiempo aumentó en 22 s, lo que corresponde a un aumento del 40%. Por lo tanto, el proxy no mejoró, debido a que el pipeline ahora incorpora validaciones adicionales como el quality Gate.

# Justificación de la versión
Se actualizó la versión de 1.2.0 a 1.2.1, correspondiente a un cambio de parche, porque los cambios realizados son correcciones y mejoras del pipeline sin cambios incompatibles en el proyecto.

# Lo que no se resolvió
El pipeline todavía no realiza un despliegue real. Para resolverlo sería necesario agregar una etapa de despliegue hacia un ambiente de producción.

# Declaración de uso de IA generativa
Se utilizó Gemini como herramienta de apoyo para comprender el significado y la sintaxis de algunas sentencias utilizadas durante el laboratorio en el archivo pipeline.yml, por ejemplo needs: validar, if: github.ref == 'refs/heads/main', la configuración de caché con cache: 'pip' y el funcionamiento del Quality Gate. Asimismo, para crear la función defectuosa de forma rápida. Finalmente, se utilizó para aclarar dudas sobre la estructura y formato de los archivos yaml.




