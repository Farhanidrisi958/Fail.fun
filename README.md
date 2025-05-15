# Fail.fun
Spend money 
<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Spend Bill Gates' Money</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f1f2f6;
      margin: 0;
      padding: 20px;
      text-align: center;
    }.money-bar {
  background: #2ecc71;
  color: white;
  font-size: 28px;
  padding: 20px;
  position: sticky;
  top: 0;
  z-index: 1000;
}

.items {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 30px;
}

.item {
  background: white;
  margin: 10px;
  padding: 20px;
  width: 250px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.item img {
  width: 100px;
  height: 100px;
  object-fit: contain;
}

.item h2 {
  font-size: 20px;
  margin: 10px 0 5px;
}

.item .price {
  font-size: 16px;
  color: #555;
}

.controls {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 10px;
}

.controls input {
  width: 50px;
  padding: 5px;
  text-align: center;
}

.controls button {
  padding: 6px 12px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.controls button.sell {
  background-color: #e74c3c;
}

.controls button:hover {
  opacity: 0.9;
}

.quantity {
  font-size: 16px;
  margin-top: 10px;
  color: #2c3e50;
}

  </style>
</head>
<body>
  <div class="money-bar" id="moneyDisplay">$100,000,000,000</div>  <div class="items" id="itemsContainer"></div>  <script>
    let totalMoney = 100000000000;
    let items = [
      { id: "coffee", name: "Coffee", price: 3, img: "https://neal.fun/spend/images/coffee.jpg" },
      { id: "pizza", name: "Pizza", price: 10, img: "https://neal.fun/spend/images/pizza.jpg" },
      { id: "burger", name: "Burger", price: 5, img: "https://neal.fun/spend/images/bigmac.jpg" },
      { id: "tshirt", name: "T-Shirt", price: 20, img: "https://neal.fun/spend/images/tshirt.jpg" },
      { id: "smartphone", name: "Smartphone", price: 1000, img: "https://neal.fun/spend/images/phone.jpg" },
      { id: "laptop", name: "Laptop", price: 1500, img: "https://neal.fun/spend/images/laptop.jpg" },
      { id: "console", name: "Game Console", price: 500, img: "https://neal.fun/spend/images/console.jpg" },
      { id: "bicycle", name: "Bicycle", price: 800, img: "https://neal.fun/spend/images/bike.jpg" },
      { id: "diamondring", name: "Diamond Ring", price: 10000, img: "https://neal.fun/spend/images/diamond.jpg" },
      { id: "rolex", name: "Rolex Watch", price: 15000, img: "https://neal.fun/spend/images/watch.jpg" },
      { id: "hoverboard", name: "Hoverboard", price: 1000, img: "https://neal.fun/spend/images/hoverboard.jpg" },
      { id: "goldentoilet", name: "Golden Toilet", price: 1000000, img: "https://neal.fun/spend/images/toilet.jpg" },
      { id: "dinosaur", name: "Dinosaur Fossil", price: 3000000, img: "https://neal.fun/spend/images/dino.jpg" },
      { id: "tesla", name: "Tesla Car", price: 75000, img: "https://neal.fun/spend/images/tesla.jpg" },
      { id: "lamborghini", name: "Lamborghini", price: 200000, img: "https://neal.fun/spend/images/lamborghini.jpg" },
      { id: "jet", name: "Private Jet", price: 40000000, img: "https://neal.fun/spend/images/jet.jpg" },
      { id: "yacht", name: "Yacht", price: 50000000, img: "https://neal.fun/spend/images/yacht.jpg" },
      { id: "helicopter", name: "Helicopter", price: 18000000, img: "https://neal.fun/spend/images/helicopter.jpg" },
      { id: "house", name: "House", price: 300000, img: "https://neal.fun/spend/images/house.jpg" },
      { id: "island", name: "Private Island", price: 100000000, img: "https://neal.fun/spend/images/island.jpg" }
    ];

    let quantities = {};
    items.forEach(item => quantities[item.id] = 0);

    const itemsContainer = document.getElementById("itemsContainer");

    items.forEach(item => {
      const itemDiv = document.createElement("div");
      itemDiv.className = "item";
      itemDiv.innerHTML = `
        <img src="${item.img}" alt="${item.name}" />
        <h2>${item.name}</h2>
        <p class="price">$${item.price.toLocaleString()}</p>
        <div class="controls">
          <button onclick="buyItem('${item.id}', ${item.price})">Buy</button>
          <input type="number" id="qty-input-${item.id}" value="1" min="1">
          <button class="sell" onclick="sellItem('${item.id}', ${item.price})">Sell</button>
        </div>
        <p class="quantity">Owned: <span id="qty-${item.id}">0</span></p>
      `;
      itemsContainer.appendChild(itemDiv);
    });

    function buyItem(id, price) {
      const qty = parseInt(document.getElementById(`qty-input-${id}`).value);
      const cost = price * qty;
      if (totalMoney >= cost) {
        totalMoney -= cost;
        quantities[id] += qty;
        updateDisplay();
      } else {
        alert("Not enough money!");
      }
    }

    function sellItem(id, price) {
      const qty = parseInt(document.getElementById(`qty-input-${id}`).value);
      if (quantities[id] >= qty) {
        totalMoney += price * qty;
        quantities[id] -= qty;
        updateDisplay();
      } else {
        alert("You don't own that many to sell!");
      }
    }

    function updateDisplay() {
      document.getElementById("moneyDisplay").innerText = `$${totalMoney.toLocaleString()}`;
      items.forEach(item => {
        document.getElementById(`qty-${item.id}`).innerText = quantities[item.id];
      });
    }
  </script></body>
</html>
