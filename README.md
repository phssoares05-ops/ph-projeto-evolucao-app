
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#101010">
<title>PH | Projeto Evolução</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#101010;color:#fff;font-family:Arial,sans-serif;padding:20px}
header{text-align:center;padding:22px 0}
header h1{color:#b5ff35;font-size:27px;margin:0}
header p{color:#aaa}
h2{font-size:19px;margin-top:25px}
.card{background:#1d1d1d;border:1px solid #333;border-radius:15px;padding:17px;margin:13px 0}
input,select,button{width:100%;padding:13px;margin:7px 0;border-radius:9px;border:1px solid #444;background:#292929;color:white;font-size:16px}
button{background:#b5ff35;color:#111;font-weight:bold;border:0;cursor:pointer}
.small{color:#aaa;font-size:13px}
.metric{font-size:28px;font-weight:bold;color:#b5ff35}
.entry{padding:10px 0;border-bottom:1px solid #444}
.entry:last-child{border:0}
.delete{background:#6b2525;color:white}
</style>
</head>
<body>

<header>
<h1>PH | PROJETO EVOLUÇÃO</h1>
<p>Disciplina hoje. Resultado amanhã.</p>
</header>

<div class="card">
<h2>Minha evolução</h2>
<p>Peso atual</p>
<div class="metric" id="pesoAtual">-- kg</div>
<p class="small">Meta: 95 kg</p>
<div id="progresso" class="small">Registre seu peso para acompanhar.</div>
</div>

<div class="card">
<h2>⚖️ Registrar peso</h2>
<input id="peso" type="number" step="0.1" placeholder="Peso em kg">
<button onclick="salvarPeso()">Salvar pesagem</button>
</div>

<div class="card">
<h2>🏋️ Treino de musculação</h2>
<input id="treino" placeholder="Ex.: Peito e tríceps">
<input id="duracao" type="number" placeholder="Duração em minutos">
<input id="exercicios" placeholder="Exercícios realizados">
<button onclick="salvarTreino()">Registrar treino</button>
</div>

<div class="card">
<h2>🏃 Corrida e caminhada</h2>
<input id="distancia" type="number" step="0.1" placeholder="Distância em km">
<input id="tempo" type="number" placeholder="Tempo em minutos">
<select id="tipoCorrida">
<option>Corrida</option>
<option>Caminhada</option>
<option>Corrida e caminhada</option>
</select>
<button onclick="salvarCorrida()">Registrar atividade</button>
</div>

<div class="card">
<h2>🥗 Alimentação</h2>
<input id="alimento" placeholder="O que você comeu?">
<input id="calorias" type="number" placeholder="Calorias aproximadas">
<button onclick="salvarAlimento()">Registrar alimentação</button>
<p>Calorias registradas hoje: <strong id="totalCalorias">0 kcal</strong></p>
</div>

<div class="card">
<h2>💧 Hidratação</h2>
<div class="metric" id="aguaAtual">0 ml</div>
<p class="small">Meta diária: 3.000 ml</p>
<button onclick="adicionarAgua(250)">+ 250 ml</button>
<button onclick="adicionarAgua(500)">+ 500 ml</button>
</div>

<div class="card">
<h2>📊 Histórico de atividades</h2>
<div id="historico">Suas atividades aparecerão aqui.</div>
<button class="delete" onclick="limparHistorico()">Apagar histórico</button>
</div>

<p class="small" style="text-align:center;margin:30px 0">
PH | PROJETO EVOLUÇÃO • Sua transformação continua.
</p>

<script>
const chave = "ph_projeto_evolucao_v1";
let dados = JSON.parse(localStorage.getItem(chave) || '{"pesos":[],"atividades":[],"agua":{}}');

function salvarDados(){
 localStorage.setItem(chave,JSON.stringify(dados));
 atualizar();
}

function hoje(){
 return new Date().toLocaleDateString("pt-BR");
}

function salvarPeso(){
 const valor = Number(document.getElementById("peso").value);
 if(!valor || valor<30 || valor>300){alert("Digite um peso válido.");return;}
 dados.pesos.push({valor,data:hoje()});
 document.getElementById("peso").value="";
 salvarDados();
}

function salvarTreino(){
 const nome=document.getElementById("treino").value.trim();
 const duracao=document.getElementById("duracao").value;
 const exercicios=document.getElementById("exercicios").value.trim();
 if(!nome){alert("Informe o treino.");return;}
 dados.atividades.unshift({tipo:"Treino",descricao:nome+" | "+exercicios+" | "+duracao+" min",data:hoje()});
 document.getElementById("treino").value="";
 document.getElementById("duracao").value="";
 document.getElementById("exercicios").value="";
 salvarDados();
}

function salvarCorrida(){
 const distancia=Number(document.getElementById("distancia").value);
 const tempo=Number(document.getElementById("tempo").value);
 const tipo=document.getElementById("tipoCorrida").value;
 if(!distancia || !tempo){alert("Informe distância e tempo.");return;}
 dados.atividades.unshift({tipo:tipo,descricao:distancia+" km em "+tempo+" minutos",data:hoje()});
 document.getElementById("distancia").value="";
 document.getElementById("tempo").value="";
 salvarDados();
}

function salvarAlimento(){
 const nome=document.getElementById("alimento").value.trim();
 const calorias=Number(document.getElementById("calorias").value);
 if(!nome || !calorias){alert("Informe alimento e calorias.");return;}
 dados.atividades.unshift({tipo:"Alimentação",descricao:nome+" | "+calorias+" kcal",calorias:calorias,data:hoje()});
 document.getElementById("alimento").value="";
 document.getElementById("calorias").value="";
 salvarDados();
}

function adicionarAgua(quantidade){
 const data=hoje();
 dados.agua[data]=(dados.agua[data]||0)+quantidade;
 salvarDados();
}

function atualizar(){
 const ultimo=dados.pesos[dados.pesos.length-1];
 document.getElementById("pesoAtual").textContent=ultimo?ultimo.valor.toFixed(1)+" kg":"-- kg";
 if(ultimo){
  const diferenca=(ultimo.valor-95).toFixed(1);
  document.getElementById("progresso").textContent=diferenca>0?"Faltam "+diferenca+" kg para sua meta!":"Meta de 95 kg alcançada!";
 }
 document.getElementById("aguaAtual").textContent=(dados.agua[hoje()]||0)+" ml";
 const calorias=dados.atividades.filter(a=>a.data===hoje()).reduce((s,a)=>s+(a.calorias||0),0);
 document.getElementById("totalCalorias").textContent=calorias+" kcal";
 const historico=document.getElementById("historico");
 const itens=[
 ...dados.pesos.map(p=>({tipo:"Pesagem",descricao:p.valor+" kg",data:p.data})),
 ...dados.atividades
 ];
 historico.innerHTML=itens.length?itens.map(i=>`<div class="entry"><strong>${i.tipo}</strong><br>${i.descricao}<br><span class="small">${i.data}</span></div>`).join(""):"Suas atividades aparecerão aqui.";
}

function limparHistorico(){
 if(confirm("Tem certeza que deseja apagar todos os registros deste aparelho?")){
  dados={pesos:[],atividades:[],agua:{}};
  salvarDados();
 }
}
atualizar();
</script>
</body>
</html>
