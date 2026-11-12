# Explica y corrige 

Línea original: [h1 style="color:red font-size:40px;"]Directo esta noche[/h1]

    Qué falla: Las propiedades dentro del atributo style se separan obligatoriamente con un punto y coma ;. Aquí falta el punto y coma entre red y font-size.

    Corrección: [h1 style="color: red; font-size: 40px;"]Directo esta noche[/h1]

    Línea original: [p style="text-align=center;"]Estreno de temporada[/p]

    Qué falla: En CSS se usan dos puntos : para asignar valores, no el signo igual =. Debe ser text-align: center;.

    Corrección: [p style="text-align: center;"]Estreno de temporada[/p]

    Línea original: [p style="background-color:yellow;"]Sorteo de una tarjeta gráfica[p]

    Qué falla: La etiqueta de cierre del párrafo está mal escrita, ya que utiliza [p] en lugar de la barra de cierre [/p].

    Corrección: [p style="background-color: yellow;"]Sorteo de una tarjeta gráfica[/p]
