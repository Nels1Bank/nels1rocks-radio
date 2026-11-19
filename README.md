
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Nels1Rocks.Radio 🤘</title>
  <link href="https://googleapis.com" rel="stylesheet">
  <style>
    :root {
      --bg-dark: #09090b;
      --card-bg: rgba(24, 24, 27, 0.85);
      --accent-red: #ff2a5f;
      --accent-orange: #ff7b00;
      --accent-purple: #8b5cf6;
      --text-main: #f4f4f5;
      --text-muted: #a1a1aa;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background: radial-gradient(circle at top center, #2e1065 0%, #180828 35%, var(--bg-dark) 80%);
      color: var(--text-main);
      font-family: 'Inter', sans-serif;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 24px 16px;
    }

    .container {
      width: 100%;
      max-width: 440px;
      display: flex;
      flex-direction: column;
      gap: 20px;
    }

    /* Card Principal do Player */
    .player-card {
      background: var(--card-bg);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 28px;
      padding: 28px 22px;
      text-align: center;
      box-shadow: 0 20px 50px rgba(0, 0, 0, 0.6), 0 0 30px rgba(255, 42, 95, 0.15);
    }

    .live-badge {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: rgba(255, 42, 95, 0.15);
      border: 1px solid rgba(255, 42, 95, 0.4);
      color: #ff6b8b;
      font-size: 11px;
      font-weight: 800;
      letter-spacing: 1.5px;
      padding: 6px 14px;
      border-radius: 999px;
      margin-bottom: 14px;
    }

    .pulse-dot {
      width: 8px;
      height: 8px;
      background-color: var(--accent-red);
      border-radius: 50%;
      box-shadow: 0 0 10px var(--accent-red);
      animation: pulse 1.5s infinite;
    }

    @keyframes pulse {
      0% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(255, 42, 95, 0.7); }
      70% { transform: scale(1); box-shadow: 0 0 0 8px rgba(255, 42, 95, 0); }
      100% { transform: scale(0.95); box-shadow: 0 0 0 0 rgba(255, 42, 95, 0); }
    }

    h1 {
      font-family: 'Metal Mania', cursive;
      font-size: 38px;
      letter-spacing: 2px;
      background: linear-gradient(90deg, #ff2a5f, #ff7b00, #facc15);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      margin-bottom: 6px;
    }

    .subtitle {
      color: var(--text-muted);
      font-size: 13px;
      margin-bottom: 18px;
    }

    .rock-icon {
      font-size: 54px;
      margin: 8px 0 18px;
      display: inline-block;
      filter: drop-shadow(0 0 16px rgba(255, 123, 0, 0.5));
      transition: transform 0.3s ease;
    }

    .playing .rock-icon {
      animation: headbang 0.6s infinite alternate ease-in-out;
    }

    @keyframes headbang {
      from { transform: rotate(-8deg) scale(1.05); }
      to { transform: rotate(8deg) scale(1.12); }
    }

    /* Botão Play Customizado */
    .play-btn {
      width: 100%;
      background: linear-gradient(135deg, var(--accent-red), var(--accent-orange));
      color: #fff;
      border: none;
      border-radius: 16px;
      padding: 16px;
      font-size: 16px;
      font-weight: 800;
      letter-spacing: 1px;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      box-shadow: 0 10px 25px rgba(255, 42, 95, 0.4);
      transition: all 0.2s ease;
      margin-bottom: 14px;
    }

    .play-btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 14px 30px rgba(255, 42, 95, 0.55);
    }

    .play-btn:active {
      transform: scale(0.98);
    }

    /* Seletor de Rádios (Fallback inteligente) */
    .server-selector {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 8px;
      margin-bottom: 14px;
    }

    .server-btn {
      background: rgba(255, 255, 255, 0.05);
      border: 1px solid rgba(255, 255, 255, 0.1);
      color: var(--text-muted);
      padding: 8px 4px;
      border-radius: 10px;
      font-size: 11px;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.2s;
    }

    .server-btn.active {
      background: rgba(139, 92, 246, 0.25);
      border-color: var(--accent-purple);
      color: #fff;
    }

    .status-bar {
      font-size: 12px;
      color: #34d399;
      min-height: 18px;
      font-weight: 600;
    }

    /* Card do Setlist */
    .setlist-card {
      background: var(--card-bg);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.08);
      border-radius: 24px;
      padding: 22px;
      box-shadow: 0 15px 35px rgba(0, 0, 0, 0.4);
    }

    .setlist-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 16px;
      padding-bottom: 12px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.08);
    }

    .setlist-title {
      font-size: 13px;
      font-weight: 800;
      letter-spacing: 1px;
      color: #facc15;
    }

    .setlist-tag {
      font-size: 11px;
      background: rgba(250, 204, 21, 0.15);
      color: #facc15;
      padding: 3px 8px;
      border-radius: 6px;
      font-weight: 600;
    }

    .track-list {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .track-item {
      display: flex;
      align-items: center;
      gap: 12px;
      padding: 10px 12px;
      background: rgba(255, 255, 255, 0.03);
      border-radius: 12px;
      font-size: 13px;
      transition: background 0.2s;
    }

    .track-item:hover {
      background: rgba(255, 255, 255, 0.08);
    }

    .track-num {
      font-weight: 800;
      font-size: 12px;
      color: var(--accent-orange);
      min-width: 20px;
    }

    .track-info {
      display: flex;
      flex-direction: column;
      text-align: left;
    }

    .track-song {
      font-weight: 600;
      color: var(--text-main);
    }

    .track-band {
      font-size: 11px;
      color: var(--text-muted);
    }

    /* Link de diagnóstico discreto */
    .debug-box {
      text-align: center;
      font-size: 11px;
      color: var(--text-muted);
      padding: 0 10px;
      line-height: 1.5;
    }

    .debug-box a {
      color: var(--accent-orange);
      text-decoration: none;
      word-break: break-all;
    }
  </style>
</head>
<body>

  <div class="container" id="app">
    <div class="player-card">
      <div class="live-badge">
        <span class="pulse-dot"></span>
        HEAVY METAL • AO VIVO 24H
      </div>

      <h1>Nels1Rocks.Radio</h1>
      <p class="subtitle">Troca automática de servidor se o sinal cair</p>

      <div class="rock-icon" id="rockIcon">🤘</div>

      <button class="play-btn" id="playBtn" onclick="togglePlay()">
        <span id="btnIcon">▶</span>
        <span id="btnText">OUVIR AGORA</span>
      </button>

      <div class="server-selector">
        <button class="server-btn active" onclick="selectStream(0)" id="srv0">Sinal 1 (SomaFM)</button>
        <button class="server-btn" onclick="selectStream(1)" id="srv1">Sinal 2 (Laut.FM)</button>
        <button class="server-btn" onclick="selectStream(2)" id="srv2">Sinal 3 (Zeno)</button>
      </div>

      <div class="status-bar" id="statusText">Pronto para tocar • Clique no Play</div>

      <audio id="radioPlayer" preload="none"></audio>
    </div>

    <div class="setlist-card">
      <div class="setlist-header">
        <span class="setlist-title">🔥 CLÁSSICOS NO AR</span>
        <span class="setlist-tag">SETLIST 24H</span>
      </div>

      <ul class="track-list">
        <li class="track-item"><span class="track-num">01</span><div class="track-info"><span class="track-song">Master of Puppets</span><span class="track-band">Metallica</span></div></li>
        <li class="track-item"><span class="track-num">02</span><div class="track-info"><span class="track-song">The Trooper</span><span class="track-band">Iron Maiden</span></div></li>
        <li class="track-item"><span class="track-num">03</span><div class="track-info"><span class="track-song">Paranoid</span><span class="track-band">Black Sabbath</span></div></li>
        <li class="track-item"><span class="track-num">04</span><div class="track-info"><span class="track-song">Raining Blood</span><span class="track-band">Slayer</span></div></li>
        <li class="track-item"><span class="track-num">05</span><div class="track-info"><span class="track-song">Cowboys From Hell</span><span class="track-band">Pantera</span></div></li>
        <li class="track-item"><span class="track-num">06</span><div class="track-info"><span class="track-song">Roots Bloody Roots</span><span class="track-band">Sepultura</span></div></li>
        <li class="track-item"><span class="track-num">07</span><div class="track-info"><span class="track-song">Symphony of Destruction</span><span class="track-band">Megadeth</span></div></li>
        <li class="track-item"><span class="track-num">08</span><div class="track-info"><span class="track-song">Breaking The Law</span><span class="track-band">Judas Priest</span></div></li>
        <li class="track-item"><span class="track-num">09</span><div class="track-info"><span class="track-song">Ace of Spades</span><span class="track-band">Motörhead</span></div></li>
        <li class="track-item"><span class="track-num">10</span><div class="track-info"><span class="track-song">Crazy Train</span><span class="track-band">Ozzy Osbourne</span></div></li>
      </ul>
    </div>

    <div class="debug-box">
      Teste direto no navegador caso o áudio bloqueie:<br>
      <a href="https://ice1.somafm.com/metal-128-mp3" target="_blank">https://ice1.somafm.com/metal-128-mp3</a>
    </div>
  </div>

  <script>
    const streams = [
