
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
            background: rgba(18, 22, 36, 0.8);
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
            padding: 22px;
            margin-top: 25px;
        }

        /* Player nativo customizado com bordas totalmente arredondadas */
        audio {
            width: 100%;
            margin-top: 10px;
            border-radius: 12px;
            accent-color: #00ffcc;
        }

        .status-text {
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.75rem;
            color: #00ffcc;
            margin-top: 14px;
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
            <div class="radio-tag">// Cyber-Glass Secure Stream</div>
        </div>

        <div class="control-group">
            <label for="streamSelect">Selecione o Canal de Áudio:</label>
            <select id="streamSelect">
                <!-- Links públicos e diretos validados com HTTPS -->
                <option value="https://stream.zeno.fm/f3wvbb757fhvv">🔥 Zeno FM - Heavy & Rock Channel</option>
                <option value="https://radios.justradio.com/stream/8002">🎸 Just Radio - Rock Classics</option>
            </select>
        </div>

        <div class="player-box">
            <!-- Player nativo do navegador tratado com link direto -->
            <audio id="nativeAudio" controls preload="none">
                <source src="https://stream.zeno.fm/f3wvbb757fhvv" type="audio/mpeg">
                Seu navegador não suporta o elemento de áudio.
            </audio>

            <div id="statusLabel" class="status-text">CLIQUE NO PLAY PARA OUVIR 👆</div>
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
            statusLabel.textContent = "🔴 CONECTANDO AO CANAL...";
        });

        audio.addEventListener('playing', () => {
            statusLabel.textContent = "🔴 TRANSMITINDO AO VIVO";
        });

        audio.addEventListener('error', () => {
            statusLabel.textContent = "⚠️ ERRO DE FLUXO. CLIQUE NO PLAY";
        });
    </script>
</body>
</html>
