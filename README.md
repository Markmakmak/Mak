# <!DOCTYPE html>
<html>
<head>
    <title>Simple Text-based Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
        }
    </style>
</head>
<body>
    <h1>Welcome to the Game</h1>
    <p>Click the button to play!</p>
    <button onclick="startGame()">Start Game</button>
    <p id="gameText"></p>

    <script>
        var questions = [
            {
                question: "What's my favorite color?",
                answer: "black",
                hint: "It's a dark shade.",
            },
            {
                question: "Where do I live?",
                answer: "St. Joseph Homes 1",
                hint: "It's a specific residential area.",
            },
            {
                question: "What course am I taking?",
                answer: "BSIT",
                hint: "It's related to information technology.",
            },
            {
                question: "How old am I?",
                answer: "21",
                hint: "I'm legally an adult.",
            },
            {
                question: "What's the biggest flex you can tell me?",
                answer: "", // The answer to this question depends on the player's response
                hint: "Think of something impressive to say.",
            }
        ];

        var currentQuestion = 0;
        var score = 0;
        var flexAnswer = "";
        var resultAnswers = [];

        function startGame() {
            var playerName = prompt("Enter your name:");
            if (playerName !== null) {
                document.getElementById("gameText").innerHTML = "Hello, " + playerName + "! You've started the game.";
                askQuestion();
            }
        }

        function askQuestion() {
            var playerAnswer = prompt(questions[currentQuestion].question);
            if (playerAnswer !== null) {
                if (playerAnswer.toLowerCase() === questions[currentQuestion].answer.toLowerCase()) {
                    document.getElementById("gameText").innerHTML = "Correct!";
                    score++;
                } else {
                    if (currentQuestion !== 4) {
                        document.getElementById("gameText").innerHTML = "Incorrect! The correct answer is: " + questions[currentQuestion].answer + ". Hint: " + questions[currentQuestion].hint;
                        resultAnswers.push(questions[currentQuestion].answer);
                    } else {
                        flexAnswer = playerAnswer;
                    }
                }
                currentQuestion++;
                if (currentQuestion < questions.length) {
                    askQuestion();
                } else {
                    endGame();
                }
            } else {
                endGame();
            }
        }

        function endGame() {
            var finalText = "Game Over! Your final score is " + score + " out of " + questions.length + "<br>";
            document.getElementById("gameText").innerHTML = finalText;

            if (score !== 5) {
                var answersText = "Your answers: " + resultAnswers.join(", ") + "<br>";
                var lastAnswerText = "Your answer for the last question: " + flexAnswer;
                document.getElementById("gameText").innerHTML += answersText + lastAnswerText;
            }
        }
    </script>
</body>
</html>
