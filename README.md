
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
            --bg-color: #0a140d; /* Verde Musgo Escuro Principal */
            --bg-gradient-end: #030704; /* Tom Musgo Profundo para o gradiente */
            --text-color: #e0e0e0;
            --accent-color: #ff0000;
            --accent-yellow: #ffcc00;
            --industrial-grey: #1f2e24; /* Bordas adaptadas ao tom musgo */
        }

        body {
            margin: 0;
            padding: 0;
            background-color: var(--bg-color);
            color: var(--text-color);
            font-family: 'Fira Code', monospace;
            overflow-x: hidden;
        }

        /* Container para o Canvas 3D que roda o Three.js (Skin reativa com fundo Verde Musgo) */
        #canvas-3d-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -1;
            background: radial-gradient(circle, var(--bg-color) 0%, var(--bg-gradient-end) 100%);
        }

        header {
            background: linear-gradient(180deg, rgba(3,7,4,0.9) 0%, rgba(3,7,4,0) 100%);
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
            background: rgba(5, 12, 8, 0.85); /* Fundo dos blocos translúcido em musgo */
            border: 2px solid var(--industrial-grey);
            box-shadow: 0 0 20px rgba(255, 0, 0, 0.15);
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
            background: rgba(31, 46, 36, 0.4);
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
            color: #aaa;
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
            color: #555;
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
        <section id="manifesto">
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
                            <button class="play-btn" onclick="playTrack('The Front Line', event)">RUN_</button>
                        </li>
                        <li class="track-item">
                            <div class="track-info">
                                <div class="title">2. Evening Tide</div>
                                <div class="desc">Linhas de baixo pesadas quebrando o misticismo do carimbo.</div>
                            </div>
                            <button class="play-btn" onclick="playTrack('Evening Tide', event)">RUN_</button>
                        </li>
                        <li class="track-item">
                            <div class="track-info">
                                <div class="title">3. Falls Like Rain</div>
                                <div class="desc">Aceleração mecânica rasgando a maquete de segurança.</div>
                            </div>
                            <button class="play-btn" onclick="playTrack('Falls Like Rain', event)">RUN_</button>
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
                            <button class="play-btn" onclick="playTrack('Life Amongst Strangers', event)">RUN_</button>
                        </li>
                        <li class="track-item">
                            <div class="track-info">
                                <div class="title">5. The Downfall of the Birdwatcher</div>
                                <div class="desc">O estouro da Singularidade do Bug em riffs jorgonescos implacáveis.</div>
                            </div>
                            <button class="play-btn" onclick="playTrack('The Downfall of the Birdwatcher', event)">RUN_</button>
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
        
        // Configurações de buffer otimizadas contra engasgos
        audioPlayer.crossOrigin = "anonymous"; 
        audioPlayer.preload = "auto";
        
        let currentTrackName = "";

        function playTrack(trackName, event) {
            const track = trackDatabase[trackName];
            if (!track) return;

            // Inicializa o contexto de áudio se não existir
            if (!audioContext) {
                audioContext = new (window.AudioContext || window.webkitAudioContext)();
                analyser = audioContext.createAnalyser();
                analyser.fftSize = 64; // Tamanho ideal para evitar overhead de processamento
                source = audioContext.createMediaElementSource(audioPlayer);
                source.connect(analyser);
                analyser.connect(audioContext.destination);
            }

            if (audioContext.state === 'suspended') {
                audioContext.resume();
            }

            const clickedBtn = event.target;
            
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
                // Reseta os estados visuais de outros botões
                document.querySelectorAll('.play-btn').forEach(btn => {
                    btn.innerText = "RUN_";
                    btn.style.backgroundColor = "transparent";
                    btn.style.color = "var(--accent-color)";
                });

                // Injeta a nova faixa com barramento limpo
                currentTrackName = trackName;
                audioPlayer.src = track.url;
                
                audioPlayer.play()
                    .then(() => {
                        clickedBtn.innerText = "STOP_";
                        clickedBtn.style.backgroundColor = "var(--accent-color)";
                        clickedBtn.style.color = "#fff";
                        console.log("Tripalium Engine injetada: " + trackName);
                    })
                    .catch(err => {
                        console.log("Erro no barramento de streaming externo: ", err);
                        // Fallback caso o servidor externo de testes dê timeout
                        audioPlayer.play();
                    });
            }
        }

        // ==========================================================
        // 2. RENDERIZADOR GRÁFICO 3D MUSGO REATIVO (THREE.JS)
        // ==========================================================
        const container = document.getElementById('canvas-3d-container');
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
        
        renderer.setSize(window.innerWidth, window.innerHeight);
        container.appendChild(renderer.domElement);

        // Geometria da carcaça industrial (Malha estruturada em wireframe adaptada ao verde musgo)
        const geometry = new THREE.IcosahedronGeometry(2, 1);
        const material = new THREE.MeshStandardMaterial({ 
            color: 0x2e4235, /* Tom de metal esverdeado industrial */
            wireframe: true, 
            roughness: 0.2,
            metalness: 0.8
        });
        const meshIndustrial = new THREE.Mesh(geometry, material);
        scene.add(meshIndustrial);

        // Iluminação estroboscópica otimizada
        const redLight = new THREE.PointLight(0xff0000, 2, 50);
        redLight.position.set(5, 5, 5);
        scene.add(redLight);

        const yellowLight = new THREE.PointLight(0xffcc00, 1, 50);
        yellowLight.position.set(-5, -5, 5);
        scene.add(yellowLight);

        camera.position.z = 5;

        const dataArray = new Uint8Array(32);

        // Loop contínuo - Processamento de física leve para não travar o áudio
        function animate() {
            requestAnimationFrame(animate);
            
            if (analyser && !audioPlayer.paused) {
                analyser.getByteFrequencyData(dataArray);
                
                // Grava a resposta dos graves de forma suave (interpolação simples)
                let bassFrequency = dataArray[2] / 255; 
                
                meshIndustrial.scale.set(1 + bassFrequency, 1 + bassFrequency, 1 + bassFrequency);
                meshIndustrial.rotation.x += 0.008 + (bassFrequency * 0.03);
                meshIndustrial.rotation.y += 0.008 + (bassFrequency * 0.03);
                
                redLight.intensity = 1.5 + (dataArray[12] / 50);
            } else {
                meshIndustrial.rotation.x += 0.002;
                meshIndustrial.rotation.y += 0.002;
                meshIndustrial.scale.set(1, 1, 1);
                redLight.intensity = 1.5;
            }

            renderer.render(scene, camera);
        }
        animate();

        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>
