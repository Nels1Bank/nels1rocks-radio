
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks Rádio</title>
    <link href="https://fonts.googleapis.com/css2?family=Metal+Mania&family=Fira+Code:wght@400;700&display=swap" rel="stylesheet">
    <style>
        * { box-sizing: border-box; }
        body {
            margin: 0;
            background: #07030a;
            color: #ffffff;
            font-family: 'Fira Code', monospace;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        .card {
            background: #10061d;
            border: 4px solid #000;
            box-shadow: 6px 6px 0px #000;
            padding: 2rem;
            text-align: center;
            max-width: 480px;
            width: 100%;
        }
        h1 {
            font-family: 'Metal Mania', cursive;
            font-size: 2.8rem;
            margin: 0 0 10px 0;
            text-shadow: 3px 3px 0px #000, 6px 6px 0px #8a2be2;
        }
        p {
            color: #bfaad1;
            font-size: 0.8rem;
            margin-bottom: 2rem;
            text-transform: uppercase;
            letter-spacing: 2px;
        }
        .player-box {
            background: #000;
            border: 2px solid #8a2be2;
            padding: 20px;
            margin-top: 10px;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 15px;
        }
        .btn-play {
            background: #8a2be2;
            color: #fff;
            border: 3px solid #000;
            padding: 12px 25px;
            font-family: 'Fira Code', monospace;
            font-weight: bold;
            font-size: 1.1rem;
            cursor: pointer;
            box-shadow: 4px 4px 0px #000;
            text-transform: uppercase;
        }
        .btn-play:active {
            box-shadow: 1px 1px 0px #000;
            transform: translate(3px, 3px);
        }
        .status {
            font-size: 0.8rem;
            color: #39ff14;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="card">
        <h1>Nels1Rocks</h1>
        <p>Rádio Online de Heavy Metal e Rock</p>
        
        <div class="player-box">
            <!-- Botão de controle manual via objeto de Audio do JS -->
            <button class="btn-play" id="toggleBtn">▶ OUVIR RÁDIO</button>
            <div id="status-msg" class="status">ESTÚDIO PRONTO</div>
        </div>
    </div>

    <script>
        // Instancia o stream diretamente via objeto JavaScript
        const audio = new Audio("https://icecast.somossistemas.com.br/proxy/nels1rocks?mp=/stream");
        audio.preload = 'none';

        const btn = document.getElementById('toggleBtn');
        const statusMsg = document.getElementById('status-msg');

        let isPlaying = false;

        btn.addEventListener('click', () => {
            if (!isPlaying) {
                statusMsg.textContent = '⏳ CONECTANDO AO SERVIDOR...';
                audio.src = "https://icecast.somossistemas.com.br/proxy/nels1rocks?mp=/stream";
                audio.play().then(() => {
                    isPlaying = true;
                    btn.textContent = '⏸ PARAR RÁDIO';
                    statusMsg.textContent = '🔴 AO VIVO NO AR';
                }).catch(err => {
                    console.error(err);
                    statusMsg.textContent = '⚠️ ERRO DE BLOQUEIO DO SERVIDOR';
                });
            } else {
                audio.pause();
                isPlaying = false;
                btn.textContent = '▶ OUVIR RÁDIO';
                statusMsg.textContent = 'ESTÚDIO PAUSADO';
            }
        });
    </script>

</body>
</html>
