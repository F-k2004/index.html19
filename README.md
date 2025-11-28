<!DOCTYPE html>
<html lang="fa">
<head>
  <meta charset="UTF-8">
  <title>🌈 موج رنگی تعاملی</title>
  <eta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    body {
      margin: 0;
      overflow: hidden;
      background: #000;
    }

    canvas {
      display: block;
    }
  </style>
</head>

<body>

  <canvas id="wave"></canvas>

  <script>
    const canvas = document.getElementById("wave");
    const ctx = canvas.getContext("2d");

    let w, h;
    function resize() {
      w = canvas.width = window.innerWidth;
      h = canvas.height = window.innerHeight;
    }
    window.addEventListener("resize", resize);
    resize();

    let mouseX = 0;
    let t = 0;

    window.addEventListener("mousemove", (e) => {
      mouseX = e.clientX / w;  // مقدار 0 تا 1
    });

    function animate() {
      t += 0.03;

      ctx.clearRect(0, 0, w, h);

      for (let i = 0; i < 40; i++) {

        let color = `hsl(${(i * 10 + t * 20) % 360}, 90%, 60%)`;
        ctx.strokeStyle = color;
        ctx.lineWidth = 2 + Math.sin(t + i) * 1.2;

        ctx.beginPath();

        for (let x = 0; x < w; x += 10) {
          let y = h/2 
                + Math.sin((x * 0.01) + t + i * 0.2) * 60
                + Math.sin((x * 0.02) + t * 1.5 + i * 0.3) * 40 * mouseX;
          
          if (x === 0)
            ctx.moveTo(x, y);
          else
            ctx.lineTo(x, y);
        }

        ctx.stroke();
      }

      requestAnimationFrame(animate);
    }

    animate();
  </script>

</body>
</html>
