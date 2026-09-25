
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks // Cyber-Metal Radio</title>
    <link href="https://fonts.googleapis.com/css2?family=Metal+Mania&family=Share+Tech+Mono&display=swap" rel="stylesheet">
    <style>
        * { box-sizing: border-box; }
        body {
            margin: 0;
            background-color: #020104;
            color: #39ff14;
            font-family: 'Share Tech Mono', monospace;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .terminal-box {
            background: #090310;
            border: 4px solid #39ff14;
            box-shadow: 12px 12px 0px #000000, 0px 0px 25px rgba(57, 255, 20, 0.2);
            padding: 2rem;
            max-width: 500px;
            width: 100%;
            text-align: center;
        }

        .logo-title {
            font-family: 'Metal Mania', cursive;
            font-size: 3.2rem;
            margin: 0;
            color: #ffffff;
            text-shadow: 3px 3px 0px #000, 5px 5px 0px #39ff14;
            letter-spacing: 2px;
        }

        .bank-tag {
            font-size: 0.65rem;
            color: #bfaad1;
            text-transform: uppercase;
            letter-spacing: 3px;
            margin: 5px 0 20px 0;
            font-weight: bold;
        }

        .panel-section {
            margin-bottom: 15px;
            text-align: left;
        }

        .panel-section label {
            font-size: 0.7rem;
            color: #39ff14;
            font-weight: bold;
            display: block;
            margin-bottom: 5px;
            text-transform: uppercase;
        }

        select {
            width: 100%;
            background: #000;
            color: #39ff14;
            border: 2px solid #39ff14;
            padding: 12px;
            font-family: 'Share Tech Mono', monospace;
            font-size: 0.9rem;
            outline: none;
            cursor: pointer;
        }

        .audio-console {
            background: #000000;
            border: 3px solid #8a2be2;
            padding: 20px;
            margin-top: 15px;
            box-shadow: inset 0 0 10px rgba(138, 43, 226, 0.4);
        }

        /* Player nativo estilizado para o Chrome não bloquear */
        audio {
            width: 100%;
            margin-top: 10px;
            accent-color: #39ff14;
            filter: invert(100%) hue-rotate(180deg) brightness(1.5);
        }

        .status-screen {
            font-size: 0.75rem;
            color: #39ff14;
            margin-top: 15px;
            font-weight: bold;
            letter-spacing: 1px;
            text-transform: uppercase;
        }
    </style>
</head>
<body>

    <div class="terminal-box">
        <h1 class="logo-title">Nels1Rocks</h1>
        <div class="bank-tag">// Nels1Bank Media Division // S1 Secure Stream</div>
        
        <div class="panel-section">
            <label for="metalStreamSelect">Selecione o Subgênero:</label>
            <select id="metalStreamSelect">
                <option value="https://stream.antenne.de/heavy-metal/stream/mp3">🔥 Heavy Metal / NWOBHM (Rock Antenne)</option>
                <option value="https://rautemusik-de-hz-fal-stream02.radiohost.de/hardrock">🎸 Hard Rock Arena (RauteMusic)</option>
                <option value="https://stream.schwarzwaldradio.com/schwarzwaldradio/mp3-192/stream.mp3">⚡ Rock Clássico & Alternativo (Schwarzwald)</option>
            </select>
        </div>

        <div class="audio-console">
            <!-- Player nativo visível para evitar qualquer bloqueio de script do Chrome -->
            <audio id="nativeAudio" controls preload="none">
                <source src="https://stream.antenne.de/heavy-metal/stream/mp3" type="audio/mpeg">
                Seu navegador não suporta áudio HTML5.
            </audio>

            <div id="statusConsole" class="status-screen">CLIQUE NO PLAY DO PLAYER ACIMA 👆</div>
        </div>
    </div>

    <script>
        const audio = document.getElementById('nativeAudio');
        const select = document.getElementById('metalStreamSelect');
        const statusConsole = document.getElementById('statusConsole');

        select.addEventListener('change', (e) => {
            audio.pause();
            audio.src = e.target.value;
            audio.load();
            audio.play().catch(err => console.log("Aguardando interação do usuário"));
            statusConsole.textContent = "🔴 TRANSMITINDO FREQUÊNCIA SELECIONADA";
        });

        audio.addEventListener('playing', () => {
            statusConsole.textContent = "🔴 AO VIVO NO AR!";
        });

        audio.addEventListener('error', () => {
            statusConsole.textContent = "⚠️ ERRO NO STREAM. TENTE OUTRA OPÇÃO";
        });
    </script>
</body>
</html>
