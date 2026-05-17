
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks | Rádio Digital</title>
    
    <!-- Google Fonts para Tipografia Industrial/Metal -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;700&family=Metal+Mania&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-dark: #0a0512;          /* Roxo ultra escuro de fundo */
            --purple-neon: #8a2be2;      /* Roxo Neon principal */
            --moss-green: #1e3f20;       /* Verde Musgo Escuro de estrutura */
            --green-neon: #39ff14;       /* Verde ativo reativo */
            --white-pure: #ffffff;       /* Branco para textos legíveis */
            --accent-yellow: #ffcc00;    /* Amarelo industrial */
            --panel-bg: rgba(20, 10, 30, 0.85);
        }

        body {
            margin: 0;
            padding: 0;
            background-color: var(--bg-dark);
            color: var(--white-pure);
            font-family: 'Fira Code', monospace;
            overflow-x: hidden;
        }

        /* Container da Skin 3D */
        #canvas-3d-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: -1;
            background: radial-gradient(circle, #1c0a35 0%, #05020a 100%);
        }

        header {
            background: linear-gradient(180deg, rgba(14, 5, 26, 0.95) 0%, rgba(0,0,0,0) 100%);
            padding: 2.5rem 2rem;
            text-align: center;
            border-bottom: 4px solid var(--moss-green);
            box-shadow: 0 4px 20px rgba(138, 43, 226, 0.3);
        }

        h1 {
            font-family: 'Metal Mania', cursive;
            font-size: 4.5rem;
            color: var(--white-pure);
            margin: 0;
            text-shadow: 3px 3px 0px var(--purple-neon), -2px -2px 0px var(--moss-green);
            letter-spacing: 3px;
        }

        .subtitle {
            font-size: 0.95rem;
            color: var(--green-neon);
            text-transform: uppercase;
            letter-spacing: 5px;
            margin-top: 0.7rem;
            font-weight: bold;
        }

        main {
            max-width: 850px;
            margin: 3rem auto;
            padding: 2.5rem;
            background: var(--panel-bg);
            border: 3px solid var(--moss-green);
            box-shadow: 0 0 30px rgba(138, 43, 226, 0.2);
            backdrop-filter: blur(6px);
            border-radius: 8px;
        }

        section {
            margin-bottom: 2.5rem;
        }

        h2 {
            font-family: 'Metal Mania', cursive;
            font-size: 2.3rem;
            color: var(--white-pure);
            border-bottom: 2px solid var(--purple-neon);
            padding-bottom: 0.5rem;
            text-transform: uppercase;
        }

        p {
            line-height: 1.7;
            font-size: 1.1rem;
            color: #dcd6e8;
        }

        /* Painel Central do Player de Stream */
        .live-player-panel {
            background: rgba(30, 63, 32, 0.3); 
            border: 2px solid var(--purple-neon);
            padding: 2rem;
            border-radius: 6px;
            text-align: center;
            margin-top: 2rem;
            position: relative;
        }

        .stream-status {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            font-weight: bold;
            font-size: 1.2rem;
            margin-bottom: 1.5rem;
            color: var(--white-pure);
        }

        .status-led {
            width: 12px;
            height: 12px;
            background-color: #555;
            border-radius: 50%;
            transition: all 0.3s ease;
        }

        .status-led.active {
            background-color: var(--green-neon);
            box-shadow: 0 0 12px var(--green-neon);
            animation: pulseLed 1.5s infinite;
        }

        @keyframes pulseLed {
            0% { opacity: 0.5; }
            50% { opacity: 1; }
            100% { opacity: 0.5; }
        }

        .master-controls {
            margin-top: 1rem;
        }

        .main-play-btn {
            background: var(--moss-green);
            border: 2px solid var(--white-pure);
            color: var(--white-pure);
            font-family: 'Fira Code', monospace;
            font-size: 1.4rem;
            font-weight: bold;
            padding: 1rem 3rem;
            cursor: pointer;
            box-shadow: 0 0 15px rgba(57, 255, 20, 0.2);
            transition: all 0.3s ease;
            text-transform: uppercase;
        }

        .main-play-btn:hover {
            background: var(--purple-neon);
            border-color: var(--green-neon);
            box-shadow: 0 0 25px var(--purple-neon);
            transform: scale(1.05);
        }

        /* Lista da Setlist Integrada */
        .station-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 1rem;
            margin-top: 1.5rem;
        }

        .station-card {
            background: rgba(14, 5, 26, 0.7);
            border-left: 6px solid var(--moss-green);
            border-right: 1px solid rgba(255,255,255,0.1);
            border-top: 1px solid rgba(255,255,255,0.1);
            border-bottom: 1px solid rgba(255,255,255,0.1);
            padding: 1.2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.2s ease;
            cursor: pointer;
        }

        .station-card:hover {
            border-left-color: var(--purple-neon);
            background: rgba(30, 63, 32, 0.2);
            transform: translateX(4px);
        }

        .station-card.active-station {
            border-left-color: var(--green-neon);
            background: rgba(138, 43, 226, 0.15);
            box-shadow: inset 0 0 10px rgba(138, 43, 226, 0.3);
        }

        .station-info .station-title {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--white-pure);
        }

        .station-info .station-genre {
            font-size: 0.85rem;
            color: var(--green-neon);
            margin-top: 0.3rem;
            text-transform: uppercase;
        }

        .select-indicator {
            font-size: 0.9rem;
            color: var(--purple-neon);
            font-weight: bold;
        }

        .active-station .select-indicator {
            color: var(--green-neon);
        }

        /* Classe para isolar o caractere do hífen/underscore na manipulação de cor */
        .blink-char {
            transition: color 0.1s ease;
        }

        footer {
            text-align: center;
            padding: 2.5rem;
            font-size: 0.85rem;
            color: #6a5a80;
            border-top: 2px solid var(--moss-green);
            background: #06030b;
        }
    </style>

    <!-- Motor Gráfico 3D (Three.js) -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
