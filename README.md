# SanValent-n
Mi Persona Especial 😍
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Para Mi Persona Especial ✨💖</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Quicksand:wght@400;600&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --rosa-pastel: #ffdeeb;
            --rosa-medio: #ff8fab;
            --rosa-fuerte: #fb6f92;
            --blanco: #fff0f3;
            --celeste-cute: #bde0fe;
        }

        body {
            margin: 0;
            padding: 0;
            font-family: 'Quicksand', sans-serif;
            background-color: var(--rosa-pastel);
            color: var(--rosa-fuerte);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow: hidden;
        }

        /* Fondo de iconos flotantes mejorado */
        .floating-bg {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none; z-index: 0;
        }

        #app {
            width: 90%;
            max-width: 380px;
            height: 85vh;
            background: rgba(255, 255, 255, 0.94);
            position: relative;
            border-radius: 40px;
            box-shadow: 0 15px 40px rgba(251, 111, 146, 0.3);
            overflow-y: auto;
            text-align: center;
            padding: 25px;
            box-sizing: border-box;
            border: 4px solid white;
            z-index: 1;
        }

        .screen {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100%;
            animation: fadeIn 0.6s ease;
        }

        .hidden { display: none !important; }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Título Editado */
        h1 { 
            font-family: 'Dancing Script', cursive; 
            font-size: 2.5rem; 
            margin: 15px 0; 
            color: var(--rosa-fuerte);
            text-shadow: 1px 1px 2px rgba(0,0,0,0.05);
        }
        
        button {
            background: linear-gradient(45deg, var(--rosa-medio), var(--rosa-fuerte));
            color: white; border: none; padding: 14px 28px; border-radius: 30px;
            font-weight: bold; cursor: pointer; transition: 0.3s;
            box-shadow: 0 5px 15px rgba(251, 111, 146, 0.4);
            border: 2px solid white;
        }

        button:hover { transform: translateY(-3px) scale(1.02); }

        .grid-menu {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px; width: 100%;
        }

        .icon-card {
            background: white; padding: 20px; border-radius: 25px;
            border: 2px dashed var(--rosa-medio); cursor: pointer; transition: 0.3s;
        }

        .icon-card:hover { background: var(--blanco); transform: translateY(-5px); }
        .icon-card span { font-size: 2.5rem; }

        /* Ruleta */
        .wheel-container {
            position: relative;
            width: 260px; height: 260px;
            margin: 20px 0;
        }

        #wheel-canvas {
            width: 100%; height: 100%;
            border-radius: 50%;
            border: 6px solid white;
            box-shadow: 0 8px 20px rgba(0,0,0,0.1);
            transition: transform 4s cubic-bezier(0.15, 0, 0.15, 1);
        }

        .wheel-pointer {
            position: absolute; top: -10px; left: 50%;
            transform: translateX(-50%); font-size: 2.5rem; z-index: 10;
        }

        /* Frasco */
        .jar-container {
            width: 170px; height: 210px;
            border: 5px solid var(--rosa-medio);
            border-radius: 20px 20px 60px 60px;
            margin: 10px auto; background: rgba(255, 255, 255, 0.8);
            padding: 15px; display: flex; flex-wrap: wrap; justify-content: center; align-content: center;
        }

        .heart-btn { font-size: 1.6rem; cursor: pointer; transition: 0.3s; margin: 3px; }
        .heart-btn:hover { transform: scale(1.4) rotate(10deg); }

        .back-link { margin-top: 25px; color: var(--rosa-medio); cursor: pointer; font-weight: bold; text-decoration: underline; }
    </style>
