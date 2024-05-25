!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JavaScript Quiz Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f4f4f4;
        }
        .quiz-container {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            max-width: 500px;
            width: 100%;
        }
        .question {
            font-size: 20px;
            margin-bottom: 20px;
        }
        .answers {
            list-style: none;
            padding: 0;
        }
        .answers li {
            margin-bottom: 10px;
        }
        .answers button {
            width: 100%;
            padding: 10px;
            background-color: #007BFF;
            border: none;
            color: white;
            border-radius: 4px;
            cursor: pointer;
        }
        .answers button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <div id="quiz">
            <div id="question-container">
                <p class="question" id="question"></p>
                <ul class="answers" id="answers"></ul>
            </div>
            <button id="next-button" style="display: none;">Next</button>
        </div>
    </div>
    <script>
        const questions = [
            {
                question: "What is the capital of France?",
                answers: ["Berlin", "Madrid", "Paris", "Lisbon"],
                correct: 2,
                difficulty: 1
            },
            {
                question: "Which planet is known as the Red Planet?",
                answers: ["Earth", "Mars", "Jupiter", "Saturn"],
                correct: 1,
                difficulty: 1
            },
            {
                question: "Who wrote 'To Kill a Mockingbird'?",
                answers: ["Harper Lee", "J.K. Rowling", "Ernest Hemingway", "Mark Twain"],
                correct: 0,
                difficulty: 2
            },
            {
                question: "What is the square root of 144?",
                answers: ["10", "12", "14", "16"],
                correct: 1,
                difficulty: 2
            },
            {
                question: "What country has the highest life expectancy?",
                answers: ["Japan", "Switzerland", "Hong Kong", "Singapore"],
                correct: 2,
                difficulty: 2
            },
            {
                question: "Where would you be if you were standing on the Spanish Steps?",
                answers: ["Madrid", "Barcelona", "Seville", "Rome"],
                correct: 3,
                difficulty: 2
            },
            {
                question: "Which language has more native speakers: English or Spanish?",
                answers: ["English", "Spanish"],
                correct: 1,
                difficulty: 1
            },
            {
                question: "What is the most common surname in the United States?",
                answers: ["Johnson", "Williams", "Smith", "Brown"],
                correct: 2,
                difficulty: 1
            },
            {
                question: "What disease commonly spread on pirate ships?",
                answers: ["Scurvy", "Malaria", "Tuberculosis", "Smallpox"],
                correct: 0,
                difficulty: 2
            },
            {
                question: "Who was the Ancient Greek God of the Sun?",
                answers: ["Zeus", "Apollo", "Hermes", "Ares"],
                correct: 1,
                difficulty: 2
            },
            {
                question: "What was the name of the crime boss who was head of the feared Chicago Outfit?",
                answers: ["Al Capone", "Bugsy Siegel", "John Dillinger", "Lucky Luciano"],
                correct: 0,
                difficulty: 3
            },
            {
                question: "What year was the United Nations established?",
                answers: ["1918", "1939", "1945", "1955"],
                correct: 2,
                difficulty: 2
            },
            {
                question: "Who has won the most total Academy Awards?",
                answers: ["Steven Spielberg", "Walt Disney", "Katharine Hepburn", "Meryl Streep"],
                correct: 1,
                difficulty: 3
            },
            {
                question: "What artist has the most streams on Spotify?",
                answers: ["Taylor Swift", "Ed Sheeran", "Drake", "Ariana Grande"],
                correct: 2,
                difficulty: 1
            },
            {
                question: "How many minutes are in a full week?",
                answers: ["10,080", "8,640", "5,760", "15,000"],
                correct: 0,
                difficulty: 1
            },
            {
                question: "What car manufacturer had the highest revenue in 2020?",
                answers: ["Toyota", "Volkswagen", "Ford", "General Motors"],
                correct: 1,
                difficulty: 3
            }
        ];

        let currentQuestionIndex = 0;
        let score = 0;

        const questionContainer = document.getElementById('question-container');
        const questionElement = document.getElementById('question');
        const answersElement = document.getElementById('answers');
        const nextButton = document.getElementById('next-button');

        function loadQuestion() {
            const currentQuestion = questions[currentQuestionIndex];
            questionElement.textContent = currentQuestion.question;
            answersElement.innerHTML = '';
            currentQuestion.answers.forEach((answer, index) => {
                const answerButton = document.createElement('button');
                answerButton.textContent = answer;
                answerButton.addEventListener('click', () => selectAnswer(index));
                const answerListItem = document.createElement('li');
                answerListItem.appendChild(answerButton);
                answersElement.appendChild(answerListItem);
            });
        }

        function selectAnswer(index) {
            const correctIndex = questions[currentQuestionIndex].correct;
            if (index === correctIndex) {
                score++;
                alert('Correct!');
            } else {
                alert('Wrong answer.');
            }
            saveProgress();
            nextButton.style.display = 'block';
        }

        function saveProgress() {
            localStorage.setItem('currentQuestionIndex', currentQuestionIndex);
            localStorage.setItem('score', score);
        }

        function loadProgress() {
            const savedQuestionIndex = localStorage.getItem('currentQuestionIndex');
            const savedScore = localStorage.getItem('score');
            if (savedQuestionIndex !== null) {
                currentQuestionIndex = parseInt(savedQuestionIndex);
            }
            if (savedScore !== null) {
                score = parseInt(savedScore);
            }
        }

        function nextQuestion() {
            currentQuestionIndex++;
            if (currentQuestionIndex < questions.length) {
                loadQuestion();
                nextButton.style.display = 'none';
            } else {
                questionContainer.innerHTML = `<p>Your score is ${score} out of ${questions.length}</p>`;
                localStorage.clear();
            }
        }

        nextButton.addEventListener('click', nextQuestion);

        window.addEventListener('load', () => {
            loadProgress();
            loadQuestion();
        });
    </script>
</body>
</html>

