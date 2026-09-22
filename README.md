<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Radio Heavy Metal & Underground</title>
    <!-- Google Fonts para Tipografia Industrial/Metal -->
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
            --moss-blue: #008080;        
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

        /* Container da Skin 3D Heavy Metal */
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
            border-radius: 0px; 
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

        /* Painel Central do Transmissor */
        .live-player-panel {
            background: #140824; 
            border: var(--cartoon-border);
            padding: 2rem;
            text-align: center;
            margin-top: 2rem;
            position: relative;
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

        /* Display Digital de 8 Segmentos */
        .segment-display-8 {
            font-family: 'Fira Code', monospace;
            font-size: 1.6rem;
            font-weight: bold;
            color: #221435; 
            background: #000000;
            padding: 0.2rem 0.7rem;
            border: 2px solid #000000;
            box-shadow: inset 0px 0px 8px rgba(0,0,0,0.8);
            min-width: 20px;
            display: inline-block;
            line-height: 1;
            letter-spacing: 0;
            transition: all 0.1s ease;
        }

        .segment-display-8.active-bit {
            color: var(--white-pure);
            text-shadow: 0px 0px 10px rgba(255, 255, 255, 0.8), 0px 0px 20px rgba(255, 255, 255, 0.5);
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

        .main-play-btn:active {
            transform: translate(2px, 2px);
            box-shadow: 2px 2px 0px #000;
        }

        /* Grid de Frequências / Estações Atualizadas */
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
            font-weight: normal;
            text-shadow: 1px 1px 0px #000;
            text-transform: uppercase;
            letter-spacing: 1px;
            text-align: right;
            max-width: 250px;
            word-wrap: break-word;
        }

        .s-sin { color: #ffcc00; } 
        .s-to { color: #bf55ec; }  
        .s-ni { color: #ffffff; }  
        .s-za { color: #00bfff; }  
        .s-do { color: #ff4500; }  

        /* Container Adsense Customizado (Bitcoin) */
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

        .btc-ad-text {
            flex-grow: 1;
        }

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
            white-space: nowrap;
        }

        .btc-ad-btn:hover {
            background: var(--white-pure);
            transform: translate(-1px, -1px);
            box-shadow: 4px 4px 0px #000;
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

    <!-- Container do Fundo 3D -->
    <div id="canvas-3d-container"></div>

    <header>
        <h1>Underground Metal & Punk</h1>
        <div class="subtitle">Transmissão Extrema em Frequência Modulada</div>
    </header>

    <main>
        <section>
            <h2>Sobre o Sistema</h2>
            <p>Plataforma de transmissão voltada ao som cru e pesado. Selecione abaixo sua frequência favorita entre as vertentes do <strong>Black Metal, Death Metal, Thrash Metal e Old School Punk</strong> e sintonize no caos absoluto.</p>
        </section>

        <!-- Painel Central de Controle / Transmissor -->
        <div class="live-player-panel">
            <div class="stream-status">
                <span>FREQUÊNCIA ATIVA:</span>
                <div id="freq-display" class="segment-display-8 active-bit">106.6 FM</div>
            </div>
            <div class="master-controls">
                <button id="master-play-btn" class="main-play-btn">▶ Iniciar Transmissão</button>
            </div>
        </div>

        <!-- Seção de Escolha de Frequências (Atualizada com Metal e Punk) -->
        <section style="margin-top: 2.5rem;">
            <h2>Frequências Extremas</h2>
            <div class="station-grid">
                
                <!-- Estação 1: Black Metal -->
                <div class="station-card active-station" data-freq="66.6 FM" data-genre="Black Metal" data-track="Mayhem - Freezing Moon">
                    <div class="station-info">
                        <div class="station-title">66.6 FM - Frost & Abyss</div>
                        <div class="station-genre">Black Metal</div>
                    </div>
                    <div class="select-panel">
                        <div class="select-indicator s-sin">SINTONIZADO</div>
                        <div class="now-playing-meta">Mayhem - Freezing Moon</div>
                    </div>
                </div>

                <!-- Estação 2: Death Metal -->
                <div class="station-card" data-freq="91.3 FM" data-genre="Death Metal" data-track="Death - Crystal Mountain">
                    <div class="station-info">
                        <div class="station-title">91.3 FM - Rotten Vault</div>
                        <div class="station-genre">Death Metal</div>
                    </div>
                    <div class="select-panel">
                        <div class="select-indicator s-to" style="display:none;">SELECIONAR</div>
                        <div class="now-playing-meta">Death - Crystal Mountain</div>
                    </div>
                </div>

                <!-- Estação 3: Thrash Metal -->
                <div class="station-card" data-freq="103.5 FM" data-genre="Thrash Metal" data-track="Slayer - Angel of Death">
                    <div class="station-info">
                        <div class="station-title">103.5 FM - Atomic Mosh</div>
                        <div class="station-genre">Thrash Metal</div>
                    </div>
                    <div class="select-panel">
                        <div class="select-indicator s-ni" style="display:none;">SELECIONAR</div>
                        <div class="now-playing-meta">Slayer - Angel of Death</div>
                    </div>
                </div>

                <!-- Estação 4: Old School Punk -->
                <div class="station-card" data-freq="99.9 FM" data-genre="Old School Punk" data-track="The Exploited - Punks Not Dead">
                    <div class="station-info">
                        <div class="station-title">99.9 FM - Anarchy Riot</div>
                        <div class="station-genre">Old School Punk</div>
                    </div>
                    <div class="select-panel">
                        <div class="select-indicator s-za" style="display:none;">SELECIONAR</div>
                        <div class="now-playing-meta">The Exploited - Punks Not Dead</div>
                    </div>
                </div>

            </div>
        </section>
    </main>

    <!-- Bloco de Anúncio Customizado Bitcoin -->
    <div class="adsense-btc-container">
        <div class="adsense-label">Patrocínio Cripto</div>
        <div class="adsense-content">
            <div class="btc-ticker-art">₿</div>
            <div class="btc-ad-text">
                <h4 class="btc-ad-title">Proteja sua Soberania Financeira</h4>
                <p class="btc-ad-desc">Acumule Satoshi enquanto o sistema tradicional desaba. A liberdade descentralizada não negocia taxas.</p>
            </div>
            <button class="btc-ad-btn">Acumular ₿</button>
        </div>
    </div>

    <footer>
        <p>&copy; 2026 Rádio Underground Heavy Metal. Todos os direitos reservados ao caos sonoro.</p>
    </footer>

    <!-- Motor Gráfico 3D (Three.js) + Correções de Lógica -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script>
        // --- 1. CONFIGURAÇÃO DO THREE.JS (Fundo 3D Otimizado) ---
        const container = document.getElementById('canvas-3d-container');
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
        
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
        container.appendChild(renderer.domElement);

        // Geometria de Partículas Metálicas Flutuantes
        const particlesGeometry = new THREE.BufferGeometry();
        const particlesCount = 700;
        const posArray = new Float32Array(particlesCount * 3);

        for(let i = 0; i < particlesCount * 3; i++) {
            posArray[i] = (Math.random() - 0.5) * 15;
        }

        particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));

        const particlesMaterial = new THREE.PointsMaterial({
            size: 0.025,
            color: 0x8a2be2,
            transparent: true,
            opacity: 0.8
        });

        const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
        scene.add(particlesMesh);

        camera.position.z = 4;

        // Loop de Animação 3D
        function animate3D() {
            requestAnimationFrame(animate3D);
            particlesMesh.rotation.y += 0.001;
            particlesMesh.rotation.x += 0.0005;
            renderer.render(scene, camera);
        }
        animate3D();

        // Redimensionamento de Tela
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });


        // --- 2. LÓGICA DE INTERAÇÃO DA RÁDIO (CORREÇÃO DE BUGS) ---
        const stationCards = document.querySelectorAll('.station-card');
        const freqDisplay = document.getElementById('freq-display');
        const masterPlayBtn = document.getElementById('master-play-btn');
        let isPlaying = false;

        stationCards.forEach(card => {
            card.addEventListener('click', () => {
                // Remove estado ativo de todos
                stationCards.forEach(c => {
                    c.classList.remove('active-station');
                    c.querySelector('.select-panel').style.display = 'none';
                });

                // Adiciona estado ativo ao selecionado
                card.classList.add('active-station');
                const selectPanel = card.querySelector('.select-panel');
                selectPanel.style.display = 'flex';

                // Atualiza dados na tela principal
                const targetFreq = card.getAttribute('data-freq');
                freqDisplay.textContent = targetFreq;
            });
        });

        // Alternador do Botão Principal de Transmissão
        masterPlayBtn.addEventListener('click', () => {
            isPlaying = !isPlaying;
            if(isPlaying) {
                masterPlayBtn.textContent = '⏹ Parar Transmissão';
                masterPlayBtn.style.background = '#39ff14';
                masterPlayBtn.style.color = '#000';
            } else {
                masterPlayBtn.textContent = '▶ Iniciar Transmissão';
                masterPlayBtn.style.background = 'var(--purple-neon)';
                masterPlayBtn.style.color = 'var(--white-pure)';
            }
        });
    </script>
</body>
</html>
