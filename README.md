<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chilmari E-shop - Your Local Online Marketplace</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Toast Notification CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/toastify-js/src/toastify.min.css">
    <style>
        .section { display: none; }
        .active-section { display: block; }
        .active-nav { color: #f97316; }
        .product-card:hover { transform: translateY(-5px); transition: all 0.3s; }
        .order-card { border-left: 4px solid #f97316; }
        .quantity-btn { width: 25px; height: 25px; display: flex; align-items: center; justify-content: center; }
        .error-border { border-color: #ef4444; }
        .loading-spinner {
            border: 3px solid rgba(255,255,255,0.3);
            border-radius: 50%;
            border-top: 3px solid #fff;
            width: 20px;
            height: 20px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .placeholder-img {
            background-color: #e5e7eb;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #9ca3af;
            font-size: 16px;
        }
    </style>
</head>
<body class="bg-gray-100 pb-16">
    <!-- Header with Search -->
    <header class="bg-orange-500 text-white p-4 sticky top-0 z-10 shadow-md">
        <div class="container mx-auto flex items-center">
            <div class="w-10 h-10 mr-2 bg-white rounded-full flex items-center justify-center">
                <span class="text-orange-500 font-bold">CE</span>
            </div>
            <div class="flex-1 relative">
                <input type="text" id="search-input" placeholder="Search products..."
                       class="w-full py-2 px-4 rounded text-gray-800 text-sm focus:outline-none focus:ring-2 focus:ring-orange-300"
                       aria-label="Search products">
                <button onclick="searchProducts()" class="absolute right-0 top-0 h-full px-4 bg-orange-600 rounded-r hover:bg-orange-700 focus:outline-none">
                    <i class="fas fa-search"></i>
                </button>
            </div>
            <div class="ml-4 relative cursor-pointer" onclick="showSection('cart')" aria-label="Cart" role="button">
                <span id="cart-count" class="absolute -top-2 -right-2 bg-red-500 text-white text-xs rounded-full w-5 h-5 flex items-center justify-center hidden">0</span>
                <i class="fas fa-shopping-cart text-xl"></i>
            </div>
        </div>
    </header>

    <!-- Main Content Sections -->
    <main>
        <!-- Home Section -->
        <section id="home-section" class="section active-section">
            <!-- Categories -->
            <div class="container mx-auto p-4 bg-white shadow-sm rounded-lg mt-2">
                <h2 class="text-lg font-bold mb-2">Categories</h2>
                <div class="grid grid-cols-4 gap-2">
                    <div class="category-item text-center p-2 cursor-pointer hover:bg-gray-50 rounded" onclick="loadProducts('electronics')" role="button" aria-label="Electronics">
                        <div class="bg-gray-200 rounded-full w-12 h-12 mx-auto mb-1 flex items-center justify-center">
                            <i class="fas fa-mobile-alt text-gray-600"></i>
                        </div>
                        <span class="text-xs">Electronics</span>
                    </div>
                    <div class="category-item text-center p-2 cursor-pointer hover:bg-gray-50 rounded" onclick="loadProducts('clothing')" role="button" aria-label="Clothing">
                        <div class="bg-gray-200 rounded-full w-12 h-12 mx-auto mb-1 flex items-center justify-center">
                            <i class="fas fa-tshirt text-gray-600"></i>
                        </div>
                        <span class="text-xs">Clothing</span>
                    </div>
                    <div class="category-item text-center p-2 cursor-pointer hover:bg-gray-50 rounded" onclick="loadProducts('grocery')" role="button" aria-label="Grocery">
                        <div class="bg-gray-200 rounded-full w-12 h-12 mx-auto mb-1 flex items-center justify-center">
                            <i class="fas fa-shopping-basket text-gray-600"></i>
                        </div>
                        <span class="text-xs">Grocery</span>
                    </div>
                    <div class="category-item text-center p-2 cursor-pointer hover:bg-gray-50 rounded" onclick="loadProducts('household')" role="button" aria-label="Household">
                        <div class="bg-gray-200 rounded-full w-12 h-12 mx-auto mb-1 flex items-center justify-center">
                            <i class="fas fa-home text-gray-600"></i>
                        </div>
                        <span class="text-xs">Household</span>
                    </div>
                </div>
            </div>

            <!-- Products -->
            <div class="container mx-auto p-4">
                <div class="flex justify-between items-center mb-4">
                    <h2 class="text-lg font-bold">Featured Products</h2>
                    <div class="text-sm bg-orange-100 text-orange-800 px-2 py-1 rounded">
                        <span id="current-category">All</span>
                    </div>
                </div>
                <div id="products-container" class="grid grid-cols-2 gap-4">
                    <!-- Products will be loaded here -->
                </div>
                <div id="loading-indicator" class="text-center py-8 hidden">
                    <div class="loading-spinner mx-auto mb-2 border-orange-500"></div>
                    <p class="text-gray-600">Loading products...</p>
                </div>
                <div id="no-products" class="text-center py-8 hidden">
                    <i class="fas fa-box-open text-4xl text-gray-400 mb-2"></i>
                    <p class="text-gray-600">No products found</p>
                </div>
            </div>
        </section>

        <!-- Product View Section -->
        <section id="product-view-section" class="section">
            <div class="container mx-auto p-4">
                <button onclick="goBack()" class="mb-4 flex items-center text-orange-500 hover:text-orange-600 focus:outline-none" aria-label="Go back">
                    <i class="fas fa-arrow-left mr-2"></i>
                    Back
                </button>
               
                <div class="bg-white rounded-lg shadow overflow-hidden">
                    <div class="h-64 bg-gray-200 flex items-center justify-center">
                        <img id="product-view-image" src="" alt="Product image" class="w-full h-full object-cover">
                    </div>
                   
                    <div class="p-4">
                        <h2 id="product-view-name" class="text-xl font-bold mb-2"></h2>
                        <p id="product-view-price" class="text-orange-500 text-xl font-bold mb-4"></p>
                        <p id="product-view-description" class="text-gray-600 mb-4"></p>
                       
                        <div class="flex space-x-2">
                            <button onclick="addToCartFromView()"
                                    class="flex-1 bg-orange-500 text-white py-2 px-4 rounded hover:bg-orange-600 focus:outline-none focus:ring-2 focus:ring-orange-300">
                                <i class="fas fa-cart-plus mr-2"></i>Add to Cart
                            </button>
                            <button onclick="buyNowFromView()"
                                    class="flex-1 bg-green-500 text-white py-2 px-4 rounded hover:bg-green-600 focus:outline-none focus:ring-2 focus:ring-green-300">
                                <i class="fas fa-bolt mr-2"></i>Buy Now
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
                    <div class="text-center py-8">
                        <i class="fas fa-shopping-cart text-4xl text-gray-400 mb-2"></i>
                        <p class="text-gray-500">Your cart is empty</p>
                        <button onclick="showSection('home')" class="mt-4 bg-orange-500 text-white py-2 px-4 rounded hover:bg-orange-600 focus:outline-none">
                            <i class="fas fa-store mr-2"></i>Continue Shopping
                        </button>
                    </div>
                </div>
                <div id="cart-summary" class="mt-4 p-4 bg-white rounded shadow hidden">
                    <h3 class="font-bold mb-2">Order Summary</h3>
                    <div class="flex justify-between mb-1">
                        <span>Subtotal:</span>
                        <span id="cart-subtotal">৳0</span>
                    </div>
                    <div class="flex justify-between mb-1">
                        <span>Delivery:</span>
                        <span>৳50</span>
                    </div>
                    <div class="flex justify-between font-bold mt-2 text-lg">
                        <span>Total:</span>
                        <span id="cart-total">৳50</span>
                    </div>
                    <button onclick="showSection('checkout')" class="mt-4 w-full bg-orange-500 text-white py-2 rounded hover:bg-orange-600 focus:outline-none focus:ring-2 focus:ring-orange-300">
                        <i class="fas fa-credit-card mr-2"></i>Proceed to Checkout
                    </button>
                </div>
            </div>
        </section>

        <!-- Checkout Section -->
        <section id="checkout-section" class="section">
            <div class="container mx-auto p-4">
                <button onclick="showSection('cart')" class="mb-4 flex items-center text-orange-500 hover:text-orange-600 focus:outline-none" aria-label="Back to cart">
                    <i class="fas fa-arrow-left mr-2"></i>
                    Back to Cart
                </button>
               
                <div class="bg-white rounded shadow p-4 mb-4">
                    <h2 class="text-lg font-bold mb-4">Delivery Information</h2>
                    <form id="delivery-form">
                        <div class="mb-3">
                            <label class="block text-sm font-medium mb-1">Full Name *</label>
                            <input type="text" required class="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-orange-300"
                                   pattern="[A-Za-z ]{3,}" title="Please enter at least 3 characters"
                                   aria-label="Full name" aria-required="true">
                            <p class="text-red-500 text-xs mt-1 hidden" id="name-error">Please enter a valid name (at least 3 letters)</p>
                        </div>
                        <div class="mb-3">
                            <label class="block text-sm font-medium mb-1">Phone Number *</label>
                            <input type="tel" required class="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-orange-300"
                                   pattern="01[3-9]\d{8}" title="Please enter a valid Bangladeshi phone number"
                                   aria-label="Phone number" aria-required="true">
                            <p class="text-red-500 text-xs mt-1 hidden" id="phone-error">Please enter a valid Bangladeshi phone number (01XXXXXXXXX)</p>
                        </div>
                        <div class="mb-3">
                            <label class="block text-sm font-medium mb-1">Delivery Address *</label>
                            <textarea required class="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-orange-300" rows="3" minlength="10"
                                      aria-label="Delivery address" aria-required="true"></textarea>
                            <p class="text-red-500 text-xs mt-1 hidden" id="address-error">Please enter a complete address (at least 10 characters)</p>
                        </div>
                        <div class="mb-3">
                            <label class="block text-sm font-medium mb-1">Delivery Area</label>
                            <select class="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-orange-300" disabled aria-label="Delivery area">
                                <option>Chilmari Only</option>
                            </select>
                        </div>
                    </form>
                </div>
               
                <div class="bg-white rounded shadow p-4 mb-4">
                    <h2 class="text-lg font-bold mb-4">Payment Method</h2>
                    <div class="space-y-3">
                        <div class="flex items-center">
                            <input type="radio" id="cod" name="payment" value="cod" checked class="mr-2 focus:ring-orange-500" aria-label="Cash on delivery">
                            <label for="cod" class="flex items-center">
                                <span class="bg-gray-200 p-2 rounded mr-2"><i class="fas fa-money-bill-wave text-gray-600"></i></span>
                                Cash on Delivery (COD)
                            </label>
                        </div>
                        <div class="flex items-center">
                            <input type="radio" id="bkash" name="payment" value="bkash" class="mr-2 focus:ring-orange-500" aria-label="bKash payment">
                            <label for="bkash" class="flex items-center">
                                <span class="bg-green-100 p-2 rounded mr-2"><i class="fas fa-mobile-alt text-green-600"></i></span>
                                bKash Payment
                            </label>
                        </div>
                        <div id="bkash-details" class="hidden pl-6 mt-2">
                            <div class="mb-2">
                                <p class="text-sm">Send money to: <span class="font-bold">01770706309</span></p>
                            </div>
                            <div class="mb-2">
                                <label class="block text-sm font-medium mb-1">bKash Transaction ID *</label>
                                <input type="text" class="w-full p-2 border rounded focus:outline-none focus:ring-2 focus:ring-orange-300"
                                       pattern="[A-Za-z0-9]{10}" title="Please enter 10 digit transaction ID"
                                       aria-label="bKash transaction ID">
                                <p class="text-red-500 text-xs mt-1 hidden" id="bkash-error">Please enter a valid 10-digit transaction ID (letters and numbers)</p>
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
                        <div class="flex justify-between font-bold mt-2 text-lg">
                            <span>Total:</span>
                            <span id="checkout-total">৳50</span>
                        </div>
                    </div>
                    <button onclick="placeOrder()" id="place-order-btn" class="mt-4 w-full bg-orange-500 text-white py-2 rounded hover:bg-orange-600 focus:outline-none focus:ring-2 focus:ring-orange-300">
                        <span id="order-btn-text"><i class="fas fa-check-circle mr-2"></i>Place Order</span>
                        <div id="order-spinner" class="loading-spinner ml-2 hidden"></div>
                    </button>
                </div>
            </div>
        </section>

        <!-- Orders Section -->
        <section id="orders-section" class="section">
            <div class="container mx-auto p-4">
                <h2 class="text-lg font-bold mb-4">Your Orders</h2>
                <div id="orders-list">
                    <div class="text-center py-8">
                        <i class="fas fa-box-open text-4xl text-gray-400 mb-2"></i>
                        <p class="text-gray-500">No orders yet</p>
                        <button onclick="showSection('home')" class="mt-4 bg-orange-500 text-white py-2 px-4 rounded hover:bg-orange-600 focus:outline-none">
                            <i class="fas fa-store mr-2"></i>Start Shopping
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- Account Section -->
        <section id="account-section" class="section">
            <div class="container mx-auto p-4">
                <h2 class="text-lg font-bold mb-4">Your Account</h2>
                <div id="user-info" class="bg-white p-4 rounded shadow text-center">
                    <div class="w-20 h-20 mx-auto bg-gray-200 rounded-full flex items-center justify-center mb-3">
                        <i class="fas fa-user text-3xl text-gray-500"></i>
                    </div>
                    <h3 class="font-bold text-lg mb-1">Guest User</h3>
                    <p class="text-gray-600 mb-4">Please login to access your account</p>
                    <button onclick="showLoginForm()" class="bg-orange-500 text-white py-2 px-6 rounded hover:bg-orange-600 focus:outline-none">
                        <i class="fas fa-sign-in-alt mr-2"></i>Login
                    </button>
                </div>
            </div>
        </section>
    </main>

    <!-- Bottom Navigation -->
    <nav class="fixed bottom-0 left-0 right-0 bg-white shadow-lg flex justify-around items-center p-3 z-10" aria-label="Main navigation">
        <a href="#" class="text-center text-orange-500 active-nav" onclick="showSection('home')" aria-label="Home" role="button">
            <div class="w-6 h-6 mx-auto"><i class="fas fa-home"></i></div>
            <span class="text-xs">Home</span>
        </a>
        <a href="#" class="text-center text-gray-600" onclick="showSection('cart')" aria-label="Cart" role="button">
            <div class="w-6 h-6 mx-auto"><i class="fas fa-shopping-cart"></i></div>
            <span class="text-xs">Cart</span>
        </a>
        <a href="#" class="text-center text-gray-600" onclick="showSection('orders')" aria-label="Orders" role="button">
            <div class="w-6 h-6 mx-auto"><i class="fas fa-box-open"></i></div>
            <span class="text-xs">Orders</span>
        </a>
        <a href="#" class="text-center text-gray-600" onclick="showSection('account')" aria-label="Account" role="button">
            <div class="w-6 h-6 mx-auto"><i class="fas fa-user"></i></div>
            <span class="text-xs">Account</span>
        </a>
    </nav>

    <!-- Support Floating Button - Fixed WhatsApp Button -->
    <div class="fixed bottom-16 right-4 z-20">
        <a href="https://wa.me/8801945312372"
           target="_blank"
           class="bg-green-500 text-white rounded-full p-3 shadow-lg block hover:bg-green-600 transition-colors"
           aria-label="Chat on WhatsApp">
            <i class="fab fa-whatsapp text-xl"></i>
        </a>
    </div>

    <!-- Toast Notification JS -->
    <script src="https://cdn.jsdelivr.net/npm/toastify-js"></script>
   
    <script>
        // Enhanced Product Data with more items and realistic details
        const sampleProducts = {
            electronics: [
                {
                    id: "e1",
                    name: "Samsung Galaxy A12",
                    price: 15500,
                    image: "https://m.media-amazon.com/images/I/61L1ItFgFHL._SL1500_.jpg",
                    description: "6.5 inch HD+ display, 4GB RAM, 128GB storage, 5000mAh battery",
                    details: "Brand: Samsung\nModel: Galaxy A12\nColor: Black\nRAM: 4GB\nStorage: 128GB (expandable)\nDisplay: 6.5\" HD+\nCamera: 48MP + 5MP + 2MP + 2MP\nBattery: 5000mAh\nOS: Android 11"
                },
                {
                    id: "e2",
                    name: "Xiaomi Redmi Buds 3 Lite",
                    price: 1200,
                    image: "https://m.media-amazon.com/images/I/51RBk3kAq5L._SL1500_.jpg",
                    description: "Bluetooth 5.2, 18 hours battery life, IP54 water resistant",
                    details: "Brand: Xiaomi\nModel: Redmi Buds 3 Lite\nColor: White\nBluetooth: 5.2\nBattery Life: 18 hours\nCharging Time: 1.5 hours\nWater Resistance: IP54\nDriver Size: 6mm\nWeight: 4.1g per earbud"
                },
                {
                    id: "e3",
                    name: "Walton Power Bank 10000mAh",
                    price: 800,
                    image: "https://m.media-amazon.com/images/I/61GIxXleO9L._SL1500_.jpg",
                    description: "Dual USB ports, LED indicator, fast charging supported",
                    details: "Brand: Walton\nCapacity: 10000mAh\nInput: 5V/2A\nOutput: 5V/2.1A\nPorts: 2 USB\nLED Indicator: Yes\nWeight: 220g\nDimensions: 13.5 x 6.8 x 1.5 cm"
                },
                {
                    id: "e4",
                    name: "Realme Smart Watch",
                    price: 2500,
                    image: "https://m.media-amazon.com/images/I/61XDeOOr0RL._SL1500_.jpg",
                    description: "1.4\" touch display, heart rate monitor, 15 days battery",
                    details: "Brand: Realme\nDisplay: 1.4\" Touchscreen\nBattery: 15 days\nWaterproof: IP68\nSensors: Heart rate, SpO2, steps\nSports Modes: 14\nNotifications: Yes\nCompatibility: Android 5.0+, iOS 10+"
                }
            ],
            clothing: [
                {
                    id: "c1",
                    name: "Men's Cotton T-Shirt",
                    price: 350,
                    image: "https://m.media-amazon.com/images/I/61-jAhtF86L._AC_UL1500_.jpg",
                    description: "Premium quality 100% cotton, regular fit, available in multiple colors",
                    details: "Material: 100% Cotton\nFit: Regular\nSleeve: Short\nColor: Black/White/Blue\nSize: S, M, L, XL\nCare: Machine wash\nOrigin: Bangladesh"
                },
                {
                    id: "c2",
                    name: "Women's Cotton Scarf",
                    price: 250,
                    image: "https://m.media-amazon.com/images/I/71sx7+-qJ5L._AC_UL1500_.jpg",
                    description: "Soft and comfortable, stylish design for all seasons",
                    details: "Material: Cotton Blend\nDimensions: 70\" x 28\"\nPattern: Floral/Geometric\nSeason: All season\nCare: Hand wash\nWeight: 120g\nOrigin: Bangladesh"
                },
                {
                    id: "c3",
                    name: "Kids Winter Jacket",
                    price: 600,
                    image: "https://m.media-amazon.com/images/I/71Qn8Y+QmJL._AC_UL1500_.jpg",
                    description: "Warm winter jacket with fleece lining, perfect for cold weather",
                    details: "Material: Polyester\nLining: Fleece\nClosure: Zipper\nPockets: 2\nAge: 5-7 years\nColor: Blue/Red/Pink\nCare: Machine wash"
                },
                {
                    id: "c4",
                    name: "Traditional Jamdani Saree",
                    price: 1200,
                    image: "https://m.media-amazon.com/images/I/81VJZ+8X1YL._AC_UL1500_.jpg",
                    description: "Authentic Bangladeshi handloom Jamdani saree with matching blouse",
                    details: "Fabric: Cotton Silk\nBlouse: Included\nLength: 5.5 meters\nWork: Handwoven Jamdani\nOccasion: Wedding/Festival\nColor: Various\nOrigin: Dhaka, Bangladesh"
                }
            ],
            grocery: [
                {
                    id: "g1",
                    name: "Pure Mustard Oil (1L)",
                    price: 180,
                    image: "https://m.media-amazon.com/images/I/71YHblzCgVL._SL1500_.jpg",
                    description: "100% pure mustard oil, cold pressed, rich in omega-3",
                    details: "Brand: PureGold\nQuantity: 1 liter\nType: Cold Pressed\nShelf Life: 12 months\nOrigin: Bangladesh\nNutrition: Rich in Omega-3\nUsage: Cooking, Hair care"
                },
                {
                    id: "g2",
                    name: "Premium Basmati Rice (5kg)",
                    price: 95,
                    image: "https://m.media-amazon.com/images/I/81W+0XwuJVL._SL1500_.jpg",
                    description: "Aromatic long grain basmati rice, new crop",
                    details: "Brand: Aromatic\nQuantity: 5kg\nType: Basmati\nGrain Length: Extra Long\nAge: New Crop\nOrigin: India\nCooking Time: 15-20 mins"
                },
                {
                    id: "g3",
                    name: "Pure Natural Honey (500gm)",
                    price: 300,
                    image: "https://m.media-amazon.com/images/I/71RMuOKN3VL._SL1500_.jpg",
                    description: "100% pure forest honey, no additives or preservatives",
                    details: "Brand: Nature's Gift\nQuantity: 500gm\nType: Forest Honey\nPurity: 100%\nBenefits: Immunity Booster\nShelf Life: 24 months\nOrigin: Sundarbans"
                },
                {
                    id: "g4",
                    name: "Spices Combo Pack (5x100gm)",
                    price: 150,
                    image: "https://m.media-amazon.com/images/I/81d5OrW-AQL._SL1500_.jpg",
                    description: "Essential spices pack including turmeric, cumin, coriander, chili, garam masala",
                    details: "Contents: Turmeric, Cumin, Coriander, Chili, Garam Masala\nQuantity: 100gm each\nOrigin: Bangladesh\nPackaging: Airtight\nShelf Life: 12 months\nUsage: Daily cooking"
                }
            ],
            household: [
                {
                    id: "h1",
                    name: "Non-Stick Frying Pan (24cm)",
                    price: 650,
                    image: "https://m.media-amazon.com/images/I/71UGB5x3VQL._SL1500_.jpg",
                    description: "Durable ceramic coating, heat resistant handle, induction compatible",
                    details: "Brand: KitchenStar\nDiameter: 24cm\nMaterial: Aluminum\nCoating: Ceramic\nHandle: Heat Resistant\nInduction Compatible: Yes\nWarranty: 1 year"
                },
                {
                    id: "h2",
                    name: "Plastic Broom with Handle",
                    price: 120,
                    image: "https://m.media-amazon.com/images/I/71yV5vZKKoL._SL1500_.jpg",
                    description: "Strong bristles, lightweight wooden handle, for indoor/outdoor use",
                    details: "Bristle Material: Durable Plastic\nHandle Material: Wood\nLength: 120cm\nType: Indoor/Outdoor\nColor: Brown\nWeight: 450g\nDurability: 6+ months"
                },
                {
                    id: "h3",
                    name: "Water Purifier (10L)",
                    price: 2500,
                    image: "https://m.media-amazon.com/images/I/71Q4+JQ2i4L._SL1500_.jpg",
                    description: "5 stage filtration system, removes bacteria and heavy metals",
                    details: "Brand: PureWater\nCapacity: 10 liters\nTechnology: RO+UV+UF\nFiltration Stages: 5\nInstallation: Counter Top\nFilter Life: 6 months\nWarranty: 1 year"
                },
                {
                    id: "h4",
                    name: "Plastic Storage Box Set (5pcs)",
                    price: 800,
                    image: "https://m.media-amazon.com/images/I/71XgNp3XZVL._SL1500_.jpg",
                    description: "Food grade plastic containers with airtight lids, stackable design",
                    details: "Number of Pieces: 5\nMaterial: Food Grade Plastic\nLids: Airtight\nStackable: Yes\nColors: Assorted\nCapacity: 0.5L to 2L\nMicrowave Safe: Yes"
                }
            ]
        };

        // Current state with localStorage support
        let currentCategory = localStorage.getItem('currentCategory') || 'electronics';
        let cart = JSON.parse(localStorage.getItem('cart')) || [];
        let currentProduct = null;

        // Initialize the app when DOM is loaded
        document.addEventListener('DOMContentLoaded', function() {
            // Setup payment method toggle
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

            // Setup form validation
            setupFormValidation();

            // Load initial cart count
            updateCartCount();
           
            // Load products
            loadProducts(currentCategory);
           
            // Set default image error handlers
            setDefaultImageHandlers();
        });

        // Set default image handlers for all images
        function setDefaultImageHandlers() {
            document.querySelectorAll('img').forEach(img => {
                img.onerror = function() {
                    this.src = 'data:image/svg+xml;charset=UTF-8,%3Csvg xmlns="http://www.w3.org/2000/svg" width="200" height="200" viewBox="0 0 200 200" fill="%23e5e7eb"%3E%3Crect width="200" height="200"%3E%3C/rect%3E%3Ctext x="50%" y="50%" font-family="Arial" font-size="16" fill="%239ca3af" text-anchor="middle" dominant-baseline="middle"%3ENo Image%3C/text%3E%3C/svg%3E';
                };
            });
        }

        // Load products function with loading indicator
        function loadProducts(category) {
            currentCategory = category;
            localStorage.setItem('currentCategory', category);
           
            // Update category display name
            const categoryDisplayNames = {
                electronics: "Electronics",
                clothing: "Clothing",
                grocery: "Grocery",
                household: "Household"
            };
            document.getElementById('current-category').textContent = categoryDisplayNames[category] || category;
           
            const productsContainer = document.getElementById('products-container');
            const loadingIndicator = document.getElementById('loading-indicator');
            const noProducts = document.getElementById('no-products');
           
            // Show loading indicator
            productsContainer.innerHTML = '';
            loadingIndicator.classList.remove('hidden');
            noProducts.classList.add('hidden');
           
            // Simulate loading delay (in real app, this would be an API call)
            setTimeout(() => {
                loadingIndicator.classList.add('hidden');
               
                const products = sampleProducts[category];
               
                if (!products || products.length === 0) {
                    noProducts.classList.remove('hidden');
                    return;
                }
               
                products.forEach(product => {
                    const productCard = `
                        <div class="product-card bg-white rounded-lg shadow overflow-hidden transition-all duration-300">
                            <div class="h-40 bg-gray-200 cursor-pointer" onclick="viewProduct('${category}', '${product.id}')" aria-label="View ${product.name}">
                                <img src="${product.image}" alt="${product.name}"
                                     class="w-full h-full object-cover"
                                     loading="lazy">
                            </div>
                            <div class="p-3">
                                <h3 class="font-medium text-sm truncate cursor-pointer" onclick="viewProduct('${category}', '${product.id}')" aria-label="View ${product.name}">${product.name}</h3>
                                <p class="text-orange-500 font-bold">৳${product.price}</p>
                                <div class="flex mt-2 space-x-2">
                                    <button onclick="event.stopPropagation(); addToCart('${category}', '${product.id}')"
                                            class="flex-1 bg-orange-500 text-white py-1 px-2 rounded text-sm hover:bg-orange-600 focus:outline-none">
                                        <i class="fas fa-cart-plus mr-1"></i>Add
                                    </button>
                                    <button onclick="event.stopPropagation(); buyNow('${category}', '${product.id}')"
                                            class="flex-1 bg-green-500 text-white py-1 px-2 rounded text-sm hover:bg-green-600 focus:outline-none">
                                        <i class="fas fa-bolt mr-1"></i>Buy
                                    </button>
                                </div>
                            </div>
                        </div>
                    `;
                    productsContainer.innerHTML += productCard;
                });
               
                // Set image error handlers for newly loaded images
                setDefaultImageHandlers();
            }, 500); // Simulate network delay
        }

        // Improved search function with loading indicator
        function searchProducts() {
            const searchInput = document.getElementById('search-input');
            const searchTerm = searchInput.value.toLowerCase().trim();
           
            if (!searchTerm) {
                loadProducts(currentCategory);
                return;
            }
           
            const productsContainer = document.getElementById('products-container');
            const loadingIndicator = document.getElementById('loading-indicator');
            const noProducts = document.getElementById('no-products');
           
            // Show loading indicator
            productsContainer.innerHTML = '';
            loadingIndicator.classList.remove('hidden');
            noProducts.classList.add('hidden');
           
            // Simulate search delay
            setTimeout(() => {
                loadingIndicator.classList.add('hidden');
               
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
                    noProducts.classList.remove('hidden');
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
                    const categoryDisplayNames = {
                        electronics: "Electronics",
                        clothing: "Clothing",
                        grocery: "Grocery",
                        household: "Household"
                    };
                    const categoryName = categoryDisplayNames[category] || category;
                   
                    productsContainer.innerHTML += `
                        <div class="col-span-2 mt-4">
                            <h3 class="font-bold text-gray-700">${categoryName}</h3>
                        </div>
                    `;
                   
                    productsByCategory[category].forEach(product => {
                        const productCard = `
                            <div class="product-card bg-white rounded-lg shadow overflow-hidden transition-all duration-300">
                                <div class="h-40 bg-gray-200 cursor-pointer" onclick="viewProduct('${product.category}', '${product.id}')" aria-label="View ${product.name}">
                                    <img src="${product.image}" alt="${product.name}"
                                         class="w-full h-full object-cover"
                                         loading="lazy">
                                </div>
                                <div class="p-3">
                                    <h3 class="font-medium text-sm truncate cursor-pointer" onclick="viewProduct('${product.category}', '${product.id}')" aria-label="View ${product.name}">${product.name}</h3>
                                    <p class="text-orange-500 font-bold">৳${product.price}</p>
                                    <div class="flex mt-2 space-x-2">
                                        <button onclick="event.stopPropagation(); addToCart('${product.category}', '${product.id}')"
                                                class="flex-1 bg-orange-500 text-white py-1 px-2 rounded text-sm hover:bg-orange-600 focus:outline-none">
                                            <i class="fas fa-cart-plus mr-1"></i>Add
                                        </button>
                                        <button onclick="event.stopPropagation(); buyNow('${product.category}', '${product.id}')"
                                                class="flex-1 bg-green-500 text-white py-1 px-2 rounded text-sm hover:bg-green-600 focus:outline-none">
                                            <i class="fas fa-bolt mr-1"></i>Buy
                                        </button>
                                    </div>
                                </div>
                            </div>
                        `;
                        productsContainer.innerHTML += productCard;
                    });
                });
               
                document.getElementById('current-category').textContent = 'Search Results';
               
                // Set image error handlers for newly loaded images
                setDefaultImageHandlers();
            }, 500); // Simulate search delay
        }

        // View product details
        function viewProduct(category, productId) {
            const product = sampleProducts[category].find(p => p.id === productId);
            if (product) {
                currentProduct = product;
               
                // Set product details
                const productImage = document.getElementById('product-view-image');
                productImage.src = product.image;
                productImage.alt = product.name;
               
                document.getElementById('product-view-name').textContent = product.name;
                document.getElementById('product-view-price').textContent = '৳' + product.price;
                document.getElementById('product-view-description').textContent = product.description;
               
                // Format and display additional details with XSS protection
                const details = product.details.split('\n').map(line => {
                    const parts = line.split(':');
                    if (parts.length > 1) {
                        return `<p class="mb-1"><span class="font-medium">${escapeHtml(parts[0])}:</span> ${escapeHtml(parts.slice(1).join(':'))}</p>`;
                    }
                    return `<p class="mb-1">${escapeHtml(line)}</p>`;
                }).join('');
               
                document.getElementById('product-view-details').innerHTML = details;
               
                // Show product view section
                showSection('product-view');
            }
        }

        // Basic HTML escaping for XSS protection
        function escapeHtml(unsafe) {
            return unsafe
                .replace(/&/g, "&amp;")
                .replace(/</g, "&lt;")
                .replace(/>/g, "&gt;")
                .replace(/"/g, "&quot;")
                .replace(/'/g, "&#039;");
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
            const cartSummary = document.getElementById('cart-summary');
            const cartSubtotal = document.getElementById('cart-subtotal');
            const cartTotal = document.getElementById('cart-total');
           
            if (cart.length === 0) {
                cartItemsContainer.innerHTML = `
                    <div class="text-center py-8">
                        <i class="fas fa-shopping-cart text-4xl text-gray-400 mb-2"></i>
                        <p class="text-gray-500">Your cart is empty</p>
                        <button onclick="showSection('home')" class="mt-4 bg-orange-500 text-white py-2 px-4 rounded hover:bg-orange-600 focus:outline-none">
                            <i class="fas fa-store mr-2"></i>Continue Shopping
                        </button>
                    </div>
                `;
                cartSummary.classList.add('hidden');
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
                    <div class="flex items-center p-3 border-b hover:bg-gray-50">
                        <div class="w-16 h-16 bg-gray-200 rounded mr-3 cursor-pointer" onclick="viewProduct('${item.category}', '${item.id}')" aria-label="View ${item.name}">
                            <img src="${item.image}" alt="${item.name}" class="w-full h-full object-cover">
                        </div>
                        <div class="flex-1">
                            <h4 class="text-sm font-medium">${escapeHtml(item.name)}</h4>
                            <p class="text-orange-500 text-sm">৳${item.price} x ${item.quantity} = ৳${item.price * item.quantity}</p>
                        </div>
                        <div class="flex items-center">
                            <button onclick="event.stopPropagation(); removeFromCart('${item.id}')" class="quantity-btn bg-gray-200 rounded-l hover:bg-gray-300 focus:outline-none" aria-label="Decrease quantity">
                                -
                            </button>
                            <span class="px-2 text-sm">${item.quantity}</span>
                            <button onclick="event.stopPropagation(); addToCart('${item.category}', '${item.id}')" class="quantity-btn bg-gray-200 rounded-r hover:bg-gray-300 focus:outline-none" aria-label="Increase quantity">
                                +
                            </button>
                            <button onclick="event.stopPropagation(); removeFromCart('${item.id}', true)" class="ml-2 text-red-500 hover:text-red-600 focus:outline-none" aria-label="Remove item">
                                <i class="fas fa-times"></i>
                            </button>
                        </div>
                    </div>
                `;
                cartItemsContainer.innerHTML += cartItem;
            });
           
            // Update totals and show summary
            cartSubtotal.textContent = `৳${subtotal}`;
            cartTotal.textContent = `৳${total}`;
            cartSummary.classList.remove('hidden');
           
            // Set image error handlers for cart images
            setDefaultImageHandlers();
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
                            <img src="${item.image}" alt="${item.name}" class="w-full h-full object-cover">
                        </div>
                        <div class="flex-1">
                            <h4 class="text-sm font-medium">${escapeHtml(item.name)}</h4>
                            <p class="text-orange-500 text-sm">৳${item.price} x ${item.quantity}</p>
                        </div>
                    </div>
                `;
                checkoutItemsContainer.innerHTML += checkoutItem;
            });
           
            // Update totals
            checkoutSubtotal.textContent = `৳${subtotal}`;
            checkoutTotal.textContent = `৳${total}`;
           
            // Set image error handlers for checkout images
            setDefaultImageHandlers();
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
                stopOnFocus: true,
                ariaLive: "polite"
            }).showToast();
        }

        // Form validation functions
        function validateName(name) {
            const regex = /^[A-Za-z ]{3,}$/;
            return regex.test(name);
        }

        function validatePhone(phone) {
            const regex = /^01[3-9]\d{8}$/;
            return regex.test(phone);
        }

        function validateAddress(address) {
            return address.length >= 10;
        }

        function validateBkashTransactionId(transactionId) {
            const regex = /^[A-Za-z0-9]{10}$/;
            return regex.test(transactionId);
        }

        // Improved form validation with real-time feedback
        function setupFormValidation() {
            const form = document.getElementById('delivery-form');
           
            // Name validation
            const nameInput = form.querySelector('input[type="text"]');
            nameInput.addEventListener('input', function() {
                const isValid = validateName(this.value);
                const errorElement = document.getElementById('name-error');
               
                if (isValid) {
                    this.classList.remove('error-border');
                    errorElement.classList.add('hidden');
                } else {
                    this.classList.add('error-border');
                    errorElement.classList.remove('hidden');
                }
            });
           
            // Phone validation
            const phoneInput = form.querySelector('input[type="tel"]');
            phoneInput.addEventListener('input', function() {
                const isValid = validatePhone(this.value);
                const errorElement = document.getElementById('phone-error');
               
                if (isValid) {
                    this.classList.remove('error-border');
                    errorElement.classList.add('hidden');
                } else {
                    this.classList.add('error-border');
                    errorElement.classList.remove('hidden');
                }
            });
           
            // Address validation
            const addressInput = form.querySelector('textarea');
            addressInput.addEventListener('input', function() {
                const isValid = validateAddress(this.value);
                const errorElement = document.getElementById('address-error');
               
                if (isValid) {
                    this.classList.remove('error-border');
                    errorElement.classList.add('hidden');
                } else {
                    this.classList.add('error-border');
                    errorElement.classList.remove('hidden');
                }
            });
           
            // bKash validation
            const bkashInput = document.querySelector('#bkash-details input');
            if (bkashInput) {
                bkashInput.addEventListener('input', function() {
                    const isValid = validateBkashTransactionId(this.value);
                    const errorElement = document.getElementById('bkash-error');
                   
                    if (isValid) {
                        this.classList.remove('error-border');
                        errorElement.classList.add('hidden');
                    } else {
                        this.classList.add('error-border');
                        errorElement.classList.remove('hidden');
                    }
                });
            }
        }

        // Improved form validation
        function placeOrder() {
            const form = document.getElementById('delivery-form');
            const inputs = form.querySelectorAll('input[required], textarea[required]');
            let isValid = true;
           
            // Validate each required field
            inputs.forEach(input => {
                let fieldValid = false;
               
                if (input.type === 'text') {
                    fieldValid = validateName(input.value);
                } else if (input.type === 'tel') {
                    fieldValid = validatePhone(input.value);
                } else if (input.tagName === 'TEXTAREA') {
                    fieldValid = validateAddress(input.value);
                }
               
                if (!fieldValid) {
                    input.classList.add('error-border');
                    isValid = false;
                   
                    // Show appropriate error message
                    if (input.type === 'text') {
                        document.getElementById('name-error').classList.remove('hidden');
                    } else if (input.type === 'tel') {
                        document.getElementById('phone-error').classList.remove('hidden');
                    } else if (input.tagName === 'TEXTAREA') {
                        document.getElementById('address-error').classList.remove('hidden');
                    }
                } else {
                    input.classList.remove('error-border');
                }
            });
           
            if (!isValid) {
                showToast('Please fill all required fields correctly');
                return;
            }
           
            const paymentMethod = document.querySelector('input[name="payment"]:checked').value;
           
            if (paymentMethod === 'bkash') {
                const transactionId = document.querySelector('#bkash-details input').value;
                if (!validateBkashTransactionId(transactionId)) {
                    document.querySelector('#bkash-details input').classList.add('error-border');
                    document.getElementById('bkash-error').classList.remove('hidden');
                    showToast('Please enter a valid 10-digit bKash transaction ID (letters and numbers)');
                    return;
                }
            }
           
            const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0) + 50;
           
            // Show loading state
            const orderBtn = document.getElementById('place-order-btn');
            const orderBtnText = document.getElementById('order-btn-text');
            const orderSpinner = document.getElementById('order-spinner');
           
            orderBtn.disabled = true;
            orderBtnText.innerHTML = '<i class="fas fa-spinner fa-spin mr-2"></i>Processing...';
            orderSpinner.classList.remove('hidden');
           
            // Simulate order processing
            setTimeout(() => {
                showToast(`Order placed successfully!\nTotal: ৳${total}\nPayment: ${paymentMethod === 'cod' ? 'Cash on Delivery' : 'bKash'}`);
               
                // Reset button state
                orderBtn.disabled = false;
                orderBtnText.innerHTML = '<i class="fas fa-check-circle mr-2"></i>Place Order';
                orderSpinner.classList.add('hidden');
               
                // Clear cart
                cart = [];
                localStorage.removeItem('cart');
                updateCart();
                updateCartCount();
                showSection('home');
               
                // Reset form
                form.reset();
            }, 2000);
        }

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
           
            // Scroll to top when changing sections
            window.scrollTo(0, 0);
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

        // Show login form (placeholder function)
        function showLoginForm() {
            showToast('Login feature will be implemented soon');
        }
    </script>
</body>
</html>
