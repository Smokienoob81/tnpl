<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For My Love</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #ffe6e6;
            text-align: center;
            padding: 50px;
            overflow: hidden;
        }
        .message-container {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            max-width: 500px;
            margin: auto;
            display: none;
            position: relative;
            z-index: 10;
        }
        h1 {
            color: #e60073;
        }
        p {
            font-size: 18px;
            color: #333;
        }
        .heart {
            font-size: 50px;
            color: #e60073;
            animation: heartbeat 1s infinite alternate;
        }
        @keyframes heartbeat {
            from { transform: scale(1); }
            to { transform: scale(1.1); }
        }
        canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }
    </style>
</head>
<body>
    <script>
        function showMessage() {
            let response = confirm("Can I have your 5 minutes?");
            if (response) {
                document.getElementById("message").style.display = "block";
                startConfetti(); // Trigger continuous confetti
            } else {
                document.body.innerHTML = "<h2>Alright, another time then! 😊</h2>";
            }
        }
    </script>

    <div class="message-container" id="message">
        <h1>For My Love ❤️</h1>
        <p>Every day with you is a celebration Diksha, but today, I just want to remind you how incredibly special you are.  
        You are the most beautiful part of my life, and I’m beyond lucky to have you by my side.</p>
        <p>Your kindness, your laughter, your dreams—they make my world brighter. No matter where life takes us, know that my heart is always with you.</p>
        <p>You are loved, cherished, and appreciated more than words can ever express.</p>
        <p>Today, tomorrow, and always—I am yours. Happy Valentine’s Day, my love. 💖</p>
        <div class="heart">❤️</div>
    </div>

    <canvas id="confettiCanvas"></canvas>

    <script>
        function startConfetti() {
            const canvas = document.getElementById("confettiCanvas");
            const ctx = canvas.getContext("2d");
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;

            const confettiParticles = [];
            const colors = ["#ff0a54", "#ff477e", "#ff85a1", "#ffb3c1", "#ffccd5", "#fff0f3"];

            function ConfettiPiece() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.size = Math.random() * 8 + 2;
                this.speedY = Math.random() * 3 + 2;
                this.color = colors[Math.floor(Math.random() * colors.length)];
            }

            ConfettiPiece.prototype.update = function () {
                this.y += this.speedY;
                if (this.y > canvas.height) {
                    this.y = -10;
                    this.x = Math.random() * canvas.width;
                }
            };

            ConfettiPiece.prototype.draw = function () {
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            };

            function initConfetti() {
                for (let i = 0; i < 100; i++) {
                    confettiParticles.push(new ConfettiPiece());
                }
            }

            function animateConfetti() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                confettiParticles.forEach(particle => {
                    particle.update();
                    particle.draw();
                });
                requestAnimationFrame(animateConfetti);
            }

            initConfetti();
            animateConfetti();
        }

        showMessage(); 
    </script>
</body>
</html>
