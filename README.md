<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <title>RemboStore_ | Top Up Instan</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background-color: #f5f6fa;
    }

    header {
      background-color: #ff6600;
      padding: 1rem 2rem;
      color: #fff;
      display: flex;
      align-items: center;
      gap: 1rem;
    }

    header img {
      height: 40px;
    }

    header h1 {
      margin: 0;
      font-size: 1.5rem;
    }

    .container {
      max-width: 600px;
      margin: auto;
      padding: 1.5rem;
    }

    .section {
      background: white;
      border-radius: 8px;
      padding: 1.5rem;
      margin-bottom: 1rem;
      box-shadow: 0 2px 10px rgba(0,0,0,0.05);
    }

    .section h2 {
      margin-top: 0;
      font-size: 1.2rem;
      color: #333;
    }

    .products, .options {
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
    }

    .product, .option {
      flex: 1 1 45%;
      background: #f2f2f2;
      padding: 1rem;
      border-radius: 8px;
      text-align: center;
      cursor: pointer;
      transition: background 0.2s;
      border: 2px solid transparent;
    }

    .product:hover, .option:hover {
      background: #e6e6e6;
    }

    .selected {
      border-color: #ff6600;
      background: #fff3e0;
    }

    .form-group {
      margin-top: 1rem;
    }

    input, select, button {
      width: 100%;
      padding: 0.75rem;
      margin-top: 0.3rem;
      border-radius: 6px;
      border: 1px solid #ccc;
      font-size: 1rem;
    }

    button {
      background: #ff6600;
      color: white;
      border: none;
      cursor: pointer;
      margin-top: 1rem;
      font-weight: bold;
    }

    button:hover {
      background: #e65c00;
    }

    #priceBox {
      margin-top: 1rem;
      font-weight: bold;
      color: #ff6600;
    }
  </style>
</head>
<body>

<header>
  <img src="https://via.placeholder.com/40x40" alt="Logo">
  <h1>RemboStore_</h1>
</header>

<div class="container">
  <div class="section">
    <h2>Pilih Produk</h2>
    <div class="products" id="productList"></div>
  </div>

  <div class="section" id="optionSection" style="display:none;">
    <h2>Pilih Paket/Nominal</h2>
    <div class="options" id="optionList"></div>
    <div id="priceBox"></div>
  </div>

  <div class="section">
    <h2>Nama Pembeli</h2>
    <input type="text" id="buyerName" placeholder="Contoh: Andi" />
  </div>

  <div class="section">
    <h2>Metode Pembayaran</h2>
    <select id="payment">
      <option value="DANA">DANA</option>
      <option value="GoPay">GoPay</option>
      <option value="OVO">OVO</option>
      <option value="Transfer Bank">Transfer Bank</option>
    </select>
  </div>

  <div class="section">
    <h2>Checkout</h2>
    <button onclick="checkout()">Beli Sekarang</button>
  </div>
</div>

<script>
  const products = [
    {
      name: 'Alight Motion',
      options: [
        { label: '1 Bulan', price: 10000 },
        { label: '1 Tahun', price: 25000 },
      ]
    },
    {
      name: 'Canva Pro',
      options: [
        { label: '1 Bulan', price: 5000 },
        { label: 'Lifetime', price: 20000 },
      ]
    },
    {
      name: 'Instagram Followers',
      options: [
        { label: '500 Followers', price: 15000 },
        { label: '1000 Followers', price: 25000 },
      ]
    }
  ];

  let selectedProduct = null;
  let selectedOption = null;

  const productList = document.getElementById('productList');
  const optionSection = document.getElementById('optionSection');
  const optionList = document.getElementById('optionList');
  const priceBox = document.getElementById('priceBox');

  function renderProducts() {
    products.forEach((p, i) => {
      const div = document.createElement('div');
      div.className = 'product';
      div.innerText = p.name;
      div.onclick = () => selectProduct(p, div);
      productList.appendChild(div);
    });
  }

  function selectProduct(product, element) {
    selectedProduct = product;
    selectedOption = null;

    document.querySelectorAll('.product').forEach(el => el.classList.remove('selected'));
    element.classList.add('selected');

    renderOptions(product.options);
  }

  function renderOptions(options) {
    optionList.innerHTML = '';
    priceBox.innerHTML = '';
    optionSection.style.display = 'block';

    options.forEach(opt => {
      const div = document.createElement('div');
      div.className = 'option';
      div.innerText = `${opt.label}`;
      div.onclick = () => selectOption(opt, div);
      optionList.appendChild(div);
    });
  }

  function selectOption(option, element) {
    selectedOption = option;

    document.querySelectorAll('.option').forEach(el => el.classList.remove('selected'));
    element.classList.add('selected');

    priceBox.innerHTML = `Harga: Rp ${option.price.toLocaleString('id-ID')}`;
  }

  function checkout() {
    const buyer = document.getElementById('buyerName').value;
    const payment = document.getElementById('payment').value;

    if (!selectedProduct || !selectedOption || !buyer) {
      alert('Harap lengkapi semua data!');
      return;
    }

    const message = `Halo, saya ingin membeli:\nProduk: ${selectedProduct.name}\nPaket: ${selectedOption.label}\nHarga: Rp${selectedOption.price.toLocaleString('id-ID')}\nNama: ${buyer}\nMetode Pembayaran: ${payment}`;
    const wa = '6281234567890'; // Ganti dengan nomormu
    const url = `https://wa.me/${wa}?text=${encodeURIComponent(message)}`;
    window.open(url, '_blank');
  }

  renderProducts();
</script>

</body>
</html>
