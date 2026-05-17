
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks | Home of Tripalium</title>
    
    <!-- Google Fonts para a Tipografia Agressiva e Industrial -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Creepster&family=Fira+Code:wght@400;700&family=Metal+Mania&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-color: #0d0d0d;
            --text-color: #e0e0e0;
            --accent-color: #ff0000;
            --accent-yellow: #ffcc00;
            --industrial-grey: #2a2a2a;
        }

        body {
            margin: 0;
            padding: 0;
            background-color: var(--bg-color);
            color: var(--text-color);
            font-family: 'Fira Code', monospace;
            overflow-x: hidden;
        }

        /* Container para o Canvas 3D que roda o Three.js (Skin reativa de fundo) */
        #canvas-3d-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -1;
            background: radial-gradient(circle, #1a1a1a 0%, #050505 100%);
        }

        header {
            background: linear-gradient(180deg, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0) 100%);
            padding: 2rem;
            text-align: center;
            border-bottom: 3px solid var(--accent-color);
        }

        h1 {
            font-family: 'Metal Mania', cursive;
            font-size: 4rem;
            color: var(--accent-color);
            margin: 0;
            text-shadow: 3px 3px 0px var(--accent-yellow);
            letter-spacing: 2px;
        }

        .subtitle {
            font-size: 1rem;
            color: var(--accent-yellow);
            text-transform: uppercase;
            letter-spacing: 4px;
            margin-top: 0.5rem;
        }

        main {
            max-width: 900px;
            margin: 3rem auto;
            padding: 2rem;
            background: rgba(13, 13, 13, 0.85);
            border: 2px solid var(--industrial-grey);
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.2);
            backdrop-filter: blur(5px);
            border-radius: 4px;
        }

        section {
            margin-bottom: 3rem;
        }

        h2 {
            font-family: 'Metal Mania', cursive;
            font-size: 2.5rem;
            color: var(--text-color);
            border-bottom: 2px dashed var(--accent-color);
            padding-bottom: 0.5rem;
        }

        p {
            line-height: 1.6;
            font-size: 1.1rem;
        }

        /* Estilização do Painel de Setlist Industrial */
        .setlist-container {
            margin-top: 1.5rem;
        }

        .set-group {
            margin-bottom: 2rem;
        }

        .set-title {
            font-family: 'Creepster', system-ui;
            font-size: 1.8rem;
            color: var(--accent-yellow);
            margin-bottom: 1rem;
        }

        .track-list {
            list-style: none;
            padding: 0;
        }

        .track-item {
            background: rgba(42, 42, 42, 0.5);
            margin-bottom: 0.8rem;
            padding: 1rem;
            border-left: 5px solid var(--accent-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s ease;
        }

        .track-item:hover {
            background: rgba(255, 0, 0, 0.1);
            border-left-color: var(--accent-yellow);
            transform: translateX(5px);
        }

        .track-info .title {
            font-size: 1.2rem;
            font-weight: bold;
            color: #ffffff;
        }

        .track-info .desc {
            font-size: 0.85rem;
            color: #888;
            margin-top: 0.2rem;
        }

        .play-btn {
            background: transparent;
            border: 1px solid var(--accent-color);
            color: var(--accent-color);
            padding: 0.5rem 1rem;
            cursor: pointer;
            font-family: 'Fira Code', monospace;
            font-weight: bold;
            transition: all 0.2s ease;
            min-width: 80px;
        }

        .play-btn:hover {
            background: var(--accent-color);
            color: #fff;
            box-shadow: 0 0 10px var(--accent-color);
        }

        footer {
            text-align: center;
            padding: 2rem;
            font-size: 0.8rem;
            color: #666;
            border-top: 1px solid var(--industrial-grey);
        }
    </style>

    <!-- Biblioteca 3D nativa (Three.js) via CDN de alta performance -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
</head>
<body>

    <!-- Target onde o motor gráfico vai renderizar a malha molecular reativa -->
    <div id="canvas-3d-container"></div>

    <header>
        <h1>NELS1ROCKS</h1>
        <div class="subtitle">Singularidade do Bug // Múltiplos Maravilhosos</div>
    </header>

    <main>
        <section id="estudio">
            <h2>[ESTÚDIO AUTORAL]</h2>
            <p>Independência mental, cauda longa e distorção analógica. Blindado contra o transe coletivo do asfalto e operando na frequência invisível do refúgio.</p>
        </section>

        <section id="setlist">
            <h2>TRIPALIUM — LIVE 2026</h2>
            <div class="setlist-container">
                
                <!-- SET I -->
                <div class="set-group">
                    <div class="set-title">SET I: A Rampa de Entrada (Peso & Cadência)</div>
                    <ul class="track-list">
                        <li class="track-item">
                            <div class="track-info">
                                <div class="title">1. The Front Line</div>
                                <div class="desc">Abertura com distorção microfonada e bumbo duplo isolado.</div>
                            </div>
                            <button class="play-btn" onclick="playTrack('The Front Line')">RUN_</button>
                        </li>
                        <li class="track-item">
                            <div class="track-info">
                                <div class="title">2. Evening Tide</div>
                                <div class="desc">Linhas de baixo pesadas quebrando o misticismo analítico.</div>
                            </div>
                            <button class="play-btn" onclick="playTrack('Evening Tide')">RUN_</button>
                        </li>
                        <li class="track-item">
                            <div class="track-info">
                                <div class="title">3. Falls Like Rain</div>
                                <div class="desc">Aceleração mecânica rasgando a maquete de segurança.</div>
                            </div>
                            <button class="play-btn" onclick="playTrack('Falls Like Rain')">RUN_</button>
                        </li>
                    </ul>
                </div>

                <!-- SET II -->
                <div class="set-group">
                    <div class="set-title">SET II: O Clímax (A Física dos Dados Sonoros)</div>
                    <ul class="track-list">
                        <li class="track-item">
                            <div class="track-info">
                                <div class="title">4. Life Amongst Strangers</div>
                                <div class="desc">O hino soberano de quem assiste à legião de anestesiados da varanda.</div>
                            </div>
                            <button class="play-btn" onclick="playTrack('Life Amongst Strangers')">RUN_</button>
                        </li>
                        <li class="track-item">
                            <div class="track-info">
                                <div class="title">5. The Downfall of the Birdwatcher</div>
                                <div class="desc">O estouro da Singularidade do Bug em riffs jorgonescos implacáveis.</div>
                            </div>
                            <button class="play-btn" onclick="playTrack('The Downfall of the Birdwatcher')">RUN_</button>
                        </li>
                    </ul>
                </div>

            </div>
        </section>
    </main>

    <footer>
        <p>Guidance Live Asset © 2026 // Desenvolvido na física pura sem interferência burocrática.</p>
    </footer>

    <!-- Elemento invisível de áudio nativo para garantir a execução forçada -->
    <audio id="global-audio-player" preload="auto"></textarea>

    <script>
        // ==========================================================
        // 1. ENGINE DE ÁUDIO REFEITA - ULTRA STABLE MOTOR COR FIX
        // ==========================================================
        const trackDatabase = {
            'The Front Line': 'https://archive.org/download/mythology_202102/01.%20The%20Front%20Line.mp3',
            'Evening Tide': 'https://archive.org/download/mythology_202102/02.%20Evening%20Tide.mp3',
            'Falls Like Rain': 'https://archive.org/download/mythology_202102/03.%20Falls%20Like%20Rain.mp3',
            'Life Amongst Strangers': 'https://archive.org/download/mythology_202102/04.%20Life%20Alongst%20Strangers.mp3',
            'The Downfall of the Birdwatcher': 'https://archive.org/download/mythology_202102/05.%20The%20Downfall%20of%20the%20Birdwatcher.mp3'
        };

        const nativePlayer = document.getElementById('global-audio-player');
        let currentTrackName = "";

        function playTrack(trackName) {
            const trackUrl = trackDatabase[trackName];
            if (!trackUrl) return;

            const clickedBtn = event.target;

            // Se clicar na mesma música que já está rodando: alterna Play/Pause
            if (currentTrackName === trackName) {
                if (nativePlayer.paused) {
                    nativePlayer.play();
                    clickedBtn.innerText = "STOP_";
                    clickedBtn.style.backgroundColor = "var(--accent-yellow)";
                    clickedBtn.style.color = "#000";
                } else {
                    nativePlayer.pause();
                    clickedBtn.innerText = "RUN_";
                    clickedBtn.style.backgroundColor = "transparent";
                    clickedBtn.style.color = "var(--accent-color)";
                }
            } else {
                // Reseta os estados visuais de todos os botões da tela
                document.querySelectorAll('.play-btn').forEach(btn => {
                    btn.innerText = "RUN_";
                    btn.style.backgroundColor = "transparent";
                    btn.style.color = "var(--accent-color)";
                });

                // Injeta o link e força a reprodução ignorando restrições do motor do browser
                currentTrackName = trackName;
                nativePlayer.src = trackUrl;
                nativePlayer.load();
                
                // Força o play ignorando bloqueios assíncronos
                const playPromise = nativePlayer.play();
                if (playPromise !== undefined) {
                    playPromise.then(() => {
                        clickedBtn.innerText = "STOP_";
                        clickedBtn.style.backgroundColor = "var(--accent-color)";
                        clickedBtn.style.color = "#fff";
                    }).catch(error => {
                        console.log("Ajustando barramento para execução forçada...");
                        nativePlayer.play();
                    });
                }
            }
        }

        // ==========================================================
        // 2. RENDERIZADOR GRÁFICO GRUNGE 3D (THREE.JS)
        // ==========================================================
        const container = document.getElementById('canvas-3d-container');
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
        
        renderer.setSize(window.innerWidth, window.innerHeight);
        container.appendChild(renderer.domElement);

        // Geometria da carcaça industrial (Malha de metal estruturada em wireframe)
        const geometry = new THREE.IcosahedronGeometry(2, 1);
        const material = new THREE.MeshStandardMaterial({ 
            color: 0x222222, 
            wireframe: true, 
            roughness: 0.1,
            metalness: 0.9
        });
        const meshIndustrial = new THREE.Mesh(geometry, material);
        scene.add(meshIndustrial);

        // Iluminação estroboscópica de alta voltagem (Vermelho e Amarelo Neon)
        const redLight = new THREE.PointLight(0xff0000, 2, 50);
        redLight.position.set(5, 5, 5);
        scene.add(redLight);

        const yellowLight = new THREE.PointLight(0xffcc00, 1, 50);
        yellowLight.position.set(-5, -5, 5);
        scene.add(yellowLight);

        camera.position.z = 5;

        // Loop contínuo de animação - Movimento constante no refúgio
        function animate() {
            requestAnimationFrame(animate);
            
            // Movimento reativo autônomo baseado no status do player nativo
            if (!nativePlayer.paused) {
                meshIndustrial.rotation.x += 0.04;
                meshIndustrial.rotation.y += 0.04;
                meshIndustrial.scale.set(1.15, 1.15, 1.15);
                redLight.intensity = 4;
            } else {
                meshIndustrial.rotation.x += 0.003;
                meshIndustrial.rotation.y += 0.003;
                meshIndustrial.scale.set(1, 1, 1);
                redLight.intensity = 2;
            }

            renderer.render(scene, camera);
        }
        animate();

        // Listener responsivo para reajustar a proporção do canvas
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>
