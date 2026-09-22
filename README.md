
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks Radio - Heavy Metal & Rock</title>
    <link href="https://fonts.googleapis.com/css2?family=Metal+Mania&family=Fira+Code:wght@400;700&display=swap" rel="stylesheet">
    <style>
        * { box-sizing: border-box; }
        body {
            margin: 0;
            background-color: #07030a;
            color: #ffffff;
            font-family: 'Fira Code', monospace;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            align-items: center;
            justify-content: center;
            padding: 20px;
            overflow-x: hidden;
        }

        .container {
            background: #10061d;
            border: 4px solid #000;
            box-shadow: 8px 8px 0px #000;
            padding: 2rem;
            text-align: center;
            max-width: 500px;
            width: 100%;
        }

        h1 {
            font-family: 'Metal Mania', cursive;
            font-size: 3.5rem;
            margin: 0;
            color: #fff;
            text-shadow: 3px 3px 0px #000, 6px 6px 0px #8a2be2;
            letter-spacing: 2px;
        }

        .subtitle {
            font-size: 0.85rem;
            color: #bfaad1;
            text-transform: uppercase;
            letter-spacing: 3px;
            margin: 10px 0 25px 0;
            font-weight: bold;
        }

        .player-box {
            background: #000000;
            border: 3px solid #8a2be2;
            padding: 20px;
            box-shadow: inset 0 0 15px rgba(138, 43, 226, 0.3);
        }

        .track-info {
            background: #140824;
            border: 2px dashed #39ff14;
            padding: 12px;
            margin-bottom: 20px;
        }

        .track-label {
            font-size: 0.75rem;
            color: #39ff14;
            text-transform: uppercase;
            margin-bottom: 5px;
            font-weight: bold;
        }

        #current-track-title {
            font-size: 1.1rem;
            font-weight: bold;
            color: #fff;
            text-shadow: 1px 1px 0px #000;
        }

        .controls {
            display: flex;
            justify-content: center;
            gap: 12px;
            margin-bottom: 20px;
        }

        .btn {
            background: #8a2be2;
            color: #fff;
            border: 3px solid #000;
            padding: 12px 20px;
            font-family: 'Fira Code', monospace;
            font-weight: bold;
            font-size: 1rem;
            cursor: pointer;
            box-shadow: 4px 4px 0px #000;
            text-transform: uppercase;
            transition: 0.1s;
        }

        .btn:active {
            box-shadow: 1px 1px 0px #000;
            transform: translate(3px, 3px);
        }

        .btn-main {
            background: #39ff14;
            color: #000;
            flex-grow: 1;
        }

        .visualizer {
            display: flex;
            justify-content: center;
            gap: 6px;
            height: 25px;
            align-items: flex-end;
            margin-bottom: 15px;
        }

        .bar {
            width: 8px;
            background: #39ff14;
            height: 4px;
            transition: height 0.15s ease;
        }

        .playing .bar {
            animation: bounce 0.5s infinite alternate;
        }
        .bar:nth-child(2) { animation-delay: 0.1s; }
        .bar:nth-child(3) { animation-delay: 0.3s; }
        .bar:nth-child(4) { animation-delay: 0.2s; }
        .bar:nth-child(5) { animation-delay: 0.4s; }

        @keyframes bounce {
            0% { height: 4px; }
            100% { height: 22px; }
        }

        .status {
            font-size: 0.8rem;
            color: #39ff14;
            font-weight: bold;
            letter-spacing: 1px;
        }

        footer {
            margin-top: 25px;
            font-size: 0.75rem;
            color: #6a5a80;
            text-transform: uppercase;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Nels1Rocks</h1>
        <div class="subtitle">24/7 Heavy Metal & Rock Infinite Loop</div>
        
        <div class="player-box">
            <div class="track-info">
                <div class="track-label">▶ TOCANDO AGORA NA PROGRAMAÇÃO</div>
                <div id="current-track-title">Carregando Setlist...</div>
            </div>

            <div class="visualizer" id="viz">
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
            </div>

            <div class="controls">
                <button class="btn btn-main" id="playBtn">▶ LIGAR RÁDIO</button>
                <button class="btn" id="nextBtn">⏭ PRÓXIMA</button>
            </div>

            <div id="statusText" class="status">SISTEMA PRONTO</div>
        </div>

        <footer>
            &copy; 2026 Nels1Rocks Radio • Powered by AutoLoop Engine
        </footer>
    </div>

    <script>
        // Setlist Infinito de Heavy Metal & Rock com streams de áudio de alta performance
        const playlist = [
            {
                title: "Nels1Rocks Heavy Metal Anthem (Live Stream)",
                url: "https://rautemusik-de-hz-fal-stream13.radiohost.de/hardrock_mp3_192"
            },
            {
                title: "Classic Rock & Metal Master Stream",
                url: "https://stream.antwrp.be/rock"
            },
            {
                title: "Power Metal & Guitar Heavy Rotation",
                url: "https://stream.rockantenne.de/heavy-metal/stream/mp3"
            }
        ];

        let currentTrackIndex = 0;
        let audio = new Audio();
        audio.crossOrigin = "anonymous";

        const playBtn = document.getElementById('playBtn');
        const nextBtn = document.getElementById('nextBtn');
        const statusText = document.getElementById('statusText');
        const trackTitle = document.getElementById('current-track-title');
        const viz = document.getElementById('viz');

        let isPlaying = false;

        function loadTrack(index) {
            currentTrackIndex = index;
            audio.src = playlist[currentTrackIndex].url;
            trackTitle.textContent = playlist[currentTrackIndex].title;
            audio.load();
        }

        function togglePlay() {
            if (!isPlaying) {
                statusText.textContent = "CONECTANDO AO ESTÚDIO...";
                audio.play().then(() => {
                    isPlaying = true;
                    playBtn.textContent = "⏸ PAUSAR";
                    statusText.textContent = "🔴 AO VIVO NO AR";
                    viz.classList.add('playing');
                }).catch(err => {
                    console.error(err);
                    statusText.textContent = "⚠️ TOQUE NOVAMENTE PARA LIBERAR";
                });
            } else {
                audio.pause();
                isPlaying = false;
                playBtn.textContent = "▶ LIGAR RÁDIO";
                statusText.textContent = "ESTÚDIO PAUSADO";
                viz.classList.remove('playing');
            }
        }

        playBtn.addEventListener('click', togglePlay);

        nextBtn.addEventListener('click', () => {
            currentTrackIndex = (currentTrackIndex + 1) % playlist.length;
            loadTrack(currentTrackIndex);
            if (isPlaying) {
                audio.play();
            }
        });

        audio.addEventListener('ended', () => {
            // Loop infinito automático para a próxima faixa da setlist
            currentTrackIndex = (currentTrackIndex + 1) % playlist.length;
            loadTrack(currentTrackIndex);
            audio.play();
        });

        audio.addEventListener('error', () => {
            statusText.textContent = "⚠️ ALTERNANDO CANAL DE BACKUP...";
            setTimeout(() => {
                currentTrackIndex = (currentTrackIndex + 1) % playlist.length;
                loadTrack(currentTrackIndex);
                if (isPlaying) audio.play();
            }, 2000);
        });

        // Inicializa a primeira faixa
        loadTrack(0);
    </script>
</body>
</html>
