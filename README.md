
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks // True Heavy & Thrash Metal</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-deep: #050507;
            --bg-card: #0d0e12;
            --bg-hover: #161821;
            --accent: #e50914;
            --accent-glow: rgba(229, 9, 20, 0.25);
            --text-main: #f4f4f6;
            --text-muted: #8c92a4;
            --border: rgba(255, 255, 255, 0.08);
            --border-active: rgba(229, 9, 20, 0.5);
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }

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

        .brand span { color: var(--accent); }

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
            border: 1px solid var(--border-active);
            text-transform: uppercase;
        }

        .live-dot {
            width: 6px;
            height: 6px;
            background: var(--accent);
            border-radius: 50%;
            box-shadow: 0 0 8px var(--accent);
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.4; transform: scale(0.85); }
            100% { opacity: 1; transform: scale(1); }
        }

        .now-playing {
            background: rgba(0, 0, 0, 0.4);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 16px;
            text-align: center;
            margin-bottom: 20px;
        }

        .current-band {
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.7rem;
            color: var(--accent);
            text-transform: uppercase;
            letter-spacing: 1.5px;
            margin-bottom: 4px;
        }

        .current-title {
            font-size: 1.05rem;
            font-weight: 600;
            color: var(--text-main);
            margin-bottom: 14px;
        }

        audio {
            width: 100%;
            height: 40px;
            accent-color: var(--accent);
        }

        .playlist-section {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .section-title {
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.65rem;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 1.5px;
        }

        .playlist-list {
            max-height: 240px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 6px;
            padding-right: 4px;
        }

        .playlist-list::-webkit-scrollbar { width: 4px; }
        .playlist-list::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }

        .track-item {
            background: rgba(255, 255, 255, 0.015);
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 10px 12px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.2s ease;
        }

        .track-item:hover {
            background: var(--bg-hover);
            border-color: rgba(255, 255, 255, 0.15);
        }

        .track-item.active {
            background: rgba(229, 9, 20, 0.1);
            border-color: var(--border-active);
        }

        .track-info-mini {
            display: flex;
            flex-direction: column;
            gap: 2px;
        }

        .mini-band {
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.6rem;
            color: var(--text-muted);
            text-transform: uppercase;
        }

        .track-item.active .mini-band { color: var(--accent); }

        .mini-title {
            font-size: 0.85rem;
            font-weight: 500;
        }

        .play-icon {
            font-size: 0.75rem;
            color: var(--text-muted);
        }

        .track-item.active .play-icon { color: var(--accent); font-weight: bold; }
    </style>
</head>
<body>

<div class="app-container">
    <div class="header">
        <div class="brand">Nels1<span>Rocks</span></div>
        <div class="live-badge">
            <div class="live-dot"></div>
            HEAVY & THRASH METAL
        </div>
    </div>

    <div class="now-playing">
        <div class="current-band" id="activeBand">Carregando peso...</div>
        <div class="current-title" id="activeTitle">Selecione o canal abaixo</div>
        <audio id="audioPlayer" controls preload="auto"></audio>
    </div>

    <div class="playlist-section">
        <div class="section-title">// CANAIS HEAVY & THRASH METAL</div>
        <div class="playlist-list" id="playlistContainer"></div>
    </div>
</div>

<script>
    // Setlist 100% Heavy, Thrash e Extremo (Canais dedicados de alta estabilidade)
    const metalStreams = [
        { band: "Thrash & Extreme Channel", title: "Slayer, Kreator, Sepultura & Sodom Stream", url: "https://rautemusik-de-hz-fal-stream12.radiohost.de/metal/stream/mp3" },
        { band: "Heavy Metal Oldschool", title: "Iron Maiden, Black Sabbath & Judas Priest", url: "https://rautemusik-de-hz-fal-stream13.radiohost.de/heavyoldie/stream/mp3" },
        { band: "Hard & Heavy Station", title: "Megadeth, Pantera & Metallica Riffs", url: "https://stream.antenne.com/rock-hard/mp3-128/streams.antenne.com/" },
        { band: "Pure Metal Attack", title: "Blind Guardian & Power/Thrash Sound", url: "https://listen.radionomy.com/metal-express-radio.m3u" }
    ];

    let currentIndex = 0;
    const audio = document.getElementById('audioPlayer');
    const container = document.getElementById('playlistContainer');
    const activeBand = document.getElementById('activeBand');
    const activeTitle = document.getElementById('activeTitle');

    function renderList() {
        container.innerHTML = '';
        metalStreams.forEach((track, index) => {
            const item = document.createElement('div');
            item.className = `track-item ${index === currentIndex ? 'active' : ''}`;
            item.innerHTML = `
                <div class="track-info-mini">
                    <span class="mini-band">${track.band}</span>
                    <span class="mini-title">${track.title}</span>
                </div>
                <div class="play-icon">${index === currentIndex ? '▶ ON' : '•'}</div>
            `;
            item.onclick = () => {
                loadStream(index);
            };
            container.appendChild(item);
        });
    }

    function loadStream(index) {
        currentIndex = index;
        const track = metalStreams[currentIndex];
        audio.src = track.url;
        audio.load();
        audio.play().catch(e => console.log("Aguardando play manual"));
        activeBand.textContent = track.band;
        activeTitle.textContent = track.title;
        renderList();
    }

    audio.onerror = () => {
        activeTitle.textContent = "⚠️ RECONECTANDO STREAM PESADO...";
        setTimeout(() => {
            currentIndex = (currentIndex + 1) % metalStreams.length;
            loadStream(currentIndex);
        }, 2000);
    };

    renderList();
    loadStream(0);
</script>

</body>
</html>
