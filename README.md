
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
            padding: 15px;
            margin-top: 10px;
        }
        audio {
            width: 100%;
        }
        .status {
            margin-top: 15px;
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
            <!-- Rota roteada via proxy seguro para contornar bloqueio de celular/HTTPS -->
            <audio id="audio-stream" controls preload="none">
                <source src="https://corsproxy.io/?https://icecast.somossistemas.com.br/proxy/nels1rocks?mp=/stream" type="audio/mpeg">
                Seu navegador não suporta áudio.
            </audio>
        </div>

        <div id="status-msg" class="status">Toque em Play para sintonizar</div>
    </div>

    <script>
        const player = document.getElementById('audio-stream');
        const statusMsg = document.getElementById('status-msg');

        player.addEventListener('playing', () => {
            statusMsg.textContent = '🔴 AO VIVO NO AR';
        });

        player.addEventListener('waiting', () => {
            statusMsg.textContent = '⏳ SINTONIZANDO FREQUÊNCIA...';
        });

        player.addEventListener('error', () => {
            statusMsg.textContent = '⚠️ ERRO NO SERVIDOR DE STREAM';
        });
    </script>

</body>
</html>
