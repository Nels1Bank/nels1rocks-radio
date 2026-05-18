
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks | Rádio Gibi Digital</title>
    
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

        /* Grid de Frequências */
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

        .guidance-highlight {
            color: var(--purple-neon);
            font-weight: bold;
        }

        .blink-char {
            transition: color 0.1s ease;
        }

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

        @media (max-width: 600px) {
            .adsense-btc-container {
                flex-direction: column;
                text-align: center;
            }
            .adsense-content {
                flex-direction: column;
                gap: 10px;
            }
            .adsense-label {
                writing-mode: horizontal-tb;
                transform: none;
                border-left: none;
                border-bottom: 2px solid #331a4a;
                padding-bottom: 4px;
                width: 100%;
            }
            .select-panel {
                align-items: center;
                margin-top: 1rem;
            }
            .now-playing-meta {
                text-align: center;
            }
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

    <!-- Motor Gráfico 3D (Three.js) -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
</head>
<body>

    <!-- Skin 3D de Fundo (Caveira Heavy Metal) -->
    <div id="canvas-3d-container"></div>

    <header>
        <h1>NELS1ROCKS</h1>
        <div class="subtitle">Singularidade da Música 🎶</div>
    </header>

    <main>
        <section id="estudio">
            <h2>[ESTÚDIO GIBI CORE]</h2>
            <p>Independência mental, linhas pretas expressivas e distorção saturada. Operando o console de quadrinhos diretamente do refúgio anti-burocrático.</p>
        </section>

        <section id="radio-core">
            <h2>CONSOLE TRANSMISSOR</h2>
            
            <!-- Painel de Controle Principal -->
            <div class="live-player-panel">
                <div class="stream-status">
                    <div class="segment-display-8" id="bit-display">0</div>
                    <!-- Modificado para atualizar automaticamente via JS -->
                    <span id="track-display">SINAL EM SUCÇÃO (STANDBY)</span>
                </div>
                
                <div class="master-controls">
                    <button class="main-play-btn" id="master-play-btn" onclick="toggleStream()">LIGAR_SINAL</button>
                </div>
            </div>

            <!-- Setlist Integrada de Streams -->
            <h3 style="margin-top: 2.5rem; color: var(--accent-yellow); text-shadow: 2px 2px 0px #000;">SETLIST DE FREQUÊNCIAS</h3>
            <div class="station-grid">
                
                <!-- Frequência 01 -->
                <div class="station-card active-station" onclick="selectStation(0, 'STREAM PRINCIPAL: HEAVY METAL')">
                    <div class="station-info">
                        <div class="station-title">Frequência 01 - Pure Metal Live</div>
                        <div class="station-genre">Estilo: Heavy, Thrash & Death</div>
                    </div>
                    <div class="select-panel">
                        <div class="select-indicator" id="ind-0">
                            <span class="s-sin">SIN</span><span class="s-to">TO</span><span class="s-ni">NI</span><span class="s-za">ZA</span><span class="s-do">DO</span><span class="blink-char" id="char-0">_</span>
                        </div>
                        <div class="now-playing-meta" id="meta-0">Tripalium - Karma Mecânico</div>
                    </div>
                </div>

                <!-- Frequência 02 -->
                <div class="station-card" onclick="selectStation(1, 'STREAM SECUNDÁRIA: HARD ROCK')">
                    <div class="station-info">
                        <div class="station-title">Frequência 02 - Rock Classics Digital</div>
                        <div class="station-genre">Estilo: Classic Rock & Grunge</div>
                    </div>
                    <div class="select-panel">
                        <div class="select-indicator" id="ind-1" style="color: #ff4500;">CONECTAR<span class="blink-char" id="char-1">_</span></div>
                        <div class="now-playing-meta" id="meta-1" style="display: none;">Black Sabbath - Iron Man</div>
                    </div>
                </div>

                <!-- Frequência 03 -->
                <div class="station-card" onclick="selectStation(2, 'STREAM TERCIÁRIA: INDUSTRIAL')">
                    <div class="station-info">
                        <div class="station-title">Frequência 03 - Industrial & Prog Core</div>
                        <div class="station-genre">Estilo: Industrial, Prog & Djent</div>
                    </div>
                    <div class="select-panel">
                        <div class="select-indicator" id="ind-2" style="color: #ff4500;">CONECTAR<span class="blink-char" id="char-2">_</span></div>
                        <div class="now-playing-meta" id="meta-2" style="display: none;">Nine Inch Nails - Closer</div>
                    </div>
                </div>

            </div>
        </section>
    </main>

    <!-- BLOCO ADSENSE: BITCOIN HARD MONEY CORE -->
    <div class="adsense-btc-container">
        <div class="adsense-label">Anúncio</div>
        <div class="adsense-content">
            <div class="btc-ticker-art">₿</div>
            <div class="btc-ad-text">
                <h4 class="btc-ad-title">21 Milhões. Sem Bypass.</h4>
                <p class="btc-ad-desc">Proteja seu power de compra na camada zero da matemática digital. Escassez absoluta auditada por nós.</p>
            </div>
            <button class="btc-ad-btn" onclick="window.open('https://bitcoin.org', '_blank')">Ver Node</button>
        </div>
    </div>

    <footer>
        <p><span class="guidance-highlight">Guidance Live Asset</span> © 2026 // Arquitetura sônica estruturada na física pura.</p>
    </footer>

    <script>
        const realApis = [
            "https://stream.screamer-radio.com/metal_high",
            "https://listen.radiorock.fi/rock_128.mp3",
            "https://icecast.omroep.nl/3fm-alternatief-mp3"
        ];

        const trackMeta = [
            "Tripalium - Karma Mecânico",
            "Black Sabbath - Iron Man",
            "Nine Inch Nails - Closer"
        ];

        let currentStationIndex = 0;
        const audioPlayer = new Audio();
        audioPlayer.crossOrigin = "anonymous"; 
        
        let audioContext;
        let analyser;
        let source;
        const dataArray = new Uint8Array(32);
        let isPlaying = false;
        
        let blinkIntervalId = null;
        let bitIntervalId = null; 
        const strobeColors = ['#ffcc00', '#8a2be2', '#ffffff', '#00bfff', '#ff4500']; 
        let colorCounter = 0;
        let currentBit = 0;

        const sintonizadoHTML = `<span class="s-sin">SIN</span><span class="s-to">TO</span><span class="s-ni">NI</span><span class="s-za">ZA</span><span class="s-do">DO</span>`;

        function startBitDisplay() {
            const bitDisplay = document.getElementById('bit-display');
            bitDisplay.classList.add('active-bit');
            
            if (bitIntervalId) clearInterval(bitIntervalId);
            bitIntervalId = setInterval(() => {
                currentBit = currentBit === 0 ? 1 : 0;
                bitDisplay.innerText = currentBit;
            }, 500); 
        }

        function stopBitDisplay() {
            if (bitIntervalId) {
                clearInterval(bitIntervalId);
                bitIntervalId = null;
            }
            const bitDisplay = document.getElementById('bit-display');
            bitDisplay.classList.remove('active-bit');
            bitDisplay.innerText = "0"; 
        }

        function startHifenStrobe() {
            if (blinkIntervalId) clearInterval(blinkIntervalId);
            blinkIntervalId = setInterval(() => {
                const activeChar = document.getElementById(`char-${currentStationIndex}`);
                if (activeChar) {
                    activeChar.style.color = strobeColors[colorCounter % strobeColors.length];
                    colorCounter++;
                }
            }, 300); 
        }

        function stopHifenStrobe() {
            if (blinkIntervalId) {
                clearInterval(blinkIntervalId);
                blinkIntervalId = null;
            }
            document.querySelectorAll('.blink-char').forEach((char, idx) => {
                char.style.color = (idx === currentStationIndex) ? '#39ff14' : '#ff4500';
            });
        }

        // FUNÇÃO ATUALIZADA: Mágica do automatismo acontece aqui
        function selectStation(index, displayName) {
            stopHifenStrobe();
            currentStationIndex = index;
            
            // Pega dinamicamente os metadados corretos da array trackMeta
            const musicaAtual = trackMeta[index];
            
            document.querySelectorAll('.station-card').forEach((card, idx) => {
                card.classList.remove('active-station');
                const metaElement = document.getElementById(`meta-${idx}`);
                
                if (idx === index) {
                    document.getElementById(`ind-${idx}`).innerHTML = `${sintonizadoHTML}<span class="blink-char" id="char-${idx}">_</span>`;
                    if (metaElement) {
                        metaElement.style.display = "block";
                        metaElement.innerText = musicaAtual; // Injeta o texto automático
                    }
                } else {
                    document.getElementById(`ind-${idx}`).innerHTML = `CONECTAR<span class="blink-char" id="char-${idx}">_</span>`;
                    if (metaElement) {
                        metaElement.style.display = "none";
                    }
                }
            });

            const cards = document.querySelectorAll('.station-card');
            cards[index].classList.add('active-station');

            if (isPlaying) {
                audioPlayer.src = realApis[currentStationIndex];
                audioPlayer.play()
                    .then(() => {
                        // Mostra automaticamente o nome da música ativa no painel principal
                        document.getElementById('track-display').innerText = `${musicaAtual} [ONLINE]`;
                        startHifenStrobe();
                    })
                    .catch(err => console.log("Erro no barramento: ", err));
            } else {
                // Atualiza o painel principal mesmo com o player desligado
                document.getElementById('track-display').innerText = `${musicaAtual} - PRONTA PARA RODAR`;
                stopHifenStrobe();
            }
        }

        function toggleStream() {
            const playBtn = document.getElementById('master-play-btn');
            const display = document.getElementById('track-display');
            const musicaAtual = trackMeta[currentStationIndex];

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
                        console.log("AudioContext em bypass.");
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
                        // Troca o texto estático pelo nome da música ativa rodando em tempo real
                        display.innerText = `${musicaAtual} [ONLINE]`;
                        startHifenStrobe(); 
                        startBitDisplay();
                    })
                    .catch(err => {
                        audioPlayer.src = "https://stream.rockantenne.de/heavy-metal/stream/mp3";
                        audioPlayer.play();
                        isPlaying = true;
                        playBtn.innerText = "DESLIGAR_";
                        display.innerText = `${musicaAtual} - SINGULARIDADE SONORA`; 
                        startHifenStrobe();
                        startBitDisplay();
                    });

            } else {
                audioPlayer.pause();
                audioPlayer.src = ""; 
                isPlaying = false;
                playBtn.innerText = "LIGAR_SINAL";
                playBtn.style.backgroundColor = "#2a1545";
                display.innerText = "SINAL EM SUCÇÃO (STANDBY)";
                stopHifenStrobe(); 
                stopBitDisplay();
            }
        }

        // ==========================================================
        // RENDERIZADOR 3D: CAVEIRA HEAVY METAL PROCEDURAL (CEL SHADING)
        // ==========================================================
        const container = document.getElementById('canvas-3d-container');
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 1000);
        
        const renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        container.appendChild(renderer.domElement);

        const format = (renderer.capabilities.isWebGL2) ? THREE.RedFormat : THREE.LuminanceFormat;
        const colorsColors = new Uint8Array([0, 0, 0, 100, 100, 100, 255, 255, 255]);
        const gradientMap = new THREE.DataTexture(colorsColors, 3, 1, format);
        gradientMap.needsUpdate = true;

        const metalMaterial = new THREE.MeshToonMaterial({ 
            color: 0x5a4f7c, 
            gradientMap: gradientMap
        });
        const darkMaterial = new THREE.MeshToonMaterial({ color: 0x11081c, gradientMap: gradientMap });
        const outlineMaterial = new THREE.MeshBasicMaterial({ color: 0x000000, side: THREE.BackSide });

        const skullGroup = new THREE.Group();

        function createThickMesh(geometry, material) {
            const mesh = new THREE.Mesh(geometry, material);
            const outlineMesh = new THREE.Mesh(geometry, outlineMaterial);
            outlineMesh.scale.multiplyScalar(1.06);
            mesh.add(outlineMesh);
            return mesh;
        }

        const craniumGeo = new THREE.SphereGeometry(1.4, 32, 32);
        craniumGeo.scale(1, 1.15, 1);
        const cranium = createThickMesh(craniumGeo, metalMaterial);
        cranium.position.y = 0.3;
        skullGroup.add(cranium);

        const eyeGeo = new THREE.SphereGeometry(0.35, 16, 16);
        const leftEye = createThickMesh(eyeGeo, darkMaterial);
        leftEye.position.set(-0.45, 0.3, 1.1);
        const rightEye = createThickMesh(eyeGeo, darkMaterial);
        rightEye.position.set(0.45, 0.3, 1.1);
        skullGroup.add(leftEye, rightEye);

        const noseGeo = new THREE.ConeGeometry(0.2, 0.4, 4);
        noseGeo.rotateX(Math.PI);
        const nose = createThickMesh(noseGeo, darkMaterial);
        nose.position.set(0, -0.05, 1.25);
        nose.scale.set(1, 1, 0.4);
        skullGroup.add(nose);

        const jawUpperGeo = new THREE.BoxGeometry(0.9, 0.4, 0.8);
        const jawUpper = createThickMesh(jawUpperGeo, metalMaterial);
        jawUpper.position.set(0, -0.4, 0.8);
        skullGroup.add(jawUpper);

        for (let i = -3; i <= 3; i++) {
            const toothGeo = new THREE.BoxGeometry(0.07, 0.12, 0.1);
            const tooth = createThickMesh(toothGeo, new THREE.MeshBasicMaterial({ color: 0xffffff }));
            tooth.position.set(i * 0.11, -0.58, 1.15);
            skullGroup.add(tooth);
        }

        const jawLowerGroup = new THREE.Group();
        const jawLowerGeo = new THREE.BoxGeometry(0.8, 0.3, 0.7);
        const jawLowerMesh = createThickMesh(jawLowerGeo, metalMaterial);
        jawLowerMesh.position.set(0, -0.15, 0.2);
        jawLowerGroup.add(jawLowerMesh);

        for (let i = -2; i <= 2; i++) {
            const toothGeo = new THREE.BoxGeometry(0.07, 0.12, 0.1);
            const tooth = createThickMesh(toothGeo, new THREE.MeshBasicMaterial({ color: 0xffffff }));
            tooth.position.set(i * 0.12, 0.02, 0.5);
            jawLowerGroup.add(tooth);
        }
        jawLowerGroup.position.set(0, -0.65, 0.6);
        skullGroup.add(jawLowerGroup);

        scene.add(skullGroup);

        const dirLight1 = new THREE.DirectionalLight(0xffffff, 2.2);
        dirLight1.position.set(6, 6, 6);
        scene.add(dirLight1);

        const dirLight2 = new THREE.DirectionalLight(0x8a2be2, 1.8);
        dirLight2.position.set(-6, -2, 4);
        scene.add(dirLight2);

        camera.position.z = 5.0;

        function animate() {
            requestAnimationFrame(animate);
            
            if (analyser && isPlaying) {
                analyser.getByteFrequencyData(dataArray);
                let bass = dataArray[2] / 255;
                let treble = dataArray[12] / 255;
                
                let scaleFactor = 1 + (bass * 0.25);
                skullGroup.scale.set(scaleFactor, scaleFactor, scaleFactor);
                
                skullGroup.rotation.x = Math.sin(Date.now() * 0.001) * 0.15 + (treble * 0.1);
                skullGroup.rotation.y += 0.012 + (bass * 0.03);
                
                jawLowerGroup.position.y = -0.65 - (bass * 0.35);
            } else {
                let time = Date.now() * 0.001;
                skullGroup.rotation.x = Math.sin(time) * 0.1;
                skullGroup.rotation.y += 0.006;
                skullGroup.position.y = Math.sin(time * 1.5) * 0.08;
                skullGroup.scale.set(1, 1, 1);
                jawLowerGroup.position.y = -0.65;
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
