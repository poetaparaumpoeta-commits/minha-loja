<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Loja Roots - Demo</title>
<style>
  :root{
    --accent:#2b6cb0;
    --muted:#6b7280;
    --bg:#fbfbfc;
    --card:#ffffff;
    --danger:#dc2626;
  }
  *{box-sizing:border-box}
  body{font-family:Inter,Arial,Helvetica,sans-serif;margin:0;background:var(--bg);color:#111}
  header.appbar{display:flex;align-items:center;justify-content:space-between;padding:12px 16px;background:linear-gradient(90deg,#f8fafc,#eef2f7);border-bottom:1px solid #e6e9ee}
  header.appbar h1{font-size:18px;margin:0}
  .container{max-width:1000px;margin:24px auto;padding:0 16px}

  /* Screens */
  .screen{display:none;min-height:60vh;padding:20px 0}
  .active{display:block}

  /* Login */
  .card{background:var(--card);border-radius:10px;padding:20px;box-shadow:0 6px 18px rgba(10,10,12,0.06);max-width:420px;margin:40px auto}
  .card h2{margin-bottom:12px}
  .field{margin-bottom:10px}
  input[type="text"], input[type="number"], input[type="password"], select, textarea{
    width:100%;padding:10px;border:1px solid #ddd;border-radius:8px;font-size:14px
  }
  button.btn{padding:10px 14px;border-radius:8px;border:none;background:var(--accent);color:#fff;cursor:pointer;font-weight:600}
  button.btn[disabled]{opacity:.55;cursor:not-allowed}

  /* Welcome */
  .welcome{display:flex;flex-direction:column;align-items:center;justify-content:center;min-height:40vh}
  .welcome h1{font-size:28px;color:var(--accent);animation:fadeIn 2.6s ease forwards;opacity:0}
  @keyframes fadeIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}

  /* Categories */
  .title{display:flex;align-items:center;justify-content:space-between;margin-bottom:10px}
  .title h2{margin:0}
  .grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:18px}
  .card-cat{position:relative;height:140px;border-radius:12px;overflow:hidden;display:flex;align-items:center;justify-content:center;color:white;font-weight:700;text-shadow:0 2px 6px rgba(0,0,0,0.45);cursor:pointer;box-shadow:0 6px 18px rgba(14,16,20,0.06);transition:transform .25s, box-shadow .25s}
  .card-cat::after{content:"";position:absolute;inset:0;background:linear-gradient(180deg,rgba(0,0,0,0.08),rgba(0,0,0,0.35));}
  .card-cat span{position:relative;z-index:2}
  .card-cat:hover{transform:translateY(-6px);box-shadow:0 12px 30px rgba(14,16,20,0.12)}

  /* Admin add button (hidden for non-owner) */
  #adminAddBtn{position:fixed;right:18px;bottom:18px;background:var(--accent);color:#fff;border:none;border-radius:50%;width:56px;height:56px;font-size:28px;display:flex;align-items:center;justify-content:center;box-shadow:0 10px 30px rgba(43,108,176,0.18);cursor:pointer}

  /* Products */
  .products{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:16px;margin-top:16px}
  .prod{background:var(--card);padding:10px;border-radius:10px;text-align:center;box-shadow:0 6px 18px rgba(10,10,12,0.05)}
  .prod img{width:100%;height:150px;object-fit:cover;border-radius:8px}
  .prod p{margin:8px 0 6px;font-weight:600}
  .prod button{width:100%;padding:8px;border-radius:8px;border:none;background:#059669;color:#fff;cursor:pointer}

  /* Modals */
  .overlay{position:fixed;inset:0;background:rgba(0,0,0,0.45);display:none;align-items:center;justify-content:center;padding:20px;z-index:60}
  .overlay.open{display:flex}
  .modal{background:#fff;border-radius:12px;padding:18px;max-width:520px;width:100%;box-shadow:0 20px 50px rgba(2,6,23,0.3)}
  .modal h3{margin:0 0 12px}
  .modal .row{display:flex;gap:8px}
  .modal .row > *{flex:1}
  .closeX{position:absolute;right:12px;top:8px;background:#eee;border-radius:6px;border:none;padding:6px;cursor:pointer}

  /* Payment options */
  .pay-methods{display:flex;gap:8px;flex-wrap:wrap}
  .pay-item{flex:1;padding:10px;border-radius:8px;border:1px solid #ddd;cursor:pointer;text-align:center}
  .pay-item.active{border-color:var(--accent);box-shadow:0 6px 18px rgba(43,108,176,0.08)}

  /* small helpers */
  .muted{color:var(--muted);font-size:13px}
  footer.small{font-size:12px;color:#666;margin-top:14px}
  @media (max-width:420px){ .card{margin:16px} .welcome h1{font-size:22px} }
</style>
</head>
<body>

<header class="appbar">
  <h1>Loja Roots</h1>
  <div class="muted">Versão demo</div>
</header>

<div class="container">

  <!-- LOGIN -->
  <section id="screen-login" class="screen active">
    <div class="card" role="form" aria-label="Formulário de login">
      <h2>Entrar na Loja Roots</h2>

      <div class="field">
        <label class="muted">Nome</label>
        <input id="inputNome" type="text" placeholder="Seu nome completo">
      </div>

      <div class="field">
        <label class="muted">Rua</label>
        <input id="inputRua" type="text" placeholder="Nome da rua">
      </div>

      <div class="field">
        <label class="muted">Número da casa</label>
        <input id="inputNumero" type="text" placeholder="Número da casa">
      </div>

      <div class="field">
        <label class="muted">Código do proprietário (opcional)</label>
        <input id="inputOwnerCode" type="password" placeholder="Digite o código do dono se for você">
        <div class="muted" style="font-size:12px;margin-top:6px">Se você é o dono, digite o código aqui para ver o botão de postar produtos.</div>
      </div>

      <div style="display:flex;gap:10px;margin-top:12px;align-items:center">
        <button id="btnAcessar" class="btn" disabled>Acessar</button>
        <button id="btnTest" class="btn" style="background:#94a3b8">Testar local</button>
      </div>

      <p class="muted" style="margin-top:10px">Preencha Nome, Rua e Número da casa para continuar.</p>
    </div>
  </section>

  <!-- WELCOME -->
  <section id="screen-welcome" class="screen">
    <div class="welcome">
      <h1>✨ Bem-vindo(a) à Loja Roots ✨</h1>
      <p class="muted" style="margin-top:8px">Busque produtos, veja categorias e poste (se for o dono).</p>
    </div>
  </section>

  <!-- CATEGORIES -->
  <section id="screen-categories" class="screen">
    <div class="title" style="width:100%">
      <div>
        <h2>Loja Roots</h2>
        <div class="muted">Escolha uma categoria</div>
      </div>
      <div class="muted" id="welcomeUser"></div>
    </div>

    <div class="grid" id="categoriesGrid">
      <!-- Cards gerados por JS -->
    </div>
  </section>

  <!-- PRODUCTS -->
  <section id="screen-products" class="screen">
    <div style="width:100%;max-width:900px">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <h2 id="productsTitle">Produtos</h2>
        <div>
          <button id="btnBackToCats" class="btn" style="background:#6b7280">Voltar</button>
        </div>
      </div>

      <div class="products" id="productsGrid"></div>
      <footer class="small muted">Imagens de exemplo. Suba suas próprias imagens no botão + (se for dono).</footer>
    </div>
  </section>

</div>

<!-- ADMIN ADD PRODUCT BUTTON (visível só para dono) -->
<button id="adminAddBtn" title="Adicionar produto" style="display:none">＋</button>

<!-- MODAL: Add Product (admin) -->
<div id="modalAdd" class="overlay" role="dialog" aria-modal="true">
  <div class="modal">
    <button class="closeX" onclick="closeAddModal()">✕</button>
    <h3>Adicionar produto</h3>
    <div class="field">
      <label class="muted">Categoria</label>
      <select id="addCategory">
        <option value="boné">Bonés</option>
        <option value="blusa">Blusas</option>
        <option value="moletom">Moletons</option>
        <option value="camiseta">Camisetas</option>
        <option value="tênis">Tênis</option>
      </select>
    </div>
    <div class="field">
      <label class="muted">Nome do produto</label>
      <input id="addName" type="text" placeholder="Ex: Boné Roots Preto">
    </div>
    <div class="field">
      <label class="muted">Imagem (URL) — ou escolha arquivo abaixo</label>
      <input id="addImgUrl" type="text" placeholder="https://...">
    </div>
    <div class="field">
      <label class="muted">Ou envie um arquivo de imagem</label>
      <input id="addImgFile" type="file" accept="image/*">
    </div>
    <div style="display:flex;gap:8px;margin-top:8px">
      <button class="btn" onclick="saveProduct()">Salvar</button>
      <button class="btn" style="background:#94a3b8" onclick="closeAddModal()">Cancelar</button>
    </div>
    <p class="muted" style="margin-top:8px;font-size:13px">Os produtos são salvos localmente no seu navegador (localStorage). Para tê-los no site público, poste esses arquivos no servidor.</p>
  </div>
</div>

<!-- MODAL: Product detail / checkout -->
<div id="modalProduct" class="overlay">
  <div class="modal" id="modalProductInner">
    <button class="closeX" onclick="closeProductModal()">✕</button>
    <h3 id="prodName">Produto</h3>
    <img id="prodImg" src="" alt="" style="width:100%;height:220px;object-fit:cover;border-radius:8px;margin:8px 0">
    <div style="display:flex;gap:8px">
      <button class="btn" onclick="openPayment('pix')">Pagar PIX</button>
      <button class="btn" onclick="openPayment('card')">Cartão</button>
    </div>
  </div>
</div>

<!-- MODAL: Payment -->
<div id="modalPayment" class="overlay">
  <div class="modal">
    <button class="closeX" onclick="closePaymentModal()">✕</button>
    <h3>Pagamento</h3>

    <div class="pay-methods" id="payMethods">
      <div class="pay-item" data-method="pix">PIX</div>
      <div class="pay-item" data-method="card">Cartão (Crédito/Débito)</div>
    </div>

    <div id="payPix" style="display:none;margin-top:12px">
      <p class="muted">Chave PIX (exemplo): <strong>lojaroots@pix.exemplo</strong></p>
      <div style="margin-top:8px">
        <button class="btn" onclick="finishPayment('pix')">Concluir via PIX</button>
      </div>
    </div>

    <div id="payCard" style="display:none;margin-top:12px">
      <div class="field"><label class="muted">Nome do cartão</label><input id="cardName" type="text" placeholder="Nome impresso no cartão"></div>
      <div class="row" style="display:flex;gap:8px">
        <input id="cardNumber" type="text" placeholder="Número do cartão" />
      </div>
      <div style="display:flex;gap:8px;margin-top:8px">
        <input id="cardExp" type="text" placeholder="MM/AA" style="flex:1"/>
        <input id="cardCvv" type="text" placeholder="CVV" style="width:120px"/>
      </div>
      <div style="margin-top:10px"><button class="btn" onclick="finishPayment('card')">Pagar com Cartão</button></div>
    </div>

  </div>
</div>

<script>
/*
  Loja Roots - arquivo único
  - Altere OWNER_SECRET abaixo para um código seu (apenas você deve conhecer).
  - Os produtos são salvos no localStorage (chave 'loja_roots_products').
  - Para publicar definitivamente: hospede index.html + arquivos no seu serviço (Netlify, GitLab Pages...).
*/

// === CONFIG
const OWNER_SECRET = 'ROOTS2025'; // <-- ALTERE para um código só seu antes de publicar

// === DOM refs
const screenLogin = document.getElementById('screen-login');
const screenWelcome = document.getElementById('screen-welcome');
const screenCats = document.getElementById('screen-categories');
const screenProducts = document.getElementById('screen-products');

const btnAcessar = document.getElementById('btnAcessar');
const btnTest = document.getElementById('btnTest');
const inputNome = document.getElementById('inputNome');
const inputRua = document.getElementById('inputRua');
const inputNumero = document.getElementById('inputNumero');
const inputOwnerCode = document.getElementById('inputOwnerCode');
const welcomeUser = document.getElementById('welcomeUser');

const adminAddBtn = document.getElementById('adminAddBtn');
const modalAdd = document.getElementById('modalAdd');
const addCategory = document.getElementById('addCategory');
const addName = document.getElementById('addName');
const addImgUrl = document.getElementById('addImgUrl');
const addImgFile = document.getElementById('addImgFile');

const categoriesGrid = document.getElementById('categoriesGrid');
const productsGrid = document.getElementById('productsGrid');
const productsTitle = document.getElementById('productsTitle');

const modalProduct = document.getElementById('modalProduct');
const prodName = document.getElementById('prodName');
const prodImg = document.getElementById('prodImg');

const modalPayment = document.getElementById('modalPayment');
const payMethods = document.getElementById('payMethods');
const payPix = document.getElementById('payPix');
const payCard = document.getElementById('payCard');

let currentUser = null;
let isOwner = false;
let currentCategory = null;
let currentProduct = null;

// Storage key
const STORAGE_KEY = 'loja_roots_products_v1';

// Seed products if none
function getStoredProducts(){
  let data = localStorage.getItem(STORAGE_KEY);
  if(!data){
    const seed = {
      "boné": [
        {name:"Boné Roots Preto", img:"https://via.placeholder.com/400x350?text=Bon%C3%A9+Preto"},
        {name:"Boné Azul Roots", img:"https://via.placeholder.com/400x350?text=Bon%C3%A9+Azul"}
      ],
      "blusa":[
        {name:"Blusa Roots Branca", img:"https://via.placeholder.com/400x350?text=Blusa+Branca"},
        {name:"Blusa Roots Preta", img:"https://via.placeholder.com/400x350?text=Blusa+Preta"}
      ],
      "moletom":[
        {name:"Moletom Roots Cinza", img:"https://via.placeholder.com/400x350?text=Moletom+Cinza"},
        {name:"Moletom Roots Azul", img:"https://via.placeholder.com/400x350?text=Moletom+Azul"}
      ],
      "camiseta":[
        {name:"Camiseta Roots Vermelha", img:"https://via.placeholder.com/400x350?text=Camiseta+Vermelha"},
        {name:"Camiseta Roots Branca", img:"https://via.placeholder.com/400x350?text=Camiseta+Branca"}
      ],
      "tênis":[
        {name:"Tênis Roots Branco", img:"https://via.placeholder.com/400x350?text=T%C3%AAnis+Branco"},
        {name:"Tênis Roots Preto", img:"https://via.placeholder.com/400x350?text=T%C3%AAnis+Preto"}
      ]
    };
    localStorage.setItem(STORAGE_KEY, JSON.stringify(seed));
    return seed;
  }
  try{ return JSON.parse(data) } catch(e){ return {} }
}
function saveStoredProducts(obj){ localStorage.setItem(STORAGE_KEY, JSON.stringify(obj)); }

// Render categories (static list)
const CATEGORIES = [
  {key:'boné', label:'Bonés', img:'https://images.unsplash.com/photo-1521335629791-ce4aec67dd53?auto=format&fit=crop&w=800&q=80'},
  {key:'blusa', label:'Blusas', img:'https://images.unsplash.com/photo-1520975918318-3e28d1f3c2f9?auto=format&fit=crop&w=800&q=80'},
  {key:'moletom', label:'Moletons', img:'https://images.unsplash.com/photo-1602810318383-e13fdb9de6b0?auto=format&fit=crop&w=800&q=80'},
  {key:'camiseta', label:'Camisetas', img:'https://images.unsplash.com/photo-1586795851500-9d08a7a71d4a?auto=format&fit=crop&w=800&q=80'},
  {key:'tênis', label:'Tênis', img:'https://images.unsplash.com/photo-1595950653234-d750089bc07c?auto=format&fit=crop&w=800&q=80'}
];

function renderCategories(){
  categoriesGrid.innerHTML = '';
  CATEGORIES.forEach(cat=>{
    const d = document.createElement('div');
    d.className = 'card-cat';
    d.style.backgroundImage = `url('${cat.img}')`;
    d.innerHTML = `<span>${cat.label}</span>`;
    d.onclick = ()=> openCategory(cat.key);
    categoriesGrid.appendChild(d);
  });
}

// Show screen helper
function showScreen(id){
  [screenLogin, screenWelcome, screenCats, screenProducts].forEach(s=>s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

// Login validation
function validateLoginInputs(){
  const filled = inputNome.value.trim() !== '' && inputRua.value.trim() !== '' && inputNumero.value.trim() !== '';
  btnAcessar.disabled = !filled;
}
[inputNome, inputRua, inputNumero].forEach(el=>el.addEventListener('input', validateLoginInputs));

// Test button (fills sample values)
btnTest.addEventListener('click', ()=>{ inputNome.value='Test User'; inputRua.value='Rua Exemplo'; inputNumero.value='123'; validateLoginInputs(); });

// On Acessar
btnAcessar.addEventListener('click', ()=>{
  currentUser = {nome: inputNome.value.trim(), rua: inputRua.value.trim(), numero: inputNumero.value.trim()};
  const enteredOwner = (inputOwnerCode.value || '').trim();
  isOwner = (enteredOwner !== '' && enteredOwner === OWNER_SECRET);
  // store owner flag in session storage for session persistence
  sessionStorage.setItem('loja_roots_isOwner', isOwner ? '1' : '0');
  welcomeUser.textContent = `Olá, ${currentUser.nome}`;
  // go to welcome and then categories
  showScreen('screen-welcome');
  setTimeout(()=>{ renderCategories(); renderOwnerUI(); showScreen('screen-categories'); }, 2000);
});

// On load, if session owner exists show admin button
function renderOwnerUI(){
  const ownerFlag = sessionStorage.getItem('loja_roots_isOwner') === '1';
  if(ownerFlag) adminAddBtn.style.display = 'flex'; else adminAddBtn.style.display = 'none';
}

// Category open
function openCategory(key){
  currentCategory = key;
  productsTitle.textContent = CATEGORIES.find(c=>c.key===key)?.label || key;
  renderProducts(key);
  showScreen('screen-products');
}

// render products from storage
function renderProducts(category){
  const data = getStoredProducts();
  const items = data[category] || [];
  productsGrid.innerHTML = '';
  items.forEach((p, idx)=>{
    const div = document.createElement('div'); div.className='prod';
    div.innerHTML = `
      <div class="prod-img"><img src="${p.img}" alt="${p.name || ''}" style="border-radius:6px;max-height:150px;"></div>
      <p>${p.name || ('Produto '+(idx+1))}</p>
      <button onclick="openProductModal('${category}',${idx})">Ver / Comprar</button>`;
    productsGrid.appendChild(div);
  });
}

// Product modal
function openProductModal(category, index){
  const data = getStoredProducts();
  const p = (data[category] || [])[index];
  if(!p) return alert('Produto não encontrado');
  currentProduct = {category, index, ...p};
  prodName.textContent = p.name || 'Produto';
  prodImg.src = p.img || '';
  modalProduct.classList.add('open');
  // open overlay
}
function closeProductModal(){ modalProduct.classList.remove('open'); currentProduct = null; }

// Admin add product flow
adminAddBtn.addEventListener('click', ()=>{ openAddModal() });
function openAddModal(){ modalAdd.classList.add('open'); }
function closeAddModal(){
  modalAdd.classList.remove('open');
  addName.value=''; addImgUrl.value=''; addImgFile.value='';
}

// Save product (admin)
function saveProduct(){
  const cat = addCategory.value;
  const name = addName.value.trim();
  if(!name){ alert('Coloque um nome para o produto'); return; }

  // prefer file over URL
  const file = addImgFile.files && addImgFile.files[0];
  if(file){
    const reader = new FileReader();
    reader.onload = function(e){
      const dataUrl = e.target.result;
      persistProduct(cat, {name, img:dataUrl});
      closeAddModal();
      if(currentCategory===cat) renderProducts(cat);
      else renderCategories();
    };
    reader.readAsDataURL(file);
    return;
  }
  const url = addImgUrl.value.trim() || 'https://via.placeholder.com/400x350?text=Sem+Imagem';
  persistProduct(cat, {name, img:url});
  closeAddModal();
  if(currentCategory===cat) renderProducts(cat);
  else renderCategories();
}
function persistProduct(category, product){
  const data = getStoredProducts();
  if(!data[category]) data[category]=[];
  data[category].push(product);
  saveStoredProducts(data);
  alert('Produto salvo localmente!');
}

// Payment flow
function openPayment(method){
  modalPayment.classList.add('open');
  if(method==='pix'){ showPayment('pix') } else if(method==='card'){ showPayment('card') } else { showPayment('pix') }
}
function closePaymentModal(){ modalPayment.classList.remove('open') }

payMethods.querySelectorAll('.pay-item').forEach(el=>{
  el.addEventListener('click', ()=> {
    payMethods.querySelectorAll('.pay-item').forEach(i=>i.classList.remove('active'));
    el.classList.add('active');
    showPayment(el.dataset.method);
  });
});
function showPayment(method){
  payPix.style.display = 'none'; payCard.style.display = 'none';
  if(method==='pix') payPix.style.display = 'block';
  else payCard.style.display = 'block';
}
function finishPayment(type){
  // This is a demo: we only show success.
  closeProductModal();
  closePaymentModal();
  alert('Pagamento simulado com sucesso via ' + (type==='pix' ? 'PIX' : 'Cartão') + ' — Obrigado!');
}

// Back to categories
document.getElementById('btnBackToCats').addEventListener('click', ()=>{ showScreen('screen-categories'); });

// exit store: reload to clear session and views
function exitStore(){ sessionStorage.removeItem('loja_roots_isOwner'); location.reload(); }

// utility: open add modal only for owner
function checkOwnerOnLoad(){
  const ownerFlag = sessionStorage.getItem('loja_roots_isOwner') === '1';
  isOwner = ownerFlag;
  renderOwnerUI();
}

// initial render
(function init(){
  // ensure welcome screen hidden initially
  screenWelcome.classList.remove('active');
  screenCats.classList.remove('active');
  screenProducts.classList.remove('active');
  renderCategories();
  checkOwnerOnLoad();
})();

// setup global access for HTML onclick handlers
window.openCategory = openCategory;
window.openProductModal = openProductModal;
window.closeProductModal = closeProductModal;
window.openAddModal = openAddModal;
window.closeAddModal = closeAddModal;
window.saveProduct = saveProduct;
window.openPayment = openPayment;
window.closePaymentModal = closePaymentModal;
window.backToCategories = ()=>{ showScreen('screen-categories'); };
window.exitStore = exitStore;

// show/hide welcome screen properly (startup)
showScreen('screen-login');

</script>
</body>
