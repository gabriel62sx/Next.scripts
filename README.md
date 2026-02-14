<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>ScriptHub — Publicar Scripts Roblox</title>
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet" />
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" />
<style>
:root {
    --bg: #000000;
    --card: #111111;
    --muted: #999;
    --accent: #606cff;
    --accent-2: #3455dd;
    --glass: rgba(255, 255, 255, 0.04);
    --text: #eee;
}
*, *::before, *::after {
    box-sizing: border-box;
}
body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif, monospace, system-ui, Segoe UI, Roboto, Helvetica, Arial, sans-serif;
    margin: 0;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    scroll-behavior: smooth;
}
a {
    color: inherit;
    text-decoration: none;
    transition: color 0.3s ease;
}
a:hover {
    color: var(--accent);
}
.navbar {
    backdrop-filter: blur(6px);
    background: linear-gradient(90deg, rgba(11, 17, 32, 0.7), rgba(11, 17, 32, 0.45));
    border-bottom: 1px solid rgba(255, 255, 255, 0.06);
    position: sticky;
    top: 0;
    z-index: 60;
}
.nav-container {
    max-width: 1100px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 14px;
}
.logo {
    display: flex;
    gap: 10px;
    align-items: center;
    font-weight: 700;
    font-size: 1rem;
    letter-spacing: 0.05em;
    color: var(--accent);
    user-select: none;
}
.logo i {
    font-size: 20px;
}
.nav-links {
    list-style: none;
    display: flex;
    gap: 12px;
    padding: 0;
    margin: 0;
}
.nav-link {
    padding: 8px 12px;
    border-radius: 8px;
    color: var(--muted);
    font-weight: 600;
    font-size: 0.85rem;
    cursor: pointer;
    user-select: none;
    transition: background-color 0.3s ease, color 0.3s ease;
}
.nav-link:hover,
.nav-link.active {
    background: var(--glass);
    color: var(--accent);
}
.container {
    max-width: 1100px;
    margin: 28px auto;
    padding: 0 18px;
}
.hero-card {
    padding: 28px;
    border-radius: 14px;
    background: var(--card);
    box-shadow: 0 6px 18px rgba(2, 6, 23, 0.75);
    text-align: center;
    user-select: none;
}
.hero-card h1 {
    font-size: 3rem;
    color: var(--accent);
    margin: 0 0 20px;
    font-weight: 900;
    letter-spacing: 0.1em;
}
.hero-card p {
    font-size: 1.3rem;
    color: var(--muted);
    margin: 0;
    font-weight: 600;
}
.search-box {
    display: flex;
    gap: 8px;
    margin-top: 12px;
}
.search-box input {
    flex: 1;
    padding: 12px 14px;
    border-radius: 10px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    background: transparent;
    color: var(--text);
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 0.85rem;
    letter-spacing: 0.05em;
    transition: border-color 0.3s ease;
}
.search-box input::placeholder {
    color: var(--muted);
}
.search-box input:focus {
    outline: none;
    border-color: var(--accent-2);
    background-color: #222;
}
.search-box button {
    padding: 0 16px;
    border-radius: 10px;
    border: none;
    background: linear-gradient(90deg, var(--accent), var(--accent-2));
    color: #ccc;
    font-weight: 700;
    cursor: pointer;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 0.85rem;
    letter-spacing: 0.05em;
    transition: background-color 0.3s;
    user-select: none;
}
.search-box button:hover {
    background: linear-gradient(90deg, var(--accent-2), var(--accent));
}
.filters {
    display: flex;
    gap: 8px;
    margin-top: 16px;
    flex-wrap: wrap;
    font-size: 0.8rem;
    letter-spacing: 0.1em;
}
.chip {
    padding: 8px 14px;
    background: transparent;
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 999px;
    color: var(--muted);
    cursor: pointer;
    user-select: none;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    transition: background-color 0.3s, border-color 0.3s, color 0.3s;
    font-size: 0.85rem;
}
.chip.active {
    background: rgba(54, 83, 177, 0.3);
    color: var(--accent-2);
    border-color: rgba(54, 83, 177, 0.7);
}
.chip:hover:not(.active) {
    background: var(--glass);
    border-color: var(--accent);
    color: var(--accent);
}
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    gap: 18px;
    margin-top: 22px;
}
.card {
    background: var(--card);
    padding: 14px;
    border-radius: 12px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    font-size: 0.85rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    letter-spacing: 0.05em;
    color: var(--text);
    display: flex;
    flex-direction: column;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    position: relative;
}
.card:hover {
    box-shadow: 0 10px 25px rgba(54, 83, 177, 0.7);
    transform: translateY(-4px);
    cursor: pointer;
}
.card img {
    width: 100%;
    height: 140px;
    object-fit: cover;
    border-radius: 8px;
    margin-bottom: 10px;
    user-select: none;
}
.card h4 {
    margin: 0 0 6px 0;
    font-size: 1.1rem;
    color: var(--accent);
}
.card p {
    color: var(--muted);
    font-size: 0.9rem;
    margin: 0 0 10px 0;
    flex-grow: 1;
}
.card .meta {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 6px;
    font-size: 0.75rem;
    color: var(--muted);
    user-select: none;
}
.btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 8px 14px;
    border-radius: 8px;
    border: none;
    cursor: pointer;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 0.9rem;
    letter-spacing: 0.03em;
    transition: background-color 0.3s ease;
    user-select: none;
    text-transform: none !important;
}
.btn-primary {
    background: linear-gradient(90deg, var(--accent), var(--accent-2));
    color: #ccc;
    font-weight: 700;
}
.btn-primary:hover {
    background: linear-gradient(90deg, var(--accent-2), var(--accent));
}
.btn-ghost {
    background: transparent;
    border: 1px solid rgba(255, 255, 255, 0.1);
    color: var(--muted);
}
.btn-ghost:hover {
    background: var(--glass);
    border-color: var(--accent);
    color: var(--accent);
}
.footer {
    background: var(--card);
    border-top: 1px solid rgba(255,255,255,0.1);
    padding: 18px 0;
    text-align: center;
    font-size: 0.9rem;
    color: var(--muted);
    position: relative;
    user-select: none;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    z-index: 10;
}
.page-nav{
    position: fixed;
    right: 12px;
    width: 40px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 12px;
    z-index: 999;
}
.page-nav.top {
    top: 12px;
}
.page-nav.bottom {
    bottom: 12px;
}
.page-nav button {
    background: var(--card);
    border: 1px solid rgba(255,255,255,0.2);
    border-radius: 8px;
    padding: 8px;
    cursor: pointer;
    color: var(--accent);
    font-size: 1.2rem;
    transition: background-color 0.3s ease;
}
.page-nav button:hover {
    background: var(--accent);
    color: #111;
}
/* Modal estilos */
.modal {
    position: fixed;
    inset: 0;
    display: none;
    align-items: center;
    justify-content: center;
    background: linear-gradient(180deg, rgba(2, 6, 23, 0.85), rgba(2, 6, 23, 0.97));
    z-index: 120;
    padding: 28px;
}
.modal.show {
    display: flex;
}
.modal-content {
    width: 100%;
    max-width: 480px;
    max-height: 90vh;
    overflow-y: auto;
    background: var(--card);
    border-radius: 12px;
    padding: 24px 28px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    position: relative;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: var(--text);
    font-size: 1rem;
    line-height: 1.4em;
    user-select: none;
}
.modal-close {
    position: absolute;
    right: 12px;
    top: 8px;
    background: transparent;
    border: none;
    color: var(--muted);
    font-size: 28px;
    cursor: pointer;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-weight: 700;
    line-height: 1;
}
.form-group {
    margin: 16px 0;
    display: flex;
    flex-direction: column;
    gap: 8px;
}
label {
    font-size: 0.9rem;
    color: var(--muted);
}
input[type=text],
textarea,
select,
input[type=file],
select#deleteScriptSelector {
    padding: 12px;
    border-radius: 8px;
    border: 1px solid rgba(255, 255, 255, 0.15);
    background: transparent;
    color: var(--text);
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 1rem;
    transition: border-color 0.3s ease;
    text-transform: none;
    resize: vertical;
}
input[type=file] {
    cursor: pointer;
}
input:focus,
select:focus,
textarea:focus {
    outline: none;
    border-color: var(--accent-2);
    background-color: #222;
}
textarea {
    min-height: 100px;
    max-height: 200px;
}
#uploadPreview {
    width: 100%;
    max-height: 180px;
    object-fit: cover;
    border-radius: 8px;
    margin-top: 12px;
    display: none;
}
pre {
    background: rgba(30,30,60,0.85);
    color: #cdf;
    padding: 8px;
    border-radius: 8px;
    margin-top: 10px;
    white-space: pre-wrap;
    max-height: 250px;
    overflow-y: auto;
    font-family: monospace;
}
/* Notificação dentro do card para senha */
.password-prompt {
    background: rgba(0,0,0,0.85);
    border-radius: 10px;
    padding: 16px;
    color: var(--accent);
    font-weight: 700;
    font-size: 1rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    box-shadow: 0 4px 14px rgba(54, 83, 177, 0.9);
    position: absolute;
    inset: 30px auto auto 30px;
    right: 30px;
    left: 30px;
    top: 50%;
    transform: translateY(-50%);
    z-index: 20;
    user-select: none;
}
.password-prompt input {
    background: #222;
    color: var(--accent);
    border-radius: 6px;
    border: 1px solid var(--accent-2);
    padding: 10px 12px;
    font-size: 1rem;
    font-weight: normal;
    width: 100%;
}
.password-prompt button {
    background: linear-gradient(90deg, var(--accent), var(--accent-2));
    border: none;
    padding: 10px 16px;
    border-radius: 10px;
    color: #eee;
    font-weight: 700;
    cursor: pointer;
    width: 100%;
    font-size: 1rem;
    user-select: none;
    transition: background-color 0.3s ease;
}
.password-prompt button:hover {
    background: linear-gradient(90deg, var(--accent-2), var(--accent));
}
.notification-card {
    position: absolute;
    top: 8px;
    right: 8px;
    background: rgba(54, 83, 177, 0.85);
    color: #eee;
    padding: 6px 12px;
    border-radius: 12px;
    font-weight: 700;
    font-size: 0.75rem;
    pointer-events: none;
    opacity: 0;
    transform: translateY(-10px);
    transition: opacity 0.3s, transform 0.3s;
    user-select: none;
    z-index: 10;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
.notification-card.show {
    opacity: 1;
    transform: translateY(0);
    pointer-events: auto;
}
</style>
</head>
<body>
<nav class="navbar" role="navigation" aria-label="Main navigation">
    <div class="nav-container">
        <div class="logo" aria-hidden="true">
            <i class="fas fa-cubes"></i>
            <span>ScriptHub</span>
        </div>
        <ul class="nav-links">
            <li><a href="#" class="nav-link active" onclick="showHome(event)">Início</a></li>
            <li><a href="#catalog" class="nav-link" onclick="showCatalog(event)">Scripts</a></li>
            <li><a href="#" class="nav-link" onclick="openAdminPanel()">Publicar <i class="fas fa-upload"></i></a></li>
            <li><a href="https://instagram.com/gabriel.futury" target="_blank" class="nav-link" aria-label="Instagram Gabriel Futury"><i class="fab fa-instagram"></i> Instagram</a></li>
        </ul>
    </div>
</nav>

<main class="container" id="main">

    <!-- Página Inicial -->
    <section class="hero-card hero" aria-labelledby="hero-title" id="homeSection" style="display: block;">
        <h1 id="hero-title">Seja bem-vindo ao melhor site de anúncios de scripts Roblox!</h1>
        <p>Encontre, publique e compartilhe scripts incríveis com nossa comunidade.</p>
    </section>

    <!-- Catálogo de scripts -->
    <section id="catalog" style="display:none;">
        <h2 style="margin:18px 0 6px 0; font-size: 12px; letter-spacing:0.1em;">Explorar Scripts</h2>
        <p style="margin:0;color:var(--muted); font-size: 9px; letter-spacing: 0.05em;">Encontre scripts por categoria, preço ou popularidade.</p>

        <div class="search-box" role="search" aria-label="Pesquisar scripts" style="margin-top:10px;">
            <input id="heroSearch" type="text" placeholder="Buscar scripts, categorias..." aria-label="Buscar scripts" onkeyup="filterGrid()" autocomplete="off" />
            <button class="btn btn-primary" onclick="filterGrid(true)" aria-label="Pesquisar"><i class="fas fa-search"></i></button>
        </div>
        <div class="filters" aria-hidden="false" style="margin-top:12px;">
            <button class="chip active" onclick="toggleCategory(this,'todas')" type="button">Todas</button>
            <button class="chip" onclick="toggleCategory(this,'automacao')" type="button">Automação</button>
            <button class="chip" onclick="toggleCategory(this,'web')" type="button">Web</button>
            <button class="chip" onclick="toggleCategory(this,'bot')" type="button">Bots</button>
            <button class="chip" onclick="toggleCategory(this,'utilidade')" type="button">Utilidade</button>
        </div>

        <div class="grid" id="scriptsGrid" aria-live="polite" style="margin-top:22px;"></div>

        <div class="footer">© <strong>ScriptHub</strong> — criado com carinho.</div>
    </section>
</main>

<!-- Painel Admin para publicar scripts -->
<div id="adminModal" class="modal" role="dialog" aria-hidden="true" aria-labelledby="adminTitle" >
    <div class="modal-content" style="max-width: 480px;">
        <button class="modal-close" onclick="closeAdminPanel()" aria-label="Fechar">&times;</button>
        <h3 id="adminTitle">Publicar Novo Script</h3>
        <form id="publishForm" onsubmit="publishScript(event)" style="display:flex;flex-direction:column;gap:16px;">
            <div class="form-group">
                <label for="scriptTitle">Título do Script</label>
                <input id="scriptTitle" type="text" placeholder="Ex: Script de Vendas Roblox" required maxlength="50" autocomplete="off" />
            </div>
            <div class="form-group">
                <label for="scriptDesc">Descrição</label>
                <textarea id="scriptDesc" placeholder="Descreva seu script..." required maxlength="260"></textarea>
            </div>

            <div class="form-group">
                <label for="scriptCode">Código do Script (Exemplo: Lua, JS, etc.)</label>
                <textarea id="scriptCode" placeholder="Cole o código aqui..." rows="6" style="resize:vertical;"></textarea>
            </div>

            <div class="form-group">
                <label for="scriptCat">Categoria</label>
                <select id="scriptCat" required>
                    <option value="" disabled selected>Selecione uma categoria</option>
                    <option value="automacao">Automação</option>
                    <option value="web">Web</option>
                    <option value="bot">Bots</option>
                    <option value="utilidade">Utilidade</option>
                </select>
            </div>

            <div class="form-group">
                <label for="uploadImg">Carregar imagem do script (Arquivo de imagem)</label>
                <input type="file" id="uploadImg" accept="image/*" />
                <img id="uploadPreview" alt="Preview da imagem carregada"/>
            </div>
            
            <div class="form-group">
                <label for="deleteScriptSelector">Excluir script existente</label>
                <select id="deleteScriptSelector" aria-label="Selecionar script para exclusão">
                    <option value="" disabled selected>Selecione um script</option>
                </select>
                <button type="button" class="btn btn-ghost" style="margin-top:8px;" onclick="deleteSelectedScript()">Excluir Script</button>
            </div>

            <div style="display:flex;gap:12px; flex-wrap: wrap; justify-content: center;">
                <button class="btn btn-primary" type="submit">Publicar</button>
                <button type="button" class="btn btn-ghost" onclick="resetPublishForm()">Limpar</button>
            </div>
        </form>
    </div>
</div>

<!-- Botões subir/descer página -->
<div class="page-nav top" aria-label="Navegação de página topo">
    <button title="Ir para o topo" onclick="scrollToTop()" aria-label="Ir para o topo"><i class="fas fa-arrow-up"></i></button>
</div>
<div class="page-nav bottom" aria-label="Navegação de página rodapé">
    <button title="Ir para o rodapé" onclick="scrollToBottom()" aria-label="Ir para o rodapé"><i class="fas fa-arrow-down"></i></button>
</div>

<script>
    let sampleScripts = [
        {id:'s1',title:'AutoVenda 2.0',cat:'automacao',desc:'Automatize vendas e integrações',price:19.99,img:'https://picsum.photos/seed/1/600/400', code: 'print("AutoVenda script executado")', unlocked: false},
        {id:'s2',title:'WebScrape Pro',cat:'web',desc:'Coleta de dados em massa com proxies',price:9.99,img:'https://picsum.photos/seed/2/600/400', code: 'console.log("Web scraping iniciado")', unlocked: false},
        {id:'s3',title:'ChatBotX',cat:'bot',desc:'Bot conversacional multicanal',price:0.00,img:'https://picsum.photos/seed/3/600/400', code: 'function chat() {return "bot ativo";}', unlocked: false},
        {id:'s4',title:'UtilsPack',cat:'utilidade',desc:'Ferramentas utilitárias para devs',price:4.5,img:'https://picsum.photos/seed/4/600/400', code: 'alert("Utils funcionando");', unlocked: false},
    ];

    // Atualiza opções de exclusão no painel publicar
    function updateDeleteOptions(){
        const select = document.getElementById('deleteScriptSelector');
        select.innerHTML = '<option value="" disabled selected>Selecione um script</option>';
        sampleScripts.forEach(s=>{
            const opt = document.createElement('option');
            opt.value = s.id;
            opt.textContent = s.title;
            select.appendChild(opt);
        });
    }

    function deleteSelectedScript(){
        const select = document.getElementById('deleteScriptSelector');
        const id = select.value;
        if(!id){
            alert('Selecione um script para excluir.');
            return;
        }
        if(confirm('Tem certeza que deseja excluir o script selecionado?')){
            sampleScripts = sampleScripts.filter(s=>s.id !== id);
            renderGrid();
            updateDeleteOptions();
            select.value = '';
            alert('Script excluído com sucesso.');
        }
    }

    function renderGrid(list = sampleScripts) {
        const grid = document.getElementById('scriptsGrid');
        grid.innerHTML = '';
        if(!list.length){
            const noScripts = document.createElement('p');
            noScripts.textContent = 'Nenhum script disponível.';
            noScripts.style.fontFamily = "'Segoe UI', Tahoma, Geneva, Verdana, sans-serif";
            noScripts.style.fontSize = '1rem';
            noScripts.style.color = 'var(--muted)';
            noScripts.style.textAlign = 'center';
            noScripts.style.gridColumn = '1 / -1';
            grid.appendChild(noScripts);
            return;
        }
        list.forEach(s => {
            const el = document.createElement('article');
            el.className = 'card';
            el.innerHTML = `
                <img src="${escapeHtml(s.img)}" alt="Imagem do script ${escapeHtml(s.title)}" loading="lazy" />
                <h4>${escapeHtml(s.title)}</h4>
                <p>${escapeHtml(s.desc)}</p>
                <div class="meta">
                    <div>${escapeHtml(s.cat)} • ${s.price > 0 ? 'R$ '+s.price.toFixed(2) : 'Grátis'}</div>
                </div>
                <div class="code-area" style="position:relative; flex-grow:1;">
                    <pre>${escapeHtml(s.code || '// Código não fornecido')}</pre>
                    <button class="btn btn-primary btn-copy" aria-label="Copiar código" style="display:none; margin-top: 8px;">Copiar Código</button>
                    <button class="btn btn-ghost btn-unlock" aria-label="Liberar código" style="margin-top: 8px;">Liberar Código</button>
                    <div class="notification-card" aria-live="polite"></div>
                    <div class="password-prompt" style="display:none;">
                        <input type="password" placeholder="Digite a senha para liberar código" aria-label="Senha para liberar código"/>
                        <button>Enviar</button>
                    </div>
                </div>
            `;

            const pre = el.querySelector('pre');
            const copyBtn = el.querySelector('.btn-copy');
            const unlockBtn = el.querySelector('.btn-unlock');
            const notifDiv = el.querySelector('.notification-card');
            const passwordPrompt = el.querySelector('.password-prompt');
            const passwordInput = passwordPrompt.querySelector('input');
            const passwordBtn = passwordPrompt.querySelector('button');

            if (s.unlocked) {
                pre.style.display = 'block';
                copyBtn.style.display = 'inline-flex';
                unlockBtn.style.display = 'none';
                passwordPrompt.style.display = 'none';
            } else {
                pre.style.display = 'none';
                copyBtn.style.display = 'none';
                unlockBtn.style.display = 'inline-flex';
                passwordPrompt.style.display = 'none';
            }

            unlockBtn.onclick = e => {
                unlockBtn.style.display = 'none';
                passwordPrompt.style.display = 'flex';
                passwordInput.focus();
            };
            passwordBtn.onclick = () => {
                const senha = passwordInput.value.trim();
                if (senha === 'moderN20') {
                    s.unlocked = true;
                    pre.style.display = 'block';
                    copyBtn.style.display = 'inline-flex';
                    unlockBtn.style.display = 'none';
                    passwordPrompt.style.display = 'none';
                    showNotificationCard(notifDiv, 'Código liberado com sucesso!');
                } else {
                    showNotificationCard(notifDiv, 'Senha incorreta!', true);
                    passwordInput.value = '';
                    passwordInput.focus();
                }
            };
            passwordInput.addEventListener('keydown', e => {
                if (e.key === 'Enter') passwordBtn.click();
                if (e.key === 'Escape'){
                   passwordPrompt.style.display = 'none';
                   unlockBtn.style.display = 'inline-flex';
                }
            });

            copyBtn.onclick = () => {
                navigator.clipboard.writeText(s.code || '');
                showNotificationCard(notifDiv, 'Código copiado com sucesso!');
            };

            grid.appendChild(el);
        });
        updateDeleteOptions();
    }

    function showNotificationCard(element, msg, isError=false) {
        element.textContent = msg;
        element.style.backgroundColor = isError ? 'rgba(204,51,51,0.85)' : 'rgba(54, 83, 177, 0.85)';
        element.classList.add('show');
        setTimeout(() => {
            element.classList.remove('show');
        }, 3000);
    }

    function escapeHtml(text) {
        if(!text) return '';
        return text.replace(/[&<>"']/g, (m) => ({
            '&': '&amp;',
            '<': '&lt;',
            '>': '&gt;',
            '"': '&quot;',
            "'": '&#39;'
        })[m]);
    }

    function filterGrid(triggerSearch) {
        const q = document.getElementById('heroSearch').value.trim().toLowerCase();
        const cat = document.querySelector('.filters .chip.active')?.textContent.toLowerCase() || 'todas';
        let filtered = sampleScripts.filter(s => {
            const matchQ = q ? (s.title + s.desc + s.cat).toLowerCase().includes(q) : true;
            const matchCat = (cat === 'todas') || s.cat === cat;
            return matchQ && matchCat;
        });
        renderGrid(filtered);
        if(triggerSearch) showNotification(filtered.length + ' resultado(s)');
    }

    function toggleCategory(btn, cat) {
        document.querySelectorAll('.chip').forEach(c => c.classList.remove('active'));
        btn.classList.add('active');
        filterGrid();
    }

    function showHome(evt) {
        evt.preventDefault();
        document.getElementById('homeSection').style.display = 'block';
        document.getElementById('catalog').style.display = 'none';
        document.querySelectorAll('.nav-link').forEach(link => link.classList.remove('active'));
        evt.currentTarget.classList.add('active');
    }
    function showCatalog(evt) {
        evt.preventDefault();
        document.getElementById('homeSection').style.display = 'none';
        document.getElementById('catalog').style.display = 'block';
        document.querySelectorAll('.nav-link').forEach(link => link.classList.remove('active'));
        evt.currentTarget.classList.add('active');
        filterGrid();
    }

    // Modal publicar script
    function openAdminPanel() {
        document.getElementById('adminModal').classList.add('show');
        document.getElementById('adminModal').setAttribute('aria-hidden', 'false');
        resetPublishForm();
        updateDeleteOptions();
    }
    function closeAdminPanel() {
        document.getElementById('adminModal').classList.remove('show');
        document.getElementById('adminModal').setAttribute('aria-hidden', 'true');
    }

    // Preview da imagem carregada
    document.getElementById('uploadImg').addEventListener('change', function(e){
        const preview = document.getElementById('uploadPreview');
        const file = e.target.files[0];
        if(file){
            const validImageTypes = ['image/jpeg', 'image/png', 'image/gif', 'image/webp'];
            if(!validImageTypes.includes(file.type)){
                alert('Arquivo de imagem inválido.');
                e.target.value = '';
                preview.style.display = 'none';
                return;
            }
            const reader = new FileReader();
            reader.onload = () => {
                preview.src = reader.result;
                preview.style.display = 'block';
            }
            reader.readAsDataURL(file);
        } else {
            preview.style.display = 'none';
        }
    });

    function publishScript(e){
        e.preventDefault();
        const title = document.getElementById('scriptTitle').value.trim();
        const desc = document.getElementById('scriptDesc').value.trim();
        const cat = document.getElementById('scriptCat').value;
        const code = document.getElementById('scriptCode').value.trim();
        const fileInput = document.getElementById('uploadImg');
        let imgUrl = '';

        if(!title || !desc || !cat){
            alert('Preencha todos os campos obrigatórios');
            return;
        }

        if(fileInput.files.length > 0){
            const file = fileInput.files[0];
            const reader = new FileReader();
            reader.onload = function(ev){
                imgUrl = ev.target.result;
                adicionarScript(imgUrl);
            };
            reader.onerror = function(){
                alert('Erro ao ler a imagem');
            };
            reader.readAsDataURL(file);
        } else {
            imgUrl = 'https://picsum.photos/seed/' + (sampleScripts.length + 10) + '/600/400';
            adicionarScript(imgUrl);
        }

        function adicionarScript(imgUrl){
            const id = 's' + (sampleScripts.length + 1);
            const unlocked = false; // inicia bloqueado
            const price = 0;
            const novoScript = {id, title, desc, img: imgUrl, cat, code, price, unlocked};
            sampleScripts.push(novoScript);
            renderGrid();
            alert(`Script "${title}" publicado com sucesso!`);
            closeAdminPanel();
        }
    }
    function resetPublishForm(){
        document.getElementById('publishForm').reset();
        document.getElementById('uploadPreview').style.display = 'none';
    }

    // Notificação temporária topo
    let notTimeout;
    function showNotification(msg, isError){
        clearTimeout(notTimeout);
        const n = document.createElement('div');
        n.className = 'notification-global';
        n.innerText = msg;
        n.style.position = 'fixed';
        n.style.top = '20px';
        n.style.left = '50%';
        n.style.transform = 'translateX(-50%)';
        n.style.padding = '12px 24px';
        n.style.borderRadius = '12px';
        n.style.fontWeight = '700';
        n.style.fontSize = '1rem';
        n.style.backgroundColor = isError ? '#cc3333cc' : 'rgba(54, 83, 177, 0.9)';
        n.style.color = '#eee';
        n.style.zIndex = '9999';
        n.style.userSelect = 'none';
        n.style.boxShadow = '0 8px 25px rgba(54, 83, 177, 0.8)';
        document.body.appendChild(n);
        setTimeout(() => {
            n.style.opacity = '0';
            setTimeout(() => n.remove(), 400);
        }, 3000);
    }

    function scrollToTop(){
        window.scrollTo({top: 0, behavior: 'smooth'});
    }
    function scrollToBottom(){
        window.scrollTo({top: document.body.scrollHeight, behavior: 'smooth'});
    }

    document.addEventListener('DOMContentLoaded', () => {
        renderGrid();
        updateDeleteOptions();
    });

    document.addEventListener('keydown', e=>{
        if(e.key === 'Escape'){
            // Fechar modal e todos password prompts visiveis
            document.querySelectorAll('.modal.show').forEach(m=>{
                m.classList.remove('show');
                m.setAttribute('aria-hidden', 'true');
            });
            document.querySelectorAll('.password-prompt').forEach(pp =>{
                pp.style.display = 'none';
                const card = pp.closest('.card');
                if(card){
                    const unlockBtn = card.querySelector('.btn-unlock');
                    if(unlockBtn) unlockBtn.style.display = 'inline-flex';
                }
            })
        }
    });
</script>
</body>
</html>
