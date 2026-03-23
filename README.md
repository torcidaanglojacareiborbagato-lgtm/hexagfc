<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<title>Hexag FC</title>

<style>
body {
  font-family: Arial;
  background: #0f172a;
  color: white;
  text-align: center;
}

.container {
  max-width: 500px;
  margin: auto;
}

input, select, button {
  width: 100%;
  margin: 5px 0;
  padding: 10px;
  border-radius: 8px;
  border: none;
}

button {
  background: #22c55e;
  color: white;
  font-weight: bold;
  cursor: pointer;
}

.card {
  background: #1e293b;
  padding: 10px;
  margin-top: 10px;
  border-radius: 10px;
}
</style>

</head>

<body>

<div class="container">

<h1>⚽ Hexag FC</h1>

<!-- LOGIN -->
<div id="login">
  <input type="password" id="senha" placeholder="Digite a senha">
  <button onclick="login()">Entrar</button>
</div>

<!-- PAINEL -->
<div id="painel" style="display:none;">

  <h2>Painel</h2>

  <input id="time" placeholder="Nome do Time">
  <input id="adv" placeholder="Adversário">

  <select id="tipo">
    <option value="mandante">🏠 Mandante</option>
    <option value="visitante">✈️ Visitante</option>
  </select>

  <button onclick="salvar()">Cadastrar Jogo</button>

  <h2>Jogos</h2>
  <div id="jogos"></div>

</div>

</div>

<script>

// LOGIN
function login(){
  let senha = document.getElementById("senha").value;

  if(senha === "hexag2024"){
    localStorage.setItem("user","admin");
  } else if(senha === "lisboa02"){
    localStorage.setItem("user","jogador");
  } else {
    alert("Senha errada");
    return;
  }

  document.getElementById("login").style.display="none";
  document.getElementById("painel").style.display="block";

  carregar();
}

// SALVAR JOGO
function salvar(){
  let jogos = JSON.parse(localStorage.getItem("jogos")) || [];

  let novo = {
    time: document.getElementById("time").value,
    adv: document.getElementById("adv").value,
    tipo: document.getElementById("tipo").value
  };

  jogos.push(novo);
  localStorage.setItem("jogos", JSON.stringify(jogos));

  carregar();
}

// LISTAR JOGOS
function carregar(){
  let jogos = JSON.parse(localStorage.getItem("jogos")) || [];
  let div = document.getElementById("jogos");

  div.innerHTML = "";

  jogos.forEach((j,i)=>{
    div.innerHTML += `
      <div class="card">
        <b>${j.time}</b> vs ${j.adv}<br>
        ${j.tipo === "mandante" ? "🏠 Mandante" : "✈️ Visitante"}
        <br><br>
        <button onclick="excluir(${i})">Excluir</button>
      </div>
    `;
  });
}

// EXCLUIR
function excluir(i){
  let jogos = JSON.parse(localStorage.getItem("jogos"));
  jogos.splice(i,1);
  localStorage.setItem("jogos", JSON.stringify(jogos));
  carregar();
}

// AUTO LOGIN
if(localStorage.getItem("user")){
  document.getElementById("login").style.display="none";
  document.getElementById("painel").style.display="block";
  carregar();
}

</script>

</body>
</html>
