# Projetos
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Desvende a Senha</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body { 
            font-family: Arial, sans-serif; 
            background: #f7f7f7; 
            display: flex; 
            flex-direction: column; 
            align-items: center; 
            justify-content: center; 
            height: 100vh; 
            margin: 0;
        }
        .container {
            background: #fff;
            padding: 32px 24px;
            border-radius: 12px;
            box-shadow: 0 2px 12px rgba(0,0,0,0.08);
            text-align: center;
            max-width: 350px;
        }
        input[type="text"] {
            padding: 8px;
            width: 90%;
            margin-bottom: 12px;
            border: 1px solid #ccc;
            border-radius: 6px;
            font-size: 1em;
        }
        button {
            padding: 8px 18px;
            background: #0078d7;
            color: #fff;
            border: none;
            border-radius: 6px;
            font-size: 1em;
            cursor: pointer;
        }
        .hint {
            margin-top: 18px;
            color: #d2691e;
            font-weight: bold;
        }
        .error {
            color: #c00;
            margin-top: 10px;
        }
        .success {
            color: #228B22;
            font-weight: bold;
            margin-top: 18px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Desvende a Senha</h2>
        <p>Digite a data por extenso para acessar o site.</p>
        <form id="senhaForm" autocomplete="off">
            <input type="text" id="senhaInput" placeholder="Ex: vinte de maio de dois mil e vinte" required>
            <br>
            <button type="submit">Enviar</button>
        </form>
        <div class="error" id="mensagemErro"></div>
        <div class="hint" id="dica" style="display:none;">Dica: Nosso namoro.</div>
        <div class="success" id="mensagemSucesso" style="display:none;">Senha correta! Bem-vindo(a)!</div>
    </div>
    <script>
        // Defina a senha correta aqui (exemplo: "vinte de maio de dois mil e vinte")
        const senhaCorreta = "vinte de maio de dois mil e vinte";
        let tentativas = 0;
        let dicaMostrada = false;
        const maxTentativasAntesDica = 2;
        const maxTentativasDepoisDica = 5;

        const form = document.getElementById('senhaForm');
        const input = document.getElementById('senhaInput');
        const erro = document.getElementById('mensagemErro');
        const dica = document.getElementById('dica');
        const sucesso = document.getElementById('mensagemSucesso');

        form.addEventListener('submit', function(e) {
            e.preventDefault();
            erro.textContent = "";
            sucesso.style.display = "none";
            const valor = input.value.trim().toLowerCase();

            if (valor === senhaCorreta) {
                sucesso.style.display = "block";
                form.style.display = "none";
                erro.textContent = "";
                dica.style.display = "none";
                return;
            }

            tentativas++;

            if (!dicaMostrada && tentativas >= maxTentativasAntesDica) {
                dica.style.display = "block";
                dicaMostrada = true;
            }

            if (dicaMostrada && tentativas >= (maxTentativasAntesDica + maxTentativasDepoisDica)) {
                erro.textContent = "Você excedeu o número de tentativas.";
                form.querySelector('button').disabled = true;
                input.disabled = true;
                return;
            }

            erro.textContent = "Senha incorreta. Tente novamente.";
            input.value = "";
            input.focus();
        });
    </script>
</body>
</html></form></div>
