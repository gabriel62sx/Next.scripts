<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NexScript | Global</title>
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
            --glass: rgba(15, 17, 21, 0.85);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Plus Jakarta Sans', sans-serif; }
        
        body { 
            background: var(--bg); 
            color: var(--text); 
            height: 100vh; 
            overflow: hidden; 
            position: relative;
        }

        /* --- CORREÇÃO DO EFEITO DE NEVE (Não interfere no layout) --- */
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

        /* --- INTERFACE PRINCIPAL --- */
        #main-content { display: none; height: 100vh; display: flex; flex-direction: column; position: relative; z-index: 5; }

        header {
            padding: 15px 30px; display: flex; justify-content: space-between; align-items: center;
            background: var(--glass); backdrop-filter: blur(10px);
            border-bottom: 1px solid var(--border);
            height: 70px; flex-shrink: 0;
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

        /* --- DASHBOARD --- */
        .dashboard-container {
            display: flex; flex: 1; overflow: hidden; /* Importante para o scroll funcionar só no conteúdo */
        }

        .sidebar {
            width: 260px; background: rgba(10, 12, 16, 0.9); border-right: 1px solid var(--border);
            padding: 20px; display: flex; flex-direction: column; gap: 10px; flex-shrink: 0;
        }

        .nav-item { 
            padding: 14px 20px; border-radius: 12px; color: var(--muted); cursor: pointer; 
            transition: 0.3s; display: flex; align-items: center; gap: 12px; font-weight: 600;
        }
        .nav-item:hover, .nav-item.active { background: var(--primary); color: white; box-shadow: 0 5px 15px rgba(59, 130, 246, 0.3); }

        .content-area {
            flex: 1; padding: 30px; overflow-y: auto; position: relative;
            display: flex; flex-direction: column;
        }

        /* --- FOOTER (NOVIDADE) --- */
        footer {
            margin-top: auto; /* Empurra para o fundo */
            padding-top: 40px;
            padding-bottom: 10px;
            border-top: 1px solid var(--border);
            color: var(--muted);
            font-size: 0.8rem;
            text-align: center;
        }
        footer p span { color: var(--primary); font-weight: bold; }

        /* --- INPUTS E BOTÕES --- */
        .input-group { margin-bottom: 15px; }
        .input-group label { display: block; margin-bottom: 6px; font-size: 0.8rem; color: var(--muted); }
        .input-field {
            width: 100%; padding: 12px; background: rgba(0,0,0,0.3); border: 1px solid #1e293b;
            border-radius: 10px; color: white; outline: none; transition: 0.3s;
        }
        .input-field:focus { border-color: var(--primary); box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.2); }

        .btn-action {
            width: 100%; padding: 12px; background: var(--primary); color: white;
            border: none; border-radius: 10px; font-weight: 700; cursor: pointer; transition: 0.3s;
            text-transform: uppercase; font-size: 0.9rem; letter-spacing: 1px;
        }
        .btn-action:hover { background: var(--primary-dark); transform: translateY(-2px); }
        
        .btn-danger { background: rgba(255, 50, 50, 0.1); color: #ff3333; border: 1px solid #ff3333; }
        .btn-danger:hover { background: #ff3333; color: white; }

        /* --- SCRIPTS --- */
        .script-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 20px; }
        .script-card { 
            background: #0a0c10; border-radius: 16px; padding: 15px; border: 1px solid #1e293b; 
            transition: 0.3s; position: relative; overflow: hidden; display: flex; flex-direction: column;
        }
        .script-card:hover { transform: translateY(-5px); border-color: var(--primary); }
        .script-thumb { width: 100%; height: 150px; border-radius: 10px; margin-bottom: 12px; object-fit: cover; background: #111; }

        /* --- CHAT CORRIGIDO (Flechas Azuis) --- */
        .chat-container { 
            display: flex; height: calc(100vh - 140px); /* Altura fixa para não vazar */
            gap: 20px; overflow: hidden;
        }
        .chat-list { 
            width: 300px; border-right: 1px solid var(--border); padding-right: 20px; 
            display: flex; flex-direction: column;
        }
        .chat-window { 
            flex: 1; display: flex; flex-direction: column; 
            background: rgba(0,0,0,0.2); border-radius: 16px; 
            border: 1px solid var(--border); 
            overflow: hidden;
            position: relative; /* Para centralizar o placeholder */
        }
        
        /* Placeholder para quando não tem chat aberto */
        .chat-placeholder {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            color: var(--muted); text-align: center;
        }
        .chat-placeholder i { font-size: 4rem; margin-bottom: 20px; color: var(--border); }

        .messages-area { 
            flex: 1; padding: 20px; overflow-y: auto; 
            display: flex; flex-direction: column; gap: 10px; 
        }
        .msg { max-width: 70%; padding: 10px 15px; border-radius: 12px; font-size: 0.9rem; line-height: 1.4; word-wrap: break-word;}
        .msg.sent { align-self: flex-end; background: var(--primary); color: white; border-bottom-right-radius: 2px; }
        .msg.received { align-self: flex-start; background: #1e293b; color: #cbd5e1; border-bottom-left-radius: 2px; }
        
        .chat-input-area { padding: 15px; border-top: 1px solid var(--border); display: flex; gap: 10px; background: rgba(0,0,0,0.3); }

        /* --- TOAST --- */
        #toast {
            position: fixed; bottom: 30px; left: 50%; transform: translateX(-50%);
            background: var(--panel); border: 1px solid var(--primary);
            padding: 12px 30px; border-radius: 50px; display: none; z-index: 10000;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5); font-weight: 600;
        }

        .hidden { display: none !important; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes slideDown { from { transform: translateY(-50px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
    </style>
</head>
<body>

    <div id="snow-container"></div>

    <div id="gatekeeper">
        <div class="hero-title">
            <h1>NexScript</h1>
            <span>CONEXÃO GLOBAL</span>
        </div>

        <div class="auth-card" id="login-box">
            <h2 style="margin-bottom: 5px;">Acessar Sistema</h2>
            <p style="color: var(--muted); margin-bottom: 25px; font-size: 0.9rem;">Entre com suas credenciais.</p>
            
            <div class="input-group">
                <input type="email" id="auth-email" class="input-field" placeholder="Seu E-mail">
            </div>
            <div class="input-group">
                <input type="password" id="auth-pass" class="input-field" placeholder="Sua Senha">
            </div>
            
            <button class="btn-action" onclick="handleLogin()">Conectar</button>
            
            <div style="display: flex; justify-content: space-between; margin-top: 20px; font-size: 0.85rem;">
                <a href="#" onclick="alert('Dica: Crie uma conta nova!')" style="color: var(--muted);">Esqueci a senha</a>
                <a href="#" onclick="toggleAuth(true)" style="color: var(--primary);">Criar Conta</a>
            </div>
        </div>

        <div class="auth-card hidden" id="register-box">
            <h2 style="margin-bottom: 20px;">Nova Identidade</h2>
            <div class="input-group">
                <label>Como quer ser chamado?</label>
                <input type="text" id="reg-name" class="input-field" placeholder="Ex: MasterCoder">
            </div>
            <div class="input-group">
                <label>E-mail</label>
                <input type="email" id="reg-email" class="input-field" placeholder="exemplo@gmail.com">
            </div>
            <div class="input-group">
                <label>Senha Segura</label>
                <input type="password" id="reg-pass" class="input-field" placeholder="Mínimo 6 dígitos">
            </div>
            <button class="btn-action" onclick="handleRegister()">Gerar ID e Entrar</button>
            <p style="margin-top: 15px; text-align: center; font-size: 0.85rem;">
                <a href="#" onclick="toggleAuth(false)" style="color: var(--muted);">Voltar para Login</a>
            </p>
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
                <div class="nav-item" onclick="showView('publish', this)"><i class="fas fa-code"></i> Publicar</div>
                <div class="nav-item" onclick="showView('chat', this)"><i class="fab fa-whatsapp"></i> Chat Secreto</div>
                <div class="nav-item" onclick="showView('settings', this)"><i class="fas fa-cog"></i> Configurações</div>
                <div style="flex: 1"></div>
                <div class="nav-item btn-danger" onclick="handleLogout()"><i class="fas fa-power-off"></i> Sair</div>
            </div>

            <div class="content-area">
                
                <div id="view-explore" class="page-view">
                    <h2 style="margin-bottom: 20px; padding-bottom: 10px; border-bottom: 1px solid var(--border);">
                        Feed Global <span style="font-size: 0.8rem; color: var(--primary);">(Simulação Local)</span>
                    </h2>
                    <div class="script-grid" id="scripts-container"></div>
                </div>

                <div id="view-publish" class="page-view hidden">
                    <h2>Criar Novo Script</h2>
                    <p style="color: var(--muted); margin-bottom: 20px;">Compartilhe sua criação.</p>
                    
                    <div style="max-width: 600px;">
                        <div class="input-group">
                            <label>Título do Projeto</label>
                            <input type="text" id="script-title" class="input-field">
                        </div>
                        <div class="input-group">
                            <label>Link da Imagem (Capa)</label>
                            <input type="text" id="script-img-url" class="input-field" placeholder="https://...">
                        </div>
                        <div class="input-group">
                            <label>Código do Script</label>
                            <textarea id="script-code" class="input-field" style="height: 150px; font-family: monospace;"></textarea>
                        </div>
                        <button class="btn-action" onclick="submitScript()">Publicar</button>
                    </div>
                </div>

                <div id="view-chat" class="page-view hidden" style="height: 100%;">
                    <div class="chat-container">
                        <div class="chat-list">
                            <h3 style="margin-bottom: 15px;">Conversas</h3>
                            <div class="input-group">
                                <input type="text" id="new-chat-id" class="input-field" placeholder="Digite ID (ex: #1234)">
                                <button class="btn-action" onclick="startChat()" style="margin-top: 5px; padding: 8px;">Nova Conversa</button>
                            </div>
                            <div id="active-chats-list" style="margin-top: 20px; overflow-y: auto;">
                                </div>
                        </div>
                        
                        <div class="chat-window">
                            <div id="chat-empty-state" class="chat-placeholder">
                                <i class="fas fa-comments"></i>
                                <h3>Selecione uma conversa</h3>
                                <p>Ou inicie um novo chat com um ID.</p>
                            </div>

                            <div id="chat-content-box" class="hidden" style="display: flex; flex-direction: column; height: 100%;">
                                <div style="padding: 15px; border-bottom: 1px solid var(--border); background: rgba(0,0,0,0.4); display: flex; align-items: center; justify-content: space-between;">
                                    <h3 id="chat-header-name">Nome do Usuário</h3>
                                    <span style="font-size: 0.7rem; color: var(--primary);">CRIPTOGRAFADO</span>
                                </div>
                                <div class="messages-area" id="msg-area"></div>
                                <div class="chat-input-area">
                                    <input type="text" id="msg-input" class="input-field" placeholder="Digite sua mensagem...">
                                    <button class="btn-action" style="width: 60px;" onclick="sendMsg()"><i class="fas fa-paper-plane"></i></button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <div id="view-settings" class="page-view hidden">
                    <h2>Meu Perfil</h2>
                    <div style="margin-top: 30px; display: flex; gap: 30px; align-items: flex-start; flex-wrap: wrap;">
                        <img id="settings-pic" src="" style="width: 100px; height: 100px; border-radius: 50%; border: 2px solid var(--primary);">
                        <div style="flex: 1; min-width: 250px;">
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

                <footer>
                    <p>&copy; 2024 <span>NexScript</span>. Todos os direitos reservados.</p>
                    <p style="margin-top: 5px; opacity: 0.6;">Desenvolvido para conectar desenvolvedores.</p>
                </footer>

            </div>
        </div>
    </div>

    <div id="toast">Notificação</div>

    <script>
        // --- SISTEMA CORE ---
        let users = JSON.parse(localStorage.getItem('nex_users')) || [];
        let globalScripts = JSON.parse(localStorage.getItem('nex_global_scripts')) || [];
        let chats = JSON.parse(localStorage.getItem('nex_chats')) || {};
        let loggedUser = null;
        let currentChatID = null;

        // Dados de Exemplo (Para não ficar vazio)
        if(globalScripts.length === 0) {
            globalScripts.push({
                id: 1, title: 'Script de Login', author: 'Sistema', date: '12/10/2024', img: 'https://via.placeholder.com/300/000000/FFFFFF/?text=LOGIN', code: 'console.log("Hello World");'
            });
        }

        // --- INICIALIZAÇÃO ---
        window.onload = function() {
            createSnow();
            checkSession();
        };

        function createSnow() {
            const container = document.getElementById('snow-container');
            for(let i=0; i<30; i++) {
                const flake = document.createElement('div');
                flake.className = 'snowflake';
                flake.style.left = Math.random() * 100 + 'vw';
                flake.style.width = flake.style.height = (Math.random() * 3 + 2) + 'px';
                flake.style.animationDuration = (Math.random() * 3 + 5) + 's';
                flake.style.animationDelay = Math.random() * 5 + 's';
                container.appendChild(flake);
            }
        }

        // --- AUTH ---
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

            if(!name || !email || pass.length < 6) return notify("Preencha tudo! Senha min. 6 dígitos.");
            if(users.find(u => u.email === email)) return notify("E-mail já registrado.");

            const newId = '#' + Math.floor(1000 + Math.random() * 9000);
            const newUser = { id: newId, name, email, pass, pic: 'https://cdn-icons-png.flaticon.com/512/149/149071.png' };

            users.push(newUser);
            localStorage.setItem('nex_users', JSON.stringify(users));
            loginUser(newUser);
            notify("Bem-vindo! Seu ID é: " + newId);
        }

        function handleLogin() {
            const email = document.getElementById('auth-email').value;
            const pass = document.getElementById('auth-pass').value;
            const user = users.find(u => u.email === email && u.pass === pass);
            if(user) loginUser(user);
            else notify("Credenciais inválidas.");
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
            
            document.getElementById('header-user-name').innerText = loggedUser.name;
            document.getElementById('header-user-id').innerText = loggedUser.id;
            document.getElementById('header-user-pic').src = loggedUser.pic;

            loadExplore();
            loadChatsList();
        }

        function showView(viewId, btn) {
            document.querySelectorAll('.page-view').forEach(el => el.classList.add('hidden'));
            document.getElementById('view-' + viewId).classList.remove('hidden');
            if(btn) {
                document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));
                btn.classList.add('active');
            }
        }

        // --- SCRIPTS ---
        function submitScript() {
            const title = document.getElementById('script-title').value;
            const code = document.getElementById('script-code').value;
            const img = document.getElementById('script-img-url').value || 'https://via.placeholder.com/300/000000/FFFFFF/?text=CODE';

            if(!title || !code) return notify("Título e código são obrigatórios.");

            const newScript = {
                id: Date.now(), title, code, img,
                author: loggedUser.name, authorId: loggedUser.id,
                date: new Date().toLocaleDateString()
            };

            globalScripts.unshift(newScript);
            localStorage.setItem('nex_global_scripts', JSON.stringify(globalScripts));
            
            notify("Script publicado!");
            document.getElementById('script-title').value = '';
            document.getElementById('script-code').value = '';
            showView('explore');
            loadExplore();
        }

        function loadExplore() {
            const container = document.getElementById('scripts-container');
            container.innerHTML = globalScripts.map(s => `
                <div class="script-card">
                    <img src="${s.img}" class="script-thumb">
                    <h3 style="font-size: 1.1rem; margin-bottom: 5px;">${s.title}</h3>
                    <div style="display: flex; justify-content: space-between; font-size: 0.8rem; color: var(--muted); margin-bottom: 10px;">
                        <span><i class="fas fa-user"></i> ${s.author}</span>
                        <span>${s.date}</span>
                    </div>
                    <button class="btn-action" style="padding: 8px; font-size: 0.8rem; margin-top: auto;" onclick="notify('Código copiado!')">
                        <i class="fas fa-copy"></i> Copiar Código
                    </button>
                </div>
            `).join('');
        }

        // --- CHAT SYSTEM ---
        function startChat() {
            const targetId = document.getElementById('new-chat-id').value;
            if(!targetId.startsWith('#')) return notify("O ID deve começar com #");
            if(targetId === loggedUser.id) return notify("Você não pode conversar consigo mesmo.");

            const chatKey = [loggedUser.id, targetId].sort().join('_');
            
            if(!chats[chatKey]) {
                chats[chatKey] = { members: [loggedUser.id, targetId], messages: [] };
                localStorage.setItem('nex_chats', JSON.stringify(chats));
            }

            loadChatsList();
            openChat(chatKey, targetId);
        }

        function loadChatsList() {
            const list = document.getElementById('active-chats-list');
            list.innerHTML = '';
            Object.keys(chats).forEach(key => {
                const chat = chats[key];
                if(chat.members.includes(loggedUser.id)) {
                    const otherId = chat.members.find(id => id !== loggedUser.id);
                    list.innerHTML += `
                        <div class="nav-item" onclick="openChat('${key}', '${otherId}')" style="justify-content: space-between; margin-bottom: 5px;">
                            <span><i class="fas fa-user-secret"></i> ${otherId}</span>
                            <i class="fas fa-chevron-right" style="font-size: 0.7rem;"></i>
                        </div>
                    `;
                }
            });
        }

        function openChat(chatKey, otherId) {
            currentChatID = chatKey;
            
            // Esconde o placeholder e mostra o chat
            document.getElementById('chat-empty-state').classList.add('hidden');
            const contentBox = document.getElementById('chat-content-box');
            contentBox.classList.remove('hidden');
            // Força o display flex para corrigir o layout
            contentBox.style.display = 'flex'; 

            document.getElementById('chat-header-name').innerText = "Conversando com " + otherId;
            renderMessages();
        }

        function sendMsg() {
            const input = document.getElementById('msg-input');
            const txt = input.value;
            if(!txt) return;

            chats[currentChatID].messages.push({
                sender: loggedUser.id, text: txt, time: new Date().toLocaleTimeString()
            });
            
            localStorage.setItem('nex_chats', JSON.stringify(chats));
            input.value = '';
            renderMessages();
        }

        function renderMessages() {
            if(!currentChatID) return;
            const area = document.getElementById('msg-area');
            const msgs = chats[currentChatID].messages;
            
            area.innerHTML = msgs.map(m => `
                <div class="msg ${m.sender === loggedUser.id ? 'sent' : 'received'}">
                    ${m.text}
                    <div style="font-size: 0.6rem; opacity: 0.7; margin-top: 4px; text-align: right;">${m.time}</div>
                </div>
            `).join('');
            
            area.scrollTop = area.scrollHeight;
        }

        // --- SETTINGS ---
        function saveProfile() {
            const newName = document.getElementById('settings-name').value;
            const newPic = document.getElementById('settings-pic-url').value;
            
            if(newName) loggedUser.name = newName;
            if(newPic) loggedUser.pic = newPic;

            const index = users.findIndex(u => u.id === loggedUser.id);
            if(index !== -1) {
                users[index] = loggedUser;
                localStorage.setItem('nex_users', JSON.stringify(users));
                localStorage.setItem('nex_session', JSON.stringify(loggedUser));
            }
            
            notify("Perfil salvo!");
            enterApp();
        }

        // --- UTILS ---
        function notify(msg) {
            const t = document.getElementById('toast');
            t.innerText = msg;
            t.style.display = 'block';
            t.style.animation = 'slideDown 0.3s forwards';
            setTimeout(() => t.style.display = 'none', 3000);
        }

        // Carrega configurações ao focar
        document.getElementById('settings-name').addEventListener('focus', () => {
             document.getElementById('settings-id').value = loggedUser.id;
             document.getElementById('settings-name').value = loggedUser.name;
             document.getElementById('settings-pic-url').value = loggedUser.pic;
             document.getElementById('settings-pic').src = loggedUser.pic;
        });
    </script>
</body>
</html>
