# Atividade2Parte2

**1-questão:**

const usuario = {
  nome: "Ana Silva";
  idade: 30;
  habilidades: ["JavaScript", "React", "Node.js"];
  ativo: true
};

* Converter para JSON:
 ```const jsonString = JSON.stringify(usuario);```

* Recuperar objeto:
```const usuarioRecuperado = JSON.parse(jsonString);```
****

**2-questão:**

const jsonString = `{
  "usuarios": [
    {"nome": "Carlos", "email": "carlos@email.com"},
    {"nome": "Maria", "email": "maria@email.com"},
    {"nome": "João", "email": "joao@email.com"}
  ]
}`;

* Converter a string JSON para um objeto:
```const dados = JSON.parse(jsonString);```

* Extrair e concatenar emails manualmente:
  `{ let emailsConcatenados = "";
for (const usuario of dados.usuarios) {
  if (emailsConcatenados !== "") {
    emailsConcatenados += ", ";
  emailsConcatenados += usuario.email;
  }`
  

**3-questão:**

const produtosJSON = ```{
  "produtos": [
    {"nome": "Mouse", "preco": 25.90},
    {"nome": "Teclado", "preco": 89.90},
    {"nome": "Monitor", "preco": 450.00},
    {"nome": "Cabo USB", "preco": 15.00}
  ]
}```;

`{function produtosAcimaDe50(jsonString) {
  const dados = JSON.parse(jsonString);
  const produtosCaros = [];

  dados.produtos.forEach((produto) => {
    if (produto.preco > 50) {
      produtosCaros.push(produto.nome);
    }
  });

  return produtosCaros;
}

* Exemplo de uso:
const resultado = produtosAcimaDe50(produtosJSON);
****

**4-questão:**

const endereco = {
  rua: "Av. Paulista",
  numero: 1000,
  cidade: "São Paulo",
  cep: "01310-100"
};

function formatarEndereco(end) {
 * Monta partes separadas e depois junta em uma única string:
  const parte1 = `${end.rua}, ${end.numero}`;
  const parte2 = end.cidade + " - CEP: " + end.cep;

  return parte1 + " - " + parte2;
}

const resultado = formatarEndereco(endereco);
****

**5-questão:**

const pedidosJSON = `{
  "pedidos": [
    {"id": 1, "cliente": "Fernanda", "total": 120.50, "status": "entregue"},
    {"id": 2, "cliente": "Roberto", "total": 89.90, "status": "processando"},
    {"id": 3, "cliente": "Carla", "total": 45.30, "status": "entregue"}
  ]
}`;

function resumoPedidos(jsonString) {
  const dados = JSON.parse(jsonString);
  let entregues = 0;
  let processando = 0;
  let totalGeral = 0;

  for (const pedido of dados.pedidos) {
    totalGeral += pedido.total;

    if (pedido.status === "entregue") {
      entregues++;
    } else if (pedido.status === "processando") {
      processando++;
    }
  }

  * Formatação do valor total em reais (duas casas decimais, vírgula):
  const totalFormatado = totalGeral.toFixed(2).replace(".", ",");

 * Montagem do texto manualmente:
  return `${entregues} pedidos entregues, ${processando} em processamento. Valor total: R$ ${totalFormatado}`;
}

const resultado = resumoPedidos(pedidosJSON);
****

**6-questão:**
```
function parseJSONSafe(jsonString) {
  try {
    return {
      sucesso: true,
      resultado: JSON.parse(jsonString)
    };
  } catch (erro) {
    return {
      sucesso: false,
      mensagem: "Falha ao converter JSON: verifique a sintaxe.",
      detalhe: erro.message
    };
  }
}

 // Teste com JSON inválido:
const jsonInvalido = '{nome: "João", "idade": 30}'; // Falta aspas em "nome"

const resultado = parseJSONSafe(jsonInvalido);
