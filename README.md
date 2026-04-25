<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ConcentraTempo</title>
    <style>
        :root { --bg: #050a0f; --green: #2ecc71; --blue: #1e3a5f; --red: #e74c3c; }
        body { background: var(--bg); color: white; font-family: 'Poppins', sans-serif; margin: 0; }
        .container { max-width: 500px; margin: 40px auto; background: rgba(10, 25, 47, 0.9); padding: 30px; border-radius: 20px; border: 1px solid var(--green); }
        .logo { font-size: 2.5rem; text-align: center; margin-bottom: 30px; }
        button { padding: 10px 15px; background: var(--green); border: none; cursor: pointer; border-radius: 5px; font-weight: bold; }
        input { width: 90%; padding: 12px; margin: 8px 0; border-radius: 5px; border: 1px solid var(--blue); background: #0b1d36; color: white; }
        h2 { color: var(--green); }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="logo">⏱️ ConcentraTempo</h1>
        <p>Bem-vindo! Digite seu nome para começar:</p>
        <input type="text" id="name" placeholder="Seu nome">
        <button onclick="alert('Bem-vindo, ' + document.getElementById('name').value + '! 🎉')">Entrar</button>
    </div>
</body>
</html>