<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks Radio - Heavy Metal</title>
    <!-- Importação das fontes Google -->
    <link rel="preconnect" href="https://googleapis.com">
    <link rel="preconnect" href="https://gstatic.com" crossorigin>
    <link href="https://googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;600;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-deep: #0a0a0c;
            --bg-card: #121216;
            --bg-hover: #1c1c24;
            --text-main: #f0f0f5;
            --text-muted: #8a8a9e;
            --border: #262633;
            --border-active: #e50914;
            --accent: #e50914;
            --accent-glow: rgba(229, 9, 20, 0.25);
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
        }

        .app-container {
            width: 100%;
            max-width: 440px;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 24px 60px rgba(0, 0, 0, 0.8), 0 0 40px var(--accent-glow);
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 12px;
            border-bottom: 1px solid var(--border);
        }

        .brand {
            font-family: 'JetBrains Mono', monospace;
            font-size: 1.2rem;
            font-weight: 700;
        }

        .brand span { 
            color: var(--accent); 
        }

        .live-badge {
            display: flex;
            align-items: center;
            gap: 6px;
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.65rem;
            background: rgba(229, 9, 20, 0.1);
            color: var(--accent);
            padding: 5px 10px;
            border-radius: 20px;
            border: 1px solid var(--accent);
        }

        .player-content {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
            margin-top: 10px;
        }

        .cover-art {
            width: 200px;
            height: 200px;
            background: linear-gradient(135deg, #1e1e24 0%, #0a0a0c 100%);
            border: 2px solid var(--border);
            border-radius: 12px;
            margin-bottom: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 3rem;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
        }

        .track-info {
            margin-bottom: 25px;
        }

        .track-title {
            font-size: 1.3rem;
            font-weight: 700;
            margin-bottom: 6px;
        }

        .track-artist {
            color: var(--text-muted);
            font-size: 0.95rem;
        }

        .controls {
            display: flex;
            align-items: center;
            gap: 20px;
            margin-bottom: 20px;
        }

        .play-btn {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            background: var(--accent);
            border: none;
            color: white;
            font-size: 1.5rem;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: transform 0.2s, box-shadow 0.2s;
            box-shadow: 0 0 15px var(--accent-glow);
        }

        .play-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 25px var(--accent);
        }

        .volume-container {
            display: flex;
            align-items: center;
            gap: 10px;
            width: 100%;
            margin-top: 10px;
        }

        .volume-slider {
            flex: 1;
            -webkit-appearance: none;
            appearance: none;
            height: 6px;
            border-radius: 3px;
            background: var(--border);
            outline: none;
        }

        .volume-slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 14px;
            height: 14px;
            border-radius: 50%;
            background: var(--accent);
            cursor: pointer;
        }
    </style>
</head>
<body>

    <div class="app-container">
        <div class="header">
            <div class="brand">Nels1Rocks<span>.Radio</span></div>
            <div class="live-badge">⚡ NO AR</div>
        </div>

        <div class="player-content">
            <div class="cover-art">🤘</div>
            
            <div class="track-info">
                <div class="track-title">Heavy Metal Stream</div>
                <div class="track-artist">Nels1Rocks Playlist</div>
            </div>

            <!-- ADICIONE SUA STREAM DA ZENO AQUI SUBISTITUINDO ESTE LINK DE TESTE -->
            <audio id="radio-player" src="https://idobi.com"></audio>

            <div class="controls">
                <button class="play-btn" id="play-button">▶</button>
            </div>

            <div class="volume-container">
                <span>🔊</span>
                <input type="range" class="volume-slider" id="volume-control" min="0" max="1" step="0.05" value="0.8">
            </div>
        </div>
    </div>

    <script>
        const audio = document.getElementById('radio-player');
        const playBtn = document.getElementById('play-button');
        const volumeControl = document.getElementById('volume-control');

        audio.volume = volumeControl.value;

        playBtn.addEventListener('click', () => {
            if (audio.paused) {
                // Atualiza o elemento de mídia para evitar cache de links caídos
                audio.load(); 
                
                audio.play()
                    .then(() => {
                        playBtn.textContent = '⏸';
                    })
                    .catch(err => {
                        console.error("Erro capturado:", err);
                        alert("Não foi possível carregar a rádio. Verifique se a rádio está transmitindo ao vivo ou troque a URL no código.");
                    });
            } else {
                audio.pause();
                playBtn.textContent = '▶';
            }
        });

        volumeControl.addEventListener('input', (e) => {
            audio.volume = e.target.value;
        });
    </script>
</body>
</html>
