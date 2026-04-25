# Concetra-tempo
Aplicativo de gerenciamento de tempo de estudos com Pomodoro
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ConcentraTempo - Gerencie seu tempo</title>
    <style>
        :root { 
            --bg: #050a0f; 
            --green: #2ecc71; 
            --blue: #1e3a5f; 
            --red: #e74c3c; 
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body { 
            background: var(--bg); 
            color: white; 
            font-family: 'Poppins', sans-serif; 
        }
        
        .bg-anim { 
            position: fixed; 
            top: 0; 
            left: 0; 
            width: 100%; 
            height: 100%; 
            z-index: -1; 
            background: radial-gradient(circle, #001f3f, #000); 
        }
        
        .container { 
            max-width: 500px; 
            margin: 40px auto; 
            background: rgba(10, 25, 47, 0.9); 
            padding: 30px; 
            border-radius: 20px; 
            border: 1px solid var(--green); 
        }
        
        .hidden { 
            display: none !important; 
        }
        
        .logo { 
            font-size: 2.5rem; 
            text-align: center; 
            -webkit-text-stroke: 1px white; 
            color: transparent; 
            margin-bottom: 30px;
            font-weight: bold;
        }
        
        .logo span { 
            color: var(--green); 
        }
        
        .user-profile { 
            display: flex; 
            justify-content: space-between; 
            align-items: center; 
            margin-bottom: 20px; 
        }
        
        .avatar { 
            width: 40px; 
            height: 40px; 
            background: var(--blue); 
            border-radius: 50%; 
            display: flex; 
            align-items: center; 
            justify-content: center; 
            font-weight: bold;
        }
        
        .username {
            font-size: 0.9rem;
            color: var(--green);
        }
        
        .nav-menu { 
            display: flex; 
            justify-content: center; 
            gap: 10px; 
            margin-bottom: 20px; 
            flex-wrap: wrap;
        }
        
        button { 
            padding: 10px 15px; 
            background: var(--green); 
            color: #000;
            border: none; 
            cursor: pointer; 
            border-radius: 5px; 
            font-weight: bold; 
            margin: 5px; 
            transition: all 0.3s ease;
        }
        
        button:hover {
            background: #27ae60;
            transform: scale(1.05);
        }
        
        button.logout-btn {
            background: var(--red);
            color: white;
        }
        
        button.logout-btn:hover {
            background: #c0392b;
        }
        
        input, select { 
            width: 100%; 
            padding: 12px; 
            margin: 8px 0; 
            border-radius: 5px; 
            border: 1px solid var(--blue); 
            background: #0b1d36; 
            color: white;
            font-family: 'Poppins', sans-serif;
        }
        
        input::placeholder {
            color: rgba(255, 255, 255, 0.5);
        }
        
        .support-btn-login { 
            display: block; 
            text-align: center; 
            margin-top: 15px; 
            color: var(--green); 
            text-decoration: none; 
            border: 1px solid var(--green); 
            padding: 8px; 
            border-radius: 5px; 
            transition: all 0.3s ease;
        }
        
        .support-btn-login:hover {
            background: var(--green);
            color: #000;
        }
        
        .item-card { 
            border-left: 3px solid var(--green); 
            padding: 15px; 
            margin: 10px 0; 
            background: rgba(255,255,255,0.05); 
            display: flex; 
            justify-content: space-between; 
            align-items: center; 
            border-radius: 5px;
            transition: all 0.3s ease;
        }
        
        .item-card:hover {
            background: rgba(46, 204, 113, 0.1);
        }
        
        .item-info {
            flex: 1;
        }
        
        .item-title {
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .item-time {
            font-size: 0.85rem;
            color: var(--green);
        }
        
        .del-btn { 
            background: var(--red); 
            color: white; 
            border: none; 
            padding: 5px 10px; 
            border-radius: 4px; 
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .del-btn:hover {
            background: #c0392b;
        }
        
        .tech-box { 
            border: 1px solid var(--blue); 
            padding: 15px; 
            border-radius: 10px; 
            margin-top: 15px; 
        }
        
        .concluido { 
            text-decoration: line-through; 
            opacity: 0.6; 
        }
        
        .timer-display {
            font-size: 2rem;
            text-align: center;
            color: var(--green);
            margin: 20px 0;
            font-weight: bold;
            font-family: 'Courier New', monospace;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-size: 0.9rem;
            color: var(--green);
        }
        
        .list-container {
            max-height: 400px;
            overflow-y: auto;
            margin-top: 20px;
        }
        
        .empty-state {
            text-align: center;
            color: rgba(255, 255, 255, 0.5);
            padding: 40px 20px;
        }
    </style>
</head>
<body>
    <div class="bg-anim"></div>
    
    <!-- Tela de Autenticação -->
    <div id="authScreen" class="container">
        <h1 class="logo">Concentra<span>⏱️</span>Tempo</h1>
        
        <div class="form-group">
            <input type="text" id="userInput" placeholder="Nome de Usuário">
        </div>
        
        <div class="form-group">
            <input type="email" id="emailInput" placeholder="Seu E-mail">
        </div>
        
        <button onclick="login(); return false;">Entrar</button>
        
        <a href="https://wa.me/5547996414795" target="_blank" class="support-btn-login">
            💬 Suporte via WhatsApp
        </a>
    </div>
    
    <!-- Tela Principal (Oculta inicialmente) -->
    <div id="mainScreen" class="container hidden">
        <h1 class="logo">Concentra<span>⏱️</span>Tempo</h1>
        
        <div class="user-profile">
            <div>
                <div class="avatar" id="avatarDisplay">U</div>
                <div class="username" id="usernameDisplay">Usuário</div>
            </div>
            <button class="logout-btn" onclick="logout()">Sair</button>
        </div>
        
        <div class="nav-menu">
            <button onclick="showTab('tarefas')">📝 Tarefas</button>
            <button onclick="showTab('pomodoro')">🍅 Pomodoro</button>
            <button onclick="showTab('relatorio')">📊 Relatório</button>
        </div>
        
        <!-- Tab: Tarefas -->
        <div id="tarefasTab">
            <h2>Minhas Tarefas</h2>
            
            <div class="form-group">
                <label for="taskInput">Nova Tarefa</label>
                <input type="text" id="taskInput" placeholder="Digite uma tarefa...">
            </div>
            
            <div class="form-group">
                <label for="taskTime">Tempo estimado (minutos)</label>
                <input type="number" id="taskTime" placeholder="Ex: 30" min="1">
            </div>
            
            <button onclick="addTask()">➕ Adicionar Tarefa</button>
            
            <div class="list-container" id="taskList">
                <div class="empty-state">Nenhuma tarefa. Comece agora! 🚀</div>
            </div>
        </div>
        
        <!-- Tab: Pomodoro -->
        <div id="pomodoroTab" class="hidden">
            <h2>Técnica Pomodoro</h2>
            
            <div class="timer-display" id="timerDisplay">25:00</div>
            
            <div style="display: flex; gap: 10px; justify-content: center;">
                <button id="startBtn" onclick="startTimer()">▶️ Iniciar</button>
                <button id="pauseBtn" onclick="pauseTimer()" class="hidden">⏸️ Pausar</button>
                <button onclick="resetTimer()">🔄 Resetar</button>
            </div>
            
            <div class="tech-box">
                <h3>Como funciona:</h3>
                <p>✅ Trabalhe por 25 minutos</p>
                <p>✅ Descanse por 5 minutos</p>
                <p>✅ A cada 4 ciclos, descanse 15 minutos</p>
            </div>
        </div>
        
        <!-- Tab: Relatório -->
        <div id="relatorioTab" class="hidden">
            <h2>Seu Relatório</h2>
            
            <div class="tech-box">
                <h3>Estatísticas</h3>
                <p>Total de Tarefas: <span id="totalTasks">0</span></p>
                <p>Tarefas Concluídas: <span id="completedTasks">0</span></p>
                <p>Tempo Total: <span id="totalTime">0h</span></p>
                <p>Sessões Pomodoro: <span id="pomodoroSessions">0</span></p>
            </div>
        </div>
    </div>

    <script>
        let currentUser = null;
        let tasks = [];
        let timerInterval = null;
        let timeLeft = 25 * 60;
        let isRunning = false;
        let pomodoroSessions = 0;

        // Login
        function login() {
            const username = document.getElementById('userInput').value;
            const email = document.getElementById('emailInput').value;

            if (username.trim() && email.trim()) {
                currentUser = { username, email };
                localStorage.setItem('user', JSON.stringify(currentUser));
                loadUserData();
                showScreen('main');
            } else {
                alert('Por favor, preencha todos os campos!');
            }
        }

        // Logout
        function logout() {
            currentUser = null;
            localStorage.removeItem('user');
            localStorage.removeItem('tasks');
            tasks = [];
            showScreen('auth');
        }

        // Alternar telas
        function showScreen(screen) {
            document.getElementById('authScreen').classList.toggle('hidden', screen !== 'auth');
            document.getElementById('mainScreen').classList.toggle('hidden', screen !== 'main');
            
            if (screen === 'main') {
                updateUserDisplay();
            }
        }

        // Alternar abas
        function showTab(tabName) {
            document.getElementById('tarefasTab').classList.add('hidden');
            document.getElementById('pomodoroTab').classList.add('hidden');
            document.getElementById('relatorioTab').classList.add('hidden');
            
            document.getElementById(tabName + 'Tab').classList.remove('hidden');
            
            if (tabName === 'relatorio') {
                updateReport();
            }
        }

        // Adicionar tarefa
        function addTask() {
            const taskInput = document.getElementById('taskInput');
            const taskTime = document.getElementById('taskTime');
            const text = taskInput.value.trim();
            const time = parseInt(taskTime.value) || 30;

            if (text) {
                const task = {
                    id: Date.now(),
                    text: text,
                    time: time,
                    completed: false,
                    createdAt: new Date().toLocaleString('pt-BR')
                };
                tasks.push(task);
                saveTasks();
                renderTasks();
                taskInput.value = '';
                taskTime.value = '';
            }
        }

        // Renderizar tarefas
        function renderTasks() {
            const taskList = document.getElementById('taskList');
            
            if (tasks.length === 0) {
                taskList.innerHTML = '<div class="empty-state">Nenhuma tarefa. Comece agora! 🚀</div>';
                return;
            }

            taskList.innerHTML = tasks.map(task => `
                <div class="item-card ${task.completed ? 'concluido' : ''}">
                    <div class="item-info">
                        <div class="item-title">${task.text}</div>
                        <div class="item-time">⏱️ ${task.time} minutos</div>
                    </div>
                    <div style="display: flex; gap: 5px;">
                        <button onclick="toggleTask(${task.id})" style="background: var(--blue);">
                            ${task.completed ? '↩️' : '✓'}
                        </button>
                        <button class="del-btn" onclick="deleteTask(${task.id})">🗑️</button>
                    </div>
                </div>
            `).join('');
        }

        // Deletar tarefa
        function deleteTask(id) {
            tasks = tasks.filter(t => t.id !== id);
            saveTasks();
            renderTasks();
        }

        // Marcar/desmarcar tarefa
        function toggleTask(id) {
            const task = tasks.find(t => t.id === id);
            if (task) {
                task.completed = !task.completed;
                saveTasks();
                renderTasks();
            }
        }

        // Timer Pomodoro
        function startTimer() {
            if (!isRunning) {
                isRunning = true;
                document.getElementById('startBtn').classList.add('hidden');
                document.getElementById('pauseBtn').classList.remove('hidden');

                timerInterval = setInterval(() => {
                    timeLeft--;
                    updateTimerDisplay();

                    if (timeLeft <= 0) {
                        clearInterval(timerInterval);
                        isRunning = false;
                        pomodoroSessions++;
                        alert('⏰ Ciclo Pomodoro completo! Descanse um pouco.');
                        resetTimer();
                    }
                }, 1000);
            }
        }

        function pauseTimer() {
            isRunning = false;
            clearInterval(timerInterval);
            document.getElementById('startBtn').classList.remove('hidden');
            document.getElementById('pauseBtn').classList.add('hidden');
        }

        function resetTimer() {
            clearInterval(timerInterval);
            timeLeft = 25 * 60;
            isRunning = false;
            updateTimerDisplay();
            document.getElementById('startBtn').classList.remove('hidden');
            document.getElementById('pauseBtn').classList.add('hidden');
        }

        function updateTimerDisplay() {
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;
            document.getElementById('timerDisplay').textContent = 
                `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
        }

        // Atualizar relatório
        function updateReport() {
            const completed = tasks.filter(t => t.completed).length;
            const total = tasks.length;
            const totalTime = tasks.reduce((sum, t) => sum + t.time, 0);

            document.getElementById('totalTasks').textContent = total;
            document.getElementById('completedTasks').textContent = completed;
            document.getElementById('totalTime').textContent = Math.round(totalTime / 60) + 'h';
            document.getElementById('pomodoroSessions').textContent = pomodoroSessions;
        }

        // Atualizar exibição do usuário
        function updateUserDisplay() {
            if (currentUser) {
                document.getElementById('avatarDisplay').textContent = currentUser.username[0].toUpperCase();
                document.getElementById('usernameDisplay').textContent = currentUser.username;
            }
        }

        // Salvar dados
        function saveTasks() {
            localStorage.setItem('tasks', JSON.stringify(tasks));
        }

        function loadUserData() {
            const savedTasks = localStorage.getItem('tasks');
            if (savedTasks) {
                tasks = JSON.parse(savedTasks);
                renderTasks();
            }
        }

        // Inicialização
        window.onload = function() {
            const savedUser = localStorage.getItem('user');
            if (savedUser) {
                currentUser = JSON.parse(savedUser);
                loadUserData();
                showScreen('main');
            } else {
                showScreen('auth');
            }
        };
    </script>
</body>
</html>