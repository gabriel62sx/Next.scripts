<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NexScript | Plataforma</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=Rajdhani:wght@700&display=swap" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
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

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Plus Jakarta Sans', sans-serif; }
        
        body { 
            background: var(--bg); 
            color: var(--text); 
            height: 100vh; 
            overflow: hidden; 
            position: relative;
        }

        /* --- EFEITO DE NEVE --- */
        #snow-container {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none; z-index: 1; overflow: hidden;
        }
        .snowflake {
            position: absolute; top: -10px; background: white;
            border-radius: 50%; opacity: 0.8;
            animation: fall linear infinite;
        }
        @keyframes fall {
            to { transform: translateY(105vh); }
        }

        /* --- TELA DE LOGIN --- */
        #gatekeeper {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: var(--bg); z-index: 9999;
            display: flex; flex-direction: column;
            justify-content: center; align-items: center;
            background-image: radial-gradient(circle at 50% 50%, #111b33 0%, #000 80%);
        }

        .hero-title {
            text-align: center; margin-bottom: 40px; z-index: 10;
            animation: slideDown 0.8s ease-out;
        }
        .hero-title h1 {
            font-family: 'Rajdhani', sans-serif;
            font-size: 5rem; line-height: 0.8;
            text-transform: uppercase;
            background: linear-gradient(to right, #fff, var(--primary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 30px rgba(59, 130, 246, 0.5);
        }
        .hero-title span {
            font-size: 1.2rem; letter-spacing: 10px; color: var(--accent);
            text-transform: uppercase; font-weight: 600; display: block; margin-top: 10px;
        }

        .auth-card {
            background: rgba(15, 17, 21, 0.6); backdrop-filter: blur(20px);
            border: 1px solid var(--border);
            padding: 40px; border-radius: 24px; width: 90%; max-width: 400px;
            box-shadow: 0 0 50px rgba(0,0,0,0.8);
            z-index: 10; position: relative;
            animation: fadeIn 1s ease;
        }

        .stats-counter {
            position: absolute; bottom: 20px; color: var(--muted); font-size: 0.8rem;
            display: flex; gap: 10px; align-items: center;
        }
        .online-dot { width: 8px; height: 8px; background: #00ff88; border-radius: 50%; box-shadow: 0 0 10px #00ff88; }

        /* --- INTERFACE PRINCIPAL --- */
        #main-content { display: none; height: 100vh; display: flex; flex-direction: column; position: relative; z-index: 5; }

        header {
            padding: 15px 30px; display: flex; justify-content: space-between; align-items: center;
            background: var(--glass); backdrop-filter: blur(10px);
            border-bottom: 1px solid var(--border);
        }

        .logo-mini { font-family: 'Rajdhani', sans-serif; font-size: 1.8rem; font-weight: 800; color: white; }
        .logo-mini span { color: var(--primary); }

        .user-pill {
            display: flex; align-items: center; gap: 12px; background: rgba(255,255,255,0.03);
            padding: 6px 15px; border-radius: 50px; cursor: pointer; border: 1px solid transparent; transition: 0.3s;
        }
        .user-pill:hover { border-color: var(--primary); background: rgba(59, 130, 246, 0.1); }
        .user-pill img { width: 35px; height: 35px; border-radius: 50%; object-fit: cover; }
        .user-id { font-size: 0.8rem; color: var(--accent); font-weight: bold; margin-right: 5px; }

        .dashboard-container { display: flex; flex: 1; overflow: hidden; }

        .sidebar {
            width: 260px; background: rgba(10, 12, 16, 0.8); border-right: 1px solid var(--border);
            padding: 20px; display: flex; flex-direction: column; gap: 10px;
        }

        .nav-item { 
            padding: 14px 20px; border-radius: 12px; color: var(--muted); cursor: pointer; 
            transition: 0.3s; display: flex; align-items: center; gap: 12px; font-weight: 600;
        }
        .nav-item:hover, .nav-item.active { background: var(--primary); color: white; box-shadow: 0 5px 15px rgba(59, 130, 246, 0.3); }

        .content-area { flex: 1; padding: 30px; overflow-y: auto; position: relative; }

        .btn-action {
            width: 100%; padding: 12px; background: var(--primary); color: white;
            border: none; border-radius: 10px; font-weight: 700; cursor: pointer; transition: 0.3s;
            text-transform: uppercase; font-size: 0.9rem; letter-spacing: 1px;
        }
        .btn-action:hover { background: var(--primary-dark); transform: translateY(-2px); }
        
        .btn-danger { background: rgba(255, 50, 50, 0.1); color: #ff3333; border: 1px solid #ff3333; }
        .btn-danger:hover { background: #ff3333; color: white; }

        .script-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); gap: 20px; }
        .script-card { 
            background: #0a0c10; border-radius: 16px; padding: 15px; border: 1px solid #1e293b; 
            transition: 0.3s; position: relative; overflow: hidden;
        }
        .script-card:hover { transform: translateY(-5px); border-color: var(--primary); }
        .script-thumb { width: 100%; height: 140px; border-radius: 10px; margin-bottom: 12px; object-fit: cover; background: #111; }

        /* --- INPUTS PERFIL --- */
        .input-group { margin-bottom: 15px; }
        .input-group label { display: block; margin-bottom: 6px; font-size: 0.8rem; color: var(--muted); }
        .input-field {
            width: 100%; padding: 12px; background: rgba(0,0,0,0.3); border: 1px solid #1e293b;
            border-radius: 10px; color: white; outline: none; transition: 0.3s;
        }

        #toast {
            position: fixed; bottom: 30px; left: 50%; transform: translateX(-50%);
            background: var(--panel); border: 1px solid var(--primary);
            padding: 12px 30px; border-radius: 50px; display: none; z-index: 10000;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5); font-weight: 600;
        }

        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes slideDown { from { transform: translateY(-50px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div id="snow-container"></div>

    <div id="gatekeeper">
        <div class="hero-title">
            <h1>NexScript</h1>
            <span>PROJECT REVOLUTION</span>
        </div>

        <div class="auth-card" id="login-box">
            <h2 style="margin-bottom: 5px;">Acessar Sistema</h2>
            <div class="input-group">
                <input type="email" id="auth-email" class="input-field" placeholder="Seu E-mail">
            </div>
            <div class="input-group">
                <input type="password" id="auth-pass" class="input-field" placeholder="Sua Senha">
            </div>
            <button class="btn-action" onclick="handleLogin()">Conectar</button>
            <div style="display: flex; justify-content: space-between; margin-top: 20px; font-size: 0.85rem;">
                <a href="#" onclick="recoverAccount()" style="color: var(--muted);">Esqueci a senha</a>
                <a href="#" onclick="toggleAuth(true)" style="color: var(--primary);">Criar Conta</a>
            </div>
        </div>

        <div class="auth-card hidden" id="register-box">
            <h2 style="margin-bottom: 20px;">Nova Identidade</h2>
            <div class="input-group">
                <input type="text" id="reg-name" class="input-field" placeholder="Nome de Usuário">
            </div>
            <div class="input-group">
                <input type="email" id="reg-email" class="input-field" placeholder="E-mail">
            </div>
            <div class="input-group">
                <input type="password" id="reg-pass" class="input-field" placeholder="Senha (min. 6 dígitos)">
            </div>
            <button class="btn-action" onclick="handleRegister()">Gerar ID e Entrar</button>
            <p style="margin-top: 15px; text-align: center; font-size: 0.85rem;">
                <a href="#" onclick="toggleAuth(false)" style="color: var(--muted);">Voltar para Login</a>
            </p>
        </div>

        <div class="stats-counter">
            <div class="online-dot"></div>
            <span id="user-count-display">Carregando usuários...</span>
        </div>
    </div>

    <div id="main-content" class="hidden">
        <header>
            <div class="logo-mini">NEX<span>SCRIPT</span></div>
            <div class="user-pill" onclick="showView('settings')">
                <span class="user-id" id="header-user-id">#0000</span>
                <span id="header-user-name">Usuário</span>
                <img id="header-user-pic" src="https://cdn-icons-png.flaticon.com/512/149/149071.png">
            </div>
        </header>

        <div class="dashboard-container">
            <div class="sidebar">
                <div class="nav-item active" onclick="showView('explore', this)"><i class="fas fa-globe"></i> Explorar</div>
                <div class="nav-item" onclick="showView('settings', this)"><i class="fas fa-cog"></i> Perfil</div>
                <div style="flex: 1"></div>
                <div class="nav-item btn-danger" onclick="handleLogout()"><i class="fas fa-power-off"></i> Sair</div>
            </div>

            <div class="content-area">
                <div id="view-explore" class="page-view">
                    <h2 style="margin-bottom: 20px; border-bottom: 1px solid var(--border); padding-bottom: 10px;">Scripts Disponíveis</h2>
                    <div class="script-grid" id="scripts-container"></div>
                </div>

                <div id="view-settings" class="page-view hidden">
                    <h2>Meu Perfil</h2>
                    <div style="margin-top: 30px; display: flex; gap: 30px; align-items: flex-start;">
                        <img id="settings-pic" src="" style="width: 100px; height: 100px; border-radius: 50%; border: 2px solid var(--primary);">
                        <div style="flex: 1; max-width: 400px;">
                            <div class="input-group">
                                <label>Seu ID (Imutável)</label>
                                <input type="text" id="settings-id" class="input-field" disabled style="opacity: 0.5;">
                            </div>
                            <div class="input-group">
                                <label>Nome de Exibição</label>
                                <input type="text" id="settings-name" class="input-field">
                            </div>
                            <div class="input-group">
                                <label>URL da Foto de Perfil</label>
                                <input type="text" id="settings-pic-url" class="input-field">
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
        // Scripts fixos para exibição já que a opção de publicar foi removida
        let defaultScripts = [
            { id: 1, title: "IMPERADOR HUB v1", author: "NexTeam", img: "https://via.placeholder.com/300/0f1115/ffffff/?text=IMPERADOR+v1" },
            { id: 2, title: "AUTO-FARM ELITE", author: "NexTeam", img: "https://via.placeholder.com/300/0f1115/ffffff/?text=FARM+ELITE" },
            { id: 3, title: "PVP GOD MODE", author: "NexTeam", img: "https://via.placeholder.com/300/0f1115/ffffff/?text=GOD+MODE" }
        ];
        let loggedUser = null;

        window.onload = function() {
            createSnow();
            checkSession();
            document.getElementById('user-count-display').innerText = (1420 + users.length) + " hackers registrados globalmente";
        };

        function createSnow() {
            const container = document.getElementById('snow-container');
            for(let i=0; i<30; i++) {
                const flake = document.createElement('div');
                flake.className = 'snowflake';
                flake.style.left = Math.random() * 100 + 'vw';
                flake.style.width = flake.style.height = (Math.random() * 3 + 2) + 'px';
                flake.style.animationDuration = (Math.random() * 3 + 5) + 's';
                container.appendChild(flake);
            }
        }

        function checkSession() {
            const session = localStorage.getItem('nex_session');
            if(session) {
                const sessionData = JSON.parse(session);
                const user = users.find(u => u.id === sessionData.id);
                if(user) { loggedUser = user; enterApp(); }
            }
        }

        function toggleAuth(showRegister) {
            document.getElementById('login-box').classList.toggle('hidden', showRegister);
            document.getElementById('register-box').classList.toggle('hidden', !showRegister);
        }

        function handleRegister() {
            const name = document.getElementById('reg-name').value;
            const email = document.getElementById('reg-email').value;
            const pass = document.getElementById('reg-pass').value;
            if(!name || !email || pass.length < 6) return notify("Erro nos dados.");
            const newId = '#' + Math.floor(1000 + Math.random() * 9000);
            const newUser = { id: newId, name, email, pass, pic: 'https://cdn-icons-png.flaticon.com/512/149/149071.png' };
            users.push(newUser);
            localStorage.setItem('nex_users', JSON.stringify(users));
            loginUser(newUser);
        }

        function handleLogin() {
            const email = document.getElementById('auth-email').value;
            const pass = document.getElementById('auth-pass').value;
            const user = users.find(u => u.email === email && u.pass === pass);
            if(user) loginUser(user);
            else notify("Incorreto.");
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

        function enterApp() {
            document.getElementById('gatekeeper').classList.add('hidden');
            document.getElementById('main-content').classList.remove('hidden');
            document.getElementById('main-content').style.display = 'flex';
            document.getElementById('header-user-name').innerText = loggedUser.name;
            document.getElementById('header-user-id').innerText = loggedUser.id;
            document.getElementById('header-user-pic').src = loggedUser.pic;
            loadExplore();
        }

        function showView(viewId, btn) {
            document.querySelectorAll('.page-view').forEach(el => el.classList.add('hidden'));
            document.getElementById('view-' + viewId).classList.remove('hidden');
            if(btn) {
                document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));
                btn.classList.add('active');
            }
        }

        function loadExplore() {
            const container = document.getElementById('scripts-container');
            container.innerHTML = defaultScripts.map(s => `
                <div class="script-card">
                    <img src="${s.img}" class="script-thumb" onerror="this.src='https://via.placeholder.com/300?text=Script'">
                    <h3>${s.title}</h3>
                    <p style="font-size:0.7rem; color:var(--muted); margin-bottom:10px;">NexScript Oficial</p>
                    <button class="btn-action" style="font-size:0.8rem;" onclick="copyScript()">
                        <i class="fas fa-copy"></i> Copiar Código
                    </button>
                </div>
            `).join('');
        }

        function copyScript() {
            const code = 'loadstring(game:HttpGet("https://raw.githubusercontent.com/leirbag975/IMPERADOR/refs/heads/main/.gitignore"))()';
            const el = document.createElement('textarea');
            el.value = code;
            document.body.appendChild(el);
            el.select();
            document.execCommand('copy');
            document.body.removeChild(el);
            notify("Comando Copiado!");
        }

        function saveProfile() {
            loggedUser.name = document.getElementById('settings-name').value;
            loggedUser.pic = document.getElementById('settings-pic-url').value;
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
            setTimeout(() => t.style.display = 'none', 3000);
        }

        document.getElementById('settings-name').addEventListener('focus', () => {
             document.getElementById('settings-id').value = loggedUser.id;
             document.getElementById('settings-name').value = loggedUser.name;
             document.getElementById('settings-pic-url').value = loggedUser.pic;
             document.getElementById('settings-pic').src = loggedUser.pic;
        });
    </script>
</body>
</html>
