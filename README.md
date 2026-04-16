# Login

<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Login Admin</title>
<script src="https://cdn.tailwindcss.com"></script>
</head>

<body class="flex items-center justify-center h-screen bg-gray-100">

<div class="bg-white p-6 rounded shadow w-full max-w-sm">
    <h2 class="text-xl font-bold mb-4 text-center">Admin</h2>

    <input id="senha" type="password" placeholder="Senha"
    class="w-full p-3 border rounded mb-4">

    <button onclick="login()"
    class="w-full bg-black text-white p-3 rounded">
        Entrar
    </button>
</div>

<script>
function login(){
    const senha = document.getElementById('senha').value;

    if(senha === "1234"){
        localStorage.setItem("admin", "true");
        window.location.href = "dashboard.html";
    } else {
        alert("Senha inválida");
    }
}
</script>

</body>
</html>
