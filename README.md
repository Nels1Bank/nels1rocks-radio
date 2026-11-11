<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks Radio - Heavy Metal</title>
    <!-- Importação das fontes Google corrigidas -->
    <link rel="preconnect" href="https://googleapis.com">
    <link rel="preconnect" href="https://gstatic.com" crossorigin>
    <link href="https://googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;600;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-deep: #050507;
            --bg-card: #0d0d12;
            --bg-hover: #161622;
            --text-main: #f0f0f5;
            --text-muted: #62627a;
            --border: #1f1f2e;
            --border-hover: #33334d;
            --accent: #ff001c;
            --accent-glow: rgba(255, 0, 28, 0.2);
            --accent-gradient: linear-gradient(135deg, #ff001c 0%, #99000b 100%);
        }

        * { 
            box-sizing: border-box; 
            margin: 0; 
            padding: 0; 
        }

        body {
            background-color: var(--bg-deep);
            color: var(--text-main);
            font-family: 'Inter', sans-serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(255, 0, 28, 0.04) 0%, transparent 40%),
                radial-gradient(circle at 90% 80%, rgba(255, 0, 28, 0.03) 0%, transparent 40%);
        }

        .app-container {
            width: 100%;
            max-width: 400px;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 24px;
            padding: 28px;
            box-shadow: 0 30px 70px rgba(0, 0, 0, 0.85), 0 0 50px rgba(255, 0, 28, 0.05);
            transition: border-color 0.3s;
        }

        .app-container:hover {
            border-color: var(--border-hover);
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 28px;
            padding-bottom: 16px;
            border-bottom: 1px solid var(--border);
        }

        .brand {
            font-family: 'JetBrains Mono', monospace;
            font-size: 1.15rem;
            font-weight: 700;
            letter-spacing: -0.5px;
        }

        .brand span { 
            color: var(--accent);
            text-shadow: 0 0 12px var(--accent-glow);
        }

        .live-badge {
            display: flex;
            align-items: center;
            gap: 6px;
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.65rem;
            font-weight: 700;
            background: rgba(255, 0, 28, 0.08);
            color: var(--accent);
            padding: 6px 12px;
            border-radius: 20px;
            border: 1px solid rgba(255, 0, 28, 0.2);
            letter-spacing: 0.5px;
        }

        .live-dot {
            width: 6px;
            height: 6px;
            background-color: var(--accent);
            border-radius: 50%;
            animation: pulse 1.8s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(0.8); opacity: 0.5; box-shadow: 0 0 0 0 rgba(255, 0, 28, 0.7); }
            50% { transform: scale(1.2); opacity: 1; box-shadow: 0 0 0 4px rgba(255, 0, 28, 0); }
            100% { transform: scale(0.8); opacity: 0.5; box-shadow: 0 0 0 0 rgba(255, 0, 28, 0); }
        }

        .player-content {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
        }

        .cover-wrapper {
            position: relative;
            margin-bottom: 28px;
        }

        .cover-art {
            width: 220px;
            height: 220px;
            background: linear-gradient(145deg, #161622 0%, #08080c 100%);
            border: 1px solid var(--border);
            border-radius: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 3.5rem;
            box-shadow: 0 16px 36px rgba(0,0,0,0.6);
            transition: transform 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275), border-color 0.3s;
        }

        .app-container.playing .cover-art {
            transform: scale(1.03);
            border-color: rgba(255, 0, 28, 0.3);
            box-shadow: 0 20px 40px rgba(0,0,0,0.7), 0 0 30px var(--accent-glow);
        }

        .track-info {
            margin-bottom: 30px;
            width: 100%;
        }

        .track-title {
            font-size: 1.35rem;
            font-weight: 700;
            margin-bottom: 6px;
            letter-spacing: -0.3px;
        }

        .track-artist {
            color: var(--text-muted);
            font-size: 0.9rem;
            font-family: 'JetBrains Mono', monospace;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .controls {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 32px;
            width: 100%;
        }

        .play-btn {
            width: 76px;
            height: 76px;
            border-radius: 50%;
            background: var(--accent-gradient);
            border: none;
            color: white;
            font-size: 1.4rem;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: transform 0.2s, box-shadow 0.2s;
            box-shadow: 0 8px 24px rgba(255, 0, 28, 0.25);
        }

        .play-btn:hover {
            transform: scale(1.06);
            box-shadow: 0 12px 28px rgba(255, 0, 28, 0.4), 0 0 20px rgba(255, 0, 28, 0.2);
        }

        .play-btn:active {
            transform: scale(0.98);
        }

        .volume-container {
            display: flex;
            align-items: center;
            gap: 12px;
            width: 100%;
            background: rgba(255, 255, 255, 0.02);
            padding: 12px 16px;
            border-radius: 14px;
            border: 1px solid var(--border);
        }

        .volume-icon {
            font-size: 0.95rem;
            color: var(--text-muted);
            width: 20px;
            text-align: left;
            user-select: none;
        }

        .volume-slider {
            flex: 1;
            -webkit-appearance: none;
            appearance: none;
            height: 4px;
            border-radius: 2px;
            background: var(--border);
            outline: none;
            cursor: pointer;
            transition: background 0.2s;
        }

        .volume-container:hover .volume-slider {
            background: var(--border-hover);
        }

        .volume-slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: var(--text-main);
            transition: transform 0.15s, background-color 0.15s;
            box-shadow: 0 2px 6px rgba(0,0,0,0.5);
        }

        .volume-slider::-webkit-slider-thumb:hover {
            transform: scale(1.25);
            background: var(--accent);
        }
    </style>
</head>
<body>

    <div class="app-container" id="app-card">
        <div class="header">
            <div class="brand">Nels1Rocks<span>.Radio</span></div>
            <div class="live-badge">
                <div class="live-dot"></div>
                <span>LIVE</span>
            </div>
        </div>

        <div class="player-content">
            <div class="cover-wrapper">
                <div class="cover-art" id="visual-cover">🤘</div>
            </div>
            
            <div class="track-info">
                <div class="track-title">Heavy Metal Stream</div>
                <div class="track-artist">Heavy Metal</div>
            </div>

            <!-- Fluxo direto de áudio em MP3 ativo -->
            <audio id="radio-player" src="https://bestnetradio.com" crossorigin="anonymous"></audio>

            <div class="controls">
                <button class="play-btn" id="play-button" aria-label="Play">▶</button>
            </div>

            <div class="volume-container">
                <span class="volume-icon" id="volume-icon">🔊</span>
                <input type="range" class="volume-slider" id="volume-control" min="0" max="1" step="0.01" value="0.8">
            </div>
        </div>
    </div>

    <script>
        const audio = document.getElementById('radio-player');
        const playBtn = document.getElementById('play-button');
        const volumeControl = document.getElementById('volume-control');
        const volumeIcon = document.getElementById('volume-icon');
        const appCard = document.getElementById('app-card');
        const visualCover = document.getElementById('visual-cover');

        // Sincronização inicial de volume
        audio.volume = volumeControl.value;

        // Gerenciamento do Play/Pause
        playBtn.addEventListener('click', () => {
            if (audio.paused) {
                // Dá um rebuild no buffer para sincronizar ao vivo instantaneamente e limpar travas antigas
                audio.load(); 
                
                audio.play()
                    .then(() => {
                        playBtn.textContent = '⏸';
                        appCard.classList.add('playing');
                        visualCover.textContent = '🔥';
                    })
                    .catch(err => {
                        console.error("Erro na execução do streaming:", err);
