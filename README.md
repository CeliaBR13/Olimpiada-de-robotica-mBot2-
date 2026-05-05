# Olimpiada-de-robotica-mBot2-
Este es el repositorio público para la olimpiada de robótica de la división de mBot2 del Colegio Cedes. En ella se recogen los diversos pasos a seguir, el diseño del robot y el código utilizado para completar la tarea dada.

Para realizar esta tarea, hemos necesitado los siguientes sensores y actuadores (también incluidos en el documento "Memoria Técnica").

-1 sensor qRGB, incluido con el kit de mBot2

-1 sensor infrarrojo, incluido con el kit de mBot2

-1 sensor de llama (utilizado en la tercera fase), externo

-2 motores de rotación continua, para las ruedas, incluidos con el kit de mBot2

-1 motor de rotación continua, externo

FASE 1
Para la primera fase, se decidió crear dos variables: una para cuando el mbot2 detectara una línea negra (detectada como azul, debido a su calibración sobre el fondo para solucionar una de las limitaciones de la tercera prueba), y otra para cuando el mbot2 detectara una línea azul (detectada como cyan, por la misma razón). El robot se dirige por el lado izquierdo de las "plantaciones", representados mediante las líneas verdes. Para ello, utilizamos el sensor Quad RGB, que al tener 4 sensores, lo que nos permitió controlar la dirección en la que se mueve el robot y controlar con alta precision la ubicacion de la linea.

FASE 2
En la segunda fase, utilizamos el sensor qRGB para seguir la línea y también el sensor infrarrojo para saber dónde está la alpaca de paja.

Primero, nuestro mBot2 sigue la línea negra. Cuando el sensor Quad RGB externo encuentra la línea roja, la sigue y recoge la alpaca que corresponde a esa línea. Luego, vuelve a encontrar la línea negra y la sigue hasta llegar al lugar donde se entregan las alpacas, y allí hace una maniobra para dejarla.

Luego, hace lo mismo con la línea verde: la encuentra, la sigue, recoge la alpaca y vuelve a la línea negra para ir al lugar de entrega, donde la deja con la misma maniobra.

Igualmente, repite el proceso con las líneas azul y amarilla. Para la alpaca amarilla, el robot sigue la línea, recoge la alpaca y da vueltas sobre sí mismo para volver a la línea negra y poder llevarla a su lugar de entrega.

Finalmente, como la última alpaca está en un lugar sin líneas en el suelo, usamos el sensor de ultrasonidos para encontrarla y llevarla al lugar blanco.

FASE 3
Para la última fase también tuvimos que utilizar el sensor qRGB, y tuvimos que incluir un sensor de llamas para detectar el incendio, y un motor de rotación continua para apagarlo. Primero, después de seguir la línea negra y cambiar a seguir la línea azul, pasa a detectar si la vela está encendida. Si estuviera encendida, la apaga y continúa hacia la línea amarilla, y si está apagada, pasa directamente a la línea amarilla. Con la transición de amarillo-rojo pasa igual, pero, al finalizar el recorrido, realiza un giro de (-)º, y se dirige hacia donde está la vela en la circunferencia blanca. Aquí nos guiamos únicamente por la luz de la vela, debido a que, como realizamos la calibración sobre el fondo (si se calibraba sobre un fondo blanco, el fondo de la lona lo detectaba como rojo, por lo que al llegar al cambio de amarillo-rojo se perdía).

El programa está dividido en fases. En la fase 0 sigue la línea negra hasta llegar a la azul; en la fase 1 gira hacia la línea azul hasta que el sensor qRGB detecte "azul" (cyan, por la calibración), con todos los sensores y luego detecta si hay un incendio. Si hubiera, lo apaga y continúa hacia la fase 2, y si no lo hubiera, simplemente sigue a la siguiente fase; en la fase 2, hace la transición "azul"-amarillo, y cuando detecta algo de amarillo, pasa a la siguiente fase; en la fase 3, repite el mismo proceso que en la fase 1, pero sobre el amarillo; en la fase 4, hace la transición amarillo-"rojo" (morado, por la calibración); en la fase 5 realiza todos los pasos idénticos a la fase 1, pero cuando detecta "rojo" con todos los sensores, se frena, haya detectado vela o no. Después de haber detectado y apagado la vela, o de no haber detectado nada, pasa a la fase 6; en la fase 6, el robot gira 66º, para dirigirse hacia la vela aislada, y se mueve en línea recta. Después de detectar el incendio en la vela aislada, la apaga.

Como módulos, utilizamos:

-event

-cyberpi, para poder programar con el controlador de cyberpi

-mbuild, para poder controlar los sensores que vienen con el kit de mBot2 y los externos

-mbot2, para poder controlar los motores que vienen con el kit de mBot2 (utilizados a la vez, y controlados mediante mbot2.drive.speed) y los externos (interpretados en el código como "M1", sólo utilizado en la tercera fase)

PROBLEMAS DETECTADOS A LO LARGO DE LAS FASES

-Error en la calibración: De vez en cuando, el robot no detectaba los colores correctamente. SOLUCIÓN: Volver a calibrar el mBot2, con el programa de ejemplo de "Color Line Follow".

-Error en la detección del color correcto del fondo: Si se calibraba el mBot2 sobre un fondo blanco, el fondo lo detectaba de color rojo. Esto no suponía ningún problema en la fase 1, pero al llegar a las fases 2 y 3 y tenía que seguir una línea blanca, se perdía. SOLUCIÓN: Calibrar el mBot2 sobre el fondo, así no tiene ningún problema a la hora de detectar la línea roja.

-Error a la hora de recoger las alpacas de paja de la fase 2: Al tratar de recoger las alpacas de paja en la fase 2, los brazos que fueron impresos las empujaban, en vez de recogerlas. SOLUCIÓN: Cortar parte de los brazos (aprox. 5 cm), para que no molestaran a la hora de girar.

-Error en el funcionamiento del ventilador: Al finalizar el código de la tercera prueba, el ventilador no se encendía, debido a un cortocircuito. SOLUCIÓN: Volver a montar el ventilador, arreglando los cables mal conectados.
