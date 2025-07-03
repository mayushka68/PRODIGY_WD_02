# PRODIGY_WD_02
Working model of task 2 of internship  at prodigy InfoTech of stopwatch using css, html and javascript.
 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #1B1B3A;
            color: #fff;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .stopwatch {
            text-align: center;
            background-color: #333;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
        }
        .time {
            font-size: 3rem;
            margin-bottom: 20px;
        }
        .buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
        }
        .btn {
            padding: 10px 20px;
            font-size: 1rem;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .btn:hover {
            background-color: #45a049;
        }
        .btn:disabled {
            background-color: #ccc;
            cursor: not-allowed;
        }
    </style>
</head>
<body>

<div class="stopwatch">
    <div class="time" id="timeDisplay">00:00:00:00</div>
    <div class="buttons">
        <button class="btn" id="startStopBtn">Start</button>
        <button class="btn" id="resetBtn" disabled>Reset</button>
    </div>
</div>

<script>
    const startStopBtn = document.getElementById("startStopBtn");
    const resetBtn = document.getElementById("resetBtn");
    const timeDisplay = document.getElementById("timeDisplay");

    let timer;
    let isRunning = false;
    let startTime;
    let elapsedTime = 0;

    function formatTime(ms) {
        const date = new Date(ms);
        const hours = String(date.getUTCHours()).padStart(2, '0');
        const minutes = String(date.getUTCMinutes()).padStart(2, '0');
        const seconds = String(date.getUTCSeconds()).padStart(2, '0');
        const milliseconds = String(date.getUTCMilliseconds()).padStart(3, '0').slice(0, 2);
        return `${hours}:${minutes}:${seconds}:${milliseconds}`;
    }

    function updateTime() {
        elapsedTime = Date.now() - startTime;
        timeDisplay.textContent = formatTime(elapsedTime);
    }

    startStopBtn.addEventListener("click", () => {
        if (isRunning) {
            clearInterval(timer);
            startStopBtn.textContent = "Start";
            resetBtn.disabled = false;
        } else {
            startTime = Date.now() - elapsedTime;
            timer = setInterval(updateTime, 10);
            startStopBtn.textContent = "Stop";
            resetBtn.disabled = false;
        }
        isRunning = !isRunning;
    });

    resetBtn.addEventListener("click", () => {
        clearInterval(timer);
        isRunning = false;
        elapsedTime = 0;
        timeDisplay.textContent = "00:00:00:00";
        startStopBtn.textContent = "Start";
        resetBtn.disabled = true;
    });
</script>

</body>
</html>




