
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks | Winamp Skin Mode</title>
    <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
    <style>
        :root { --skin-color: #00ff41; }
        body { background-color: #000; color: #ffcc00; font-family: 'VT323', monospace; display: flex; flex-direction: column; align-items: center; justify-content: center; height: 100vh; margin: 0; }
        
        #winamp-container {
            width: 380px; background: #333; border: 3px solid #555; padding: 10px;
            box-shadow: 10px 10px 0px #111; position: relative; border-radius: 2px;
        }

        .winamp-title {
            background: linear-gradient(90deg, #000080, #1084d0); color: white;
            font-size: 11px; padding: 3px 10px; margin-bottom: 5px; text-transform: uppercase;
            display: flex; justify-content: space-between; border: 1px solid #777;
        }

        .main-display {
            background: #000; border: 2px inset #555; height: 85px; padding: 10px;
            display: flex; flex-direction: column; justify-content: space-between;
        }

        .track-info {
            font-size: 9pt; color: var(--skin-color); /* Limite rigoroso de 9pt */
            text-transform: uppercase; white-space: nowrap; overflow: hidden;
            text-shadow: 0 0 5px var(--skin-color);
        }

        .kbps-info { font-size: 8pt; color: var(--skin-color); display: flex; justify-content: space-between; opacity: 0.8; }

        .visualizer { display: flex; align-items: flex-end; gap: 2px; height: 15px; margin-top: 5px; }
        .bar { width: 3px; background: var(--skin-color); animation: bounce 0.5s infinite ease-in-out; }
        @keyframes bounce { 0%, 100% { height: 3px; } 50% { height: 12px; } }

        .controls { display: flex; gap: 5px; margin-top: 15px; justify-content: center; }
        .btn {
            background: #444; border: 2px outset #666; color: #ccc;
            padding: 6px 12px; cursor: pointer; font-size: 12px; font-family: 'VT323';
            text-transform: uppercase;
        }
        .btn:active { border-style: inset; background: #222; color: #fff; }

        #yt-player { position: absolute; left: -9999px; visibility: hidden; }
        
        .footer-info { font-size: 8pt; color: #555; margin-top: 12px; text-align: center; border-top: 1px solid #222; padding-top: 5px; }
    </style>
</head>
<body>

<div id="winamp-container">
    <div class="winamp-title">
        <span>Nels1Rocks v3.1 - Winamp Skin</span>
        <span>_ ◻ X</span>
    </div>

    <div class="main-display" id="display">
        <div class="track-info" id="track-name">SISTEMA OFFLINE - PRESS PLAY</div>
        <div class="visualizer">
            <div class="bar" style="animation-delay: 0.1s"></div>
            <div class="bar" style="animation-delay: 0.3s"></div>
            <div class="bar" style="animation-delay: 0.2s"></div>
            <div class="bar" style="animation-delay: 0.4s"></div>
            <div class="bar" style="animation-delay: 0.5s"></div>
            <div class="bar" style="animation-delay: 0.2s"></div>
        </div>
        <div class="kbps-info">
            <span id="stat-bits">320 KBPS</span>
            <span id="stat-khz">44.1 KHZ</span>
            <span id="timer">00:00</span>
        </div>
    </div>

    <div class="controls">
        <button class="btn" onclick="prev()">PREV</button>
        <button class="btn" id="play-btn" onclick="play()">PLAY</button>
        <button class="btn" onclick="pause()">PAUSE</button>
        <button class="btn" onclick="next()">NEXT</button>
    </div>

    <div class="footer-info">
        MIXER: SHUFFLE ACTIVE | SYNE3 CASH/DEBT: 0.83
    </div>
</div>

<div id="yt-player"><div id="player"></div></div>

<script>
    // Setlist completo conforme solicitado
    const playlist = [
        { b: "Ramones", t: "Rocket to Russia (Full)", id: "LhGq83WStS0" },
        { b: "Rammstein", t: "Amerika", id: "Rr8ljRgcJNM" },
        { b: "Megadeth", t: "Conquer or Die", id: "pG7_gU6V2vA" },
        { b: "Megadeth", t: "Dystopia", id: "bK95lWHX7E4" },
        { b: "Sepultura", t: "Nation / Roots / Arise", id: "L397TWLwrUU" },
        { b: "Korzus", t: "Internally / Correria", id: "5A86665_9uE" },
        { b: "Joelho de Porco", t: "As Melhores", id: "uY9K1fO_6mQ" },
        { b: "Mutantes", t: "As Melhores", id: "rS1uOOnkS_M" },
        { b: "Dimmu Borgir", t: "Gates of Babylon", id: "V6vXU_p2jF0" },
        { b: "Amon Amarth", t: "Thunder God", id: "edBYB1VCV0k" },
        { b: "Ratos de Porão", t: "Vivo 92 (Full)", id: "nB-F_ZfT8K8" },
        { b: "Shaman", t: "Lisbon / Fairy Tale", id: "j_tN7m7-fDk" },
        { b: "Blaze Bayley", t: "Silicon Messiah", id: "uVv0H_f7Bv4" },
        { b: "Accept", t: "Fast as a Shark", id: "tTeXBTStek0" },
        { b: "Krisiun", t: "Angelous Venenous", id: "8jWv06U9tGo" },
        { b: "Crypta", t: "From the Ashes", id: "S_W7SrePshA" },
        { b: "Iron Maiden", t: "Running Free (D'Anno)", id: "N6S96o-F6Yc" }
    ];

    let player, idx = Math.floor(Math.random() * playlist.length);
    const skins = ["#00ff41", "#ff00ff", "#00ffff", "#ffff00", "#ff4444", "#ffffff"];

    function onYouTubeIframeAPIReady() {
        player = new YT.Player('player', {
            height: '0', width: '0', videoId: playlist[idx].id,
            playerVars: { 'autoplay': 0, 'controls': 0 },
            events: { 'onStateChange': (e) => { if(e.data === 0) next(); } }
        });
    }

    function play() { 
        player.playVideo(); 
        updateUI(); 
        document.getElementById('play-btn').innerText = "PLAYING";
    }

    function pause() { 
        player.pauseVideo(); 
        document.getElementById('play-btn').innerText = "PLAY";
    }

    function next() { 
        idx = (idx + 1) % playlist.length; 
        changeSkin(); 
        player.loadVideoById(playlist[idx].id); 
        updateUI(); 
    }

    function prev() { 
        idx = (idx - 1 + playlist.length) % playlist.length; 
        changeSkin(); 
        player.loadVideoById(playlist[idx].id); 
        updateUI(); 
    }

    function updateUI() {
        document.getElementById('track-name').innerText = `${playlist[idx].b} - ${playlist[idx].t}`;
    }

    function changeSkin() {
        const newColor = skins[Math.floor(Math.random() * skins.length)];
        document.documentElement.style.setProperty('--skin-color', newColor);
    }

    var tag = document.createElement('script'); tag.src = "https://www.youtube.com/iframe_api";
    var firstScriptTag = document.getElementsByTagName('script')[0];
    firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
</script>
</body>
</html>
