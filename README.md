
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks | Maquinado Digital</title>
    <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
    <style>
        :root { 
            --neon-color: #00f2ff; 
            --glass-bg: rgba(0, 242, 255, 0.15);
            --border-color: rgba(0, 242, 255, 0.4);
        }
        
        body { 
            background: radial-gradient(circle, #1a1a2e 0%, #000000 100%); 
            color: #fff; 
            font-family: 'VT323', monospace; 
            display: flex; 
            flex-direction: column; 
            align-items: center; 
            justify-content: center; 
            min-height: 100vh; 
            margin: 0;
            overflow: hidden;
        }

        #winamp-shell {
            width: 420px;
            background: var(--glass-bg);
            backdrop-filter: blur(15px);
            border: 2px solid var(--border-color);
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 0 30px var(--glass-bg), inset 0 0 15px var(--border-color);
            position: relative;
        }

        .winamp-top-bar { 
            height: 6px; 
            background: var(--border-color); 
            border-radius: 10px;
            margin-bottom: 15px; 
            box-shadow: 0 0 10px var(--neon-color);
        }

        .display-unit {
            background: rgba(0, 0, 0, 0.6);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            height: 110px;
            padding: 12px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            box-shadow: inset 0 0 10px #000;
        }

        .track-text {
            font-size: 11pt;
            color: var(--neon-color);
            text-transform: uppercase;
            white-space: nowrap;
            overflow: hidden;
            text-shadow: 0 0 8px var(--neon-color);
            letter-spacing: 1px;
        }

        .visual-bars { display: flex; align-items: flex-end; gap: 3px; height: 20px; }
        .v-bar { width: 5px; background: var(--neon-color); border-radius: 2px; animation: pulse 0.6s infinite ease-in-out; }
        @keyframes pulse { 0%, 100% { height: 5px; opacity: 0.5; } 50% { height: 18px; opacity: 1; } }

        /* Letreiro LED Correndo para a Direita */
        .led-container {
            width: 100%;
            overflow: hidden;
            white-space: nowrap;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 4px;
            margin-top: 5px;
        }

        .led-text {
            display: inline-block;
            font-size: 14pt;
            color: var(--neon-color);
            text-shadow: 0 0 8px var(--neon-color);
            animation: scrollRight 6s linear infinite;
        }

        @keyframes scrollRight {
            from { transform: translateX(-100%); }
            to { transform: translateX(100%); }
        }

        .btn-group { display: flex; gap: 10px; margin-top: 20px; justify-content: center; }
        .w-btn {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid var(--border-color);
            color: #fff;
            padding: 10px 16px;
            border-radius: 50px;
            cursor: pointer;
            font-size: 14px;
            font-family: 'VT323';
            text-transform: uppercase;
            transition: 0.3s;
        }
        .w-btn:hover { background: var(--glass-bg); box-shadow: 0 0 15px var(--neon-color); transform: scale(1.05); }

        .signature { margin-top: 30px; font-size: 11pt; color: var(--neon-color); opacity: 0.8; }

        .ads-container {
            margin-top: 40px; width: 420px; border-radius: 10px;
            background: rgba(255, 255, 255, 0.05); border: 1px solid rgba(255, 255, 255, 0.1);
            padding: 15px; text-align: center; color: #aaa; font-size: 10pt;
        }
        .ads-link { color: var(--neon-color); text-decoration: none; font-weight: bold; }
    </style>
</head>
<body>

<div id="winamp-shell">
    <div class="winamp-top-bar"></div>

    <div class="display-unit">
        <div class="track-text" id="now-playing">SISTEMA MAQUINADO - PLAY</div>
        
        <div style="display: flex; justify-content: space-between; font-size: 8pt; color: var(--neon-color); opacity: 0.7;">
            <span>HI-RES AUDIO</span>
            <span>XP TRANSLUCENT</span>
        </div>

        <!-- Letreiro LED Nels1Rocks -->
        <div class="led-container">
            <div class="led-text">Nels1Rocks &nbsp;&nbsp;&nbsp; Nels1Rocks &nbsp;&nbsp;&nbsp; Nels1Rocks</div>
        </div>

        <div class="visual-bars">
            <div class="v-bar" style="animation-delay: 0.1s"></div>
            <div class="v-bar" style="animation-delay: 0.3s"></div>
            <div class="v-bar" style="animation-delay: 0.2s"></div>
            <div class="v-bar" style="animation-delay: 0.5s"></div>
            <div class="v-bar" style="animation-delay: 0.4s"></div>
            <div class="v-bar" style="animation-delay: 0.6s"></div>
        </div>
    </div>

    <div class="btn-group">
        <button class="w-btn" onclick="prev()">PREV</button>
        <button class="w-btn" id="play-trigger" onclick="play()">PLAY</button>
        <button class="w-btn" onclick="pause()">STOP</button>
        <button class="w-btn" onclick="next()">NEXT</button>
    </div>
