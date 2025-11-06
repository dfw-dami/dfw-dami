<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Animated GitHub Stats</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #0D1117;
            color: #FFFFFF;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            padding: 40px 20px;
            overflow-x: hidden;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
            margin: 40px 0;
        }

        .stat-card {
            background: linear-gradient(135deg, #1a1f2e 0%, #0D1117 100%);
            border: 2px solid #00F7FF;
            border-radius: 20px;
            padding: 30px;
            position: relative;
            overflow: hidden;
            animation: slideIn 0.8s ease-out;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(
                45deg,
                transparent,
                rgba(0, 247, 255, 0.1),
                transparent
            );
            animation: shimmer 3s infinite;
        }

        @keyframes shimmer {
            0% {
                transform: translateX(-100%) translateY(-100%) rotate(45deg);
            }
            100% {
                transform: translateX(100%) translateY(100%) rotate(45deg);
            }
        }

        .stat-title {
            color: #00F7FF;
            font-size: 18px;
            font-weight: bold;
            margin-bottom: 20px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .stat-number {
            font-size: 48px;
            font-weight: bold;
            color: #00FF41;
            display: inline-block;
        }

        .stat-label {
            color: #888;
            font-size: 14px;
            margin-top: 10px;
        }

        /* Circle Progress */
        .circle-container {
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 40px 0;
        }

        .circle-wrap {
            position: relative;
            width: 200px;
            height: 200px;
        }

        .circle-bg {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            border: 8px solid #1a1f2e;
        }

        .circle-progress {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            border: 8px solid transparent;
            border-top-color: #00F7FF;
            border-right-color: #00F7FF;
            animation: circleRotate 2s ease-out forwards;
            transform: rotate(-90deg);
        }

        @keyframes circleRotate {
            from {
                transform: rotate(-90deg);
            }
            to {
                transform: rotate(270deg);
            }
        }

        .circle-inner {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
        }

        .circle-number {
            font-size: 48px;
            font-weight: bold;
            color: #00F7FF;
        }

        .circle-label {
            font-size: 14px;
            color: #888;
            margin-top: 5px;
        }

        /* Contribution Graph */
        .graph-container {
            margin: 40px 0;
            padding: 30px;
            background: linear-gradient(135deg, #1a1f2e 0%, #0D1117 100%);
            border: 2px solid #00F7FF;
            border-radius: 20px;
        }

        .graph-title {
            color: #00F7FF;
            font-size: 24px;
            font-weight: bold;
            margin-bottom: 20px;
            text-align: center;
        }

        .graph-bars {
            display: flex;
            align-items: flex-end;
            justify-content: space-around;
            height: 200px;
            gap: 5px;
        }

        .bar {
            flex: 1;
            background: linear-gradient(to top, #00FF41, #00F7FF);
            border-radius: 5px 5px 0 0;
            animation: barGrow 1s ease-out forwards;
            transform-origin: bottom;
            transform: scaleY(0);
            position: relative;
        }

        .bar::after {
            content: '';
            position: absolute;
            top: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 8px;
            height: 8px;
            background: #FF6D00;
            border-radius: 50%;
            box-shadow: 0 0 10px #FF6D00;
        }

        @keyframes barGrow {
            to {
                transform: scaleY(1);
            }
        }

        .bar:nth-child(1) { height: 20%; animation-delay: 0.1s; }
        .bar:nth-child(2) { height: 50%; animation-delay: 0.2s; }
        .bar:nth-child(3) { height: 80%; animation-delay: 0.3s; }
        .bar:nth-child(4) { height: 40%; animation-delay: 0.4s; }
        .bar:nth-child(5) { height: 90%; animation-delay: 0.5s; }
        .bar:nth-child(6) { height: 60%; animation-delay: 0.6s; }
        .bar:nth-child(7) { height: 100%; animation-delay: 0.7s; }
        .bar:nth-child(8) { height: 70%; animation-delay: 0.8s; }
        .bar:nth-child(9) { height: 85%; animation-delay: 0.9s; }
        .bar:nth-child(10) { height: 45%; animation-delay: 1s; }

        /* Trophy Animation */
        .trophies {
            display: flex;
            justify-content: center;
            gap: 30px;
            flex-wrap: wrap;
            margin: 40px 0;
        }

        .trophy {
            font-size: 60px;
            animation: float 3s ease-in-out infinite, fadeInScale 1s ease-out;
        }

        .trophy:nth-child(1) { animation-delay: 0s, 0.2s; }
        .trophy:nth-child(2) { animation-delay: 0.5s, 0.4s; }
        .trophy:nth-child(3) { animation-delay: 1s, 0.6s; }
        .trophy:nth-child(4) { animation-delay: 1.5s, 0.8s; }

        @keyframes float {
            0%, 100% {
                transform: translateY(0px);
            }
            50% {
                transform: translateY(-20px);
            }
        }

        @keyframes fadeInScale {
            from {
                opacity: 0;
                transform: scale(0);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        h1 {
            text-align: center;
            color: #00F7FF;
            font-size: 48px;
            margin-bottom: 20px;
            animation: glow 2s ease-in-out infinite;
        }

        @keyframes glow {
            0%, 100% {
                text-shadow: 0 0 10px #00F7FF, 0 0 20px #00F7FF;
            }
            50% {
                text-shadow: 0 0 20px #00F7FF, 0 0 40px #00F7FF, 0 0 60px #00F7FF;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>📊 GitHub Stats Animation Demo</h1>

        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-title">⭐ Total Stars</div>
                <div class="stat-number" data-target="29">0</div>
                <div class="stat-label">Stars Earned</div>
            </div>

            <div class="stat-card">
                <div class="stat-title">💻 Commits</div>
                <div class="stat-number" data-target="82">0</div>
                <div class="stat-label">This Year</div>
            </div>

            <div class="stat-card">
                <div class="stat-title">🔥 Contributions</div>
                <div class="stat-number" data-target="156">0</div>
                <div class="stat-label">Total</div>
            </div>
        </div>

        <div class="circle-container">
            <div class="circle-wrap">
                <div class="circle-bg"></div>
                <div class="circle-progress"></div>
                <div class="circle-inner">
                    <div class="circle-number" data-target="5">0</div>
                    <div class="circle-label">Day Streak</div>
                </div>
            </div>
        </div>

        <div class="graph-container">
            <div class="graph-title">📈 Contribution Graph</div>
            <div class="graph-bars">
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
            </div>
        </div>

        <div class="trophies">
            <div class="trophy">🏆</div>
            <div class="trophy">🥇</div>
            <div class="trophy">⭐</div>
            <div class="trophy">🎯</div>
        </div>
    </div>

    <script>
        // Counter Animation
        function animateCounter(element) {
            const target = parseInt(element.getAttribute('data-target'));
            const duration = 2000;
            const increment = target / (duration / 16);
            let current = 0;

            const timer = setInterval(() => {
                current += increment;
                if (current >= target) {
                    element.textContent = target;
                    clearInterval(timer);
                } else {
                    element.textContent = Math.floor(current);
                }
            }, 16);
        }

        // Start animations when page loads
        window.addEventListener('load', () => {
            const counters = document.querySelectorAll('.stat-number, .circle-number');
            counters.forEach(counter => {
                setTimeout(() => animateCounter(counter), 300);
            });
        });

        // Restart animation on click
        document.addEventListener('click', () => {
            location.reload();
        });
    </script>
</body>
</html>
