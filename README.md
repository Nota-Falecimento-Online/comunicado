# Nota de Falecimento 

<html lang="pt-br">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Painel</title>
<script src="https://cdn.tailwindcss.com"></script>
</head>

<body class="bg-gray-100 p-4">

<h1 class="text-xl font-bold mb-4">Nova Nota</h1>

<input id="nome" placeholder="Nome" class="w-full p-3 border mb-2 rounded">
<input id="frase" placeholder="Frase" class="w-full p-3 border mb-2 rounded">

<button onclick="salvar()" class="w-full bg-black text-white p-3 rounded">
    Salvar Nota
</button>

<h2 class="mt-6 font-bold">Minhas Notas</h2>
<div id="lista"></div>

<script type="module">
import { db, auth } from './firebase.js';
import { addDoc, collection, getDocs } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

window.salvar = async () => {
    await addDoc(collection(db, "notas"), {
        nome: document.getElementById('nome').value,
        frase: document.getElementById('frase').value,
        user: auth.currentUser.uid
    });

    alert("Salvo!");
    carregar();
};

async function carregar() {
    const querySnapshot = await getDocs(collection(db, "notas"));
    let html = "";

    querySnapshot.forEach(doc => {
        const d = doc.data();
        html += `<div class="bg-white p-3 rounded shadow mt-2">
            <b>${d.nome}</b><br>${d.frase}
        </div>`;
    });

    document.getElementById('lista').innerHTML = html;
}

carregar();
</script>

</body>
</html>
