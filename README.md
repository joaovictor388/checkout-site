<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Checkout</title>
  <script src="https://sdk.mercadopago.com/js/v2"></script>
  <style>
    body { font-family: sans-serif; max-width: 500px; margin: auto; padding: 20px; }
    h2 { text-align: center; }
    .form-group { margin-bottom: 15px; }
    label { display: block; margin-bottom: 5px; }
    input, select { width: 100%; padding: 10px; border-radius: 5px; border: 1px solid #ccc; }
    button { width: 100%; padding: 15px; background-color: #3483fa; color: white; font-size: 16px; border: none; border-radius: 5px; cursor: pointer; }
    .resumo { background: #f9f9f9; padding: 15px; border-radius: 5px; margin-bottom: 20px; }
  </style>
</head>
<body>

  <h2>Finalizar Compra</h2>

  <div class="resumo">
    <p><strong>Produto:</strong> Fone Bluetooth</p>
    <p><strong>Valor:</strong> R$ 199,90</p>
    <p><strong>Frete:</strong> Grátis</p>
    <p><strong>Total:</strong> <span id="total">R$ 199,90</span></p>
  </div>

  <form id="paymentForm">
    <div class="form-group">
      <label for="email">E-mail do comprador</label>
      <input type="email" id="email" name="email" required />
    </div>

    <div class="form-group">
      <label for="paymentMethod">Forma de Pagamento</label>
      <select id="paymentMethod" name="paymentMethod" required>
        <option value="pix">Pix</option>
        <option value="credit_card">Cartão de Crédito</option>
        <option value="boleto">Boleto Bancário</option>
      </select>
    </div>

    <!-- Campos do cartão (visíveis apenas se cartão for selecionado) -->
    <div id="cardData" style="display: none;">
      <div class="form-group">
        <label for="cardNumber">Número do Cartão</label>
        <input type="text" id="cardNumber" />
      </div>
      <div class="form-group">
        <label for="expiration">Validade (MM/AA)</label>
        <input type="text" id="expiration" />
      </div>
      <div class="form-group">
        <label for="cvv">CVV</label>
        <input type="text" id="cvv" />
      </div>
    </div>

    <button type="submit">Pagar</button>
  </form>

  <script>
    const paymentForm = document.getElementById('paymentForm');
    const paymentMethodSelect = document.getElementById('paymentMethod');
    const cardData = document.getElementById('cardData');

    // Exibe campos do cartão apenas se "Cartão" for selecionado
    paymentMethodSelect.addEventListener('change', function () {
      if (this.value === 'credit_card') {
        cardData.style.display = 'block';
      } else {
        cardData.style.display = 'none';
      }
    });

    paymentForm.addEventListener('submit', function (e) {
      e.preventDefault();
      const formData = new FormData(paymentForm);
      const data = Object.fromEntries(formData);

      // Aqui você faria o fetch para criar o pagamento no backend
      alert(`Pagamento com ${data.paymentMethod} iniciado para ${data.email}`);
    });
  </script>

</body>
</html>
