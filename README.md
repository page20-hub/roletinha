# Roleta Magica
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Sistema de Roleta Completo</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@600&display=swap');

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
            color: #fff;
            text-align: center;
            padding: 20px;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            margin: 0;
            position: relative;
        }

        /* --- Estilos Gerais --- */
        .page {
            width: 100%;
            max-width: 600px;
            display: none;
            animation: fadeIn 0.8s ease-out;
        }

        .page.active {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        h1 {
            font-size: 2.5rem;
            margin-bottom: 20px;
            text-shadow: 0 2px 8px rgba(0,0,0,0.7);
        }
        
        .container {
            background-color: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 4px 30px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 400px;
            border: 1px solid rgba(255, 255, 255, 0.3);
            margin-bottom: 20px;
        }

        button {
            padding: 12px 25px;
            border: none;
            border-radius: 5px;
            background-color: #1e90ff;
            color: #fff;
            font-weight: bold;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #0d82d4;
        }
        input[type="text"] {
            width: calc(100% - 20px);
            padding: 10px;
            border: none;
            border-radius: 5px;
            margin-bottom: 15px;
            background-color: rgba(255, 255, 255, 0.2);
            color: white;
            font-size: 1rem;
            transition: background-color 0.3s ease;
        }
        input[type="text"]::placeholder {
            color: rgba(255, 255, 255, 0.7);
        }
        p {
            font-size: 1.1rem;
            margin-bottom: 20px;
        }
        #mensagem {
            margin-top: 15px;
            font-weight: bold;
        }

        /* --- Estilos da Página Inicial --- */
        #home-page {
            max-width: 500px;
        }
        #btnAdmin {
            position: absolute;
            top: 20px;
            right: 20px;
            background: #000;
            border: 2px solid #fff;
            color: #fff;
            padding: 8px 15px;
            font-size: 0.9rem;
            text-decoration: none;
        }

        /* --- Estilos da Página ADM --- */
        #admin-page h2 {
            font-size: 2rem;
            margin-top: 0;
            border-bottom: 2px solid rgba(255, 255, 255, 0.3);
            padding-bottom: 10px;
        }
        #admin-page button.admin-button {
            background-color: #007bff;
            margin: 5px;
        }
        #admin-page button.admin-button:hover {
            background-color: #0056b3;
        }
        ul {
            list-style-type: none;
            padding: 0;
            text-align: left;
            max-height: 300px;
            overflow-y: auto;
        }
        li {
            background-color: rgba(255, 255, 255, 0.1);
            margin-bottom: 8px;
            padding: 10px;
            border-radius: 4px;
            border-left: 5px solid #1e90ff;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        li .action-buttons-user {
            display: flex;
            gap: 10px;
        }
        li .edit-button {
            background-color: #ffc107;
            color: #333;
            padding: 5px 10px;
            font-size: 0.8rem;
        }
        li .edit-button:hover {
            background-color: #e0a800;
        }
        li .delete-button {
            background-color: #dc3545;
            color: white;
            padding: 5px 10px;
            font-size: 0.8rem;
        }
        li .delete-button:hover {
            background-color: #c82333;
        }
        .action-buttons {
            display: flex;
            justify-content: space-around;
            width: 100%;
            margin-top: 20px;
        }
        .action-buttons button {
            background-color: #dc3545;
        }
        .action-buttons button:hover {
            background-color: #c82333;
        }
        .log-container {
            margin-top: 40px;
            text-align: left;
        }
        .log-container h3 {
            border-bottom: 2px solid rgba(255, 255, 255, 0.3);
            padding-bottom: 8px;
        }

        /* --- Estilos da Roleta --- */
        #roleta-page {
            max-width: none;
        }
        #welcome-message {
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 0 2px 8px rgba(0,0,0,0.7);
            color: #fff;
        }
        #current-time {
            font-size: 1.2rem;
            margin-bottom: 20px;
            color: rgba(255, 255, 255, 0.8);
        }
        #container {
            position: relative;
            width: 320px;
            height: 320px;
            margin-bottom: 40px;
            border-radius: 50%;
            border: 8px solid #000;
            background: conic-gradient(
                #1e90ff 0deg 180deg,
                #ff3b3b 180deg 360deg
            );
            box-shadow: 0 0 20px rgba(0,0,0,0.8);
            transition: transform 4s cubic-bezier(0.33, 1, 0.68, 1);
            cursor: pointer;
            user-select: none;
            z-index: 1;
        }
        #seta {
            position: absolute;
            top: -60px;
            left: 50%;
            width: 0;
            height: 0;
            border-left: 25px solid transparent;
            border-right: 25px solid transparent;
            border-bottom: 40px solid #fff;
            filter: drop-shadow(0 0 3px rgba(0,0,0,0.9));
            user-select: none;
            transition: left 0.5s ease, border-bottom-color 0.5s ease;
            transform: translateX(-50%);
            z-index: 10;
        }
        #girarBtn {
            background: #000;
            color: #1e90ff;
            font-weight: 700;
            font-size: 1.3rem;
            padding: 15px 40px;
            border: 3px solid #1e90ff;
            border-radius: 50px;
            box-shadow: 0 6px 15px rgba(30,144,255,0.5);
            user-select: none;
        }
        #girarBtn:hover:not(:disabled) {
            background: #1e90ff;
            color: #000;
            box-shadow: 0 8px 25px rgba(30,144,255,0.8);
            border-color: #000;
        }
        #girarBtn:disabled {
            background: #555;
            color: #999;
            cursor: not-allowed;
            box-shadow: none;
            border-color: #444;
        }
        #resultado {
            margin-top: 30px;
            font-size: 2rem;
            font-weight: 700;
            min-height: 50px;
            text-shadow: 0 2px 6px rgba(0,0,0,0.7);
            user-select: none;
            letter-spacing: 1px;
        }
        .back-button {
            margin-top: 20px;
            background: #fff;
            color: #333;
        }
    </style>