</div>

<div class="signature">Nels1Rocks @Brasil-2026 - Maquinado Digital</div>

<div class="ads-container">
    PROJETO SURREALISTA: <a href="#" class="ads-link">CONHEÇA A OBRA</a><br>
    CULTURA METAL: <a href="#" class="ads-link">ASSINE HEAVY METAL 2026</a>
</div>

<div id="yt-engine"><div id="player"></div></div>

<script>
    const playlist = [
        { b: "SEPULTURA", t: "ARISE (REMASTERED)", id: "6BOHpjIZyx0" },
        { b: "KORZUS", t: "INTERNALLY / CORRERIA", id: "5A86665_9uE" },
        { b: "KRISIUN", t: "ANGELOUS VENENOUS", id: "8jWv06U9tGo" },
        { b: "CRYPTA", t: "FROM THE ASHES", id: "S_W7SrePshA" },
        { b: "KREATOR", t: "PLEASURE TO KILL", id: "v_7_T77v_r0" },
        { b: "IN FLAMES", t: "CLOUD CONNECTED", id: "jJPXshHofXU" },
        { b: "NIGHTWISH", t: "GHOST LOVE SCORE", id: "uN3yqMr3hnY" },
        { b: "STRATOVARIUS", t: "BLACK DIAMOND", id: "Tn58-Nl9NYw" }
    ];

    let player, idx = Math.floor(Math.random() * playlist.length);
    const skins = [
        {c: "#00f2ff", g: "rgba(0, 242, 255, 0.15)", b: "rgba(0, 242, 255, 0.4)"}, 
        {c: "#ff00ff", g: "rgba(255, 0, 255, 0.15)", b: "rgba(255, 0, 255, 0.4)"}, 
        {c: "#39ff14", g: "rgba(57, 255, 20, 0.15)", b: "rgba(57, 255, 20, 0.4)"}, 
        {c: "#ff9100", g: "rgba(255, 145, 0, 0.15)", b: "rgba(255, 145, 0, 0.4)"}
    ];

    function onYouTubeIframeAPIReady() {
        player = new YT.Player('player', {
            height: '0', width: '0', 
            videoId: playlist[idx].id,
            host: 'https://www.youtube-nocookie.com',
            events: { 
                'onReady': (e) => { e.target.cueVideoById(playlist[idx].id); },
                'onStateChange': (e) => { 
                    if(e.data === 0) next();
                    if(e.data === 1) updateSyncDisplay();
                } 
            }
        });
    }

    function play() { player.playVideo(); document.getElementById('play-trigger').innerText = "LIVE"; }
    function pause() { player.pauseVideo(); document.getElementById('play-trigger').innerText = "PLAY"; }
    function next() { idx = (idx + 1) % playlist.length; changeSkin(); player.loadVideoById(playlist[idx].id); }
    function prev() { idx = (idx - 1 + playlist.length) % playlist.length; changeSkin(); player.loadVideoById(playlist[idx].id); }

    function updateSyncDisplay() {
        document.getElementById('now-playing').innerText = `${playlist[idx].b} - ${playlist[idx].t}`;
    }

    function changeSkin() {
        const s = skins[Math.floor(Math.random() * skins.length)];
        document.documentElement.style.setProperty('--neon-color', s.c);
        document.documentElement.style.setProperty('--glass-bg', s.g);
        document.documentElement.style.setProperty('--border-color', s.b);
    }

    var tag = document.createElement('script'); 
    tag.src = "https://www.youtube.com/iframe_api";
    var firstScriptTag = document.getElementsByTagName('script')[0];
    firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
</script>
</body>
</html>
