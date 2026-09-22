
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks Radio</title>
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
            max-width: 450px;
            width: 100%;
        }
        h1 {
            font-family: 'Metal Mania', cursive;
            font-size: 3rem;
            margin: 0 0 10px 0;
            text-shadow: 3px 3px 0px #000, 6px 6px 0px #8a2be2;
        }
        p {
            color: #bfaad1;
            font-size: 0.9rem;
            margin-bottom: 2rem;
            text-transform: uppercase;
            letter-spacing: 2px;
        }
        audio {
            width: 100%;
            outline: none;
        }
        .status {
            margin-top: 15px;
            font-size: 0.85rem;
            color: #39ff14;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="card">
        <h1>Nels1Rocks</h1>
        <p>Heavy Metal & Rock</p>
        
        <!-- Player Nativo Otimizado com sufixo de compatibilidade de stream -->
        <audio id="player" controls preload="none">
            <source src="https://icecast.somossistemas.com.br/proxy/nels1rocks?mp=/stream/;" type="audio/mpeg">
            Seu navegador não suporta áudio.
        </audio>

        <div id="msg" class="status">Pressione Play para conectar</div>
    </div>

    <script>
        const audio = document.getElementById('player');
        const msg = document.getElementById('msg');

        audio.addEventListener('playing', () => {
            msg.textContent = '● AO VIVO NO AR';
        });
        audio.addEventListener('pause', () => {
            msg.textContent = 'PAUSADO';
        });
        audio.addEventListener('error', () => {
            msg.textContent = '⚠️ ERRO AO CONECTAR AO STREAM';
        });
    </script>

</body>
</html>
