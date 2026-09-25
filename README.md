
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks Radio</title>
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
        }

        .container {
            background: #10061d;
            border: 4px solid #000;
            box-shadow: 8px 8px 0px #000;
            padding: 2rem;
            text-align: center;
            max-width: 480px;
            width: 100%;
        }

        h1 {
            font-family: 'Metal Mania', cursive;
            font-size: 3.2rem;
            margin: 0;
            color: #fff;
            text-shadow: 3px 3px 0px #000, 6px 6px 0px #8a2be2;
        }

        .subtitle {
            font-size: 0.75rem;
            color: #39ff14;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin: 10px 0 20px 0;
            font-weight: bold;
        }

        .player-box {
            background: #000000;
            border: 3px solid #8a2be2;
            padding: 20px;
        }

        .btn-live {
            background: #39ff14;
            color: #000;
            border: 3px solid #000;
            padding: 16px;
            font-family: 'Fira Code', monospace;
            font-weight: bold;
            font-size: 1.1rem;
            cursor: pointer;
            box-shadow: 4px 4px 0px #000;
            text-transform: uppercase;
            width: 100%;
            margin-top: 15px;
            transition: transform 0.1s, box-shadow 0.1s;
        }

        .btn-live:active {
            box-shadow: 1px 1px 0px #000;
            transform: translate(3px, 3px);
        }

        .status {
            font-size: 0.8rem;
            color: #bfaad1;
            margin-top: 15px;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Nels1Rocks</h1>
        <div class="subtitle">Heavy Metal 24/7 (HTTPS Secure)</div>
        
        <div class="player-box">
            <!-- Elemento de áudio sem source estática para controle total via JS -->
            <audio id="radioStream" preload="none"></audio>

            <div id="statusText" class="status">PRONTO PARA CONECTAR AO AR</div>
            <button class="btn-live" id="playBtn">▶ LIGAR SOM DA RÁDIO</button>
        </div>
    </div>

    <script>
        const audio = document.getElementById('radioStream');
        const playBtn = document.getElementById('playBtn');
        const statusText = document.getElementById('statusText');
        
        const baseUrl = "https://stream.rockantenne.de/heavy-metal/stream/mp3";
        let isPlaying = false;
        let reconnectTimeout = null;

        playBtn.addEventListener('click', async () => {
            if (!isPlaying) {
                await startRadio();
            } else {
                stopRadio(true);
            }
        });

        async function startRadio() {
            try {
                statusText.textContent = "CONECTANDO AO SERVIDOR SEGURO...";
                playBtn.disabled = true;

                // Adiciona timestamp para burlar cache de rede travado
                audio.src = `${baseUrl}?cb=${new Date().getTime()}`;
                audio.load();

                await audio.play();
                isPlaying = true;
                playBtn.textContent = "⏸ PARAR RÁDIO";
                playBtn.style.background = "#ff3333";
                playBtn.style.color = "#fff";
                statusText.textContent = "🔴 AO VIVO NO AR!";
            } catch (error) {
                console.error("Erro na reprodução:", error);
                statusText.textContent = "⚠️ ERRO DE SINAL. TENTANDO DE NOVO...";
                scheduleReconnect();
            } finally {
                playBtn.disabled = false;
            }
        }

        function stopRadio(userManual = false) {
            if (reconnectTimeout) clearTimeout(reconnectTimeout);
            audio.pause();
            audio.src = "";
            isPlaying = false;
            
            playBtn.textContent = "▶ LIGAR SOM DA RÁDIO";
            playBtn.style.background = "#39ff14";
            playBtn.style.color = "#000";
            
            if (userManual) {
                statusText.textContent = "TRANSMISSÃO PAUSADA";
            }
        }

        function scheduleReconnect() {
            if (!isPlaying) return;
            statusText.textContent = "🔄 RECONECTANDO AUTOMATICAMENTE...";
            if (reconnectTimeout) clearTimeout(reconnectTimeout);
            
            reconnectTimeout = setTimeout(() => {
                if (isPlaying) {
                    startRadio();
                }
            }, 3000); // Tenta reconectar após 3 segundos
        }

        // Eventos nativos de monitoramento de fluxo
        audio.addEventListener('stalled', () => {
            if (isPlaying) {
                statusText.textContent = "⚠️ SINAL ENGASGADO. RECUPERANDO...";
            }
        });

        audio.addEventListener('waiting', () => {
            if (isPlaying) {
                statusText.textContent = "⏳ AGUARDANDO BUFFER DO METAL...";
            }
        });

        audio.addEventListener('playing', () => {
            statusText.textContent = "🔴 AO VIVO NO AR!";
        });

        audio.addEventListener('error', (e) => {
            console.error("Erro de sinal disparado pelo stream:", e);
            if (isPlaying) {
                scheduleReconnect();
            }
        });
    </script>
</body>
</html>
