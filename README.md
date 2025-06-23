<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chilmari E-shop</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Toast Notification CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/toastify-js/src/toastify.min.css">
    <style>
        .section { display: none; }
        .active-section { display: block; }
        .active-nav { color: #f97316; }
        .product-card:hover { transform: translateY(-5px); transition: all 0.3s; }
        .order-card { border-left: 4px solid #f97316; }
        .quantity-btn { width: 25px; height: 25px; display: flex; align-items: center; justify-content: center; }
    </style>
</head>
<body class="bg-gray-100 pb-16">
    <!-- Header with Search -->
    <header class="bg-orange-500 text-white p-4 sticky top-0 z-10">
        <div class="container mx-auto flex items-center">
            <div class="w-10 h-10 mr-2 bg-white rounded-full flex items-center justify-center">
                <span class="text-orange-500 font-bold">CE</span>
            </div>
            <div class="flex-1 relative">
                <input type="text" id="search-input" placeholder="Search products..."
                       class="w-full py-2 px-4 rounded text-gray-800 text-sm">
                <button onclick="searchProducts()" class="absolute right-0 top-0 h-full px-4 bg-orange-600 rounded-r">
                    🔍
                </button>
            </div>
            <div class="ml-4 relative" onclick="showSection('cart')">
                <span id="cart-count" class="absolute -top-2 -right-2 bg-red-500 text-white text-xs rounded-full w-5 h-5 flex items-center justify-center hidden">0</span>
                🛒
            </div>
        </div>
    </header>

    <!-- Main Content Sections -->
    <main>
        <!-- Home Section -->
        <section id="home-section" class="section active-section">
            <!-- Categories -->
            <div class="container mx-auto p-4 bg-white shadow-sm">
                <h2 class="text-lg font-bold mb-2">Categories</h2>
                <div class="grid grid-cols-4 gap-2">
                    <div class="category-item text-center p-2" onclick="loadProducts('electronics')">
                        <div class="bg-gray-200 rounded-full w-12 h-12 mx-auto mb-1 flex items-center justify-center">
                            📱
                        </div>
                        <span class="text-xs">Electronics</span>
                    </div>
                    <div class="category-item text-center p-2" onclick="loadProducts('clothing')">
                        <div class="bg-gray-200 rounded-full w-12 h-12 mx-auto mb-1 flex items-center justify-center">
                            👕
                        </div>
                        <span class="text-xs">Clothing</span>
                    </div>
                    <div class="category-item text-center p-2" onclick="loadProducts('grocery')">
                        <div class="bg-gray-200 rounded-full w-12 h-12 mx-auto mb-1 flex items-center justify-center">
                            🛒
                        </div>
                        <span class="text-xs">Grocery</span>
                    </div>
                    <div class="category-item text-center p-2" onclick="loadProducts('household')">
                        <div class="bg-gray-200 rounded-full w-12 h-12 mx-auto mb-1 flex items-center justify-center">
                            🏠
                        </div>
                        <span class="text-xs">Household</span>
                    </div>
                </div>
            </div>

            <!-- Products -->
            <div class="container mx-auto p-4">
                <div class="flex justify-between items-center mb-4">
                    <h2 class="text-lg font-bold">Featured Products</h2>
                    <div class="text-sm">
                        <span id="current-category">All</span>
                    </div>
                </div>
                <div id="products-container" class="grid grid-cols-2 gap-4">
                    <!-- Products will be loaded here -->
                </div>
            </div>
        </section>

        <!-- Product View Section -->
        <section id="product-view-section" class="section">
            <div class="container mx-auto p-4">
                <button onclick="goBack()" class="mb-4 flex items-center text-orange-500">
                    <svg class="w-5 h-5 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18"></path>
                    </svg>
                    Back
                </button>
               
                <div class="bg-white rounded-lg shadow overflow-hidden">
                    <div class="h-64 bg-gray-200">
                        <img id="product-view-image" src="" alt="" class="w-full h-full object-cover">
                    </div>
                   
                    <div class="p-4">
                        <h2 id="product-view-name" class="text-xl font-bold mb-2"></h2>
                        <p id="product-view-price" class="text-orange-500 text-xl font-bold mb-4"></p>
                        <p id="product-view-description" class="text-gray-600 mb-4"></p>
                       
                        <div class="flex space-x-2">
                            <button onclick="addToCartFromView()"
                                    class="flex-1 bg-orange-500 text-white py-2 px-4 rounded hover:bg-orange-600">
                                Add to Cart
                            </button>
                            <button onclick="buyNowFromView()"
                                    class="flex-1 bg-green-500 text-white py-2 px-4 rounded hover:bg-green-600">
                                Buy Now
                            </button>
                        </div>
                    </div>
                </div>
               
                <div class="mt-6 bg-white rounded-lg shadow p-4">
                    <h3 class="font-bold mb-2">Product Details</h3>
                    <div id="product-view-details" class="text-sm text-gray-600">
                        <!-- Additional details will be loaded here -->
                    </div>
                </div>
            </div>
        </section>

        <!-- Cart Section -->
        <section id="cart-section" class="section">
            <div class="container mx-auto p-4">
                <h2 class="text-lg font-bold mb-4">Your Cart</h2>
                <div id="cart-items">
                    <p class="text-center text-gray-500 py-8">Your cart is empty</p>
                </div>
                <div class="mt-4 p-4 bg-white rounded shadow">
                    <h3 class="font-bold mb-2">Order Summary</h3>
                    <div class="flex justify-between mb-1">
                        <span>Subtotal:</span>
                        <span id="cart-subtotal">৳0</span>
                    </div>
                    <div class="flex justify-between mb-1">
                        <span>Delivery:</span>
                        <span>৳50</span>
                    </div>
                    <div class="flex justify-between font-bold mt-2">
                        <span>Total:</span>
                        <span id="cart-total">৳50</span>
                    </div>
                    <button onclick="showSection('checkout')" class="mt-4 w-full bg-orange-500 text-white py-2 rounded">
                        Proceed to Checkout
                    </button>
                </div>
            </div>
        </section>

        <!-- Checkout Section -->
        <section id="checkout-section" class="section">
            <div class="container mx-auto p-4">
                <button onclick="showSection('cart')" class="mb-4 flex items-center text-orange-500">
                    <svg class="w-5 h-5 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18"></path>
                    </svg>
                    Back to Cart
                </button>
               
                <div class="bg-white rounded shadow p-4 mb-4">
                    <h2 class="text-lg font-bold mb-4">Delivery Information</h2>
                    <form id="delivery-form">
                        <div class="mb-3">
                            <label class="block text-sm font-medium mb-1">Full Name</label>
                            <input type="text" required class="w-full p-2 border rounded"
                                   pattern="[A-Za-z ]{3,}" title="Please enter at least 3 characters">
                        </div>
                        <div class="mb-3">
                            <label class="block text-sm font-medium mb-1">Phone Number</label>
                            <input type="tel" required class="w-full p-2 border rounded"
                                   pattern="01[3-9]\d{8}" title="Please enter a valid Bangladeshi phone number">
                        </div>
                        <div class="mb-3">
                            <label class="block text-sm font-medium mb-1">Delivery Address</label>
                            <textarea required class="w-full p-2 border rounded" rows="3" minlength="10"></textarea>
                        </div>
                        <div class="mb-3">
                            <label class="block text-sm font-medium mb-1">Delivery Area</label>
                            <select class="w-full p-2 border rounded" disabled>
                                <option>Chilmari Only</option>
                            </select>
                        </div>
                    </form>
                </div>
               
                <div class="bg-white rounded shadow p-4 mb-4">
                    <h2 class="text-lg font-bold mb-4">Payment Method</h2>
                    <div class="space-y-3">
                        <div class="flex items-center">
                            <input type="radio" id="cod" name="payment" value="cod" checked class="mr-2">
                            <label for="cod" class="flex items-center">
                                <span class="bg-gray-200 p-1 rounded mr-2">💰</span>
                                Cash on Delivery (COD)
                            </label>
                        </div>
                        <div class="flex items-center">
                            <input type="radio" id="bkash" name="payment" value="bkash" class="mr-2">
                            <label for="bkash" class="flex items-center">
                                <span class="bg-green-100 p-1 rounded mr-2">💳</span>
                                bKash Payment
                            </label>
                        </div>
                        <div id="bkash-details" class="hidden pl-6 mt-2">
                            <div class="mb-2">
                                <p class="text-sm">Send money to: <span class="font-bold">01770706309</span></p>
                            </div>
                            <div class="mb-2">
                                <label class="block text-sm font-medium mb-1">bKash Transaction ID</label>
                                <input type="text" class="w-full p-2 border rounded" pattern="\d{10}" title="Please enter 10 digit transaction ID">
                            </div>
                        </div>
                    </div>
                </div>
               
                <div class="bg-white rounded shadow p-4">
                    <h2 class="text-lg font-bold mb-4">Order Summary</h2>
                    <div id="checkout-items" class="mb-3">
                        <!-- Items will be loaded here -->
                    </div>
                    <div class="border-t pt-3">
                        <div class="flex justify-between mb-1">
                            <span>Subtotal:</span>
                            <span id="checkout-subtotal">৳0</span>
                        </div>
                        <div class="flex justify-between mb-1">
                            <span>Delivery:</span>
                            <span>৳50</span>
                        </div>
                        <div class="flex justify-between font-bold mt-2">
                            <span>Total:</span>
                            <span id="checkout-total">৳50</span>
                        </div>
                    </div>
                    <button onclick="placeOrder()" class="mt-4 w-full bg-orange-500 text-white py-2 rounded">
                        Place Order
                    </button>
                </div>
            </div>
        </section>

        <!-- Orders Section -->
        <section id="orders-section" class="section">
            <div class="container mx-auto p-4">
                <h2 class="text-lg font-bold mb-4">Your Orders</h2>
                <div id="orders-list">
                    <!-- Orders will be loaded here -->
                    <p class="text-center text-gray-500 py-8">No orders yet</p>
                </div>
            </div>
        </section>

        <!-- Account Section -->
        <section id="account-section" class="section">
            <div class="container mx-auto p-4">
                <h2 class="text-lg font-bold mb-4">Your Account</h2>
                <div id="user-info" class="bg-white p-4 rounded shadow">
                    <!-- User info will be loaded here -->
                    <p>Please login to view your account</p>
                    <button onclick="showLoginForm()" class="mt-2 bg-orange-500 text-white py-1 px-3 rounded text-sm">
                        Login
                    </button>
                </div>
            </div>
        </section>
    </main>

    <!-- Bottom Navigation -->
    <nav class="fixed bottom-0 left-0 right-0 bg-white shadow-lg flex justify-around items-center p-3">
        <a href="#" class="text-center text-orange-500 active-nav" onclick="showSection('home')">
            <div class="w-6 h-6 mx-auto">🏠</div>
            <span class="text-xs">Home</span>
        </a>
        <a href="#" class="text-center text-gray-600" onclick="showSection('cart')">
            <div class="w-6 h-6 mx-auto">🛒</div>
            <span class="text-xs">Cart</span>
        </a>
        <a href="#" class="text-center text-gray-600" onclick="showSection('orders')">
            <div class="w-6 h-6 mx-auto">📦</div>
            <span class="text-xs">Orders</span>
        </a>
        <a href="#" class="text-center text-gray-600" onclick="showSection('account')">
            <div class="w-6 h-6 mx-auto">👤</div>
            <span class="text-xs">Account</span>
        </a>
    </nav>

    <!-- Support Floating Button - Fixed WhatsApp Button -->
    <div class="fixed bottom-16 right-4 z-20">
        <a href="https://wa.me/8801945312372"
           target="_blank"
           class="bg-green-500 text-white rounded-full p-3 shadow-lg block"
           onclick="window.open('https://wa.me/8801945312372', '_blank')">
            💬
        </a>
    </div>

    <!-- Toast Notification JS -->
    <script src="https://cdn.jsdelivr.net/npm/toastify-js"></script>
   
    <script>
        // Sample Product Data with more items
        const sampleProducts = {
            electronics: [
                {
                    id: "e1",
                    name: "Smartphone X3",
                    price: 15500,
                    image: "https://m.media-amazon.com/images/I/61L1ItFgFHL._SL1500_.jpg",
                    description: "6.5 inch display, 128GB storage",
                    details: "Brand: XYZ\nModel: X3\nColor: Black\nRAM: 6GB\nStorage: 128GB\nBattery: 5000mAh"
                },
                {
                    id: "e2",
                    name: "Wireless Earbuds",
                    price: 1200,
                    image: "https://m.media-amazon.com/images/I/51RBk3kAq5L._SL1500_.jpg",
                    description: "Bluetooth 5.0, 20 hours battery",
                    details: "Brand: SoundPlus\nBluetooth Version: 5.0\nBattery Life: 20 hours\nCharging Time: 2 hours\nWater Resistance: IPX4"
                },
                {
                    id: "e3",
                    name: "Power Bank 10000mAh",
                    price: 800,
                    image: "https://m.media-amazon.com/images/I/61GIxXleO9L._SL1500_.jpg",
                    description: "Fast charging, dual USB ports",
                    details: "Capacity: 10000mAh\nInput: 5V/2A\nOutput: 5V/2.1A\nPorts: 2 USB\nLED Indicator: Yes"
                },
                {
                    id: "e4",
                    name: "Smart Watch",
                    price: 2500,
                    image: "https://m.media-amazon.com/images/I/61XDeOOr0RL._SL1500_.jpg",
                    description: "Heart rate monitor, waterproof",
                    details: "Display: 1.4\" Touchscreen\nBattery: 7 days\nWaterproof: IP68\nSensors: Heart rate, steps\nCompatibility: Android/iOS"
                }
            ],
            clothing: [
                {
                    id: "c1",
                    name: "Men's T-Shirt",
                    price: 350,
                    image: "https://m.media-amazon.com/images/I/61-jAhtF86L._AC_UL1500_.jpg",
                    description: "100% cotton, regular fit",
                    details: "Material: 100% Cotton\nFit: Regular\nSleeve: Short\nColor: Black\nCare: Machine wash"
                },
                {
                    id: "c2",
                    name: "Women's Scarf",
                    price: 250,
                    image: "https://m.media-amazon.com/images/I/71sx7+-qJ5L._AC_UL1500_.jpg",
                    description: "Soft fabric, stylish design",
                    details: "Material: Polyester\nDimensions: 70\" x 28\"\nPattern: Floral\nSeason: All season\nCare: Hand wash"
                },
                {
                    id: "c3",
                    name: "Kids Jacket",
                    price: 600,
                    image: "https://m.media-amazon.com/images/I/71Qn8Y+QmJL._AC_UL1500_.jpg",
                    description: "Winter jacket, warm material",
                    details: "Material: Polyester\nLining: Fleece\nClosure: Zipper\nPockets: 2\nAge: 5-7 years"
                },
                {
                    id: "c4",
                    name: "Saree",
                    price: 1200,
                    image: "https://m.media-amazon.com/images/I/81VJZ+8X1YL._AC_UL1500_.jpg",
                    description: "Traditional Bangladeshi saree",
                    details: "Fabric: Cotton Silk\nBlouse: Included\nLength: 5.5 meters\nWork: Embroidery\nOccasion: Wedding/Festival"
                }
            ],
            grocery: [
                {
                    id: "g1",
                    name: "Pure Mustard Oil",
                    price: 180,
                    image: "https://m.media-amazon.com/images/I/71YHblzCgVL._SL1500_.jpg",
                    description: "1 liter, 100% pure",
                    details: "Brand: PureGold\nQuantity: 1 liter\nType: Cold Pressed\nShelf Life: 12 months\nOrigin: Bangladesh"
                },
                {
                    id: "g2",
                    name: "Basmati Rice",
                    price: 95,
                    image: "https://m.media-amazon.com/images/I/81W+0XwuJVL._SL1500_.jpg",
                    description: "5kg pack, premium quality",
                    details: "Brand: Aromatic\nQuantity: 5kg\nType: Basmati\nGrain Length: Extra Long\nAge: New Crop"
                },
                {
                    id: "g3",
                    name: "Honey",
                    price: 300,
                    image: "https://m.media-amazon.com/images/I/71RMuOKN3VL._SL1500_.jpg",
                    description: "Pure natural honey, 500gm",
                    details: "Brand: Nature's Gift\nQuantity: 500gm\nType: Forest Honey\nPurity: 100%\nBenefits: Immunity Booster"
                },
                {
                    id: "g4",
                    name: "Spices Pack",
                    price: 150,
                    image: "https://m.media-amazon.com/images/I/81d5OrW-AQL._SL1500_.jpg",
                    description: "5 essential spices",
                    details: "Contents: Turmeric, Cumin, Coriander, Chili, Garam Masala\nQuantity: 100gm each\nOrigin: Bangladesh\nPackaging: Airtight\nShelf Life: 12 months"
                }
            ],
            household: [
                {
                    id: "h1",
                    name: "Non-Stick Pan",
                    price: 650,
                    image: "https://m.media-amazon.com/images/I/71UGB5x3VQL._SL1500_.jpg",
                    description: "24cm, durable coating",
                    details: "Diameter: 24cm\nMaterial: Aluminum\nCoating: Ceramic\nHandle: Heat Resistant\nInduction Compatible: Yes"
                },
                {
                    id: "h2",
                    name: "Broom Stick",
                    price: 120,
                    image: "https://m.media-amazon.com/images/I/71yV5vZKKoL._SL1500_.jpg",
                    description: "Strong bristles, wooden handle",
                    details: "Bristle Material: Plastic\nHandle Material: Wood\nLength: 120cm\nType: Indoor/Outdoor\nColor: Brown"
                },
                {
                    id: "h3",
                    name: "Water Purifier",
                    price: 2500,
                    image: "https://m.media-amazon.com/images/I/71Q4+JQ2i4L._SL1500_.jpg",
                    description: "5 stage filtration",
                    details: "Stages: 5\nCapacity: 10 liters\nTechnology: RO+UV+UF\nInstallation: Counter Top\nWarranty: 1 year"
                },
                {
                    id: "h4",
                    name: "Storage Box Set",
                    price: 800,
                    image: "https://m.media-amazon.com/images/I/71XgNp3XZVL._SL1500_.jpg",
                    description: "5 pieces plastic box set",
                    details: "Number of Pieces: 5\nMaterial: Food Grade Plastic\nLids: Airtight\nStackable: Yes\nColors: Assorted"
                }
            ]
        };

        // Current state with localStorage support
        let currentCategory = localStorage.getItem('currentCategory') || 'electronics';
        let cart = JSON.parse(localStorage.getItem('cart')) || [];
        let currentProduct = null;

        // Load products function
        function loadProducts(category) {
            currentCategory = category;
            localStorage.setItem('currentCategory', category);
            document.getElementById('current-category').textContent =
                category.charAt(0).toUpperCase() + category.slice(1);
           
            const productsContainer = document.getElementById('products-container');
            productsContainer.innerHTML = '';
           
            const products = sampleProducts[category];
           
            if (!products || products.length === 0) {
                productsContainer.innerHTML = `
                    <div class="col-span-2 text-center text-gray-500 py-8">
                        No products found in this category
                    </div>
                `;
                return;
            }
           
            products.forEach(product => {
                const productCard = `
                    <div class="product-card bg-white rounded-lg shadow overflow-hidden">
                        <div class="h-40 bg-gray-200" onclick="viewProduct('${category}', '${product.id}')">
                            <img src="${product.image}" alt="${product.name}"
                                 class="w-full h-full object-cover">
                        </div>
                        <div class="p-3">
                            <h3 class="font-medium text-sm truncate" onclick="viewProduct('${category}', '${product.id}')">${product.name}</h3>
                            <p class="text-orange-500 font-bold">৳${product.price}</p>
                            <div class="flex mt-2 space-x-2">
                                <button onclick="event.stopPropagation(); addToCart('${category}', '${product.id}')"
                                        class="flex-1 bg-orange-500 text-white py-1 px-2 rounded text-sm hover:bg-orange-600">
                                    Add to Cart
                                </button>
                                <button onclick="event.stopPropagation(); buyNow('${category}', '${product.id}')"
                                        class="flex-1 bg-green-500 text-white py-1 px-2 rounded text-sm hover:bg-green-600">
                                    Buy Now
                                </button>
                            </div>
                        </div>
                    </div>
                `;
                productsContainer.innerHTML += productCard;
            });
        }

        // Improved search function
        function searchProducts() {
            const searchInput = document.getElementById('search-input');
            const searchTerm = searchInput.value.toLowerCase().trim();
           
            if (!searchTerm) {
                loadProducts(currentCategory);
                return;
            }
           
            const productsContainer = document.getElementById('products-container');
            productsContainer.innerHTML = '';
           
            // Search in all categories and product fields
            let foundProducts = [];
            Object.keys(sampleProducts).forEach(category => {
                sampleProducts[category].forEach(product => {
                    if (product.name.toLowerCase().includes(searchTerm) ||
                        product.description.toLowerCase().includes(searchTerm) ||
                        product.details.toLowerCase().includes(searchTerm)) {
                        foundProducts.push({...product, category});
                    }
                });
            });
           
            if (foundProducts.length === 0) {
                productsContainer.innerHTML = `
                    <div class="col-span-2 text-center text-gray-500 py-8">
                        No products found for "${searchTerm}"
                    </div>
                `;
                return;
            }
           
            // Group by category for better display
            const productsByCategory = {};
            foundProducts.forEach(product => {
                if (!productsByCategory[product.category]) {
                    productsByCategory[product.category] = [];
                }
                productsByCategory[product.category].push(product);
            });
           
            // Display with category headings
            Object.keys(productsByCategory).forEach(category => {
                const categoryName = category.charAt(0).toUpperCase() + category.slice(1);
                productsContainer.innerHTML += `
                    <div class="col-span-2 mt-4">
                        <h3 class="font-bold text-gray-700">${categoryName}</h3>
                    </div>
                `;
               
                productsByCategory[category].forEach(product => {
                    const productCard = `
                        <div class="product-card bg-white rounded-lg shadow overflow-hidden">
                            <div class="h-40 bg-gray-200" onclick="viewProduct('${product.category}', '${product.id}')">
                                <img src="${product.image}" alt="${product.name}"
                                     class="w-full h-full object-cover">
                            </div>
                            <div class="p-3">
                                <h3 class="font-medium text-sm truncate" onclick="viewProduct('${product.category}', '${product.id}')">${product.name}</h3>
                                <p class="text-orange-500 font-bold">৳${product.price}</p>
                                <div class="flex mt-2 space-x-2">
                                    <button onclick="event.stopPropagation(); addToCart('${product.category}', '${product.id}')"
                                            class="flex-1 bg-orange-500 text-white py-1 px-2 rounded text-sm hover:bg-orange-600">
                                        Add to Cart
                                    </button>
                                    <button onclick="event.stopPropagation(); buyNow('${product.category}', '${product.id}')"
                                            class="flex-1 bg-green-500 text-white py-1 px-2 rounded text-sm hover:bg-green-600">
                                        Buy Now
                                    </button>
                                </div>
                            </div>
                        </div>
                    `;
                    productsContainer.innerHTML += productCard;
                });
            });
           
            document.getElementById('current-category').textContent = 'Search Results';
        }

        // View product details
        function viewProduct(category, productId) {
            const product = sampleProducts[category].find(p => p.id === productId);
            if (product) {
                currentProduct = product;
               
                // Set product details
                document.getElementById('product-view-image').src = product.image;
                document.getElementById('product-view-name').textContent = product.name;
                document.getElementById('product-view-price').textContent = '৳' + product.price;
                document.getElementById('product-view-description').textContent = product.description;
               
                // Format and display additional details
                const details = product.details.split('\n').map(line => {
                    const parts = line.split(':');
                    if (parts.length > 1) {
                        return `<p><span class="font-medium">${parts[0]}:</span> ${parts.slice(1).join(':')}</p>`;
                    }
                    return `<p>${line}</p>`;
                }).join('');
               
                document.getElementById('product-view-details').innerHTML = details;
               
                // Show product view section
                showSection('product-view');
            }
        }

        // Go back from product view
        function goBack() {
            showSection('home');
        }

        // Add to cart from product view
        function addToCartFromView() {
            if (currentProduct) {
                const existingItem = cart.find(item => item.id === currentProduct.id);
               
                if (existingItem) {
                    existingItem.quantity += 1;
                } else {
                    cart.push({
                        ...currentProduct,
                        quantity: 1
                    });
                }
               
                localStorage.setItem('cart', JSON.stringify(cart));
                updateCart();
                showToast(`${currentProduct.name} added to cart!`);
                updateCartCount();
            }
        }

        // Buy now from product view
        function buyNowFromView() {
            if (currentProduct) {
                // Clear cart and add only this product
                cart = [{
                    ...currentProduct,
                    quantity: 1
                }];
                localStorage.setItem('cart', JSON.stringify(cart));
                updateCart();
                updateCartCount();
                showSection('cart');
            }
        }

        // Improved cart system with quantity
        function addToCart(category, productId) {
            const product = sampleProducts[category].find(p => p.id === productId);
            if (product) {
                const existingItem = cart.find(item => item.id === productId);
               
                if (existingItem) {
                    existingItem.quantity += 1;
                } else {
                    cart.push({
                        ...product,
                        quantity: 1
                    });
                }
               
                localStorage.setItem('cart', JSON.stringify(cart));
                updateCart();
                showToast(`${product.name} added to cart!`);
                updateCartCount();
            }
        }

        // Remove from cart with quantity control
        function removeFromCart(productId, removeAll = false) {
            const itemIndex = cart.findIndex(item => item.id === productId);
           
            if (itemIndex !== -1) {
                if (removeAll || cart[itemIndex].quantity <= 1) {
                    cart.splice(itemIndex, 1);
                } else {
                    cart[itemIndex].quantity -= 1;
                }
               
                localStorage.setItem('cart', JSON.stringify(cart));
                updateCart();
                updateCartCount();
            }
        }

        // Update cart count in header
        function updateCartCount() {
            const cartCount = cart.reduce((sum, item) => sum + item.quantity, 0);
            const cartCountElement = document.getElementById('cart-count');
           
            if (cartCount > 0) {
                cartCountElement.textContent = cartCount;
                cartCountElement.classList.remove('hidden');
            } else {
                cartCountElement.classList.add('hidden');
            }
        }

        // Update cart function
        function updateCart() {
            const cartItemsContainer = document.getElementById('cart-items');
            const cartSubtotal = document.getElementById('cart-subtotal');
            const cartTotal = document.getElementById('cart-total');
           
            if (cart.length === 0) {
                cartItemsContainer.innerHTML = '<p class="text-center text-gray-500 py-8">Your cart is empty</p>';
                cartSubtotal.textContent = '৳0';
                cartTotal.textContent = '৳50';
                return;
            }
           
            // Calculate subtotal
            const subtotal = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            const total = subtotal + 50; // Adding delivery charge
           
            // Update cart items
            cartItemsContainer.innerHTML = '';
            cart.forEach(item => {
                const cartItem = `
                    <div class="flex items-center p-3 border-b">
                        <div class="w-16 h-16 bg-gray-200 rounded mr-3" onclick="viewProduct('${item.category}', '${item.id}')">
                            <img src="${item.image}" alt="${item.name}" class="w-full h-full object-cover">
                        </div>
                        <div class="flex-1">
                            <h4 class="text-sm font-medium">${item.name}</h4>
                            <p class="text-orange-500 text-sm">৳${item.price} x ${item.quantity} = ৳${item.price * item.quantity}</p>
                        </div>
                        <div class="flex items-center">
                            <button onclick="event.stopPropagation(); removeFromCart('${item.id}')" class="quantity-btn bg-gray-200 rounded-l">
                                -
                            </button>
                            <span class="px-2">${item.quantity}</span>
                            <button onclick="event.stopPropagation(); addToCart('${item.category}', '${item.id}')" class="quantity-btn bg-gray-200 rounded-r">
                                +
                            </button>
                            <button onclick="event.stopPropagation(); removeFromCart('${item.id}', true)" class="ml-2 text-red-500">
                                ✕
                            </button>
                        </div>
                    </div>
                `;
                cartItemsContainer.innerHTML += cartItem;
            });
           
            // Update totals
            cartSubtotal.textContent = `৳${subtotal}`;
            cartTotal.textContent = `৳${total}`;
        }

        // Load checkout items
        function loadCheckoutItems() {
            const checkoutItemsContainer = document.getElementById('checkout-items');
            const checkoutSubtotal = document.getElementById('checkout-subtotal');
            const checkoutTotal = document.getElementById('checkout-total');
           
            checkoutItemsContainer.innerHTML = '';
           
            if (cart.length === 0) {
                return;
            }
           
            // Calculate subtotal
            const subtotal = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            const total = subtotal + 50; // Adding delivery charge
           
            // Update checkout items
            cart.forEach(item => {
                const checkoutItem = `
                    <div class="flex items-center mb-2 p-2 bg-gray-50 rounded">
                        <div class="w-12 h-12 bg-gray-200 rounded mr-3">
                            <img src="${item.image}" class="w-full h-full object-cover">
                        </div>
                        <div class="flex-1">
                            <h4 class="text-sm font-medium">${item.name}</h4>
                            <p class="text-orange-500 text-sm">৳${item.price} x ${item.quantity}</p>
                        </div>
                    </div>
                `;
                checkoutItemsContainer.innerHTML += checkoutItem;
            });
           
            // Update totals
            checkoutSubtotal.textContent = `৳${subtotal}`;
            checkoutTotal.textContent = `৳${total}`;
        }

        // Toast notification function
        function showToast(message) {
            Toastify({
                text: message,
                duration: 3000,
                close: true,
                gravity: "top",
                position: "right",
                backgroundColor: "#f97316",
                stopOnFocus: true
            }).showToast();
        }

        // Improved form validation
        function placeOrder() {
            const form = document.getElementById('delivery-form');
            const inputs = form.querySelectorAll('input[required], textarea[required]');
            let isValid = true;
           
            // Validate each required field
            inputs.forEach(input => {
                if (!input.value.trim()) {
                    input.classList.add('border-red-500');
                    isValid = false;
                } else {
                    input.classList.remove('border-red-500');
                   
                    // Specific validation for phone number
                    if (input.type === 'tel' && !/^01[3-9]\d{8}$/.test(input.value)) {
                        input.classList.add('border-red-500');
                        isValid = false;
                        showToast('Please enter a valid Bangladeshi phone number');
                    }
                }
            });
           
            if (!isValid) {
                showToast('Please fill all required fields correctly');
                return;
            }
           
            const paymentMethod = document.querySelector('input[name="payment"]:checked').value;
           
            if (paymentMethod === 'bkash') {
                const transactionId = document.querySelector('#bkash-details input').value;
                if (!transactionId) {
                    showToast('Please enter bKash transaction ID');
                    return;
                }
               
                // Basic bKash transaction ID validation
                if (!/^\d{10}$/.test(transactionId)) {
                    showToast('Please enter a valid 10-digit bKash transaction ID');
                    return;
                }
            }
           
            const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0) + 50;
           
            showToast(`Order placed successfully!\nTotal: ৳${total}\nPayment: ${paymentMethod === 'cod' ? 'Cash on Delivery' : 'bKash'}`);
           
            // Clear cart
            cart = [];
            localStorage.removeItem('cart');
            updateCart();
            updateCartCount();
            showSection('home');
        }

        // Payment method toggle
        document.addEventListener('DOMContentLoaded', function() {
            document.getElementById('bkash').addEventListener('change', function() {
                document.getElementById('bkash-details').classList.toggle('hidden', !this.checked);
            });
           
            document.getElementById('cod').addEventListener('change', function() {
                document.getElementById('bkash-details').classList.toggle('hidden', this.checked);
            });
           
            // Enter key press for search
            document.getElementById('search-input').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    searchProducts();
                }
            });

            // Input validation on blur
            document.getElementById('delivery-form').addEventListener('blur', function(e) {
                if (e.target.tagName === 'INPUT' || e.target.tagName === 'TEXTAREA') {
                    if (e.target.required && !e.target.value.trim()) {
                        e.target.classList.add('border-red-500');
                    } else {
                        e.target.classList.remove('border-red-500');
                    }
                }
            }, true);

            // Load initial cart count
            updateCartCount();
        });

        // Show section function
        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.section').forEach(section => {
                section.classList.remove('active-section');
            });
           
            // Show selected section
            document.getElementById(`${sectionId}-section`).classList.add('active-section');
           
            // Update active nav item
            document.querySelectorAll('nav a').forEach(navItem => {
                navItem.classList.remove('active-nav');
                navItem.classList.add('text-gray-600');
            });
           
            // Set current nav as active if it's in the bottom nav
            const navItem = document.querySelector(`nav a[onclick="showSection('${sectionId}')"]`);
            if (navItem) {
                navItem.classList.add('active-nav');
                navItem.classList.remove('text-gray-600');
            }
           
            // Update section data if needed
            if (sectionId === 'cart') {
                updateCart();
            } else if (sectionId === 'checkout') {
                loadCheckoutItems();
            }
        }

        // Buy now function
        function buyNow(category, productId) {
            const product = sampleProducts[category].find(p => p.id === productId);
            if (product) {
                // Clear cart and add only this product
                cart = [{
                    ...product,
                    quantity: 1
                }];
                localStorage.setItem('cart', JSON.stringify(cart));
                updateCart();
                updateCartCount();
                showSection('cart');
            }
        }

        // Initialize the app
        document.addEventListener('DOMContentLoaded', function() {
            loadProducts(currentCategory);
        });
    </script>
</body>
</html>

# fghbgfhgfgf
