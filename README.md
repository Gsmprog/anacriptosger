<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Pontos de Entrada e Capital - Fibonacci</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            padding: 20px;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            background-color: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .section {
            margin-bottom: 20px;
        }
        .section h2 {
            color: #333;
            font-size: 1.2em;
            margin-bottom: 10px;
        }
        label {
            font-size: 1em;
            color: #444;
            margin-top: 10px;
        }
        input {
            width: 100%;
            padding: 10px;
            margin: 5px 0 15px 0;
            border-radius: 5px;
            border: 1px solid #ccc;
            font-size: 1em;
        }
        button {
            padding: 10px 20px;
            background-color: #4caf50;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
        }
        button:hover {
            background-color: #45a049;
        }
        .result {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Calculadora de Pontos de Entrada e Capital - Fibonacci</h1>
        
        <!-- Seção de Entrada de Valores -->
        <div class="section">
            <h2>Dados de Capital e Valores</h2>
            <label for="capital">Capital disponível (R$):</label>
            <input type="number" id="capital" placeholder="Ex: 1000" required>

            <label for="topo">Valor do topo (R$):</label>
            <input type="number" id="topo" placeholder="Ex: 100" required>

            <label for="fundo">Valor do fundo (R$):</label>
            <input type="number" id="fundo" placeholder="Ex: 50" required>
        </div>

        <!-- Seção de Percentuais -->
        <div class="section">
            <h2>Percentuais para Alocação de Capital</h2>
            <label for="percentual382">Percentual para Correção 0.382 (%):</label>
            <input type="number" id="percentual382" value="30" required>

            <label for="percentual50">Percentual para Correção 0.5 (%):</label>
            <input type="number" id="percentual50" value="60" required>

            <label for="percentual618">Percentual para Correção 0.618 (%):</label>
            <input type="number" id="percentual618" value="10" required>
        </div>

        <button onclick="calcularEntradas()">Calcular Pontos de Entrada</button>

        <!-- Seção de Resultados -->
        <div class="result" id="resultado"></div>
    </div>

    <script>
        function calcularEntradas() {
            const capital = parseFloat(document.getElementById("capital").value);
            const topo = parseFloat(document.getElementById("topo").value);
            const fundo = parseFloat(document.getElementById("fundo").value);

            // Capturar os percentuais
            const percentual382 = parseFloat(document.getElementById("percentual382").value) / 100;
            const percentual50 = parseFloat(document.getElementById("percentual50").value) / 100;
            const percentual618 = parseFloat(document.getElementById("percentual618").value) / 100;

            if (isNaN(capital) || isNaN(topo) || isNaN(fundo) || topo <= fundo) {
                alert("Por favor, insira valores válidos (o topo deve ser maior que o fundo).");
                return;
            }

            // Diferença entre topo e fundo
            const diferenca = topo - fundo;

            // Correções de Fibonacci
            const fib382 = 0.382;
            const fib50 = 0.5;
            const fib618 = 0.618;

            // Pontos de entrada baseados nas correções de Fibonacci
            const entrada382 = topo - (diferenca * fib382);
            const entrada50 = topo - (diferenca * fib50);
            const entrada618 = topo - (diferenca * fib618);

            // Fracionamento do capital baseado nos percentuais inseridos
            const valor382 = capital * percentual382;
            const valor50 = capital * percentual50;
            const valor618 = capital * percentual618;

            // Cálculo dos lucros para cada entrada
            const lucro382 = ((topo / entrada382) - 1) * valor382;
            const lucro50 = ((topo / entrada50) - 1) * valor50;
            const lucro618 = ((topo / entrada618) - 1) * valor618;

            // Cálculo do lucro total
            const lucroTotal = lucro382 + lucro50 + lucro618;

            // Exibir resultado
            document.getElementById("resultado").innerHTML = `
                <h2>Pontos de Entrada e Lucros Calculados:</h2>
                <p><strong>Correção 0.382:</strong> R$ ${entrada382.toFixed(4)} <br> 
                Valor alocado: R$ ${valor382.toFixed(4)} <br> 
                Lucro estimado: R$ ${lucro382.toFixed(4)}</p>
                
                <p><strong>Correção 0.5:</strong> R$ ${entrada50.toFixed(4)} <br> 
                Valor alocado: R$ ${valor50.toFixed(4)} <br> 
                Lucro estimado: R$ ${lucro50.toFixed(4)}</p>
                
                <p><strong>Correção 0.618:</strong> R$ ${entrada618.toFixed(4)} <br> 
                Valor alocado: R$ ${valor618.toFixed(4)} <br> 
                Lucro estimado: R$ ${lucro618.toFixed(4)}</p>

                <h3>Lucro Total Estimado ao atingir o topo: R$ ${lucroTotal.toFixed(4)}</h3>
            `;
        }
    </script>
</body>
</html>
