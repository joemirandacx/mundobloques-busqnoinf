# Solución al problema "El mundo de los bloques" utilizando Búsqueda no Informada.

## Situaciones

![Situacion Inicial y Final de los bloques](img/mundobloques.png)

## Formalización

Los cubos **verde**, **amarillo** y **rojo** serán representados con las letras **v**, **a** y **r** respectivamente.

El objetivo puede ser descrito como el estado de una pila ~~ubicado en la columna central~~.

La estructura que soporta el estado de la pila consta de **3** parametros. Cada parametro puede tomar uno de los siguientes valores:
- **0** para indicar que no tiene un cubo.
- **v**, **a** ó **r** para indicar el color del cubo.

### Formalización de los estados

-  **Estado Inicial :** (r,v,0)

-  **Estado Objetivo :** (v,a,r)

### Formalización de las acciones

Las acciones que se pueden aplicar sobre una pila son las de **apilar** y **desapilar**/**quitar** un elemento. Sin enmbargo, para este caso es necesario diferenciar el **color** del elemento y el **tamaño** de la pila. Entonces tendremos un total de **18** posibles acciones.

## Implementación

## Prueba de escritorio
