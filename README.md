[<html lang="pt-br">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>NexScript | Plataforma</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=Rajdhani:wght@700&display=swap" rel="stylesheet" />
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
            overflow: hidden;
            position: relative;
            display: flex;
            flex-direction: column;
        }

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
            to {
                transform: translateY(105vh);
            }
        }

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

        .stats-counter {
            position: absolute;
            bottom: 20px;
            color: var(--muted);
            font-size: 0.8rem;
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .online-dot {
            width: 8px;
            height: 8px;
            background: #00ff88;
            border-radius: 50%;
            box-shadow: 0 0 10px #00ff88;
        }

        #main-content {
            flex: 1;
            display: flex;
            flex-direction: column;
            position: relative;
            z-index: 5;
        }

        header {
            padding: 12px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: var(--glass);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid var(--border);
            flex-shrink: 0;
        }

        /* Logo: no color in span so it does not affect tab title */
        .logo-mini {
            font-family: 'Rajdhani', sans-serif;
            font-size: 1.8rem;
            font-weight: 800;
            color: white;
            user-select: none;
        }

        /* Removed the color on span to avoid blue text in title */
        .logo-mini span {
            color: white; 
        }

        .user-pill {
            display: flex;
            align-items: center;
            gap: 12px;
            background: rgba(255, 255, 255, 0.03);
            padding: 6px 15px;
            border-radius: 50px;
            cursor: pointer;
            border: 1px solid transparent;
            transition: 0.3s;
            user-select: none;
        }

        .user-pill:hover {
            border-color: var(--primary);
            background: rgba(59, 130, 246, 0.1);
        }

        .user-pill img {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            object-fit: cover;
        }

        .user-id {
            font-size: 0.8rem;
            color: var(--accent);
            font-weight: bold;
            margin-right: 5px;
        }

        .dashboard-container {
            display: flex;
            flex: 1;
            overflow: hidden;
            min-height: 0;
            flex-direction: column;
        }

        .sidebar {
            width: 260px;
            background: rgba(10, 12, 16, 0.8);
            border-right: 1px solid var(--border);
            padding: 15px;
            display: flex;
            flex-direction: column;
            gap: 8px;
            flex-shrink: 0;
        }

        .nav-item {
            padding: 14px 20px;
            border-radius: 12px;
            color: var(--muted);
            cursor: pointer;
            transition: 0.3s;
            display: flex;
            align-items: center;
            gap: 12px;
            font-weight: 600;
            user-select: none;
        }

        .nav-item:hover,
        .nav-item.active {
            background: var(--primary);
            color: white;
            box-shadow: 0 5px 15px rgba(59, 130, 246, 0.3);
        }

        .content-area {
            flex: 1;
            padding: 20px 30px;
            overflow-y: auto;
            position: relative;
            min-height: 0;
            display: flex;
            flex-direction: column;
        }

        .content-area::-webkit-scrollbar {
            width: 6px;
        }

        .content-area::-webkit-scrollbar-track {
            background: transparent;
        }

        .content-area::-webkit-scrollbar-thumb {
            background: var(--primary);
            border-radius: 3px;
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
            user-select: none;
        }

        .btn-action:hover {
            background: var(--primary-dark);
            transform: translateY(-2px);
        }

        .btn-danger {
            background: rgba(255, 50, 50, 0.1);
            color: #ff3333;
            border: 1px solid #ff3333;
        }

        .btn-danger:hover {
            background: #ff3333;
            color: white;
        }

        .script-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
            flex-grow: 1;
        }

        .script-card {
            background: #0a0c10;
            border-radius: 16px;
            padding: 18px;
            border: 1px solid #1e293b;
            transition: 0.3s;
            position: relative;
            overflow: hidden;
            display: flex;
            flex-direction: column;
        }

        .script-card:hover {
            transform: translateY(-5px);
            border-color: var(--primary);
            box-shadow: 0 10px 30px rgba(59, 130, 246, 0.15);
        }

        .script-thumb {
            width: 100%;
            height: 140px;
            border-radius: 10px;
            margin-bottom: 14px;
            object-fit: cover;
            background: #111;
        }

        .script-card h3 {
            font-size: 1.3rem;
            margin-bottom: 6px;
            font-family: 'Rajdhani', sans-serif;
        }

        .script-author {
            font-size: 0.75rem;
            color: var(--muted);
            margin-bottom: 8px;
        }

        .script-password {
            display: flex;
            align-items: center;
            gap: 8px;
            background: rgba(0, 240, 255, 0.05);
            border: 1px solid rgba(0, 240, 255, 0.2);
            border-radius: 8px;
            padding: 8px 12px;
            margin-bottom: 14px;
        }

        .script-password i {
            color: var(--accent);
            font-size: 0.85rem;
        }

        .script-password span {
            font-size: 0.8rem;
            color: var(--muted);
        }

        .script-password strong {
            color: var(--accent);
            font-family: 'Rajdhani', sans-serif;
            font-size: 1rem;
            letter-spacing: 2px;
            user-select: all;
        }

        .input-group {
            margin-bottom: 15px;
        }

        .input-group label {
            display: block;
            margin-bottom: 6px;
            font-size: 0.8rem;
            color: var(--muted);
        }

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

        #toast {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            background: var(--panel);
            border: 1px solid var(--primary);
            padding: 12px 30px;
            border-radius: 50px;
            display: none;
            z-index: 10000;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
            font-weight: 600;
            user-select: none;
        }

        .profile-section {
            margin-top: 20px;
            display: flex;
            gap: 30px;
            align-items: flex-start;
        }

        .profile-section img {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            border: 2px solid var(--primary);
            flex-shrink: 0;
            object-fit: cover;
        }

        .profile-form {
            flex: 1;
            max-width: 400px;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .hidden {
            display: none !important;
        }

        footer {
            background: var(--panel);
            padding: 12px 30px;
            border-top: 1px solid var(--border);
            color: var(--muted);
            font-size: 0.8rem;
            text-align: center;
            flex-shrink: 0;
            user-select: none;
        }

        @media (max-width: 768px) {
            .sidebar {
                width: 60px;
                padding: 10px;
            }
            .nav-item span,
            .nav-item {
                font-size: 0;
                gap: 0;
                justify-content: center;
                padding: 14px;
            }
            .nav-item i {
                font-size: 1.2rem;
            }
            .content-area {
                padding: 15px;
            }
            .script-grid {
                grid-template-columns: 1fr;
            }
            .profile-section {
                flex-direction: column;
                align-items: center;
            }
        }
    </style>
</head>
<body>
    <div id="snow-container"></div>

    <div id="gatekeeper">
        <!-- LOGIN BOX -->
        <div class="auth-card" id="login-box">
            <h2>Acessar Sistema</h2>
            <div class="input-group">
                <input type="email" id="auth-email" class="input-field" placeholder="Seu E-mail" />
            </div>
            <div class="input-group">
                <input type="password" id="auth-pass" class="input-field" placeholder="Sua Senha" />
            </div>
            <button class="btn-action" onclick="handleLogin()">Conectar</button>
            <div style="display:flex;justify-content:space-between;margin-top:20px;font-size:0.85rem;">
                <a href="#" onclick="recoverAccount()" style="color:var(--muted);">Esqueci a senha</a>
                <a href="#" onclick="toggleAuth(true)" style="color:var(--primary);">Criar Conta</a>
            </div>
        </div>

        <!-- REGISTER BOX -->
        <div class="auth-card hidden" id="register-box">
            <h2>Nova Identidade</h2>
            <div class="input-group">
                <input type="text" id="reg-name" class="input-field" placeholder="Nome de Usuário" />
            </div>
            <div class="input-group">
                <input type="email" id="reg-email" class="input-field" placeholder="E-mail" />
            </div>
            <div class="input-group">
                <input type="password" id="reg-pass" class="input-field" placeholder="Senha (min. 6 dígitos)" />
            </div>
            <button class="btn-action" onclick="handleRegister()">Gerar ID e Entrar</button>
            <p style="margin-top:15px;text-align:center;font-size:0.85rem;">
                <a href="#" onclick="toggleAuth(false)" style="color:var(--muted);">Voltar para Login</a>
            </p>
        </div>

        <div class="stats-counter">
            <div class="online-dot"></div>
            <span id="user-count-display">Carregando usuários...</span>
        </div>
    </div>

    <div id="main-content" class="hidden" style="display:flex; flex-direction: column; height: 100vh;">
        <header>
            <div class="logo-mini">NEXSCRIPT</div>
            <div class="user-pill" onclick="showView('settings')">
                <span class="user-id" id="header-user-id">#0000</span>
                <span id="header-user-name">Usuário</span>
                <img id="header-user-pic" src="https://cdn-icons-png.flaticon.com/512/149/149071.png" />
            </div>
        </header>

        <div style="display: flex; flex: 1; overflow: hidden;">
            <div class="sidebar">
                <div class="nav-item active" onclick="showView('explore', this)">
                    <i class="fas fa-globe"></i> <span>Explorar</span>
                </div>
                <div class="nav-item" onclick="showView('settings', this)">
                    <i class="fas fa-cog"></i> <span>Perfil</span>
                </div>
                <div style="flex:1"></div>
                <div class="nav-item btn-danger" onclick="handleLogout()">
                    <i class="fas fa-power-off"></i> <span>Sair</span>
                </div>
            </div>

            <div class="content-area">
                <div id="view-explore" class="page-view" style="display:flex; flex-direction: column; flex-grow: 1;">
                    <h2 style="margin-bottom: 20px; border-bottom: 1px solid var(--border); padding-bottom: 10px;">
                        Scripts Disponíveis
                    </h2>
                    <div class="script-grid" id="scripts-container"></div>
                    
                    <!-- Rodapé dentro de explorar -->
                    <footer>
                        © 2024 NexScript - Todos os direitos reservados.
                    </footer>
                </div>

                <div id="view-settings" class="page-view hidden">
                    <h2>Meu Perfil</h2>
                    <div class="profile-section">
                        <img id="settings-pic" src="" alt="Foto do usuário" />
                        <div class="profile-form">
                            <div class="input-group">
                                <label>Seu ID (Imutável)</label>
                                <input type="text" id="settings-id" class="input-field" disabled style="opacity:0.5;" />
                            </div>
                            <div class="input-group">
                                <label>Nome de Exibição</label>
                                <input type="text" id="settings-name" class="input-field" />
                            </div>
                            <div class="input-group">
                                <label>URL da Foto de Perfil</label>
                                <input type="text" id="settings-pic-url" class="input-field" />
                            </div>
                            <button class="btn-action" onclick="saveProfile()">Salvar Perfil</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div id="toast">Notificação do Sistema</div>

    <script>
        let users = JSON.parse(localStorage.getItem('nex_users')) || [];
        let loggedUser = null;

        window.onload = function () {
            createSnow();
            checkSession();
            document.getElementById('user-count-display').innerText = 1420 + users.length + " hackers registrados globalmente";
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

        function checkSession() {
            const session = localStorage.getItem('nex_session');
            if (session) {
                const sessionData = JSON.parse(session);
                const user = users.find(u => u.id === sessionData.id);
                if (user) {
                    loggedUser = user;
                    enterApp();
                }
            }
        }

        function toggleAuth(showRegister) {
            document.getElementById('login-box').classList.toggle('hidden', showRegister);
            document.getElementById('register-box').classList.toggle('hidden', !showRegister);
        }

        function handleRegister() {
            const name = document.getElementById('reg-name').value.trim();
            const email = document.getElementById('reg-email').value.trim();
            const pass = document.getElementById('reg-pass').value;
            if (!name || !email || pass.length < 6) return notify("Preencha tudo corretamente.");
            if (users.find(u => u.email === email)) return notify("E-mail já cadastrado.");
            const newId = '#' + Math.floor(1000 + Math.random() * 9000);
            const newUser = { id: newId, name, email, pass, pic: 'https://cdn-icons-png.flaticon.com/512/149/149071.png' };
            users.push(newUser);
            localStorage.setItem('nex_users', JSON.stringify(users));
            loginUser(newUser);
        }

        function handleLogin() {
            const email = document.getElementById('auth-email').value.trim();
            const pass = document.getElementById('auth-pass').value;
            const user = users.find(u => u.email === email && u.pass === pass);
            if (user) loginUser(user);
            else notify("E-mail ou senha incorretos.");
        }

        function loginUser(user) {
            loggedUser = user;
            localStorage.setItem('nex_session', JSON.stringify(user));
            enterApp();
        }

        function handleLogout() {
            localStorage.removeItem('nex_session');
            location.reload();
        }

        function recoverAccount() {
            notify("Função em desenvolvimento.");
        }

        function enterApp() {
            document.getElementById('gatekeeper').classList.add('hidden');
            document.getElementById('main-content').classList.remove('hidden');
            document.getElementById('main-content').style.display = 'flex';
            document.getElementById('header-user-name').innerText = loggedUser.name;
            document.getElementById('header-user-id').innerText = loggedUser.id;
            document.getElementById('header-user-pic').src = loggedUser.pic;
            loadExplore();
            loadSettingsData();
        }

        function showView(viewId, btn) {
            document.querySelectorAll('.page-view').forEach(el => el.classList.add('hidden'));
            document.getElementById('view-' + viewId).classList.remove('hidden');
            if (btn) {
                document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));
                btn.classList.add('active');
            }
            if (viewId === 'settings') loadSettingsData();
        }

        function loadSettingsData() {
            if (!loggedUser) return;
            document.getElementById('settings-id').value = loggedUser.id;
            document.getElementById('settings-name').value = loggedUser.name;
            document.getElementById('settings-pic-url').value = loggedUser.pic;
            document.getElementById('settings-pic').src = loggedUser.pic;
        }

        function loadExplore() {
            const container = document.getElementById('scripts-container');
            container.innerHTML = `
                <div class="script-card">
                    <img src="https://via.placeholder.com/300x160/0f1115/3b82f6?text=IMPERADOR+HUB" class="script-thumb" onerror="this.src='https://via.placeholder.com/300x160?text=Script'">
                    <h3>IMPERADOR HUB v1</h3>
                    <p class="script-author">NexScript Oficial</p>
                    <div class="script-password">
                        <i class="fas fa-key"></i>
                        <span>Senha:</span>
                        <strong>imperio</strong>
                    </div>
                    <button class="btn-action" style="font-size:0.8rem;" onclick="copyScript()">
                        <i class="fas fa-copy"></i> Copiar Código
                    </button>
                </div>
            `;
        }

        function copyScript() {
            const code = 'loadstring(game:HttpGet("https://raw.githubusercontent.com/leirbag975/IMPERADOR/refs/heads/main/.gitignore"))()';
            if (navigator.clipboard) {
                navigator.clipboard.writeText(code).then(() => notify("Comando Copiado!"));
            } else {
                const el = document.createElement('textarea');
                el.value = code;
                document.body.appendChild(el);
                el.select();
                document.execCommand('copy');
                document.body.removeChild(el);
                notify("Comando Copiado!");
            }
        }

        function saveProfile() {
            const newName = document.getElementById('settings-name').value.trim();
            const newPic = document.getElementById('settings-pic-url').value.trim();
            if (!newName) return notify("Nome não pode ser vazio.");
            loggedUser.name = newName;
            loggedUser.pic = newPic || loggedUser.pic;
            const index = users.findIndex(u => u.id === loggedUser.id);
            users[index] = loggedUser;
            localStorage.setItem('nex_users', JSON.stringify(users));
            localStorage.setItem('nex_session', JSON.stringify(loggedUser));
            notify("Perfil Atualizado!");
            enterApp();
        }

        function notify(msg) {
            const t = document.getElementById('toast');
            t.innerText = msg;
            t.style.display = 'block';
            setTimeout(() => (t.style.display = 'none'), 3000);
        }
    </script>
</body>
</html>
](https://rewards.bing.com/welcome?rh=D599F4CF&ref=rafsrchae&form=ML2XE3&OCID=ML2XE3&PUBL=RewardsDO&CREA=ML2XE3)
