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

----
## Creación de lenguaje

#### MagicLang

MagicLang es un lenguaje de programación esotérico de estilo imperativo cuyo objetivo principal es ofrecer una experiencia lúdica y temática inspirada en el vocabulario vinculado a la magia. Sus construcciones sintácticas, como *hechizo, invocar, conjurar, ritual, encantar o forjar*, remiten al imaginario de los rituales y encantamientos, haciendo que el código se interprete como un grimorio. Aunque no tiene una finalidad práctica o pedagógica específica, su diseño sigue una estructura coherente que recuerda a lenguajes procedurales clásicos, lo que permite entenderlo y ejecutarlo de forma intuitiva para quienes ya están familiarizados con la programación imperativa.

En MagicLang, los programas están compuestos por sentencias secuenciales que permiten declarar variables (forjar), definir o ejecutar hechizos (funciones sin retorno explícito), repetir bloques (conjurar), seleccionar el flujo dependiendo de una condición (ritual) y mostrar resultados por pantalla (encantar). Las variables tienen alcance global si se declaran fuera de bloques o hechizos, pero su visibilidad se restringe al bloque o hechizo en el que se declaran si están definidas internamente. El paso de parámetros es por referencia, por lo que los hechizos pueden modificar directamente el contenido de las variables pasadas como argumentos, generando efectos colaterales fuera de su bloque de ejecución. Además, se permite la anidación de hechizos, la combinación de operaciones en asignaciones y el uso de bloques anónimos dentro de invocaciones.

A nivel de tipos, el lenguaje es fuertemente tipado e implícito y admite únicamente dos tipos de datos primitivos: números y booleanos. No se permite la mezcla libre de tipos ni operaciones inválidas entre ellos, y cualquier intento de operar con variables no declaradas o fuera de alcance provoca un fallo en la ejecución. Las expresiones numéricas y lógicas son completas, permitiendo operaciones aritméticas básicas, comparaciones y combinaciones booleanas. En resumen, MagicLang propone una estética encantadora sobre una base imperativa sólida, combinando la familiaridad de lenguajes tradicionales con un vocabulario vinculado a las artes mágicas.

~~~
<programa> ::= { <lista_sentencias> }
<lista_sentencias> ::= <sentencia> | <sentencia> <lista_sentencias>
<sentencia> ::= λ | <asignacion>; | <funcion> | <invocacion>; | <repeticion> | <condicional> | <imprimir>;

<asignacion> ::= forjar <identificador> = <valor>

<identificador> ::= <minuscula> <caracteres>
<caracteres> ::= λ | <caracter><caracteres>
<caracter> ::= <minuscula> | <mayuscula> | <numero> | <simbolo>

<funcion> ::= hechizo <identificador>(<parametros>) <bloque>

<parametros> ::= λ | <identificador> | <identificador>, <parametros>
<bloque> ::= [<lista_sentencias>]

<invocacion> ::= invocar <identificador>(<argumento>) | invocar <bloque>
<argumento> ::= λ | <valor> | <valor>, <argumento>

<repeticion> ::= conjurar (<valor_numerico>) veces <bloque>

<condicional> ::= ritual(<valor_booleano>) <bloque> | ritual(<valor_booleano>) <bloque> fallido <bloque>

<imprimir> ::= encantar(<valor>)

<valor> ::= <valor_numerico> | <valor_booleano>

<valor_numerico> ::= <numero> | <operacion_numerica> | <identificador>
<operacion_numerica> ::= <valor_numerico> <operador_numerico> <valor_numerico> | (<valor_numerico>)

<valor_booleano> ::= <booleano> | <operacion_booleana> | <identificador>
<operacion_booleana> ::= no <valor_booleano> | <valor_booleano> <operador_booleano> <valor_booleano> | <valor_numerico> <comparador_numerico> <valor_numerico> | (<valor_booleano>)

<operador_numerico> ::= + | - | * | / | %
<comparador_numerico> ::= <comparacion> | < | > | <= | >=
<operador_booleano> ::= <comparacion> | y | o
<comparacion> ::= == | !=
<booleano> ::= Verdadero | Falso
<numero> ::= <digito> | <digito><numero>
<digito> ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
<minuscula> ::= a | b | c | d | e | f | g | h | i | j | k | l | m | n | ñ | o | p | q | r | s | t | u | v | w | x | y | z
<mayuscula> ::= A | B | C | D | E | F | G | H | I | J | K | L | M | N | Ñ | O | P | Q | R | S | T | U | V | W | X | Y | Z
<simbolo> ::= _ | - | # | $ | ?
~~~

Algunos ejemplos de programas:
#### 1:
~~~
{
    forjar x = 1;

    hechizo duplicar(var) [
        forjar var = var * 2
    ]

    invocar duplicar(x);
    invocar duplicar(x);

    encantar(x);
}
~~~
Salida del programa:
~~~
4
~~~

#### 2:
~~~
{
    hechizo aumentarVAR_XvecesY(var, x, y) [
        conjurar (x) veces [
            forjar var = var + y
        ]
    ]

    forjar ejemplo = 10;

    invocar aumentarVAR_XvecesY(ejemplo, 4, 15);

    encantar(ejemplo);
}
~~~
Salida del programa:
~~~
70
~~~

#### 3:
~~~
{
    forjar valor = 10;

    invocar [
        conjurar (5) veces [
            forjar valor = valor * 2
        ]
    ]

    forjar mayorA300 = valor > 300;

    ritual(mayorA300) [
        forjar valor = valor / 2;
    ] fallido [
        forjar valor = valor * 2;
    ]

    encantar(mayorA300);
    encantar(valor);
}
~~~
Salida del programa:
~~~
Verdadero
160
~~~

