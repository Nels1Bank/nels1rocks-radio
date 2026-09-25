
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks Radio - Core Engine v3</title>
    <link href="https://fonts.googleapis.com/css2?family=Metal+Mania&family=Fira+Code:wght@400;700&display=swap" rel="stylesheet">
    <style>
        * { box-sizing: border-box; }
        body {
            margin: 0;
            background-color: #030105;
            color: #ffffff;
            font-family: 'Fira Code', monospace;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .radio-card {
            background: #0d0417;
            border: 4px solid #39ff14;
            box-shadow: 12px 12px 0px #000000, 0px 0px 20px rgba(57, 255, 20, 0.15);
            padding: 2rem;
            max-width: 480px;
            width: 100%;
            text-align: center;
        }

        .header-title {
            font-family: 'Metal Mania', cursive;
            font-size: 3.5rem;
            margin: 0;
            color: #ffffff;
            text-shadow: 3px 3px 0px #000, 6px 6px 0px #8a2be2;
            letter-spacing: 2px;
        }

        .tagline {
            font-size: 0.7rem;
            color: #39ff14;
            text-transform: uppercase;
            letter-spacing: 3px;
            margin: 8px 0 20px 0;
            font-weight: bold;
        }

        .control-group {
            margin-bottom: 15px;
            text-align: left;
        }

        .control-group label {
            font-size: 0.7rem;
            color: #bfaad1;
            font-weight: bold;
            display: block;
            margin-bottom: 6px;
            text-transform: uppercase;
        }

        select, input[type="range"] {
            width: 100%;
            background: #000;
            color: #39ff14;
            border: 2px solid #8a2be2;
            padding: 12px;
            font-family: 'Fira Code', monospace;
            font-weight: bold;
            font-size: 0.85rem;
            outline: none;
            cursor: pointer;
        }

        input[type="range"] {
            padding: 5px;
            accent-color: #39ff14;
        }

        .player-console {
            background: #000000;
            border: 3px solid #8a2be2;
            padding: 20px;
            margin-top: 15px;
        }

        /* Equalizador Gráfico */
        .eq-visualizer {
            display: flex;
            justify-content: center;
            align-items: flex-end;
            gap: 5px;
            height: 40px;
            margin-bottom: 15px;
        }

        .eq-bar {
            width: 6px;
            background: #39ff14;
            height: 6px;
        }

        .active-playback .eq-bar {
            animation: pulse-bar 0.5s infinite alternate ease-in-out;
        }

        .active-playback .eq-bar:nth-child(2) { animation-delay: 0.1s; }
        .active-playback .eq-bar:nth-child(3) { animation-delay: 0.3s; }
        .active-playback .eq-bar:nth-child(4) { animation-delay: 0.2s; }
        .active-playback .eq-bar:nth-child(5) { animation-delay: 0.4s; }
        .active-playback .eq-bar:nth-child(6) { animation-delay: 0.15s; }

        @keyframes pulse-bar {
            0% { height: 6px; background: #39ff14; }
            50% { height: 25px; background: #b1fc03; }
            100% { height: 38px; background: #ff3333; }
        }

        .btn-action {
            background: #39ff14;
            color: #000000;
            border: 3px solid #000;
            padding: 16px;
            font-family: 'Fira Code', monospace;
            font-weight: bold;
            font-size: 1rem;
            cursor: pointer;
            box-shadow: 4px 4px 0px #000;
            text-transform: uppercase;
            width: 100%;
            transition: all 0.1s ease;
        }

        .btn-action:hover { background: #4eff28; }
        .btn-action:active {
            box-shadow: 1px 1px 0px #000;
            transform: translate(3px, 3px);
        }

        .status-display {
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

    <div class="radio-card">
        <h1 class="header-title">Nels1Rocks</h1>
        <div class="tagline">Engine v3 // Secured Metal Streams</div>
        
        <div class="control-group">
            <label for="streamSelector">Selecione o Gênero:</label>
            <select id="streamSelector">
                <option value="https://stream.antenne.de/heavy-metal/stream/mp3">🔥 Heavy Metal / NWOBHM (Rock Antenne)</option>
                <option value="https://rautemusik-de-hz-fal-stream02.radiohost.de/hardrock">🎸 Hard Rock Classic (RauteMusic)</option>
                <option value="https://stream.schwarzwaldradio.com/schwarzwaldradio/mp3-192/stream.mp3">⚡ Rock & Melodic Arena (Schwarzwald)</option>
                <option value="https://s2.radio.co/s83713f83c/listen">💀 Thrash, Death & Extreme (Underground)</option>
            </select>
        </div>

        <div class="control-group">
            <label for="volumeSlider">Volume do Amplificador:</label>
            <input type="range" id="volumeSlider" min="0" max="1" step="0.05" value="0.8">
        </div>

        <div class="player-console">
            <!-- Elemento de Áudio Nativo Isolado -->
            <audio id="audioEngine" preload="none"></audio>

            <div class="eq-visualizer" id="eqVisualizer">
                <div class="eq-bar"></div>
                <div class="eq-bar"></div>
                <div class="eq-bar"></div>
                <div class="eq-bar"></div>
                <div class="eq-bar"></div>
                <div class="eq-bar"></div>
            </div>

            <div id="statusLabel" class="status-display">SISTEMA PRONTO</div>
            <button class="btn-action" id="powerBtn">▶ LIGAR SOM DA RÁDIO</button>
        </div>
    </div>

    <script>
        const audio = document.getElementById('audioEngine');
        const powerBtn = document.getElementById('powerBtn');
        const statusLabel = document.getElementById('statusLabel');
        const eqVisualizer = document.getElementById('eqVisualizer');
        const streamSelector = document.getElementById('streamSelector');
        const volumeSlider = document.getElementById('volumeSlider');

        let isRunning = false;

        // Configura volume inicial
        audio.volume = volumeSlider.value;

        volumeSlider.addEventListener('input', (e) => {
            audio.volume = e.target.value;
        });

        powerBtn.addEventListener('click', async () => {
            if (!isRunning) {
                await turnOnRadio();
            } else {
                turnOffRadio();
            }
        });

        streamSelector.addEventListener('change', async () => {
            if (isRunning) {
                turnOffRadio();
                await turnOnRadio();
            }
        });

        async function turnOnRadio() {
            try {
                statusLabel.textContent = "ESTABELECENDO CONEXÃO...";
                powerBtn.disabled = true;

                const url = streamSelector.value;
                // Injeta parâmetro único para evitar cache persistente do navegador
                audio.src = `${url}?ts=${Date.now()}`;
                audio.load();

                await audio.play();
                isRunning = true;

                powerBtn.textContent = "⏸ PARAR RÁDIO";
                powerBtn.style.background = "#ff3333";
                powerBtn.style.color = "#ffffff";
                statusLabel.textContent = "🔴 TRANSMITINDO AO VIVO!";
                eqVisualizer.classList.add('active-playback');
            } catch (err) {
                console.error("Erro ao tocar:", err);
                statusLabel.textContent = "⚠️ ERRO NO STREAM. TENTE OUTRO GÊNERO";
                turnOffRadio();
            } finally {
                powerBtn.disabled = false;
            }
        }

        function turnOffRadio() {
            audio.pause();
            audio.src = "";
            isRunning = false;

            powerBtn.textContent = "▶ LIGAR SOM DA RÁDIO";
            powerBtn.style.background = "#39ff14";
            powerBtn.style.color = "#000000";
            statusLabel.textContent = "TRANSMISSÃO INTERROMPIDA";
            eqVisualizer.classList.remove('active-playback');
        }

        audio.addEventListener('error', (e) => {
            console.error("Erro na tag de áudio:", e);
            if (isRunning) {
                statusLabel.textContent = "⚠️ QUEDA DE SINAL DETECTADA";
                turnOffRadio();
            }
        });
    </script>
</body>
</html>
