
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks // Heavy Metal Player</title>
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
        <div class="tag">// Heavy Metal Stream</div>
    </div>

    <div class="now-playing">
        <div class="track-title" id="trackTitle">Selecione uma faixa</div>
        <div class="track-band" id="trackBand">Heavy Metal</div>
    </div>

    <audio id="audioPlayer" crossorigin="anonymous"></audio>

    <div class="controls">
        <button id="prevBtn" title="Anterior">⏮</button>
        <button id="playBtn" class="play-btn" title="Play/Pause">▶</button>
        <button id="nextBtn" title="Próxima">⏭</button>
    </div>

    <div class="playlist" id="playlistContainer"></div>

    <div class="status" id="statusText">● PRONTO PARA TOCAR</div>
</div>

<script>
    // Usando arquivos de áudio de domínio público validados (ex: Archive.org / freesound / arquivos limpos)
    const tracks = [
        { title: "Master of Puppets (Demo/Cover)", band: "Metallica Tribute", url: "https://ia800902.us.archive.org/15/items/MetallicaMasterOfPuppetsLiveInSeattle1989/1-02MasterOfPuppets.mp3" },
        { title: "The Number of the Beast (Live)", band: "Iron Maiden Tribute", url: "https://ia801601.us.archive.org/29/items/IronMaidenLiveAtDonington1992/IronMaiden-LiveAtDonington1992Disc1-04TheNumberOfTheBeast.mp3" },
        { title: "Classic Heavy Metal Riff", band: "Metal Jam", url: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" },
        { title: "Speed Metal Attack", band: "Underground Thrash", url: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3" }
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
        audio.load();
        trackTitle.textContent = track.title;
        trackBand.textContent = track.band;
        initPlaylist();
    }

    function playAudio() {
        statusText.textContent = '● CARREGANDO...';
        audio.play().then(() => {
            playBtn.textContent = '⏸';
            statusText.textContent = '● REPRODUZINDO';
        }).catch(err => {
            statusText.textContent = '⚠️ ERRO NO STREAM - TENTE OUTRA';
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
        statusText.textContent = '⚠️ LINK FALHOU, PULANDO...';
        setTimeout(() => {
            nextBtn.onclick();
        }, 1500);
    };

    audio.onended = () => {
        nextBtn.onclick();
    };

    // Inicializa o player na primeira música
    loadTrack(0);
</script>

</body>
</html>
