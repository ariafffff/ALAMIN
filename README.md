<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chilmari E-shop - Admin Panel</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        .sidebar { width: 250px; transition: all 0.3s; }
        .sidebar-collapsed { width: 70px; }
        .sidebar-collapsed .sidebar-text { display: none; }
        .sidebar-collapsed .logo-text { display: none; }
        .sidebar-collapsed .menu-item { justify-content: center; }
        .content-area { margin-left: 250px; transition: all 0.3s; }
        .content-collapsed { margin-left: 70px; }
        .active-menu { background-color: #fb923c; color: white; }
        .dashboard-card { transition: all 0.3s; }
        .dashboard-card:hover { transform: translateY(-5px); }
    </style>
</head>
<body class="bg-gray-100">
    <!-- Admin Layout -->
    <div class="flex h-screen">
        <!-- Sidebar -->
        <div id="sidebar" class="sidebar bg-gray-800 text-white fixed h-full">
            <div class="p-4 flex items-center border-b border-gray-700">
                <div class="w-10 h-10 bg-orange-500 rounded-full flex items-center justify-center">
                    <span class="font-bold">CE</span>
                </div>
                <span class="logo-text ml-3 text-xl font-bold">Chilmari Shop</span>
            </div>
           
            <div class="p-4">
                <div class="mb-6">
                    <div class="flex items-center mb-2 p-2 rounded hover:bg-gray-700 cursor-pointer">
                        <img src="https://randomuser.me/api/portraits/men/1.jpg" class="w-8 h-8 rounded-full">
                        <div class="sidebar-text ml-3">
                            <div class="font-medium">Admin User</div>
                            <div class="text-xs text-gray-400">Super Admin</div>
                        </div>
                    </div>
                </div>
               
                <ul class="space-y-2">
                    <li>
                        <a href="#" class="menu-item flex items-center p-2 rounded hover:bg-gray-700 active-menu" onclick="showAdminSection('dashboard')">
                            <i class="fas fa-tachometer-alt"></i>
                            <span class="sidebar-text ml-3">Dashboard</span>
                        </a>
                    </li>
                    <li>
                        <a href="#" class="menu-item flex items-center p-2 rounded hover:bg-gray-700" onclick="showAdminSection('products')">
                            <i class="fas fa-box-open"></i>
                            <span class="sidebar-text ml-3">Products</span>
                        </a>
                    </li>
                    <li>
                        <a href="#" class="menu-item flex items-center p-2 rounded hover:bg-gray-700" onclick="showAdminSection('orders')">
                            <i class="fas fa-shopping-cart"></i>
                            <span class="sidebar-text ml-3">Orders</span>
                            <span class="sidebar-text ml-auto bg-orange-500 text-white text-xs px-2 py-1 rounded-full">15</span>
                        </a>
                    </li>
                    <li>
                        <a href="#" class="menu-item flex items-center p-2 rounded hover:bg-gray-700" onclick="showAdminSection('customers')">
                            <i class="fas fa-users"></i>
                            <span class="sidebar-text ml-3">Customers</span>
                        </a>
                    </li>
                    <li>
                        <a href="#" class="menu-item flex items-center p-2 rounded hover:bg-gray-700" onclick="showAdminSection('categories')">
                            <i class="fas fa-tags"></i>
                            <span class="sidebar-text ml-3">Categories</span>
                        </a>
                    </li>
                    <li>
                        <a href="#" class="menu-item flex items-center p-2 rounded hover:bg-gray-700" onclick="showAdminSection('reports')">
                            <i class="fas fa-chart-bar"></i>
                            <span class="sidebar-text ml-3">Reports</span>
                        </a>
                    </li>
                    <li>
                        <a href="#" class="menu-item flex items-center p-2 rounded hover:bg-gray-700" onclick="showAdminSection('settings')">
                            <i class="fas fa-cog"></i>
                            <span class="sidebar-text ml-3">Settings</span>
                        </a>
                    </li>
                </ul>
            </div>
           
            <div class="absolute bottom-0 w-full p-4 border-t border-gray-700">
                <a href="#" class="menu-item flex items-center p-2 rounded hover:bg-gray-700" onclick="toggleSidebar()">
                    <i class="fas fa-chevron-left"></i>
                    <span class="sidebar-text ml-3">Collapse</span>
                </a>
            </div>
        </div>

        <!-- Main Content -->
        <div id="content-area" class="content-area flex-1 overflow-auto">
            <!-- Top Navigation -->
            <nav class="bg-white shadow py-4 px-6 flex justify-between items-center">
                <div class="flex items-center">
                    <button onclick="toggleSidebar()" class="mr-4 text-gray-600">
                        <i class="fas fa-bars"></i>
                    </button>
                    <h1 id="admin-section-title" class="text-xl font-bold text-gray-800">Dashboard</h1>
                </div>
               
                <div class="flex items-center space-x-4">
                    <div class="relative">
                        <button class="text-gray-600">
                            <i class="fas fa-bell"></i>
                            <span class="absolute -top-1 -right-1 bg-red-500 text-white text-xs rounded-full w-4 h-4 flex items-center justify-center">3</span>
                        </button>
                    </div>
                    <div class="relative">
                        <button class="text-gray-600">
                            <i class="fas fa-envelope"></i>
                            <span class="absolute -top-1 -right-1 bg-blue-500 text-white text-xs rounded-full w-4 h-4 flex items-center justify-center">5</span>
                        </button>
                    </div>
                    <div class="border-l pl-4">
                        <div class="flex items-center">
                            <img src="https://randomuser.me/api/portraits/men/1.jpg" class="w-8 h-8 rounded-full">
                            <span class="ml-2">Admin</span>
                        </div>
                    </div>
                </div>
            </nav>

            <!-- Admin Sections -->
            <div class="p-6">
                <!-- Dashboard Section -->
                <div id="dashboard-section" class="admin-section">
                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-6">
                        <div class="dashboard-card bg-white p-6 rounded-lg shadow">
                            <div class="flex justify-between items-center">
                                <div>
                                    <p class="text-gray-500">Total Sales</p>
                                    <h3 class="text-2xl font-bold">৳1,25,000</h3>
                                </div>
                                <div class="bg-orange-100 p-3 rounded-full text-orange-500">
                                    <i class="fas fa-shopping-cart"></i>
                                </div>
                            </div>
                            <p class="mt-2 text-sm text-green-500">
                                <i class="fas fa-arrow-up"></i> 12% from last month
                            </p>
                        </div>
                       
                        <div class="dashboard-card bg-white p-6 rounded-lg shadow">
                            <div class="flex justify-between items-center">
                                <div>
                                    <p class="text-gray-500">Total Orders</p>
                                    <h3 class="text-2xl font-bold">156</h3>
                                </div>
                                <div class="bg-blue-100 p-3 rounded-full text-blue-500">
                                    <i class="fas fa-truck"></i>
                                </div>
                            </div>
                            <p class="mt-2 text-sm text-green-500">
                                <i class="fas fa-arrow-up"></i> 8% from last month
                            </p>
                        </div>
                       
                        <div class="dashboard-card bg-white p-6 rounded-lg shadow">
                            <div class="flex justify-between items-center">
                                <div>
                                    <p class="text-gray-500">Total Products</p>
                                    <h3 class="text-2xl font-bold">48</h3>
                                </div>
                                <div class="bg-green-100 p-3 rounded-full text-green-500">
                                    <i class="fas fa-boxes"></i>
                                </div>
                            </div>
                            <p class="mt-2 text-sm text-gray-500">
                                <i class="fas fa-equals"></i> Same as last month
                            </p>
                        </div>
                       
                        <div class="dashboard-card bg-white p-6 rounded-lg shadow">
                            <div class="flex justify-between items-center">
                                <div>
                                    <p class="text-gray-500">Total Customers</p>
                                    <h3 class="text-2xl font-bold">89</h3>
                                </div>
                                <div class="bg-purple-100 p-3 rounded-full text-purple-500">
                                    <i class="fas fa-users"></i>
                                </div>
                            </div>
                            <p class="mt-2 text-sm text-green-500">
                                <i class="fas fa-arrow-up"></i> 15% from last month
                            </p>
                        </div>
                    </div>
                   
                    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6 mb-6">
                        <div class="bg-white p-6 rounded-lg shadow lg:col-span-2">
                            <div class="flex justify-between items-center mb-4">
                                <h3 class="font-bold">Sales Overview</h3>
                                <select class="border rounded px-2 py-1 text-sm">
                                    <option>Last 7 Days</option>
                                    <option>Last Month</option>
                                    <option selected>Last Year</option>
                                </select>
                            </div>
                            <div class="h-64 bg-gray-100 rounded flex items-center justify-center">
                                [Sales Chart Placeholder]
                            </div>
                        </div>
                       
                        <div class="bg-white p-6 rounded-lg shadow">
                            <h3 class="font-bold mb-4">Recent Orders</h3>
                            <div class="space-y-4">
                                <div class="flex items-center justify-between border-b pb-3">
                                    <div>
                                        <p class="font-medium">#ORD-1256</p>
                                        <p class="text-sm text-gray-500">2 items</p>
                                    </div>
                                    <div class="text-right">
                                        <p class="text-orange-500 font-medium">৳1,250</p>
                                        <p class="text-xs text-gray-500">10 min ago</p>
                                    </div>
                                </div>
                                <div class="flex items-center justify-between border-b pb-3">
                                    <div>
                                        <p class="font-medium">#ORD-1255</p>
                                        <p class="text-sm text-gray-500">5 items</p>
                                    </div>
                                    <div class="text-right">
                                        <p class="text-orange-500 font-medium">৳2,850</p>
                                        <p class="text-xs text-gray-500">25 min ago</p>
                                    </div>
                                </div>
                                <div class="flex items-center justify-between border-b pb-3">
                                    <div>
                                        <p class="font-medium">#ORD-1254</p>
                                        <p class="text-sm text-gray-500">1 item</p>
                                    </div>
                                    <div class="text-right">
                                        <p class="text-orange-500 font-medium">৳650</p>
                                        <p class="text-xs text-gray-500">1 hour ago</p>
                                    </div>
                                </div>
                                <div class="flex items-center justify-between">
                                    <div>
                                        <p class="font-medium">#ORD-1253</p>
                                        <p class="text-sm text-gray-500">3 items</p>
                                    </div>
                                    <div class="text-right">
                                        <p class="text-orange-500 font-medium">৳1,750</p>
                                        <p class="text-xs text-gray-500">2 hours ago</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                   
                    <div class="bg-white p-6 rounded-lg shadow">
                        <h3 class="font-bold mb-4">Top Selling Products</h3>
                        <div class="overflow-x-auto">
                            <table class="min-w-full divide-y divide-gray-200">
                                <thead class="bg-gray-50">
                                    <tr>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Product</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Category</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Price</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Sold</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Revenue</th>
                                    </tr>
                                </thead>
                                <tbody class="bg-white divide-y divide-gray-200">
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="flex items-center">
                                                <div class="flex-shrink-0 h-10 w-10 bg-gray-200 rounded overflow-hidden">
                                                    <img src="https://m.media-amazon.com/images/I/61L1ItFgFHL._SL1500_.jpg" class="h-full w-full object-cover">
                                                </div>
                                                <div class="ml-4">
                                                    <div class="text-sm font-medium text-gray-900">Smartphone X3</div>
                                                </div>
                                            </div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">Electronics</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">৳15,500</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">42</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-orange-500">৳6,51,000</td>
                                    </tr>
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="flex items-center">
                                                <div class="flex-shrink-0 h-10 w-10 bg-gray-200 rounded overflow-hidden">
                                                    <img src="https://m.media-amazon.com/images/I/81VJZ+8X1YL._AC_UL1500_.jpg" class="h-full w-full object-cover">
                                                </div>
                                                <div class="ml-4">
                                                    <div class="text-sm font-medium text-gray-900">Saree</div>
                                                </div>
                                            </div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">Clothing</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">৳1,200</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">38</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-orange-500">৳45,600</td>
                                    </tr>
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="flex items-center">
                                                <div class="flex-shrink-0 h-10 w-10 bg-gray-200 rounded overflow-hidden">
                                                    <img src="https://m.media-amazon.com/images/I/71YHblzCgVL._SL1500_.jpg" class="h-full w-full object-cover">
                                                </div>
                                                <div class="ml-4">
                                                    <div class="text-sm font-medium text-gray-900">Pure Mustard Oil</div>
                                                </div>
                                            </div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">Grocery</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">৳180</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">35</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-orange-500">৳6,300</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
               
                <!-- Products Section -->
                <div id="products-section" class="admin-section hidden">
                    <div class="flex justify-between items-center mb-6">
                        <h2 class="text-xl font-bold">Products Management</h2>
                        <button onclick="showProductModal()" class="bg-orange-500 text-white px-4 py-2 rounded hover:bg-orange-600">
                            <i class="fas fa-plus mr-2"></i> Add Product
                        </button>
                    </div>
                   
                    <div class="bg-white rounded-lg shadow overflow-hidden">
                        <div class="p-4 border-b flex justify-between items-center">
                            <div class="flex items-center">
                                <select class="border rounded px-3 py-1 mr-2">
                                    <option>Bulk Action</option>
                                    <option>Delete Selected</option>
                                    <option>Change Category</option>
                                </select>
                                <button class="bg-gray-100 px-3 py-1 rounded text-sm">Apply</button>
                            </div>
                            <div class="relative">
                                <input type="text" placeholder="Search products..." class="border rounded px-3 py-1 pl-8">
                                <i class="fas fa-search absolute left-3 top-2 text-gray-400"></i>
                            </div>
                        </div>
                       
                        <div class="overflow-x-auto">
                            <table class="min-w-full divide-y divide-gray-200">
                                <thead class="bg-gray-50">
                                    <tr>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                                            <input type="checkbox">
                                        </th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Product</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Category</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Price</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Stock</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Actions</th>
                                    </tr>
                                </thead>
                                <tbody class="bg-white divide-y divide-gray-200">
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <input type="checkbox">
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="flex items-center">
                                                <div class="flex-shrink-0 h-10 w-10 bg-gray-200 rounded overflow-hidden">
                                                    <img src="https://m.media-amazon.com/images/I/61L1ItFgFHL._SL1500_.jpg" class="h-full w-full object-cover">
                                                </div>
                                                <div class="ml-4">
                                                    <div class="text-sm font-medium text-gray-900">Smartphone X3</div>
                                                    <div class="text-sm text-gray-500">#PRD-001</div>
                                                </div>
                                            </div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">Electronics</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">৳15,500</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">25</td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">Active</span>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                                            <a href="#" class="text-blue-500 hover:text-blue-700 mr-3"><i class="fas fa-edit"></i></a>
                                            <a href="#" class="text-red-500 hover:text-red-700"><i class="fas fa-trash"></i></a>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <input type="checkbox">
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="flex items-center">
                                                <div class="flex-shrink-0 h-10 w-10 bg-gray-200 rounded overflow-hidden">
                                                    <img src="https://m.media-amazon.com/images/I/81VJZ+8X1YL._AC_UL1500_.jpg" class="h-full w-full object-cover">
                                                </div>
                                                <div class="ml-4">
                                                    <div class="text-sm font-medium text-gray-900">Saree</div>
                                                    <div class="text-sm text-gray-500">#PRD-002</div>
                                                </div>
                                            </div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">Clothing</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">৳1,200</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">15</td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">Active</span>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                                            <a href="#" class="text-blue-500 hover:text-blue-700 mr-3"><i class="fas fa-edit"></i></a>
                                            <a href="#" class="text-red-500 hover:text-red-700"><i class="fas fa-trash"></i></a>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <input type="checkbox">
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="flex items-center">
                                                <div class="flex-shrink-0 h-10 w-10 bg-gray-200 rounded overflow-hidden">
                                                    <img src="https://m.media-amazon.com/images/I/71YHblzCgVL._SL1500_.jpg" class="h-full w-full object-cover">
                                                </div>
                                                <div class="ml-4">
                                                    <div class="text-sm font-medium text-gray-900">Pure Mustard Oil</div>
                                                    <div class="text-sm text-gray-500">#PRD-003</div>
                                                </div>
                                            </div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">Grocery</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">৳180</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">0</td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-red-100 text-red-800">Out of Stock</span>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                                            <a href="#" class="text-blue-500 hover:text-blue-700 mr-3"><i class="fas fa-edit"></i></a>
                                            <a href="#" class="text-red-500 hover:text-red-700"><i class="fas fa-trash"></i></a>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                       
                        <div class="p-4 border-t flex items-center justify-between">
                            <div class="text-sm text-gray-500">
                                Showing <span class="font-medium">1</span> to <span class="font-medium">3</span> of <span class="font-medium">15</span> products
                            </div>
                            <div class="flex space-x-1">
                                <button class="px-3 py-1 border rounded text-sm bg-gray-100">&laquo;</button>
                                <button class="px-3 py-1 border rounded text-sm bg-orange-500 text-white">1</button>
                                <button class="px-3 py-1 border rounded text-sm">2</button>
                                <button class="px-3 py-1 border rounded text-sm">3</button>
                                <button class="px-3 py-1 border rounded text-sm">&raquo;</button>
                            </div>
                        </div>
                    </div>
                </div>
               
                <!-- Orders Section -->
                <div id="orders-section" class="admin-section hidden">
                    <div class="flex justify-between items-center mb-6">
                        <h2 class="text-xl font-bold">Orders Management</h2>
                        <div class="flex items-center space-x-2">
                            <select class="border rounded px-3 py-1">
                                <option>Filter by Status</option>
                                <option>Pending</option>
                                <option>Processing</option>
                                <option>Completed</option>
                                <option>Cancelled</option>
                            </select>
                            <input type="date" class="border rounded px-3 py-1">
                        </div>
                    </div>
                   
                    <div class="bg-white rounded-lg shadow overflow-hidden">
                        <div class="overflow-x-auto">
                            <table class="min-w-full divide-y divide-gray-200">
                                <thead class="bg-gray-50">
                                    <tr>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Order ID</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Customer</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Date</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Amount</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Payment</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Actions</th>
                                    </tr>
                                </thead>
                                <tbody class="bg-white divide-y divide-gray-200">
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-orange-500">#ORD-1256</td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="text-sm font-medium text-gray-900">Rahim Khan</div>
                                            <div class="text-sm text-gray-500">01712-345678</div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">15 Jun 2023</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">৳1,250</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">Cash on Delivery</td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-yellow-100 text-yellow-800">Pending</span>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                                            <a href="#" class="text-blue-500 hover:text-blue-700 mr-3"><i class="fas fa-eye"></i></a>
                                            <a href="#" class="text-green-500 hover:text-green-700 mr-3"><i class="fas fa-check"></i></a>
                                            <a href="#" class="text-red-500 hover:text-red-700"><i class="fas fa-times"></i></a>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-orange-500">#ORD-1255</td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="text-sm font-medium text-gray-900">Fatema Begum</div>
                                            <div class="text-sm text-gray-500">01812-987654</div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">14 Jun 2023</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">৳2,850</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">bKash</td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-blue-100 text-blue-800">Processing</span>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                                            <a href="#" class="text-blue-500 hover:text-blue-700 mr-3"><i class="fas fa-eye"></i></a>
                                            <a href="#" class="text-green-500 hover:text-green-700 mr-3"><i class="fas fa-check"></i></a>
                                            <a href="#" class="text-red-500 hover:text-red-700"><i class="fas fa-times"></i></a>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-orange-500">#ORD-1254</td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="text-sm font-medium text-gray-900">Karim Uddin</div>
                                            <div class="text-sm text-gray-500">01912-456789</div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">13 Jun 2023</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">৳650</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">Cash on Delivery</td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">Completed</span>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                                            <a href="#" class="text-blue-500 hover:text-blue-700 mr-3"><i class="fas fa-eye"></i></a>
                                            <a href="#" class="text-green-500 hover:text-green-700 mr-3"><i class="fas fa-check"></i></a>
                                            <a href="#" class="text-red-500 hover:text-red-700"><i class="fas fa-times"></i></a>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                       
                        <div class="p-4 border-t flex items-center justify-between">
                            <div class="text-sm text-gray-500">
                                Showing <span class="font-medium">1</span> to <span class="font-medium">3</span> of <span class="font-medium">15</span> orders
                            </div>
                            <div class="flex space-x-1">
                                <button class="px-3 py-1 border rounded text-sm bg-gray-100">&laquo;</button>
                                <button class="px-3 py-1 border rounded text-sm bg-orange-500 text-white">1</button>
                                <button class="px-3 py-1 border rounded text-sm">2</button>
                                <button class="px-3 py-1 border rounded text-sm">3</button>
                                <button class="px-3 py-1 border rounded text-sm">&raquo;</button>
                            </div>
                        </div>
                    </div>
                </div>
               
                <!-- Customers Section -->
                <div id="customers-section" class="admin-section hidden">
                    <div class="flex justify-between items-center mb-6">
                        <h2 class="text-xl font-bold">Customers Management</h2>
                        <button class="bg-orange-500 text-white px-4 py-2 rounded hover:bg-orange-600">
                            <i class="fas fa-plus mr-2"></i> Add Customer
                        </button>
                    </div>
                   
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-6">
                        <div class="bg-white p-6 rounded-lg shadow">
                            <div class="flex items-center">
                                <div class="bg-blue-100 p-3 rounded-full text-blue-500 mr-4">
                                    <i class="fas fa-users fa-lg"></i>
                                </div>
                                <div>
                                    <p class="text-gray-500">Total Customers</p>
                                    <h3 class="text-2xl font-bold">89</h3>
                                </div>
                            </div>
                        </div>
                        <div class="bg-white p-6 rounded-lg shadow">
                            <div class="flex items-center">
                                <div class="bg-green-100 p-3 rounded-full text-green-500 mr-4">
                                    <i class="fas fa-shopping-cart fa-lg"></i>
                                </div>
                                <div>
                                    <p class="text-gray-500">Active Customers</p>
                                    <h3 class="text-2xl font-bold">72</h3>
                                </div>
                            </div>
                        </div>
                        <div class="bg-white p-6 rounded-lg shadow">
                            <div class="flex items-center">
                                <div class="bg-purple-100 p-3 rounded-full text-purple-500 mr-4">
                                    <i class="fas fa-chart-line fa-lg"></i>
                                </div>
                                <div>
                                    <p class="text-gray-500">New This Month</p>
                                    <h3 class="text-2xl font-bold">15</h3>
                                </div>
                            </div>
                        </div>
                    </div>
                   
                    <div class="bg-white rounded-lg shadow overflow-hidden">
                        <div class="p-4 border-b flex justify-between items-center">
                            <div class="relative">
                                <input type="text" placeholder="Search customers..." class="border rounded px-3 py-1 pl-8">
                                <i class="fas fa-search absolute left-3 top-2 text-gray-400"></i>
                            </div>
                        </div>
                       
                        <div class="overflow-x-auto">
                            <table class="min-w-full divide-y divide-gray-200">
                                <thead class="bg-gray-50">
                                    <tr>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Customer</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Contact</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Orders</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Total Spent</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Last Order</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Actions</th>
                                    </tr>
                                </thead>
                                <tbody class="bg-white divide-y divide-gray-200">
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="flex items-center">
                                                <div class="flex-shrink-0 h-10 w-10 bg-gray-200 rounded-full overflow-hidden">
                                                    <img src="https://randomuser.me/api/portraits/men/32.jpg" class="h-full w-full object-cover">
                                                </div>
                                                <div class="ml-4">
                                                    <div class="text-sm font-medium text-gray-900">Rahim Khan</div>
                                                    <div class="text-sm text-gray-500">rahim@example.com</div>
                                                </div>
                                            </div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">01712-345678</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">12</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">৳15,250</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">15 Jun 2023</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                                            <a href="#" class="text-blue-500 hover:text-blue-700 mr-3"><i class="fas fa-eye"></i></a>
                                            <a href="#" class="text-green-500 hover:text-green-700 mr-3"><i class="fas fa-edit"></i></a>
                                            <a href="#" class="text-red-500 hover:text-red-700"><i class="fas fa-trash"></i></a>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="flex items-center">
                                                <div class="flex-shrink-0 h-10 w-10 bg-gray-200 rounded-full overflow-hidden">
                                                    <img src="https://randomuser.me/api/portraits/women/44.jpg" class="h-full w-full object-cover">
                                                </div>
                                                <div class="ml-4">
                                                    <div class="text-sm font-medium text-gray-900">Fatema Begum</div>
                                                    <div class="text-sm text-gray-500">fatema@example.com</div>
                                                </div>
                                            </div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">01812-987654</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">8</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">৳9,850</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">14 Jun 2023</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                                            <a href="#" class="text-blue-500 hover:text-blue-700 mr-3"><i class="fas fa-eye"></i></a>
                                            <a href="#" class="text-green-500 hover:text-green-700 mr-3"><i class="fas fa-edit"></i></a>
                                            <a href="#" class="text-red-500 hover:text-red-700"><i class="fas fa-trash"></i></a>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="flex items-center">
                                                <div class="flex-shrink-0 h-10 w-10 bg-gray-200 rounded-full overflow-hidden">
                                                    <img src="https://randomuser.me/api/portraits/men/67.jpg" class="h-full w-full object-cover">
                                                </div>
                                                <div class="ml-4">
                                                    <div class="text-sm font-medium text-gray-900">Karim Uddin</div>
                                                    <div class="text-sm text-gray-500">karim@example.com</div>
                                                </div>
                                            </div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">01912-456789</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">5</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">৳6,750</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">13 Jun 2023</td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                                            <a href="#" class="text-blue-500 hover:text-blue-700 mr-3"><i class="fas fa-eye"></i></a>
                                            <a href="#" class="text-green-500 hover:text-green-700 mr-3"><i class="fas fa-edit"></i></a>
                                            <a href="#" class="text-red-500 hover:text-red-700"><i class="fas fa-trash"></i></a>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                       
                        <div class="p-4 border-t flex items-center justify-between">
                            <div class="text-sm text-gray-500">
                                Showing <span class="font-medium">1</span> to <span class="font-medium">3</span> of <span class="font-medium">89</span> customers
                            </div>
                            <div class="flex space-x-1">
                                <button class="px-3 py-1 border rounded text-sm bg-gray-100">&laquo;</button>
                                <button class="px-3 py-1 border rounded text-sm bg-orange-500 text-white">1</button>
                                <button class="px-3 py-1 border rounded text-sm">2</button>
                                <button class="px-3 py-1 border rounded text-sm">3</button>
                                <button class="px-3 py-1 border rounded text-sm">&raquo;</button>
                            </div>
                        </div>
                    </div>
                </div>
               
                <!-- Categories Section -->
                <div id="categories-section" class="admin-section hidden">
                    <div class="flex justify-between items-center mb-6">
                        <h2 class="text-xl font-bold">Categories Management</h2>
                        <button onclick="showCategoryModal()" class="bg-orange-500 text-white px-4 py-2 rounded hover:bg-orange-600">
                            <i class="fas fa-plus mr-2"></i> Add Category
                        </button>
                    </div>
                   
                    <div class="bg-white rounded-lg shadow overflow-hidden">
                        <div class="overflow-x-auto">
                            <table class="min-w-full divide-y divide-gray-200">
                                <thead class="bg-gray-50">
                                    <tr>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Category</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Products</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                                        <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Actions</th>
                                    </tr>
                                </thead>
                                <tbody class="bg-white divide-y divide-gray-200">
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="flex items-center">
                                                <div class="flex-shrink-0 h-10 w-10 bg-gray-200 rounded-full flex items-center justify-center">
                                                    📱
                                                </div>
                                                <div class="ml-4">
                                                    <div class="text-sm font-medium text-gray-900">Electronics</div>
                                                </div>
                                            </div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">15</td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">Active</span>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                                            <a href="#" class="text-blue-500 hover:text-blue-700 mr-3"><i class="fas fa-edit"></i></a>
                                            <a href="#" class="text-red-500 hover:text-red-700"><i class="fas fa-trash"></i></a>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="flex items-center">
                                                <div class="flex-shrink-0 h-10 w-10 bg-gray-200 rounded-full flex items-center justify-center">
                                                    👕
                                                </div>
                                                <div class="ml-4">
                                                    <div class="text-sm font-medium text-gray-900">Clothing</div>
                                                </div>
                                            </div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">12</td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">Active</span>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                                            <a href="#" class="text-blue-500 hover:text-blue-700 mr-3"><i class="fas fa-edit"></i></a>
                                            <a href="#" class="text-red-500 hover:text-red-700"><i class="fas fa-trash"></i></a>
                                        </td>
                                    </tr>
                                    <tr>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <div class="flex items-center">
                                                <div class="flex-shrink-0 h-10 w-10 bg-gray-200 rounded-full flex items-center justify-center">
                                                    🛒
                                                </div>
                                                <div class="ml-4">
                                                    <div class="text-sm font-medium text-gray-900">Grocery</div>
                                                </div>
                                            </div>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">10</td>
                                        <td class="px-6 py-4 whitespace-nowrap">
                                            <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">Active</span>
                                        </td>
                                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                                            <a href="#" class="text-blue-500 hover:text-blue-700 mr-3"><i class="fas fa-edit"></i></a>
                                            <a href="#" class="text-red-500 hover:text-red-700"><i class="fas fa-trash"></i></a>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
               
                <!-- Reports Section -->
                <div id="reports-section" class="admin-section hidden">
                    <div class="flex justify-between items-center mb-6">
                        <h2 class="text-xl font-bold">Reports & Analytics</h2>
                        <div class="flex items-center space-x-2">
                            <select class="border rounded px-3 py-1">
                                <option>Last 7 Days</option>
                                <option>Last Month</option>
                                <option selected>Last Year</option>
                            </select>
                            <button class="bg-orange-500 text-white px-3 py-1 rounded">
                                <i class="fas fa-download mr-1"></i> Export
                            </button>
                        </div>
                    </div>
                   
                    <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 mb-6">
                        <div class="bg-white p-6 rounded-lg shadow">
                            <h3 class="font-bold mb-4">Sales Report</h3>
                            <div class="h-64 bg-gray-100 rounded flex items-center justify-center">
                                [Sales Chart Placeholder]
                            </div>
                        </div>
                        <div class="bg-white p-6 rounded-lg shadow">
                            <h3 class="font-bold mb-4">Revenue Report</h3>
                            <div class="h-64 bg-gray-100 rounded flex items-center justify-center">
                                [Revenue Chart Placeholder]
                            </div>
                        </div>
                    </div>
                   
                    <div class="bg-white p-6 rounded-lg shadow mb-6">
                        <h3 class="font-bold mb-4">Top Selling Products</h3>
                        <div class="h-64 bg-gray-100 rounded flex items-center justify-center">
                            [Products Chart Placeholder]
                        </div>
                    </div>
                   
                    <div class="bg-white p-6 rounded-lg shadow">
                        <h3 class="font-bold mb-4">Customer Acquisition</h3>
                        <div class="h-64 bg-gray-100 rounded flex items-center justify-center">
                            [Customers Chart Placeholder]
                        </div>
                    </div>
                </div>
               
                <!-- Settings Section -->
                <div id="settings-section" class="admin-section hidden">
                    <h2 class="text-xl font-bold mb-6">Settings</h2>
                   
                    <div class="bg-white rounded-lg shadow overflow-hidden mb-6">
                        <div class="p-4 border-b">
                            <h3 class="font-bold">Shop Information</h3>
                        </div>
                        <div class="p-6">
                            <form>
                                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                                    <div>
                                        <label class="block text-sm font-medium text-gray-700 mb-1">Shop Name</label>
                                        <input type="text" class="w-full border rounded px-3 py-2" value="Chilmari E-shop">
                                    </div>
                                    <div>
                                        <label class="block text-sm font-medium text-gray-700 mb-1">Shop Email</label>
                                        <input type="email" class="w-full border rounded px-3 py-2" value="info@chilmari-eshop.com">
                                    </div>
                                    <div>
                                        <label class="block text-sm font-medium text-gray-700 mb-1">Shop Phone</label>
                                        <input type="tel" class="w-full border rounded px-3 py-2" value="01770706309">
                                    </div>
                                    <div>
                                        <label class="block text-sm font-medium text-gray-700 mb-1">Shop Address</label>
                                        <input type="text" class="w-full border rounded px-3 py-2" value="Chilmari, Kurigram, Bangladesh">
                                    </div>
                                </div>
                                <div class="mt-6">
                                    <button type="submit" class="bg-orange-500 text-white px-4 py-2 rounded hover:bg-orange-600">
                                        Save Changes
                                    </button>
                                </div>
                            </form>
                        </div>
                    </div>
                   
                    <div class="bg-white rounded-lg shadow overflow-hidden mb-6">
                        <div class="p-4 border-b">
                            <h3 class="font-bold">Payment Methods</h3>
                        </div>
                        <div class="p-6">
                            <div class="space-y-4">
                                <div class="flex items-center justify-between p-3 border rounded">
                                    <div class="flex items-center">
                                        <div class="bg-gray-100 p-2 rounded mr-3">
                                            <i class="fas fa-money-bill-wave text-green-500"></i>
                                        </div>
                                        <div>
                                            <h4 class="font-medium">Cash on Delivery</h4>
                                            <p class="text-sm text-gray-500">Pay when you receive the product</p>
                                        </div>
                                    </div>
                                    <label class="relative inline-flex items-center cursor-pointer">
                                        <input type="checkbox" checked class="sr-only peer">
                                        <div class="w-11 h-6 bg-gray-200 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-orange-500"></div>
                                    </label>
                                </div>
                                <div class="flex items-center justify-between p-3 border rounded">
                                    <div class="flex items-center">
                                        <div class="bg-gray-100 p-2 rounded mr-3">
                                            <i class="fas fa-mobile-alt text-blue-500"></i>
                                        </div>
                                        <div>
                                            <h4 class="font-medium">bKash</h4>
                                            <p class="text-sm text-gray-500">Mobile banking payment</p>
                                        </div>
                                    </div>
                                    <label class="relative inline-flex items-center cursor-pointer">
                                        <input type="checkbox" checked class="sr-only peer">
                                        <div class="w-11 h-6 bg-gray-200 peer-focus:outline-none rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-orange-500"></div>
                                    </label>
                                </div>
                                <div class="flex items-center justify-between p-3 border rounded">
                                    <div class="flex items-center">
                                        <div class="bg-gray-100 p-2 rounded mr-3">
                                            <i class="fas fa-credit-card text-purple-500"></i>
                                        </div>
                                        <div>
                                            <h4 class="font-medium">Credit/Debit Card</h4>
                                            <p class="text-sm text-gray-500">Coming soon</p>
                                        </div>
                                    </div>
                                    <label class="relative inline-flex items-center cursor-pointer">
                                        <input type="checkbox" disabled class="sr-only peer">
                                        <div class="w-11 h-6 bg-gray-200 rounded-full peer peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-gray-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-gray-500"></div>
                                    </label>
                                </div>
                            </div>
                        </div>
                    </div>
                   
                    <div class="bg-white rounded-lg shadow overflow-hidden">
                        <div class="p-4 border-b">
                            <h3 class="font-bold">Delivery Settings</h3>
                        </div>
                        <div class="p-6">
                            <form>
                                <div class="mb-4">
                                    <label class="block text-sm font-medium text-gray-700 mb-1">Delivery Charge</label>
                                    <input type="number" class="w-full border rounded px-3 py-2" value="50">
                                </div>
                                <div class="mb-4">
                                    <label class="block text-sm font-medium text-gray-700 mb-1">Delivery Areas</label>
                                    <div class="border rounded p-2">
                                        <div class="flex items-center mb-2">
                                            <input type="checkbox" checked class="mr-2">
                                            <span>Chilmari</span>
                                        </div>
                                        <div class="flex items-center mb-2">
                                            <input type="checkbox" class="mr-2">
                                            <span>Kurigram</span>
                                        </div>
                                        <div class="flex items-center">
                                            <input type="checkbox" class="mr-2">
                                            <span>Other Areas</span>
                                        </div>
                                    </div>
                                </div>
                                <div>
                                    <button type="submit" class="bg-orange-500 text-white px-4 py-2 rounded hover:bg-orange-600">
                                        Save Changes
                                    </button>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Add Product Modal -->
    <div id="product-modal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg shadow-lg w-full max-w-2xl max-h-screen overflow-y-auto">
            <div class="p-4 border-b flex justify-between items-center">
                <h3 class="text-lg font-bold">Add New Product</h3>
                <button onclick="hideModal('product-modal')" class="text-gray-500 hover:text-gray-700">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div class="p-6">
                <form>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-1">Product Name</label>
                            <input type="text" class="w-full border rounded px-3 py-2" required>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-1">Category</label>
                            <select class="w-full border rounded px-3 py-2" required>
                                <option value="">Select Category</option>
                                <option>Electronics</option>
                                <option>Clothing</option>
                                <option>Grocery</option>
                                <option>Household</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-1">Price (৳)</label>
                            <input type="number" class="w-full border rounded px-3 py-2" required>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-1">Stock Quantity</label>
                            <input type="number" class="w-full border rounded px-3 py-2" required>
                        </div>
                        <div class="md:col-span-2">
                            <label class="block text-sm font-medium text-gray-700 mb-1">Description</label>
                            <textarea class="w-full border rounded px-3 py-2" rows="3"></textarea>
                        </div>
                        <div class="md:col-span-2">
                            <label class="block text-sm font-medium text-gray-700 mb-1">Product Images</label>
                            <div class="border-2 border-dashed rounded p-4 text-center">
                                <div class="flex justify-center mb-2">
                                    <i class="fas fa-cloud-upload-alt text-3xl text-gray-400"></i>
                                </div>
                                <p class="text-sm text-gray-500">Drag & drop images here or click to browse</p>
                                <input type="file" class="hidden" multiple>
                            </div>
                        </div>
                    </div>
                    <div class="mt-6 flex justify-end space-x-3">
                        <button type="button" onclick="hideModal('product-modal')" class="px-4 py-2 border rounded hover:bg-gray-100">
                            Cancel
                        </button>
                        <button type="submit" class="bg-orange-500 text-white px-4 py-2 rounded hover:bg-orange-600">
                            Save Product
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <!-- Add Category Modal -->
    <div id="category-modal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 hidden">
        <div class="bg-white rounded-lg shadow-lg w-full max-w-md">
            <div class="p-4 border-b flex justify-between items-center">
                <h3 class="text-lg font-bold">Add New Category</h3>
                <button onclick="hideModal('category-modal')" class="text-gray-500 hover:text-gray-700">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            <div class="p-6">
                <form>
                    <div class="mb-4">
                        <label class="block text-sm font-medium text-gray-700 mb-1">Category Name</label>
                        <input type="text" class="w-full border rounded px-3 py-2" required>
                    </div>
                    <div class="mb-4">
                        <label class="block text-sm font-medium text-gray-700 mb-1">Icon</label>
                        <div class="grid grid-cols-5 gap-2">
                            <button type="button" class="p-2 border rounded hover:bg-gray-100">📱</button>
                            <button type="button" class="p-2 border rounded hover:bg-gray-100">👕</button>
                            <button type="button" class="p-2 border rounded hover:bg-gray-100">🛒</button>
                            <button type="button" class="p-2 border rounded hover:bg-gray-100">🏠</button>
                            <button type="button" class="p-2 border rounded hover:bg-gray-100">🍎</button>
                        </div>
                    </div>
                    <div class="mb-4">
                        <label class="block text-sm font-medium text-gray-700 mb-1">Status</label>
                        <select class="w-full border rounded px-3 py-2" required>
                            <option value="active">Active</option>
                            <option value="inactive">Inactive</option>
                        </select>
                    </div>
                    <div class="flex justify-end space-x-3">
                        <button type="button" onclick="hideModal('category-modal')" class="px-4 py-2 border rounded hover:bg-gray-100">
                            Cancel
                        </button>
                        <button type="submit" class="bg-orange-500 text-white px-4 py-2 rounded hover:bg-orange-600">
                            Save Category
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>

    <script>
        // Toggle sidebar
        function toggleSidebar() {
            const sidebar = document.getElementById('sidebar');
            const content = document.getElementById('content-area');
           
            sidebar.classList.toggle('sidebar-collapsed');
            content.classList.toggle('content-collapsed');
        }

        // Show admin section
        function showAdminSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.admin-section').forEach(section => {
                section.classList.add('hidden');
            });
           
            // Show selected section
            document.getElementById(`${sectionId}-section`).classList.remove('hidden');
           
            // Update active menu
            document.querySelectorAll('.menu-item').forEach(item => {
                item.classList.remove('active-menu');
            });
           
            // Set current menu as active
            const menuItem = document.querySelector(`.menu-item[onclick="showAdminSection('${sectionId}')"]`);
            if (menuItem) {
                menuItem.classList.add('active-menu');
            }
           
            // Update section title
            const titleMap = {
                'dashboard': 'Dashboard',
                'products': 'Products Management',
                'orders': 'Orders Management',
                'customers': 'Customers Management',
                'categories': 'Categories Management',
                'reports': 'Reports & Analytics',
                'settings': 'Settings'
            };
           
            document.getElementById('admin-section-title').textContent = titleMap[sectionId];
        }

        // Show product modal
        function showProductModal() {
            document.getElementById('product-modal').classList.remove('hidden');
        }

        // Show category modal
        function showCategoryModal() {
            document.getElementById('category-modal').classList.remove('hidden');
        }

        // Hide modal
        function hideModal(modalId) {
            document.getElementById(modalId).classList.add('hidden');
        }

        // Initialize the admin panel
        document.addEventListener('DOMContentLoaded', function() {
            showAdminSection('dashboard');
        });
    </script>
