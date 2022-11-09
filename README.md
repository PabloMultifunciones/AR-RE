# AR-RE
Aprendizaje Reforzado - Reward Enginering y porque es importante
### Introduccion ###

Una de las cosas esenciales en todos los agentes de gradiente de políticas es cómo trabajamos con la recompensa. De la recompensa, la función depende de qué tan bien estará aprendiendo nuestro Modelo. Este es un ejemplo de cómo se verían nuestras recompensas en nuestro juego de pong:  

[0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, -1.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0]  

Entonces, las recompensas son en su mayoría cero y, a veces, podemos ver 1 o -1 en la lista. Esto se debe a que el entorno nos da una bonificación cuando la pelota pasa a través de un oponente o de nosotros. Cuando la pelota pasa por nuestra paleta, perdemos y obtenemos una recompensa de -1, y cuando el oponente no logra atrapar la pelota, ganamos y obtenemos un +1.  

Si entrenamos nuestra red con esta recompensa, no aprende nada porque la recompensa es la mayor parte del tiempo cero. En este caso, el agente no recibe retroalimentación sobre lo que es bueno o malo. La mayoría de los gradientes se convertirían en cero porque la función de pérdida utiliza la multiplicación de recompensas. El entorno nos premia justo cuando la pelota pasa por nuestra pala (puntuamos -1) o por la pala de nuestro adversario (puntuamos +1).  

Ahora piénsalo:  

Nuestra paleta se mueve hacia arriba y hacia abajo, golpea la pelota y viaja hacia el lado izquierdo de la pantalla. El oponente no logra atraparlo, y ganamos y obtenemos una puntuación de uno. En este escenario, ¿qué acciones fueron buenas?  

1. ¿La acción que tomamos cuando golpeamos la pelota?
2. ¿La acción que tomamos cuando obtuvimos una puntuación de 1?

Por supuesto, la primera opción es correcta. La segunda opción es incorrecta porque no importa nuestra acción cuando la pelota está llegando al oponente. Solo la acción que tomamos para golpear la pelota fue importante para ganar. Todo después de golpear la pelota fue irrelevante para nuestra victoria. (Se puede discutir un argumento algo similar: perder las acciones cercanas cuando obtuvimos una puntuación de -1 es más crítico que las acciones realizadas muchos pasos antes).  

Así que aquí está el truco. Establecemos la recompensa de las acciones realizadas antes de cada recompensa, similar a la recompensa obtenida. Por ejemplo, si obtuvimos una recompensa +1 en el tiempo 200, decimos que la recompensa del tiempo 199 es +0,99, la recompensa del tiempo 198 es +0,98, y así sucesivamente. Con esta definición de recompensa, tenemos las recompensas por acciones que resultaron en un +1 o -1. Suponemos que cuanto más reciente es la acción de la recompensa obtenida, más crítica es.  
