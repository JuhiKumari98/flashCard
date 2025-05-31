# flashCard
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Flashcard Quiz App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f4f8;
      margin: 0;
      padding: 20px;
    }

    h1 {
      text-align: center;
      color: #333;
    }

    .container {
      max-width: 600px;
      margin: auto;
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }

    input, button, textarea {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      font-size: 16px;
      border-radius: 8px;
      border: 1px solid #ccc;
    }

    button {
      background-color: #007bff;
      color: white;
      cursor: pointer;
      border: none;
    }

    button:hover {
      background-color: #0056b3;
    }

    .flashcard {
      margin-top: 20px;
    }

    .quiz-section {
      display: none;
    }

    .score {
      font-size: 20px;
      font-weight: bold;
      text-align: center;
      color: green;
    }
  </style>
</head>
<body>

  <h1>Flashcard Quiz App</h1>
  <div class="container">
    <div class="add-section">
      <h2>Add Flashcard</h2>
      <input id="question" type="text" placeholder="Enter question" />
      <input id="answer" type="text" placeholder="Enter answer" />
      <button onclick="addFlashcard()">Add Flashcard</button>
    </div>

    <hr>

    <div class="quiz-section" id="quizSection">
      <h2>Quiz Time</h2>
      <div class="flashcard" id="quizCard"></div>
      <input id="userAnswer" type="text" placeholder="Your answer" />
      <button onclick="submitAnswer()">Submit Answer</button>
    </div>

    <div class="score" id="scoreDisplay"></div>

    <button onclick="startQuiz()">Start Quiz</button>
  </div>

  <script>
    const flashcards = [];
    let currentCard = 0;
    let score = 0;

    function addFlashcard() {
      const question = document.getElementById('question').value.trim();
      const answer = document.getElementById('answer').value.trim();
      if (question && answer) {
        flashcards.push({ question, answer });
        alert("Flashcard added!");
        document.getElementById('question').value = '';
        document.getElementById('answer').value = '';
      } else {
        alert("Please enter both question and answer.");
      }
    }

    function startQuiz() {
      if (flashcards.length === 0) {
        alert("Add at least one flashcard to start quiz.");
        return;
      }
      score = 0;
      currentCard = 0;
      document.getElementById('scoreDisplay').innerText = '';
      document.getElementById('quizSection').style.display = 'block';
      showQuestion();
    }

    function showQuestion() {
      const card = flashcards[currentCard];
      document.getElementById('quizCard').innerText = card.question;
      document.getElementById('userAnswer').value = '';
    }

    function submitAnswer() {
      const userAns = document.getElementById('userAnswer').value.trim().toLowerCase();
      const correctAns = flashcards[currentCard].answer.trim().toLowerCase();
      if (userAns === correctAns) {
        score++;
        alert("Correct!");
      } else {
        alert(`Wrong! Correct answer was: ${flashcards[currentCard].answer}`);
      }

      currentCard++;
      if (currentCard < flashcards.length) {
        showQuestion();
      } else {
        document.getElementById('quizSection').style.display = 'none';
        document.getElementById('scoreDisplay').innerText =
          `Quiz Completed! Your Score: ${score} / ${flashcards.length}`;
      }
    }
  </script>
</body>
</html>
