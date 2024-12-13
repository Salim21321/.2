<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Английский тест B1-B2</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #e0f7fa, #82caff);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            color: #333;
        }

        .container {
            width: 90%;
            max-width: 700px;
            background: #fff;
            border-radius: 20px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
            padding: 20px;
            text-align: center;
            overflow: hidden;
        }

        .intro {
            background-color: #0288d1;
            color: #fff;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            font-size: 18px;
        }

        .intro h2 {
            margin-top: 0;
            font-size: 24px;
        }

        .intro p {
            font-size: 16px;
            line-height: 1.6;
        }

        #question {
            font-size: 22px;
            font-weight: bold;
            color: #0288d1;
            margin-bottom: 20px;
        }

        #options {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }

        button {
            background-color: #4caf50;
            color: white;
            font-size: 16px;
            padding: 12px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        button:hover {
            background-color: #45a049;
            transform: scale(1.05);
        }

        button:active {
            background-color: #3e8e41;
        }

        .result {
            font-size: 20px;
            font-weight: bold;
            color: #00796b;
            margin-top: 20px;
        }
    </style>
    <script>
        const questions = [
            { question: "What is the past tense of the verb 'go'?", answers: ["went", "gone", "goes"], correctAnswer: 0 },
            { question: "I _______ to the store yesterday.", answers: ["goes", "went", "going"], correctAnswer: 1 },
            { question: "What is the opposite of 'cheap'?", answers: ["expensive", "costly", "low"], correctAnswer: 0 },
            { question: "Which of the following is a synonym for 'happy'?", answers: ["sad", "cheerful", "angry"], correctAnswer: 1 },
            { question: "Fill in the blank: 'He is _______ student in the class.'", answers: ["the smartest", "smartest", "more smarter"], correctAnswer: 0 },
            { question: "Which sentence is in the passive voice?", answers: ["The book was read by the teacher.", "The teacher reads the book.", "The teacher will read the book."], correctAnswer: 0 },
            { question: "What does 'reliable' mean?", answers: ["Someone who is easy to trust", "Something that is not trustworthy", "Someone who is always late"], correctAnswer: 0 },
            { question: "Fill in the blank: 'She hasn’t finished her homework _______.',", answers: ["already", "yet", "never"], correctAnswer: 1 },
            { question: "Which sentence is in the future perfect tense?", answers: ["I will have finished my work by tomorrow.", "I finish my work tomorrow.", "I will finish my work tomorrow."], correctAnswer: 0 },
            { question: "What does the idiom 'break the ice' mean?", answers: ["To start a fire", "To make a situation less awkward", "To literally break ice"], correctAnswer: 1 },
            { question: "Which of the following is a compound sentence?", answers: ["She likes pizza and pasta.", "I will go if it stops raining.", "She went to the store because she needed milk."], correctAnswer: 2 },
            { question: "Choose the correct word: 'I have been _______ to the museum.'", answers: ["gone", "been", "go"], correctAnswer: 1 },
            { question: "What is the correct plural form of 'child'?", answers: ["children", "childs", "childes"], correctAnswer: 0 },
            { question: "Choose the correct phrase: 'I prefer reading _______ watching TV.'", answers: ["than", "to", "for"], correctAnswer: 1 },
            { question: "What does 'to be in charge' mean?", answers: ["To have control or responsibility", "To be excited", "To be lazy"], correctAnswer: 0 },
            { question: "Which sentence uses 'much' correctly?", answers: ["I have much friends.", "I don't have much time.", "I have much fun."], correctAnswer: 1 },
            { question: "Choose the correct word: 'She is interested _______ art.'", answers: ["at", "in", "on"], correctAnswer: 1 },
            { question: "What is the correct form of the verb in the sentence: 'By the time you arrive, I _______ my homework.'", answers: ["will finish", "finished", "will have finished"], correctAnswer: 2 },
            { question: "What is the past participle of 'eat'?", answers: ["ate", "eaten", "eats"], correctAnswer: 1 },
            { question: "Which of these is an example of a countable noun?", answers: ["water", "apple", "information"], correctAnswer: 1 },
            { question: "What does 'in the long run' mean?", answers: ["Immediately", "After a long time", "During a long trip"], correctAnswer: 1 },
            { question: "Which word is a noun?", answers: ["run", "beautiful", "happiness"], correctAnswer: 2 },
            { question: "Which word is an adjective?", answers: ["quickly", "beautiful", "walked"], correctAnswer: 1 },
            { question: "Fill in the blank: 'I _______ to the gym twice a week.'", answers: ["go", "going", "went"], correctAnswer: 0 },
            { question: "What is the meaning of the idiom 'piece of cake'?", answers: ["Something very difficult", "Something very easy", "A literal cake"], correctAnswer: 1 },
            { question: "Choose the correct word: 'The book _______ by the author last year.'", answers: ["was written", "is written", "will be written"], correctAnswer: 0 },
            { question: "What is the meaning of the phrasal verb 'give up'?", answers: ["to stop trying", "to continue", "to give away something"], correctAnswer: 0 },
            { question: "What is the superlative form of 'far'?", answers: ["farthest", "further", "farther"], correctAnswer: 0 },
        ];

        let currentQuestionIndex = 0;
        let score = 0;

        function displayQuestion() {
            if (currentQuestionIndex < questions.length) {
                document.getElementById("question").textContent = questions[currentQuestionIndex].question;

                const options = document.getElementById("options");
                options.innerHTML = '';
                questions[currentQuestionIndex].answers.forEach((answer, index) => {
                    const button = document.createElement("button");
                    button.textContent = answer;
                    button.classList.add("btn-text");
                    button.onclick = function () { checkAnswer(index); };
                    options.appendChild(button);
                });
            } else {
document.getElementById("question").textContent = "Тест завершен!";
                document.getElementById("options").innerHTML = `Ваш балл: ${score} из ${questions.length}`;
            }
        }

        
        function checkAnswer(selectedIndex) {
            const correctIndex = questions[currentQuestionIndex].correctAnswer; 
            if (selectedIndex === correctIndex) {
                score++; т
            }
            currentQuestionIndex++; 
            displayQuestion(); 
        }

        
        window.onload = displayQuestion;
    </script>
</head>
<body>
    <div class="container">
        <div class="intro">
            <h2>Добро пожаловать в тест по английскому языку!</h2>
            <p>Этот тест поможет вам улучшить знание английского языка на уровнях B1 и B2. Здесь вы найдете вопросы на грамматику, лексику и правильное использование языка в повседневной жизни.</p>
            <p>Ответьте на вопросы и проверьте, насколько хорошо вы понимаете английский!</p>
        </div>
        
        <div class="test-content">
            <p id="question"></p> 
            <div id="options"></div> 
        </div>
    </div>
</body>
</html>
