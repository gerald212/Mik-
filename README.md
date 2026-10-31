
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Animated Heart</title>

    <style>
        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            background: #100817;
            color: white;
            font-family: Arial, sans-serif;
        }

        canvas {
            width: 90vw;
            max-width: 440px;
        }

        h1 {
            color: pink;
            text-shadow: 0 0 15px red;
        }

        p {
            color: #ffb6d5;
        }
    </style>
</head>

<body>

    <canvas id="heart" width="500" height="500"></canvas>

    <h1>Made with Love ❤️</h1>
    <p>A little heart animation</p>

    <script>
        const canvas = document.getElementById("heart");
        const ctx = canvas.getContext("2d");

        let pulse = 0;

        function drawHeart(scale) {

            ctx.beginPath();

            for (let i = 0; i <= 400; i++) {

                let t = (i / 400) * Math.PI * 2;

                let x = 16 * Math.pow(Math.sin(t), 3);

                let y = 13 * Math.cos(t)
                    - 5 * Math.cos(2 * t)
                    - 2 * Math.cos(3 * t)
                    - Math.cos(4 * t);

                let px = 250 + x * scale;
                let py = 245 - y * scale;

                if (i === 0) {
                    ctx.moveTo(px, py);
                } else {
                    ctx.lineTo(px, py);
                }
            }

            ctx.closePath();

            let gradient = ctx.createLinearGradient(
                130, 120, 370, 390
            );

            gradient.addColorStop(0, "#ff8ab5");
            gradient.addColorStop(0.5, "#ff174f");
            gradient.addColorStop(1, "#a90035");

            ctx.fillStyle = gradient;

            ctx.shadowColor = "red";
            ctx.shadowBlur = 30;

            ctx.fill();

            ctx.shadowBlur = 0;

            ctx.strokeStyle = "pink";
            ctx.lineWidth = 2;
            ctx.stroke();
        }

        function animate() {

            ctx.clearRect(
                0, 0,
                canvas.width,
                canvas.height
            );

            let scale = 10.5 + Math.sin(pulse) * 0.45;

            drawHeart(scale);

            pulse += 0.055;

            requestAnimationFrame(animate);
        }

        animate();
    </script>

</body>
</html>
