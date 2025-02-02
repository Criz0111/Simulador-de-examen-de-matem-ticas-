<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulador de Examen de Matemáticas</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 20px;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .question {
            background-color: #fff;
            border-radius: 8px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }
        .question h2 {
            margin-top: 0;
            color: #555;
        }
        .options {
            margin-left: 20px;
        }
        .options label {
            display: block;
            margin: 10px 0;
        }
        button {
            display: block;
            margin: 20px auto;
            padding: 10px 20px;
            font-size: 16px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #218838;
        }
        .result {
            text-align: center;
            font-size: 20px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Simulador de Examen de Matemáticas</h1>

    <div id="quiz">
        <!-- Las preguntas se insertarán aquí dinámicamente -->
    </div>

    <button id="calcularNotaButton">Calcular nota</button>
    <div class="result" id="resultado"></div>

    <script>
        // Datos de las preguntas y respuestas correctas
       const preguntas = [
{
    id: 59373,
    texto: "Al factorizar (x - 2)^2 - x + 2 se tiene:",
    opciones: [
        { letra: "a", texto: "(X-3)(X+4)" },
        { letra: "b", texto: "(X+3)(X-4)" },
        { letra: "c", texto: "(X-3)(X-2)" },
        { letra: "d", texto: "(X+3)(X+4)" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 59374,
    texto: "Después de factorizar la expresión 36m^4 - 4n^2, uno de los factores es:",
    opciones: [
        { letra: "a", texto: "(6m^2 + n)" },
        { letra: "b", texto: "(6m^2 + n^2)" },
        { letra: "c", texto: "(6m^2 + 2n)" },
        { letra: "d", texto: "(m^2 + 2n)" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59375,
    texto: "Hallar las raíces de: x^2 - 20x + 100 = 0",
    opciones: [
        { letra: "a", texto: "10" },
        { letra: "b", texto: "-10" },
        { letra: "c", texto: "100" },
        { letra: "d", texto: "+10" },
        { letra: "e", texto: "ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59376,
    texto: "Al efectuar las operaciones indicadas en: E = 3(1 - a)(1 + a)(a^2 + a + 1)(a^2 - a + 1)",
    opciones: [
        { letra: "a", texto: "3(1+a^6)" },
        { letra: "b", texto: "3(1-a^6)" },
        { letra: "c", texto: "3(a+a^2 + a^6)" },
        { letra: "d", texto: "3(1+a^2 + a^6)" },
        { letra: "e", texto: "3(a-a^2 + a^6)" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 59377,
    texto: "Después de factorizar: E = 25(4x^2 - 12xy + 9y^2) - 9a^2b^2, uno de los factores es:",
    opciones: [
        { letra: "a", texto: "(10x+15y-3ab)" },
        { letra: "b", texto: "(10x+15y-3ab)" },
        { letra: "c", texto: "(10x-5y+3ab)" },
        { letra: "d", texto: "(10x-15y+3ab)" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59378,
    texto: "Para que la suma de las raíces de la ecuación: 4x^2 = -7 + kx sea tres, entonces el valor de k es:",
    opciones: [
        { letra: "a", texto: "-12" },
        { letra: "b", texto: "12" },
        { letra: "c", texto: "7" },
        { letra: "d", texto: "todas las anteriores" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 59379,
    texto: "La suma de los coeficientes del segundo y tercer término de la expresión (1 - 2a)^3 es:",
    opciones: [
        { letra: "a", texto: "6" },
        { letra: "b", texto: "-6" },
        { letra: "c", texto: "12" },
        { letra: "d", texto: "18" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 59380,
    texto: "La representación de la siguiente cifra 2.71 × 10^(-2) es:",
    opciones: [
        { letra: "a", texto: "0,271" },
        { letra: "b", texto: "0,0271" },
        { letra: "c", texto: "0,00271" },
        { letra: "d", texto: "27,1" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 59381,
    texto: "El valor de k para la cual: 3x^3 - 2x^2 - 8 + kx sea divisible entre x-1 es:",
    opciones: [
        { letra: "a", texto: "7" },
        { letra: "b", texto: "-7" },
        { letra: "c", texto: "1" },
        { letra: "d", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59382,
    texto: "La representación de la siguiente cifra 0.0041 × 10^3 es:",
    opciones: [
        { letra: "a", texto: "41" },
        { letra: "b", texto: "4,1" },
        { letra: "c", texto: "0,41" },
        { letra: "d", texto: "Ninguna" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 59383,
    texto: "Treinta huevos cuestan 15 bs. ¿Cuántos cuestan 200 huevos?",
    opciones: [
        { letra: "a", texto: "50 bs" },
        { letra: "b", texto: "100 bs" },
        { letra: "c", texto: "150 bs" },
        { letra: "d", texto: "200 bs" },
        { letra: "e", texto: "ninguna de las anteriores" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 59384,
    texto: "La solución de la siguiente expresión (8 × 10^{12})^(1/4) es:",
    opciones: [
        { letra: "a", texto: "2 × 10^6" },
        { letra: "b", texto: "2 × 10^4" },
        { letra: "c", texto: "2 × 10^3" },
        { letra: "d", texto: "2 × 10^2" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 59385,
    texto: "Al desarrollar el siguiente binomio (2x - 3y)^3, el tercer término es:",
    opciones: [
        { letra: "a", texto: "-24x^3y" },
        { letra: "b", texto: "54xy^2" },
        { letra: "c", texto: "-54xy^3" },
        { letra: "d", texto: "36x^2y" },
        { letra: "e", texto: "Ninguno de los anteriores" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 59386,
    texto: "Simplificando la siguiente expresión: \n\\frac{-(a-b/a-b} + \\frac{a}{a} = \\frac{a+b}{a+b} + \\frac{3b}{a-b}",
    opciones: [
        { letra: "a", texto: "a + 1" },
        { letra: "b", texto: "1" },
        { letra: "c", texto: "b + 1" },
        { letra: "d", texto: "Ninguna" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 59644,
    texto: "El valor numérico de la expresión: \n\\frac{20^{t+1}}{4^{t+2} + 2^{t+2}} \nes:",
    opciones: [
        { letra: "a", texto: "5" },
        { letra: "b", texto: "6" },
        { letra: "c", texto: "4" },
        { letra: "d", texto: "2" },
        { letra: "e", texto: "ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59645,
    texto: "Después de simplificar la siguiente expresión: C = 5\\sqrt{700} - 4\\sqrt{343} - 3\\sqrt{112} - 21\\sqrt{7}^{-1}, el resultado para C es:",
    opciones: [
        { letra: "a", texto: "5\\sqrt{7}" },
        { letra: "b", texto: "6\\sqrt{7}" },
        { letra: "c", texto: "7\\sqrt{7}" },
        { letra: "d", texto: "8\\sqrt{7}" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59646,
    texto: "Después de simplificar la siguiente expresión: C = \\sqrt{588} - \\sqrt{300} + \\sqrt{108} - 21\\sqrt{3}^{-1}, el resultado para C es:",
    opciones: [
        { letra: "a", texto: "5\\sqrt{3}" },
        { letra: "b", texto: "4\\sqrt{3}" },
        { letra: "c", texto: "2\\sqrt{7}" },
        { letra: "d", texto: "3\\sqrt{3}" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59647,
    texto: "El valor numérico de \\left( \\frac{x^{a+b}}{x^b} \\right) x^{-a} para x = 3; a = 1; b = 20 es:",
    opciones: [
        { letra: "a", texto: "1" },
        { letra: "b", texto: "3" },
        { letra: "c", texto: "4" },
        { letra: "d", texto: "2" },
        { letra: "e", texto: "ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59648,
    texto: "La solución para C después de simplificar la siguiente expresión es: \n\\\[\nC = \\frac{3^x - 3^{x+2}}{3^{x-1} - 3^{x+1}} + \\frac{3^{x+4} - 3^{x-1}}{3^{x+3} + 3^{x+2}} \\cdot \\frac{500}{109}\n\\\]",
    opciones: [
        { letra: "a", texto: "10" },
        { letra: "b", texto: "5" },
        { letra: "c", texto: "20" },
        { letra: "d", texto: "50" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59649,
    texto: "La longitud de un rectángulo tiene un perímetro de 70 metros. Si su lado mayor mide el cuádruple de su lado menor, entonces el lado mayor en metros mide:",
    opciones: [
        { letra: "a", texto: "14" },
        { letra: "b", texto: "36" },
        { letra: "c", texto: "42" },
        { letra: "d", texto: "28" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "d"
},
{
    id: 59372,
    texto: "Hallar las raíces de 9 + 6x + x^2 = 0:",
    opciones: [
        { letra: "a", texto: "X = 2" },
        { letra: "b", texto: "X = 3" },
        { letra: "c", texto: "X = -3" },
        { letra: "d", texto: "X = -2" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 59650,
    texto: "Si vendo los 5/8 de una pieza de tela me quedan 24 metros, entonces la pieza de tela en metros tenía:",
    opciones: [
        { letra: "a", texto: "84" },
        { letra: "b", texto: "36" },
        { letra: "c", texto: "64" },
        { letra: "d", texto: "90" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 59671,
    texto: "Después de factorizar \\frac{1}{4}x^2 - \\frac{1}{16}y^4, la suma de sus factores es:",
    opciones: [
        { letra: "a", texto: "1" },
        { letra: "b", texto: "2" },
        { letra: "c", texto: "x" },
        { letra: "d", texto: "y" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 59651,
    texto: "La suma de patos y vacas en un corral es 131. Si el número de patas es de 360, entonces el número de vacas es:",
    opciones: [
        { letra: "a", texto: "55" },
        { letra: "b", texto: "82" },
        { letra: "c", texto: "49" },
        { letra: "d", texto: "58" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 59652,
    texto: "De 80,000 estudiantes universitarios, el 48% son varones. ¿Cuántas son mujeres?",
    opciones: [
        { letra: "a", texto: "42,000" },
        { letra: "b", texto: "52,000" },
        { letra: "c", texto: "36,000" },
        { letra: "d", texto: "41,600" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "d"
},
{
    id: 59653,
    texto: "Si la suma de la mitad de un número, su doble y su triple es 110, entonces el número es:",
    opciones: [
        { letra: "a", texto: "10" },
        { letra: "b", texto: "18" },
        { letra: "c", texto: "20" },
        { letra: "d", texto: "30" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 59654,
    texto: "Con los siguientes valores numéricos; x=5, y=3, z=2. El resultado de C es:",
    opciones: [
        { letra: "a", texto: "10" },
        { letra: "b", texto: "15" },
        { letra: "c", texto: "20" },
        { letra: "d", texto: "25" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "NA" // Respuesta no proporcionada en la pregunta original
},
{
    id: 59655,
    texto: "Con los siguientes valores numéricos; x=8, y=6, z=4. El resultado de C es:",
    opciones: [
        { letra: "a", texto: "12" },
        { letra: "b", texto: "16" },
        { letra: "c", texto: "20" },
        { letra: "d", texto: "24" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "NA" // Respuesta no proporcionada en la pregunta original
},
{
    id: 59656,
    texto: "El valor numérico de la expresión es:",
    opciones: [
        { letra: "a", texto: "2" },
        { letra: "b", texto: "4" },
        { letra: "c", texto: "6" },
        { letra: "d", texto: "5" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "NA" // Respuesta no proporcionada en la pregunta original
},
{
    id: 59657,
    texto: "Una de las raíces de la ecuación 5x^2 + kx - 2 = 0 es 2, entonces el valor de k es:",
    opciones: [
        { letra: "a", texto: "-9" },
        { letra: "b", texto: "13" },
        { letra: "c", texto: "-13" },
        { letra: "d", texto: "5" },
        { letra: "e", texto: "ninguna" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 59658,
    texto: "¿Cuál es el valor de k para que la división \\frac{kx^2 - (k + 3)x - 12}{2x + 3} sea exacta?",
    opciones: [
        { letra: "a", texto: "3" },
        { letra: "b", texto: "4" },
        { letra: "c", texto: "5" },
        { letra: "d", texto: "6" },
        { letra: "e", texto: "ninguna" }
    ],
    respuestaCorrecta: "a"
}
];
{
    id: 59659,
    texto: "El resto de dividir el polinomio (8x^3 - 6x^2 + 3x + 4) entre (x - \\frac{1}{2}) es:",
    opciones: [
        { letra: "a", texto: "0" },
        { letra: "b", texto: "1" },
        { letra: "c", texto: "5" },
        { letra: "d", texto: "2" },
        { letra: "e", texto: "ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59660,
    texto: "El resto de realizar la división \\frac{(x+1)^3 - (x-1)^5 - (x+2)^2}{x-2} es:",
    opciones: [
        { letra: "a", texto: "20" },
        { letra: "b", texto: "-10" },
        { letra: "c", texto: "10" },
        { letra: "d", texto: "1" },
        { letra: "e", texto: "ninguna" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 59661,
    texto: "El valor de k para que la división (3x^2 - 5x + 2k - 5) ÷ (x - 2) tenga resto 41 es:",
    opciones: [
        { letra: "a", texto: "25" },
        { letra: "b", texto: "40" },
        { letra: "c", texto: "0" },
        { letra: "d", texto: "22" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59662,
    texto: "El resto de la siguiente división es: (8x^2 + 4x - 35) ÷ (2x + 5)",
    opciones: [
        { letra: "a", texto: "0" },
        { letra: "b", texto: "5" },
        { letra: "c", texto: "1" },
        { letra: "d", texto: "8" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59663,
    texto: "El valor de k en la ecuación 2x^2 - kx + 15 = 0, para que el producto de sus raíces sea igual al triple de la suma de sus raíces, es:",
    opciones: [
        { letra: "a", texto: "\\frac{5}{6}" },
        { letra: "b", texto: "\\frac{6}{5}" },
        { letra: "c", texto: "2" },
        { letra: "d", texto: "3" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 59664,
    texto: "Después de factorizar x(x + 6)^2 - y^2, uno de sus factores es:",
    opciones: [
        { letra: "a", texto: "x + y - 3" },
        { letra: "b", texto: "x + y" },
        { letra: "c", texto: "x - y" },
        { letra: "d", texto: "x + y + 3" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 59665,
    texto: "La solución para B después de simplificar la siguiente expresión es:", // La expresión no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "1" },
        { letra: "b", texto: "x" },
        { letra: "c", texto: "x + 1" },
        { letra: "d", texto: "x - 1" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59666,
    texto: "Al descomponer la expresión x^{17} - x en un producto de factores primos, ¿cuántos factores primos se tienen como resultado?",
    opciones: [
        { letra: "a", texto: "3" },
        { letra: "b", texto: "4" },
        { letra: "c", texto: "5" },
        { letra: "d", texto: "6" },
        { letra: "e", texto: "ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59667,
    texto: "Después de factorizar \\frac{1}{4}x^2 - \\frac{1}{16}y^4, la suma de sus factores es:",
    opciones: [
        { letra: "a", texto: "2x" },
        { letra: "b", texto: "3x" },
        { letra: "c", texto: "x" },
        { letra: "d", texto: "2y" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59668,
    texto: "Factorizando y simplificando la expresión: (x + y)^4 - (x - y)^4, se obtiene:",
    opciones: [
        { letra: "a", texto: "9xy(x^2 + y^2)" },
        { letra: "b", texto: "16xy(x^2 + y^2)" },
        { letra: "c", texto: "8xy(x^2 + y^2)" },
        { letra: "d", texto: "9y(x + y)" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 59669,
    texto: "Factorizar y simplificar (x + y)(x - y) + 3x(x + y) + (x + y)^2:",
    opciones: [
        { letra: "a", texto: "5x(x + y)" },
        { letra: "b", texto: "15x(x + y)" },
        { letra: "c", texto: "25x(x + y)" },
        { letra: "d", texto: "50x(x + y)" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 59670,
    texto: "Después de factorizar 4by + ax - 2bx - 2ay, uno de sus factores es:",
    opciones: [
        { letra: "a", texto: "a + 2b" },
        { letra: "b", texto: "x - 2y" },
        { letra: "c", texto: "x + 2y" },
        { letra: "d", texto: "x - y" },
        { letra: "e", texto: "NA" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 65971,
    texto: "Después de factorizar la expresión, hallar la diferencia de sus factores primos expresada en valor absoluto:", // La expresión no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "4" },
        { letra: "b", texto: "6" },
        { letra: "c", texto: "8" },
        { letra: "d", texto: "2" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "d"
},
{
    id: 65972,
    texto: "Después de factorizar la expresión 10x^2 - 9x - 9, uno de sus factores es:",
    opciones: [
        { letra: "a", texto: "2x + 3" },
        { letra: "b", texto: "5x - 3" },
        { letra: "c", texto: "2x -3" },
        { letra: "d", texto: "5x + 2" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 66300,
    texto: "Simplificando la expresión, se obtiene:", // La expresión no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "x" },
        { letra: "b", texto: "x + 2" },
        { letra: "c", texto: "x" },
        { letra: "d", texto: "x + 2" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66301,
    texto: "Después de factorizar la expresión x^4 - 5x^2 + 4, la suma de sus factores es:",
    opciones: [
        { letra: "a", texto: "4" },
        { letra: "b", texto: "x^4" },
        { letra: "c", texto: "4x" },
        { letra: "d", texto: "x + 2" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66302,
    texto: "El cociente de dividir:", // La expresión no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "x + 1" },
        { letra: "b", texto: "x + 2" },
        { letra: "c", texto: "x - 1" },
        { letra: "d", texto: "x" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66303,
    texto: "Después de factorizar la expresión:", // La expresión no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "5x + 2" },
        { letra: "b", texto: "7x - 1" },
        { letra: "c", texto: "3x + 1" },
        { letra: "d", texto: "4x - 1" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66304,
    texto: "Después de factorizar la expresión x^2 - 28, hallar la diferencia de sus factores expresada en valor absoluto:",
    opciones: [
        { letra: "a", texto: "6" },
        { letra: "b", texto: "8" },
        { letra: "c", texto: "5" },
        { letra: "d", texto: "2" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 66305,
    texto: "Después de factorizar la expresión x^2 - 45, hallar la diferencia de sus factores expresada en valor absoluto:",
    opciones: [
        { letra: "a", texto: "7" },
        { letra: "b", texto: "8" },
        { letra: "c", texto: "5" },
        { letra: "d", texto: "2" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 66306,
    texto: "Hallar la raíz de:", // La ecuación no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "X = 2, X = 3" },
        { letra: "b", texto: "X = 3, X = -2" },
        { letra: "c", texto: "X = 1, X = -2" },
        { letra: "d", texto: "X = -1, X = -3" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 66307,
    texto: "La solución de la ecuación cuadrática x^2 - 4x = 5 es:",
    opciones: [
        { letra: "a", texto: "X = 5; X = 4" },
        { letra: "b", texto: "X = 5; X = 1" },
        { letra: "c", texto: "X = 5; X = -4" },
        { letra: "d", texto: "X = 5; X = -1" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "d"
},
{
    id: 66308,
    texto: "Resuelva la siguiente ecuación x^{-4} - 13x^{-2} - 48 = 0 e identifique una de las soluciones:",
    opciones: [
        { letra: "a", texto: "0.5" },
        { letra: "b", texto: "-0.25" },
        { letra: "c", texto: "0.35" },
        { letra: "d", texto: "-0.5" },
        { letra: "e", texto: "Ninguno de los anteriores" }
    ],
    respuestaCorrecta: "d"
},
{
    id: 66309,
    texto: "La solución para C después de simplificar la siguiente expresión es: C = \\left\\{ \\left[ (x - \\frac{9}{x}) + (x + 3) \\right] \\cdot (x - 3)^{-1} \\right\\}^{-1}",
    opciones: [
        { letra: "a", texto: "x + 1" },
        { letra: "b", texto: "x - 3" },
        { letra: "c", texto: "x + 3" },
        { letra: "d", texto: "Ninguna" },
        { letra: "e", texto: "x" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66310,
    texto: "En la siguiente ecuación 4x = \\frac{mx}{4} + 22, si la solución de x es igual a 8, entonces el valor de m es:",
    opciones: [
        { letra: "a", texto: "6" },
        { letra: "b", texto: "-6" },
        { letra: "c", texto: "5" },
        { letra: "d", texto: "10" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66311,
    texto: "Después de resolver la ecuación, si la solución de x es igual a 8, entonces el valor de m es:", // La ecuación no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "1" },
        { letra: "b", texto: "2" },
        { letra: "c", texto: "4" },
        { letra: "d", texto: "8" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "d"
},
{
    id: 66312,
    texto: "La suma de las edades de un padre y su hijo es 60 años. Si la edad del hijo es \\frac{1}{4} de la edad del padre, entonces la edad del padre es:",
    opciones: [
        { letra: "a", texto: "42" },
        { letra: "b", texto: "40" },
        { letra: "c", texto: "48" },
        { letra: "d", texto: "44" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 66313,
    texto: "La solución para x de la ecuación es:", // La ecuación no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "\\frac{5}{13}" },
        { letra: "b", texto: "\\frac{13}{5}" },
        { letra: "c", texto: "-\\frac{5}{13}" },
        { letra: "d", texto: "1" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66314,
    texto: "La solución para x de la ecuación es:", // La ecuación no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "\\frac{a}{3}" },
        { letra: "b", texto: "\\frac{a}{5}" },
        { letra: "c", texto: "\\frac{a}{2}" },
        { letra: "d", texto: "a + 1" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66315,
    texto: "Elva tiene el triple de la edad de su hija Roxana. Si en 12 años la edad de la madre será el doble de la edad de la hija, entonces la cantidad de años de Elva es:",
    opciones: [
        { letra: "a", texto: "48" },
        { letra: "b", texto: "36" },
        { letra: "c", texto: "45" },
        { letra: "d", texto: "30" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 66316,
    texto: "La solución para x de la ecuación es:", // La ecuación no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "3" },
        { letra: "b", texto: "5" },
        { letra: "c", texto: "2" },
        { letra: "d", texto: "4" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66317,
    texto: "Después de resolver la ecuación x + 5 - \\frac{9}{x^2 + 8x + 16} = 1, encontrar “C” sabiendo que: C = x - 5:",
    opciones: [
        { letra: "a", texto: "5" },
        { letra: "b", texto: "2" },
        { letra: "c", texto: "0" },
        { letra: "d", texto: "3" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 66319,
    texto: "La solución de la ecuación A + 5x = A - (x + 12) es:",
    opciones: [
        { letra: "a", texto: "X = 2" },
        { letra: "b", texto: "X = -2" },
        { letra: "c", texto: "X = 3" },
        { letra: "d", texto: "X = 5" },
        { letra: "e", texto: "X = 0" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 66320,
    texto: "Al resolver la ecuación \\sqrt{x + 3} + \\sqrt{x + 3} = 5, las soluciones de x son:",
    opciones: [
        { letra: "a", texto: "9 y 1" },
        { letra: "b", texto: "8 y 1" },
        { letra: "c", texto: "7 y 1" },
        { letra: "d", texto: "6 y 1" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66321,
    texto: "En la ecuación \\sqrt{5x + 6} = 3, el valor numérico de 3x - 4 es:",
    opciones: [
        { letra: "a", texto: "11" },
        { letra: "b", texto: "14" },
        { letra: "c", texto: "17" },
        { letra: "d", texto: "20" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 65970,
    texto: "Para poder factorizar el polinomio x^2 + Px - 6, los valores de P son:",
    opciones: [
        { letra: "a", texto: "-1, 1, 5, -5" },
        { letra: "b", texto: "2, -3, 6, -6" },
        { letra: "c", texto: "1, -1, 6, -6" },
        { letra: "d", texto: "1, 2, -3, 3" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66322,
    texto: "En la ecuación, el valor numérico de x + 8 es:", // La ecuación no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "21" },
        { letra: "b", texto: "22" },
        { letra: "c", texto: "23" },
        { letra: "d", texto: "18" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66366,
    texto: "El paso de una sustancia del estado sólido al estado líquido se denomina:",
    opciones: [
        { letra: "a", texto: "Fusión" },
        { letra: "b", texto: "Condensación" },
        { letra: "c", texto: "Sublimación" },
        { letra: "d", texto: "Evaporación" },
        { letra: "e", texto: "Ninguna de las anteriores" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66323,
    texto: "Después de resolver la ecuación, el valor numérico de x + 8 es:", // La ecuación no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "8" },
        { letra: "b", texto: "2" },
        { letra: "c", texto: "3" },
        { letra: "d", texto: "6" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66324,
    texto: "Después de resolver la ecuación, encontrar “x” sabiendo que x ∈ ℕ:", // La ecuación no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "3" },
        { letra: "b", texto: "2" },
        { letra: "c", texto: "1" },
        { letra: "d", texto: "0" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66326,
    texto: "Después de resolver la ecuación, el valor numérico de x + 8 es:", // La ecuación no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "3" },
        { letra: "b", texto: "6" },
        { letra: "c", texto: "9" },
        { letra: "d", texto: "5" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66327,
    texto: "Después de resolver la ecuación, el valor numérico de x + 8 es:", // La ecuación no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "-5" },
        { letra: "b", texto: "-6" },
        { letra: "c", texto: "65" },
        { letra: "d", texto: "5" },
        { letra:  "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "d"
},
{
    id: 66328,
    texto: "Después de resolver la ecuación, el valor numérico de x + 8 es:", // La ecuación no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "3" },
        { letra: "b", texto: "6" },
        { letra: "c", texto: "1" },
        { letra: "d", texto: "7" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66329,
    texto: "Después de resolver la ecuación, el valor numérico de x + 8 es:", // La ecuación no fue proporcionada en la pregunta original.
    opciones: [
        { letra: "a", texto: "4" },
        { letra: "b", texto: "6" },
        { letra: "c", texto: "0" },
        { letra: "d", texto: "3" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66330,
    texto: "Después de resolver el sistema de ecuaciones, el valor numérico de x + 8 es:", // El sistema de ecuaciones no fue proporcionado en la pregunta original.
    opciones: [
        { letra: "a", texto: "7" },
        { letra: "b", texto: "4" },
        { letra: "c", texto: "11" },
        { letra: "d", texto: "20" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66331,
    texto: "Después de resolver la inecuación lineal \\frac{3}{10} ≤ \\frac{2x - 5}{15} < \\frac{21}{20}, la solución es:",
    opciones: [
        { letra: "a", texto: "\\frac{19}{4} ≤ x < \\frac{83}{8}" },
        { letra: "b", texto: "\\frac{19}{4} ≤ x < \\frac{88}{7}" },
        { letra: "c", texto: "\\frac{21}{4} ≤ x < \\frac{83}{8}" },
        { letra: "d", texto: "\\frac{21}{4} ≤ x < \\frac{88}{7}" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66332,
    texto: "La suma de los números enteros del conjunto solución es:",
    opciones: [
        { letra: "a", texto: "-4" },
        { letra: "b", texto: "5" },
        { letra: "c", texto: "-5" },
        { letra: "d", texto: "4" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66333,
    texto: "Después de resolver la inecuación, el conjunto solución es:",
    opciones: [
        { letra: "a", texto: "10" },
        { letra: "b", texto: "15" },
        { letra: "c", texto: "7" },
        { letra: "d", texto: "9" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66334,
    texto: "Encontrar el conjunto solución de la inecuación: (x - 2)",
    opciones: [
        { letra: "a", texto: "[2; 4.5]" },
        { letra: "b", texto: "-2, 4" },
        { letra: "c", texto: "-2, 4.5" },
        { letra: "d", texto: "2, 4" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66335,
    texto: "Encontrar el conjunto solución de la inecuación: x^2 + 6 ≥ x",
    opciones: [
        { letra: "a", texto: "[-2, 3]" },
        { letra: "b", texto: "[2, 3/2]" },
        { letra: "c", texto: "[-2, 3/2]" },
        { letra: "d", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66337,
    texto: "La suma de los números naturales que pertenecen al conjunto solución de la inecuación |4x - 1| ≤ 15 es:",
    opciones: [
        { letra: "a", texto: "Ninguna" },
        { letra: "b", texto: "15" },
        { letra: "c", texto: "10" },
        { letra: "d", texto: "9" },
        { letra: "e", texto: "6" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 66339,
    texto: "Resolver la siguiente ecuación ln(a) = 0:",
    opciones: [
        { letra: "a", texto: "1/2 ln(a)" },
        { letra: "b", texto: "a^2" },
        { letra: "c", texto: "ln(a)" },
        { letra: "d", texto: "ln(a^2)" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 66340,
    texto: "Después de reducir la expresión: log_8 (log_3 (81)), el resultado es:",
    opciones: [
        { letra: "a", texto: "2/3" },
        { letra: "b", texto: "3/2" },
        { letra: "c", texto: "2" },
        { letra: "d", texto: "3" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66342,
    texto: "Encontrar el valor de Y para la siguiente ecuación exponencial: 5^(y+1) - 10 * 5^(y-1) = 15",
    opciones: [
        { letra: "a", texto: "-1" },
        { letra: "b", texto: "2" },
        { letra: "c", texto: "-2" },
        { letra: "d", texto: "1" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66344,
    texto: "Utilizando identidades trigonométricas y simplificando, se obtiene:",
    opciones: [
        { letra: "a", texto: "sin(β)" },
        { letra: "b", texto: "cos(β)" },
        { letra: "c", texto: "csc(β)" },
        { letra: "d", texto: "sec(β)" },
        { letra: "e", texto: "Ninguno" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66349,
    texto: "La recta y = 3x - 6 es una línea que pasa por:",
    opciones: [
        { letra: "a", texto: "(0, 3)" },
        { letra: "b", texto: "x = 3" },
        { letra: "c", texto: "y = 3" },
        { letra: "d", texto: "(3, 3)" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66350,
    texto: "Resolver la siguiente ecuación: log(x) + log(20) = 3",
    opciones: [
        { letra: "a", texto: "10" },
        { letra: "b", texto: "5" },
        { letra: "c", texto: "50" },
        { letra: "d", texto: "-5" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "c"
},
{
    id: 66352,
    texto: "La pendiente de la recta que pasa por los puntos (3, 4) y (1, -2) es:",
    opciones: [
        { letra: "a", texto: "3" },
        { letra: "b", texto: "-3" },
        { letra: "c", texto: "5" },
        { letra: "d", texto: "-5" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66353,
    texto: "Un triángulo tiene sus ángulos internos A = 56°, B = 92° y C es:",
    opciones: [
        { letra: "a", texto: "C = 30°" },
        { letra: "b", texto: "C = 32°" },
        { letra: "c", texto: "C = 23°" },
        { letra: "d", texto: "C = 33°" },
        { letra: "e", texto: "Ninguna" }
    ],
    respuestaCorrecta: "b"
},
{
    id: 66354,
    texto: "La raíz de la ecuación log_3 (2x + 1) = log_3 (x - 2) + 1 es:",
    opciones: [
        { letra: "a", texto: "7" },
        { letra: "b", texto: "-7" },
        { letra: "c", texto: "17" },
        { letra: "d", texto: "-17" },
        { letra: "e", texto: "Ninguno de los anteriores" }
    ],
    respuestaCorrecta: "a"
},
{
    id: 66355,
    texto: "La hipotenusa de un triángulo rectángulo es 10 y uno de sus catetos es 6. Determinar el área del triángulo:",
    opciones: [
        { letra: "a", texto: "48" },
        { letra: "b", texto: "30" },
        { letra: "c", texto: "24" },
        { letra: "d", texto: "60"},
        {letra: "e", texto: "ninguno de los anteriores"},
        ],
        respuestacorrecta: "c"
        },
        {
    id: 66356,
    texto: "Resolver la siguiente ecuación logarítmica: \(\log_2(x) = -2\)",
    opciones: [
        { letra: "a", texto: "1" },
        { letra: "b", texto: "0.5" },
        { letra: "c", texto: "0.25" },
        { letra: "d", texto: "-4"},
        {letra: "e", texto: "ninguno de los anteriores"},
        ],
        respuestacorrecta: "c"
        },
];

        // Generar preguntas
        function generarPreguntas() {
            const quiz = document.getElementById("quiz");
            preguntas.forEach((pregunta, index) => {
                const div = document.createElement("div");
                div.className = "question";
                div.innerHTML = `
                    <h2>Pregunta ${index + 1}</h2>
                    <p>${pregunta.texto}</p>
                    <div class="options">
                        ${pregunta.opciones.map(op => `
                            <label><input type="radio" name="q${pregunta.id}" value="${op.letra}"> ${op.letra}. ${op.texto}</label>
                        `).join("")}
                    </div>
                `;
                quiz.appendChild(div);
            });
        }

        // Calcular nota
        function calcularNota() {
            let correctas = 0;
            preguntas.forEach(p => {
                const seleccion = document.querySelector(`input[name="q${p.id}"]:checked`);
                if (seleccion && seleccion.value === p.respuestaCorrecta) correctas++;
            });
            const nota = (correctas / preguntas.length * 100).toFixed(2);
            document.getElementById("resultado").innerHTML = `
                <p>Correctas: ${correctas} / ${preguntas.length}</p>
                <p>Nota: ${nota}%</p>
            `;
        }

        window.onload = generarPreguntas;
    </script>
</body>
</html>
