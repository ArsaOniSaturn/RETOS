# Problema Original

Actualmente, el sistema de ventas de nuestra tienda está "atado". Una sola función se encarga de todo el proceso, lo que genera Baja Cohesión: tenemos lógica de matemáticas mezclada con acceso a archivos y visualización de datos.

Si el dueño del negocio pide un cambio en los precios, o el equipo técnico decide cambiar la base de datos, tenemos que editar la misma clase una y otra vez, violando el principio SRP (Responsabilidad Única).

Siguiendo los estándares de High Cohesion, el equipo debe separar esta clase en partes independientes para que cada una solucione un problema concreto. Instrucciones: Crear una clase que solo haga cálculos (Lógica de negocio). Crear una clase que solo guarde datos (Persistencia). Crear una clase que solo gestione la comunicación/recibo (Notificación).




# Explicación de la solución

¿Dónde y cómo se aplican los principios?
SRP — Single Responsibility Principle
La pregunta clave del SRP es: ¿cuál es la única razón por la que esta clase debería cambiar?

SalesCalculator solo cambia si cambia la lógica matemática, por ejemplo si el IVA pasa de 19% a 21%, o si se agrega un nuevo tipo de descuento.
SalesRepository solo cambia si cambia dónde se guardan los datos, por ejemplo si pasas de una lista en memoria a una base de datos real.
SalesNotifier solo cambia si cambia cómo se le muestra la información al cliente, por ejemplo si en vez de print() quieres enviar un correo o un SMS.

Ninguna clase tiene más de una razón para cambiar. Eso es exactamente SRP.

High Cohesion — GRASP
La pregunta clave de High Cohesion es: ¿todos los métodos de esta clase trabajan juntos hacia el mismo objetivo?

En SalesCalculator, calcular_subtotal(), calcular_descuento() y calcular_total() todos giran alrededor de hacer cuentas. Están fuertemente relacionados.
En SalesRepository, guardar() y obtener_todas() los dos giran alrededor de manejar la colección de ventas. Uno guarda, el otro recupera, pero el tema es el mismo.
En SalesNotifier, imprimir_recibo() y notificar() los dos giran alrededor de comunicarle algo al usuario. El objetivo es siempre el mismo.


La conexión entre los dos principios
SRP y High Cohesion se refuerzan mutuamente. Cuando una clase tiene una sola responsabilidad, sus métodos naturalmente quedan cohesionados porque todos apuntan al mismo objetivo. Si una clase tuviera cálculos y notificaciones mezcladas, ni cumpliría SRP ni tendría alta cohesión.
