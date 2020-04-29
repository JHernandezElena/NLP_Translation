# LSTM_GRU_Translation

Para esta práctica he probado diferentes modelos para la traducción de español a inglés. En el repo se encuentran los .ipynb ejecutados y carpetas comprimidas para los notebooks guardados en html, los modelos entrenados, y el dataset utilizado.

En el **notebook 1** pruebo un RNN, que es el modelo sequencial más simple que hemos aprendido. Con dos layers de SimpleRNN obtenemos un error de 1.68554, y traducciones bastante malas
El problema es que un RNN simple no es bueno para procesar frases largas como es nuestro caso. Por tanto, vamos a probar otro tipo de recurrent layers  que funcionan mucho mejor, como el LSTM y el GRU.


En el **notebook 2** hago una comparación básica entre LSTM (modelLSTM1.h1) y GRU (modelGRU.h1) con los mismos parámetros y la misma construcción del modelo construido con RNN en el notebook anterior.  Sorpendentemente, el GRU (error 1.72046) obtiene un error menor que LSTM (error 1.73903). Pero es aun sorprende más que ambos errores son mayores que lo obtenido en el notebook 1 con layers RNN.  Esto se puede deber a que estamos entrenando modelos muy poco complejos y restringiendo la cantidad de datos de entrada.
Como hemos visto en clase, GRU es un modelo un poco menos desarrollado que LSTM por tanto en los siguientes notebooks vamos a optimizar el modelo LSTM. Voy a construir modelos LSTM con mayor complejidad y aumentando los datos de entrada para conseguir reducir el error.


En el **notebook 3** túneo el modelo LSTM2 añadiendole una capa extra de LSTM y dos capas de Dropoout-0.2 para evitar sobre-entrenamiento.
Uso el mismo learning rate, batch y epochs que en el notebook 1 pero obtengo un mayor error (1.81399) y peores traducciones, por tanto hago ciertos ajustes:
- Disminuyo el learning rate para hacer que aprenda más lento
- Aumento el número de epochs para compensar la reducción del learning rate
- Aumento el batch size

Con este modelo LSTM3 tampoco mejoramos lo obtenido en el notebook uno ya que vuelve a crecer el error (1.88772) y las traducciones son peores. Esto se puede ver facilmente en la tabla final en la que comparamos las traducciones de ambos modelos LSTM2 y LSTM3. Quizá sea porque el modelo es demasiado complejo para los datos que tenemos


En el **notebook 4** entreno el modelo LSTM4 con los mismos parámetros que el LSTM2 pero con un dataset de entrada mayor pasando de 50.000 traducciones a 80.000 Con esto pretendo ver si el model era demasiado complejo para los datos y al añadir más datos de entrada quizá mejore. El error baja mucho hasta obtener 1.05608. Esta mejora es sustancial en el error y además también obtenemos mejores traducciones basadas en el contexto de la frase como podemos ver y se explica en las tablas finales.


En el **notebook 5** ajusto el modelo anterior para reducir el sobre-entrenamiento ya que la curva de error y de error de validación que se dibujan divergen mucho. Esto parece indicar que nuestro modelo no  generaliza bien, por ello, incremento el dropout en la última capa del modelo a 0.2 y reduzco el batch size a 320 para entrenar el modelo
LSTM5 y intentar conseguir mejorar el buen modelo obtenido en el notebook 3. Sin embargo, el error sube un poco (1.07117) y las traducciones no mejoran mucho.


En el **notebook 6**, visto que el reducir el batch empeora un poco el modelo, lo aumento a 448 para hacer la última prueba. Sin embargo el error (1.06087) vuelve a ser peor que en modelo LSTM4.


Por último, en el **notebook 7**, uso el ajuste del mejor modelo LSTM4 para traducir a la inversa, de inglés a español. Aunque el error sube a de 1.05608 para spa-to-eng a 1.26519 para eng-to-spa, hace un muy buen trabajo en la traducción, mejorando incluso la traducción dada en algunos casos. 

*Los resultados se comentan al final de cada notebook en mayor profundidad