</head>
<body>

    <button id="btnAdmin" onclick="abrirPainelAdmin()">ADM</button>

    <div id="home-page" class="page active">
        <div class="container">
            <h1>Acesso à Roleta</h1>
            <p>Por favor, insira seus dados para continuar.</p>
            <input type="text" id="userInputHome" placeholder="Digite seu Nome de Usuário">
            <input type="text" id="idInputUser" placeholder="Digite seu ID">
            <button onclick="acessarRoleta()">Acessar</button>
            <p id="mensagem"></p>
        </div>
    </div>

    <div id="admin-page" class="page">
        <h1>Painel do Administrador</h1>
        <div class="container">
            <h2>Adicionar Participante</h2>
            <input type="text" id="idInput" placeholder="ID do participante">
            <input type="text" id="userInput" placeholder="Nome do usuário">
            <button onclick="adicionarID()" class="admin-button">Adicionar</button>
        </div>
        <div class="container">
            <h2>Participantes Registrados:</h2>
            <ul id="listaIds"></ul>
        </div>
        <div class="container log-container">
            <h2>Histórico de Giros:</h2>
            <ul id="historicoGiro"></ul>
        </div>
        <div class="action-buttons">
            <button onclick="mostrarPagina('home-page')" class="back-button">Voltar</button>
            <button onclick="resetarDados()" class="back-button">Resetar Dados</button>
        </div>
    </div>

    <div id="roleta-page" class="page">
        <h1 id="welcome-message">Seja Bem Vindo!</h1>
        <p id="current-time"></p>
        <h1>Roleta Mágica</h1>
        <div id="container"></div>
        <div id="seta"></div>
        <button id="girarBtn">Girar Roleta</button>
        <div id="resultado"></div>
        <button onclick="mostrarPagina('home-page')" class="back-button">Voltar</button>
    </div>

    <script src="https://www.gstatic.com/firebasejs/8.6.8/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.6.8/firebase-database.js"></script>

    <script>
        // *** 1. COPIE E COLE SUA CONFIGURAÇÃO DO FIREBASE AQUI ***
        const firebaseConfig = {
          apiKey: "SUA_API_KEY",
          authDomain: "SEU_AUTH_DOMAIN",
          projectId: "SEU_PROJECT_ID",
          databaseURL: "SUA_DATABASE_URL",
          storageBucket: "SEU_STORAGE_BUCKET",
          messagingSenderId: "SEU_MESSAGING_SENDER_ID",
          appId: "SEU_APP_ID"
        };
        // Inicializa o Firebase
        firebase.initializeApp(firebaseConfig);
        const database = firebase.database();
        const listaIDsRef = database.ref('usuarios');
        const historicoGiroRef = database.ref('historico');

        let listaIDs = [];
        let historicoGiro = [];
        let usuarioAtual = null;

        // --- Funções de Sincronização em Tempo Real ---
        listaIDsRef.on('value', (snapshot) => {
            const data = snapshot.val();
            listaIDs = data ? Object.values(data) : [];
            atualizarLista();
        });

        historicoGiroRef.on('value', (snapshot) => {
            const data = snapshot.val();
            historicoGiro = data ? Object.values(data) : [];
            atualizarHistoricoGiro();
        });

        // --- Funções de Navegação ---
        function mostrarPagina(pageId) {
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            document.getElementById(pageId).classList.add('active');
            
            if (pageId === 'roleta-page') {
                document.getElementById('welcome-message').textContent = `Seja Bem Vindo, ${usuarioAtual.usuario}!`;
                updateCurrentTime();
            }
        }

        // Função para atualizar o horário
        function updateCurrentTime() {
            const now = new Date();
            document.getElementById('current-time').textContent = now.toLocaleString('pt-BR', {
                weekday: 'short', year: 'numeric', month: 'short', day: 'numeric',
                hour: '2-digit', minute: '2-digit', second: '2-digit',
                timeZoneName: 'short'
            });
        }
        setInterval(updateCurrentTime, 1000);

        // --- Funções do ADM e Usuário ---
        function atualizarLista() {
            const ul = document.getElementById("listaIds");
            ul.innerHTML = "";
            listaIDs.forEach(user => {
                let li = document.createElement("li");
                li.innerHTML = `
                    <span>ID: ${user.id} | Usuário: ${user.usuario}</span>
                    <div class="action-buttons-user">
                        <button class="edit-button" onclick="editarUsuario('${user.id}')">Editar</button>
                        <button class="delete-button" onclick="excluirUsuario('${user.id}')">Excluir</button>
                    </div>
                `;
                ul.appendChild(li);
            });
        }

        function atualizarHistoricoGiro() {
            const ul = document.getElementById("historicoGiro");
            ul.innerHTML = "";
            historicoGiro.forEach(log => {
                let li = document.createElement("li");
                li.textContent = `[${log.horario}] - Usuário: ${log.usuario} - Cor: ${log.cor}`;
                ul.appendChild(li);
            });
        }

        function abrirPainelAdmin() {
            const senha = prompt("Por favor, digite a senha de acesso:");
            if (senha === "20082002") {
                mostrarPagina('admin-page');
            } else {
                alert("Senha incorreta!");
            }
        }

        function adicionarID() {
            const idInput = document.getElementById("idInput");
            const userInput = document.getElementById("userInput");
            const novoID = idInput.value.trim();
            const novoUsuario = userInput.value.trim();
            
            if (novoID === "" || novoUsuario === "") {
                alert("Por favor, preencha todos os campos.");
                return;
            }
            if (listaIDs.some(user => user.id === novoID)) {
                alert("Este ID já está registrado.");
                return;
            }

            const novoUsuarioRef = listaIDsRef.child(novoID);
            novoUsuarioRef.set({
                id: novoID, 
                usuario: novoUsuario
            });

            idInput.value = "";
            userInput.value = "";
            alert("Participante registrado com sucesso!");
        }

        function editarUsuario(id) {
            const userParaEditar = listaIDs.find(user => user.id === id);
            if (userParaEditar) {
                const novoNome = prompt(`Digite o novo nome para o usuário com ID ${id}:`, userParaEditar.usuario);
                if (novoNome !== null && novoNome.trim() !== "") {
                    listaIDsRef.child(id).update({
                        usuario: novoNome.trim()
                    });
                    alert("Nome do usuário alterado com sucesso!");
                }
            }
        }
        
        function excluirUsuario(id) {
            const confirmacao = confirm(`Você tem certeza que deseja excluir o usuário com ID ${id}?`);
            if (confirmacao) {
                listaIDsRef.child(id).remove();
                alert("Usuário excluído com sucesso.");
            }
        }

        function resetarDados() {
            const confirmacao = confirm("Você tem certeza que deseja resetar TODOS os dados (usuários e histórico)? Esta ação é irreversível.");
            if (confirmacao) {
                listaIDsRef.remove();
                historicoGiroRef.remove();
                alert("Todos os dados foram resetados com sucesso.");
            }
        }

        function acessarRoleta() {
            const idInput = document.getElementById("idInputUser");
            const userInput = document.getElementById("userInputHome");
            const idUsuario = idInput.value.trim();
            const nomeUsuario = userInput.value.trim();
            const mensagem = document.getElementById("mensagem");

            if (idUsuario === "" || nomeUsuario === "") {
                mensagem.textContent = "Por favor, preencha todos os campos.";
                mensagem.style.color = "red";
                return;
            }

            const usuarioValido = listaIDs.find(user => user.id === idUsuario && user.usuario.toLowerCase() === nomeUsuario.toLowerCase());

            if (usuarioValido) {
                mensagem.textContent = "Acesso concedido! Carregando a roleta...";
                mensagem.style.color = "green";
                usuarioAtual = usuarioValido;
                setTimeout(() => {
                    mostrarPagina('roleta-page');
                }, 1000);
            } else {
                mensagem.textContent = "ID ou Usuário não registrado. Acesso negado.";
                mensagem.style.color = "red";
            }
        }

        // --- Lógica da Roleta ---
        const roleta = document.getElementById('container');
        const seta = document.getElementById('seta');
        const btnGirar = document.getElementById('girarBtn');
        const resultado = document.getElementById('resultado');

        let girando = false;

        btnGirar.addEventListener('click', () => {
            if (girando) return;
            girando = true;
            resultado.textContent = '';
            btnGirar.disabled = true;

            seta.style.left = '50%';
            seta.style.borderBottomColor = '#fff';

            const escolha = Math.floor(Math.random() * 2);
            const corVencedora = escolha === 0 ? 'Azul' : 'Vermelho';

            const anguloBase = escolha === 0 ? 0 : 180;
            const anguloAleatorio = anguloBase + Math.random() * 180;
            const voltas = 5;
            const anguloFinal = voltas * 360 + anguloAleatorio;

            roleta.style.transition = 'transform 4s cubic-bezier(0.33, 1, 0.68, 1)';
            roleta.style.transform = `rotate(${anguloFinal}deg)`;

            roleta.addEventListener('transitionend', function handler() {
                const anguloAjustado = anguloAleatorio % 360;
                roleta.style.transition = 'none';
                roleta.style.transform = `rotate(${anguloAjustado}deg)`;

                if (escolha === 0) {
                    seta.style.left = '25%';
                    seta.style.borderBottomColor = '#1e90ff';
                } else {
                    seta.style.left = '75%';
                    seta.style.borderBottomColor = '#ff3b3b';
                }

                resultado.textContent = `A cor selecionada foi: ${corVencedora}`;
                
                // Salva o log do giro
                const data = new Date();
                const log = {
                    horario: data.toLocaleString('pt-BR'),
                    usuario: usuarioAtual.usuario,
                    cor: corVencedora
                };

                const novoLogRef = historicoGiroRef.push();
                novoLogRef.set(log);

                girando = false;
                btnGirar.disabled = false;
                roleta.removeEventListener('transitionend', handler);
            });
        });

        // Inicializa a página
        mostrarPagina('home-page');
    </script>
</body>
</html>
