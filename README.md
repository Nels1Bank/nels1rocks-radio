
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks // Heavy Metal Radio</title>
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@400;600;700&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        * { box-sizing: border-box; }
        body {
            margin: 0;
            min-height: 100vh;
            background: #05060a;
            color: #fff;
            font-family: 'Outfit', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 15px;
        }
        .player-card {
            width: 100%;
            max-width: 400px;
            background: #0f131f;
            border: 1px solid rgba(255, 51, 102, 0.3);
            border-radius: 24px;
            padding: 25px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.8);
        }
        .header {
            text-align: center;
            margin-bottom: 20px;
        }
        .logo {
            font-family: 'JetBrains Mono', monospace;
            font-size: 1.8rem;
            font-weight: 700;
        }
        .logo span { color: #ff3366; }
        .tag {
            font-size: 0.65rem;
            color: #8190a8;
            font-family: 'JetBrains Mono', monospace;
            letter-spacing: 1px;
            text-transform: uppercase;
            margin-top: 5px;
        }
        .now-playing {
            text-align: center;
            margin-bottom: 20px;
            background: rgba(255, 255, 255, 0.03);
            padding: 15px;
            border-radius: 14px;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }
        .track-title {
            font-weight: 700;
            font-size: 1rem;
            margin-bottom: 4px;
        }
        .track-band {
            color: #ff3366;
            font-size: 0.75rem;
            font-family: 'JetBrains Mono', monospace;
            text-transform: uppercase;
        }
        .controls {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 15px;
            margin-bottom: 20px;
        }
        button {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 51, 102, 0.2);
            color: #fff;
            width: 45px;
            height: 45px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1rem;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: 0.2s;
        }
        button:hover {
            border-color: #ff3366;
            color: #ff3366;
            transform: scale(1.05);
        }
        button.play-btn {
            width: 60px;
            height: 60px;
            background: #ff3366;
            color: #05060a;
            border: none;
            font-size: 1.3rem;
            font-weight: bold;
        }
        button.play-btn:hover {
            background: #ff5580;
            color: #05060a;
        }
        .playlist {
            max-height: 200px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 6px;
        }
        .playlist::-webkit-scrollbar { width: 4px; }
        .playlist::-webkit-scrollbar-thumb { background: #ff3366; border-radius: 10px; }
        .playlist-item {
            background: rgba(255, 255, 255, 0.02);
            border: 1px solid transparent;
            padding: 10px 12px;
            border-radius: 10px;
            cursor: pointer;
            text-align: left;
            color: #fff;
            font-size: 0.85rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: 0.2s;
        }
        .playlist-item:hover {
            background: rgba(255, 51, 102, 0.08);
        }
        .playlist-item.active {
            border-color: #ff3366;
            background: rgba(255, 51, 102, 0.12);
        }
        .status {
            text-align: center;
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.65rem;
            color: #8190a8;
            margin-top: 15px;
            letter-spacing: 1px;
        }
    </style>
</head>
<body>

<div class="player-card">
    <div class="header">
        <div class="logo">Nels1<span>Rocks</span></div>
        <div class="tag">// Heavy Metal Radio Stream</div>
    </div>

    <div class="now-playing">
        <div class="track-title" id="trackTitle">Selecione uma estação</div>
        <div class="track-band" id="trackBand">Live Stream</div>
    </div>

    <audio id="audioPlayer"></audio>

    <div class="controls">
        <button id="prevBtn" title="Anterior">⏮</button>
        <button id="playBtn" class="play-btn" title="Play/Pause">▶</button>
        <button id="nextBtn" title="Próxima">⏭</button>
    </div>

    <div class="playlist" id="playlistContainer"></div>

    <div class="status" id="statusText">● PRONTO PARA CONECTAR</div>
</div>

<script>
    // Usando streams de rádio online dedicadas a Rock/Metal (Icecast/Shoutcast streams públicos)
    const tracks = [
        { title: "Classic Heavy Metal", band: "Hard Radio", url: "https://rautemusik-de-hz-fal-stream13.radiohost.de/heavy-metal" },
        { title: "Rock & Metal Anthems", band: "Rock Radio Stream", url: "https://stream.rockantenne.de/heavy-metal/stream/mp3,128" },
        { title: "Underground Metal Channel", band: "Metal Devastation", url: "https://radio.metaldevastationradio.com:8000/stream" },
        { title: "Pure Metal Stream", band: "Hard Rock Station", url: "https://live.hardsoundradio.com:8000/stream" }
    ];

    let currentIndex = 0;
    const audio = document.getElementById('audioPlayer');
    const playBtn = document.getElementById('playBtn');
    const prevBtn = document.getElementById('prevBtn');
    const nextBtn = document.getElementById('nextBtn');
    const trackTitle = document.getElementById('trackTitle');
    const trackBand = document.getElementById('trackBand');
    const playlistContainer = document.getElementById('playlistContainer');
    const statusText = document.getElementById('statusText');

    function initPlaylist() {
        playlistContainer.innerHTML = '';
        tracks.forEach((track, index) => {
            const item = document.createElement('div');
            item.className = `playlist-item ${index === currentIndex ? 'active' : ''}`;
            item.innerHTML = `<span>${track.band} - ${track.title}</span>`;
            item.onclick = () => {
                currentIndex = index;
                loadTrack(currentIndex);
                playAudio();
            };
            playlistContainer.appendChild(item);
        });
    }

    function loadTrack(index) {
        currentIndex = index;
        const track = tracks[currentIndex];
        audio.src = track.url;
        trackTitle.textContent = track.title;
        trackBand.textContent = track.band;
        initPlaylist();
    }

    function playAudio() {
        statusText.textContent = '● CONECTANDO AO STREAM...';
        audio.play().then(() => {
            playBtn.textContent = '⏸';
            statusText.textContent = '● AO VIVO';
        }).catch(err => {
            statusText.textContent = '⚠️ CLIQUE NO PLAY PARA CONECTAR';
        });
    }

    function pauseAudio() {
        audio.pause();
        playBtn.textContent = '▶';
        statusText.textContent = '⏸ PAUSADO';
    }

    playBtn.onclick = () => {
        if (audio.paused) {
            playAudio();
        } else {
            pauseAudio();
        }
    };

    nextBtn.onclick = () => {
        currentIndex = (currentIndex + 1) % tracks.length;
        loadTrack(currentIndex);
        playAudio();
    };

    prevBtn.onclick = () => {
        currentIndex = (currentIndex - 1 + tracks.length) % tracks.length;
        loadTrack(currentIndex);
        playAudio();
    };

    audio.onerror = () => {
        statusText.textContent = '⚠️ ERRO NA ESTAÇÃO, TENTE OUTRA';
    };

    // Inicializa na primeira estação
    loadTrack(0);
</script>

</body>
</html>
