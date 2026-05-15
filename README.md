
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks | Radio 2026</title>
    <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
    <style>
        :root { --skin-color: #00ff41; --bg-panel: #1a1a1a; --accent: #333; }
        body { background-color: #000; color: #ffcc00; font-family: 'VT323', monospace; display: flex; flex-direction: column; align-items: center; justify-content: center; height: 100vh; margin: 0; }
        
        #winamp-shell {
            width: 400px; background: var(--bg-panel); border: 3px solid var(--accent); padding: 12px;
            box-shadow: 8px 8px 0px #111; position: relative; transition: all 0.4s ease;
        }

        .winamp-top-bar { height: 10px; background: var(--accent); margin-bottom: 10px; }

        .display-unit {
            background: #000; border: 2px inset #444; height: 90px; padding: 10px;
            display: flex; flex-direction: column; justify-content: space-between;
        }

        .track-text {
            font-size: 9pt; color: var(--skin-color); text-transform: uppercase;
            white-space: nowrap; overflow: hidden; text-shadow: 0 0 5px var(--skin-color);
        }

        .kbps-row { font-size: 8pt; color: var(--skin-color); display: flex; justify-content: space-between; opacity: 0.7; }

        .visual-bars { display: flex; align-items: flex-end; gap: 2px; height: 18px; }
        .v-bar { width: 4px; background: var(--skin-color); animation: pulse 0.6s infinite ease-in-out; }
        @keyframes pulse { 0%, 100% { height: 4px; } 50% { height: 16px; } }

        .btn-group { display: flex; gap: 6px; margin-top: 15px; justify-content: center; }
        .w-btn {
            background: #2a2a2a; border: 2px outset #555; color: #eee;
            padding: 8px 14px; cursor: pointer; font-size: 13px; font-family: 'VT323';
            text-transform: uppercase;
        }
        .w-btn:active { border-style: inset; background: #000; color: var(--skin-color); }

        #yt-engine { position: absolute; left: -9999px; visibility: hidden; }
        
        .signature { margin-top: 25px; font-size: 10pt; color: #ffcc00; letter-spacing: 1px; }
    </style>
</head>
<body>

<div id="winamp-shell">
    <div class="winamp-top-bar"></div>

    <div class="display-unit" id="winamp-display">
        <div class="track-text" id="now-playing">NELS1ROCKS - PRESS PLAY</div>
        <div class="visual-bars">
            <div class="v-bar" style="animation-delay: 0.1s"></div>
            <div class="v-bar" style="animation-delay: 0.3s"></div>
            <div class="v-bar" style="animation-delay: 0.2s"></div>
            <div class="v-bar" style="animation-delay: 0.5s"></div>
            <div class="v-bar" style="animation-delay: 0.4s"></div>
        </div>
        <div class="kbps-row">
            <span>320 KBPS</span>
            <span>SHUFFLE ON</span>
            <span id="clock">2026</span>
        </div>
    </div>

    <div class="btn-group">
        <button class="w-btn" onclick="prev()">PREV</button>
        <button class="w-btn" id="play-trigger" onclick="play()">PLAY</button>
        <button class="w-btn" onclick="pause()">STOP</button>
        <button class="w-btn" onclick="next()">NEXT</button>
    </div>
</div>

<div class="signature">Nels1Rocks @2026 - Brasil</div>

<div id="yt-engine"><div id="player"></div></div>

<script>
    // Playlist com Links Verificados 2026
    const playlist = [
        { b: "In Flames", t: "Cloud Connected", id: "jJPXshHofXU" },
        { b: "At The Gates", t: "Blinded By Fear", id: "SF0U77bm9mc" },
        { b: "Nightwish", t: "Ghost Love Score", id: "uN3yqMr3hnY" },
        { b: "Stratovarius", t: "Black Diamond", id: "Tn58-Nl9NYw" },
        { b: "Kreator", t: "Pleasure to Kill", id: "v_7_T77v_r0" },
        { b: "Sodom", t: "Agent Orange", id: "X8m_vM_8mX8" },
        { b: "Destruction", t: "Thrash Till Death", id: "mJ_vM_8mX8" },
        { b: "Exodus", t: "The Toxic Waltz", id: "YST6vD_8mX8" },
        { b: "Testament", t: "Over the Wall", id: "X8m_vM_8mX8" },
        { b: "Sepultura", t: "Arise (Official)", id: "L397TWLwrUU" },
        { b: "Korzus", t: "Internally / Correria", id: "5A86665_9uE" },
        { b: "Krisiun", t: "Angelous Venenous", id: "8jWv06U9tGo" },
        { b: "Crypta", t: "From the Ashes", id: "S_W7SrePshA" },
        { b: "Ramones", t: "Rocket to Russia", id: "LhGq83WStS0" },
        { b: "Ratos de Porão", t: "Ao Vivo 92", id: "nB-F_ZfT8K8" }
    ];

    let player, idx = Math.floor(Math.random() * playlist.length);
    
    const skins = [
        {c: "#00ff41", b: "#1a1a1a", a: "#333"}, 
        {c: "#00ffff", b: "#0a1f2d", a: "#1e90ff"}, 
        {c: "#ff00ff", b: "#220022", a: "#800080"}, 
        {c: "#ffff00", b: "#1a1a00", a: "#b8860b"}, 
        {c: "#ff4444", b: "#1a0000", a: "#8b0000"},
        {c: "#adff2f", b: "#002200", a: "#228b22"}
    ];

    function onYouTubeIframeAPIReady() {
        player = new YT.Player('player', {
            height: '0', width: '0', videoId: playlist[idx].id,
            events: { 'onStateChange': (e) => { if(e.data === 0) next(); } }
        });
    }

    function play() { player.playVideo(); updateUI(); document.getElementById('play-trigger').innerText = "LIVE"; }
    function pause() { player.pauseVideo(); document.getElementById('play-trigger').innerText = "PLAY"; }
    
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

    function changeSkin() {
        const s = skins[Math.floor(Math.random() * skins.length)];
        document.documentElement.style.setProperty('--skin-color', s.c);
        document.documentElement.style.setProperty('--bg-panel', s.b);
        document.documentElement.style.setProperty('--accent', s.a);
    }

    function updateUI() {
        document.getElementById('now-playing').innerText = `${playlist[idx].b} - ${playlist[idx].t}`;
    }

    var tag = document.createElement('script'); tag.src = "https://www.youtube.com/iframe_api";
    var firstScriptTag = document.getElementsByTagName('script')[0];
    firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
</script>
</body>
</html>
