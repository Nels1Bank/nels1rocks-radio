
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks Radio</title>
    <link href="https://fonts.googleapis.com/css2?family=Metal+Mania&family=Fira+Code:wght@400;700&display=swap" rel="stylesheet">
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

        /* Painel Central do Transmissor */
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

        /* Grid de Frequências / Estações */
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

        .s-sin { color: #ffcc00; } 

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

    <header>
        <h1>Nels1Rocks</h1>
        <div class="subtitle">Heavy Metal & Rock Web Radio</div>
    </header>

    <main>
        <section>
            <h2>Sobre a Rádio</h2>
            <p>Seja bem-vindo ao transmissor oficial da Nels1Rocks. Som pesado, sem frescura e direto na sua frequência.</p>
        </section>

        <!-- Painel Central do Transmissor -->
        <div class="live-player-panel">
            <div class="stream-status">
                <span>STATUS:</span>
                <div id="status-display" class="segment-display-8">PARADO</div>
            </div>
            
            <!-- Elemento de áudio escondido para tocar o stream -->
            <audio id="radio-audio" preload="none"></audio>

            <div class="master-controls">
                <button id="play-btn" class="main-play-btn">▶ PLAY</button>
            </div>
        </div>

        <!-- Estações / Links de Stream -->
        <section style="margin-top: 3rem;">
            <h2>Frequências</h2>
            <div class="station-grid">
                <div class="station-card active-station" data-stream="https://icecast.somossistemas.com.br/proxy/nels1rocks?mp=/stream">
                    <div class="station-info">
                        <div class="station-title">Nels1Rocks Main Stream</div>
                        <div class="station-genre">Heavy Metal / Rock</div>
                    </div>
                    <div class="select-panel">
                        <span class="select-indicator s-sin">● ATIVO</span>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <footer>
        &copy; 2026 Nels1Rocks Radio. Todos os direitos reservados.
    </footer>

    <script>
        const audio = document.getElementById('radio-audio');
        const playBtn = document.getElementById('play-btn');
        const statusDisplay = document.getElementById('status-display');
        const stationCard = document.querySelector('.station-card');

        let currentStreamUrl = stationCard.getAttribute('data-stream');
        let isPlaying = false;

        playBtn.addEventListener('click', () => {
            if (!isPlaying) {
                statusDisplay.textContent = 'CONECTANDO...';
                audio.src = currentStreamUrl;
                audio.play().then(() => {
                    isPlaying = true;
                    playBtn.textContent = '⏹ PARAR';
                    statusDisplay.textContent = 'AO VIVO';
                }).catch((error) => {
                    console.error("Erro ao reproduzir:", error);
                    statusDisplay.textContent = 'ERRO AO CONECTAR';
                    isPlaying = false;
                    playBtn.textContent = '▶ PLAY';
                });
            } else {
                audio.pause();
                audio.src = '';
                isPlaying = false;
                playBtn.textContent = '▶ PLAY';
                statusDisplay.textContent = 'PARADO';
            }
        });

        // Tratamento caso caia a conexão do stream
        audio.addEventListener('error', () => {
            statusDisplay.textContent = 'ERRO NO STREAM';
            playBtn.textContent = '▶ PLAY';
            isPlaying = false;
        });
    </script>
</body>
</html>
