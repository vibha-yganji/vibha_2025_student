<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cookie Clicker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
            position: relative;
        }

        #gameContainer {
            text-align: center;
            position: relative;
            z-index: 2; /* Ensures game content is above the falling cookies */
        }

        #ledSign {
            font-size: 60px;
            font-weight: bold;
            color: rgb(67, 153, 170);
            text-shadow: 0 0 5px rgb(67, 121, 138), 0 0 10px rgb(109, 164, 182), 0 0 15px rgb(45, 83, 129), 0 0 20px rgb(38, 90, 122), 0 0 25px rgb(85, 101, 132), 0 0 30px rgb(64, 131, 142), 0 0 35px rgb(36, 103, 109);
            margin-bottom: 20px;
            animation: flash 1s infinite;
        }

        @keyframes flash {
            0%, 100% {
                opacity: 1;
            }
            50% {
                opacity: 0.3;
            }
        }

        #cookie {
            width: 120px;
            height: 120px;
            background-color: transparent;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 60px;
            color: #fff;
            cursor: pointer;
            position: relative;
            z-index: 2;
            transition: transform 0.1s ease;
            margin: 0 auto;
        }

        #cookie:active {
            transform: scale(0.95);
        }

        #score {
            font-size: 32px;
            margin: 20px 0;
            z-index: 2;
        }

        #workerCount {
            font-size: 24px;
            color: #333;
            margin-top: 10px;
            z-index: 2;
        }

        #shopLink {
            font-size: 18px;
            color: #007BFF;
            cursor: pointer;
            margin-top: 20px;
            text-decoration: underline;
        }

        .falling-cookie {
            position: absolute;
            top: -150px; /* Start above the viewport */
            width: 50px;
            height: 50px;
            background-color: transparent;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 30px;
            color: #fff;
            pointer-events: none; /* Ensure cookies don't block interaction with game elements */
            animation: fall linear infinite;
        }

        @keyframes fall {
            0% {
                transform: translateY(-150px);
            }
            100% {
                transform: translateY(calc(100vh + 50px)); /* End below the viewport */
            }
        }
    </style>
</head>

<body>
    <div id="gameContainer">
        <div id="ledSign">COOKIE CLICKER</div>
        <div id="cookie">🍪</div>
        <div id="score">Score: 0</div>
        <div id="workerCount">Workers: 0</div>
        <div id="shopLink" onclick="window.location.href='shop.html'">Go to Shop</div>
    </div>

    <!-- Falling cookies -->
    <div class="falling-cookie" style="left: 10%; animation-duration: 6s;"></div>
    <div class="falling-cookie" style="left: 30%; animation-duration: 8s;"></div>
    <div class="falling-cookie" style="left: 50%; animation-duration: 7s;"></div>
    <div class="falling-cookie" style="left: 70%; animation-duration: 9s;"></div>
    <div class="falling-cookie" style="left: 90%; animation-duration: 5s;"></div>

    <audio id="clickSound" src="click.mp3"></audio>

    <script>
        let score = 0;
        let workers = 0;
        const workerCost = 50;

        const clickSound = document.getElementById('clickSound');

        document.getElementById('cookie').addEventListener('click', () => {
            score++;
            updateScore();
            clickSound.play();
        });

        function updateScore() {
            document.getElementById('score').innerText = `Score: ${score}`;
            document.getElementById('workerCount').innerText = `Workers: ${workers}`;
        }

        function addWorker() {
            if (score >= workerCost) {
                score -= workerCost;
                workers++;
                updateScore();
            }
        }

        setInterval(() => {
            score += workers;
            updateScore();
        }, 1000);

        // Example of how you might trigger adding a worker (e.g., from the shop page)
        // This would need to be triggered based on interaction with the shop page.
    </script>
</body>

