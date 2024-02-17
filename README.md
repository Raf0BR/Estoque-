<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Gerenciador de Estoque</title>
<style>
  body {
    font-family: Arial, sans-serif;
    text-align: center;
  }
  button {
    padding: 10px 20px;
    margin: 10px;
    font-size: 16px;
  }
  #output {
    margin-top: 20px;
    text-align: left;
  }
</style>
</head>
<body>

<h1>Gerenciador de Estoque</h1>

<button onclick="showCadastro()">Cadastrar</button>
<button onclick="showConsulta()">Consultar</button>
<button onclick="showEstoque()">Estoque</button>

<div id="cadastro" style="display: none;">
  <h2>Cadastro de Produto</h2>
  <input type="text" id="nomeProduto" placeholder="Nome do Produto"><br>
  <input type="number" id="quantidadeProduto" placeholder="Quantidade"><br>
  <input type="number" id="valorProduto" placeholder="Valor"><br>
  <button onclick="cadastrarProduto()">Cadastrar Produto</button>
</div>

<div id="consulta" style="display: none;">
  <h2>Consulta de Produto</h2>
  <input type="text" id="consultaProduto" placeholder="Nome do Produto"><br>
  <button onclick="consultarProduto()">Consultar</button>
  <div id="output"></div>
</div>

<div id="estoque" style="display: none;">
  <h2>Estoque</h2>
  <button onclick="listarEstoque()">Listar Estoque</button>
  <ul id="listaEstoque"></ul>
</div>

<script>
  let estoque = [];

  function showCadastro() {
    document.getElementById("cadastro").style.display = "block";
    document.getElementById("consulta").style.display = "none";
    document.getElementById("estoque").style.display = "none";
  }

  function showConsulta() {
    document.getElementById("cadastro").style.display = "none";
    document.getElementById("consulta").style.display = "block";
    document.getElementById("estoque").style.display = "none";
  }

  function showEstoque() {
    document.getElementById("cadastro").style.display = "none";
    document.getElementById("consulta").style.display = "none";
    document.getElementById("estoque").style.display = "block";
  }

  function cadastrarProduto() {
    const nome = document.getElementById("nomeProduto").value;
    const quantidade = parseInt(document.getElementById("quantidadeProduto").value);
    const valor = parseFloat(document.getElementById("valorProduto").value);
    
    estoque.push({ nome, quantidade, valor });
    alert("Produto cadastrado com sucesso!");
  }

  function consultarProduto() {
    const nomeConsulta = document.getElementById("consultaProduto").value;
    const produto = estoque.find(item => item.nome === nomeConsulta);
    
    if (produto) {
      document.getElementById("output").innerHTML = `
        <p>Nome: ${produto.nome}</p>
        <p>Quantidade: ${produto.quantidade}</p>
        <p>Valor: ${produto.valor}</p>
      `;
    } else {
      document.getElementById("output").innerHTML = "Produto não encontrado.";
    }
  }

  function listarEstoque() {
    const listaEstoque = document.getElementById("listaEstoque");
    listaEstoque.innerHTML = "";

    const estoqueOrdenado = estoque.slice().sort((a, b) => b.quantidade - a.quantidade);

    estoqueOrdenado.forEach(item => {
      const li = document.createElement("li");
      li.textContent = `${item.nome} - Quantidade: ${item.quantidade} - Valor: ${item.valor}`;
      listaEstoque.appendChild(li);
    });
  }
</script>

</body>
</html>
