
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hold the Button Challenge</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      background-color: #f0f0f0;
      user-select: none;
      -webkit-user-select: none;
      -moz-user-select: none;
      background-image: url('https://www.example.com/background.jpg'); /* Replace with a URL to your desired background image */
      background-size: cover;
      background-position: center;
      color: #333;
    }

    .container {
      background: rgba(255, 255, 255, 0.8);
      padding: 20px;
      border-radius: 10px;
      display: inline-block;
      margin-top: 50px;
    }

    button {
      padding: 15px 30px;
      font-size: 16px;
      cursor: pointer;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
      transition: background-color 0.3s ease, transform 0.1s;
    }

    button:hover {
      background-color: #45a049;
    }

    button:active {
      transform: scale(0.95);
    }

    .results {
      margin-top: 20px;
      font-size: 18px;
    }

    p {
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Hold the Button for 10 Seconds</h1>
    <button id="hold-button">Hold Me</button>
    <div class="results">
      <p>Last Attempt: <span id="last-attempt">None</span></p>
      <p>Closest Attempt: <span id="closest-attempt">None</span></p>
    </div>
    <p>By Ayman Ali</p>
  </div>
  <script>
    let lastAttempt = "None";
    let closestAttempt = 10.00; // Initialize closest attempt to the target time.
    const holdButton = document.getElementById("hold-button");
    const lastAttemptDisplay = document.getElementById("last-attempt");
    const closestAttemptDisplay = document.getElementById("closest-attempt");

    let timer;
    let startTime;

    holdButton.addEventListener("mousedown", () => {
      startTime = new Date().getTime();
      timer = setInterval(updateTime, 10);
    });

    holdButton.addEventListener("mouseup", () => {
      clearInterval(timer);
      const endTime = new Date().getTime();
      const holdTime = (endTime - startTime) / 1000;
      lastAttempt = holdTime.toFixed(2);
      if (closestAttempt === 10.00 || Math.abs(10 - holdTime) < Math.abs(10 - closestAttempt)) {
        closestAttempt = holdTime;
      }
      lastAttemptDisplay.textContent = `${lastAttempt} seconds`;
      closestAttemptDisplay.textContent = `${closestAttempt.toFixed(2)} seconds`;
    });

    function updateTime() {
      const currentTime = new Date().getTime();
      const elapsedTime = (currentTime - startTime) / 1000;
      if (elapsedTime >= 10) {
        clearInterval(timer);
      }
    }

    document.addEventListener("contextmenu", (event) => event.preventDefault());
    document.addEventListener("keydown", (event) => {
      if ((event.ctrlKey && event.key === "c") || (event.metaKey && event.key === "c")) {
        event.preventDefault();
      }
    });
  </script>
</body>
</html>
