MODELADO Y VALIDACIÓN DE ARQUITECTURA






TALLER #1 - README








INTEGRANTES

ANGELICA MARIA VERGARA GRANADOS
CARLOS FRANCISCO CORZO CASTAÑEDA
JAVIER ANDRÉS CARRANZA BARRAGAN
CARLOS DAVID BERNAL PÉREZ

















DOCUMENTO ARQUITECTURA DE LA SOLUCION
"PAGO DE SERVICIOS PÚBLICOS" 
Versión	Fecha	Descripción de la modificación
1.0
	20/05/2018	Documento de arquitectura de la solución "Pago de servicios públicos", en donde se busca detallar y ajustar la arquitectura del sistema partiendo de un contexto y unas restricciones especificadas en el taller.




















































Tabla de Contenido

1.	Introducción	3
1.1 Objetivo	3
1.2 Definiciones, Acrónimos y Abreviaturas	3
1.3 Referencias	3
1.4 Alcance	3
2.	Contexto	4
2.1 Fundamentos de la solución	4
3.	Drivers de Arquitectura	4
3.1 Objetivos de la arquitectura de la solución	4
3.2 Requerimientos Funcionales Significativos	4
3.3 Restricciones	5































1.	Introducción
El presente documento proporciona una descripción de la arquitectura de la solución "Pago de servicios públicos". Pretende dar a entender a analistas, desarrolladores y arquitectos un punto de partida en el diseño y desarrollo de la aplicación, además de la divulgación de las decisiones arquitecturales tomadas de acuerdo al contexto de la solución y sus restricciones.

1.1 Objetivo
Este documento consta de los siguientes objetivos:
o	Servir como base para el análisis, construcción y evolución del sistema.
o	Proporcionar una descripción general del sistema al lector.
o	Justificar y describir las decisiones de arquitectura tomadas.
 
2.	Contexto
El Banco ABC está realizando varios proyectos de actualización tecnológica los cuales le permiten ofrecer sus productos financieros de manera más ágil y de esta manera responder a nuevas necesidades del mercado. 
El Banco acaba de firmar una alianza estratégica con diferentes proveedores de servicios públicos (Agua, Gas, Luz, Telefonía) o también llamados convenios, para permitir a los clientes del banco a través de los diferentes canales de servicio (Cajeros Automáticos, Cajero de Oficina, Teléfono, Portal Web, Aplicación Móvil) permitir el pago de los mismos. 
La solución de "Pago de servicios públicos" busca satisfacer la necesidad de integración entre los servicios de pago del banco ABC y los servicios expuestos por los convenios para el mismo fin. 
2.1 Decisiones arquitecturales de la solución

DECS_ARQ_1: Se utilizará el patrón arquitectural orientado a servicios de Domain Inventory ya que el servicio de pago para servicios públicos está altamente posicionado en el inventario de la empresa debido a su gran impacto en el negocio y su alta capacidad de reutilización por medio de los diferentes canales bancarios.
DECS_ARQ_2: Se realizará la implementación de los servicios bajo el principio de diseño Estandarizado del contrato de servicio con el fin de evitar que los consumidores estén acoplados a la implementación y aplicando el principio de Contract first para todos los servicios del inventario.
DECS_ARQ_3: Se hará la implementación de los servicios utilizando el lenguaje de programación node.js y .net core y usando el principio de diseño Composición de Servicios bajo la aproximación de orquestación, en donde un servicio coordinador se encargará de llamar al servicio de enrutamiento (Dispatcher) con el fin de consultar el convenio al que debe ser dirigida la petición y así tomar la decisión basado en los datos devueltos.
DECS_ARQ_4: Se implementará un Inventario de Servicios bajo la tecnología .NET con el fin de tener registrada la información de los diferentes servicios que se pueden utilizar y los datos necesarios para el posterior enrutamiento.
DECS_ARQ_5: Se implementará un servicio Dispatcher utilizando la tecnología .NET el cual se encargará de enviar las peticiones a un transformador de formatos si es necesario, y a su vez enviar la petición al servicio correspondiente.
DECS_ARQ_6: La implementación de los servicios está basada en el patrón Microservice Deployment al tratar a cada uno de los servicios utilizados como un objeto independientemente desplegable contribuyendo así a la autonomía del servicio.
DECS_ARQ_7: La implementación de los servicios está basada en el patrón Service Decomposition al realizar una descomposición de las diferentes funcionalidades que podría llevar a cabo un solo servicio entre distintos servicios más granulares.
DECS_ARQ_8: La implementación de la solución está basada en el patrón Data Format Transformation con el objetivo de dinámicamente transformar el formatod e los datos cuando sea necesario según el formato requerido por los servicios expuestos por los convenios.




3.	Drivers de Arquitectura
3.1 Objetivos de la arquitectura de la solución
La arquitectura solución del sistema de Pago de Servicios Públicos consta de los siguientes objetivos:
•	Permitir la inclusión de nuevos convenios de manera ágil.
•	Brindar la posibilidad de cambios paramétricos en el enrutamiento a nivel de servicios.
•	Permitir el pago de diversos servicios públicos para distintos convenios.
3.2 Requerimientos Funcionales Significativos

Los requerimientos funcionales arquitecturalmente significativos se listan a continuación:

•	Consulta de saldo a pagar.
•	Pago del servicio.
•	Compensación del pago.

3.3 Restricciones
Se enumeran a continuación las restricciones que mayor impacto tienen en la arquitectura:
•	Creación de un servicio basado en el patrón Intermediate Routing que realice enrutamiento basado en datos con el fin de enrutar las peticiones al tipo de servicio adecuado.
•	La composición de servicios (ya sea por orquestación o coreografía) no puede realizarse utilizando BPEL.
•	Creación de un inventario de servicios y registro de los mismos. 


