
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
            font-size: 2.8rem;
            margin: 0 0 10px 0;
            text-shadow: 3px 3px 0px #000, 6px 6px 0px #8a2be2;
        }
        p {
            color: #bfaad1;
            font-size: 0.8rem;
            margin-bottom: 1.5rem;
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
            gap: 12px;
        }
        .btn {
            background: #39ff14;
            color: #000;
            border: 3px solid #000;
            padding: 12px 20px;
            font-family: 'Fira Code', monospace;
            font-weight: bold;
            font-size: 1rem;
            cursor: pointer;
            box-shadow: 4px 4px 0px #000;
            text-transform: uppercase;
            width: 100%;
        }
        .btn:active {
            box-shadow: 1px 1px 0px #000;
            transform: translate(3px, 3px);
        }
        .btn-alt {
            background: #8a2be2;
            color: #fff;
        }
        .status {
            font-size: 0.75rem;
            color: #39ff14;
            font-weight: bold;
            word-break: break-all;
            background: #111;
            padding: 8px;
            width: 100%;
            border: 1px dashed #444;
        }
    </style>
</head>
<body>

    <div class="card">
        <h1>Nels1Rocks</h1>
        <p>Heavy Metal & Rock Stream</p>
        
        <div class="player-box">
            <button class="btn" id="playNels1">▶ OUVIR NELS1ROCKS</button>
            <button class="btn btn-alt" id="playTest">▶ TESTAR OUTRA RÁDIO (ROCK)</button>
            <div id="statusText" class="status">PRONTO</div>
        </div>
    </div>

    <script>
        const statusText = document.getElementById('statusText');
        let currentAudio = null;

        function playStream(url, name) {
            if (currentAudio) {
                currentAudio.pause();
                currentAudio = null;
            }

            statusText.textContent = `Conectando em ${name}...`;
            currentAudio = new Audio(url);
            currentAudio.crossOrigin = "anonymous";

            currentAudio.addEventListener('playing', () => {
                statusText.textContent = `🔴 ${name}: AO VIVO!`;
            });

            currentAudio.addEventListener('waiting', () => {
                statusText.textContent = `⏳ ${name}: Bufferizando dados...`;
            });

            currentAudio.addEventListener('error', (e) => {
                statusText.textContent = `❌ ${name}: Servidor Offline ou Bloqueado.`;
                console.error(e);
            });

            currentAudio.play().catch(err => {
                statusText.textContent = `⚠️ Toque novamente para liberar o áudio.`;
                console.error(err);
            });
        }

        // Botão 1: O seu servidor oficial
        document.getElementById('playNels1').addEventListener('click', () => {
            playStream("https://icecast.somossistemas.com.br/proxy/nels1rocks?mp=/stream", "Nels1Rocks");
        });

        // Botão 2: Stream de teste público mundial (Guitarix/Rock Stream) para provar que o player funciona
        document.getElementById('playTest').addEventListener('click', () => {
            playStream("https://rautemusik-de-hz-fal-stream13.radiohost.de/hardrock_mp3_192", "Rádio Teste Rock");
        });
    </script>
</body>
</html>
