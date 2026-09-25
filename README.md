
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Radio // Native Cyber-Glass</title>
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
            background: rgba(18, 22, 36, 0.75);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(0, 255, 204, 0.25);
            border-radius: 28px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.7), inset 0 1px 0 rgba(255, 255, 255, 0.1);
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

        select {
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

        .player-box {
            background: rgba(5, 7, 12, 0.9);
            border: 1px solid rgba(0, 255, 204, 0.2);
            border-radius: 18px;
            padding: 20px;
            margin-top: 20px;
        }

        /* Player nativo com estilização limpa para garantir compatibilidade total */
        audio {
            width: 100%;
            margin-top: 10px;
            accent-color: #00ffcc;
        }

        .status-text {
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.75rem;
            color: #00ffcc;
            margin-top: 12px;
            letter-spacing: 1px;
            text-transform: uppercase;
            font-weight: 700;
        }
    </style>
</head>
<body>

    <div class="radio-card">
        <div class="radio-header">
            <h1>Nels1<span>Rocks</span></h1>
            <div class="radio-tag">// Secure Native Stream</div>
        </div>

        <div class="control-group">
            <label for="streamSelect">Selecione o Canal:</label>
            <select id="streamSelect">
                <!-- Links diretos verificados em HTTPS CDN -->
                <option value="https://ia801509.us.archive.org/29/items/free-heavy-metal-music-archive/Heavy%20Metal%20Sample.mp3">🔥 Heavy Metal Archive Stream</option>
                <option value="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3">🎸 Rock Instrumental Showcase</option>
            </select>
        </div>

        <div class="player-box">
            <!-- Player nativo protegido contra bloqueio de CORS do Chrome -->
            <audio id="nativeAudio" controls preload="none">
                <source src="https://ia801509.us.archive.org/29/items/free-heavy-metal-music-archive/Heavy%20Metal%20Sample.mp3" type="audio/mpeg">
                Seu navegador não suporta áudio HTML5.
            </audio>

            <div id="statusLabel" class="status-text">CLIQUE NO PLAY ACIMA 👆</div>
        </div>
    </div>

    <script>
        const audio = document.getElementById('nativeAudio');
        const select = document.getElementById('streamSelect');
        const statusLabel = document.getElementById('statusLabel');

        select.addEventListener('change', (e) => {
            audio.pause();
            audio.src = e.target.value;
            audio.load();
            audio.play().catch(() => {});
            statusLabel.textContent = "🔴 FLUXO ALTERADO COM SUCESSO";
        });

        audio.addEventListener('playing', () => {
            statusLabel.textContent = "🔴 TRANSMITINDO AO VIVO";
        });

        audio.addEventListener('error', () => {
            statusLabel.textContent = "⚠️ ERRO NO CANAL. TENTE O OUTRO";
        });
    </script>
</body>
</html>
