# PRODIGY_WD_Task2

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Stopwatch App</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #1e3c72, #2a5298);
      color: white;
      text-align: center;
      padding: 40px;
    }

    h1 {
      margin-bottom: 30px;
      font-size: 3em;
    }

    #display {
      font-size: 3em;
      margin: 20px auto;
      padding: 20px;
      border: 3px solid white;
      border-radius: 10px;
      width: 300px;
      background: rgba(255,255,255,0.1);
    }

    .buttons {
      margin: 20px;
    }

    button {
      padding: 10px 20px;
      font-size: 1.1em;
      margin: 0 10px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background 0.3s ease;
    }

    #startStop {
      background-color: #4CAF50;
      color: white;
    }

    #reset {
      background-color: #f44336;
      color: white;
    }

    #lap {
      background-color: #2196F3;
      color: white;
    }

    button:hover {
      opacity: 0.9;
    }

    ul {
      list-style: none;
      padding: 0;
    }

    li {
      background: rgba(255, 255, 255, 0.1);
      margin: 5px auto;
      padding: 8px 12px;
      width: 200px;
      border-radius: 6px;
    }
  </style>
</head>
<body>
  <h1>Stopwatch</h1>
  <div id="display">00:00:00</div>
  <div class="buttons">
    <button id="startStop">Start</button>
    <button id="lap">Lap</button>
    <button id="reset">Reset</button>
  </div>
  <h2>Laps</h2>
  <ul id="laps"></ul>

  <script>
    let startTime = 0;
    let elapsed = 0;
    let timerInterval;
    let isRunning = false;

    const display = document.getElementById('display');
    const startStopBtn = document.getElementById('startStop');
    const lapBtn = document.getElementById('lap');
    const resetBtn = document.getElementById('reset');
    const lapsList = document.getElementById('laps');

    function formatTime(ms) {
      let totalSeconds = Math.floor(ms / 1000);
      let minutes = String(Math.floor(totalSeconds / 60)).padStart(2, '0');
      let seconds = String(totalSeconds % 60).padStart(2, '0');
      let centiseconds = String(Math.floor((ms % 1000) / 10)).padStart(2, '0');
      return `${minutes}:${seconds}:${centiseconds}`;
    }

    function updateDisplay() {
      display.textContent = formatTime(elapsed);
    }

    startStopBtn.addEventListener('click', () => {
      if (!isRunning) {
        startTime = Date.now() - elapsed;
        timerInterval = setInterval(() => {
          elapsed = Date.now() - startTime;
          updateDisplay();
        }, 10);
        startStopBtn.textContent = 'Pause';
        isRunning = true;
      } else {
        clearInterval(timerInterval);
        startStopBtn.textContent = 'Start';
        isRunning = false;
      }
    });

    resetBtn.addEventListener('click', () => {
      clearInterval(timerInterval);
      elapsed = 0;
      updateDisplay();
      lapsList.innerHTML = '';
      startStopBtn.textContent = 'Start';
      isRunning = false;
    });

    lapBtn.addEventListener('click', () => {
      if (isRunning) {
        const li = document.createElement('li');
        li.textContent = formatTime(elapsed);
        lapsList.appendChild(li);
      }
    });
  </script>
</body>
</html>
