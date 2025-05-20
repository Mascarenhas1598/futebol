# futebol
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Previsão de Gols - Brasileirão Feminino A1</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 text-gray-800 font-sans">

  <div class="max-w-xl mx-auto mt-10 bg-white p-8 rounded-xl shadow-md text-center">
    <h1 class="text-2xl font-bold mb-6">Previsão de Gols - Simulação Interna</h1>

    <button onclick="calcularProbabilidade()" class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-6 rounded">
      Rodar Simulação
    </button>

    <div id="resultado" class="mt-6 hidden text-left">
      <h2 class="text-xl font-semibold mb-2">Resultado da Previsão:</h2>
      <p><strong>Média Estimada de Gols:</strong> <span id="mediaGols"></span></p>
      <p><strong>Probabilidade de mais de 2.5 gols:</strong> <span id="probabilidade"></span>%</p>
      <p><strong>Classificação:</strong> <span id="classificacao"></span></p>
    </div>
  </div>

  <script>
    // Base estatística interna para simulação
    const estatisticasTimes = {
      "corinthians": { ataque: 3.0, defesa: 1.0 },
      "ferroviária": { ataque: 1.0, defesa: 3.0 }
    };

    function calcularProbabilidade() {
      const equipeA = estatisticasTimes["corinthians"];
      const equipeB = estatisticasTimes["ferroviária"];

      const golsA = (equipeA.ataque + equipeB.defesa) / 2;
      const golsB = (equipeB.ataque + equipeA.defesa) / 2;
      const somaGols = golsA + golsB;
      const difGols = golsA - golsB;

      const z = (0.65 * golsA) + (0.16 * golsB) + (0.48 * difGols) + (0.81 * somaGols) - 1.97;
      const prob = 1 / (1 + Math.exp(-z));
      const classificacao = prob > 0.5 ? "Alta" : "Baixa";

      document.getElementById("mediaGols").textContent = somaGols.toFixed(2);
      document.getElementById("probabilidade").textContent = (prob * 100).toFixed(2);
      document.getElementById("classificacao").textContent = classificacao;
      document.getElementById("resultado").classList.remove("hidden");
    }
  </script>
</body>
</html>
