<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<title>Hexag FC</title>

<style>
body{
  margin:0;
  font-family: Arial;
  background:#f5f5f5;
}

/* TOPO */
.topo{
  background:#f59e0b;
  color:white;
  padding:15px;
  font-weight:bold;
}

/* BANNER */
.banner{
  height:200px;
  background:linear-gradient(to bottom, #10b981, #065f46);
}

/* CONTEUDO */
.container{
  padding:15px;
}

/* CARD */
.card{
  background:white;
  padding:20px;
  border-radius:15px;
  box-shadow:0 2px 10px rgba(0,0,0,0.1);
  margin-top:15px;
}

/* LOGIN MODAL */
.modal{
  position:fixed;
  top:0;
  left:0;
  width:100%;
  height:100%;
  background:rgba(0,0,0,0.4);
  display:flex;
  align-items:center;
  justify-content:center;
}

.box{
  background:white;
  padding:30px;
  border-radius:15px;
  width:300px;
  text-align:center;
}

button{
  width:100%;
  padding:12px;
  margin-top:10px;
  border:none;
  border-radius:10px;
  cursor:pointer;
  font-weight:bold;
}

.btn1{background:#f59e0b;color:white;}
.btn2{background:#eee;}

input{
  width:100%;
  padding:10px;
  margin-top:10px;
  border-radius:10px;
  border:1px solid #ccc;
}
</style>

</head>
<body>

<!-- TOPO -->
<div class="topo">HEXAG FC</div>

<!-- BANNER -->
<div class="banner"></div>

<!-- CONTEÚDO -->
<div class="container">

<h3>🔴 Ao Vivo</h3>

<div class="card">
  <b>Pindorama</b>  
  <h2>0 x 0</h2>
  <b>Hexagonal</b>
</div>

<h3>📅 Próximas Partidas</h3>

<div id="lista"></div>

</div>

<!-- MODAL ESCOLHA -->
<div class="modal" id="modalEscolha">
  <div class="box">
    <h2>Acesso</h2>
    <button class="btn1" onclick="abrirAdmin()">Sou Administrador</button>
    <button class="btn2" onclick="abrirJogador()">Sou Jogador</button>
  </div>
</div>

<!-- MODAL ADMIN -->
<div class="modal" id="modalAdmin" style="display:none;">
  <div class="box">
    <h2>Painel Administrativo</h2>
    <input type="password" id="senhaAdmin" placeholder="Senha">
    <button class="btn1" onclick="loginAdmin()">Entrar</button>
    <button onclick="voltar()">Voltar</button>
  </div>
</div>

<!-- MODAL JOGADOR -->
<div class="modal" id="modalJogador" style="display:none;">
  <div class="box">
    <h2>Portal do Jogador</h2>
    <input type="password" id="senhaJogador" placeholder="Senha">
    <button class="btn1" onclick="loginJogador()">Entrar</button>
    <button onclick="voltar()">Voltar</button>
  </div>
</div>

<!-- PAINEL ADMIN -->
<div class="modal" id="painel" style="display:none;">
  <div class="box">
    <h2>Cadastro de Jogo</h2>

    <input id="time" placeholder="Time">
    <input id="adv" placeholder="Adversário">

    <select id="tipo">
      <option value="mandante">Mandante</option>
      <option value="visitante">Visitante</option>
    </select>

    <button class="btn1" onclick="salvar()">Salvar</button>
    <button onclick="fecharPainel()">Fechar</button>
  </div>
</div>

<script>

// ABRIR TELAS
function abrirAdmin(){
  esconderTudo();
  modalAdmin.style.display="flex";
}

function abrirJogador(){
  esconderTudo();
  modalJogador.style.display="flex";
}

function voltar(){
  esconderTudo();
  modalEscolha.style.display="flex";
}

function esconderTudo(){
  modalEscolha.style.display="none";
  modalAdmin.style.display="none";
  modalJogador.style.display="none";
}

// LOGIN
function loginAdmin(){
  if(senhaAdmin.value === "hexag2024"){
    modalAdmin.style.display="none";
    painel.style.display="flex";
  } else {
    alert("Senha errada");
  }
}

function loginJogador(){
  if(senhaJogador.value === "lisboa02"){
    alert("Entrou como jogador");
    modalJogador.style.display="none";
  } else {
    alert("Senha errada");
  }
}

// SALVAR JOGO
function salvar(){
  let jogos = JSON.parse(localStorage.getItem("jogos")) || [];

  jogos.push({
    time: time.value,
    adv: adv.value,
    tipo: tipo.value
  });

  localStorage.setItem("jogos", JSON.stringify(jogos));
  carregar();
}

// MOSTRAR
function carregar(){
  let jogos = JSON.parse(localStorage.getItem("jogos")) || [];
  lista.innerHTML = "";

  jogos.forEach(j=>{
    lista.innerHTML += `
      <div class="card">
        ${j.time} vs ${j.adv}<br>
        ${j.tipo === "mandante" ? "🏠 Mandante" : "✈️ Visitante"}
      </div>
    `;
  });
}

function fecharPainel(){
  painel.style.display="none";
  modalEscolha.style.display="flex";
}

// INICIAR
carregar();

</script>

</body>
</html>
