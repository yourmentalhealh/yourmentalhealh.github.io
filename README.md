

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>My Mental Health Checker</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: url('my mental health checker.jpg') no-repeat center top;
      background-size: cover;
      background-color: #2a2a2a;
      color: #fff;
      text-shadow: 1px 1px 4px rgba(0,0,0,0.7);
    }

    @media (max-width: 600px) {
      body {
        background: #2a2a2a;
      }
      header img {
        height: 60px;
      }
    }

    .overlay {
      background-color: rgba(0, 0, 0, 0.6);
      padding: 30px;
      min-height: 100vh;
    }

    header {
      text-align: center;
      margin-bottom: 30px;
    }

    header img {
      height: 100px;
      margin-bottom: 10px;
    }

    h1 {
      font-size: 2em;
      margin: 0;
    }

    form {
      max-width: 600px;
      margin: 0 auto;
      background-color: rgba(255, 255, 255, 0.1);
      padding: 20px;
      border-radius: 10px;
    }

    label {
      display: block;
      margin-top: 20px;
      font-weight: bold;
    }

    input[type="range"] {
      width: 100%;
    }

    .scale-labels {
      display: flex;
      justify-content: space-between;
      font-size: 0.9em;
      opacity: 0.9;
    }

    button {
      margin-top: 30px;
      padding: 10px 20px;
      background-color: #4CAF50;
      color: white;
      font-size: 16px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background-color: #45a049;
    }

    .screen {
      display: none;
    }

    .active {
      display: block;
    }

    .result-screen {
      text-align: center;
      padding-top: 50px;
    }
  </style>
</head>
<body>
  <div class="overlay">
    <!-- Welcome Screen -->
    <div id="welcome-screen" class="screen active">
      <header>
        <img src="download.png" alt="STI Logo" />
        <h1>Welcome to My Mental Health Checker</h1>
      </header>
      <p>This tool is intended to help you reflect on your mental well-being. Your responses are confidential and will not be stored.</p>
      <p>Click "Proceed" to start the self-assessment.</p>
      <button onclick="showScreen('assessment-screen')">Proceed</button>
    </div>

    <!-- Assessment Screen -->
    <div id="assessment-screen" class="screen">
      <header>
        <img src="download.png" alt="STI Logo" />
        <h1>My Mental Health Checker</h1>
      </header>
      <form onsubmit="calculateScore(event)">
        <p>Please rate the following from 1 (Lowest) to 5 (Highest):</p>

        <label>1. I feel optimistic about the future.</label>
        <input type="number" name="q1" min="1" max="5" required />

        <label>2. I feel relaxed most of the time.</label>
        <input type="number" name="q2" min="1" max="5" required />

        <label>3. I have been feeling close to other people.</label>
        <input type="number" name="q3" min="1" max="5" required />

        <label>4. I have energy to do the things I need to do.</label>
        <input type="number" name="q4" min="1" max="5" required />

        <label>5. I’ve been dealing well with problems.</label>
        <input type="number" name="q5" min="1" max="5" required />

        <label>6. I feel confident in myself.</label>
        <input type="number" name="q6" min="1" max="5" required />

        <label>7. I feel in control of my emotions.</label>
        <input type="number" name="q7" min="1" max="5" required />

        <button type="submit">Submit Assessment</button>
      </form>
    </div>

    <!-- Result Screen -->
    <div id="result-screen" class="screen result-screen">
      <header>
        <img src="download.png" alt="STI Logo" />
        <h1>Your Mental Health Assessment Result</h1>
      </header>
      <div id="result-text"></div>
    </div>
  </div>

  <script>
    function showScreen(id) {
      document.querySelectorAll('.screen').forEach(screen => {
        screen.classList.remove('active');
      });
      document.getElementById(id).classList.add('active');
    }

    function calculateScore(event) {
      event.preventDefault();
      const form = event.target;
      let total = 0;
      let max = 7 * 5;
      for (let i = 1; i <= 7; i++) {
        total += parseInt(form['q' + i].value);
      }
      let percent = (total / max) * 100;
      let message = '';
      if (percent >= 80) {
        message = 'You seem to be doing well mentally. Keep it up!';
      } else if (percent >= 50) {
        message = 'You might be experiencing some mental stress. Consider taking some self-care steps or talking to someone.';
      } else {
        message = 'You may be struggling. It is highly recommended to talk to a mental health professional.';
      }
      document.getElementById('result-text').innerHTML = `<h3>Your Score: ${total} / ${max}</h3><p>${message}</p>`;
      showScreen('result-screen');
    }
  </script>
</body>
</html>
