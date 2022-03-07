# Solución al problema "El mundo de los bloques" utilizando Búsqueda no Informada.

## Situaciones

![Situacion Inicial y Final de los bloques](img/mundobloques.png)

## Formalización

Los bloques **verde**, **amarillo** y **rojo** serán representados con las letras **v**, **a** y **r** respectivamente.

El objetivo puede ser descrito como el estado de una pila ~~ubicada en la columna central~~.

La estructura que soporta el estado de la pila consta de **3** parámetros. Cada parametro puede tomar uno de los siguientes valores:
- **0** para indicar que no tiene un bloque.
- **v**, **a** ó **r** para indicar el color del bloque.

### Formalización de los estados

-  **Estado Inicial :** (r,v,0)

-  **Estado Objetivo :** (v,a,r)

### Formalización de las acciones

Las acciones que se pueden aplicar sobre una pila son las de **apilar** y **desapilar**/**quitar** un bloque. Sin enmbargo, para este caso es necesario diferenciar el **color** del bloque y el **tamaño** de la pila. Entonces tendremos un total de **18** posibles acciones.

## Implementación

El siguiente código esta escrito utilizando el lenguaje Prolog.

```prolog
solucion(A):- sgte(e(r,v,0), [e(r,v,0)], V , [], A).

sgte(e(v,a,r),V,V,A,A).
sgte(e(X,Y,Z),Lv,V,La,A):-
	accion(e(X,Y,Z), e(Xs,Ys,Zs), Acc),
	not(pertenece(e(Xs,Ys,Zs), Lv)),
	writeln(Acc),
	sgte(e(Xs,Ys,Zs), [e(Xs,Ys,Zs)|Lv], V, [Acc|La], A).

pertenece(X,[X|_]):-!.
pertenece(X,[_|R]):-pertenece(X,R).

% Acciones:

% Quitar bloque verde
accion(e(v,0,0), e(0,0,0), 'quita bloque verde').
accion(e(X,v,0), e(X,0,0), 'quita bloque verde').
accion(e(X,Y,v), e(X,Y,0), 'quita bloque verde').

% Quitar bloque amarillo
accion(e(a,0,0), e(0,0,0), 'quita bloque amarillo').
accion(e(X,a,0), e(X,0,0), 'quita bloque amarillo').
accion(e(X,Y,a), e(X,Y,0), 'quita bloque amarillo').

% Quitar bloque rojo 
accion(e(r,0,0), e(0,0,0), 'quitar bloque rojo').
accion(e(X,r,0), e(X,0,0), 'quitar bloque rojo').
accion(e(X,Y,r), e(X,Y,0), 'quitar bloque rojo').

% Apilar bloque verde
accion(e(0,0,0), e(v,0,0), 'apilar bloque verde').
accion(e(X,0,0), e(X,v,0), 'apilar bloque verde'):- X\=v.
accion(e(X,Y,0), e(X,Y,v), 'apilar bloque verde'):- X\=v, Y\=v.

% Apilar bloque amarillo
accion(e(0,0,0), e(a,0,0), 'apilar bloque amarillo').
accion(e(X,0,0), e(X,a,0), 'apilar bloque amarillo'):- X\=a.
accion(e(X,Y,0), e(X,Y,a), 'apilar bloque amarillo'):- X\=a, Y\=a.

% Apilar bloque rojo
accion(e(0,0,0), e(r,0,0), 'apilar bloque rojo').
accion(e(X,0,0), e(X,r,0), 'apilar bloque rojo'):- X\=r.
accion(e(X,Y,0), e(X,Y,r), 'apilar bloque rojo'):- X\=r, Y\=r.
```

## Prueba de escritorio

```
abierta   = (r,v,0)
nodo      = (r,v,0)
sucesores = (r,0,0) (r,v,a)
---------------------------------------------------
abierta   = (r,0,0) (r,v,a)
nodo      = (r,0,0)
sucesores = (0,0,0) (r,a,0)
---------------------------------------------------
abierta   = (r,v,a) (0,0,0) (r,a,0)
nodo      = (r,v,a)
sucesores = no tiene uno válido
---------------------------------------------------
abierta   = (0,0,0) (r,a,0)
nodo      = (0,0,0)
sucesores = (v,0,0) (a,0,0)
---------------------------------------------------
abierta   = (r,a,0) (v,0,0) (a,0,0)
nodo      = (r,a,0)
sucesores = (r,a,v)
---------------------------------------------------
abierta   = (v,0,0) (a,0,0) (r,a,v)
nodo      = (v,0,0)
sucesores = (v,a,0) (v,r,0)
---------------------------------------------------
abierta   = (a,0,0) (r,a,v) (v,a,0) (v,r,0)
nodo      = (a,0,0)
sucesores = (a,v,0) (a,r,0)
---------------------------------------------------
abierta   = (r,a,v) (v,a,0) (v,r,0) (a,v,0) (a,r,0)
nodo      = (r,a,v)
sucesores = no tiene uno válido
---------------------------------------------------
abierta   = (v,a,0) (v,r,0) (a,v,0) (a,r,0)
nodo      = (v,a,0)
sucesores = (v,a,r)
---------------------------------------------------
abierta   = (v,r,0) (a,v,0) (a,r,0) (v,a,r)
nodo      = (v,r,0)
sucesores = (v,r,a)
---------------------------------------------------
abierta   = (a,v,0) (a,r,0) (v,a,r) (v,r,a)
nodo      = (a,v,0) 
sucesores = (a,v,r) 
---------------------------------------------------
abierta   = (a,r,0) (v,a,r) (v,r,a) (a,v,r) 
nodo      = (a,r,0)
sucesores = (a,r,v)
---------------------------------------------------
abierta   = (v,a,r) (v,r,a) (a,v,r) (a,r,v)
nodo      = (v,a,r) es meta/objetivo !
```

### Solución

-  **Estado Inicial :** (r,v,0)
-  **Estado Objetivo :** (v,a,r)

```
N°   Acción            Nuevo Estado
-----------------------------------
1.   Quitar verde    : (r,0,0)
2.   Quitar rojo     : (0,0,0)
3.   Apilar verde    : (v,0,0)
4.   Apilar amarillo : (v,a,0)
5.   Apilar rojo     : (v,a,r)
```
