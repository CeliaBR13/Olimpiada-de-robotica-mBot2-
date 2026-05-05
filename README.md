# Olimpiada-de-robotica-mBot2-
Este es el repositorio público para la olimpiada de robótica de la división de mBot2 del Colegio Cedes. En ella se recogen los diversos pasos a seguir, el diseño del robot y el código utilizado para completar la tarea dada.

Para realizar esta tarea, hemos necesitado los siguientes sensores y actuadores (también incluidos en el documento "Memoria Técnica").

-1 sensor qRGB, incluido con el kit de mBot2

-1 sensor infrarrojo, incluido con el kit de mBot2

-1 sensor de llama (utilizado en la tercera fase), externo

-2 motores de rotación continua, para las ruedas, incluidos con el kit de mBot2

-1 motor de rotación continua, externo

FASE 1
Para la primera fase, se decidió crear dos variables: una para cuando el mbot2 detectara una línea negra (detectada como azul, debido a su calibración sobre el fondo para solucionar una de las limitaciones de la tercera prueba), y otra para cuando el mbot2 detectara una línea negra (detectada como cyan, por la misma razón). El robot se dirige por el lado izquierdo de las "plantaciones", representados mediante las líneas verdes. Para ello, utilizamos (-), lo que nos permitió controlar la dirección en la que se mueve el robot.

FASE 2
Para la segunda fase tuvimos que utilizar, además del sensor qRGB para seguir la línea, el sensor infrarrojo, para detectar dónde está la alpaca de paja. (-)

FASE 3
Para la última fase también tuvimos que utilizar el sensor qRGB, y tuvimos que incluir un sensor de llamas para detectar el incendio, y un motor de rotación continua para apagarlo. Primero, después de seguir la línea negra y cambiar a seguir la línea azul, pasa a detectar si la vela está encendida. Si estuviera encendida, la apaga y continúa hacia la línea amarilla, y si está apagada, pasa directamente a la línea amarilla. Con la transición de amarillo-rojo pasa igual, pero, al finalizar el recorrido, realiza un giro de (-)º, y se dirige hacia donde está la vela en la circunferencia blanca. Aquí nos guiamos únicamente por la luz de la vela, debido a que, como realizamos la calibración sobre el fondo (si se calibraba sobre un fondo blanco, el fondo de la lona lo detectaba como rojo, por lo que al llegar al cambio de amarillo-rojo se perdía).

El programa está dividido en fases. En la fase 0 sigue la línea negra hasta llegar a la azul; en la fase 1 gira hacia la línea azul hasta que el sensor qRGB detecte "azul" (cyan, por la calibración), con todos los sensores y luego detecta si hay un incendio. Si hubiera, lo apaga y continúa hacia la fase 2, y si no lo hubiera, simplemente sigue a la siguiente fase; en la fase 2, hace la transición "azul"-amarillo, y cuando detecta algo de amarillo, pasa a la siguiente fase; en la fase 3, repite el mismo proceso que en la fase 1, pero sobre el amarillo; en la fase 4, hace la transición amarillo-"rojo" (morado, por la calibración); en la fase 5 realiza todos los pasos idénticos a la fase 1, pero cuando detecta "rojo" con todos los sensores, se frena, haya detectado vela o no. Después de haber detectado y apagado la vela, o de no haber detectado nada, pasa a la fase 6; en la fase 6, el robot gira (-)º, para dirigirse hacia la vela aislada, y se mueve en línea recta. Después de detectar el incendio en la vela aislada, la apaga.

Como módulos, utilizamos:

-event

-cyberpi, para poder programar con el controlador de cyberpi

-mbuild, para poder controlar los sensores que vienen con el kit de mBot2 y los externos

-mbot2, para poder controlar los motores que vienen con el kit de mBot2 (utilizados a la vez, y controlados mediante mbot2.drive.speed) y los externos (interpretados en el código como "M1", sólo utilizado en la tercera fase)
