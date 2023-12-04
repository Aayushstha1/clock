<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Watch</title>
  <style>
    /* Basic styling for demonstration purposes */
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      background-color: #3498db; /* Blue background color */
      color: white;
    }
    .watch-container {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    .watch {
      width: 200px;
      height: 200px;
      border-radius: 50%;
      background-color: #fff;
      position: relative;
      border: 10px solid #333;
    }
    .hour-hand {
      width: 2px;
      height: 50px;
      background-color: #333;
      position: absolute;
      top: 50%;
      left: 50%;
      transform-origin: bottom;
      transform: translate(-50%, -100%);
    }
    .minute-hand {
      width: 2px;
      height: 80px;
      background-color: #333;
      position: absolute;
      top: 50%;
      left: 50%;
      transform-origin: bottom;
      transform: translate(-50%, -100%);
    }
    .second-hand {
      width: 1px;
      height: 90px;
      background-color: red;
      position: absolute;
      top: 50%;
      left: 50%;
      transform-origin: bottom;
      transform: translate(-50%, -100%);
      z-index: 1;
    }
    .center {
      width: 10px;
      height: 10px;
      background-color: #333;
      border-radius: 50%;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    .digital-time {
      font-size: 24px;
      margin-top: 20px;
    }
  </style>
</head>
<body>

  <div class="watch-container">
    <div class="watch">
      <div class="hour-hand"></div>
      <div class="minute-hand"></div>
      <div class="second-hand"></div>
      <div class="center"></div>
    </div>
    <div class="digital-time" id="digitalTime">00:00:00 AM</div>
  </div>

  <script>
    function updateClock() {
      const hourHand = document.querySelector('.hour-hand');
      const minuteHand = document.querySelector('.minute-hand');
      const secondHand = document.querySelector('.second-hand');
      const digitalTime = document.getElementById('digitalTime');

      const now = new Date();
      let hours = now.getHours();
      const minutes = now.getMinutes();
      const seconds = now.getSeconds();

      const isPM = hours >= 12;

      hours = hours % 12 || 12; // Convert hours to 12-hour format

      const hourDeg = (hours * 30) + (0.5 * minutes); // Each hour mark is 30 degrees
      const minuteDeg = (minutes * 6) + (0.1 * seconds); // Each minute mark is 6 degrees
      const secondDeg = seconds * 6; // Each second mark is 6 degrees

      hourHand.style.transform = `translate(-50%, -100%) rotate(${hourDeg}deg)`;
      minuteHand.style.transform = `translate(-50%, -100%) rotate(${minuteDeg}deg)`;
      secondHand.style.transform = `translate(-50%, -100%) rotate(${secondDeg}deg)`;

      // Format digital time with AM/PM notation
      const formattedTime = `${formatTime(hours)}:${formatTime(minutes)}:${formatTime(seconds)} ${isPM ? 'PM' : 'AM'}`;
      digitalTime.textContent = formattedTime;
    }

    function formatTime(time) {
      return time < 10 ? `0${time}` : time;
    }

    // Update clock every second
    setInterval(updateClock, 1000);

    // Initial call to display time immediately
    updateClock();
  </script>
</body>
</html>
