# Nota de Falecimento - Modelo Padrão
<div id="nota-para-exportar" class="shadow-2xl border-t-[12px] border-black bg-white p-8 w-[500px] text-center">

    <!-- FOTO -->
    <img id="out-foto" class="w-[150px] h-[200px] object-cover mx-auto mb-4 border shadow">

    <!-- NOME -->
    <h1 id="out-nome" class="text-2xl font-serif font-bold uppercase"></h1>

    <!-- DATAS -->
    <p id="out-datas" class="text-gray-500 text-sm my-2"></p>

    <!-- FRASE -->
    <p id="out-frase" class="italic text-lg my-6 text-gray-700"></p>

    <!-- BLOCO VELÓRIO -->
    <div class="bg-gray-100 p-4 rounded mb-4">
        <p class="text-xs uppercase text-gray-400">Velório</p>
        <p id="out-velorio-local" class="font-bold text-lg"></p>
        <p id="out-velorio-data" class="text-sm"></p>
        <p id="out-velorio-endereco" class="text-sm text-gray-600"></p>
    </div>

    <!-- BLOCO SEPULTAMENTO -->
    <div class="bg-gray-100 p-4 rounded mb-4">
        <p class="text-xs uppercase text-gray-400">Sepultamento</p>
        <p id="out-sepultamento-local" class="font-bold text-lg"></p>
        <p id="out-sepultamento-data" class="text-sm"></p>
        <p id="out-sepultamento-endereco" class="text-sm text-gray-600"></p>
    </div>

    <!-- COROA -->
    <div class="mt-6 border-t pt-4">
        <p class="text-sm font-bold">Coroa de Flores</p>
        <p class="text-xs text-gray-500 mb-2">
            Envie suas condolências com uma coroa de flores
        </p>
        <p id="out-whats" class="text-green-600 font-bold cursor-pointer"></p>
    </div>

</div>

<h3 class="font-bold mt-4">Velório</h3>
<input id="in-velorio-local" placeholder="Local do velório" class="w-full border p-2 mb-2">
<input id="in-velorio-data" placeholder="Data e horário" class="w-full border p-2 mb-2">
<input id="in-velorio-endereco" placeholder="Endereço" class="w-full border p-2">

<h3 class="font-bold mt-4">Sepultamento</h3>
<input id="in-sep-local" placeholder="Local do sepultamento" class="w-full border p-2 mb-2">
<input id="in-sep-data" placeholder="Data e horário" class="w-full border p-2 mb-2">
<input id="in-sep-endereco" placeholder="Endereço" class="w-full border p-2">
