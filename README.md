# Nota de Falecimento - Modelo Padrão
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Comunicado de Falecimento - Gerador</title>
    
    <!-- Bibliotecas Necessárias -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
    
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Libre+Baskerville:ital,wght@0,400;0,700;1,400&family=Montserrat:wght@300;400;700&display=swap');
        
        body { font-family: 'Montserrat', sans-serif; background-color: #f8f9fa; }
        .font-serif { font-family: 'Libre Baskerville', serif; }
        
        /* Estilo do Card de Falecimento */
        #nota-para-exportar {
            width: 500px;
            background: white;
            padding: 40px;
            border: 1px solid #eee;
            color: #1a1a1a;
            text-align: center;
        }
        .foto-perfil {
            width: 160px;
            height: 200px;
            object-fit: cover;
            border: 1px solid #ddd;
            margin: 0 auto 20px auto;
            display: block;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }
        .divisor { width: 50px; height: 2px; background: #444; margin: 15px auto; }
        
        /* Botão WhatsApp Flutuante */
        .wpp-float {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background: #25d366;
            color: white;
            padding: 15px 25px;
            border-radius: 50px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            display: flex;
            align-items: center;
            gap: 10px;
            z-index: 999;
            text-decoration: none;
        }
    </style>
</head>
<body class="bg-gray-100 p-4">

    <div class="max-w-5xl mx-auto grid grid-cols-1 lg:grid-cols-2 gap-8">
        
        <!-- COLUNA ESQUERDA: FORMULÁRIO -->
        <div class="bg-white p-6 rounded-xl shadow-lg">
            <h2 class="text-2xl font-bold text-gray-800 mb-6 border-b pb-2">Criar Novo Comunicado</h2>
            
            <div class="space-y-4">
                <div>
                    <label class="block text-sm font-bold text-gray-700">Nome do Falecido</label>
                    <input type="text" id="in-nome" class="w-full border p-3 rounded mt-1" placeholder="Nome Completo">
                </div>

                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-bold text-gray-700">Nascimento</label>
                        <input type="date" id="in-nasc" class="w-full border p-3 rounded mt-1">
                    </div>
                    <div>
                        <label class="block text-sm font-bold text-gray-700">Falecimento</label>
                        <input type="date" id="in-falec" class="w-full border p-3 rounded mt-1">
                    </div>
                </div>

                <div>
                    <label class="block text-sm font-bold text-gray-700">Foto do Falecido</label>
                    <input type="file" id="in-foto" accept="image/*" class="w-full border p-2 rounded mt-1">
                </div>

                <div>
                    <label class="block text-sm font-bold text-gray-700">Cemitério (SP e Grande SP)</label>
                    <select id="in-cemiterio" class="w-full border p-3 rounded mt-1">
                        <option value="">Selecione um cemitério...</option>
                        <option value="Cemitério da Consolação|R. da Consolação, 1660 - São Paulo, SP">Cemitério da Consolação</option>
                        <option value="Cemitério do Morumby|Rua Dep. Laércio Corte, 468 - São Paulo, SP">Cemitério do Morumby</option>
                        <option value="Cemitério Vila Formosa|Av. Flor de Vila Formosa - São Paulo, SP">Cemitério Vila Formosa</option>
                        <option value="Cemitério da Quarta Parada|Av. Salim Farah Maluf - São Paulo, SP">Cemitério da Quarta Parada</option>
                        <option value="Cemitério Gethsêmani Morumbi|Praça da Ressurreição, 1 - São Paulo, SP">Cemitério Gethsêmani</option>
                        <option value="Cemitério Parque dos Girassóis|Av. Sadamu Inoue, 6061 - São Paulo, SP">Cemitério Parque dos Girassóis</option>
                        <option value="Cemitério de Congonhas|R. Min. Álvaro de Sousa Lima, 101 - SP">Cemitério de Congonhas</option>
                        <option value="Cemitério AlphaCampus|Estrada de Santa Inês, 3000 - Itapevi/Barueri">Cemitério AlphaCampus</option>
                    </select>
                </div>

                <div>
                    <label class="block text-sm font-bold text-gray-700">Horário e Funcionamento</label>
                    <input type="text" id="in-horario" class="w-full border p-3 rounded mt-1" placeholder="Ex: Velório das 08:00 às 14:00h">
                </div>

                <div>
                    <label class="block text-sm font-bold text-gray-700">Frase Personalizada</label>
                    <textarea id="in-frase" class="w-full border p-3 rounded mt-1" rows="2">"Combati o bom combate, acabei a carreira, guardei a fé."</textarea>
                </div>

                <button onclick="gerarPreview()" class="w-full bg-slate-800 text-white font-bold py-4 rounded-lg hover:bg-black transition uppercase">
                    Visualizar Nota de Falecimento
                </button>
            </div>
        </div>

        <!-- COLUNA DIREITA: PREVIEW E PDF -->
        <div id="coluna-preview" class="hidden flex flex-col items-center">
            <h2 class="text-xl font-bold mb-4 text-gray-700 uppercase">Pré-visualização</h2>
            
            <!-- ÁREA QUE VIRA PDF -->
            <div id="nota-para-exportar" class="shadow-2xl border-t-[15px] border-slate-900">
                <img id="out-foto" src="https://via.placeholder.com/160x200?text=Foto" class="foto-perfil">
                
                <h1 id="out-nome" class="font-serif text-3xl font-bold mb-2 uppercase">Nome do Falecido</h1>
                <p id="out-datas" class="text-gray-500 font-light tracking-tighter italic text-sm"></p>
                
                <div class="divisor"></div>
                
                <p id="out-frase" class="font-serif italic text-lg text-gray-700 my-6 px-4"></p>
                
                <div class="bg-gray-50 p-6 rounded-lg border border-gray-100 text-center">
                    <p class="text-[10px] uppercase tracking-widest text-gray-400 mb-1">Local do Sepultamento</p>
                    <p id="out-cemiterio" class="font-bold text-slate-800 text-xl"></p>
                    <p id="out-endereco" class="text-blue-600 text-sm underline cursor-pointer mb-3"></p>
                    <p id="out-horario" class="font-bold text-gray-700"></p>
                </div>

                <p class="mt-8 text-[9px] text-gray-300 uppercase">Comunicado Oficial</p>
            </div>

            <div class="mt-6 w-full max-w-[500px] flex gap-4">
                <button onclick="baixarPDF()" class="flex-1 bg-red-700 text-white font-bold py-4 rounded shadow-lg hover:bg-red-800 transition">
                    GERAR PDF AGORA
                </button>
            </div>
        </div>

    </div>

    <!-- BOTÃO WHATSAPP DA FLORICULTURA -->
    <a href="https://wa.me/5511986464780?text=Quero%20pedir%20uma%20coroa%20de%20flores" target="_blank" class="wpp-float">
        <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24"><path d="M.057 24l1.687-6.163c-1.041-1.804-1.588-3.849-1.587-5.946.003-6.556 5.338-11.891 11.893-11.891 3.181.001 6.167 1.24 8.413 3.488 2.245 2.248 3.481 5.236 3.48 8.414-.003 6.557-5.338 11.892-11.893 11.892-1.99-.001-3.951-.5-5.688-1.448l-6.305 1.654zm6.597-3.807c1.676.995 3.276 1.591 5.392 1.592 5.448 0 9.886-4.434 9.889-9.885.002-5.462-4.415-9.89-9.881-9.892-5.452 0-9.887 4.434-9.889 9.884-.001 2.225.651 3.891 1.746 5.634l-.999 3.648 3.742-.981z"/></svg>
        PEDIR COROA DE FLORES
    </a>

    <script>
        const { jsPDF } = window.jspdf;

        // Preview da imagem
        document.getElementById('in-foto').onchange = function(e) {
            const reader = new FileReader();
            reader.onload = function() {
                document.getElementById('out-foto').src = reader.result;
            }
            reader.readAsDataURL(e.target.files[0]);
        };

        function gerarPreview() {
            const nome = document.getElementById('in-nome').value;
            const nasc = document.getElementById('in-nasc').value.split('-').reverse().join('/');
            const falec = document.getElementById('in-falec').value.split('-').reverse().join('/');
            const cemData = document.getElementById('in-cemiterio').value.split('|');
            const horario = document.getElementById('in-horario').value;
            const frase = document.getElementById('in-frase').value;

            if(!nome || !falec) {
                alert("Preencha o nome e a data de falecimento.");
                return;
            }

            document.getElementById('out-nome').innerText = nome;
            document.getElementById('out-datas').innerText = `Nascimento: ${nasc} — Falecimento: ${falec}`;
            document.getElementById('out-frase').innerText = `"${frase}"`;
            document.getElementById('out-cemiterio').innerText = cemData[0] || "";
            document.getElementById('out-endereco').innerText = cemData[1] || "";
            document.getElementById('out-horario').innerText = horario;

            // Link Google Maps
            if(cemData[1]) {
                const mapsUrl = `https://www.google.com/maps/search/?api=1&query=${encodeURIComponent(cemData[0] + " " + cemData[1])}`;
                document.getElementById('out-endereco').onclick = () => window.open(mapsUrl, '_blank');
            }

            document.getElementById('coluna-preview').classList.remove('hidden');
        }

        async function baixarPDF() {
            const element = document.getElementById('nota-para-exportar');
            const canvas = await html2canvas(element, { scale: 2 });
            const imgData = canvas.toDataURL('image/jpeg', 1.0);
            
            const pdf = new jsPDF({
                orientation: 'portrait',
                unit: 'px',
                format: [500, 700]
            });

            pdf.addImage(imgData, 'JPEG', 0, 0, 500, 700);
            pdf.save(`Comunicado_${document.getElementById('in-nome').value}.pdf`);
        }
    </script>
</body>
</html>