</head>
<body>

    <!-- Skin 3D de Fundo -->
    <div id="canvas-3d-container"></div>

    <header>
        <h1>NELS1ROCKS</h1>
        <div class="subtitle">Singularidade do Bug // Múltiplos Maravilhosos</div>
    </header>

    <main>
        <section id="estudio">
            <h2>[ESTÚDIO AUTORAL]</h2>
            <p>Independência mental, cauda longa e distorção analógica. Operando na frequência invisível do refúgio sônico com conexões diretas via satélite de rede.</p>
        </section>

        <section id="radio-core">
            <h2>CONSOLE TRANSMISSOR</h2>
            
            <!-- Painel de Controle Principal -->
            <div class="live-player-panel">
                <div class="stream-status">
                    <div class="status-led" id="live-led"></div>
                    <span id="track-display">SINAL EM SUCÇÃO (STANDBY)</span>
                </div>
                
                <div class="master-controls">
                    <button class="main-play-btn" id="master-play-btn" onclick="toggleStream()">LIGAR_SINAL</button>
                </div>
            </div>

            <!-- Setlist Integrada de Streams -->
            <h3 style="margin-top: 2.5rem; color: var(--green-neon);">SETLIST DE FREQUÊNCIAS</h3>
            <div class="station-grid">
                
                <!-- Frequência 01 -->
                <div class="station-card active-station" onclick="selectStation(0, 'STREAM PRINCIPAL: HEAVY METAL')">
                    <div class="station-info">
                        <div class="station-title">Frequência 01 - Pure Metal Live</div>
                        <div class="station-genre">Estilo: Heavy, Thrash & Death</div>
                    </div>
                    <div class="select-indicator" id="ind-0">SINTONIZADO<span class="blink-char" id="char-0">_</span></div>
                </div>

                <!-- Frequência 02 -->
                <div class="station-card" onclick="selectStation(1, 'STREAM SECUNDÁRIA: HARD ROCK')">
                    <div class="station-info">
                        <div class="station-title">Frequência 02 - Rock Classics Digital</div>
                        <div class="station-genre">Estilo: Classic Rock & Grunge</div>
                    </div>
                    <div class="select-indicator" id="ind-1">CONECTAR<span class="blink-char" id="char-1">_</span></div>
                </div>

                <!-- Frequência 03 -->
                <div class="station-card" onclick="selectStation(2, 'STREAM TERCIÁRIA: INDUSTRIAL')">
                    <div class="station-info">
                        <div class="station-title">Frequência 03 - Industrial & Prog Core</div>
                        <div class="station-genre">Estilo: Industrial, Prog & Djent</div>
                    </div>
                    <div class="select-indicator" id="ind-2">CONECTAR<span class="blink-char" id="char-2">_</span></div>
                </div>

            </div>
        </section>
    </main>

    <footer>
        <p>Nels1Bank & Guidance Live Asset © 2026 // Arquitetura sônica estruturada na física pura.</p>
    </footer>

    <script>
        // Links alternativos de alta estabilidade
        const realApis = [
            "https://stream.screamer-radio.com/metal_high",
            "https://listen.radiorock.fi/rock_128.mp3",
            "https://icecast.omroep.nl/3fm-alternatief-mp3"
        ];

        let currentStationIndex = 0;
        const audioPlayer = new Audio();
        audioPlayer.crossOrigin = "anonymous"; 
        
        let audioContext;
        let analyser;
        let source;
        const dataArray = new Uint8Array(32);
        let isPlaying = false;
        
        // Variáveis de controle do estrobo do hífen
        let blinkIntervalId = null;
        const strobeColors = ['#8a2be2', '#ffcc00', '#39ff14', '#ffffff']; // Roxo, Amarelo, Verde, Branco
        let colorCounter = 0;

        // Gerenciador do Loop do Hífen
        function startHifenStrobe() {
            if (blinkIntervalId) clearInterval(blinkIntervalId);
            
            blinkIntervalId = setInterval(() => {
                // Seleciona apenas o caractere da estação que está sintonizada no momento
                const activeChar = document.getElementById(`char-${currentStationIndex}`);
                if (activeChar) {
                    activeChar.style.color = strobeColors[colorCounter % strobeColors.length];
                    colorCounter++;
                }
            }, 300); // Rotaciona a cor a cada 300ms
        }

        function stopHifenStrobe() {
            if (blinkIntervalId) {
                clearInterval(blinkIntervalId);
                blinkIntervalId = null;
            }
            // Reseta a cor de todos os underscores para o padrão
            document.querySelectorAll('.blink-char').forEach((char, idx) => {
                char.style.color = (idx === currentStationIndex) ? 'var(--green-neon)' : 'var(--purple-neon)';
            });
        }

        function selectStation(index, displayName) {
            // Para o estrobo antigo antes de mudar o índice
            stopHifenStrobe();
            
            currentStationIndex = index;
            
            document.querySelectorAll('.station-card').forEach((card, idx) => {
                card.classList.remove('active-station');
                const textNode = idx === index ? "SINTONIZADO" : "CONECTAR";
                document.getElementById(`ind-${idx}`).innerHTML = `${textNode}<span class="blink-char" id="char-${idx}">_</span>`;
            });

            const cards = document.querySelectorAll('.station-card');
            cards[index].classList.add('active-station');

            if (isPlaying) {
                audioPlayer.src = realApis[currentStationIndex];
                audioPlayer.play()
                    .then(() => {
                        document.getElementById('track-display').innerText = displayName + " [ONLINE]";
                        startHifenStrobe(); // Reativa no novo alvo
                    })
                    .catch(err => console.log("Erro de transmutação: ", err));
            } else {
                document.getElementById('track-display').innerText = "SINTONIA MODIFICADA - PRONTA PARA RODAR";
                stopHifenStrobe();
            }
        }

        function toggleStream() {
            const playBtn = document.getElementById('master-play-btn');
            const led = document.getElementById('live-led');
            const display = document.getElementById('track-display');

            if (!isPlaying) {
                if (!audioContext) {
                    try {
                        audioContext = new (window.AudioContext || window.webkitAudioContext)();
                        analyser = audioContext.createAnalyser();
                        analyser.fftSize = 64;
                        source = audioContext.createMediaElementSource(audioPlayer);
                        source.connect(analyser);
                        analyser.connect(audioContext.destination);
                    } catch (e) {
                        console.log("AudioContext em modo direto.");
                    }
                }

                if (audioContext && audioContext.state === 'suspended') {
                    audioContext.resume();
                }

                audioPlayer.src = realApis[currentStationIndex];
                
                audioPlayer.play()
                    .then(() => {
                        isPlaying = true;
                        playBtn.innerText = "DESLIGAR_";
                        playBtn.style.backgroundColor = "var(--purple-neon)";
                        led.classList.add('active');
                        display.innerText = "SINAL EM TEMPO REAL [ONLINE]";
                        
                        startHifenStrobe(); // Liga o estrobo do hífen na sintonia
                    })
                    .catch(err => {
                        audioPlayer.src = "https://stream.rockantenne.de/heavy-metal/stream/mp3";
                        audioPlayer.play();
                        isPlaying = true;
                        playBtn.innerText = "DESLIGAR_";
                        led.classList.add('active');
                        display.innerText = "ROTA DE CONTINGÊNCIA ATIVA";
                        
                        startHifenStrobe();
                    });

            } else {
                audioPlayer.pause();
                audioPlayer.src = ""; 
                isPlaying = false;
                playBtn.innerText = "LIGAR_SINAL";
                playBtn.style.backgroundColor = "var(--moss-green)";
                led.classList.remove('active');
                display.innerText = "SINAL EM SUCÇÃO (STANDBY)";
                
                stopHifenStrobe(); // Desliga o estrobo
            }
        }

        // ==========================================================
        // 2. SKIN 3D TEMÁTICA: TOROIDE RETORCIDO (THREE.JS)
        // ==========================================================
        const container = document.getElementById('canvas-3d-container');
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
        
        renderer.setSize(window.innerWidth, window.innerHeight);
        container.appendChild(renderer.domElement);

        const geometry = new THREE.TorusKnotGeometry(1.6, 0.4, 100, 16);
        const material = new THREE.MeshStandardMaterial({ 
            color: 0xffffff, 
            wireframe: true,
            roughness: 0.3,
            metalness: 0.8
        });
        const meshIndustrial = new THREE.Mesh(geometry, material);
        scene.add(meshIndustrial);

        const purpleLight = new THREE.PointLight(0x8a2be2, 5, 60);
        purpleLight.position.set(6, 6, 4);
        scene.add(purpleLight);

        const mossLight = new THREE.PointLight(0x39ff14, 3, 60);
        mossLight.position.set(-6, -6, 4);
        scene.add(mossLight);

        camera.position.z = 5.5;

        function animate() {
            requestAnimationFrame(animate);
            
            if (analyser && isPlaying) {
                analyser.getByteFrequencyData(dataArray);
                let bassValue = dataArray[3] / 255;
                let trebleValue = dataArray[14] / 255;
                
                let scaleFactor = 1 + (bassValue * 0.35);
                meshIndustrial.scale.set(scaleFactor, scaleFactor, scaleFactor);
                
                meshIndustrial.rotation.x += 0.005 + (trebleValue * 0.05);
                meshIndustrial.rotation.y += 0.007 + (bassValue * 0.03);
                
                purpleLight.intensity = 3 + (trebleValue * 7);
                mossLight.intensity = 2 + (bassValue * 6);
            } else {
                meshIndustrial.rotation.x += 0.002;
                meshIndustrial.rotation.y += 0.003;
                meshIndustrial.scale.set(1, 1, 1);
                purpleLight.intensity = 4;
                mossLight.intensity = 1.5;
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
