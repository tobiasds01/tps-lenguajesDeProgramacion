# TPs de Características de Lenguajes de Programación
## Di Salvo, Tobías

## TP 1
Empezaremos con un mapa conceptual sobre los lenguajes de programación y sus características. Esta es mi propuesta:

![Mapa conceptual](Mapas-conceptuales.png)

## TP 2
Para el segundo TP realizaremos una clasificación de lenguajes en base a sus características. Pueden verse en el siguiente enlace:
[Enlace a la tabla](https://docs.google.com/spreadsheets/d/19aTSzIjQNs6RBNJFz0bftTlqKr-uWbohbBZnxmP0-r0/edit?usp=sharing)

## TP 3
El lenguaje elegido para el TP3 es CAT, un lenguaje esotérico que basa su ejecución en una pila. Las instrucciones se apilan en una estructura y se van ejecutándo secuencialmente sobre el elemento que está en el tope. Esta gramática es del lenguaje puro, con sus instrucciones primitivas únicamente.

#### GIC
~~~
S -> L | F | SS | [S]
L -> N | B
N -> 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
B -> true | false
F -> dup | swap | drop | cat | cons | ifte | dip | eq | add | sub | mul | div
~~~
#### BNF
~~~
<expresion> ::= <literal> | <funcion> | <expresión> <expresion> | [ <expresion> ]

<literal> ::= <num> | <bool>

<num> ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9

<bool> ::= true | false

<función> ::= dup | swap | drop | cat | cons | ifte | dip | eq | add | sub | mul | div
~~~
#### EBNF
~~~
programa = { expresion }* ;
expresion = literal | funcion | "[" expresion "]" ;

literal    = num | bool ;

num        = "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" ;

bool       = "true" | "false" ;

funcion    = "dup" | "swap" | "drop" | "cat" | "cons" | "ifte" | "dip" |
             "eq" | "add" | "sub" | "mul" | "div" ;

~~~
#### ABNF
~~~
expresion:  literal
            funcion
            [expresion]
            λ

literal: uno de  num bool

num: uno de  0 1 2 3 4 5 6 7 8 9

bool: uno de  true false

funcion: uno de  dup swap drop cat cons ifte dip eq add sub mul div
~~~

## TP 4
Para el cuarto trabajo desarrollaremos el **Árbol semántico** y el **Diagrama de Conway** sobre la gramática planteada en el anterior ejercicio. El primero nos indica cómo podemos utilizar la gramática para llegar a las expresiones de nuestro lenguaje. Por otra parte, el segundo nos muestra el flujo que tiene nuestra gramática planteada.

#### Árbol semántico
Veremos un ejemplo de un árbol semántico para la siguiente expresión:
~~~
9 1 sub 8 swap eq true drop [ 2 dup mul ] [ 3 6 add ] ifte
~~~
En ella pasamos por varias funciones, números, un booleano y citas (los bloques de código delimitados por "[]"). Entonces:

![Árbol semántico](Arbol-semantico.png)

#### Diagrama de: Programa
![Diagrama de Conway](Diagrama-conway.png)
#### Diagrama de: Expresión
![Diagrama de Conway: Expresión](Conway-expresion.png)
#### Diagrama de: Función
![Diagrama de Conway: Función](Conway-funcion.png)
#### Diagrama de: Booleano
![Diagrama de Conway: Booleano](Conway-bool.png)
#### Diagrama de: Número
![Diagrama de Conway: Número](Conway-num.png)

## TP 5
Para el TP5 se analizará el concepto de **Parámetros** en cuanto a los tipos de *Binding* existentes en ellos. Para esto, se utilizarán ejemplos de varios lenguajes de programación con diferentes características en ellos.
### Cuadro de análisis del concepto "Parámetros" en los lenguajes de programación

| Binding |   | Estático  | Dinámico  | Ejemplo dinámico  |
|---------|---|-----------|-----------|-------------------|
| **De valor** | El parámetro se asocia a una copia del valor pasado. |Valor copiado al parámetro formal. Común en C, Java (tipos primitivos), Pascal. | Algunos lenguajes permiten reevaluar expresiones o usar *call-by-name*. | `procedure f(x) = x * x;` <br>`call f(a + b)` → se evalúa `a + b` cada vez (ALGOL) |            |
| **De tipo** | El parámetro se vincula a un tipo de dato, ya sea explícitamente declarado (tipado estático) o inferido en tiempo de ejecución (tipado dinámico). | Tipado estático: tipo de parámetro se declara. C, Java, C++, Kotlin, Rust. | Inferencia o sin tipo declarado. Python, PHP, JS, Ruby, Lua.  | `def f(x): return x * 2` (Python) <br>`f(5)` y `f("ho")` ambos válidos |
| **De alcance** | Determina en qué partes del código el parámetro es accesible. | Parámetros definidos solo dentro del cuerpo de la función.              | Lenguajes dinámicos pueden usar entornos dinámicos. | `def f(): print(x)` <br>`x = 5; f()` (Python)   |
| **De almacenamiento** | Define dónde se guarda el parámetro en memoria | Parámetro se asigna a espacio en stack (por valor) o heap (por referencia). | En intérpretes, se maneja todo como referencias internas. | `void f(int x) { x = 5; }` (C) → `x` es local, en el stack |
| **De nombre** | Relaciona el identificador usado por el programador con el valor pasado como argumento. | Parámetros posicionales. C, Java, Pascal, C++. | Parámetros nombrados / con nombre clave. Python, Kotlin, Ruby. | `def saluda(nombre="Pepe")` <br>`saluda(nombre="Juan")` |
| **De tiempo de vida** | Es el periodo durante el cual el parámetro existe en memoria y puede ser usado. | Limitado al tiempo de ejecución de la función. | Clausuras o funciones anidadas pueden extender su vida. | `function outer() { let x = 5; return () => x++; }` (JS) → `x` sobrevive |
