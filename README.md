
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Radio // Cyber-Glass Edition</title>
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@400;600;800&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        * { box-sizing: border-box; }
        body {
            margin: 0;
            background: linear-gradient(135deg, #0d0f18 0%, #05060a 100%);
            color: #00ffcc;
            font-family: 'Outfit', sans-serif;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .radio-card {
            background: rgba(18, 22, 36, 0.7);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(0, 255, 204, 0.2);
            border-radius: 28px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.6), inset 0 1px 0 rgba(255, 255, 255, 0.1);
            padding: 35px;
            max-width: 440px;
            width: 100%;
            text-align: center;
        }

        .radio-header h1 {
            font-family: 'JetBrains Mono', monospace;
            font-size: 2.2rem;
            margin: 0 0 5px 0;
            color: #ffffff;
            letter-spacing: -1px;
        }

        .radio-header h1 span {
            color: #00ffcc;
        }

        .radio-tag {
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.7rem;
            color: #8b9bb4;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 25px;
            font-weight: 600;
        }

        .control-group {
            margin-bottom: 20px;
            text-align: left;
        }

        .control-group label {
            display: block;
            font-size: 0.75rem;
            color: #8b9bb4;
            font-weight: 600;
            margin-bottom: 8px;
            text-transform: uppercase;
            font-family: 'JetBrains Mono', monospace;
        }

        select, input[type="range"] {
            width: 100%;
            background: rgba(10, 13, 22, 0.9);
            color: #ffffff;
            border: 1px solid rgba(0, 255, 204, 0.3);
            border-radius: 14px;
            padding: 14px;
            font-family: 'Outfit', sans-serif;
            font-size: 0.95rem;
            outline: none;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        select:hover, select:focus {
            border-color: #00ffcc;
            box-shadow: 0 0 12px rgba(0, 255, 204, 0.2);
        }

        input[type="range"] {
            padding: 8px;
            accent-color: #00ffcc;
        }

        .visualizer-box {
            background: rgba(5, 7, 12, 0.8);
            border: 1px solid rgba(255, 255, 255, 0.05);
            border-radius: 18px;
            padding: 20px;
            margin-top: 20px;
        }

        .bars-container {
            display: flex;
            justify-content: center;
            align-items: flex-end;
            gap: 6px;
            height: 35px;
            margin-bottom: 15px;
        }

        .bar {
            width: 5px;
            background: #8b9bb4;
            border-radius: 3px;
            height: 6px;
            transition: height 0.2s;
        }

        .playing .bar {
            animation: wave 0.5s infinite alternate ease-in-out;
        }

        .playing .bar:nth-child(2) { animation-delay: 0.1s; }
        .playing .bar:nth-child(3) { animation-delay: 0.3s; }
        .playing .bar:nth-child(4) { animation-delay: 0.15s; }
        .playing .bar:nth-child(5) { animation-delay: 0.25s; }

        @keyframes wave {
            0% { height: 6px; background: #00ffcc; }
            100% { height: 30px; background: #ff007f; }
        }

        .status-text {
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.75rem;
            color: #8b9bb4;
            margin-bottom: 15px;
            letter-spacing: 1px;
            text-transform: uppercase;
        }

        .btn-action {
            background: #00ffcc;
            color: #05060a;
            border: none;
            border-radius: 14px;
            padding: 16px;
            font-family: 'JetBrains Mono', monospace;
            font-weight: 700;
            font-size: 1rem;
            cursor: pointer;
            width: 100%;
            letter-spacing: 0.5px;
            transition: all 0.2s ease;
            box-shadow: 0 4px 20px rgba(0, 255, 204, 0.3);
        }

        .btn-action:hover {
            background: #00cca3;
            transform: translateY(-2px);
            box-shadow: 0 6px 25px rgba(0, 255, 204, 0.4);
        }

        .btn-action:active {
            transform: translateY(0);
        }
    </style>
</head>
<body>

    <div class="radio-card">
        <div class="radio-header">
            <h1>Nels1<span>Rocks</span></h1>
            <div class="radio-tag">// Cyber-Glass Stream Interface</div>
        </div>

        <div class="control-group">
            <label for="streamSelect">Selecione o Fluxo:</label>
            <select id="streamSelect">
                <!-- Links diretos verificados em HTTPS puro -->
                <option value="https://ia801509.us.archive.org/29/items/free-heavy-metal-music-archive/Heavy%20Metal%20Sample.mp3">🔥 Heavy Metal Archive (CDN Estável)</option>
                <option value="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3">🎸 Rock Instrumental Showcase</option>
                <option value="https://streaming.exclusive.radio/er/heavyrock/icecast.audio">⚡ Exclusive Heavy Rock Stream</option>
            </select>
        </div>

        <div class="control-group">
            <label for="volumeSlider">Volume Master:</label>
            <input type="range" id="volumeSlider" min="0" max="1" step="0.05" value="0.8">
        </div>

        <div class="visualizer-box">
            <audio id="audioEngine" preload="auto"></audio>

            <div class="bars-container" id="barsContainer">
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
            </div>

            <div id="statusLabel" class="status-text">SISTEMA PRONTO</div>
            <button class="btn-action" id="powerBtn">▶ INICIAR TRANSMISSÃO</button>
        </div>
    </div>

    <script>
        const audio = document.getElementById('audioEngine');
        const powerBtn = document.getElementById('powerBtn');
        const statusLabel = document.getElementById('statusLabel');
        const barsContainer = document.getElementById('barsContainer');
        const streamSelect = document.getElementById('streamSelect');
        const volumeSlider = document.getElementById('volumeSlider');

        let active = false;
        audio.volume = volumeSlider.value;

        volumeSlider.addEventListener('input', (e) => {
            audio.volume = e.target.value;
        });

        powerBtn.addEventListener('click', () => {
            if (!active) {
                audio.src = streamSelect.value;
                audio.play().then(() => {
                    active = true;
                    powerBtn.textContent = "⏸ PARAR TRANSMISSÃO";
                    powerBtn.style.background = "#ff007f";
                    powerBtn.style.color = "#ffffff";
                    powerBtn.style.boxShadow = "0 4px 20px rgba(255, 0, 127, 0.3)";
                    statusLabel.textContent = "● AO VIVO NO AR";
                    barsContainer.classList.add('playing');
                }).catch(err => {
                    console.error(err);
                    statusLabel.textContent = "⚠️ CLIQUE NOVAMENTE";
                });
            } else {
                audio.pause();
                active = false;
                powerBtn.textContent = "▶ INICIAR TRANSMISSÃO";
                powerBtn.style.background = "#00ffcc";
                powerBtn.style.color = "#05060a";
                powerBtn.style.boxShadow = "0 4px 20px rgba(0, 255, 204, 0.3)";
                statusLabel.textContent = "SISTEMA PAUSADO";
                barsContainer.classList.remove('playing');
            }
        });

        streamSelect.addEventListener('change', () => {
            if (active) {
                audio.src = streamSelect.value;
                audio.play();
            }
        });

        audio.addEventListener('ended', () => {
            if (active) {
                audio.currentTime = 0;
                audio.play();
            }
        });
    </script>
</body>
</html>
