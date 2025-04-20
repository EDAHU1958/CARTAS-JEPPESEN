<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cuestionario Cartas Jeppesen</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .quiz-container {
            max-width: 800px;
            margin: auto;
            padding: 2rem;
            background-color: #f3f4f6; /* bg-gray-100 */
            border-radius: 0.5rem; /* rounded-lg */
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06); /* shadow-md */
        }
        .question {
            font-size: 1.25rem; /* text-xl */
            font-weight: 500; /* font-semibold */
            margin-bottom: 1rem; /* mb-4 */
            color: #1f2937; /* text-gray-800 */
        }
        .options {
            margin-bottom: 1.5rem; /* mb-6 */
        }
        .option {
            display: block;
            padding: 0.75rem 1rem; /* py-3 px-4 */
            background-color: white; /* bg-white */
            border-radius: 0.375rem; /* rounded-md */
            border: 1px solid #e5e7eb; /* border-gray-200 */
            margin-bottom: 0.5rem; /* mb-2 */
            cursor: pointer;
            transition: background-color 0.3s ease, border-color 0.3s ease; /* Smooth transition */
            color: #374151; /* text-gray-700 */
        }
        .option:hover {
            background-color: #f9fafb; /* hover:bg-gray-50 */
            border-color: #d1d5db; /* hover:border-gray-300 */
        }
        .option input[type="radio"] {
            margin-right: 0.5rem; /* mr-2 */
            vertical-align: middle;
        }
        .answer {
            font-weight: 600; /* font-semibold */
            margin-top: 1rem; /* mt-4 */
            padding: 0.75rem 1rem; /* py-3 px-4 */
            border-radius: 0.375rem; /* rounded-md */
            background-color: #eff6ff; /* bg-blue-100 */
            border: 1px solid #dbeafe; /* border-blue-200 */
            color: #1e40af; /* text-blue-700 */
        }
        .feedback {
            margin-top: 1rem; /* mt-4 */
            padding: 0.75rem 1rem; /* py-3 px-4 */
            border-radius: 0.375rem; /* rounded-md */
            font-weight: 500; /* font-medium */
        }
        .correct {
            background-color: #f0fdf4; /* bg-green-100 */
            border: 1px solid #dcfce7; /* border-green-200 */
            color: #15803d; /* text-green-700 */
        }
        .incorrect {
            background-color: #fef2f2; /* bg-red-100 */
            border: 1px solid #fecaca; /* border-red-300 */
            color: #b91c1c; /* text-red-700 */
        }
        .actions {
            margin-top: 2rem; /* mt-8 */
            display: flex;
            justify-content: flex-end; /* justify-end */
        }
        .button {
            padding: 0.75rem 1.5rem; /* py-3 px-6 */
            border-radius: 0.375rem; /* rounded-md */
            font-weight: 600; /* font-semibold */
            cursor: pointer;
            transition: background-color 0.3s ease, color 0.3s ease;
        }
        .primary-button {
            background-color: #4f46e5; /* bg-indigo-600 */
            color: white; /* text-white */
        }
        .primary-button:hover {
            background-color: #4338ca; /* hover:bg-indigo-700 */
        }
        .secondary-button {
            background-color: #e5e7eb; /* bg-gray-200 */
            color: #374151; /* text-gray-700 */
            margin-right: 0.75rem; /* mr-3 */
        }
        .secondary-button:hover {
            background-color: #d1d5db; /* hover:bg-gray-300 */
        }
        .hidden {
            display: none;
        }
        .results {
            margin-top: 2rem;
            padding: 1.5rem;
            background-color: #f7fafc;
            border-radius: 0.5rem;
            border: 1px solid #e2e8f0;
            text-align: center;
        }
        .results h2 {
            font-size: 1.5rem;
            font-weight: 600;
            margin-bottom: 1rem;
            color: #1e293b;
        }
        .results p {
            font-size: 1.125rem;
            margin-bottom: 0.75rem;
            color: #334155;
        }
        .results button {
            margin-top: 1.5rem;
        }
    </style>
