
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
        <div class="subtitle">Heavy Metal Amp Simulator</div>
        
        <div class="player-box">
            <div class="track-info">
                <div style="font-size: 0.7rem; color: #39ff14; margin-bottom: 4px;">ESTÚDIO DE DISTORÇÃO</div>
                <div id="track-title">PRONTO PARA O RIF_</div>
            </div>

            <div class="visualizer" id="viz">
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
            </div>

            <button class="btn" id="toggleBtn">▶ LIGAR RÁDIO</button>
            <div class="status" id="statusMsg">Simulação de amplificador ativa</div>
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

        // Raízes de Heavy Metal (Drop D e Afinação padrão pesada em Hz)
        const metalNotes = [
            73.42,  // D2 (Drop D base)
            82.41,  // E2 (Low E)
            92.50,  // F#2
            110.00, // A2
            123.47  // B2
        ];

        const songTitles = [
            "Nels1Rocks - True Distortion Riff",
            "Heavy Metal Crunch Engine 24/7",
            "Thrash Metal Power Chords Loop",
            "Underground Amp Simulator Live"
        ];

        // Função que cria a curva de distorção valvulada (Overdrive pesado)
        function makeDistortionCurve(amount) {
            let k = typeof amount === 'number' ? amount : 50,
                n_samples = 44100,
                curve = new Float32Array(n_samples),
                deg = Math.PI / 180;
            for (let i = 0; i < n_samples; ++i) {
                let x = (i * 2) / n_samples - 1;
                curve[i] = ((3 + k) * x * 20 * deg) / (Math.PI + k * Math.abs(x));
            }
            return curve;
        }

        function playDistortedGuitar(ctx, rootFreq) {
            if (!isPlaying) return;
            const now = ctx.currentTime;

            // 1. Criar Waveshaper para distorção de guitarra
            const distortion = ctx.createWaveShaper();
            distortion.curve = makeDistortionCurve(600); // Nível alto de ganho/distorção
            distortion.oversample = '4x';

            // 2. Filtro de corte (Cabinet Simulator) - remove o som metálico/eletrônico agudo
            const cabFilter = ctx.createBiquadFilter();
            cabFilter.type = 'lowpass';
            cabFilter.frequency.setValueAtTime(2000, now); // Corta tudo acima de 2kHz (deixa encorpado)

            // 3. Ganho geral de volume com decay de palhetada
            const gainNode = ctx.createGain();
            gainNode.gain.setValueAtTime(0.18, now);
            gainNode.gain.exponentialRampToValueAtTime(0.001, now + 0.5);

            // Conexões: Osciladores -> Distorção -> Filtro Caixa -> Volume -> Saída
            distortion.connect(cabFilter);
            cabFilter.connect(gainNode);
            gainNode.connect(ctx.destination);

            // Toca o Power Chord (Fundamental + Quinta + Oitava)
            [rootFreq, rootFreq * 1.5, rootFreq * 2].forEach((freq, idx) => {
                let osc = ctx.createOscillator();
                // Mistura onda dente-de-serra e quadrada para encorpar o timbre de crunch
                osc.type = idx === 0 ? 'sawtooth' : 'square';
                osc.frequency.setValueAtTime(freq, now);
                
                osc.connect(distortion);
                osc.start(now);
                osc.stop(now + 0.5);
            });
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
            statusMsg.textContent = "🔴 AMPLIFICADOR NO MÁXIMO";

            let titleIdx = 0;
            trackTitle.textContent = songTitles[titleIdx];

            // Loop de riffs pesados simulando palhetadas rítmicas
            riffInterval = setInterval(() => {
                if (!isPlaying) return;

                let randomNote = metalNotes[Math.floor(Math.random() * metalNotes.length)];
                playDistortedGuitar(audioCtx, randomNote);

                if (Math.random() < 0.2) {
                    titleIdx = (titleIdx + 1) % songTitles.length;
                    trackTitle.textContent = songTitles[titleIdx];
                }
            }, 320);
        }

        function stopRadio() {
            isPlaying = false;
            clearInterval(riffInterval);
            toggleBtn.textContent = "▶ LIGAR RÁDIO";
            toggleBtn.classList.remove('playing');
            viz.classList.remove('playing');
            statusMsg.textContent = "TRANSMISSÃO PAUSADA";
            trackTitle.textContent = "PRONTO PARA O RIF_";
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
