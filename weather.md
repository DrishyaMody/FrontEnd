---
layout: default
title: Student Blog
---

<html>
<head>
  <title>Change Background Color</title>
</head>
<body>

  <button id="blueButton" onclick="changeColor('lightblue')">Blue</button>
  <button id="greenButton" onclick="changeColor('lightgreen')">Green</button>
  <button id="redButton" onclick="changeColor('lightcoral')">Red</button>

  <script>
    function changeColor(color) {
      document.body.style.backgroundColor = color;
    }
  </script>

</body>
</html>



