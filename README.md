
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks Rádio</title>
    <link href="https://fonts.googleapis.com/css2?family=Metal+Mania&family=Fira+Code:wght@400;700&display=swap" rel="stylesheet">
    <style>
        * { box-sizing: border-box; }
        body {
            margin: 0;
            background: #07030a;
            color: #ffffff;
            font-family: 'Fira Code', monospace;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        .card {
            background: #10061d;
            border: 4px solid #000;
            box-shadow: 6px 6px 0px #000;
            padding: 2.5rem;
            text-align: center;
            max-width: 480px;
            width: 100%;
        }
        h1 {
            font-family: 'Metal Mania', cursive;
            font-size: 3rem;
            margin: 0 0 10px 0;
            text-shadow: 3px 3px 0px #000, 6px 6px 0px #8a2be2;
        }
        p {
            color: #bfaad1;
            font-size: 0.85rem;
            margin-bottom: 2rem;
            text-transform: uppercase;
            letter-spacing: 2px;
        }
        .player-box {
            background: #000;
            border: 2px solid #8a2be2;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 15px;
        }
        .btn-play {
            background: #39ff14;
            color: #000;
            border: 3px solid #000;
            padding: 14px 28px;
            font-family: 'Fira Code', monospace;
            font-weight: bold;
            font-size: 1.1rem;
            cursor: pointer;
            box-shadow: 4px 4px 0px #000;
            text-transform: uppercase;
            transition: 0.1s;
        }
        .btn-play:active {
            box-shadow: 1px 1px 0px #000;
            transform: translate(3px, 3px);
        }
        .btn-play.playing {
            background: #ff3333;
            color: #fff;
        }
        .status {
            font-size: 0.8rem;
            color: #39ff14;
            font-weight: bold;
            letter-spacing: 1px;
        }
        .visualizer {
            display: flex;
            gap: 4px;
            height: 20px;
            align-items: flex-end;
            margin-top: 5px;
        }
        .bar {
            width: 6px;
            background: #39ff14;
            height: 4px;
            transition: height 0.2s;
        }
        .playing .bar {
            animation: bounce 0.6s infinite alternate;
        }
        .bar:nth-child(2) { animation-delay: 0.2s; }
        .bar:nth-child(3) { animation-delay: 0.4s; }
        .bar:nth-child(4) { animation-delay: 0.1s; }

        @keyframes bounce {
            0% { height: 4px; }
            100% { height: 18px; }
        }
    </style>
</head>
<body>

    <div class="card">
        <h1>Nels1Rocks</h1>
        <p>Heavy Metal & Rock Stream</p>
        
        <div class="player-box">
            <button class="btn-play" id="playBtn">▶ LIGAR SOM</button>
            <div id="statusText" class="status">PRONTO PARA CONECTAR</div>
            
            <div class="visualizer" id="viz">
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
            </div>
        </div>
    </div>

    <script>
        // URLs alternativas de contorno (Estratégia de stream handler independente)
        const streamUrls = [
            "https://corsproxy.io/?https://icecast.somossistemas.com.br/proxy/nels1rocks?mp=/stream",
            "https://icecast.somossistemas.com.br/proxy/nels1rocks?mp=/stream/;"
        ];

        let audio = null;
        let currentUrlIndex = 0;
        const playBtn = document.getElementById('playBtn');
        const statusText = document.getElementById('statusText');
        const viz = document.getElementById('viz');

        function initAudio() {
            if (audio) {
                audio.pause();
                audio = null;
            }

            statusText.textContent = "CONECTANDO AO SERVIDOR...";
            audio = new Audio(streamUrls[currentUrlIndex]);
            audio.crossOrigin = "anonymous";

            audio.addEventListener('playing', () => {
                statusText.textContent = "🔴 AO VIVO NO AR";
                playBtn.textContent = "⏸ DESLIGAR";
                playBtn.classList.add('playing');
                viz.classList.add('playing');
            });

            audio.addEventListener('waiting', () => {
                statusText.textContent = "⏳ BUFFERIZANDO...";
            });

            audio.addEventListener('error', (e) => {
                console.warn("Tentativa falhou, alternando rota...", e);
                currentUrlIndex++;
                if (currentUrlIndex < streamUrls.length) {
                    initAudio();
                    audio.play().catch(() => {});
                } else {
                    statusText.textContent = "⚠️ ERRO: SERVIDOR BLOQUEADO";
                    playBtn.textContent = "▶ TENTAR NOVAMENTE";
                    playBtn.classList.remove('playing');
                    viz.classList.remove('playing');
                }
            });
        }

        playBtn.addEventListener('click', () => {
            if (!audio || audio.paused) {
                initAudio();
                audio.play().catch(err => {
                    statusText.textContent = "⚠️ TOQUE NOVAMENTE PARA LIBERAR";
                    console.error(err);
                });
            } else {
                audio.pause();
                audio.currentTime = 0;
                playBtn.textContent = "▶ LIGAR SOM";
                playBtn.classList.remove('playing');
                viz.classList.remove('playing');
                statusText.textContent = "ESTÚDIO PAUSADO";
            }
        });
    </script>
</body>
</html>
