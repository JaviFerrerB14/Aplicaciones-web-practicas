# Escribe la version corregida

## Errores
Falta la etiqueta de cierre /html al final del documento.

La etiqueta head no se cierra correctamente con /head antes de abrir el body.

El título está mal cerrado: Se abrió con title pero se cerró mal antes del head (pone title Mi tienda de gadgets</head> en lugar de /title).

El encabezado h1 está mal cerrado: Se abrió con h1 y se cerró con un /h2 incorrecto.

En la frase b cancelación de ruido/p/b, las etiquetas están cruzadas de forma incorrecta. Debe cerrarse primero la etiqueta que se abrió último (en este caso, la b y luego el p).

## Correcion 

[!DOCTYPE html]

[html lang="es"]

[head]

    [meta charset="utf-8"]
    
    [title]Mi tienda de gadgets[/title]
    
[/head]

[body]

    [h1]Ofertas de otoño[/h1]
    
    [p]Auriculares con [b]cancelación de ruido[/b][/p]
    
[/body]

[/html]
