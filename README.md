# Quiz App

This is a simple web-based Quiz Application that includes user login functionality. The application is built using HTML, CSS, and JavaScript.

## Features

- User login validation
- Timed quiz questions
- Score tracking
- Display of final score

## Folder Structure

To run this project, you need a web browser that supports HTML5, CSS, and JavaScript.

### Installation

1. Clone the repository to your local machine using the following command:
    ```bash
    git clone https:https://github.com/Aasrithakavya123/online-quiz-app-using-html-css-javascript/tree/main
    ```

2. Navigate to the project directory:
    ```bash
    cd quiz-app
    ```

### Usage

1. Open the `index.html` file in your preferred web browser.

2. You will see a login screen. Enter a valid username and password to access the quiz. For the purpose of this demo, any non-empty username and password will grant access.

3. After successful login, the quiz will start. Answer the questions within the given time.

4. Your final score will be displayed at the end of the quiz.

### File Overview

#### index.html

This file contains the structure of the web application, including the login form and the quiz container.

#### style.css

This file contains the styles for the web application to make it visually appealing.

#### script.js

This file contains the JavaScript code for user login validation, quiz functionality, and score tracking.

### Example Code

#### HTML (index.html)
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="style.css">
  <title>Quiz App</title>
</head>
<body>
  <div id="login-container" class="container">
    <h2>Login</h2>
    <form id="loginForm">
      <label for="username">Username:</label>
      <input type="text" id="username" name="username" required>
      <label for="password">Password:</label>
      <input type="password" id="password" name="password" required>
      <button type="button" onclick="validateLogin()">Login</button>
    </form>
    <p id="error-message"></p>
  </div>
  <div id="quiz-container" class="container hidden">
    <div id="final-score" class="hidden">
      <h2>Final Score</h2>
      <p id="score-message"></p>
    </div>
    <h2>Quiz Time!</h2>
    <p id="timer"></p>
    <p id="question"></p>
    <div id="options"></div>
    <p id="result-message"></p>
  </div>
  <script src="script.js"></script>
</body>
</html>
JavaScript (script.js)
javascript
Copy code
var currentUser;
var currentQuestionIndex = 0;
var score = 0;
var timer;
var timeLimit = 20; // Set the time limit for each question in seconds

var questions = [
  {
    question: "Which of the following is considered an element of cybersecurity?",
    options: ["Network Security", "Operational Security", "Application Security", "All of the above"],
    correctAnswer: "All of the above"
  },
  {
    question: "Which planet is known as the Red Planet?",
    options: ["Venus", "Mars", "Jupiter", "Saturn"],
    correctAnswer: "Mars"
  },
  {
    question: "What is the largest mammal?",
    options: ["Elephant", "Blue Whale", "Giraffe", "Hippopotamus"],
    correctAnswer: "Blue Whale"
  },
  {
    question: "Who wrote 'Romeo and Juliet'?",
    options: ["Charles Dickens", "William Shakespeare", "Jane Austen", "Mark Twain"],
    correctAnswer: "William Shakespeare"
  },
  {
    question: "What is the currency of Japan?",
    options: ["Yuan", "Won", "Yen", "Ringgit"],
    correctAnswer: "Yen"
  }
];

function validateLogin() {
  var username = document.getElementById('username').value;
  var password = document.getElementById('password').value;
  var errorMessage = document.getElementById('error-message');

  currentUser = username;
  errorMessage.textContent = '';
  showQuiz();
  startTimer();
  showNextQuestion();
}

function showQuiz() {
  document.getElementById('login-container').classList.add('hidden');
  document.getElementById('quiz-container').classList.remove('hidden');
}

function startTimer() {
  var timerElement = document.getElementById('timer');
  var timeRemaining = timeLimit;

  timer = setInterval(function () {
    timerElement.textContent = 'Time Remaining: ' + timeRemaining + 's';

    if (timeRemaining <= 0) {
      clearInterval(timer);
      timerElement.textContent = 'Time\'s up!';
      showNextQuestion();
    }

    timeRemaining--;
  }, 1000);
}

function showNextQuestion() {
  if (currentQuestionIndex < questions.length) {
    var questionElement = document.getElementById('question');
    var optionsElement = document.getElementById('options');
    var resultMessageElement = document.getElementById('result-message');

    questionElement.textContent = questions[currentQuestionIndex].question;

    optionsElement.innerHTML = '';

    questions[currentQuestionIndex].options.forEach(function (option) {
      var optionButton = document.createElement('button');
      optionButton.textContent = option;
      optionButton.onclick = function () {
        selectAnswer(option);
      };
      optionsElement.appendChild(optionButton);
    });

    resultMessageElement.textContent = '';
  } else {
    showResult();
  }
}

function selectAnswer(selectedOption) {
  var correctAnswer = questions[currentQuestionIndex].correctAnswer;
  var resultMessageElement = document.getElementById('result-message');
  clearInterval(timer);

  if (selectedOption === correctAnswer) {
    score++;
  }

  currentQuestionIndex++;
  resultMessageElement.textContent = 'Your answer is ' + (selectedOption === correctAnswer ? 'correct!' : 'incorrect.');
  resultMessageElement.style.color = selectedOption === correctAnswer ? 'green' : 'red';

  setTimeout(function () {
    showNextQuestion();
    startTimer();
  }, 1000);
}

function showResult() {
  var resultMessageElement = document.getElementById('result-message');
  resultMessageElement.textContent = 'Quiz completed, ' + currentUser + '! Your score is ' + score + ' out of ' + questions.length + '.';
  resultMessageElement.style.color = 'black';
}
CSS (style.css)
css
Copy code
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: purple;
}

.container {
  background-color: violet;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 0 15px palevioletred;
  max-width: 400px;
  width: 100%;
  box-sizing: border-box;
  transition: box-shadow 0.3s ease;
}

.container:hover {
  box-shadow: 0 0 20px palevioletred;
}

.hidden {
  display: none;
}

h2 {
  color: #333;
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 8px;
  color: #48044f;
}

input {
  width: 100%;
  padding: 12px;
  margin-bottom: 16px;
  box-sizing: border-box;
  border: 1px solid rgb(228, 167, 228);
  border-radius: 5px;
  transition: border-color 0.3s ease;
}

input:focus {
  border-color: #7b0c55;
}

button {
  background-color: rgb(97, 15, 97);
  color: rgb(241, 227, 237);
  padding: 12px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 15px;
  width: 100%;
  box-sizing: border-box;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #45a049;
}

#error-message {
  color: #f2edf0;
  margin-top: 15px;
}

#result-message {
  color: red;
  margin-top: 15px;
}

#timer {
  margin-bottom: 15px;
  color: #555;
}

#quiz-container {
  text-align: center;
}

#question {
  margin-bottom: 20px;
  color: #333;
}

#options button {
  display: block;
  width: 100%;
  padding: 12





Is this conversation helpful so far?






