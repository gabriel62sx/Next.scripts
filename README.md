<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NexScript | Privado</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        :root {
            --bg: #030508;
            --panel: #0a0d14;
            --primary: #2962ff;
            --accent: #00e5ff;
            --text: #ffffff;
            --muted: #64748b;
            --error: #ff3333;
            --border: rgba(41, 98, 255, 0.1);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Plus Jakarta Sans', sans-serif; }
        body { background: var(--bg); color: var(--text); overflow-x: hidden; }

        /* --- TELA DE ACESSO INICIAL (FORÇADA) --- */
        #gatekeeper {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: var(--bg); z-index: 9999;
            display: flex; justify-content: center; align-items: center;
            background-image: radial-gradient(circle at center, #111b33 0%, var(--bg) 70%);
        }

        .auth-card {
            background: var(--panel); border: 1px solid var(--border);
            padding: 40px; border-radius: 24px; width: 100%; max-width: 420px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.5);
            animation: fadeIn 0.6s ease;
        }

        /* --- INTERFACE PRINCIPAL --- */
        #main-content { display: none; } /* Escondido até logar */

        header {
            padding: 15px 5%; display: flex; justify-content: space-between; align-items: center;
            background: rgba(10, 13, 20, 0.8); backdrop-filter: blur(10px);
            border-bottom: 1px solid var(--border); position: sticky; top: 0; z-index: 100;
        }

        .logo { font-weight: 800; font-size: 1.5rem; letter-spacing: -1px; }
        .logo span { color: var(--primary); text-shadow: 0 0 10px var(--primary); }

        .user-pill {
            display: flex; align-items: center; gap: 12px; background: rgba(255,255,255,0.05);
            padding: 5px 15px; border-radius: 50px; cursor: pointer; border: 1px solid transparent;
        }
        .user-pill:hover { border-color: var(--primary); }
        .user-pill img { width: 32px; height: 32px; border-radius: 50%; object-fit: cover; background: #222; }

        /* --- DASHBOARD --- */
        .dashboard { max-width: 1200px; margin: 40px auto; padding: 0 20px; display: grid; grid-template-columns: 280px 1fr; gap: 30px; }

        .sidebar-nav { display: flex; flex-direction: column; gap: 10px; }
        .nav-item { 
            padding: 12px 20px; border-radius: 12px; color: var(--muted); cursor: pointer; 
            transition: 0.3s; display: flex; align-items: center; gap: 12px;
        }
        .nav-item:hover, .nav-item.active { background: var(--primary); color: white; }

        .content-area { background: var(--panel); border-radius: 24px; border: 1px solid var(--border); padding: 30px; min-height: 600px; }

        /* --- TABS DO EXPLORER --- */
        .explorer-tabs { display: flex; gap: 15px; margin-bottom: 25px; border-bottom: 1px solid #1e293b; padding-bottom: 10px; }
        .tab-btn {
            background: transparent; border: none; color: var(--muted); font-weight: 600; cursor: pointer; padding: 8px 16px; border-radius: 8px; transition: 0.3s;
        }
        .tab-btn.active { background: rgba(41, 98, 255, 0.1); color: var(--primary); }
        .tab-btn:hover { color: white; }

        /* --- FORMULÁRIOS --- */
        .input-group { margin-bottom: 20px; }
        .input-group label { display: block; margin-bottom: 8px; font-size: 0.85rem; color: var(--muted); }
        .input-field {
            width: 100%; padding: 14px; background: #05070a; border: 1px solid #1e293b;
            border-radius: 12px; color: white; outline: none; transition: 0.3s;
        }
        .input-field:focus { border-color: var(--primary); box-shadow: 0 0 0 4px rgba(41, 98, 255, 0.1); }

        .btn-action {
            width: 100%; padding: 14px; background: var(--primary); color: white;
            border: none; border-radius: 12px; font-weight: 700; cursor: pointer; transition: 0.3s;
        }
        .btn-action:hover { opacity: 0.9; transform: translateY(-2px); }

        /* --- CONFIGURAÇÕES DE PERFIL --- */
        .profile-edit { display: flex; flex-direction: column; align-items: center; gap: 20px; }
        .profile-pic-upload {
            width: 120px; height: 120px; border-radius: 50%; border: 2px dashed var(--primary);
            display: flex; justify-content: center; align-items: center; cursor: pointer;
            overflow: hidden; position: relative;
        }
        .profile-pic-upload img { width: 100%; height: 100%; object-fit: cover; }
        .profile-pic-upload i { position: absolute; font-size: 1.5rem; color: var(--primary); background: rgba(0,0,0,0.5); padding: 10px; border-radius: 50%; opacity: 0; transition: 0.3s; }
        .profile-pic-upload:hover i { opacity: 1; }

        /* --- SCRIPTS GRID --- */
        .script-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 20px; }
        .script-card { background: #05070a; border-radius: 16px; padding: 15px; border: 1px solid #1e293b; position: relative; }
        .script-thumb { width: 100%; height: 150px; border-radius: 10px; margin-bottom: 15px; object-fit: cover; }
        .badge-private { position: absolute; top: 10px; right: 10px; background: #000; color: var(--accent); padding: 4px 8px; border-radius: 4px; font-size: 0.7rem; font-weight: bold; }

        /* --- TOAST --- */
        #toast {
            position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%);
            background: var(--panel); border: 1px solid var(--primary);
            padding: 12px 30px; border-radius: 50px; display: none; z-index: 10000;
        }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>

    <div id="gatekeeper">
        <div class="auth-card" id="login-box">
            <h1 style="margin-bottom: 10px; text-align: center;">NEX<span>SCRIPT</span></h1>
            <p style="text-align: center; color: var(--muted); margin-bottom: 30px;">Acesse sua conta para continuar</p>
            
            <div class="input-group">
                <label>E-mail Google</label>
                <input type="email" id="auth-email" class="input-field" placeholder="exemplo@gmail.com">
            </div>
            <div class="input-group">
                <label>Senha</label>
                <input type="password" id="auth-pass" class="input-field" placeholder="••••••••">
            </div>
            <button class="btn-action" onclick="handleLogin()">Entrar na Plataforma</button>
            <p style="margin-top: 20px; text-align: center; font-size: 0.9rem;">
                Novo por aqui? <a href="javascript:void(0)" onclick="toggleAuth(true)" style="color: var(--primary); text-decoration: none;">Criar conta real</a>
            </p>
        </div>

        <div class="auth-card" id="register-box" style="display: none;">
            <h2 style="margin-bottom: 25px;">Registrar Agora</h2>
            <div class="input-group">
                <label>Nome Completo</label>
                <input type="text" id="reg-name" class="input-field" placeholder="Como quer ser chamado?">
            </div>
            <div class="input-group">
                <label>E-mail Real (Google)</label>
                <input type="email" id="reg-email" class="input-field" placeholder="exemplo@gmail.com">
            </div>
            <div class="input-group">
                <label>Crie uma Senha</label>
                <input type="password" id="reg-pass" class="input-field" placeholder="Mínimo 6 dígitos">
            </div>
            <button class="btn-action" onclick="handleRegister()">Finalizar Registro</button>
            <p style="margin-top: 20px; text-align: center; font-size: 0.9rem;">
                Já tem conta? <a href="javascript:void(0)" onclick="toggleAuth(false)" style="color: var(--primary); text-decoration: none;">Fazer Login</a>
            </p>
        </div>
    </div>

    <div id="main-content">
        <header>
            <div class="logo">NEX<span>SCRIPT</span></div>
            <div class="user-pill" onclick="showView('settings')">
                <span id="header-user-name">Usuário</span>
                <img id="header-user-pic" src="https://cdn-icons-png.flaticon.com/512/149/149071.png">
            </div>
        </header>

        <div class="dashboard">
            <div class="sidebar-nav">
                <div class="nav-item active" onclick="showView('explore', this)"><i class="fas fa-compass"></i> Explorar</div>
                <div class="nav-item" onclick="showView('publish', this)"><i class="fas fa-plus-circle"></i> Publicar Script</div>
                <div class="nav-item" onclick="showView('settings', this)"><i class="fas fa-user-gear"></i> Configurações</div>
                <div class="nav-item" onclick="handleLogout()" style="margin-top: 50px; color: var(--error);"><i class="fas fa-sign-out-alt"></i> Sair</div>
            </div>

            <div class="content-area">
                <div id="view-explore" class="page-view">
                    <div class="explorer-tabs">
                        <button class="tab-btn active" onclick="switchExploreTab('global', this)">🌍 Feed Global</button>
                        <button class="tab-btn" onclick="switchExploreTab('private', this)">🔒 Meus Scripts (Armazém)</button>
                    </div>

                    <h2 style="margin-bottom: 20px;" id="explore-title">Scripts Publicados Globalmente</h2>
                    <div class="script-grid" id="scripts-container">
                        </div>
                </div>

                <div id="view-publish" class="page-view" style="display: none;">
                    <h2>Lançar Novo Script</h2>
                    <p style="color: var(--muted); margin-bottom: 30px;">Preencha os dados abaixo.</p>
                    
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 30px;">
                        <div>
                            <div class="input-group">
                                <label>Título do Projeto</label>
                                <input type="text" id="script-title" class="input-field">
                            </div>
                            <div class="input-group">
                                <label>Visibilidade (Onde publicar?)</label>
                                <select id="script-visibility" class="input-field">
                                    <option value="global">🌍 Público Global (Todos veem)</option>
                                    <option value="private">🔒 Privado Local (Armazém Pessoal)</option>
                                </select>
                            </div>
                            <div class="input-group">
                                <label>Link Showcase (YouTube)</label>
                                <input type="text" id="script-yt" class="input-field" placeholder="https://youtube.com/...">
                            </div>
                        </div>
                        <div>
                            <label class="form-label">Capa do Script</label>
                            <input type="file" id="script-file" hidden onchange="processScriptImg(this)">
                            <div class="profile-pic-upload" onclick="document.getElementById('script-file').click()" style="width: 100%; border-radius: 12px;">
                                <img id="script-preview" src="">
                                <i class="fas fa-upload" style="opacity: 1;"></i>
                            </div>
                        </div>
                    </div>
                    <div class="input-group">
                        <label>Código Raw</label>
                        <textarea id="script-raw" class="input-field" style="height: 150px; resize: none; font-family: monospace;"></textarea>
                    </div>
                    <button class="btn-action" onclick="submitScript()">Salvar Script</button>
                </div>

                <div id="view-settings" class="page-view" style="display: none;">
                    <h2>Configurações de Perfil</h2>
                    <div class="profile-edit">
                        <input type="file" id="user-file" hidden onchange="updateProfilePic(this)">
                        <div class="profile-pic-upload" onclick="document.getElementById('user-file').click()">
                            <img id="edit-user-pic" src="https://cdn-icons-png.flaticon.com/512/149/149071.png">
                            <i class="fas fa-camera"></i>
                        </div>
                        
                        <div style="width: 100%; max-width: 400px;">
                            <div class="input-group">
                                <label>Nome de Exibição</label>
                                <input type="text" id="edit-name" class="input-field">
                            </div>
                            <div class="input-group">
                                <label>E-mail Vinculado</label>
                                <input type="text" id="edit-email" class="input-field" disabled style="opacity: 0.5;">
                            </div>
                            <button class="btn-action" onclick="saveProfile()">Salvar Alterações</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div id="toast">Mensagem do sistema</div>

    <script>
        // --- LOGICA DE BANCO DE DADOS (LOCALSTORAGE) ---
        let users = JSON.parse(localStorage.getItem('nex_users')) || [];
        let loggedUser = null;
        let tempScriptImg = null;
        let currentExploreMode = 'global'; // 'global' ou 'private'

        // --- INIT SYSTEM (Verifica Login Persistente) ---
        (function initApp() {
            const savedSession = localStorage.getItem('nex_session');
            if(savedSession) {
                const sessionData = JSON.parse(savedSession);
                // Verifica se o usuário ainda existe no banco
                const validUser = users.find(u => u.id === sessionData.id);
                
                if(validUser) {
                    loggedUser = validUser;
                    startApp();
                } else {
                    localStorage.removeItem('nex_session'); // Sessão inválida
                }
            }
        })();

        // --- AUTH SYSTEM ---
        function toggleAuth(isReg) {
            document.getElementById('login-box').style.display = isReg ? 'none' : 'block';
            document.getElementById('register-box').style.display = isReg ? 'block' : 'none';
        }

        function handleRegister() {
            const name = document.getElementById('reg-name').value;
            const email = document.getElementById('reg-email').value;
            const pass = document.getElementById('reg-pass').value;

            if(!name || !email.includes('@gmail.com') || pass.length < 6) {
                notify("Use um e-mail @gmail.com real e senha de 6 dígitos.");
                return;
            }

            if(users.find(u => u.email === email)) {
                notify("Este e-mail já possui uma conta NexScript.");
                return;
            }

            const newUser = { name, email, pass, pic: 'https://cdn-icons-png.flaticon.com/512/149/149071.png', id: Date.now() };
            users.push(newUser);
            localStorage.setItem('nex_users', JSON.stringify(users));
            
            // Login Automático após registro
            loggedUser = newUser;
            localStorage.setItem('nex_session', JSON.stringify(loggedUser));

            notify("Conta criada com sucesso!");
            startApp();
        }

        function handleLogin() {
            const email = document.getElementById('auth-email').value;
            const pass = document.getElementById('auth-pass').value;

            const user = users.find(u => u.email === email && u.pass === pass);

            if(user) {
                loggedUser = user;
                // Salva a sessão permanentemente
                localStorage.setItem('nex_session', JSON.stringify(loggedUser));
                startApp();
            } else {
                notify("E-mail não registrado ou senha incorreta.");
            }
        }

        function handleLogout() {
            localStorage.removeItem('nex_session');
            location.reload();
        }

        function startApp() {
            document.getElementById('gatekeeper').style.display = 'none';
            document.getElementById('main-content').style.display = 'block';
            
            // Carregar dados no Header
            document.getElementById('header-user-name').innerText = loggedUser.name;
            document.getElementById('header-user-pic').src = loggedUser.pic;
            
            // Carregar dados nas Configurações
            document.getElementById('edit-name').value = loggedUser.name;
            document.getElementById('edit-email').value = loggedUser.email;
            document.getElementById('edit-user-pic').src = loggedUser.pic;

            loadScripts(currentExploreMode);
            notify("Bem-vindo de volta, " + loggedUser.name);
        }

        // --- NAVEGAÇÃO ---
        function showView(viewId, el) {
            document.querySelectorAll('.page-view').forEach(v => v.style.display = 'none');
            document.getElementById('view-' + viewId).style.display = 'block';
            
            if(el) {
                document.querySelectorAll('.sidebar-nav .nav-item').forEach(i => i.classList.remove('active'));
                el.classList.add('active');
            }
        }

        function switchExploreTab(mode, btn) {
            currentExploreMode = mode;
            document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            
            const title = mode === 'global' ? "Scripts Publicados Globalmente" : "Meu Armazém de Scripts (Privado)";
            document.getElementById('explore-title').innerText = title;
            
            loadScripts(mode);
        }

        // --- PERFIL ---
        function updateProfilePic(input) {
            if (input.files && input.files[0]) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    document.getElementById('edit-user-pic').src = e.target.result;
                    loggedUser.pic = e.target.result;
                }
                reader.readAsDataURL(input.files[0]);
            }
        }

        function saveProfile() {
            const newName = document.getElementById('edit-name').value;
            loggedUser.name = newName;
            
            // Atualiza no banco geral
            users = users.map(u => u.id === loggedUser.id ? loggedUser : u);
            localStorage.setItem('nex_users', JSON.stringify(users));
            
            // Atualiza sessão
            localStorage.setItem('nex_session', JSON.stringify(loggedUser));
            
            document.getElementById('header-user-name').innerText = newName;
            document.getElementById('header-user-pic').src = loggedUser.pic;
            notify("Perfil atualizado com sucesso!");
        }

        // --- SCRIPTS ---
        function processScriptImg(input) {
            const reader = new FileReader();
            reader.onload = (e) => {
                tempScriptImg = e.target.result;
                document.getElementById('script-preview').src = tempScriptImg;
            };
            reader.readAsDataURL(input.files[0]);
        }

        function submitScript() {
            const title = document.getElementById('script-title').value;
            const yt = document.getElementById('script-yt').value;
            const code = document.getElementById('script-raw').value;
            const visibility = document.getElementById('script-visibility').value; // 'global' ou 'private'

            if(!title || !code) return notify("Preencha o título e o código!");

            const script = {
                id: Date.now(),
                title, code, yt, 
                img: tempScriptImg || 'https://via.placeholder.com/300x150/111/fff?text=No+Preview',
                author: loggedUser.name,
                authorId: loggedUser.id,
                date: new Date().toLocaleDateString()
            };

            if(visibility === 'global') {
                const db = JSON.parse(localStorage.getItem('nex_global_scripts')) || [];
                db.unshift(script);
                localStorage.setItem('nex_global_scripts', JSON.stringify(db));
                notify("Script publicado no Feed Global!");
            } else {
                const db = JSON.parse(localStorage.getItem('nex_private_scripts')) || [];
                db.unshift(script);
                localStorage.setItem('nex_private_scripts', JSON.stringify(db));
                notify("Script salvo no seu Armazém Local!");
            }

            // Limpar formulário e ir para o explore
            document.getElementById('script-title').value = '';
            document.getElementById('script-raw').value = '';
            document.getElementById('script-preview').src = '';
            tempScriptImg = null;
            
            showView('explore');
            // Muda a aba para onde o usuário acabou de postar
            const tabBtn = document.querySelectorAll('.tab-btn');
            if(visibility === 'global') switchExploreTab('global', tabBtn[0]);
            else switchExploreTab('private', tabBtn[1]);
        }

        function loadScripts(mode) {
            const container = document.getElementById('scripts-container');
            let db = [];

            if(mode === 'global') {
                db = JSON.parse(localStorage.getItem('nex_global_scripts')) || [];
            } else {
                // Modo privado: carrega TUDO e filtra apenas pelo ID do usuário logado
                const allPrivate = JSON.parse(localStorage.getItem('nex_private_scripts')) || [];
                db = allPrivate.filter(s => s.authorId === loggedUser.id);
            }
            
            if(db.length === 0) {
                container.innerHTML = `<p style='color:var(--muted); grid-column: 1/-1; text-align:center; padding: 40px;'>Nenhum script encontrado em ${mode === 'global' ? 'Global' : 'Seu Armazém'}.</p>`;
                return;
            }

            container.innerHTML = db.map(s => `
                <div class="script-card">
                    ${mode === 'private' ? '<span class="badge-private">PRIVADO</span>' : ''}
                    <img src="${s.img}" class="script-thumb">
                    <h3>${s.title}</h3>
                    <p style="font-size:0.8rem; color:var(--muted); margin: 5px 0;">
                        ${mode === 'global' ? 'Por: ' + s.author : 'Data: ' + s.date}
                    </p>
                    <button class="btn-action" style="padding:8px; font-size:0.8rem;" onclick="copyScript('${btoa(s.code)}')">Copiar Código</button>
                    ${s.yt ? `<a href="${s.yt}" target="_blank" style="display:block; text-align:center; margin-top:10px; font-size:0.8rem; color:var(--primary); text-decoration:none;">Ver Showcase <i class="fas fa-external-link-alt"></i></a>` : ''}
                </div>
            `).join('');
        }

        function copyScript(encoded) {
            navigator.clipboard.writeText(atob(encoded));
            notify("Código copiado para a área de transferência!");
        }

        function notify(msg) {
            const t = document.getElementById('toast');
            t.innerText = msg;
            t.style.display = 'block';
            setTimeout(() => t.style.display = 'none', 3000);
        }

    </script>
</body>
</html>
