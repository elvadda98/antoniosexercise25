<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Giochi di Lingua Italiana</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0f2027 0%, #203a43 50%, #2c5364 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
        }

        .container {
            max-width: 1200px;
            width: 100%;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #0f2027, #203a43);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .game-selector {
            display: flex;
            justify-content: center;
            background: #f0f0f0;
            padding: 15px;
            border-bottom: 2px solid #ddd;
        }

        .game-btn {
            background: linear-gradient(135deg, #2c5364, #203a43);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 0 10px;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(44, 83, 100, 0.3);
        }

        .game-btn:hover, .game-btn.active {
            background: linear-gradient(135deg, #0f2027, #203a43);
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(15, 32, 39, 0.4);
        }

        .game-section {
            padding: 30px;
            display: none;
        }

        .game-section.active {
            display: block;
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f8);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #0f2027;
            box-shadow: 0 4px 15px rgba(15, 32, 39, 0.2);
        }

        .word-bank h3 {
            color: #0f2027;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #0f2027, #203a43);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(15, 32, 39, 0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(15, 32, 39, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #0f2027;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #0f2027;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .check-btn {
            background: linear-gradient(135deg, #0f2027, #203a43);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(15, 32, 39, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(15, 32, 39, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #0f2027, #203a43);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(15, 32, 39, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 24px;
            margin-right: 10px;
            vertical-align: middle;
        }

        .shuffle-btn {
            background: linear-gradient(135deg, #2c5364, #203a43);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 14px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(44, 83, 100, 0.3);
        }

        .shuffle-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(44, 83, 100, 0.4);
        }

        /* Multiple Choice Styles */
        .options-container {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
            margin-top: 20px;
        }

        .option {
            background: linear-gradient(135deg, #0f2027, #203a43);
            color: white;
            padding: 15px 25px;
            border-radius: 10px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
            text-align: center;
            min-width: 150px;
        }

        .option:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(15, 32, 39, 0.4);
        }

        .option.correct {
            background: linear-gradient(135deg, #4CAF50, #2E7D32);
        }

        .option.incorrect {
            background: linear-gradient(135deg, #f44336, #c62828);
        }

        /* Matching Game Styles */
        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        .column {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .match-item {
            background: linear-gradient(135deg, #0f2027, #203a43);
            color: white;
            padding: 15px;
            margin: 10px 0;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
        }

        .match-item.selected {
            background: linear-gradient(135deg, #2c5364, #203a43);
            transform: scale(1.05);
        }

        .match-item.matched {
            background: linear-gradient(135deg, #4CAF50, #2E7D32);
            cursor: default;
        }

        /* Flashcard Styles */
        .flashcard-container {
            perspective: 1000px;
            width: 300px;
            height: 200px;
            margin: 0 auto;
        }

        .flashcard {
            width: 100%;
            height: 100%;
            position: relative;
            transform-style: preserve-3d;
            transition: transform 0.6s;
            cursor: pointer;
        }

        .flashcard.flipped {
            transform: rotateY(180deg);
        }

        .flashcard-front, .flashcard-back {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            font-size: 1.5em;
            font-weight: bold;
            color: white;
        }

        .flashcard-front {
            background: linear-gradient(135deg, #0f2027, #203a43);
        }

        .flashcard-back {
            background: linear-gradient(135deg, #2c5364, #203a43);
            transform: rotateY(180deg);
        }

        .flashcard-controls {
            display: flex;
            justify-content: center;
            margin-top: 30px;
            gap: 15px;
        }

        @media (max-width: 768px) {
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
            
            .game-selector {
                flex-wrap: wrap;
                gap: 10px;
            }
            
            .matching-container {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="score">Punteggio: <span id="score">0</span>/<span id="total">0</span></div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-language icon"></i> Giochi di Lingua Italiana</h1>
            <p>Scegli un gioco per migliorare il tuo italiano!</p>
        </div>

        <div class="game-selector">
            <button class="game-btn active" data-game="fill-blanks">Completa le Frasi</button>
            <button class="game-btn" data-game="multiple-choice">Scelta Multipla</button>
            <button class="game-btn" data-game="matching">Abbinamento</button>
            <button class="game-btn" data-game="flashcards">Flashcard</button>
        </div>

        <!-- Fill in the Blanks Game -->
        <div class="game-section active" id="fill-blanks">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Parole da usare:</h3>
                <div class="word-options">
                    <span class="word-option">both</span>
                    <span class="word-option">price</span>
                    <span class="word-option">near</span>
                    <span class="word-option">inside</span>
                    <span class="word-option">far</span>
                </div>
            </div>

            <button class="shuffle-btn" onclick="shuffleQuestions()">
                <i class="fas fa-random"></i> Mescola le Frasi
            </button>

            <div id="questions-container">
                <!-- Le domande verranno inserite dinamicamente qui -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Controlla Risposte</button>
        </div>

        <!-- Multiple Choice Game -->
        <div class="game-section" id="multiple-choice">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Scegli la risposta corretta:</h3>
            </div>

            <div id="mc-questions-container">
                <!-- Le domande a scelta multipla verranno inserite dinamicamente qui -->
            </div>

            <button class="check-btn" onclick="checkMultipleChoice()">Controlla Risposte</button>
        </div>

        <!-- Matching Game -->
        <div class="game-section" id="matching">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Abbina le parole alle loro traduzioni:</h3>
            </div>

            <div class="matching-container">
                <div class="column" id="left-column">
                    <h3 style="text-align: center;">Inglese</h3>
                    <!-- Le parole inglesi verranno inserite dinamicamente qui -->
                </div>
                <div class="column" id="right-column">
                    <h3 style="text-align: center;">Italiano</h3>
                    <!-- Le parole italiane verranno inserite dinamicamente qui -->
                </div>
            </div>

            <button class="check-btn" onclick="checkMatching()">Controlla Abbinamenti</button>
        </div>

        <!-- Flashcards Game -->
        <div class="game-section" id="flashcards">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Flashcard - Clicca per girare:</h3>
            </div>

            <div class="flashcard-container">
                <div class="flashcard" id="current-flashcard">
                    <div class="flashcard-front">
                        <span id="flashcard-front-text">Parola</span>
                    </div>
                    <div class="flashcard-back">
                        <span id="flashcard-back-text">Traduzione</span>
                    </div>
                </div>
            </div>

            <div class="flashcard-controls">
                <button class="shuffle-btn" onclick="prevFlashcard()">
                    <i class="fas fa-arrow-left"></i> Precedente
                </button>
                <button class="shuffle-btn" onclick="flipFlashcard()">
                    <i class="fas fa-sync-alt"></i> Gira
                </button>
                <button class="shuffle-btn" onclick="nextFlashcard()">
                    Successiva <i class="fas fa-arrow-right"></i>
                </button>
            </div>
        </div>
    </div>

    <script>
        let score = 0;
        let totalQuestions = 0;
        let currentGame = "fill-blanks";
        
        // Fill in the blanks questions
        let questions = [
            {
                id: 1,
                question: "I like <input type='text' class='fill-blank' data-answer='both' placeholder='risposta'> chocolate and vanilla ice cream.",
                answer: "both"
            },
            {
                id: 2,
                question: "The <input type='text' class='fill-blank' data-answer='price' placeholder='risposta'> of this car is too high for my budget.",
                answer: "price"
            },
            {
                id: 3,
                question: "My apartment is <input type='text' class='fill-blank' data-answer='near' placeholder='risposta'> the city center.",
                answer: "near"
            },
            {
                id: 4,
                question: "It's raining, so let's stay <input type='text' class='fill-blank' data-answer='inside' placeholder='risposta'>.",
                answer: "inside"
            },
            {
                id: 5,
                question: "The mountains are <input type='text' class='fill-blank' data-answer='far' placeholder='risposta'> from here.",
                answer: "far"
            },
            {
                id: 6,
                question: "<input type='text' class='fill-blank' data-answer='both' placeholder='risposta'> of my parents are doctors.",
                answer: "both"
            },
            {
                id: 7,
                question: "What's the <input type='text' class='fill-blank' data-answer='price' placeholder='risposta'> of this shirt?",
                answer: "price"
            },
            {
                id: 8,
                question: "Is there a grocery store <input type='text' class='fill-blank' data-answer='near' placeholder='risposta'> here?",
                answer: "near"
            },
            {
                id: 9,
                question: "The cat is hiding <input type='text' class='fill-blank' data-answer='inside' placeholder='risposta'> the box.",
                answer: "inside"
            },
            {
                id: 10,
                question: "How <input type='text' class='fill-blank' data-answer='far' placeholder='risposta'> is the beach from your house?",
                answer: "far"
            },
            {
                id: 11,
                question: "We can <input type='text' class='fill-blank' data-answer='both' placeholder='risposta'> go to the party together.",
                answer: "both"
            },
            {
                id: 12,
                question: "The <input type='text' class='fill-blank' data-answer='price' placeholder='risposta'> includes taxes and shipping.",
                answer: "price"
            }
        ];

        // Multiple choice questions
        let mcQuestions = [
            {
                question: "What does 'gatto' mean in English?",
                options: ["Cat", "Dog", "Bird", "Fish"],
                answer: "Cat"
            },
            {
                question: "How do you say 'house' in Italian?",
                options: ["Casa", "Macchina", "Scuola", "Ufficio"],
                answer: "Casa"
            },
            {
                question: "What is the Italian word for 'book'?",
                options: ["Libro", "Quaderno", "Rivista", "Giornale"],
                answer: "Libro"
            },
            {
                question: "What does 'buongiorno' mean?",
                options: ["Good morning", "Good night", "Thank you", "Please"],
                answer: "Good morning"
            },
            {
                question: "How do you say 'water' in Italian?",
                options: ["Acqua", "Vino", "Birra", "Caffè"],
                answer: "Acqua"
            }
        ];

        // Matching pairs
        let matchingPairs = [
            { english: "Hello", italian: "Ciao" },
            { english: "Goodbye", italian: "Arrivederci" },
            { english: "Thank you", italian: "Grazie" },
            { english: "Please", italian: "Per favore" },
            { english: "Sorry", italian: "Scusa" },
            { english: "Yes", italian: "Sì" },
            { english: "No", italian: "No" },
            { english: "Maybe", italian: "Forse" }
        ];

        // Flashcards data
        let flashcards = [
            { front: "Cat", back: "Gatto" },
            { front: "Dog", back: "Cane" },
            { front: "House", back: "Casa" },
            { front: "Book", back: "Libro" },
            { front: "Water", back: "Acqua" },
            { front: "Food", back: "Cibo" },
            { front: "Friend", back: "Amico" },
            { front: "Family", back: "Famiglia" }
        ];

        let currentFlashcardIndex = 0;
        let selectedMatchItems = { left: null, right: null };
        let matchedPairs = [];

        // Initialize the page
        window.onload = function() {
            // Set up game navigation
            document.querySelectorAll('.game-btn').forEach(button => {
                button.addEventListener('click', function() {
                    // Remove active class from all buttons and sections
                    document.querySelectorAll('.game-btn').forEach(btn => btn.classList.remove('active'));
                    document.querySelectorAll('.game-section').forEach(section => section.classList.remove('active'));
                    
                    // Add active class to clicked button and corresponding section
                    this.classList.add('active');
                    currentGame = this.dataset.game;
                    document.getElementById(currentGame).classList.add('active');
                    
                    // Initialize the selected game
                    initGame(currentGame);
                });
            });
            
            // Initialize the first game
            initGame(currentGame);
        };

        // Initialize the selected game
        function initGame(gameType) {
            switch(gameType) {
                case "fill-blanks":
                    totalQuestions = questions.length;
                    document.getElementById('total').textContent = totalQuestions;
                    shuffleQuestions();
                    break;
                case "multiple-choice":
                    totalQuestions = mcQuestions.length;
                    document.getElementById('total').textContent = totalQuestions;
                    renderMultipleChoice();
                    break;
                case "matching":
                    totalQuestions = matchingPairs.length;
                    document.getElementById('total').textContent = totalQuestions;
                    renderMatchingGame();
                    break;
                case "flashcards":
                    totalQuestions = flashcards.length;
                    document.getElementById('total').textContent = totalQuestions;
                    renderFlashcard();
                    break;
            }
            score = 0;
            document.getElementById('score').textContent = score;
        }

        // Fill in the blanks functions
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        function renderQuestions() {
            const container = document.getElementById('questions-container');
            container.innerHTML = '';
            
            questions.forEach((q, index) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'question';
                questionDiv.innerHTML = `
                    <h3>Domanda ${index + 1}:</h3>
                    <p>${q.question}</p>
                    <div class="feedback" id="feedback-${q.id}" style="display: none;"></div>
                `;
                container.appendChild(questionDiv);
            });
        }

        function shuffleQuestions() {
            questions = shuffleArray([...questions]);
            renderQuestions();
            
            // Show confirmation message
            const feedback = document.createElement('div');
            feedback.className = 'feedback correct';
            feedback.textContent = 'Frasi mescolate!';
            feedback.style.marginTop = '10px';
            feedback.style.marginBottom = '20px';
            
            const container = document.getElementById('questions-container');
            container.parentNode.insertBefore(feedback, container);
            
            // Remove message after 2 seconds
            setTimeout(() => {
                feedback.remove();
            }, 2000);
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Find question ID from input field
                const inputId = blank.closest('.question').querySelector('.feedback').id.split('-')[1];
                const feedback = document.getElementById(`feedback-${inputId}`);
                
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Corretto!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Sbagliato. La risposta corretta è: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            // Update score
            score = correctCount;
            document.getElementById('score').textContent = score;
            
            // Show final score
            const finalFeedback = document.createElement('div');
            finalFeedback.className = 'feedback ' + (score === questions.length ? 'correct' : 'incorrect');
            finalFeedback.textContent = score === questions.length ? 
                '🎉 Complimenti! Hai risposto correttamente a tutte le domande!' : 
                `Hai totalizzato ${score} punti su ${questions.length}. Continua a esercitarti!`;
            finalFeedback.style.marginTop = '20px';
            
            const checkBtn = document.querySelector('.check-btn');
            checkBtn.parentNode.insertBefore(finalFeedback, checkBtn.nextSibling);
            
            // Remove message after 5 seconds
            setTimeout(() => {
                finalFeedback.remove();
            }, 5000);
        }

        // Multiple choice functions
        function renderMultipleChoice() {
            const container = document.getElementById('mc-questions-container');
            container.innerHTML = '';
            
            mcQuestions.forEach((q, index) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'question';
                
                // Shuffle options
                const shuffledOptions = shuffleArray([...q.options]);
                
                let optionsHTML = '';
                shuffledOptions.forEach(option => {
                    optionsHTML += `<div class="option" data-value="${option}">${option}</div>`;
                });
                
                questionDiv.innerHTML = `
                    <h3>Domanda ${index + 1}:</h3>
                    <p>${q.question}</p>
                    <div class="options-container">
                        ${optionsHTML}
                    </div>
                    <div class="feedback" id="mc-feedback-${index}" style="display: none;"></div>
                `;
                container.appendChild(questionDiv);
                
                // Add event listeners to options
                questionDiv.querySelectorAll('.option').forEach(option => {
                    option.addEventListener('click', function() {
                        // Remove any previous selections for this question
                        questionDiv.querySelectorAll('.option').forEach(opt => {
                            opt.classList.remove('selected');
                        });
                        
                        // Select this option
                        this.classList.add('selected');
                    });
                });
            });
        }

        function checkMultipleChoice() {
            let correctCount = 0;
            
            mcQuestions.forEach((q, index) => {
                const selectedOption = document.querySelector(`#mc-questions-container .question:nth-child(${index + 1}) .option.selected`);
                const feedback = document.getElementById(`mc-feedback-${index}`);
                
                if (selectedOption) {
                    if (selectedOption.dataset.value === q.answer) {
                        selectedOption.classList.add('correct');
                        feedback.textContent = '✅ Corretto!';
                        feedback.className = 'feedback correct';
                        correctCount++;
                    } else {
                        selectedOption.classList.add('incorrect');
                        feedback.textContent = `❌ Sbagliato. La risposta corretta è: "${q.answer}"`;
                        feedback.className = 'feedback incorrect';
                        
                        // Highlight correct answer
                        document.querySelectorAll(`#mc-questions-container .question:nth-child(${index + 1}) .option`).forEach(opt => {
                            if (opt.dataset.value === q.answer) {
                                opt.classList.add('correct');
                            }
                        });
                    }
                } else {
                    feedback.textContent = `❌ Nessuna risposta selezionata. La risposta corretta è: "${q.answer}"`;
                    feedback.className = 'feedback incorrect';
                    
                    // Highlight correct answer
                    document.querySelectorAll(`#mc-questions-container .question:nth-child(${index + 1}) .option`).forEach(opt => {
                        if (opt.dataset.value === q.answer) {
                            opt.classList.add('correct');
                        }
                    });
                }
                feedback.style.display = 'block';
            });
            
            // Update score
            score = correctCount;
            document.getElementById('score').textContent = score;
            
            // Show final score
            showFinalScore(correctCount, mcQuestions.length);
        }

        // Matching game functions
        function renderMatchingGame() {
            const leftColumn = document.getElementById('left-column');
            const rightColumn = document.getElementById('right-column');
            
            // Clear columns
            leftColumn.querySelectorAll('.match-item').forEach(item => item.remove());
            rightColumn.querySelectorAll('.match-item').forEach(item => item.remove());
            
            // Reset matched pairs
            matchedPairs = [];
            
            // Shuffle the pairs
            const shuffledPairs = shuffleArray([...matchingPairs]);
            
            // Create left column items (English)
            shuffledPairs.forEach((pair, index) => {
                const item = document.createElement('div');
                item.className = 'match-item';
                item.textContent = pair.english;
                item.dataset.index = index;
                item.addEventListener('click', () => selectMatchItem('left', index, item));
                leftColumn.appendChild(item);
            });
            
            // Create right column items (Italian - shuffled)
            const shuffledItalian = shuffleArray([...shuffledPairs]);
            shuffledItalian.forEach((pair, index) => {
                const item = document.createElement('div');
                item.className = 'match-item';
                item.textContent = pair.italian;
                item.dataset.index = shuffledPairs.findIndex(p => p.italian === pair.italian);
                item.addEventListener('click', () => selectMatchItem('right', item.dataset.index, item));
                rightColumn.appendChild(item);
            });
        }

        function selectMatchItem(side, index, element) {
            // If already matched, do nothing
            if (element.classList.contains('matched')) return;
            
            // If already selected, deselect
            if (selectedMatchItems[side] === index) {
                element.classList.remove('selected');
                selectedMatchItems[side] = null;
                return;
            }
            
            // Deselect any previously selected item on this side
            document.querySelectorAll(`#${side === 'left' ? 'left' : 'right'}-column .match-item`).forEach(item => {
                item.classList.remove('selected');
            });
            
            // Select this item
            element.classList.add('selected');
            selectedMatchItems[side] = index;
            
            // If both sides have a selection, check if they match
            if (selectedMatchItems.left !== null && selectedMatchItems.right !== null) {
                if (selectedMatchItems.left === selectedMatchItems.right) {
                    // Match found
                    document.querySelectorAll(`.match-item[data-index="${selectedMatchItems.left}"]`).forEach(item => {
                        item.classList.add('matched');
                        item.classList.remove('selected');
                    });
                    matchedPairs.push(selectedMatchItems.left);
                    score++;
                    document.getElementById('score').textContent = score;
                }
                
                // Reset selections after a short delay
                setTimeout(() => {
                    document.querySelectorAll('.match-item.selected').forEach(item => {
                        item.classList.remove('selected');
                    });
                    selectedMatchItems.left = null;
                    selectedMatchItems.right = null;
                }, 1000);
            }
        }

        function checkMatching() {
            if (matchedPairs.length === matchingPairs.length) {
                showFinalScore(score, matchingPairs.length, '🎉 Complimenti! Hai abbinato tutte le coppie correttamente!');
            } else {
                showFinalScore(score, matchingPairs.length, `Hai abbinato ${score} coppie su ${matchingPairs.length}. Continua a esercitarti!`);
            }
        }

        // Flashcard functions
        function renderFlashcard() {
            const flashcard = flashcards[currentFlashcardIndex];
            document.getElementById('flashcard-front-text').textContent = flashcard.front;
            document.getElementById('flashcard-back-text').textContent = flashcard.back;
            document.getElementById('current-flashcard').classList.remove('flipped');
        }

        function flipFlashcard() {
            document.getElementById('current-flashcard').classList.toggle('flipped');
        }

        function nextFlashcard() {
            currentFlashcardIndex = (currentFlashcardIndex + 1) % flashcards.length;
            renderFlashcard();
        }

        function prevFlashcard() {
            currentFlashcardIndex = (currentFlashcardIndex - 1 + flashcards.length) % flashcards.length;
            renderFlashcard();
        }

        // Utility function to show final score
        function showFinalScore(correct, total, customMessage = null) {
            const finalFeedback = document.createElement('div');
            finalFeedback.className = 'feedback ' + (correct === total ? 'correct' : 'incorrect');
            
            if (customMessage) {
                finalFeedback.textContent = customMessage;
            } else {
                finalFeedback.textContent = correct === total ? 
                    '🎉 Complimenti! Hai risposto correttamente a tutte le domande!' : 
                    `Hai totalizzato ${correct} punti su ${total}. Continua a esercitarti!`;
            }
            
            finalFeedback.style.marginTop = '20px';
            
            const checkBtn = document.querySelector('.check-btn');
            checkBtn.parentNode.insertBefore(finalFeedback, checkBtn.nextSibling);
            
            // Remove message after 5 seconds
            setTimeout(() => {
                finalFeedback.remove();
            }, 5000);
        }
    </script>
</body>
</html>
