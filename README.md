
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
            color: #444;
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
        <section id="backstage">
            <h2>[BACKSTAGE]</h2>
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
                                <div class="desc">Linhas de baixo pesadas quebrando o misticismo do carimbo.</div>
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
        <p>Nels1Bank & Guidance Live Asset © 2026 // Desenvolvido na física pura sem carimbo burocrático.</p>
    </footer>

    <script>
        // ==========================================================
        // 1. BANCO DE DADOS DE ÁUDIO & CONTROLE DA ENGINE (AUDIO API)
        // ==========================================================
        const trackDatabase = {
            'The Front Line': {
                url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3', // Endereço dos arquivos .mp3
                desc: 'Abertura com distorção microfonada e bumbo duplo isolado.'
            },
            'Evening Tide': {
                url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3',
                desc: 'Linhas de baixo pesadas quebrando o misticismo do carimbo.'
            },
            'Falls Like Rain': {
                url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3',
                desc: 'Aceleração mecânica rasgando a maquete de segurança.'
            },
            'Life Amongst Strangers': {
                url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-4.mp3',
                desc: 'O hino soberano de quem assiste à legião de anestesiados da varanda.'
            },
            'The Downfall of the Birdwatcher': {
                url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-5.mp3',
                desc: 'O estouro da Singularidade do Bug em riffs jorgonescos implacáveis.'
            }
        };

        let audioContext;
        let analyser;
        let source;
        const audioPlayer = new Audio();
        audioPlayer.crossOrigin = "anonymous"; 
        let currentTrackName = "";

        function playTrack(trackName) {
            const track = trackDatabase[trackName];
            if (!track) return;

            // Ativa o pipeline de áudio nativo no primeiro input do usuário (Física do DOM)
            if (!audioContext) {
                audioContext = new (window.AudioContext || window.webkitAudioContext)();
                analyser = audioContext.createAnalyser();
                analyser.fftSize = 64; // Tamanho do buffer de frequência para tempo de resposta bruto
                source = audioContext.createMediaElementSource(audioPlayer);
                source.connect(analyser);
                analyser.connect(audioContext.destination);
            }

            if (audioContext.state === 'suspended') {
                audioContext.resume();
            }

            const clickedBtn = event.target;
            
            // Se clicar na mesma música que já está rodando: alterna Play/Pause
            if (currentTrackName === trackName) {
                if (audioPlayer.paused) {
                    audioPlayer.play();
                    clickedBtn.innerText = "STOP_";
                    clickedBtn.style.backgroundColor = "var(--accent-yellow)";
                    clickedBtn.style.color = "#000";
                } else {
                    audioPlayer.pause();
                    clickedBtn.innerText = "RUN_";
                    clickedBtn.style.backgroundColor = "transparent";
                    clickedBtn.style.color = "var(--accent-color)";
                }
            } else {
                // Reseta os estados visuais dos botões de controle das outras faixas
                document.querySelectorAll('.play-btn').forEach(btn => {
                    btn.innerText = "RUN_";
                    btn.style.backgroundColor = "transparent";
                    btn.style.color = "var(--accent-color)";
                });

                // Carrega e dispara a nova pedrada
                audioPlayer.src = track.url;
                audioPlayer.play()
                    .then(() => {
                        currentTrackName = trackName;
                        clickedBtn.innerText = "STOP_";
                        clickedBtn.style.backgroundColor = "var(--accent-color)";
                        clickedBtn.style.color = "#fff";
                        console.log("Tripalium Engine injetada: " + trackName);
                    })
                    .catch(err => console.log("Erro no barramento de áudio: ", err));
            }
        }

        // ==========================================================
        // 2. RENDERIZADOR GRÁFICO GRUNGE 3D & VISUALIZER (THREE.JS)
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

        // Array de buffer para capturar os decibéis em tempo real
        const dataArray = new Uint8Array(32);

        // Loop contínuo de animação - A física dos dados moldando a skin
        function animate() {
            requestAnimationFrame(animate);
            
            // Se a música estiver ativa, extrai a frequência e deforma a estrutura 3D
            if (analyser && !audioPlayer.paused) {
                analyser.getByteFrequencyData(dataArray);
                
                // Monitora as frequências de sub-grave (bumbos e linhas de baixo pesadas)
                let bassFrequency = dataArray[2] / 255; 
                
                // Modula a escala do objeto diretamente pela pressão dos graves
                meshIndustrial.scale.set(1 + bassFrequency, 1 + bassFrequency, 1 + bassFrequency);
                meshIndustrial.rotation.x += 0.01 + (bassFrequency * 0.04);
                meshIndustrial.rotation.y += 0.01 + (bassFrequency * 0.04);
                
                // Intensidade do estrobo acompanha a saturação dos agudos (guitarras)
                redLight.intensity = 2 + (dataArray[12] / 40);
            } else {
                // Rotação cadenciada de repouso (Estado de espera no refúgio)
                meshIndustrial.rotation.x += 0.003;
                meshIndustrial.rotation.y += 0.003;
                meshIndustrial.scale.set(1, 1, 1);
                redLight.intensity = 2;
            }

            renderer.render(scene, camera);
        }
        animate();

        // Listener responsivo para reajustar a tela e não bugar a proporção do canvas
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>
