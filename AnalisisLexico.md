[< Regresar al Índice](README.md)

# 1. Análisis Léxico

- [1. Análisis Léxico](#1-análisis-léxico)
  - [1.1. Conceptos básicos](#11-conceptos-básicos)
- [2. Proceso](#2-proceso)
- [3. Tabla de símbolos](#3-tabla-de-símbolos)
- [4. Reconocimiento de Tokens](#4-reconocimiento-de-tokens)
  - [4.1. Diagrama de Transición de estados](#41-diagrama-de-transición-de-estados)
  - [4.2. Reconocimiento de palabras reservadas e identificadores](#42-reconocimiento-de-palabras-reservadas-e-identificadores)
- [5. Autómatas Finitos](#5-autómatas-finitos)
  - [5.1. Construcción de AFN de una Expresión Regular](#51-construcción-de-afn-de-una-expresión-regular)
    - [5.1.1. Or](#511-or)
    - [5.1.2. Concatenación](#512-concatenación)
    - [5.1.3. Kleene](#513-kleene)


## 1.1. Conceptos básicos
- **Token:** Unidad léxica o atributo
- **Patrón:** Descripción de un lexema.
- **Lexema:** Secuencia de caracteres del programa fuente.

Analizador léxico obtiene **tokens** del código fuente. Los tokens salen de los lexemas contenidos en el código y que corresponden al lenguaje de programación.

|Código|Lexemas|Tokens|
|:--:|:--:|:--:|
|int num = 12;|int <br/> num <br/> =<br/> 12<br/>; | int -> reservada <br/>num -> id<br/>= -> =<br/>12 -> entero<br/>; -> reservada

Estos tokens se le dan al analizador sintáctico, el cual analiza que la sintaxis de estos tokens sea correcta.

Ambos comparten la tabla de símbolos que salen a partir del análisis sintáctico.

# 2. Proceso
1. **Preprocesamiento:** 
    - Quita comentarios
    - Quita saltos de líneas
    - Quita caracteres de separación

# 3. Tabla de símbolos
La tabla de símbolos es una tabla en la que se almacenan los identificadores del programa, el analizador léxico y sintáctico construyen estan tabla.

```c
posicion = incial + velocidad * 60
```
Tabla de símbolos
|id|nombre|
|--|------|
|1|posicion|
|2|inicial|
|3|velocidad|

Se considera como   

```c
id(1) = id(2) + id(3) * 60
```

# 4. Reconocimiento de Tokens
Cuando hablamos de una gramática, nos referimos a la estructura de un lenguaje para realizar algo. Por ejemplo.

![gramatica](assets/gramatica-if.png)

La gramática, entonces, se compone por una colección de tokens definidos en el lenguaje.

![tokens](assets/tokens-l.png)


## 4.1. Diagrama de Transición de estados
Los diagramas de transición de estados son un diagrama de máquina de estados o de autómata finito que representa la manera de reconocer lexemas o tokens.

Por ejemplo, el diagrama de transición para los operadores relacionales:

![afn oprel](assets/afn-oprel.png)

## 4.2. Reconocimiento de palabras reservadas e identificadores
Para identificar palabras reservadas, existen dos maneras de hacerlo (generalmente)

1. Realizar diagramas de transición para cada uno de las palabras reservadas.
![diagrama transición then](assets/diagrama-then.png)
2. Realizar diagrama de transición para encontrar el patrón que tienen las palabras, una vez que se encuentra la palabra, se busca en la tabla de símbolos (en donde las palabras reservadas fueron cargadas previamente).
![diagrama tokens](assets/transicion-tabla-simbolos.png)

# 5. Autómatas Finitos

Son la teoría detrás de las máquina de estados. Existen dos tipos, 

- **Autómatas finitos deterministas (AFD):** Todos los estados tienen solamente una transición por cada condición de transición. Es decir, no se puede transicionar a dos o más estados por la misma condición.
    - Solo tiene un estado final
- **Autómatas finitos no deterministas (AFN):** Pueden haber mas de una transición de un estado a otro con la misma condición de transición. 
    - Si tiene epsilon es AFN
    - Si tiene dos o más estados finales es un AFN

## 5.1. Construcción de AFN de una Expresión Regular
Podemos construi un AFN en base a una expresión regular siguiendo el algoritmo de McNaughton-Yamada-Thompson.
### 5.1.1. Or
Para s|t

![expr or](./assets/afn-or.png)

### 5.1.2. Concatenación
Para st

![expr concat](./assets/afn-concat.png)


### 5.1.3. Kleene
Para s*

![expr concat](./assets/afn-kleene.png)
