
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
            background: rgba(18, 22, 36, 0.85);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(0, 255, 204, 0.3);
            border-radius: 32px;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.8), inset 0 1px 0 rgba(255, 255, 255, 0.15);
            padding: 40px;
            max-width: 440px;
            width: 100%;
            text-align: center;
        }

        .radio-header h1 {
            font-family: 'JetBrains Mono', monospace;
            font-size: 2.4rem;
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

        select {
            width: 100%;
            background: rgba(10, 13, 22, 0.95);
            color: #ffffff;
            border: 1px solid rgba(0, 255, 204, 0.4);
            border-radius: 16px;
            padding: 16px;
            font-family: 'Outfit', sans-serif;
            font-size: 0.95rem;
            outline: none;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        select:hover, select:focus {
            border-color: #00ffcc;
            box-shadow: 0 0 15px rgba(0, 255, 204, 0.25);
        }

        .player-box {
            background: rgba(5, 7, 12, 0.95);
            border: 1px solid rgba(0, 255, 204, 0.25);
            border-radius: 20px;
            padding: 24px;
            margin-top: 25px;
        }

        .btn-play {
            background: #00ffcc;
            color: #05060a;
            border: none;
            border-radius: 16px;
            padding: 16px;
            font-family: 'JetBrains Mono', monospace;
            font-weight: 700;
            font-size: 1rem;
            cursor: pointer;
            width: 100%;
            letter-spacing: 1px;
            transition: all 0.2s ease;
            box-shadow: 0 4px 20px rgba(0, 255, 204, 0.3);
            text-transform: uppercase;
        }

        .btn-play:hover {
            background: #00cca3;
            transform: translateY(-2px);
            box-shadow: 0 6px 25px rgba(0, 255, 204, 0.4);
        }

        .status-text {
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.75rem;
            color: #8b9bb4;
            margin-top: 15px;
            letter-spacing: 1.5px;
            text-transform: uppercase;
            font-weight: 700;
        }
    </style>
</head>
<body>

    <div class="radio-card">
        <div class="radio-header">
            <h1>Nels1<span>Rocks</span></h1>
            <div class="radio-tag">// Cyber-Glass Station</div>
        </div>

        <div class="control-group">
            <label for="trackSelect">Selecione o Canal:</label>
            <select id="trackSelect">
                <!-- Links diretos garantidos e livres de bloqueio CORS -->
                <option value="https://www.w3schools.com/html/horse.mp3">🔥 Canal 1 - Teste de Áudio Oficial (W3C)</option>
                <option value="https://actions.google.com/sounds/v1/ambiences/rain_heavy.ogg">⚡ Canal 2 - Chuva Cyberpunk (Google API)</option>
            </select>
        </div>

        <div class="player-box">
            <audio id="audioPlayer" preload="auto"></audio>
            <button class="btn-play" id="playBtn">▶ LIGAR SOM</button>
            <div id="statusLabel" class="status-text">SISTEMA EM ESPERA</div>
        </div>
    </div>

    <script>
        const audio = document.getElementById('audioPlayer');
        const playBtn = document.getElementById('playBtn');
        const trackSelect = document.getElementById('trackSelect');
        const statusLabel = document.getElementById('statusLabel');

        let isPlaying = false;

        playBtn.addEventListener('click', () => {
            if (!isPlaying) {
                audio.src = trackSelect.value;
                audio.play().then(() => {
                    isPlaying = true;
                    playBtn.textContent = "⏸ PARAR SOM";
                    playBtn.style.background = "#ff007f";
                    playBtn.style.boxShadow = "0 4px 20px rgba(255, 0, 127, 0.3)";
                    statusLabel.textContent = "● TOCANDO AO VIVO";
                }).catch(err => {
                    console.error(err);
                    statusLabel.textContent = "⚠️ CLIQUE NOVAMENTE NO BOTÃO";
                });
            } else {
                audio.pause();
                isPlaying = false;
                playBtn.textContent = "▶ LIGAR SOM";
                playBtn.style.background = "#00ffcc";
                playBtn.style.boxShadow = "0 4px 20px rgba(0, 255, 204, 0.3)";
                statusLabel.textContent = "SISTEMA PAUSADO";
            }
        });

        trackSelect.addEventListener('change', () => {
            if (isPlaying) {
                audio.src = trackSelect.value;
                audio.play().catch(() => {});
            }
        });

        audio.addEventListener('ended', () => {
            if (isPlaying) {
                audio.currentTime = 0;
                audio.play().catch(() => {});
            }
        });
    </script>
</body>
</html>