</head>
<body>

    <div class="floating-bg" id="bg-elements"></div>

    <div id="app">
        <section id="welcome" class="screen">
            <div style="font-size: 4.5rem;">💌</div>
            <h1>Para mi persona especial</h1>
            <p>He preparado este espacio con mucho amor solo para ti.</p>
            <br>
            <button onclick="nav('menu')">ABRIR REGALO ✨</button>
        </section>

        <section id="menu" class="screen hidden">
            <h2>Elige una sorpresa 🎀</h2>
            <div class="grid-menu">
                <div class="icon-card" onclick="nav('wheel')">
                    <span>🎡</span><br><small>Número de Suerte</small>
                </div>
                <div class="icon-card" onclick="nav('reasons')">
                    <span>🏺</span><br><small>Frasco de Amor</small>
                </div>
                <div class="icon-card" onclick="nav('video')" style="grid-column: span 2;">
                    <span>🎥</span><br><small>Un video especial</small>
                </div>
            </div>
        </section>

        <section id="wheel" class="screen hidden">
            <h2>Gira la ruleta ✨</h2>
            <div class="wheel-container">
                <div class="wheel-pointer">🎀</div>
                <canvas id="wheel-canvas" width="300" height="300"></canvas>
            </div>
            <button id="spin-btn" onclick="spinWheel()">¡GIRAR! ⭐</button>
            <p id="wheel-msg" style="margin-top: 15px; font-weight: bold; font-size: 1.1rem; color: var(--rosa-fuerte);"></p>
            <div class="back-link" onclick="nav('menu')">Volver al menú</div>
        </section>

        <section id="reasons" class="screen hidden">
            <h2>10 razones por ti ✨</h2>
            <div class="jar-container" id="jar"></div>
            <p id="reason-display" style="min-height: 60px; padding: 15px; font-style: italic; font-size: 1rem;">Toca un icono del frasco...</p>
            <div class="back-link" onclick="nav('menu')">Volver al menú</div>
        </section>

        <section id="video" class="screen hidden">
            <h2>Eres mi sol ☀️</h2>
            <div style="border: 6px solid white; border-radius: 25px; overflow: hidden; width: 100%; box-shadow: 0 5px 15px rgba(0,0,0,0.1);">
                <iframe width="100%" height="250" src="https://youtu.be/WoHWH7xwOKY?si=DfrIiNU5aZqkGYPq" frameborder="0" allowfullscreen></iframe>
            </div>
            <div class="back-link" onclick="nav('menu')">Volver al menú</div>
        </section>
    </div>

    <script>
        function nav(id) {
            document.querySelectorAll('.screen').forEach(s => s.classList.add('hidden'));
            document.getElementById(id).classList.remove('hidden');
            if(id === 'wheel') drawWheel();
        }

        // Fondo con muchísimos iconos cute
        function createBg() {
            const bg = document.getElementById('bg-elements');
            const icons = ['❤️', '✨', '⭐', '💖', '🌸', '🎀', '🧸', '🦋', '🌷', '🍓', '🍭', '🌈'];
            for (let i = 0; i < 30; i++) {
                const span = document.createElement('span');
                span.innerText = icons[Math.floor(Math.random() * icons.length)];
                span.style.position = 'absolute';
                span.style.left = Math.random() * 100 + 'vw';
                span.style.top = Math.random() * 100 + 'vh';
                span.style.fontSize = Math.random() * 20 + 15 + 'px';
                span.style.opacity = '0.35';
                span.style.animation = `float ${Math.random() * 5 + 5}s infinite ease-in-out`;
                bg.appendChild(span);
            }
        }
        createBg();

        // Configuración de la Ruleta
        const premios = ["Cena Especial 🍝", "Vale por 100 Besos 💋", "Noche Romántica 😍", "Un Masaje Relajante 💆‍♂️", "Hacer lo que Quieras 💖"];
        const numOpciones = [1, 2, 3, 4, 5];
        const colors = ["#ffadad", "#ffd6a5", "#fdffb6", "#caffbf", "#9bf6ff"];
        let currentRotation = 0;

        function drawWheel() {
            const canvas = document.getElementById('wheel-canvas');
            const ctx = canvas.getContext('2d');
            const slice = (2 * Math.PI) / numOpciones.length;
            
            ctx.clearRect(0,0,300,300);
            for (let i = 0; i < numOpciones.length; i++) {
                ctx.beginPath();
                ctx.fillStyle = colors[i];
                ctx.moveTo(150, 150);
                ctx.arc(150, 150, 150, i * slice, (i + 1) * slice);
                ctx.fill();
                
                // Texto de números
                ctx.save();
                ctx.translate(150, 150);
                ctx.rotate(i * slice + slice/2);
                ctx.fillStyle = "white";
                ctx.font = "bold 35px Quicksand";
                ctx.shadowColor = "rgba(0,0,0,0.3)";
                ctx.shadowBlur = 4;
                ctx.fillText(numOpciones[i], 85, 12);
                ctx.restore();
            }
        }

        function spinWheel() {
            const wheel = document.getElementById('wheel-canvas');
            const msg = document.getElementById('wheel-msg');
            const btn = document.getElementById('spin-btn');
            
            btn.disabled = true;
            msg.innerText = "¡Girando con magia! ✨";
            
            const extraDegrees = Math.floor(Math.random() * 360) + 2160; // Mínimo 6 vueltas
            currentRotation += extraDegrees;
            wheel.style.transform = `rotate(${currentRotation}deg)`;
            
            setTimeout(() => {
                const actualDeg = currentRotation % 360;
                // Ajuste para detectar el número que queda bajo el marcador (arriba)
                const index = (numOpciones.length - 1 - Math.floor(actualDeg / (360 / numOpciones.length))) % numOpciones.length;
                msg.innerHTML = `🌟 Ganaste el número ${numOpciones[index]}: <br> <strong>${premios[index]}</strong>`;
                btn.disabled = false;
            }, 4000);
        }

        // Frasco con iconos variados
        const razones = ["Tu Paciencia.💖", "Siempre Estás Cuando te Necesito.✨", "Cómo Me Haces Reír Cada Día.🎀", "Tus Locuras que Amo.🌸", "La Forma en La que Me Miras.⭐", "Eres Mi Persona Favorita.🧸", "Me Haces Ser Mejor.🍓", "Tu Apoyo Cuando no Estoy al 100%.🦋", "Simplemente por Ser Tú.🍭", "El Mundo es Mejor Contigo.💓"];
        const jar = document.getElementById('jar');
        const jarIcons = ['💖', '✨', '🎀', '🌸', '⭐', '🧸', '🍓', '🦋', '🍭', '💓'];
        razones.forEach((r, i) => {
            const span = document.createElement('span');
            span.className = 'heart-btn';
            span.innerHTML = jarIcons[i];
            span.onclick = () => {
                document.getElementById('reason-display').innerHTML = `<strong>Razón ${i+1}:</strong> ${r}`;
            };
            jar.appendChild(span);
        });
    </script>

    <style>
        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-25px) rotate(15deg); }
        }
    </style>
</body>
</html>
