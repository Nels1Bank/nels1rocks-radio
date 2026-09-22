
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Radio Heavy Metal & Underground</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;700&family=Metal+Mania&display=swap" rel="stylesheet">

    <style>
        :root {
            --bg-dark: #07030a;         
            --purple-neon: #8a2be2;      
            --moss-green: #1a0f2e;       
            --green-neon: #39ff14;       
            --white-pure: #ffffff;       
            --accent-yellow: #ffcc00;    
            --panel-bg: rgba(10, 5, 20, 0.93);
            --cartoon-border: 4px solid #000000; 
        }

        body {
            margin: 0;
            padding: 0;
            background-color: var(--bg-dark);
            color: var(--white-pure);
            font-family: 'Fira Code', monospace;
            overflow-x: hidden;
        }

        #canvas-3d-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -1;
            background: radial-gradient(circle, #1a0826 0%, #030105 100%);
        }

        header {
            background: #0f051c;
            padding: 2.5rem 2rem;
            text-align: center;
            border-bottom: 6px solid #000000; 
            box-shadow: 0 6px 0 #1f0b3a;
        }

        h1 {
            font-family: 'Metal Mania', cursive;
            font-size: 4.5rem;
            color: var(--white-pure);
            margin: 0;
            text-shadow: 4px 4px 0px #000000, 8px 8px 0px var(--purple-neon);
            letter-spacing: 3px;
        }

        .subtitle {
            font-size: 0.95rem;
            color: var(--purple-neon);
            text-transform: uppercase;
            letter-spacing: 5px;
            margin-top: 0.7rem;
            font-weight: bold;
            text-shadow: 2px 2px 0px #000;
        }

        main {
            max-width: 850px;
            margin: 3rem auto;
            padding: 2.5rem;
            background: var(--panel-bg);
            border: var(--cartoon-border);
            box-shadow: 8px 8px 0px #000000; 
        }

        section {
            margin-bottom: 2.5rem;
        }

        h2 {
            font-family: 'Metal Mania', cursive;
            font-size: 2.3rem;
            color: var(--white-pure);
            border-bottom: 4px solid #000000;
            padding-bottom: 0.5rem;
            text-transform: uppercase;
            text-shadow: 2px 2px 0px var(--purple-neon);
        }

        p {
            line-height: 1.7;
            font-size: 1.1rem;
            color: #dcd6e8;
            background: rgba(0,0,0,0.5);
            padding: 1rem;
            border-left: 4px solid var(--purple-neon);
        }

        .live-player-panel {
            background: #140824; 
            border: var(--cartoon-border);
            padding: 2rem;
            text-align: center;
            margin-top: 2rem;
            box-shadow: 5px 5px 0px #000000;
        }

        .stream-status {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            font-weight: bold;
            font-size: 1.2rem;
            margin-bottom: 1.5rem;
            color: var(--white-pure);
            text-shadow: 2px 2px 0px #000;
        }

        .segment-display-8 {
            font-family: 'Fira Code', monospace;
            font-size: 1.6rem;
            font-weight: bold;
            color: var(--white-pure);
            background: #000000;
            padding: 0.2rem 0.7rem;
            border: 2px solid #000000;
            box-shadow: inset 0px 0px 8px rgba(0,0,0,0.8);
            text-shadow: 0px 0px 10px rgba(255, 255, 255, 0.8);
        }

        .master-controls {
            margin-top: 1rem;
        }

        .main-play-btn {
            background: var(--purple-neon);
            border: var(--cartoon-border);
            color: var(--white-pure);
            font-family: 'Fira Code', monospace;
            font-size: 1.4rem;
            font-weight: bold;
            padding: 1rem 3rem;
            cursor: pointer;
            box-shadow: 4px 4px 0px #000;
            transition: transform 0.1s ease, box-shadow 0.1s ease;
            text-transform: uppercase;
            border-radius: 50px; 
        }

        .main-play-btn:hover {
            background: var(--white-pure);
            color: #000;
            transform: translate(-2px, -2px);
            box-shadow: 6px 6px 0px #000;
        }

        .station-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 1.2rem;
            margin-top: 1.5rem;
        }

        .station-card {
            background: #0e051a;
            border: var(--cartoon-border);
            box-shadow: 4px 4px 0px #000;
            padding: 1.2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            cursor: pointer;
            transition: background 0.2s;
        }

        .station-card:hover {
            background: #190a2e;
            transform: translate(-2px, -2px);
            box-shadow: 6px 6px 0px #000;
        }

        .station-card.active-station {
            background: #25123e;
            border-color: var(--purple-neon);
            box-shadow: 5px 5px 0px var(--purple-neon);
        }

        .station-info .station-title {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--white-pure);
            text-shadow: 1px 1px 0px #000;
        }

        .station-info .station-genre {
            font-size: 0.85rem;
            color: #a59cb5;
            margin-top: 0.3rem;
            text-transform: uppercase;
            font-weight: bold;
        }

        .select-panel {
            display: flex;
            flex-direction: column;
            align-items: flex-end;
            gap: 4px;
        }

        .select-indicator {
            font-size: 1rem;
            font-weight: bold;
            text-shadow: 2px 2px 0px #000;
        }

        .now-playing-meta {
            font-size: 0.8rem;
            color: var(--white-pure);
            text-transform: uppercase;
            text-align: right;
            max-width: 250px;
        }

        .s-sin { color: #ffcc00; } 

        .adsense-btc-container {
            max-width: 850px;
            margin: 0 auto 3rem auto;
            padding: 1rem;
            background: #130a1d;
            border: var(--cartoon-border);
            box-shadow: 6px 6px 0px #000;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 15px;
            box-sizing: border-box;
        }

        .adsense-label {
            font-size: 0.65rem;
            color: #6a5a80;
            text-transform: uppercase;
            letter-spacing: 2px;
            writing-mode: vertical-rl;
            transform: rotate(180deg);
            border-left: 2px solid #331a4a;
            padding-left: 4px;
        }

        .adsense-content {
            display: flex;
            align-items: center;
            gap: 20px;
            width: 100%;
        }

        .btc-ticker-art {
            font-size: 2.2rem;
            font-weight: bold;
            color: var(--accent-yellow);
            text-shadow: 3px 3px 0px #000;
            background: #000;
            padding: 0.4rem 1rem;
            border: 2px dashed var(--accent-yellow);
        }

        .btc-ad-text { flex-grow: 1; }

        .btc-ad-title {
            font-size: 1.1rem;
            font-weight: bold;
            color: var(--white-pure);
            margin: 0 0 0.2rem 0;
            text-transform: uppercase;
        }

        .btc-ad-desc {
            font-size: 0.8rem;
            color: #a59cb5;
            margin: 0;
        }

        .btc-ad-btn {
            background: #ff9900;
            color: #000;
            border: 3px solid #000;
            font-family: 'Fira Code', monospace;
            font-weight: bold;
            font-size: 0.9rem;
            padding: 0.6rem 1.2rem;
            cursor: pointer;
            box-shadow: 3px 3px 0px #000;
            text-transform: uppercase;
        }

        footer {
            text-align: center;
            padding: 2.5rem;
            font-size: 0.85rem;
            color: #6a5a80;
            border-top: 6px solid #000000;
            background: #06030b;
        }
    </style>
</head>
<body>

    <div id="canvas-3d-container"></div>

    <header>
        <h1>Underground Metal & Punk</h1>
        <div class="subtitle">Transmissão Extrema em Frequência Modulada</div>
    </header>

    <main>
        <section>
            <h2>Sobre o Sistema</h2>
            <p>Plataforma com streams reais integradas de <strong>Black Metal, Death Metal, Thrash Metal e Old School Punk</strong>. Selecione sua estação e aperte o play para o som ecoar.</p>
        </section>

        <div class="live-player-panel">
            <div class="stream-status">
                <span>FREQUÊNCIA ATIVA:</span>
                <div id="freq-display" class="segment-display-8">66.6 FM</div>
            </div>
            <div class="master-controls">
                <button id="master-play-btn" class="main-play-btn">▶ Iniciar Transmissão</button>
            </div>
        </div>

        <section style="margin-top: 2.5rem;">
            <h2>Frequências Extremas</h2>
            <div class="station-grid">
                
                <!-- Estação 1: Metal Geral / Extremo (Stream Real de WebRadio) -->
                <div class="station-card active-station" data-freq="66.6 FM" data-genre="Heavy & Extreme Metal" data-stream="https://rautemusik-de-hz-fal-stream05.radiohost.de/metal">
                    <div class="station-info">
                        <div class="station-title">66.6 FM - Frost & Abyss</div>
                        <div class="station-genre">Black / Heavy Metal</div>
                    </div>
                    <div class="select-panel">
                        <div class="select-indicator s-sin">SINTONIZADO</div>
                        <div class="now-playing-meta">RauteMusik Metal Stream</div>
                    </div>
                </div>

                <!-- Estação 2: Hard Rock & Heavy -->
                <div class="station-card" data-freq="91.3 FM" data-genre="Hard & Heavy" data-stream="https://stream.melodicarock.com/stream">
                    <div class="station-info">
                        <div class="station-title">91.3 FM - Rotten Vault</div>
                        <div class="station-genre">Death / Melodic Heavy</div>
                    </div>
                    <div class="select-panel" style="display:none;">
                        <div class="select-indicator s-sin">SELECIONAR</div>
                        <div class="now-playing-meta">Melodic Rock Stream</div>
                    </div>
                </div>

                <!-- Estação 3: Rock Clássico / Thrash Vibe -->
                <div class="station-card" data-freq="103.5 FM" data-genre="Classic Metal" data-stream="https://live.classicrockonthe.net/stream">
                    <div class="station-info">
                        <div class="station-title">103.5 FM - Atomic Mosh</div>
                        <div class="station-genre">Thrash / Classic Heavy</div>
                    </div>
                    <div class="select-panel" style="display:none;">
                        <div class="select-indicator s-sin">SELECIONAR</div>
                        <div class="now-playing-meta">Classic Rock Stream</div>
                    </div>
                </div>

                <!-- Estação 4: Punk & Hardcore -->
                <div class="station-card" data-freq="99.9 FM" data-genre="Punk & Riot" data-stream="https://punk.stream.laut.fm/punk">
                    <div class="station-info">
                        <div class="station-title">99.9 FM - Anarchy Riot</div>
                        <div class="station-genre">Old School Punk</div>
                    </div>
                    <div class="select-panel" style="display:none;">
                        <div class="select-indicator s-sin">SELECIONAR</div>
                        <div class="now-playing-meta">Laut.fm Punk Stream</div>
                    </div>
                </div>

            </div>
        </section>
    </main>

    <div class="adsense-btc-container">
        <div class="adsense-label">Patrocínio Cripto</div>
        <div class="adsense-content">
            <div class="btc-ticker-art">₿</div>
            <div class="btc-ad-text">
                <h4 class="btc-ad-title">Proteja sua Soberania Financeira</h4>
                <p class="btc-ad-desc">Acumule Satoshi enquanto o sistema tradicional desaba.</p>
            </div>
            <button class="btc-ad-btn">Acumular ₿</button>
        </div>
    </div>

    <footer>
        <p>&copy; 2026 Rádio Underground Heavy Metal. Transmissão ativa e sem censura.</p>
    </footer>

    <!-- Elemento de Áudio HTML5 Oculto -->
    <audio id="radio-audio" preload="none"></audio>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script>
        // Fundo 3D
        const container = document.getElementById('canvas-3d-container');
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        container.appendChild(renderer.domElement);

        const particlesGeometry = new THREE.BufferGeometry();
        const posArray = new Float32Array(700 * 3);
        for(let i = 0; i < 700 * 3; i++) posArray[i] = (Math.random() - 0.5) * 15;
        particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
        const particlesMesh = new THREE.Points(particlesGeometry, new THREE.PointsMaterial({ size: 0.025, color: 0x8a2be2, transparent: true, opacity: 0.8 }));
        scene.add(particlesMesh);
        camera.position.z = 4;

        function animate3D() {
            requestAnimationFrame(animate3D);
            particlesMesh.rotation.y += 0.001;
            renderer.render(scene, camera);
        }
        animate3D();

        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });

        // Lógica de Áudio Real da Rádio
        const audioEl = document.getElementById('radio-audio');
        const stationCards = document.querySelectorAll('.station-card');
        const freqDisplay = document.getElementById('freq-display');
        const masterPlayBtn = document.getElementById('master-play-btn');
        
        let currentStreamUrl = stationCards[0].getAttribute('data-stream');
        let isPlaying = false;

        stationCards.forEach(card => {
            card.addEventListener('click', () => {
                stationCards.forEach(c => {
                    c.classList.remove('active-station');
                    c.querySelector('.select-panel').style.display = 'none';
                });

                card.classList.add('active-station');
                card.querySelector('.select-panel').style.display = 'flex';

                freqDisplay.textContent = card.getAttribute('data-freq');
                currentStreamUrl = card.getAttribute('data-stream');

                if (isPlaying) {
                    audioEl.src = currentStreamUrl;
                    audioEl.play().catch(e => console.log("Erro ao carregar stream:", e));
                }
            });
        });

        masterPlayBtn.addEventListener('click', () => {
            isPlaying = !isPlaying;
            if(isPlaying) {
                masterPlayBtn.textContent = '⏹ Parar Transmissão';
                masterPlayBtn.style.background = '#39ff14';
                masterPlayBtn.style.color = '#000';
                audioEl.src = currentStreamUrl;
                audioEl.play().catch(err => {
                    alert("O navegador bloqueou o autoplay direto. Clique novamente ou interaja com a página!");
                    isPlaying = false;
                    masterPlayBtn.textContent = '▶ Iniciar Transmissão';
                    masterPlayBtn.style.background = 'var(--purple-neon)';
                    masterPlayBtn.style.color = 'var(--white-pure)';
                });
            } else {
                masterPlayBtn.textContent = '▶ Iniciar Transmissão';
                masterPlayBtn.style.background = 'var(--purple-neon)';
                masterPlayBtn.style.color = 'var(--white-pure)';
                audioEl.pause();
                audioEl.src = '';
            }
        });
    </script>
</body>
</html>
