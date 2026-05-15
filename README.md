
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks | Radio 2026</title>
    <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
    <style>
        :root { --skin-color: #00ff41; --bg-panel: #1a1a1a; --accent: #333; }
        body { background-color: #000; color: #ffcc00; font-family: 'VT323', monospace; display: flex; flex-direction: column; align-items: center; justify-content: center; min-height: 100vh; margin: 0; padding-bottom: 20px; }
        
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

        .ads-container {
            margin-top: 40px; width: 400px; border: 1px dashed #444; padding: 10px; background: #050505;
            text-align: center; color: #888; font-size: 9pt;
        }
        .ads-link { color: #ffcc00; text-decoration: none; border-bottom: 1px solid #ffcc00; }
    </style>
</head>
<body>

<div id="winamp-shell">
    <div class="winamp-top-bar"></div>

    <div class="display-unit">
        <div class="track-text" id="now-playing">ESTAÇÃO CARREGADA - APERTE PLAY</div>
        <div class="visual-bars">
            <div class="v-bar" style="animation-delay: 0.1s"></div>
            <div class="v-bar" style="animation-delay: 0.3s"></div>
            <div class="v-bar" style="animation-delay: 0.2s"></div>
            <div class="v-bar" style="animation-delay: 0.5s"></div>
            <div class="v-bar" style="animation-delay: 0.4s"></div>
        </div>
        <div class="kbps-row">
            <span>320 KBPS</span>
            <span>NO-ADS MODE</span>
            <span id="sync-status">STABLE</span>
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

<div class="ads-container">
    PROMOÇÃO: <a href="#" class="ads-link">BOX ESPECIAL SURREALISMO - NÃO LEIA</a><br>
    REVISTA HEAVY METAL #2026 - <a href="#" class="ads-link">ASSINE JÁ</a>
</div>

<div id="yt-engine"><div id="player"></div></div>

<script>
    const playlist = [
        { b: "SEPULTURA", t: "ARISE (OFFICIAL RE-UPLOAD)", id: "L397TWLwrUU" },
        { b: "KORZUS", t: "INTERNALLY / CORRERIA", id: "5A86665_9uE" },
        { b: "KRISIUN", t: "ANGELOUS VENENOUS", id: "8jWv06U9tGo" },
        { b: "CRYPTA", t: "FROM THE ASHES", id: "S_W7SrePshA" },
        { b: "KREATOR", t: "PLEASURE TO KILL", id: "v_7_T77v_r0" },
        { b: "IN FLAMES", t: "CLOUD CONNECTED", id: "jJPXshHofXU" },
        { b: "NIGHTWISH", t: "GHOST LOVE SCORE", id: "uN3yqMr3hnY" },
        { b: "RATOS DE PORÃO", t: "AO VIVO NO SESC", id: "nB-F_ZfT8K8" }
    ];

    let player, idx = Math.floor(Math.random() * playlist.length);
    
    const skins = [
        {c: "#00ff41", b: "#1a1a1a", a: "#333"}, 
        {c: "#00ffff", b: "#0a1f2d", a: "#1e90ff"}, 
        {c: "#ff4444", b: "#1a0000", a: "#8b0000"}
    ];

    function onYouTubeIframeAPIReady() {
        // Uso do domínio youtube-nocookie para reduzir anúncios
        player = new YT.Player('player', {
            height: '0', width: '0', 
            videoId: playlist[idx].id,
            host: 'https://www.youtube-nocookie.com',
            playerVars: { 
                'autoplay': 0, 
                'controls': 0, 
                'origin': window.location.origin 
            },
            events: { 
                'onReady': (e) => { 
                    e.target.cueVideoById(playlist[idx].id);
                    console.log("Player Ready & Cued"); 
                },
                'onStateChange': (e) => { 
                    if(e.data === 0) next();
                    if(e.data === 1) updateSyncDisplay();
                } 
            }
        });
    }

    function play() { 
        player.playVideo(); 
        document.getElementById('play-trigger').innerText = "LIVE"; 
    }
    
    function pause() { 
        player.pauseVideo(); 
        document.getElementById('play-trigger').innerText = "PLAY"; 
    }
    
    function next() { 
        idx = (idx + 1) % playlist.length; 
        changeSkin(); 
        player.loadVideoById(playlist[idx].id); 
    }

    function prev() { 
        idx = (idx - 1 + playlist.length) % playlist.length; 
        changeSkin(); 
        player.loadVideoById(playlist[idx].id); 
    }

    function updateSyncDisplay() {
        document.getElementById('now-playing').innerText = `${playlist[idx].b} - ${playlist[idx].t}`;
    }

    function changeSkin() {
        const s = skins[Math.floor(Math.random() * skins.length)];
        document.documentElement.style.setProperty('--skin-color', s.c);
        document.documentElement.style.setProperty('--bg-panel', s.b);
        document.documentElement.style.setProperty('--accent', s.a);
    }

    var tag = document.createElement('script'); 
    tag.src = "https://www.youtube.com/iframe_api";
    var firstScriptTag = document.getElementsByTagName('script')[0];
    firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
</script>
</body>
</html>
