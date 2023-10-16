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

  <button onclick="changeColor('lightblue')">Blue</button>
  <button onclick="changeColor('lightgreen')">Green</button>
  <button onclick="changeColor('lightcoral')">Red</button>

  <script>
    function changeColor(color) {
      document.body.style.backgroundColor = color;
    }
  </script>

</body>
</html>

