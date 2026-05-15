
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks | Heavy Radio</title>
    <!-- Fonte estilo rádio antigo / terminal -->
    <link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
    <style>
        body {
            background-color: #000; /* Fundo sempre preto */
            color: #ffcc00; /* Texto amarelo */
            font-family: 'VT323', monospace;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        #radio-shell {
            width: 420px;
            background: #111;
            border: 5px solid #333;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 0 50px rgba(0,0,0,1), inset 0 0 20px #000;
            text-align: center;
        }

        .header-title {
            background-color: #ffcc00;
            color: #000;
            font-size: 28px;
            padding: 5px;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 5px;
            margin-bottom: 20px;
            border: 2px solid #000;
        }

        /* Display de Rádio Antigo */
        .radio-display {
            background-color: #1a1a1a;
            border: 4px inset #333;
            height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 25px;
            overflow: hidden;
            box-shadow: inset 0 0 15px #000;
        }

        .track-info {
            font-size: 9pt; /* Máximo 9 conforme instrução */
            color: #00ff41; /* Verde fósforo antigo */
            text-transform: uppercase;
            white-space: nowrap;
            letter-spacing: 1px;
            text-shadow: 0 0 8px #00ff41;
        }

        .controls-row {
            display: flex;
            justify-content: space-around;
            margin-bottom: 15px;
        }

        .btn-radio {
            background: #222;
            color: #ffcc00;
            border: 3px outset #444;
            padding: 10px 15px;
            font-family: 'VT323', monospace;
            cursor: pointer;
            font-size: 16px;
            min-width: 80px;
        }

        .btn-radio:active {
            border-style: inset;
            background: #000;
        }

        .mixer-info {
            font-size: 8pt;
            color: #444;
            text-align: left;
            border-top: 1px solid #222;
            padding-top: 10px;
            line-height: 1.2;
        }

        /* Esconde o player real do Google */
        #yt-api-frame {
            position: absolute;
            left: -9999px;
            visibility: hidden;
        }
    </style>
</head>
<body>

<div id="radio-shell">
    <div class="header-title">NELS1ROCKS</div>
    
    <div class="radio-display">
        <div id="track-text" class="track-info">SISTEMA OFFLINE - PRESS PLAY</div>
    </div>

    <div class="controls-row">
        <button class="btn-radio" onclick="prev()">PREV</button>
        <button class="btn-radio" id="powerBtn" onclick="togglePower()" style="background: #300; border-color: #600;">ON/OFF</button>
        <button class="btn-radio" onclick="next()">NEXT</button>
    </div>

    <div class="mixer-info">
        MODE: 24/7 SHUFFLE MIXER<br>
        CODEC: THRASH/HARDCORE/PUNK/METAL<br>
        SYNE3 LIQUIDITY STATUS: 0.83 CASH/DEBT
    </div>
</div>

<!-- Player oculto -->
<div id="yt-api-frame">
    <div id="player"></div>
</div>

<script>
    // Playlist Hardcore/Metal para o Nels1Rocks
    const playlist = [
        {id: "xnKhs2z8KwI", b: "Metallica", t: "Master of Puppets"},
        {id: "nM__lPTWThU", b: "Judas Priest", t: "Painkiller"},
        {id: "z8ZqFlw6hYg", b: "Slayer", t: "Raining Blood"},
        {id: "9d4ui9q7eDM", b: "Megadeth", t: "Holy Wars"},
        {id: "FuO3hHwQ54Q", b: "Helloween", t: "Eagle Fly Free"},
        {id: "L397TWLwrUU", b: "Sepultura", t: "Arise"},
        {id: "-KTsXHvlAJA", b: "Dead Kennedys", t: "Holiday in Cambodia"},
        {id: "WxnN05vOuSM", b: "Iron Maiden", t: "Number of the Beast"}
    ];

    let player;
    let idx = Math.floor(Math.random() * playlist.length); // Shuffle inicial

    function onYouTubeIframeAPIReady() {
        player = new YT.Player('player', {
            height: '0', width: '0',
            videoId: playlist[idx].id,
            events: { 'onStateChange': stateChange }
        });
    }

    function togglePower() {
        const btn = document.getElementById('powerBtn');
        if (player.getPlayerState() === 1) {
            player.pauseVideo();
            btn.style.background = "#300";
            document.getElementById('track-text').innerText = "PAUSED - STANDBY";
        } else {
            player.playVideo();
            btn.style.background = "#004400";
            btn.style.borderColor = "#00ff00";
            updateDisplay();
        }
    }

    function updateDisplay() {
        const s = playlist[idx];
        document.getElementById('track-text').innerText = `${s.b} - ${s.t}`;
    }

    function stateChange(e) {
        if (e.data == 0) next(); // Auto-play 24/7
    }

    function next() {
        idx = (idx + 1) % playlist.length;
        player.loadVideoById(playlist[idx].id);
        updateDisplay();
    }

    function prev() {
        idx = (idx - 1 + playlist.length) % playlist.length;
        player.loadVideoById(playlist[idx].id);
        updateDisplay();
    }

    // Carrega API do Google
    var tag = document.createElement('script');
    tag.src = "https://www.youtube.com/iframe_api";
    var firstScriptTag = document.getElementsByTagName('script')[0];
    firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
</script>

</body>
</html>
