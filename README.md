<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta content="width=device-width, initial-scale=1.0" name="viewport" />
    <title>Mini Ecommerce</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css"
      rel="stylesheet"
    />
  </head>
  <body class="bg-gray-100">
    <div class="container mx-auto p-4">
      <!-- Header -->
      <div class="flex justify-between items-center mb-4">
        <h1 class="text-xl font-bold">Mini Ecommerce</h1>
        <div class="flex items-center space-x-2">
          <input
            id="search-input"
            class="border border-gray-300 rounded p-2"
            placeholder="all"
            type="text"
          />
          <button
            id="search-button"
            class="bg-green-500 text-white px-4 py-2 rounded"
          >
            Search
          </button>
          <button
            class="bg-purple-500 text-white px-4 py-2 rounded"
            id="cart-button"
          >
            <i class="fas fa-shopping-cart"></i> <span id="cart-count">0</span>
          </button>
        </div>
      </div>
      <!-- Products -->
      <div
        id="product-list"
        class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4"
      >
        <!-- Product 1 -->
        <div
          class="bg-white p-4 rounded shadow product"
          data-product-name="Keyboard Logitek"
        >
          <img
            alt="Keyboard Logitech"
            class="w-full h-48 object-cover mb-4"
            height="200"
            src="https://storage.googleapis.com/a1aa/image/4FyXjilePOVQPyZXzySgrSh9ewRTe9snM9Qu7IXnlBAWMUunA.jpg"
            width="300"
          />
          <h2 class="text-lg font-bold mb-2">Keyboard Logitek</h2>
          <p class="text-gray-600 mb-2">Keyboard yang mantap untuk kantoran</p>
          <p class="text-gray-800 font-bold mb-4">Rp 60.000,00</p>
          <button
            class="bg-purple-500 text-white px-4 py-2 rounded add-to-cart"
            data-product-id="1"
          >
            Add To Cart
          </button>
          <button
            class="bg-red-500 text-white px-4 py-2 rounded remove-from-cart hidden"
            data-product-id="1"
          >
            Remove From Cart
          </button>
        </div>
        <!-- Product 2 -->
        <div
          class="bg-white p-4 rounded shadow product"
          data-product-name="Keyboard MSI"
        >
          <img
            alt="Keyboard MSI"
            class="w-full h-48 object-cover mb-4"
            height="200"
            src="https://storage.googleapis.com/a1aa/image/jIk9LcohwloeOKrep6XEwwyWPd5mcprZ086wWG1ud3YJGK3TA.jpg"
            width="300"
          />
          <h2 class="text-lg font-bold mb-2">Keyboard MSI</h2>
          <p class="text-gray-600 mb-2">Keyboard gaming MSI mekanik</p>
          <p class="text-gray-800 font-bold mb-4">Rp 300.000,00</p>
          <button
            class="bg-purple-500 text-white px-4 py-2 rounded add-to-cart"
            data-product-id="2"
          >
            Add To Cart
          </button>
          <button
            class="bg-red-500 text-white px-4 py-2 rounded remove-from-cart hidden"
            data-product-id="2"
          >
            Remove From Cart
          </button>
        </div>
        <!-- Product 3 -->
        <div
          class="bg-white p-4 rounded shadow product"
          data-product-name="Mouse Genius"
        >
          <img
            alt="Mouse Genius"
            class="w-full h-48 object-cover mb-4"
            height="200"
            src="genius.jpg"
            width="300"
          />
          <h2 class="text-lg font-bold mb-2">Mouse Genius</h2>
          <p class="text-gray-600 mb-2">Mouse Genius biar lebih pinter</p>
          <p class="text-gray-800 font-bold mb-4">Rp 50.000,00</p>
          <button
            class="bg-purple-500 text-white px-4 py-2 rounded add-to-cart"
            data-product-id="3"
          >
            Add To Cart
          </button>
          <button
            class="bg-red-500 text-white px-4 py-2 rounded remove-from-cart hidden"
            data-product-id="3"
          >
            Remove From Cart
          </button>
        </div>
        <!-- Product 4 -->
        <div
          class="bg-white p-4 rounded shadow product"
          data-product-name="Mouse"
        >
          <img
            alt="Mouse"
            class="w-full h-48 object-cover mb-4"
            height="200"
            src="jerry.jpg"
            width="300"
          />
          <h2 class="text-lg font-bold mb-2">Mouse Jerry</h2>
          <p class="text-gray-600 mb-2">Mouse yang nyaman untuk digunakan</p>
          <p class="text-gray-800 font-bold mb-4">Rp 70.000,00</p>
          <button
            class="bg-purple-500 text-white px-4 py-2 rounded add-to-cart"
            data-product-id="4"
          >
            Add To Cart
          </button>
          <button
            class="bg-red-500 text-white px-4 py-2 rounded remove-from-cart hidden"
            data-product-id="4"
          >
            Remove From Cart
          </button>
        </div>
      </div>
    </div>
    <script>
      document.addEventListener("DOMContentLoaded", function () {
        const cart = new Set();
        const cartCountElement = document.getElementById("cart-count");
        const searchButton = document.getElementById("search-button");
        const searchInput = document.getElementById("search-input");
        const productList = document.getElementById("product-list");
        const products = document.querySelectorAll(".product");

        function updateCartCount() {
          cartCountElement.textContent = cart.size;
        }

        function filterProducts() {
          const searchTerm = searchInput.value.toLowerCase();
          products.forEach((product) => {
            const productName = product
              .getAttribute("data-product-name")
              .toLowerCase();
            if (productName.includes(searchTerm)) {
              product.classList.remove("hidden");
            } else {
              product.classList.add("hidden");
            }
          });
        }

        document.querySelectorAll(".add-to-cart").forEach((button) => {
          button.addEventListener("click", function () {
            const productId = this.getAttribute("data-product-id");
            cart.add(productId);
            this.classList.add("hidden");
            this.nextElementSibling.classList.remove("hidden");
            updateCartCount();
          });
        });

        document.querySelectorAll(".remove-from-cart").forEach((button) => {
          button.addEventListener("click", function () {
            const productId = this.getAttribute("data-product-id");
            cart.delete(productId);
            this.classList.add("hidden");
            this.previousElementSibling.classList.remove("hidden");
            updateCartCount();
          });
        });

        searchButton.addEventListener("click", filterProducts);
        searchInput.addEventListener("input", filterProducts);
      });
    </script>
  </body>
</html>

