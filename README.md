<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>NexScript | Plataforma</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=Rajdhani:wght@700&family=Press+Start+2P&display=swap" rel="stylesheet" />
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet" />

    <style>
        :root {
            --bg: #050505;
            --panel: #0f1115;
            --primary: #3b82f6;
            --primary-dark: #1d4ed8;
            --accent: #00f0ff;
            --text: #e2e8f0;
            --muted: #64748b;
            --border: rgba(59, 130, 246, 0.15);
            --glass: rgba(15, 17, 21, 0.7);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Plus Jakarta Sans', sans-serif;
        }

        body {
            background: var(--bg);
            color: var(--text);
            height: 100vh;
            overflow: hidden; /* Garante tela cheia sem scroll na body */
            display: flex;
            flex-direction: column;
        }

        /* Efeito de Neve */
        #snow-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            pointer-events: none;
            z-index: 1;
            overflow: hidden;
        }

        .snowflake {
            position: absolute;
            top: -10px;
            background: white;
            border-radius: 50%;
            opacity: 0.8;
            animation: fall linear infinite;
        }

        @keyframes fall {
            to { transform: translateY(105vh); }
        }

        /* TELA DE LOGIN (Gatekeeper) */
        #gatekeeper {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--bg);
            z-index: 9999;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background-image: radial-gradient(circle at 50% 40%, #111b33 0%, #000 80%);
        }

        .auth-card {
            background: rgba(15, 17, 21, 0.6);
            backdrop-filter: blur(20px);
            border: 1px solid var(--border);
            padding: 40px;
            border-radius: 24px;
            width: 90%;
            max-width: 400px;
            box-shadow: 0 0 50px rgba(0, 0, 0, 0.8);
            z-index: 10;
            position: relative;
            animation: fadeIn 1s ease;
        }

        .auth-card h2 {
            margin-bottom: 20px;
            font-family: 'Rajdhani', sans-serif;
            font-size: 1.6rem;
            color: white;
        }

        .input-group { margin-bottom: 15px; }
        .input-field {
            width: 100%;
            padding: 12px;
            background: rgba(0, 0, 0, 0.3);
            border: 1px solid #1e293b;
            border-radius: 10px;
            color: white;
            outline: none;
            transition: 0.3s;
        }
        .input-field:focus {
            border-color: var(--primary);
            box-shadow: 0 0 15px rgba(59, 130, 246, 0.2);
        }

        .btn-action {
            width: 100%;
            padding: 12px;
            background: var(--primary);
            color: white;
            border: none;
            border-radius: 10px;
            font-weight: 700;
            cursor: pointer;
            transition: 0.3s;
            text-transform: uppercase;
            font-size: 0.9rem;
            letter-spacing: 1px;
        }
        .btn-action:hover {
            background: var(--primary-dark);
            transform: translateY(-2px);
        }

        /* CONTEÚDO PRINCIPAL */
        #main-content {
            flex: 1;
            display: flex; /* Sidebar na esquerda, conteudo na direita */
            position: relative;
            z-index: 5;
            height: 100vh;
        }

        /* Sidebar Simplificada */
        .sidebar {
            width: 80px; /* Mais fina para dar destaque ao conteudo */
            background: rgba(10, 12, 16, 0.8);
            border-right: 1px solid var(--border);
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px 0;
            flex-shrink: 0;
        }

        .nav-item {
            width: 50px;
            height: 50px;
            border-radius: 12px;
            color: var(--muted);
            cursor: pointer;
            transition: 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            margin-bottom: 20px;
        }

        .nav-item:hover, .nav-item.active {
            background: var(--primary);
            color: white;
            box-shadow: 0 0 15px rgba(59, 130, 246, 0.5);
        }

        /* Área de Conteúdo */
        .content-area {
            flex: 1;
            display: flex;
            flex-direction: column;
            overflow-y: auto; /* Scroll apenas aqui se precisar */
            position: relative;
            background: radial-gradient(circle at top right, #0a101f 0%, #050505 60%);
        }

        .container-padding {
            padding: 40px;
            flex: 1;
            display: flex;
            flex-direction: column;
        }

        /* Estilo do Card do Script */
        .script-card {
            background: #0a0c10;
            border-radius: 16px;
            padding: 25px;
            border: 1px solid #1e293b;
            transition: 0.3s;
            max-width: 600px;
            margin: 0 auto 50px auto; /* Centralizado horizontalmente */
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        .script-card:hover {
            border-color: var(--primary);
            box-shadow: 0 10px 40px rgba(59, 130, 246, 0.2);
        }

        .script-thumb {
            width: 100%;
            height: 200px;
            border-radius: 10px;
            margin-bottom: 20px;
            object-fit: cover;
            background: #111;
            border: 1px solid #333;
        }

        .script-info h3 {
            font-family: 'Rajdhani', sans-serif;
            font-size: 1.8rem;
            color: white;
            margin-bottom: 5px;
        }

        .script-password {
            background: rgba(0, 240, 255, 0.05);
            border: 1px solid rgba(0, 240, 255, 0.2);
            padding: 10px;
            border-radius: 8px;
            margin: 15px 0;
            color: var(--accent);
            font-family: monospace;
        }

        /* ESTILO PIXEL ART */
        .pixel-message-container {
            text-align: center;
            margin-top: auto; /* Empurra para baixo se tiver espaço, mas fica abaixo do script */
            margin-bottom: 50px;
            animation: pulse 2s infinite;
        }

        .pixel-big {
            font-family: 'Press Start 2P', cursive;
            font-size: 2rem; /* Grande */
            color: var(--accent);
            text-shadow: 4px 4px 0px #000, 0 0 20px var(--primary);
            line-height: 1.5;
            margin-bottom: 20px;
        }

        .pixel-small {
            font-family: 'Press Start 2P', cursive;
            font-size: 1rem;
            color: #fff;
            opacity: 0.8;
            text-shadow: 2px 2px 0px #000;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.02); }
            100% { transform: scale(1); }
        }

        footer {
            background: var(--panel);
            padding: 15px;
            border-top: 1px solid var(--border);
            text-align: center;
            color: var(--muted);
            font-size: 0.8rem;
            font-family: 'Rajdhani', sans-serif;
            letter-spacing: 1px;
        }

        /* Utilitarios */
        .hidden { display: none !important; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        
        /* Responsivo para celular */
        @media (max-width: 768px) {
            .pixel-big { font-size: 1.2rem; }
            .sidebar { width: 50px; }
            .script-card { width: 100%; }
        }
    </style>
</head>
<body>
    <div id="snow-container"></div>

    <div id="gatekeeper">
        <div class="auth-card" id="login-box">
            <h2 style="text-align: center;">ACESSO AO SISTEMA</h2>
            <div class="input-group">
                <input type="email" id="auth-email" class="input-field" placeholder="E-mail" />
            </div>
            <div class="input-group">
                <input type="password" id="auth-pass" class="input-field" placeholder="Senha" />
            </div>
            <button class="btn-action" onclick="handleLogin()">ENTRAR</button>
            <div style="margin-top:15px; text-align:center; font-size:0.8rem;">
                <a href="#" onclick="toggleAuth(true)" style="color:var(--primary);">Criar Conta</a>
            </div>
        </div>

        <div class="auth-card hidden" id="register-box">
            <h2 style="text-align: center;">REGISTRO</h2>
            <div class="input-group">
                <input type="text" id="reg-name" class="input-field" placeholder="Nome" />
            </div>
            <div class="input-group">
                <input type="email" id="reg-email" class="input-field" placeholder="E-mail" />
            </div>
            <div class="input-group">
                <input type="password" id="reg-pass" class="input-field" placeholder="Senha" />
            </div>
            <button class="btn-action" onclick="handleRegister()">CRIAR E ENTRAR</button>
            <p style="margin-top:10px; text-align:center; font-size:0.8rem;">
                <a href="#" onclick="toggleAuth(false)" style="color:var(--muted);">Voltar</a>
            </p>
        </div>
    </div>

    <div id="main-content" class="hidden">
        <div class="sidebar">
            <div class="nav-item active" title="Explorar">
                <i class="fas fa-terminal"></i>
            </div>
            <div style="flex:1"></div>
            <div class="nav-item" onclick="handleLogout()" title="Sair" style="color: #ff4444;">
                <i class="fas fa-power-off"></i>
            </div>
        </div>

        <div class="content-area">
            <div class="container-padding">
                <h1 style="font-family: 'Rajdhani'; font-size: 3rem; margin-bottom: 30px; text-align: center; color: white; letter-spacing: 2px;">
                    NEXSCRIPT <span style="color:var(--primary);">HUB</span>
                </h1>

                <div class="script-card">
                    <img src="https://via.placeholder.com/600x320/0f1115/3b82f6?text=IMPERADOR+HUB+V1" class="script-thumb" onerror="this.src='https://via.placeholder.com/600x320?text=Script'">
                    <div class="script-info">
                        <h3>IMPERADOR HUB v1</h3>
                        <p style="color:var(--muted); font-size:0.9rem;">O melhor script para farm automático.</p>
                        
                        <div class="script-password">
                            <i class="fas fa-key"></i> Senha: <strong>imperio</strong>
                        </div>
                        
                        <button class="btn-action" onclick="copyScript()">
                            <i class="fas fa-copy"></i> COPIAR SCRIPT
                        </button>
                    </div>
                </div>

                <div class="pixel-message-container">
                    <div class="pixel-big">
                        EM BREVE<br>NOVOS SCRIPTS
                    </div>
                    <div class="pixel-small">
                        @gabriel.futury
                    </div>
                </div>
            </div>

            <footer>
                © 2024 NexScript Platform - Developed by @gabriel.futury
            </footer>
        </div>
    </div>

    <script>
        // Lógica Simplificada
        let users = JSON.parse(localStorage.getItem('nex_users')) || [];

        window.onload = function () {
            createSnow();
            checkSession();
        };

        function createSnow() {
            const container = document.getElementById('snow-container');
            for (let i = 0; i < 30; i++) {
                const flake = document.createElement('div');
                flake.className = 'snowflake';
                flake.style.left = Math.random() * 100 + 'vw';
                const size = Math.random() * 3 + 2;
                flake.style.width = flake.style.height = size + 'px';
                flake.style.animationDuration = (Math.random() * 3 + 5) + 's';
                flake.style.animationDelay = (Math.random() * 5) + 's';
                container.appendChild(flake);
            }
        }

        function toggleAuth(showRegister) {
            document.getElementById('login-box').classList.toggle('hidden', showRegister);
            document.getElementById('register-box').classList.toggle('hidden', !showRegister);
        }

        function handleLogin() {
            const email = document.getElementById('auth-email').value.trim();
            const pass = document.getElementById('auth-pass').value;
            const user = users.find(u => u.email === email && u.pass === pass);
            if (user) loginUser(user);
            else alert("Dados incorretos!");
        }

        function handleRegister() {
            const name = document.getElementById('reg-name').value.trim();
            const email = document.getElementById('reg-email').value.trim();
            const pass = document.getElementById('reg-pass').value;
            if(!name || !email || !pass) return alert("Preencha tudo.");
            
            const newUser = { name, email, pass };
            users.push(newUser);
            localStorage.setItem('nex_users', JSON.stringify(users));
            loginUser(newUser);
        }

        function loginUser(user) {
            localStorage.setItem('nex_session', JSON.stringify(user));
            enterApp();
        }

        function checkSession() {
            if (localStorage.getItem('nex_session')) enterApp();
        }

        function enterApp() {
            document.getElementById('gatekeeper').classList.add('hidden');
            document.getElementById('main-content').classList.remove('hidden');
        }

        function handleLogout() {
            localStorage.removeItem('nex_session');
            location.reload();
        }

        function copyScript() {
            const code = 'loadstring(game:HttpGet("https://raw.githubusercontent.com/leirbag975/IMPERADOR/refs/heads/main/.gitignore"))()';
            navigator.clipboard.writeText(code).then(() => alert("Script Copiado!"));
        }
    </script>
</body>
</html>
