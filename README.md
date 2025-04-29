<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formatador de MAC Address</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(to right, #4facfe, #00f2fe);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 8px 16px rgba(0,0,0,0.2);
            width: 90%;
            max-width: 500px;
            animation: slideIn 0.8s ease-out;
        }
        @keyframes slideIn {
            from { opacity: 0; transform: translateY(-30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        h2 {
            text-align: center;
            margin-bottom: 20px;
            color: #333;
        }
        label {
            display: block;
            margin-top: 15px;
            font-weight: bold;
            color: #555;
        }
        input, select, button {
            width: 100%;
            padding: 10px;
            margin-top: 5px;
            border-radius: 8px;
            border: 1px solid #ccc;
            transition: all 0.3s ease;
        }
        input:focus, select:focus {
            border-color: #4facfe;
            box-shadow: 0 0 5px #4facfe;
        }
        button {
            background: #4facfe;
            color: white;
            border: none;
            cursor: pointer;
            margin-top: 20px;
            font-size: 16px;
        }
        button:hover {
            background: #00c6ff;
        }
        .output {
            margin-top: 20px;
            padding: 15px;
            background: #f9f9f9;
            border-radius: 10px;
            font-family: monospace;
            font-size: 15px;
            word-wrap: break-word;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>Formatador de MAC Address</h2>

    <label>Digite o IP (MAC Address):</label>
    <input type="text" id="macInput" placeholder="Ex: 2c 9c 58 e5 93 0b">

    <label>Tipo de Conexão:</label>
    <select id="connectionType">
        <option value="Wi-Fi">Wi-Fi</option>
        <option value="Ethernet">Ethernet</option>
    </select>

    <label>Número do Notebook:</label>
    <select id="notebookNumber">
        <!-- Preenche automaticamente via JavaScript -->
    </select>

    <button onclick="formatar()">Formatar</button>

    <div class="output" id="resultado" style="display: none;"></div>
</div>

<script>
    // Preencher opções de número do notebook
    const selectNotebook = document.getElementById('notebookNumber');
    for (let i = 610; i <= 1000; i++) { // Você pode ajustar até onde quiser
        const option = document.createElement('option');
        option.value = i;
        option.textContent = i;
        selectNotebook.appendChild(option);
    }

    function formatar() {
        let entrada = document.getElementById('macInput').value.trim();
        let tipo = document.getElementById('connectionType').value;
        let numero = document.getElementById('notebookNumber').value;

        if (!entrada) {
            alert('Por favor, digite o IP (MAC Address).');
            return;
        }

        // Limpa entrada, substitui por espaço, divide
        entrada = entrada.replace(/[-:.]/g, ' ').replace(/\s+/g, ' ').toUpperCase();
        let partes = entrada.split(' ');

        if (partes.length !== 6) {
            alert('O MAC Address deve ter 6 blocos.');
            return;
        }

        let macPontos = partes.join(':');
        let macHifens = partes.join('-');
        let fraseFinal = `${tipo} notebook ${numero} : ${macPontos}`;

        // Exibir
        document.getElementById('resultado').style.display = 'block';
        document.getElementById('resultado').innerHTML = `
            <strong>Formato com dois-pontos:</strong><br>${macPontos}<br><br>
            <strong>Formato com hífens:</strong><br>${macHifens}<br><br>
            <strong>Frase Final:</strong><br>${fraseFinal}
        `;
    }
</script>

</body>
</html>
