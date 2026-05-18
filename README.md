
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks - Dashboard</title>
    <style>
        /* Estilização Geral - Pegada Dark/Rock */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #0d0d0d;
            color: #e0e0e0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }

        .dashboard-container {
            background: linear-gradient(145deg, #141414, #1f1f1f);
            border: 1px solid #333;
            border-radius: 12px;
            padding: 30px;
            width: 100%;
            max-width: 500px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.7);
            text-align: center;
        }

        h1 {
            font-size: 1.8rem;
            color: #ff3333;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 25px;
            border-bottom: 2px solid #333;
            padding-bottom: 10px;
        }

        /* Widget de Mídia */
        .player-widget {
            background-color: #0a0a0a;
            border-left: 4px solid #ff3333;
            border-radius: 6px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.8);
        }

        .status-label {
            font-size: 0.75rem;
            text-transform: uppercase;
            color: #888;
            letter-spacing: 1px;
            margin-bottom: 8px;
            display: block;
        }

        /* Onde a mágica acontece - IDs para o JavaScript alterar */
        .music-title {
            font-size: 1.3rem;
            font-weight: bold;
            color: #fff;
            margin-bottom: 5px;
            transition: color 0.3s ease;
        }

        .artist-name {
            font-size: 1rem;
            color: #b0b0b0;
            font-style: italic;
        }

        /* Indicador de Atualização Ativa */
        .live-indicator {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            font-size: 0.7rem;
            color: #00ff66;
            text-transform: uppercase;
            margin-top: 15px;
        }

        .dot {
            width: 8px;
            height: 8px;
            background-color: #00ff66;
            border-radius: 50%;
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { opacity: 0.4; }
            50% { opacity: 1; }
            100% { opacity: 0.4; }
        }
    </style>
</head>
<body>

    <div class="dashboard-container">
        <h1>Nels1Rocks</h1>
        
        <!-- Widget que mostra o que está tocando -->
        <div class="player-widget">
            <span class="status-label">Tocando Agora</span>
            <!-- O JavaScript vai substituir o conteúdo inicial abaixo dinamicamente -->
            <div id="current-track" class="music-title">Carregando faixa...</div>
            <div id="current-artist" class="artist-name">Carregando artista...</div>
        </div>

        <!-- Indicador de que o script de automação está rodando -->
        <div class="live-indicator">
            <div class="dot"></div>
            <span>Auto-Sync Ativo</span>
        </div>
    </div>

    <script>
        // LÓGICA DE AUTOMAÇÃO (JavaScript)
        
        // Função que simula a busca de dados de uma API (Spotify, arquivo local, etc.)
        // Na prática real, aqui entraria um fetch() buscando o JSON do player.
        function atualizarMediaAutomatico() {
            // Simulando dados que mudariam em tempo real no seu player
            const dadosDoPlayer = {
                musica: "Karma Mecânico",
                artista: "Tripalium"
            };

            // Captura os elementos do HTML pelos IDs únicos
            const elementoMusica = document.getElementById("current-track");
            const elementoArtista = document.getElementById("current-artist");

            // Injeta os nomes automaticamente nas tags correspondentes do HTML
            elementoMusica.innerText = dadosDoPlayer.musica;
            elementoArtista.innerText = dadosDoPlayer.artista;
            
            console.log(`[Nels1Rocks] Atualizado automaticamente: ${dadosDoPlayer.artista} - ${dadosDoPlayer.musica}`);
        }

        // Executa a função assim que a página carregar
        window.onload = function() {
            atualizarMediaAutomatico();
            
            // Loop de Automação: Executa a checagem a cada 5 segundos (5000 milissegundos)
            // para garantir que se a música mudar no player, muda na tela sozinho.
            setInterval(atualizarMediaAutomatico, 5000);
        };
    </script>

</body>
</html>
