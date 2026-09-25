
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

        select, input[type="range"] {
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

        input[type="range"] {
            padding: 5px;
            accent-color: #39ff14;
        }

        .audio-console {
            background: #000000;
            border: 3px solid #8a2be2;
            padding: 20px;
            margin-top: 15px;
            box-shadow: inset 0 0 10px rgba(138, 43, 226, 0.4);
        }

        /* VU Meter / Equalizador Estilizado */
        .vu-container {
            display: flex;
            justify-content: center;
            align-items: flex-end;
            gap: 5px;
            height: 40px;
            margin-bottom: 15px;
        }

        .vu-bar {
            width: 6px;
            background: #39ff14;
            height: 6px;
        }

        .streaming .vu-bar {
            animation: freq-pulse 0.4s infinite alternate ease-in-out;
        }

        .streaming .vu-bar:nth-child(2) { animation-delay: 0.1s; }
        .streaming .vu-bar:nth-child(3) { animation-delay: 0.3s; }
        .streaming .vu-bar:nth-child(4) { animation-delay: 0.15s; }
        .streaming .vu-bar:nth-child(5) { animation-delay: 0.25s; }
        .streaming .vu-bar:nth-child(6) { animation-delay: 0.05s; }

        @keyframes freq-pulse {
            0% { height: 6px; background: #39ff14; }
            50% { height: 22px; background: #b1fc03; }
            100% { height: 38px; background: #ff0055; }
        }

        .btn-stream {
            background: #39ff14;
            color: #000000;
            border: 3px solid #000;
            padding: 16px;
            font-family: 'Share Tech Mono', monospace;
            font-weight: bold;
            font-size: 1.1rem;
            cursor: pointer;
            box-shadow: 4px 4px 0px #000;
            text-transform: uppercase;
            width: 100%;
            transition: all 0.08s ease;
        }

        .btn-stream:hover { background: #b1fc03; }
        .btn-stream:active {
            box-shadow: 1px 1px 0px #000;
            transform: translate(3px, 3px);
        }

        .status-screen {
            font-size: 0.75rem;
            color: #bfaad1;
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
            <label for="metalStreamSelect">Selecione a Frequência / Gênero:</label>
            <select id="metalStreamSelect">
                <option value="https://stream.antenne.de/heavy-metal/stream/mp3">🔥 Heavy Metal / NWOBHM (Rock Antenne)</option>
                <option value="https://rautemusik-de-hz-fal-stream02.radiohost.de/hardrock">🎸 Hard Rock Arena (RauteMusic)</option>
                <option value="https://stream.schwarzwaldradio.com/schwarzwaldradio/mp3-192/stream.mp3">⚡ Rock Clássico & Alternativo (Schwarzwald)</option>
                <option value="https://s2.radio.co/s83713f83c/listen">💀 Extreme Metal & Thrash (Underground Channel)</option>
            </select>
        </div>

        <div class="panel-section">
            <label for="gainSlider">Ganho do Amplificador (Volume):</label>
            <input type="range" id="gainSlider" min="0" max="1" step="0.05" value="0.85">
        </div>

        <div class="audio-console">
            <!-- Tag de áudio limpa sem source estática -->
            <audio id="globalAudioPlayer" preload="none"></audio>

            <div class="vu-container" id="vuMeter">
                <div class="vu-bar"></div>
                <div class="vu-bar"></div>
                <div class="vu-bar"></div>
                <div class="vu-bar"></div>
                <div class="vu-bar"></div>
                <div class="vu-bar"></div>
            </div>

            <div id="statusConsole" class="status-screen">SISTEMA EM ESPERA</div>
            <button class="btn-stream" id="togglePowerBtn">▶ LIGAR SOM DA RÁDIO</button>
        </div>
    </div>

    <script>
        const audio = document.getElementById('globalAudioPlayer');
        const togglePowerBtn = document.getElementById('togglePowerBtn');
        const statusConsole = document.getElementById('statusConsole');
        const vuMeter = document.getElementById('vuMeter');
        const metalStreamSelect = document.getElementById('metalStreamSelect');
        const gainSlider = document.getElementById('gainSlider');

        let isLive = false;

        // Configura volume inicial
        audio.volume = gainSlider.value;

        gainSlider.addEventListener('input', (e) => {
            audio.volume = e.target.value;
        });

        togglePowerBtn.addEventListener('click', async () => {
            if (!isLive) {
                await activateRadio();
            } else {
                deactivateRadio(true);
            }
        });

        metalStreamSelect.addEventListener('change', async () => {
            if (isLive) {
                deactivateRadio(false);
                await activateRadio();
            }
        });

        async function activateRadio() {
            try {
                statusConsole.textContent = "INICIALIZANDO STREAM SEGURO...";
                togglePowerBtn.disabled = true;

                const streamUrl = metalStreamSelect.value;
                // Injeta parâmetro dinâmico para zerar o cache do navegador
                audio.src = `${streamUrl}${streamUrl.includes('?') ? '&' : '?'}_t=${Date.now()}`;
                audio.load();

                await audio.play();
                isLive = true;

                togglePowerBtn.textContent = "⏸ PARAR RÁDIO";
                togglePowerBtn.style.background = "#ff0055";
                togglePowerBtn.style.color = "#ffffff";
                statusConsole.textContent = "🔴 AO VIVO NO AR!";
                vuMeter.classList.add('streaming');
            } catch (err) {
                console.error("Erro na ativação:", err);
                statusConsole.textContent = "⚠️ FALHA DE CONEXÃO. TENTE OUTRO CANAL";
                deactivateRadio(false);
            } finally {
                togglePowerBtn.disabled = false;
            }
        }

        function deactivateRadio(manual = false) {
            audio.pause();
            audio.src = "";
            isLive = false;

            togglePowerBtn.textContent = "▶ LIGAR SOM DA RÁDIO";
            togglePowerBtn.style.background = "#39ff14";
            togglePowerBtn.style.color = "#000000";
            vuMeter.classList.remove('streaming');
            
            if (manual) {
                statusConsole.textContent = "TRANSMISSÃO INTERROMPIDA";
            }
        }

        audio.addEventListener('error', (e) => {
            console.error("Erro no fluxo de áudio:", e);
            if (isLive) {
                statusConsole.textContent = "⚠️ QUEDA DE SINAL DETECTADA";
                deactivateRadio(false);
            }
        });
    </script>
</body>
</html>
