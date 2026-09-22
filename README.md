
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks Radio - Heavy Metal</title>
    <link href="https://fonts.googleapis.com/css2?family=Metal+Mania&family=Fira+Code:wght@400;700&display=swap" rel="stylesheet">
    <style>
        * { box-sizing: border-box; }
        body {
            margin: 0;
            background-color: #07030a;
            color: #ffffff;
            font-family: 'Fira Code', monospace;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .container {
            background: #10061d;
            border: 4px solid #000;
            box-shadow: 8px 8px 0px #000;
            padding: 2rem;
            text-align: center;
            max-width: 480px;
            width: 100%;
        }

        h1 {
            font-family: 'Metal Mania', cursive;
            font-size: 3.5rem;
            margin: 0;
            color: #fff;
            text-shadow: 3px 3px 0px #000, 6px 6px 0px #8a2be2;
            letter-spacing: 2px;
        }

        .subtitle {
            font-size: 0.8rem;
            color: #39ff14;
            text-transform: uppercase;
            letter-spacing: 3px;
            margin: 10px 0 20px 0;
            font-weight: bold;
        }

        .player-box {
            background: #000000;
            border: 3px solid #8a2be2;
            padding: 20px;
            box-shadow: inset 0 0 15px rgba(138, 43, 226, 0.3);
        }

        .track-info {
            background: #140824;
            border: 2px dashed #39ff14;
            padding: 12px;
            margin-bottom: 20px;
        }

        #track-title {
            font-size: 1rem;
            font-weight: bold;
            color: #fff;
        }

        .btn {
            background: #39ff14;
            color: #000;
            border: 3px solid #000;
            padding: 15px 25px;
            font-family: 'Fira Code', monospace;
            font-weight: bold;
            font-size: 1.1rem;
            cursor: pointer;
            box-shadow: 4px 4px 0px #000;
            text-transform: uppercase;
            width: 100%;
            transition: 0.1s;
        }

        .btn:active {
            box-shadow: 1px 1px 0px #000;
            transform: translate(3px, 3px);
        }

        .btn.playing {
            background: #ff3333;
            color: #fff;
        }

        .visualizer {
            display: flex;
            justify-content: center;
            gap: 6px;
            height: 25px;
            align-items: flex-end;
            margin: 20px 0 15px 0;
        }

        .bar {
            width: 8px;
            background: #39ff14;
            height: 4px;
        }

        .playing .bar {
            animation: bounce 0.4s infinite alternate;
        }
        .bar:nth-child(2) { animation-delay: 0.1s; }
        .bar:nth-child(3) { animation-delay: 0.3s; }
        .bar:nth-child(4) { animation-delay: 0.2s; }
        .bar:nth-child(5) { animation-delay: 0.4s; }

        @keyframes bounce {
            0% { height: 4px; }
            100% { height: 22px; }
        }

        .status {
            font-size: 0.75rem;
            color: #bfaad1;
            margin-top: 10px;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Nels1Rocks</h1>
        <div class="subtitle">Heavy Metal Distortion Engine</div>
        
        <div class="player-box">
            <div class="track-info">
                <div style="font-size: 0.7rem; color: #39ff14; margin-bottom: 4px;">ESTADO DO MOTOR DE GUITARRA</div>
                <div id="track-title">PRONTO PARA O SOM PESADO</div>
            </div>

            <div class="visualizer" id="viz">
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
            </div>

            <button class="btn" id="toggleBtn">▶ LIGAR RÁDIO</button>
            <div class="status" id="statusMsg">Timbre de distorção ativado</div>
        </div>
    </div>

    <script>
        let audioCtx = null;
        let isPlaying = false;
        let riffInterval = null;

        const toggleBtn = document.getElementById('toggleBtn');
        const trackTitle = document.getElementById('track-title');
        const statusMsg = document.getElementById('statusMsg');
        const viz = document.getElementById('viz');

        // Acordes de Rock Pesado e Metal (Power Chords em Hz: Fundamental + Quinta Justa)
        const powerChords = [
            { name: "E5 Power Riff (Drop E)", root: 82.41, fifth: 123.47 },   // E2 + B2
            { name: "A5 Heavy Metal Attack", root: 110.00, fifth: 164.81 },  // A2 + E3
            { name: "D5 Distortion Grind", root: 73.42, fifth: 110.00 },   // D2 + A2
            { name: "G5 Fast Thrash Riff", root: 98.00, fifth: 146.83 },   // G2 + D3
            { name: "B5 Dark Metal Breakdown", root: 61.74, fifth: 92.50 }   // B1 + F#2
        ];

        const songTitles = [
            "Nels1Rocks - Heavy Metal Core Riff",
            "Underground Distortion Loop (Live)",
            "Power Metal Blast Beat Machine",
            "Thrash Guitars Heavy Rotation"
        ];

        function playPowerChord(ctx, chord) {
            if (!isPlaying) return;

            const now = ctx.currentTime;

            // Função para gerar uma oitava distorcida (simulando amplificador valvulado)
            function createDistortedOscillator(freq, gainValue) {
                let osc = ctx.createOscillator();
                let gain = ctx.createGain();
                
                // Usando 'sawtooth' (dente de serra) que é a base para timbres de guitarra com distorção
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(freq, now);

                // Envoltória de ataque rápido e decay de guitarra pesada
                gain.gain.setValueAtTime(gainValue, now);
                gain.gain.exponentialRampToValueAtTime(0.001, now + 0.45);

                osc.connect(gain);
                gain.connect(ctx.destination);

                osc.start(now);
                osc.stop(now + 0.45);
            }

            // Toca a fundamental e a quinta simultaneamente (Power Chord encorpado) + oitava grave
            createDistortedOscillator(chord.root, 0.12);
            createDistortedOscillator(chord.fifth, 0.10);
            createDistortedOscillator(chord.root / 2, 0.08); // Sub-grave de peso
        }

        function startRadio() {
            if (!audioCtx) {
                audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            }
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }

            isPlaying = true;
            toggleBtn.textContent = "⏸ DESLIGAR RÁDIO";
            toggleBtn.classList.add('playing');
            viz.classList.add('playing');
            statusMsg.textContent = "🔴 ROLANDO O SOM PESADO";

            let titleIdx = 0;
            trackTitle.textContent = songTitles[titleIdx];

            // Ritmo dinâmico de riffs em loop infinito
            riffInterval = setInterval(() => {
                if (!isPlaying) return;

                let randomChord = powerChords[Math.floor(Math.random() * powerChords.length)];
                playPowerChord(audioCtx, randomChord);

                // Troca o título da "música" a cada alguns segundos
                if (Math.random() < 0.2) {
                    titleIdx = (titleIdx + 1) % songTitles.length;
                    trackTitle.textContent = songTitles[titleIdx];
                }
            }, 300); // Ritmo de andamento de metal pesado
        }

        function stopRadio() {
            isPlaying = false;
            clearInterval(riffInterval);
            toggleBtn.textContent = "▶ LIGAR RÁDIO";
            toggleBtn.classList.remove('playing');
            viz.classList.remove('playing');
            statusMsg.textContent = "TRANSMISSÃO PAUSADA";
            trackTitle.textContent = "PRONTO PARA O SOM PESADO";
        }

        toggleBtn.addEventListener('click', () => {
            if (!isPlaying) {
                startRadio();
            } else {
                stopRadio();
            }
        });
    </script>
</body>
</html>
