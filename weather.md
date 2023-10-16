---
layout: default
title: Student Blog
---

<!DOCTYPE html>
<html>
<head>
  <title>Change Background Color</title>
</head>
<body>

  <button id="blueButton">Blue</button>
  <button id="greenButton">Green</button>
  <button id="redButton">Red</button>

  <script>
    document.getElementById('blueButton').onclick = function() {
      document.body.style.backgroundColor = 'lightblue';
    };

    document.getElementById('greenButton').onclick = function() {
      document.body.style.backgroundColor = 'lightgreen';
    };

    document.getElementById('redButton').onclick = function() {
      document.body.style.backgroundColor = 'lightcoral';
    };
  </script>

</body>
</html>


