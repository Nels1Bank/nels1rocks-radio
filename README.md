
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks // Heavy Metal Broadcast</title>
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
            border: 2px solid #ff3366;
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 0 30px rgba(255, 51, 102, 0.2);
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
            letter-spacing: 2px;
            text-transform: uppercase;
            margin-top: 5px;
        }
        .now-playing {
            text-align: center;
            margin-bottom: 20px;
            background: rgba(0, 0, 0, 0.4);
            padding: 15px;
            border-radius: 12px;
            border: 1px solid rgba(255, 51, 102, 0.4);
        }
        .track-title {
            font-weight: 700;
            font-size: 1.05rem;
            margin-bottom: 4px;
        }
        .track-band {
            color: #ff3366;
            font-size: 0.75rem;
            font-family: 'JetBrains Mono', monospace;
            text-transform: uppercase;
            letter-spacing: 1px;
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
            border: 1px solid rgba(255, 51, 102, 0.3);
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
            background: rgba(255, 51, 102, 0.1);
            transform: scale(1.05);
        }
        button.play-btn {
            width: 65px;
            height: 65px;
            background: #ff3366;
            color: #05060a;
            border: none;
            font-size: 1.4rem;
            font-weight: bold;
        }
        button.play-btn:hover {
            background: #ff5580;
            color: #05060a;
            box-shadow: 0 0 15px #ff3366;
        }
        .metal-setlist-header {
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.75rem;
            color: #ff3366;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 10px;
            font-weight: 700;
            border-left: 3px solid #ff3366;
            padding-left: 8px;
        }
        .metal-box {
            max-height: 190px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 8px;
            background: #07090f;
            padding: 8px;
            border-radius: 12px;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }
        .metal-box::-webkit-scrollbar { width: 5px; }
        .metal-box::-webkit-scrollbar-thumb { background: #ff3366; border-radius: 10px; }
        
        .setlist-item {
            background: rgba(255, 255, 255, 0.03);
            border: 1px solid rgba(255, 255, 255, 0.05);
            padding: 12px;
            border-radius: 8px;
            cursor: pointer;
            text-align: left;
            color: #fff;
            font-size: 0.85rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: 0.2s;
            font-family: 'JetBrains Mono', monospace;
        }
        .setlist-item:hover {
            background: rgba(255, 51, 102, 0.15);
            border-color: rgba(255, 51, 102, 0.4);
        }
        .setlist-item.active {
            border-color: #ff3366;
            background: rgba(255, 51, 102, 0.25);
            color: #fff;
            font-weight: bold;
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
        <div class="tag">// Heavy Metal Broadcast</div>
    </div>

    <div class="now-playing">
        <div class="track-title" id="trackTitle">Selecione o canal</div>
        <div class="track-band" id="trackBand">Metal Stream</div>
    </div>

    <audio id="audioPlayer"></audio>

    <div class="controls">
        <button id="prevBtn" title="Anterior">⏮</button>
        <button id="playBtn" class="play-btn" title="Play/Pause">▶</button>
        <button id="nextBtn" title="Próxima">⏭</button>
    </div>

    <div class="metal-setlist-header">⚡ THRASH & METAL SETLIST</div>
    <div class="metal-box" id="setlistContainer"></div>

    <div class="status" id="statusText">● PRONTO PARA O SOM</div>
</div>

<script>
    // Streams dedicados e testados focados em Heavy Metal Tradicional, Thrash e Rock Pesado
    const setlistTracks = [
        { title: "Heavy Metal Maniacs", band: "Metal Devastation Radio", url: "https://radio.metaldevastationradio.com:8000/stream" },
        { title: "Pure Heavy Metal & NWOBHM", band: "Hard Sound Radio", url: "https://live.hardsoundradio.com:8000/stream" },
        { title: "Thrash, Speed & Death", band: "Total Metal Radio", url: "https://s4.radio.co/s8b8240f9b/listen" },
        { title: "Classic Rock & Metal Power", band: "Gonguet Heavy Metal", url: "https://listen.gonguet.com/heavy" }
    ];

    let currentIndex = 0;
    const audio = document.getElementById('audioPlayer');
    const playBtn = document.getElementById('playBtn');
    const prevBtn = document.getElementById('prevBtn');
    const nextBtn = document.getElementById('nextBtn');
    const trackTitle = document.getElementById('trackTitle');
    const trackBand = document.getElementById('trackBand');
    const setlistContainer = document.getElementById('setlistContainer');
    const statusText = document.getElementById('statusText');

    function renderSetlist() {
        setlistContainer.innerHTML = '';
        setlistTracks.forEach((track, index) => {
            const item = document.createElement('div');
            item.className = `setlist-item ${index === currentIndex ? 'active' : ''}`;
            item.innerHTML = `<span>[${index + 1}] ${track.band}</span>`;
            item.onclick = () => {
                currentIndex = index;
                loadTrack(currentIndex);
                playAudio();
            };
            setlistContainer.appendChild(item);
        });
    }

    function loadTrack(index) {
        currentIndex = index;
        const track = setlistTracks[currentIndex];
        audio.src = track.url;
        trackTitle.textContent = track.title;
        trackBand.textContent = track.band;
        renderSetlist();
    }

    function playAudio() {
        statusText.textContent = '● CONECTANDO AO METAL STREAM...';
        audio.play().then(() => {
            playBtn.textContent = '⏸';
            statusText.textContent = '● AO VIVO NA PRESSÃO';
        }).catch(err => {
            statusText.textContent = '⚠️ CLIQUE NO PLAY PARA LIBERAR O SOM';
        });
    }

    function pauseAudio() {
        audio.pause();
        playBtn.textContent = '▶';
        statusText.textContent = '⏸ SOM PAUSADO';
    }

    playBtn.onclick = () => {
        if (audio.paused) {
            playAudio();
        } else {
            pauseAudio();
        }
    };

    nextBtn.onclick = () => {
        currentIndex = (currentIndex + 1) % setlistTracks.length;
        loadTrack(currentIndex);
        playAudio();
    };

    prevBtn.onclick = () => {
        currentIndex = (currentIndex - 1 + setlistTracks.length) % setlistTracks.length;
        loadTrack(currentIndex);
        playAudio();
    };

    audio.onerror = () => {
        statusText.textContent = '⚠️ FALHA NA FREQUÊNCIA, PULANDO...';
    };

    loadTrack(0);
</script>

</body>
</html>
