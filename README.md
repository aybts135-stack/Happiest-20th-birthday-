# Happiest 20th birthday
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday Sis!</title>
    <style>
        :root {
            --purple-bg: #4b0082;
            --text-gold: #ffd700;
        }

        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            background-color: var(--purple-bg);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            text-align: center;
        }

        /* Sparkling Background Canvas */
        #sparkleCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: radial-gradient(circle, #6a0dad, #2e0854);
        }

        .container {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            padding: 2rem;
            border-radius: 20px;
            border: 2px solid rgba(255, 255, 255, 0.2);
            z-index: 10;
            max-width: 90%;
        }

        h1 { font-size: 3rem; text-shadow: 2px 2px 10px rgba(0,0,0,0.5); }
        p { font-size: 1.5rem; }

        .btn-group { margin-top: 20px; }

        button {
            padding: 12px 25px;
            font-size: 1.2rem;
            margin: 10px;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.2s, background 0.3s;
            font-weight: bold;
        }

        .btn-yes { background: #ff4d6d; color: white; }
        .btn-no { background: #6c757d; color: white; }
        .btn-enjoy { background: #ffd700; color: #333; margin-top: 30px; }

        button:hover { transform: scale(1.1); }

        /* Floating Elements */
        .floating {
            position: absolute;
            bottom: -100px;
            animation: float Up 6s linear infinite;
            z-index: 1;
            pointer-events: none;
        }

        @keyframes floatUp {
            0% { transform: translateY(0) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-120vh) rotate(360deg); opacity: 0; }
        }

        .footer-note {
            margin-top: 40px;
            font-style: italic;
            font-weight: bold;
            color: #ffb3c1;
        }

        .hidden { display: none; }
    </style>
</head>
<body>

    <canvas id="sparkleCanvas"></canvas>

    <div id="page1" class="container">
        <h1>Siblings Forever????</h1>
        <div class="btn-group">
            <button class="btn-yes" onclick="showBirthday()">Yes!</button>
            <button class="btn-no" onclick="prettyPlease()">No</button>
        </div>
        <p id="prettyText" style="color: #ffb3c1; margin-top: 15px;"></p>
    </div>

    <div id="page2" class="container hidden">
        <h1 style="color: var(--text-gold);">Happiest 20th Birthday myyy darling sister! 💐💕</h1>
        
        <div id="enjoySection">
            <button class="btn-enjoy" onclick="enjoyResponse()">Are you enjoying this?</button>
        </div>
        
        <p id="meTooText" class="hidden" style="font-size: 2rem; color: #00f2ff;">me toooo sis🥳</p>

        <div class="footer-note">
            With immense love from Akash and Tiya 💖💐💕
        </div>
    </div>

    <script>
        // Sparkle Background Logic
        const canvas = document.getElementById('sparkleCanvas');
        const ctx = canvas.getContext('2d');
        let particles = [];

        function initCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }

        class Particle {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.size = Math.random() * 2 + 0.5;
                this.speedX = Math.random() * 1 - 0.5;
                this.speedY = Math.random() * 1 - 0.5;
                this.opacity = Math.random();
            }
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                if (this.opacity < 1) this.opacity += 0.01;
            }
            draw() {
                ctx.fillStyle = `rgba(255, 255, 255, ${this.opacity})`;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        function createParticles() {
            for (let i = 0; i < 100; i++) {
                particles.push(new Particle());
            }
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles.forEach(p => {
                p.update();
                p.draw();
            });
            requestAnimationFrame(animate);
        }

        // Floating Balloons, Hearts, Confetti
        function spawnFloating() {
            const types = ['🎈', '💖', '❤️', '✨', '🎊', '⭐'];
            const el = document.createElement('div');
            el.className = 'floating';
            el.innerHTML = types[Math.floor(Math.random() * types.length)];
            el.style.left = Math.random() * 100 + 'vw';
            el.style.fontSize = (Math.random() * 20 + 20) + 'px';
            el.style.animationDuration = (Math.random() * 3 + 4) + 's';
            document.body.appendChild(el);
            
            setTimeout(() => el.remove(), 6000);
        }

        setInterval(spawnFloating, 300);

        // Navigation Logic
        function prettyPlease() {
            document.getElementById('prettyText').innerText = "prweeeeety pls💖";
        }

        function showBirthday() {
            document.getElementById('page1').classList.add('hidden');
            document.getElementById('page2').classList.remove('hidden');
        }

        function enjoyResponse() {
            document.getElementById('enjoySection').classList.add('hidden');
            document.getElementById('meTooText').classList.remove('hidden');
        }

        window.addEventListener('resize', initCanvas);
        initCanvas();
        createParticles();
        animate();
    </script>
</body>
</html>
