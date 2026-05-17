[index.html](https://github.com/user-attachments/files/27901322/index.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>StudioThaisSerra - Sistema de Gestão</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        .bg-gradient-salao { background: linear-gradient(135deg, #fff0f5 0%, #fae1eb 100%); }
        .tab-active { border-bottom-color: #ec4899; color: #ec4899; font-weight: bold; }
    </style>
</head>
<body class="bg-gradient-salao min-h-screen text-gray-800 font-sans">

    <div id="telaLogin" class="fixed inset-0 bg-pink-50 flex items-center justify-center p-4 z-50">
        <div class="bg-white rounded-2xl max-w-sm w-full p-6 shadow-xl border border-pink-100 text-center">
            <div class="w-16 h-16 bg-pink-500 rounded-full flex items-center justify-center text-white text-2xl font-bold mx-auto mb-4 shadow-md">T</div>
            <h2 class="text-2xl font-bold text-gray-700 mb-6">Studio<span class="text-pink-500">ThaisSerra</span></h2>
            
            <div id="selecaoPerfil" class="space-y-3">
                <p class="text-gray-500 text-sm mb-4">Escolha o seu perfil de acesso:</p>
                <button onclick="escolherPerfil('admin')" class="w-full bg-pink-500 hover:bg-pink-600 text-white font-semibold py-3 rounded-xl transition-colors flex items-center justify-center gap-2">
                    <i class="fas fa-user-shield"></i> Entrar como Admin
                </button>
                <button onclick="escolherPerfil('funcionario')" class="w-full bg-gray-700 hover:bg-gray-800 text-white font-semibold py-3 rounded-xl transition-colors flex items-center justify-center gap-2">
                    <i class="fas fa-users"></i> Entrar como Funcionário
                </button>
            </div>

            <form id="formLogin" class="space-y-4 hidden mt-4">
                <p id="textoLoginPerfil" class="text-sm font-medium text-gray-600"></p>
                <input type="password" id="senhaAcesso" placeholder="Digite a Senha" class="w-full px-4 py-2.5 rounded-xl border border-gray-200 text-center text-lg focus:outline-none focus:border-pink-400" required>
                <div class="flex gap-2">
                    <button type="button" onclick="voltarParaPerfeis()" class="w-1/2 bg-gray-200 text-gray-600 font-semibold py-2.5 rounded-xl">Voltar</button>
                    <button type="submit" class="w-1/2 bg-pink-500 hover:bg-pink-600 text-white font-semibold py-2.5 rounded-xl">Entrar</button>
                </div>
            </form>
            <p id="erroLogin" class="text-red-500 text-sm mt-2 hidden">Senha incorreta! Tente novamente.</p>
        </div>
    </div>

    <div id="conteudoSistema" class="hidden">
        <nav class="bg-white shadow-md px-6 py-4 flex justify-between items-center border-b border-pink-200">
            <div class="flex items-center space-x-2">
                <div class="w-10 h-10 bg-pink-500 rounded-full flex items-center justify-center text-white font-bold text-xl shadow-md">T</div>
                <span class="text-2xl font-bold tracking-wide text-gray-700">Studio<span class="text-pink-500">ThaisSerra</span></span>
            </div>
            <div class="flex items-center space-x-4">
                <span id="badgePerfil" class="text-xs px-3 py-1 rounded-full font-semibold border"></span>
                <button onclick="logout()" class="text-xs text-gray-400 hover:text-red-500 transition-colors"><i class="fas fa-sign-out-alt mr-1"></i>Sair</button>
            </div>
        </nav>

        <div class="bg-white shadow-sm border-b border-gray-100">
            <div class="max-w-7xl mx-auto flex space-x-8 px-6 text-gray-500 font-medium">
                <button onclick="mudarAba('inicio')" id="btn-inicio" class="py-4 border-b-2 border-transparent hover:text-pink-500 transition-colors tab-active">
                    <i class="fas fa-home mr-2"></i>Início
                </button>
                <button onclick="mudarAba('agenda')" id="btn-agenda" class="py-4 border-b-2 border-transparent hover:text-pink-500 transition-colors">
                    <i class="fas fa-calendar-alt mr-2"></i>Agenda
                </button>
                <button onclick="mudarAba('clientes')" id="btn-clientes" class="py-4 border-b-2 border-transparent hover:text-pink-500 transition-colors abaAdmin">
                    <i class="fas fa-users mr-2"></i>Clientes
                </button>
                <button onclick="mudarAba('servicos')" id="btn-servicos" class="py-4 border-b-2 border-transparent hover:text-pink-500 transition-colors abaAdmin">
                    <i class="fas fa-cut mr-2"></i>Serviços & Preços
                </button>
            </div>
        </div>

        <main class="max-w-7xl mx-auto px-4 py-8">
            <section id="aba-inicio" class="space-y-8">
                <div class="bg-white rounded-2xl p-6 shadow-sm border border-pink-100 flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                    <div>
                        <h1 class="text-2xl md:text-3xl font-bold text-gray-800">Olá, StudioThaisSerra! ✨</h1>
                        <p class="text-gray-500 mt-1">Gerencie os horários e agendamentos do salão aqui.</p>
                    </div>
                    <button onclick="abrirModal()" class="bg-pink-500 hover:bg-pink-600 text-white font-semibold px-5 py-2.5 rounded-xl shadow-md transition-all flex items-center gap-2">
                        <i class="fas fa-plus"></i> Novo Agendamento
                    </button>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <div class="bg-white p-6 rounded-2xl shadow-sm border border-pink-100 flex items-center justify-between">
                        <div><p class="text-sm font-medium text-gray-400 uppercase">Agendados</p><p id="resumoAgendamentos" class="text-3xl font-bold text-gray-800 mt-1">0</p></div>
                        <div class="w-12 h-12 bg-pink-100 rounded-xl flex items-center justify-center text-pink-500 text-xl"><i class="fas fa-calendar-check"></i></div>
                    </div>
                    <div class="bg-white p-6 rounded-2xl shadow-sm border border-pink-100 flex items-center justify-between cardAdmin">
                        <div><p class="text-sm font-medium text-gray-400 uppercase">Clientes Cadastrados</p><p id="resumoClientes" class="text-3xl font-bold text-gray-800 mt-1">0</p></div>
                        <div class="w-12 h-12 bg-purple-100 rounded-xl flex items-center justify-center text-purple-500 text-xl"><i class="fas fa-users"></i></div>
                    </div>
                    <div class="bg-white p-6 rounded-2xl shadow-sm border border-pink-100 flex items-center justify-between cardAdmin">
                        <div><p class="text-sm font-medium text-gray-400 uppercase">Serviços no Catálogo</p><p id="resumoServicos" class="text-3xl font-bold text-gray-800 mt-1">0</p></div>
                        <div class="w-12 h-12 bg-amber-100 rounded-xl flex items-center justify-center text-amber-500 text-xl"><i class="fas fa-cut"></i></div>
                    </div>
                </div>
            </section>

            <section id="aba-agenda" class="hidden space-y-6">
                <div class="flex justify-between items-center">
                    <h2 class="text-2xl font-bold text-gray-800"><i class="fas fa-calendar-alt text-pink-500 mr-2"></i>Compromissos Agendados</h2>
                    <button onclick="abrirModal()" class="bg-pink-500 hover:bg-pink-600 text-white font-sm px-4 py-2 rounded-xl transition-all">
                        <i class="fas fa-plus mr-1"></i> Agendar
                    </button>
                </div>
                <div class="bg-white rounded-2xl p-6 shadow-sm border border-pink-100 overflow-x-auto">
                    <table class="w-full text-left border-collapse">
                        <thead>
                            <tr class="border-b border-gray-100 text-gray-400 text-sm font-medium">
                                <th class="pb-3">Cliente</th><th class="pb-3">Procedimento</th><th class="pb-3">Data</th><th class="pb-3">Horário</th><th class="pb-3 text-right">Ações</th>
                            </tr>
                        </thead>
                        <tbody id="listaAgenda" class="divide-y divide-gray-50 text-gray-700"></tbody>
                    </table>
                </div>
            </section>

            <section id="aba-clientes" class="hidden grid grid-cols-1 lg:grid-cols-3 gap-8">
                <div class="bg-white rounded-2xl p-6 shadow-sm border border-pink-100 h-fit">
                    <h2 id="tituloFormCliente" class="text-xl font-bold text-gray-800 mb-4"><i class="fas fa-user-plus text-pink-500 mr-2"></i>Novo Cliente</h2>
                    <form id="formCliente" class="space-y-4">
                        <input type="hidden" id="editClienteId">
                        <div><label class="block text-sm font-semibold text-gray-600 mb-1">Nome Completo</label><input type="text" id="nomeCadCliente" placeholder="Ex: Maria Silva" class="w-full px-4 py-2.5 rounded-xl border border-gray-200 focus:outline-none" required></div>
                        <div><label class="block text-sm font-semibold text-gray-600 mb-1">WhatsApp</label><input type="text" id="telCadCliente" placeholder="(85) 99999-0000" class="w-full px-4 py-2.5 rounded-xl border border-gray-200 focus:outline-none"></div>
                        <button type="submit" id="btnSalvarCliente" class="w-full bg-gray-800 hover:bg-gray-900 text-white font-semibold py-2.5 rounded-xl transition-colors">Salvar Cliente</button>
                        <button type="button" id="btnCancelarEditCliente" onclick="resetarFormCliente()" class="w-full bg-gray-200 text-gray-600 font-semibold py-2 rounded-xl transition-colors hidden">Cancelar Edição</button>
                    </form>
                </div>
                <div class="lg:col-span-2 bg-white rounded-2xl p-6 shadow-sm border border-pink-100">
                    <h2 class="text-xl font-bold text-gray-800 mb-4"><i class="fas fa-users text-pink-500 mr-2"></i>Lista de Clientes</h2>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="border-b border-gray-100 text-gray-400 text-sm font-medium">
                                    <th class="pb-3">Nome</th><th class="pb-3">Contato</th><th class="pb-3 text-right">Ações</th>
                                </tr>
                            </thead>
                            <tbody id="listaClientes" class="divide-y divide-gray-50 text-gray-700"></tbody>
                        </table>
                    </div>
                </div>
            </section>

            <section id="aba-servicos" class="hidden grid grid-cols-1 lg:grid-cols-3 gap-8">
                <div class="bg-white rounded-2xl p-6 shadow-sm border border-pink-100 h-fit">
                    <h2 id="tituloFormServico" class="text-xl font-bold text-gray-800 mb-4"><i class="fas fa-plus-circle text-pink-500 mr-2"></i>Novo Serviço</h2>
                    <form id="formServico" class="space-y-4">
                        <input type="hidden" id="editServicoId">
                        <div><label class="block text-sm font-semibold text-gray-600 mb-1">Procedimento</label><input type="text" id="nomeServico" placeholder="Ex: Mechas" class="w-full px-4 py-2.5 rounded-xl border border-gray-200 focus:outline-none" required></div>
                        <div><label class="block text-sm font-semibold text-gray-600 mb-1">Preço (R$)</label><input type="number" step="0.01" id="precoServico" placeholder="0,00" class="w-full px-4 py-2.5 rounded-xl border border-gray-200 focus:outline-none" required></div>
                        <div><label class="block text-sm font-semibold text-gray-600 mb-1">Tempo (min)</label><input type="number" id="tempoServico" placeholder="60" class="w-full px-4 py-2.5 rounded-xl border border-gray-200 focus:outline-none"></div>
                        <button type="submit" id="btnSalvarServico" class="w-full bg-gray-800 hover:bg-gray-900 text-white font-semibold py-2.5 rounded-xl transition-colors">Salvar Serviço</button>
                        <button type="button" id="btnCancelarEditServico" onclick="resetarFormServico()" class="w-full bg-gray-200 text-gray-600 font-semibold py-2 rounded-xl transition-colors hidden">Cancelar Edição</button>
                    </form>
                </div>
                <div class="lg:col-span-2 bg-white rounded-2xl p-6 shadow-sm border border-pink-100">
                    <h2 class="text-xl font-bold text-gray-800 mb-4"><i class="fas fa-list-ul text-pink-500 mr-2"></i>Catálogo de Preços</h2>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="border-b border-gray-100 text-gray-400 text-sm font-medium">
                                    <th class="pb-3">Procedimento</th><th class="pb-3">Preço</th><th class="pb-3 text-right">Ações</th>
                                </tr>
                            </thead>
                            <tbody id="listaServicos" class="divide-y divide-gray-50 text-gray-700"></tbody>
                        </table>
                    </div>
                </div>
            </section>
        </main>

        <div id="modalAgendamento" class="hidden fixed inset-0 bg-black/50 flex items-center justify-center p-4 z-50">
            <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-xl relative">
                <button onclick="fecharModal()" class="absolute top-4 right-4 text-gray-400 text-xl">&times;</button>
                <h3 id="tituloModalAgenda" class="text-xl font-bold text-gray-800 mb-4">Agendar Horário</h3>
                <form id="formAgendamento" class="space-y-4">
                    <input type="hidden" id="editAgendaId">
                    <div>
                        <label class="block text-sm font-semibold text-gray-600 mb-1">Cliente</label>
                        <input type="text" id="inputClienteNome" list="datalistClientes" class="w-full px-4 py-2.5 rounded-xl border border-gray-200" placeholder="Digite ou selecione o nome..." required>
                        <datalist id="datalistClientes"></datalist>
                    </div>
                    <div>
                        <label class="block text-sm font-semibold text-gray-600 mb-1">Serviço</label>
                        <select id="selectServico" class="w-full px-4 py-2.5 rounded-xl border border-gray-200" required></select>
                    </div>
                    <div class="grid grid-cols-2 gap-4">
                        <div><label class="block text-sm font-semibold text-gray-600 mb-1">Data</label><input type="date" id="dataAgenda" class="w-full px-4 py-2.5 rounded-xl border border-gray-200" required></div>
                        <div><label class="block text-sm font-semibold text-gray-600 mb-1">Hora</label><input type="time" id="horaAgenda" class="w-full px-4 py-2.5 rounded-xl border border-gray-200" required></div>
                    </div>
                    <button type="submit" id="btnConfirmarAgenda" class="w-full bg-pink-500 hover:bg-pink-600 text-white font-semibold py-3 rounded-xl transition-colors">Confirmar Horário</button>
                </form>
            </div>
        </div>
    </div>

    <script>
        // CONFIGURAÇÕES DE SENHAS INICIAIS
        if (!localStorage.getItem("senhaAdmin")) localStorage.setItem("senhaAdmin", "1234");
        if (!localStorage.getItem("senhaFuncionario")) localStorage.setItem("senhaFuncionario", "4321"); // Senha das meninas

        let perfilSelecionado = "";

        function escolherPerfil(perfil) {
            perfilSelecionado = perfil;
            document.getElementById("selecaoPerfil").classList.add("hidden");
            document.getElementById("formLogin").classList.remove("hidden");
            document.getElementById("textoLoginPerfil").innerText = perfil === 'admin' ? "Entrando como Administradora" : "Entrando como Funcionária";
            document.getElementById("senhaAcesso").value = "";
            document.getElementById("senhaAcesso").focus();
        }

        function voltarParaPerfeis() {
            document.getElementById("selecaoPerfil").classList.remove("hidden");
            document.getElementById("formLogin").classList.add("hidden");
            document.getElementById("erroLogin").classList.add("hidden");
        }

        document.getElementById("formLogin").addEventListener("submit", function(e) {
            e.preventDefault();
            const senhaDigitada = document.getElementById("senhaAcesso").value;
            const senhaCorreta = perfilSelecionado === 'admin' ? localStorage.getItem("senhaAdmin") : localStorage.getItem("senhaFuncionario");

            if (senhaDigitada === senhaCorreta) {
                document.getElementById("telaLogin").classList.add("hidden");
                document.getElementById("conteudoSistema").classList.remove("hidden");
                configurarVisibilidadePerfil();
            } else {
                document.getElementById("erroLogin").classList.remove("hidden");
            }
        });

        function configurarVisibilidadePerfil() {
            const badge = document.getElementById("badgePerfil");
            if (perfilSelecionado === 'admin') {
                badge.innerText = "Modo: Admin";
                badge.className = "text-xs px-3 py-1 rounded-full font-semibold border bg-pink-100 text-pink-700 border-pink-300";
                // Mostrar abas exclusivas
                document.querySelectorAll(".abaAdmin, .cardAdmin").forEach(el => el.classList.remove("hidden"));
            } else {
                badge.innerText = "Modo: Funcionária";
                badge.className = "text-xs px-3 py-1 rounded-full font-semibold border bg-gray-100 text-gray-700 border-gray-300";
                // Esconder abas administrativas
                document.querySelectorAll(".abaAdmin, .cardAdmin").forEach(el => el.classList.add("hidden"));
                mudarAba('agenda'); // Força ir para a agenda
            }
        }

        function logout() {
            document.getElementById("conteudoSistema").classList.add("hidden");
            document.getElementById("telaLogin").classList.remove("hidden");
            voltarParaPerfeis();
        }

        function mudarAba(aba) {
            if (perfilSelecionado === 'funcionario' && (aba === 'clientes' || aba === 'servicos')) return;
            var abas = ['inicio', 'agenda', 'clientes', 'servicos'];
            for(var i = 0; i < abas.length; i++) {
                document.getElementById('aba-' + abas[i]).classList.add('hidden');
                document.getElementById('btn-' + abas[i]).classList.remove('tab-active');
            }
            document.getElementById('aba-' + aba).classList.remove('hidden');
            document.getElementById('btn-' + aba).classList.add('tab-active');
        }
        
        function abrirModal() { 
            document.getElementById("modalAgendamento").classList.remove("hidden"); 
        }
        
        function fecharModal() { 
            document.getElementById("modalAgendamento").classList.add("hidden"); 
            document.getElementById("formAgendamento").reset();
            document.getElementById("editAgendaId").value = "";
            document.getElementById("tituloModalAgenda").innerText = "Agendar Horário";
            document.getElementById("btnConfirmarAgenda").innerText = "Confirmar Horário";
        }

        function resetarFormCliente() {
            document.getElementById("formCliente").reset();
            document.getElementById("editClienteId").value = "";
            document.getElementById("tituloFormCliente").innerHTML = '<i class="fas fa-user-plus text-pink-500 mr-2"></i>Novo Cliente';
            document.getElementById("btnSalvarCliente").innerText = "Salvar Cliente";
            document.getElementById("btnCancelarEditCliente").classList.add("hidden");
        }

        function resetarFormServico() {
            document.getElementById("formServico").reset();
            document.getElementById("editServicoId").value = "";
            document.getElementById("tituloFormServico").innerHTML = '<i class="fas fa-plus-circle text-pink-500 mr-2"></i>Novo Serviço';
            document.getElementById("btnSalvarServico").innerText = "Salvar Serviço";
            document.getElementById("btnCancelarEditServico").classList.add("hidden");
        }
    </script>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
        import { getFirestore, collection, addDoc, onSnapshot, doc, deleteDoc, updateDoc } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

        const firebaseConfig = {
            apiKey: "AIzaSyAiNwTa_UXYAPoSaclVSEATyScMCpCLnQw",
            authDomain: "salaopro-ab385.firebaseapp.com",
            projectId: "salaopro-ab385",
            storageBucket: "salaopro-ab385.firebasestorage.app",
            messagingSenderId: "1018725024284",
            appId: "1:1018725024284:web:b9ceb76498d6bb986495d9"
        };

        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);

        const servicosRef = collection(db, "servicos");
        const clientesRef = collection(db, "clientes");
        const agendaRef = collection(db, "agenda");

        // LISTAR SERVIÇOS
        onSnapshot(servicosRef, (snapshot) => {
            const lista = document.getElementById("listaServicos");
            const select = document.getElementById("selectServico");
            document.getElementById("resumoServicos").innerText = snapshot.size;
            lista.innerHTML = ""; select.innerHTML = '<option value="">Escolha o procedimento...</option>';
            snapshot.forEach((doc) => {
                const item = doc.data();
                lista.innerHTML += `<tr>
                    <td class="py-3 font-medium">${item.nome}</td>
                    <td class="text-pink-600 font-bold">R$ ${parseFloat(item.preco).toFixed(2)}</td>
                    <td class="text-right space-x-2">
                        <button onclick="window.carregarDadosServico('${doc.id}', '${item.nome}', '${item.preco}', '${item.tempo || ''}')" class="text-blue-400 hover:text-blue-600"><i class="fas fa-edit"></i></button>
                        <button onclick="window.deletarItem('servicos', '${doc.id}')" class="text-gray-400 hover:text-red-500"><i class="fas fa-trash-alt"></i></button>
                    </td>
                </tr>`;
                select.innerHTML += `<option value="${item.nome}">${item.nome}</option>`;
            });
        });

        document.getElementById("formServico").addEventListener("submit", async (e) => {
            e.preventDefault();
            const id = document.getElementById("editServicoId").value;
            const dados = {
                nome: document.getElementById("nomeServico").value,
                preco: document.getElementById("precoServico").value,
                tempo: document.getElementById("tempoServico").value
            };
            if (id) {
                await updateDoc(doc(db, "servicos", id), dados);
                resetarFormServico();
            } else {
                await addDoc(servicosRef, dados);
                document.getElementById("formServico").reset();
            }
        });

        window.carregarDadosServico = (id, nome, preco, tempo) => {
            document.getElementById("editServicoId").value = id;
            document.getElementById("nomeServico").value = nome;
            document.getElementById("precoServico").value = preco;
            document.getElementById("tempoServico").value = tempo;
            document.getElementById("tituloFormServico").innerHTML = '<i class="fas fa-edit text-blue-500 mr-2"></i>Editar Serviço';
            document.getElementById("btnSalvarServico").innerText = "Atualizar Serviço";
            document.getElementById("btnCancelarEditServico").classList.remove("hidden");
        };

        // LISTAR CLIENTES
        onSnapshot(clientesRef, (snapshot) => {
            const lista = document.getElementById("listaClientes");
            const datalist = document.getElementById("datalistClientes");
            document.getElementById("resumoClientes").innerText = snapshot.size;
            lista.innerHTML = ""; datalist.innerHTML = "";
            snapshot.forEach((doc) => {
                const item = doc.data();
                lista.innerHTML += `<tr>
                    <td class="py-3 font-medium">${item.nome}</td>
                    <td>${item.telefone || '---'}</td>
                    <td class="text-right space-x-2">
                        <button onclick="window.carregarDadosCliente('${doc.id}', '${item.nome}', '${item.telefone || ''}')" class="text-blue-400 hover:text-blue-600"><i class="fas fa-edit"></i></button>
                        <button onclick="window.deletarItem('clientes', '${doc.id}')" class="text-gray-400 hover:text-red-500"><i class="fas fa-trash-alt"></i></button>
                    </td>
                </tr>`;
                datalist.innerHTML += `<option value="${item.nome}">`;
            });
        });

        document.getElementById("formCliente").addEventListener("submit", async (e) => {
            e.preventDefault();
            const id = document.getElementById("editClienteId").value;
            const dados = {
                nome: document.getElementById("nomeCadCliente").value,
                telefone: document.getElementById("telCadCliente").value
            };
            if (id) {
                await updateDoc(doc(db, "clientes", id), dados);
                resetarFormCliente();
            } else {
                await addDoc(clientesRef, dados);
                document.getElementById("formCliente").reset();
            }
        });

        window.carregarDadosCliente = (id, nome, telefone) => {
            document.getElementById("editClienteId").value = id;
            document.getElementById("nomeCadCliente").value = nome;
            document.getElementById("telCadCliente").value = telefone;
            document.getElementById("tituloFormCliente").innerHTML = '<i class="fas fa-edit text-blue-500 mr-2"></i>Editar Cliente';
            document.getElementById("btnSalvarCliente").innerText = "Atualizar Cliente";
            document.getElementById("btnCancelarEditCliente").classList.remove("hidden");
        };

        // LISTAR AGENDA
        onSnapshot(agendaRef, (snapshot) => {
            const lista = document.getElementById("listaAgenda");
            document.getElementById("resumoAgendamentos").innerText = snapshot.size;
            lista.innerHTML = "";
            if(snapshot.empty) { lista.innerHTML = `<tr><td colspan="5" class="py-4 text-center text-gray-400">Nenhum agendamento cadastrado.</td></tr>`; return; }
            snapshot.forEach((doc) => {
                const item = doc.data();
                const dataF = item.data.split('-').reverse().join('/');
                lista.innerHTML += `<tr>
                    <td class="py-3 font-medium">${item.cliente}</td>
                    <td class="text-pink-600">${item.servico}</td>
                    <td>${dataF}</td>
                    <td>${item.hora}</td>
                    <td class="text-right space-x-2">
                        <button onclick="window.carregarDadosAgenda('${doc.id}', '${item.cliente}', '${item.servico}', '${item.data}', '${item.hora}')" class="text-blue-400 hover:text-blue-600"><i class="fas fa-edit"></i></button>
                        <button onclick="window.deletarItem('agenda', '${doc.id}')" class="text-gray-400 hover:text-red-500"><i class="fas fa-trash-alt"></i></button>
                    </td>
                </tr>`;
            });
        });

        document.getElementById("formAgendamento").addEventListener("submit", async (e) => {
            e.preventDefault();
            const id = document.getElementById("editAgendaId").value;
            const dados = {
                cliente: document.getElementById("inputClienteNome").value,
                servico: document.getElementById("selectServico").value,
                data: document.getElementById("dataAgenda").value,
                hora: document.getElementById("horaAgenda").value
            };

            if (id) {
                await updateDoc(doc(db, "agenda", id), dados);
            } else {
                await addDoc(agendaRef, dados);
            }
            fecharModal();
        });

        window.carregarDadosAgenda = (id, cliente, servico, data, hora) => {
            document.getElementById("editAgendaId").value = id;
            document.getElementById("inputClienteNome").value = cliente;
            document.getElementById("selectServico").value = servico;
            document.getElementById("dataAgenda").value = data;
            document.getElementById("horaAgenda").value = hora;
            document.getElementById("tituloModalAgenda").innerText = "Editar Agendamento";
            document.getElementById("btnConfirmarAgenda").innerText = "Atualizar Horário";
            abrirModal();
        };

        window.deletarItem = async (colecao, id) => {
            if(confirm("Deseja apagar permanentemente?")) await deleteDoc(doc(db, colecao, id));
        };
    </script>
</body>
</html>
