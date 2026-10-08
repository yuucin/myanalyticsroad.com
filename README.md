# MyAnalyticsRoad.com
<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GTM Test E-Ticaret Mağazası</title>

  <!-- ========================================================= -->
  <!-- 1. GOOGLE TAG MANAGER (HEAD) KODUNU BURAYA YAPIŞTIRIN -->
  <!-- ========================================================= -->
  <!-- <script>(function(w,d,s,l,i)...</script> -->

  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 20px; background-color: #f4f4f9; color: #333; }
    header { background: #1a73e8; color: white; padding: 15px 20px; border-radius: 8px; margin-bottom: 20px; display: flex; justify-content: space-between; align-items: center; }
    .container { max-width: 1000px; margin: 0 auto; }
    .products { display: flex; gap: 20px; flex-wrap: wrap; margin-bottom: 30px; }
    .card { background: white; border: 1px solid #ddd; border-radius: 8px; padding: 15px; width: 200px; text-align: center; box-shadow: 0 2px 4px rgba(0,0,0,0.05); }
    .card img { max-width: 100%; height: 120px; object-fit: cover; border-radius: 4px; }
    .price { font-weight: bold; color: #2e7d32; margin: 10px 0; }
    button { background: #1a73e8; color: white; border: none; padding: 10px 15px; border-radius: 4px; cursor: pointer; font-size: 14px; }
    button:hover { background: #1557b0; }
    .cart-section, .form-section { background: white; padding: 20px; border-radius: 8px; margin-bottom: 20px; border: 1px solid #ddd; }
    input { width: 100%; padding: 8px; margin: 8px 0 15px 0; box-sizing: border-box; border: 1px solid #ccc; border-radius: 4px; }
    footer { text-align: center; margin-top: 40px; color: #777; font-size: 12px; }
  </style>
</head>
<body>

  <!-- ========================================================= -->
  <!-- 2. GOOGLE TAG MANAGER (BODY - NOSCRIPT) BURAYA YAPIŞTIRIN -->
  <!-- ========================================================= -->
  <!-- <noscript><iframe src="https://www.googletagmanager.com/ns.html..."></noscript> -->

  <div class="container">
    <header>
      <h1>GTM Test Mağazası</h1>
      <div>Sepetteki Ürün: <span id="cart-count">0</span></div>
    </header>

    <h2>Öne Çıkan Ürünler</h2>
    <div class="products">
      
      <!-- Ürün 1 -->
      <div class="card" data-id="p101" data-name="Kablosuz Kulaklık" data-price="750">
        <img src="https://via.placeholder.com/150?text=Kulaklik" alt="Kablosuz Kulaklık">
        <h3>Kablosuz Kulaklık</h3>
        <p class="price">750 TL</p>
        <button class="add-to-cart-btn" onclick="addToCart('p101', 'Kablosuz Kulaklık', 750)">Sepete Ekle</button>
      </div>

      <!-- Ürün 2 -->
      <div class="card" data-id="p102" data-name="Akıllı Saat" data-price="1200">
        <img src="https://via.placeholder.com/150?text=Akilli+Saat" alt="Akıllı Saat">
        <h3>Akıllı Saat</h3>
        <p class="price">1200 TL</p>
        <button class="add-to-cart-btn" onclick="addToCart('p102', 'Akıllı Saat', 1200)">Sepete Ekle</button>
      </div>

      <!-- Ürün 3 -->
      <div class="card" data-id="p103" data-name="Mekanik Klavye" data-price="1500">
        <img src="https://via.placeholder.com/150?text=Klavye" alt="Mekanik Klavye">
        <h3>Mekanik Klavye</h3>
        <p class="price">1500 TL</p>
        <button class="add-to-cart-btn" onclick="addToCart('p103', 'Mekanik Klavye', 1500)">Sepete Ekle</button>
      </div>

    </div>

    <!-- Ödeme / Satın Alma Simülasyonu -->
    <div class="cart-section">
      <h2>Siparişi Tamamla</h2>
      <p>Toplam Tutar: <strong id="total-price">0</strong> TL</p>
      <button id="btn-checkout" onclick="completePurchase()">Satın Almayı Tamamla</button>
    </div>

    <!-- Bülten ve İletişim Formu (Form Submission Testi İçin) -->
    <div class="form-section">
      <h2>İndirim Kuponu Alın (Form Testi)</h2>
      <form id="newsletter-form" onsubmit="handleFormSubmit(event)">
        <label for="email">E-Posta Adresiniz:</label>
        <input type="email" id="email" name="user_email" placeholder="ornek@email.com" required>
        <button type="submit" id="btn-submit-form">Kupon Gönder</button>
      </form>
    </div>

    <footer>
      <p>GTM Eğitimi ve Pratik Testleri İçin Hazırlanmıştır.</p>
    </footer>
  </div>

  <!-- JavaScript ile dataLayer Simülasyonları -->
  <script>
    // dataLayer Dizisini Başlatıyoruz
    window.dataLayer = window.dataLayer || [];

    let cartTotal = 0;
    let itemCount = 0;

    // 1. Sepete Ekleme Fonksiyonu (E-commerce add_to_cart event'i)
    function addToCart(id, name, price) {
      cartTotal += price;
      itemCount += 1;

      document.getElementById('cart-count').innerText = itemCount;
      document.getElementById('total-price').innerText = cartTotal;

      // GTM dataLayer'a e-ticaret olayı gönderme
      window.dataLayer.push({
        'event': 'add_to_cart',
        'ecommerce': {
          'currency': 'TRY',
          'value': price,
          'items': [{
            'item_id': id,
            'item_name': name,
            'price': price,
            'quantity': 1
          }]
        }
      });

      alert(name + " sepete eklendi!");
    }

    // 2. Satın Alma Fonksiyonu (E-commerce purchase event'i)
    function completePurchase() {
      if (cartTotal === 0) {
        alert("Sepetiniz boş! Önce ürün ekleyin.");
        return;
      }

      const transactionId = 'T-' + Math.floor(100000 + Math.random() * 900000);

      // GTM dataLayer'a satın alma olayı gönderme
      window.dataLayer.push({
        'event': 'purchase',
        'ecommerce': {
          'transaction_id': transactionId,
          'value': cartTotal,
          'currency': 'TRY',
          'tax': cartTotal * 0.20,
          'shipping': 29.99
        }
      });

      alert("Sipariş alındı! Sipariş No: " + transactionId);
      
      // Sıfırla
      cartTotal = 0;
      itemCount = 0;
      document.getElementById('cart-count').innerText = 0;
      document.getElementById('total-price').innerText = 0;
    }

    // 3. Form Gönderim Fonksiyonu
    function handleFormSubmit(event) {
      event.preventDefault();
      const email = document.getElementById('email').value;

      // Özel dataLayer Event'i Fırlatma
      window.dataLayer.push({
        'event': 'lead_form_submit',
        'form_name': 'Newsletter Discount',
        'user_email_domain': email.split('@')[1] || ''
      });

      alert("Kupon e-posta adresinize gönderildi!");
      document.getElementById('newsletter-form').reset();
    }
  </script>

</body>
</html>
