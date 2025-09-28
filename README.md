<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Massa Nostra - Monte Seu Macarrão</title>
    <!-- Carregando Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Import da fonte Inter */
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f4f7f9;
        }
        .section-title {
            @apply text-xl font-bold border-b-2 pb-2 mb-4 text-red-700 border-red-200;
        }
        .input-style {
            @apply w-full p-3 border border-gray-300 rounded-lg focus:ring-red-500 focus:border-red-500 transition duration-150;
        }
        .limit-reached {
            @apply ring-4 ring-yellow-400 bg-yellow-100;
        }
        /* Adicionando sombra ao texto para que fique legível sobre a bandeira */
        .flag-text-shadow {
            text-shadow: 1px 1px 4px rgba(0,0,0,0.9); /* Sombra mais forte */
        }
        /* Cores vibrantes da bandeira italiana aplicadas ao fundo do cabeçalho */
        .italian-flag-gradient {
             /* Cores: Verde (#008C45), Branco (#FFFFFF), Vermelho (#CD212A) */
            background: linear-gradient(to right, #008C45 33.3%, #FFFFFF 33.3%, #FFFFFF 66.6%, #CD212A 66.6%);
        }
    </style>
</head>
<body class="min-h-screen p-4 flex justify-center">

    <div id="app" class="w-full max-w-xl bg-white shadow-2xl rounded-xl space-y-6 md:p-0">
        <!-- CABEÇALHO COM BANDEIRA NO FUNDO TOTAL -->
        <header class="text-center relative italian-flag-gradient rounded-t-xl py-6 shadow-2xl">
            <!-- Link do Google Drive para a logo. ATENÇÃO: Verifique as permissões. -->
            <img src="https://drive.google.com/uc?id=1cGwwqA1h1z9G_s5l8DM9qkV9XkdYF--6" 
                 alt="Logo Massa Nostra" 
                 class="w-40 h-40 object-cover mx-auto rounded-full mb-3 shadow-2xl border-4 border-white z-10 relative">
                 
            <div class="px-2">
                <h1 class="text-4xl font-extrabold text-white sm:text-5xl flag-text-shadow leading-tight">MASSA NOSTRA POTY</h1>
                <p class="text-base text-white font-medium mt-1 flag-text-shadow">@massanostra_poty | Monte seu prato e faça seu pedido!</p>
            </div>
        </header>

        <!-- CONSTRUTOR DE PEDIDOS -->
        <div class="p-6 space-y-6 md:p-8 pt-0">

            <section id="custom-order-section" class="space-y-6 p-4 border border-red-100 rounded-xl bg-red-50">
                <h2 class="section-title text-red-800">Monte Seu Prato</h2>

                <!-- Tamanho e Preço Base -->
                <div class="space-y-2">
                    <label class="block font-semibold text-gray-700">1. Escolha o Tamanho</label>
                    <div class="flex space-x-4">
                        <label class="flex items-center p-3 bg-white rounded-lg shadow-md hover:bg-red-50 transition duration-150 flex-1 cursor-pointer">
                            <input type="radio" name="size" value="P" data-price="24.90" class="form-radio text-red-600" checked>
                            <span class="ml-2 font-medium">P (R$ 24,90)</span>
                        </label>
                        <label class="flex items-center p-3 bg-white rounded-lg shadow-md hover:bg-red-50 transition duration-150 flex-1 cursor-pointer">
                            <input type="radio" name="size" value="G" data-price="32.90" class="form-radio text-red-600">
                            <span class="ml-2 font-medium">G (R$ 32,90)</span>
                        </label>
                    </div>
                </div>

                <!-- Massas e Molhos -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="space-y-2">
                        <label class="block font-semibold text-gray-700">2. Escolha a Massa (Obrigatório)</label>
                        <div id="massa-options" class="space-y-1">
                            <!-- Inserido via JS -->
                        </div>
                    </div>

                    <div class="space-y-2">
                        <label class="block font-semibold text-gray-700">3. Escolha o Molho (Obrigatório)</label>
                        <div id="molho-options" class="space-y-1">
                            <!-- Inserido via JS -->
                        </div>
                    </div>
                </div>

                <!-- Acompanhamentos -->
                <div class="space-y-2">
                    <label class="block font-semibold text-gray-700">4. Acompanhamentos (Máx. 6)</label>
                    <p id="acomp-counter" class="text-sm font-medium text-gray-500">Selecionados: 0/6</p>
                    <div id="acomp-options" class="grid grid-cols-2 sm:grid-cols-3 gap-2">
                        <!-- Inserido via JS -->
                    </div>
                </div>

                <!-- Observações e Preço do Item -->
                <div class="space-y-2">
                    <label for="obs" class="block font-semibold text-gray-700">5. Observações (Ex: Sem cebolinha, queijo a parte)</label>
                    <input type="text" id="obs" class="input-style" placeholder="Digite aqui...">
                    <p class="text-2xl font-extrabold text-green-700 mt-4 text-right">
                        Preço do Item: <span id="item-price-display">R$ 24,90</span>
                    </p>
                </div>
                
                <!-- Botão Adicionar ao Carrinho -->
                <button id="add-to-cart-btn" onclick="addToCart()" 
                    class="w-full bg-green-600 hover:bg-green-700 text-white font-bold py-3 rounded-lg shadow-md transition duration-300 transform hover:scale-[1.01] active:scale-[0.98]">
                    ADICIONAR AO CARRINHO E MONTAR OUTRO PRATO
                </button>
            </section>

            <!-- CARRINHO (ITENS ATUAIS) -->
            <section class="space-y-4 p-4 border border-gray-200 rounded-xl bg-gray-50">
                <h2 class="section-title text-gray-700 border-gray-200">Seu Carrinho (<span id="cart-count">0</span> Pratos)</h2>
                <ul id="cart-list" class="space-y-3">
                    <li id="empty-cart-message" class="text-gray-500 italic text-center">Nenhum item no carrinho.</li>
                </ul>
                <p class="text-3xl font-extrabold text-red-700 pt-3 border-t border-gray-300 text-right">
                    SUBTOTAL: <span id="subtotal-display">R$ 0,00</span>
                </p>
            </section>

            <!-- DADOS DE ENTREGA E PAGAMENTO -->
            <section id="checkout-section" class="space-y-6" style="display: none;">
                <h2 class="section-title">Dados de Entrega e Pagamento</h2>

                <!-- Dados do Cliente -->
                <div class="space-y-3">
                    <label class="block font-semibold text-gray-700">Seus Dados:</label>
                    <input type="text" id="nome" class="input-style" placeholder="Nome Completo *" required>
                    <input type="tel" id="telefone" class="input-style" placeholder="Telefone (WhatsApp) *" required>
                    <input type="text" id="endereco" class="input-style" placeholder="Endereço (Rua, Número, Bairro) *" required>
                    <input type="text" id="referencia" class="input-style" placeholder="Ponto de Referência (Ex: Casa verde, ao lado da praça)">
                </div>

                <!-- Taxa de Entrega -->
                <div class="space-y-2">
                    <label class="block font-semibold text-gray-700">Taxa de Entrega</label>
                    <div class="flex flex-col space-y-2">
                        <label class="flex items-center p-2 bg-white rounded-lg shadow-sm cursor-pointer">
                            <input type="radio" name="deliveryFee" value="2.00" class="form-radio text-red-600" checked>
                            <span class="ml-2">Entrega na Cidade (R$ 2,00)</span>
                        </label>
                        <label class="flex items-center p-2 bg-white rounded-lg shadow-sm cursor-pointer">
                            <input type="radio" name="deliveryFee" value="5.00" class="form-radio text-red-600">
                            <span class="ml-2">Entrega até 5km (R$ 5,00)</span>
                        </label>
                    </div>
                </div>
                
                <!-- Forma de Pagamento -->
                <div class="space-y-2">
                    <label class="block font-semibold text-gray-700">Forma de Pagamento</label>
                    <select id="payment-method" class="input-style">
                        <option value="Pix">Pix (Informar na mensagem)</option>
                        <option value="Dinheiro">Dinheiro (Precisa de troco?)</option>
                        <option value="Cartao-Debito">Cartão de Débito</option>
                        <option value="Cartao-Credito">Cartão de Crédito</option>
                    </select>
                </div>
                
                <!-- TOTAL FINAL -->
                <div class="mt-6 p-4 bg-red-100 rounded-lg shadow-inner">
                    <p class="text-lg font-bold text-red-800">Subtotal: <span id="final-subtotal">R$ 0,00</span></p>
                    <p class="text-lg font-bold text-red-800">Taxa: <span id="final-fee">R$ 2,00</span></p>
                    <p class="text-4xl font-extrabold text-red-900 mt-2">TOTAL FINAL: <span id="final-total">R$ 0,00</span></p>
                </div>

                <!-- BOTÃO WHATSAPP -->
                <button onclick="generateWhatsAppLink()" 
                    class="w-full flex items-center justify-center bg-green-500 hover:bg-green-600 text-white font-extrabold py-4 rounded-lg shadow-xl transition duration-300 transform hover:scale-[1.01] active:scale-[0.98]">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor" class="mr-2">
                        <path d="M12.001 2c-5.522 0-9.999 4.477-9.999 9.999 0 3.864 2.193 7.224 5.434 8.937l-.547 1.884c-.053.183.018.384.183.454.16.07.362.003.415-.177l.568-1.859c.772.196 1.583.298 2.404.298 5.522 0 9.999-4.477 9.999-9.999s-4.477-9.999-9.999-9.999zm4.646 12.339l-.025.048c-.627 1.127-1.428 1.176-2.923 1.025-1.579-.164-3.56-1.077-5.118-2.635-1.558-1.558-2.471-3.539-2.635-5.118-.151-1.495-.102-2.296 1.025-2.923l.048-.025.109-.052c.245-.118.528-.108.763.027l1.559.866c.216.12.339.362.31.597l-.078.618c-.035.267-.168.513-.377.674l-.234.186c-.198.158-.178.431.042.616l2.365 2.365c.184.22.457.24.616.042l.186-.234c.161-.209.407-.342.674-.377l.618-.078c.235-.029.477.094.597.31l.866 1.559c.135.235.145.518.027.763l-.052.109z"/>
                    </svg>
                    ENVIAR PEDIDO VIA WHATSAPP
                </button>
            </section>
        </div>

    </div>

    <script>
        // --- DADOS DO CARDÁPIO ---
        const MENU = {
            massas: ["Penne", "Spaguetti", "Parafuso", "Fetutini"],
            molhos: ["Bolonhesa", "Branco", "Rosé", "Sugo"],
            acompanhamentos: [
                "Bacon", "Calabresa", "Milho", "Ervilha", "Azeitona", 
                "Cebola", "Alho Frito", "Uva Passa", "Presunto", "Palmito", 
                "Pimentão", "Tomate Seco", "Catupiry", "Cheddar", "Frango", 
                "Champignon", "Tomate"
            ],
            prices: {
                'P': 24.90,
                'G': 32.90
            },
            whatsappNumber: "5517997381858" // Incluindo 55 (Brasil). ATUALIZE ESTE NÚMERO!
        };

        // --- ESTADO GLOBAL ---
        let cart = []; // Array de objetos para armazenar pedidos
        let currentItemPrice = MENU.prices['P'];
        let selectedAcompanhamentos = 0;

        // --- REFERÊNCIAS DOM ---
        const massaOptionsDiv = document.getElementById('massa-options');
        const molhoOptionsDiv = document.getElementById('molho-options');
        const acompOptionsDiv = document.getElementById('acomp-options');
        const acompCounter = document.getElementById('acomp-counter');
        const itemPriceDisplay = document.getElementById('item-price-display');
        const sizeRadios = document.querySelectorAll('input[name="size"]');
        const cartList = document.getElementById('cart-list');
        const emptyCartMessage = document.getElementById('empty-cart-message');
        const cartCountDisplay = document.getElementById('cart-count');
        const subtotalDisplay = document.getElementById('subtotal-display');
        const checkoutSection = document.getElementById('checkout-section');
        
        const finalSubtotal = document.getElementById('final-subtotal');
        const finalFee = document.getElementById('final-fee');
        const finalTotal = document.getElementById('final-total');
        const deliveryFeeRadios = document.querySelectorAll('input[name="deliveryFee"]');

        // --- FUNÇÕES DE RENDERIZAÇÃO INICIAL ---

        function renderOption(container, name, options, type = 'radio') {
            container.innerHTML = options.map(option => `
                <label class="flex items-center cursor-pointer">
                    <input type="${type}" name="${name}" value="${option}" 
                           class="${type === 'radio' ? 'form-radio text-red-600' : 'form-checkbox text-red-600'}">
                    <span class="ml-2">${option}</span>
                </label>
            `).join('');
        }

        function setupUI() {
            // Renderiza Massas e Molhos (Radio Buttons)
            renderOption(massaOptionsDiv, 'massa', MENU.massas);
            renderOption(molhoOptionsDiv, 'molho', MENU.molhos);

            // Renderiza Acompanhamentos (Checkboxes) e Adiciona Listener
            acompanhamentosHTML = MENU.acompanhamentos.map(acomp => `
                <label class="flex items-center p-2 bg-white rounded-lg shadow-sm hover:bg-red-50 transition duration-150 cursor-pointer">
                    <input type="checkbox" name="acomp" value="${acomp}" class="form-checkbox text-red-600">
                    <span class="ml-2 text-sm">${acomp}</span>
                </label>
            `).join('');
            acompOptionsDiv.innerHTML = acompanhamentosHTML;
            acompOptionsDiv.addEventListener('change', updateAcompCount);

            // Adiciona Listener para Tamanho
            sizeRadios.forEach(radio => {
                radio.addEventListener('change', updateItemPrice);
            });
            
            // Adiciona Listener para Taxa de Entrega
            deliveryFeeRadios.forEach(radio => {
                radio.addEventListener('change', updateFinalSummary);
            });

            updateItemPrice(); // Inicializa o preço do item
            updateFinalSummary(); // Inicializa o total final
        }

        // --- FUNÇÕES DE LÓGICA DE PEDIDO ---

        function updateItemPrice() {
            const selectedSize = document.querySelector('input[name="size"]:checked');
            if (selectedSize) {
                currentItemPrice = parseFloat(selectedSize.dataset.price);
                itemPriceDisplay.textContent = `R$ ${currentItemPrice.toFixed(2).replace('.', ',')}`;
            }
        }

        function updateAcompCount(event) {
            const checkboxes = document.querySelectorAll('input[name="acomp"]:checked');
            selectedAcompanhamentos = checkboxes.length;
            acompCounter.textContent = `Selecionados: ${selectedAcompanhamentos}/6`;

            // Limita a 6 seleções
            if (selectedAcompanhamentos >= 6) {
                document.querySelectorAll('input[name="acomp"]:not(:checked)').forEach(cb => {
                    cb.disabled = true;
                    // Adiciona um estilo visual de limite atingido
                    cb.closest('label').classList.add('limit-reached');
                });
            } else {
                document.querySelectorAll('input[name="acomp"]').forEach(cb => {
                    cb.disabled = false;
                    cb.closest('label').classList.remove('limit-reached');
                });
            }
        }

        function getFormData() {
            const sizeRadio = document.querySelector('input[name="size"]:checked');
            const massaRadio = document.querySelector('input[name="massa"]:checked');
            const molhoRadio = document.querySelector('input[name="molho"]:checked');
            const acompCheckboxes = document.querySelectorAll('input[name="acomp"]:checked');
            
            if (!sizeRadio || !massaRadio || !molhoRadio) {
                showModal('Por favor, selecione o **Tamanho**, a **Massa** e o **Molho**.', 'bg-red-500');
                return null;
            }

            const customItem = {
                size: sizeRadio.value,
                price: currentItemPrice,
                massa: massaRadio.value,
                molho: molhoRadio.value,
                acompanhamentos: Array.from(acompCheckboxes).map(cb => cb.value),
                obs: document.getElementById('obs').value.trim()
            };

            return customItem;
        }

        function addToCart() {
            const item = getFormData();
            if (item) {
                cart.push(item);
                showModal('Prato adicionado ao carrinho! Você pode montar outro.', 'bg-green-500');
                renderCart();
                resetForm();
            }
        }
        
        function resetForm() {
            // Desmarca todos os checkboxes de acompanhamentos e inputs de texto
            document.querySelectorAll('input[name="massa"]').forEach(r => r.checked = false);
            document.querySelectorAll('input[name="molho"]').forEach(r => r.checked = false);
            document.querySelectorAll('input[name="acomp"]').forEach(cb => cb.checked = false);
            document.getElementById('obs').value = '';

            // Reinicia a contagem de acompanhamentos e reabilita os checkboxes
            selectedAcompanhamentos = 0;
            updateAcompCount();
            
            // Mantém o tamanho e preço iniciais (P) selecionados
            document.querySelector('input[name="size"][value="P"]').checked = true;
            updateItemPrice();
        }

        // --- FUNÇÕES DE CARRINHO E TOTALIZAÇÃO ---

        function renderCart() {
            cartList.innerHTML = '';
            let subtotal = 0;

            if (cart.length === 0) {
                cartList.innerHTML = `<li id="empty-cart-message" class="text-gray-500 italic text-center">Nenhum item no carrinho.</li>`;
                checkoutSection.style.display = 'none';
            } else {
                checkoutSection.style.display = 'block';
                cart.forEach((item, index) => {
                    subtotal += item.price;
                    const li = document.createElement('li');
                    li.className = 'p-3 border border-gray-100 bg-white rounded-lg shadow-sm space-y-1';
                    
                    const acompList = item.acompanhamentos.length > 0 ? 
                        item.acompanhamentos.join(', ') : 'Nenhum';
                        
                    li.innerHTML = `
                        <div class="flex justify-between items-center">
                            <h3 class="font-bold text-gray-800">#${index + 1} - Massa ${item.size} (${item.massa})</h3>
                            <button onclick="removeItem(${index})" class="text-red-500 hover:text-red-700 text-sm font-semibold transition duration-150">
                                Remover
                            </button>
                        </div>
                        <p class="text-sm text-gray-600">Molho: ${item.molho}</p>
                        <p class="text-sm text-gray-600">Acompanhamentos (+ Cebolinha): ${acompList}</p>
                        <p class="text-sm text-gray-600 italic">Obs: ${item.obs || 'Nenhuma'}</p>
                        <p class="text-lg font-extrabold text-green-700 text-right">R$ ${item.price.toFixed(2).replace('.', ',')}</p>
                    `;
                    cartList.appendChild(li);
                });
            }

            cartCountDisplay.textContent = cart.length;
            subtotalDisplay.textContent = `R$ ${subtotal.toFixed(2).replace('.', ',')}`;
            updateFinalSummary();
        }

        function removeItem(index) {
            cart.splice(index, 1);
            renderCart();
            updateFinalSummary();
        }

        function updateFinalSummary() {
            const subtotal = cart.reduce((sum, item) => sum + item.price, 0);
            const feeRadio = document.querySelector('input[name="deliveryFee"]:checked');
            const deliveryFee = feeRadio ? parseFloat(feeRadio.value) : 2.00;
            const finalTotalValue = subtotal + deliveryFee;

            finalSubtotal.textContent = `R$ ${subtotal.toFixed(2).replace('.', ',')}`;
            finalFee.textContent = `R$ ${deliveryFee.toFixed(2).replace('.', ',')}`;
            finalTotal.textContent = `R$ ${finalTotalValue.toFixed(2).replace('.', ',')}`;
        }

        // --- FUNÇÕES DE CHECKOUT E WHATSAPP ---
        
        function validateCheckoutForm() {
            const requiredFields = [
                { id: 'nome', name: 'Nome' },
                { id: 'telefone', name: 'Telefone' },
                { id: 'endereco', name: 'Endereço' }
            ];
            let isValid = true;
            let missingFields = [];
            
            // Limpa classes de erro anteriores
            document.querySelectorAll('.input-style').forEach(input => {
                input.classList.remove('border-red-500', 'ring-2', 'ring-red-500');
            });

            requiredFields.forEach(field => {
                const input = document.getElementById(field.id);
                if (!input.value.trim()) {
                    isValid = false;
                    missingFields.push(field.name);
                    // Adiciona destaque visual ao campo vazio
                    input.classList.add('border-red-500', 'ring-2', 'ring-red-500');
                }
            });

            if (!isValid) {
                const message = `Por favor, preencha os campos obrigatórios: **${missingFields.join(', ')}**.`;
                showModal(message, 'bg-red-500');
            }

            return isValid;
        }

        function generateWhatsAppLink() {
            if (cart.length === 0) {
                showModal('Seu carrinho está vazio. Adicione um prato antes de enviar.', 'bg-yellow-500');
                return;
            }

            if (!validateCheckoutForm()) {
                return;
            }

            const nome = document.getElementById('nome').value.trim();
            const telefone = document.getElementById('telefone').value.trim();
            const endereco = document.getElementById('endereco').value.trim();
            const referencia = document.getElementById('referencia').value.trim();
            const paymentMethod = document.getElementById('payment-method').value;
            
            const subtotal = cart.reduce((sum, item) => sum + item.price, 0);
            const feeRadio = document.querySelector('input[name="deliveryFee"]:checked');
            const deliveryFee = feeRadio ? parseFloat(feeRadio.value) : 2.00;
            const finalTotalValue = subtotal + deliveryFee;
            
            const feeLabel = feeRadio.nextElementSibling.textContent.trim();


            // Montagem da Mensagem do Pedido
            let message = `🍝 Olá, Massa Nostra! Meu pedido é o seguinte:\n\n`;
            
            message += `--- ITENS (${cart.length} prato(s)) ---\n`;
            cart.forEach((item, index) => {
                const acompText = item.acompanhamentos.length > 0 ? item.acompanhamentos.join(', ') : 'Nenhum';
                message += `\n*PRATO #${index + 1} (${item.size}):*\n`;
                message += `  Massa: ${item.massa}\n`;
                message += `  Molho: ${item.molho}\n`;
                message += `  Acompanhamentos (+ Cebolinha): ${acompText}\n`;
                message += `  Obs: ${item.obs || 'Nenhuma'}\n`;
                message += `  Valor: R$ ${item.price.toFixed(2).replace('.', ',')}\n`;
            });
            
            message += `\n--- RESUMO DA COMPRA ---\n`;
            message += `*SUBTOTAL DOS ITENS:* R$ ${subtotal.toFixed(2).replace('.', ',')}\n`;
            message += `*TAXA DE ENTREGA:* ${feeLabel} (R$ ${deliveryFee.toFixed(2).replace('.', ',')})\n`;
            message += `*TOTAL FINAL:* R$ ${finalTotalValue.toFixed(2).replace('.', ',')}\n\n`;
            
            message += `--- DADOS DO CLIENTE ---\n`;
            message += `Nome: ${nome}\n`;
            message += `Telefone: ${telefone}\n`;
            message += `Endereço: ${endereco}\n`;
            message += `Referência: ${referencia || 'Sem referência'}\n`;
            message += `Pagamento: ${paymentMethod}\n\n`;
            
            message += `Aguardamos a confirmação! Obrigado!`;
            
            const encodedMessage = encodeURIComponent(message);
            const whatsappLink = `https://wa.me/${MENU.whatsappNumber}?text=${encodedMessage}`;
            
            console.log("WhatsApp Link gerado:", whatsappLink); // Log para debug

            try {
                const newWindow = window.open(whatsappLink, '_blank');
                
                // Verifica se a nova janela foi aberta ou se foi bloqueada
                if (newWindow === null || typeof newWindow === 'undefined' || newWindow.closed) {
                    // Pop-up bloqueado
                    showModal(`
                        <h3 class="text-xl font-bold text-yellow-700 mb-2">Atenção: Pop-up Bloqueado!</h3>
                        <p>Seu navegador impediu a abertura automática do WhatsApp. Clique no link abaixo para enviar o pedido:</p>
                        <a href="${whatsappLink}" target="_blank" class="text-blue-600 underline font-bold mt-3 block p-2 border border-blue-200 bg-blue-50 rounded-lg hover:bg-blue-100">
                            CLIQUE AQUI PARA ABRIR O WHATSAPP
                        </a>
                        <p class="text-sm mt-2 text-gray-500">Ou use o botão 'Entendi' e libere pop-ups para este site.</p>
                    `, 'bg-yellow-600');
                }
            } catch (error) {
                console.error("Erro ao tentar abrir o WhatsApp:", error);
                showModal('Ocorreu um erro inesperado ao tentar abrir o WhatsApp.', 'bg-red-500');
            }
        }

        // --- FUNÇÃO MODAL (Substituto de alert/confirm) ---

        function showModal(message, bgColor) {
            const modalId = 'temp-modal';
            let modal = document.getElementById(modalId);
            
            if (!modal) {
                modal = document.createElement('div');
                modal.id = modalId;
                modal.className = 'fixed inset-0 bg-gray-900 bg-opacity-50 flex items-center justify-center p-4 z-50 transition-opacity duration-300 opacity-0';
                modal.innerHTML = `
                    <div class="bg-white p-6 rounded-lg shadow-2xl max-w-sm w-full transform scale-95 transition-transform duration-300">
                        <div id="modal-content" class="text-center"></div>
                        <button onclick="document.getElementById('${modalId}').remove()" class="mt-4 w-full ${bgColor} text-white font-bold py-2 rounded-lg hover:opacity-90">
                            Entendi
                        </button>
                    </div>
                `;
                document.body.appendChild(modal);
            }
            
            document.getElementById('modal-content').innerHTML = message;
            
            // Força o reflow para a transição
            setTimeout(() => {
                modal.classList.remove('opacity-0');
                modal.querySelector('div').classList.remove('scale-95');
                modal.querySelector('div').classList.add('scale-100');
            }, 10);
        }

        // --- INICIALIZAÇÃO ---
        window.onload = setupUI;
        
    </script>
</body>
</html>
