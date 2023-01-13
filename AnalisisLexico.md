# Análisis Léxico

## Conceptos básicos
- **Token:** Unidad léxica o atributo
- **Patrón:** Descripción de un lexema.
- **Lexema:** Secuencia de caracteres del programa fuente.

Analizador léxico obtiene **tokens** del código fuente. Los tokens salen de los lexemas contenidos en el código y que corresponden al lenguaje de programación.

|Código|Lexemas|Tokens|
|:--:|:--:|:--:|
|int num = 12;|int <br/> num <br/> =<br/> 12<br/>; | int -> reservada <br/>num -> id<br/>= -> =<br/>12 -> entero<br/>; -> reservada

Estos tokens se le dan al analizador sintáctico, el cual analiza que la sintaxis de estos tokens sea correcta.

Ambos comparten la tabla de símbolos que salen a partir del análisis sintáctico.

# Proceso
1. **Preprocesamiento:** 
    - Quita comentarios
    - Quita saltos de líneas
    - Quita caracteres de separación

# Tabla de símbolos
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