</head>
<body class="bg-gray-100 font-sans">
    <div class="quiz-container">
        <h1 class="text-2xl font-bold mb-6 text-gray-800">Cuestionario de Cartas Jeppesen</h1>
        <div id="quiz-content">
            </div>
        <div id="results" class="results hidden">
            <h2>Resultados del Cuestionario</h2>
            <p>Tu puntuación: <span id="final-score">0</span> / <span id="total-questions">0</span></p>
            <p>Porcentaje: <span id="percentage">0</span>%</p>
            <button id="restart-button" class="button primary-button">Reiniciar Cuestionario</button>
        </div>
    </div>
    <script>
        const quizData = [
            {
                question: "¿Qué son las Cartas Jeppesen?",
                options: [
                    "Mapas topográficos detallados.",
                    "Cartas aeronáuticas diseñadas para la navegación IFR.",
                    "Registros de mantenimiento de aeronaves.",
                    "Pronósticos meteorológicos para aviación."
                ],
                correctAnswer: "Cartas aeronáuticas diseñadas para la navegación IFR.",
                module: 1
            },
            {
                question: "¿Cuál es el propósito principal de las Cartas Jeppesen en la aviación IFR?",
                options: [
                    "Proporcionar entretenimiento a los pilotos durante el vuelo.",
                    "Servir como herramienta de apoyo para la planificación y ejecución de vuelos IFR.",
                    "Registrar las horas de vuelo de la tripulación.",
                    "Mostrar la ubicación de los aeropuertos en todo el mundo."
                ],
                correctAnswer: "Servir como herramienta de apoyo para la planificación y ejecución de vuelos IFR.",
                module: 1
            },
            {
                question: "¿Por qué son necesarias las cartas aeronáuticas antes de cualquier vuelo?",
                options: [
                    "Para cumplir con las regulaciones de la aerolínea.",
                    "Para informar a los pasajeros sobre la ruta del vuelo.",
                    "Para proporcionar información esencial para la navegación y seguridad del vuelo.",
                    "Para calcular el consumo de combustible de la aeronave."
                ],
                correctAnswer: "Para proporcionar información esencial para la navegación y seguridad del vuelo.",
                module: 1
            },
            {
                question: "¿Cuáles de los siguientes son tipos de Cartas Jeppesen según la fase de vuelo?",
                options: [
                    "Cartas de navegación marítima.",
                    "Cartas de aproximación (ILS, RNAV, VOR, NDB).",
                    "Cartas de rutas terrestres.",
                    "Cartas estelares."
                ],
                correctAnswer: "Cartas de aproximación (ILS, RNAV, VOR, NDB).",
                module: 1
            },
            {
                question: "¿Qué diferencia a las Cartas Jeppesen de otras cartas aeronáuticas?",
                options: [
                    "Utilizan un idioma diferente.",
                    "Contienen información menos precisa.",
                    "Tienen una presentación y organización específica, a menudo consideradas más fáciles de usar.",
                    "Son gratuitas."
                ],
                correctAnswer: "Tienen una presentación y organización específica, a menudo consideradas más fáciles de usar.",
                module: 1
            },
            {
                question: "¿Cuáles son las partes principales de una Carta de Aproximación Jeppesen?",
                options: [
                    "Introducción, desarrollo y conclusión.",
                    "Encabezado, vista en planta, vista de perfil y tabla de mínimos meteorológicos.",
                    "Índice, glosario y bibliografía.",
                    "Resumen, apéndice y anexos."
                ],
                correctAnswer: "Encabezado, vista en planta, vista de perfil y tabla de mínimos meteorológicos.",
                module: 2
            },
            {
                question: "¿Qué información se encuentra en el encabezado de una Carta de Aproximación Jeppesen?",
                options: [
                    "Título del procedimiento, nombre del piloto y fecha del vuelo.",
                    "Ciudad y país, nombre del procedimiento, fecha de publicación y efectividad, códigos OACI e IATA del aeropuerto, frecuencias de comunicación, altitudes mínimas y DA(H)/MDA.",
                    "Instrucciones de la torre de control, velocidad del viento y dirección de la pista.",
                    "Lista de pasajeros, número de vuelo y tipo de aeronave."
                ],
                correctAnswer: "Ciudad y país, nombre del procedimiento, fecha de publicación y efectividad, códigos OACI e IATA del aeropuerto, frecuencias de comunicación, altitudes mínimas y DA(H)/MDA.",
                module: 2
            },
            {
                question: "¿Qué elementos se pueden encontrar en la vista en planta de una Carta de Aproximación Jeppesen?",
                options: [
                    "Instrucciones de despegue, velocidad de ascenso y ángulo de alabeo.",
                    "Radioayudas a cruzar, radiales, altitudes a volar, altitudes mínimas, distancias, IAF, IF, FAF, DA/H, VDP, MAP, patrones de espera.",
                    "Información del radar meteorológico, tipo de nubes y visibilidad.",
                    "Rutas de rodaje en tierra, posiciones de estacionamiento y servicios de combustible."
                ],
                correctAnswer: "Radioayudas a cruzar, radiales, altitudes a volar, altitudes mínimas, distancias, IAF, IF, FAF, DA/H, VDP, MAP, patrones de espera.",
                module: 2
            },
            {
                question: "¿Qué información proporciona la vista de perfil en una Carta de Aproximación Jeppesen?",
                options: [
                    "Rutas de navegación en ruta, waypoints y distancias entre aeropuertos.",
                    "Altitudes, DA(H)/MDA y el MAP, relacionados con los descensos necesarios durante la aproximación.",
                    "Frecuencias de radio de la torre de control, procedimientos de comunicación y fraseología.",
                    "Información sobre el terreno, obstáculos y elevaciones del terreno."
                ],
                correctAnswer: "Altitudes, DA(H)/MDA y el MAP, relacionados con los descensos necesarios durante la aproximación.",
                module: 2
            },
            {
                question: "¿Qué tipo de información se encuentra en la tabla de mínimos meteorológicos?",
                options: [
                    "Pronósticos de temperatura, presión y humedad.",
                    "Mínimos de visibilidad y techo de nubes requeridos para el procedimiento de aproximación.",
                    "Información sobre tormentas, turbulencia y cizalladura del viento.",
                    "Datos sobre la calidad del aire, niveles de contaminación y radiación solar."
                ],
                correctAnswer: "Mínimos de visibilidad y techo de nubes requeridos para el procedimiento de aproximación.",
                module: 2
            },
            {
                question: "¿En qué orden se recomienda leer las cartas de aproximación?",
                options: [
                    "De izquierda a derecha y de abajo hacia arriba.",
                    "De derecha a izquierda y en espiral.",
                    "En cualquier orden, siempre y cuando se revise toda la información.",
                    "De arriba hacia abajo, en forma de lista."
                ],
                correctAnswer: "De derecha a izquierda y en espiral.",
                module: 3
            },
            {
                question: "¿Qué indican las frecuencias ATIS con el indicativo 'D'?",
                options: [
                    "Frecuencias de la torre de control digital.",
                    "Frecuencias de aproximación con servicio de radar.",
                    "Servicio automático de información terminal digital.",
                    "Frecuencias de emergencia."
                ],
                correctAnswer: "Servicio automático de información terminal digital.",
                module: 3
            },
            {
                question: "¿Qué representan los símbolos VOR, NDB, ILS y DME en una carta de aproximación?",
                options: [
                    "Tipos de aeronaves.",
                    "Radioayudas para la navegación.",
                    "Puntos de notificación obligatorios.",
                    "Zonas de espacio aéreo restringido."
                ],
                correctAnswer: "Radioayudas para la navegación.",
                module: 3
            },
            {
                question: "¿Cuál es la función de los patrones de espera en un procedimiento de aproximación?",
                options: [
                    "Proporcionar una ruta de escape en caso de emergencia.",
                    "Permitir a las aeronaves ajustar su velocidad y altitud antes de la aproximación final.",
                    "Indicar la ubicación de las pistas de aterrizaje.",
                    "Señalizar la dirección del viento."
                ],
                correctAnswer: "Permitir a las aeronaves ajustar su velocidad y altitud antes de la aproximación final.",
                module: 3
            },
            {
                question: "¿Dónde se encuentra la descripción del procedimiento de aproximación frustrada en una carta?",
                options: [
                    "En el encabezado de la carta.",
                    "En la vista de perfil, cerca de la tabla de mínimos.",
                    "En la vista en planta, y potencialmente con iconos.",
                    "En una sección separada de notas y restricciones."
                ],
                correctAnswer: "En la vista en planta, y potencialmente con iconos.",
                module: 3
            },
            {
                question: "¿Qué tipo de información se encuentra en las cartas de aeródromo?",
                options: [
                    "Rutas de navegación en ruta y waypoints.",
                    "Características de pistas, mínimos de despegue y posiciones de estacionamiento.",
                    "Frecuencias de radio de la torre de control y procedimientos de comunicación.",
                    "Información sobre el terreno, obstáculos y elevaciones del terreno."
                ],
                correctAnswer: "Características de pistas, mínimos de despegue y posiciones de estacionamiento.",
                module: 4
            },
            {
                question: "¿Por qué son relevantes las Cartas Jeppesen para vuelos internacionales?",
                options: [
                    "Porque son más baratas que otras cartas.",
                    "Debido a su formato estándar y la información adicional que suelen contener.",
                    "Porque son obligatorias para todos los vuelos internacionales.",
                    "Porque están disponibles en más idiomas."
                ],
                correctAnswer: "Debido a su formato estándar y la información adicional que suelen contener.",
                module: 4
            },
            {
                question: "¿Qué se enfatiza como fundamental para convertirse en un buen piloto, además de la instrucción formal?",
                options: [
                    "La suerte y el talento natural.",
                    "La capacidad de memorizar toda la información de las cartas.",
                    "El estudio personal y la práctica continua.",
                    "La experiencia de vuelo en simuladores avanzados."
                ],
                correctAnswer: "El estudio personal y la práctica continua.",
                module: 4
            },
            {
                question: "¿Cómo se utilizan las Cartas Jeppesen digitales?",
                options: [
                    "Se imprimen en papel de gran formato.",
                    "Se transmiten por radio a la aeronave durante el vuelo.",
                    "Se visualizan en herramientas como Electronic Flight Bags (EFBs).",
                    "Se proyectan en el parabrisas de la aeronave."
                ],
                correctAnswer: "Se visualizan en herramientas como Electronic Flight Bags (EFBs).",
                module: 4
            },
            {
                question: "¿En qué aspectos difieren las Cartas Jeppesen de otras cartas aeronáuticas, como las de la NOS?",
                options: [
                    "No hay diferencias significativas.",
                    "En el color del papel y el tamaño de la letra.",
                    "En la claridad de presentación del terreno, manejo de componentes inoperativos y ubicación de información importante.",
                    "Las Cartas Jeppesen son solo para uso militar, mientras que las de la NOS son para aviación civil."
                ],
                correctAnswer: "En la claridad de presentación del terreno, manejo de componentes inoperativos y ubicación de información importante.",
                module: 5
            },
            {
                question: "¿Cuál es un factor a considerar al decidir si el costo de las Cartas Jeppesen se justifica para pilotos de aviación general (GA) que vuelan IFR?",
                options: [
                    "Si el piloto vuela principalmente en áreas rurales.",
                    "Si el piloto tiene buena visión nocturna.",
                    "Los beneficios en claridad y organización frente al costo.",
                    "Si el piloto prefiere usar cartas en papel en lugar de digitales."
                ],
                correctAnswer: "Los beneficios en claridad y organización frente al costo.",
                module: 5
            }
        ];

        const quizContent = document.getElementById('quiz-content');
        const resultsContainer = document.getElementById('results');
        const finalScoreDisplay = document.getElementById('final-score');
        const totalQuestionsDisplay = document.getElementById('total-questions');
        const percentageDisplay = document.getElementById('percentage');
        const restartButton = document.getElementById('restart-button');
        let currentQuestionIndex = 0;
        let score = 0;
        let userAnswers = [];
        let currentModule = 1; // Start with module 1

        function loadQuizContent() {
            quizContent.innerHTML = ''; // Clear previous content
            const moduleQuestions = quizData.filter(q => q.module === currentModule);

            if (moduleQuestions.length === 0) {
                // If there are no questions for the current module, show a message
                quizContent.innerHTML = `<p class="text-center text-gray-500 py-8">No hay preguntas disponibles para el Módulo ${currentModule}.</p>`;
                if (currentModule > 1) {
                    // Show restart button if it's not the first module
                    const button = document.createElement('button');
                    button.textContent = 'Ver Resultados'; // Change button text
                    button.className = 'button primary-button mt-4';
                    button.onclick = showResults;
                    quizContent.appendChild(button);
                }
                return;
            }

            const currentQuestion = moduleQuestions[currentQuestionIndex];

            const questionElement = document.createElement('p');
            questionElement.className = 'question';
            questionElement.textContent = currentQuestion.question;

            const optionsElement = document.createElement('div');
            optionsElement.className = 'options';

            currentQuestion.options.forEach((option, index) => {
                const optionElement = document.createElement('label');
                optionElement.className = 'option';

                const radioInput = document.createElement('input');
                radioInput.type = 'radio';
                radioInput.name = 'question';
                radioInput.value = option;
                radioInput.id = `option-${index}`;
                radioInput.addEventListener('change', () => {
                    userAnswers[currentQuestionIndex] = option;
                });

                optionElement.appendChild(radioInput);
                optionElement.appendChild(document.createTextNode(option));
                optionsElement.appendChild(optionElement);
            });

            const actionsElement = document.createElement('div');
            actionsElement.className = 'actions';

            const nextButton = document.createElement('button');
            nextButton.textContent = 'Siguiente';
            nextButton.className = 'button primary-button';
            nextButton.addEventListener('click', () => {
                if (userAnswers[currentQuestionIndex] === undefined) {
                    alert('Por favor, selecciona una respuesta.');
                    return;
                }

                if (userAnswers[currentQuestionIndex] === currentQuestion.correctAnswer) {
                    score++;
                }

                currentQuestionIndex++;

                if (currentQuestionIndex < moduleQuestions.length) {
                    loadQuizContent();
                } else {
                    // Move to the next module
                    currentModule++;
                    currentQuestionIndex = 0; // Reset question index for the new module
                    if (currentModule <= 5) { // Assuming 5 modules
                        loadQuizContent(); // Load the first question of the next module
                    }
                    else{
                         showResults();
                    }

                }
            });

            const prevButton = document.createElement('button');
            prevButton.textContent = 'Anterior';
            prevButton.className = 'button secondary-button';
            prevButton.addEventListener('click', () => {
                currentQuestionIndex--;
                if (currentQuestionIndex >= 0) {
                    loadQuizContent();
                } else {
                    currentQuestionIndex = 0;
                }
            });

            if (currentQuestionIndex > 0) {
                actionsElement.appendChild(prevButton);
            }
            actionsElement.appendChild(nextButton);

            quizContent.appendChild(questionElement);
            quizContent.appendChild(optionsElement);
            quizContent.appendChild(actionsElement);
        }

        function showResults() {
            quizContent.classList.add('hidden');
            resultsContainer.classList.remove('hidden');

            const totalQuestions = quizData.filter(q => q.module <= 5).length; // Get total number of questions
            const percentage = (score / totalQuestions) * 100;

            finalScoreDisplay.textContent = score;
            totalQuestionsDisplay.textContent = totalQuestions;
            percentageDisplay.textContent = percentage.toFixed(2);
        }

        restartButton.addEventListener('click', () => {
            currentQuestionIndex = 0;
            score = 0;
            userAnswers = [];
            currentModule = 1; // Restart from Module 1
            resultsContainer.classList.add('hidden');
            quizContent.classList.remove('hidden');
            loadQuizContent();
        });

        loadQuizContent(); // Start the quiz
    </script>
</body>
</html>
