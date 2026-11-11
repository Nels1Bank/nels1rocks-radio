
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nels1Rocks Radio - Heavy Metal</title>
    <!-- Importação das fontes Google -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;600;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-deep: #0a0a0c;
            --bg-card: #121216;
            --bg-hover: #1c1c24;
            --text-main: #f0f0f5;
            --text-muted: #8a8a9e;
            --border: #262633;
            --border-active: #e50914;
            --accent: #e50914;
            --accent-glow: rgba(229, 9, 20, 0.25);
        }

        * { 
            box-sizing: border-box; 
            margin: 0; 
            padding: 0; 
        }

        body {
            background-color: var(--bg-deep);
            color: var(--text-main);
            font-family: 'Inter', sans-serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .app-container {
            width: 100%;
            max-width: 440px;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 20px;
            padding: 25px;
            box-shadow: 0 24px 60px rgba(0, 0, 0, 0.8), 0 0 40px var(--accent-glow);
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 12px;
            border-bottom: 1px solid var(--border);
        }

        .brand {
            font-family: 'JetBrains Mono', monospace;
            font-size: 1.2rem;
            font-weight: 700;
        }

        .brand span { 
            color: var(--accent); 
        }

        .live-badge {
            display: flex;
            align-items: center;
            gap: 6px;
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.65rem;
            background: rgba(229, 9, 20, 0.1);
            color: var(--accent);
            padding: 5px 10px;
            border-radius: 20px;
            border: 1px solid var(--border-
