[< Regresar al Índice](README.md)

<br />

Tabla de Contenidos
- [1. Introducción](#1-introducción)
- [2. Mangos y Reducciones](#2-mangos-y-reducciones)
- [3. Gramática de Operadores](#3-gramática-de-operadores)
  - [3.1. Elección de Mangos](#31-elección-de-mangos)
- [4. Análisis LR(0)](#4-análisis-lr0)
  - [4.1. Estados del Análisis Ascendente](#41-estados-del-análisis-ascendente)
- [5. Tabla](#5-tabla)
  - [5.1. Armar tabla](#51-armar-tabla)
    - [5.1.1. ir\_A](#511-ir_a)
    - [5.1.2. Reducciones](#512-reducciones)
    - [5.1.3. Desplazamiento](#513-desplazamiento)
    - [5.1.4. Aceptación](#514-aceptación)



# 1. Introducción
Análisis sintáctico por *desplazamiento* y *reducción*, también se conoce como análisis de tipo **LR**.

En este tipo de análisis, las derivaciones se hacen primero por la **derecha** (a diferencia del análisis sintáctico descendente).

# 2. Mangos y Reducciones

Los mangos son subcadenas que concuerdan con el lado derecho de una producción, su reducción al no terminal es el **paso inverso** de una **derivación por la derecha**.

Una **reducción** es la operación inversa de una **derivación**.

**Ejemplo**

Suponiendo la siguiente gramática

$$
S \to aABe
$$

$$
A \to Abc | b
$$

$$
B \to d
$$

Reducción (operación inversa de las derivaciones) de la cadena `abbcde` hasta $S$.
- a**b**bcde
- a**A**bcde
- aAde
- aABe
- S

Que corresponde a la operación inversa de la siguiente derivación:

$$
S \to aABe \to aAde \to aAbcde \to abbcde
$$

> NOTA: Este tipo de análisis sintáctico no funciona bien en gramáticas no factorizadas y recursivas


# 3. Gramática de Operadores

No se pueden producir 2 no terminales juntos

Se usan para determinar el uso de operadores dentro del lenguaje. Como los operadores tienen una jerarquía, se especifica su precedencia con los siguientes símbolos.

Menos precedencia 
$$
\lessdot
$$

Misma precedencia
$$
\dot =
$$

Más precedencia
$$
\gtrdot
$$

## 3.1. Elección de Mangos

**Ejercicio**

Considerando esta tabla de precedencia

||id|+|*|$|
|-|-|-|-|-|
|id||$\gtrdot$|$\gtrdot$|$\gtrdot$|
|+|$\lessdot$|$\gtrdot$|$\lessdot$|$\gtrdot$|
|*|$\lessdot$|$\gtrdot$|$\gtrdot$|$\gtrdot$|
|$|$\lessdot$|$\lessdot$|$\lessdot$||

Evalua la siguiente cadena

$ id + id * id $

Suponiendo la gramática

$$
E \to E + E \to E * E \to (E) | id
$$

--- 

Se evalúan las precedencias entre cada elemento

$$
\$ \lessdot id \gtrdot + \lessdot id \gtrdot * \lessdot id \gtrdot \$
$$

**Identificar Mangos**

Se encuentra el primer $\gtrdot$ y se regresa hasta el primer $\lessdot$, lo que esté en medio es el mango.

$$
\lessdot \to id \leftarrow \gtrdot
$$

Reemplazamos los mangos por E

$$
\$ \lessdot E \gtrdot + \lessdot E \gtrdot * \lessdot E \gtrdot \$
$$

Quitamos los $E$ y evaluamos las precedencias de nuevo

$$
\$ \lessdot + \lessdot  *  \gtrdot \$
$$

Reemplazamos $\lessdot * \gtrdot$ por $E$ (producción $E \to E * E$)

$$
\$ \lessdot +  \gtrdot \$
$$

Reemplazamos $\lessdot + \gtrdot$ por $E$ (producción $E \to E + E$)

(Aunque no pongamos E porque estamos evaluando la gramática de los operadores unicamente.)

$$
\$  \$
$$

# 4. Análisis LR(0)

Una prouducción LR(0) tiene un punto en cierta posición

$$
A \to \cdot XYZ
$$

## 4.1. Estados del Análisis Ascendente

- **Desplazar:** Mover el siguiente símbolo de la cadena de entrada a el conjunto de símbolos (columna de símbolos).
- **Reducir:** Sustituir símbolos en la columna de símbolos por un no terminal de la gramática.
- **Aceptar:** Se terminó el análisis sintáctico de manera satisfactoria.
- **Error:** Se encontró un error en el programa.

![ejemplo analisis sint ascendente](assets/analisisis-sint-acendente.png)

# 5. Tabla

1. Gramática extendida

$$
E \to \dots
$$

Extendida

$$
E' \to E
$$

$$
E \to \dots
$$

2. Estados

- Expandir gramática
- Si es estado 0 $I_0$
  - Poner punto en la primer posición de la primer producción
- Si es cualquier otro estado $I_n$
  - Tomar el siguiente estado no completado y desplazar el punto
- Si el punto queda a la izquierda de un no terminal $S$
  - Poner todas las producciones de $S$ con un punto antes. (Cerradura)
- Si hay otra producción en la que se tiene un punto antes del mismo no terminal $S$
  - Agregar esa producción (con el punto desplazado) al estado (y marcar esa proudcción como completada)

## 5.1. Armar tabla

### 5.1.1. ir_A
En los estados, si hay un estado $I_n$ en el que exista una producción con punto - no terminal ($\cdot A$).

Buscar en qué otro estado $I_m$ aparece ese no terminal, seguido por un punto ($A \cdot$).

**En la tabla**

Poner en $m$ en la intersección de $n$ con $A$.


### 5.1.2. Reducciones

Sacar primeros y siguientes

Numerar producciones de la gramática expandida (sin OR | )

Si un estado $I_n$ tiene una producción con el punto hasta el final ($A \to B \cdot$), buscar el número de producción $p$ que es igual a la producción encontrada.

**En la tabla**

Poner $R_p$ en todos los cruces de $n$ con $Siguiente(A)$

### 5.1.3. Desplazamiento

Si un estado $I_n$ tiene una producción con punto - terminal ($\cdot a$).

Buscar en qué otro estado $I_m$ aparece una proudcción con ese terminal, seguido por punto ($a \cdot$).

**En la tabla**

Poner $d_m$ en la intersección de $n$ con $a$.


### 5.1.4. Aceptación

Si un estado $I_n$ tiene una producción con el símbolo inicial con el punto hasta el final $E' \to E \cdot$.

**En la tabla**

Poner $accept$ en el cruce de $n$ con $  en la tabla.
