[< Regresar al Índice](README.md)

# Introducción

La fase del análisis sintáctico se verifica que la manera en la que está escrito el programa sea correcta (por lo menos desde un punto de vista sintáctico).

![Fases compilador](assets/analisis-sintactico.png)

## Funciones del Analizador Sintáctico

1. Recoger Información sobre componentes léxicos en la tabla de símbolos
2. Realizar la verificación de tipo y otras clases de análsisi semántico.
3. Generar (algo de) código intermedio
4. Manejar errores


# Manejo de Errores

Gran parte de la fase del analizador sintáctico es encontrar errores en el programa que impiden la correcta compilaciíon del mismo.

Algunos tipos de errores comunes son:
- Léxicos, escribir mal un id, operador o palabra clave.
- Sintáctico, paréntesis no equilibrados
- Semántico, un operador u operando no compatibles
- Lógico, recursión infinita