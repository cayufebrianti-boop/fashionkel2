<html lang="id" class="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GayaKita - Toko Fashion Modern</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Tailwind Config for Dark Mode & Colors -->
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        primary: '#4F46E5', // Indigo 600
                        secondary: '#10B981', // Emerald 500
                    }
                }
            }
        }
    </script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* Animasi Kustom */
        .fade-in {
            animation: fadeIn 0.4s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* Notifikasi Toast */
        #toast {
            visibility: hidden;
            min-width: 250px;
            background-color: #333;
            color: #fff;
            text-align: center;
            border-radius: 8px;
            padding: 16px;
            position: fixed;
            z-index: 50;
            left: 50%;
            bottom: 30px;
            transform: translateX(-50%);
            opacity: 0;
            transition: opacity 0.3s, bottom 0.3s;
        }
        #toast.show {
            visibility: visible;
            opacity: 1;
            bottom: 50px;
        }

        .no-scrollbar::-webkit-scrollbar { display: none; }
        .no-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
    </style>
</head>
<body class="bg-gray-50 text-gray-800 dark:bg-gray-900 dark:text-gray-200 transition-colors duration-300 min-h-screen flex flex-col">

    <!-- Navigasi -->
    <nav class="bg-white dark:bg-gray-800 shadow-md sticky top-0 z-40 transition-colors duration-300">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16">
                <!-- Logo & Menu Desktop -->
                <div class="flex items-center">
                    <a href="#" onclick="navigate('home')" class="flex-shrink-0 flex items-center cursor-pointer">
                        <i class="fas fa-shopping-bag text-primary text-2xl mr-2"></i>
                        <span class="font-bold text-xl tracking-wider text-primary dark:text-indigo-400">GayaKita</span>
                    </a>
                    <div class="hidden md:ml-6 md:flex md:space-x-4">
                        <a href="#" onclick="navigate('home')" class="text-gray-600 dark:text-gray-300 hover:text-primary px-3 py-2 rounded-md text-sm font-medium transition">Beranda</a>
                        <a href="#" onclick="navigate('products')" class="text-gray-600 dark:text-gray-300 hover:text-primary px-3 py-2 rounded-md text-sm font-medium transition">Produk</a>
                        <a href="#" onclick="navigate('about')" class="text-gray-600 dark:text-gray-300 hover:text-primary px-3 py-2 rounded-md text-sm font-medium transition">Tentang Kami</a>
                        <a href="#" onclick="navigate('contact')" class="text-gray-600 dark:text-gray-300 hover:text-primary px-3 py-2 rounded-md text-sm font-medium transition">Kontak</a>
                    </div>
                </div>

                <!-- Ikon Kanan -->
                <div class="flex items-center space-x-4">
                    <button onclick="toggleDarkMode()" class="text-gray-500 hover:text-primary dark:text-gray-300 transition" title="Ganti Tema">
                        <i id="theme-icon" class="fas fa-moon"></i>
                    </button>

                    <button onclick="navigate('cart')" class="text-gray-500 hover:text-primary dark:text-gray-300 relative transition cursor-pointer" title="Keranjang">
                        <i class="fas fa-shopping-cart text-xl"></i>
                        <span id="cart-count" class="absolute -top-2 -right-2 bg-red-500 text-white text-xs rounded-full h-5 w-5 flex items-center justify-center">0</span>
                    </button>

                    <button id="user-btn" onclick="navigate('login')" class="hidden md:flex items-center text-gray-500 hover:text-primary dark:text-gray-300 transition font-medium text-sm">
                        <i class="fas fa-user mr-1"></i> <span id="user-text">Masuk</span>
                    </button>

                    <div class="md:hidden flex items-center">
                        <button onclick="toggleMobileMenu()" class="text-gray-500 hover:text-primary focus:outline-none">
                            <i class="fas fa-bars text-xl"></i>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Menu Mobile -->
        <div id="mobile-menu" class="hidden md:hidden bg-white dark:bg-gray-800 border-t dark:border-gray-700">
            <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
                <a href="#" onclick="navigate('home'); toggleMobileMenu()" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 dark:text-gray-200">Beranda</a>
                <a href="#" onclick="navigate('products'); toggleMobileMenu()" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 dark:text-gray-200">Produk</a>
                <a href="#" onclick="navigate('about'); toggleMobileMenu()" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 dark:text-gray-200">Tentang Kami</a>
                <a href="#" onclick="navigate('contact'); toggleMobileMenu()" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 dark:text-gray-200">Kontak</a>
                <a href="#" onclick="navigate('login'); toggleMobileMenu()" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 dark:text-gray-200 font-bold">Masuk</a>
            </div>
        </div>
    </nav>

    <!-- AREA KONTEN UTAMA -->
    <main class="flex-grow w-full max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        
        <!-- 1. HALAMAN HOME -->
        <section id="view-home" class="page-view fade-in">
            <div class="relative bg-primary rounded-2xl overflow-hidden shadow-xl mb-12 h-64 md:h-96 flex items-center justify-center">
                <div class="absolute inset-0">
                    <img src="https://images.unsplash.com/photo-1441986300917-64674bd600d8?w=1200&q=80" alt="[Gambar Hero Toko Fashion]" class="w-full h-full object-cover opacity-40 mix-blend-multiply">
                </div>
                <div class="relative text-center px-4">
                    <h1 class="text-3xl md:text-5xl font-extrabold text-white mb-4">GayaKita. Ekspresikan Dirimu.</h1>
                    <p class="text-indigo-100 text-lg mb-8 max-w-lg mx-auto">Koleksi pilihan untuk menunjang penampilan harian Anda dengan kualitas premium.</p>
                    <button onclick="navigate('products')" class="bg-white text-primary font-bold py-3 px-8 rounded-full hover:bg-gray-100 transition shadow-lg">Belanja Sekarang</button>
                </div>
            </div>

            <div class="mb-12">
                <h2 class="text-2xl font-bold mb-6">Highlight Produk</h2>
                <div id="featured-products-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6"></div>
            </div>
        </section>

        <!-- 2. HALAMAN PRODUK -->
        <section id="view-products" class="page-view hidden fade-in">
            <div class="flex flex-col md:flex-row justify-between items-center mb-8 gap-4">
                <h1 class="text-3xl font-bold">Koleksi Kami</h1>
                <div class="flex w-full md:w-auto gap-2">
                    <input type="text" id="search-input" placeholder="Cari produk..." class="border rounded-lg px-4 py-2 flex-grow dark:bg-gray-800 dark:border-gray-700">
                    <select id="category-filter" class="border rounded-lg px-4 py-2 dark:bg-gray-800 dark:border-gray-700">
                        <option value="all">Semua</option>
                        <option value="Pria">Pria</option>
                        <option value="Wanita">Wanita</option>
                        <option value="Aksesoris">Aksesoris</option>
                    </select>
                </div>
            </div>
            <div id="all-products-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6"></div>
        </section>

        <!-- 3. HALAMAN DETAIL PRODUK -->
        <section id="view-detail" class="page-view hidden fade-in">
            <div class="bg-white dark:bg-gray-800 rounded-2xl shadow-lg p-6 md:flex gap-8">
                <div class="md:w-1/2">
                    <img id="detail-img" src="" alt="[Detail Produk]" class="w-full rounded-xl object-cover h-96">
                </div>
                <div class="md:w-1/2 flex flex-col justify-center mt-6 md:mt-0">
                    <span id="detail-category" class="text-primary font-bold uppercase text-sm"></span>
                    <h1 id="detail-name" class="text-3xl font-bold my-2"></h1>
                    <p id="detail-price" class="text-2xl font-bold text-secondary mb-4"></p>
                    <p id="detail-desc" class="text-gray-600 dark:text-gray-400 mb-6"></p>
                    <p class="mb-6">Stok Tersisa: <span id="detail-stock" class="font-bold"></span></p>
                    <button id="btn-add-to-cart" class="bg-primary text-white font-bold py-3 px-6 rounded-lg hover:bg-indigo-700 transition">Tambah ke Keranjang</button>
                </div>
            </div>
        </section>

        <!-- 4. HALAMAN KERANJANG -->
        <section id="view-cart" class="page-view hidden fade-in">
            <h1 class="text-2xl font-bold mb-6">Keranjang Belanja</h1>
            <div class="grid lg:grid-cols-3 gap-8">
                <div id="cart-items-container" class="lg:col-span-2 space-y-4"></div>
                <div class="bg-white dark:bg-gray-800 p-6 rounded-xl shadow-md h-fit">
                    <h2 class="text-lg font-bold mb-4">Ringkasan Pesanan</h2>
                    <div class="flex justify-between mb-4">
                        <span>Total:</span>
                        <span id="cart-total" class="font-bold text-xl text-primary">Rp 0</span>
                    </div>
                    <button onclick="navigate('checkout')" class="w-full bg-secondary text-white font-bold py-3 rounded-lg">Checkout</button>
                </div>
            </div>
        </section>

        <!-- 5. HALAMAN CHECKOUT -->
        <section id="view-checkout" class="page-view hidden fade-in">
            <div class="max-w-3xl mx-auto bg-white dark:bg-gray-800 p-8 rounded-xl shadow-lg">
                <h1 class="text-2xl font-bold mb-6">Simulasi Checkout</h1>
                <form onsubmit="event.preventDefault(); showSuccess();" class="space-y-4">
                    <input type="text" placeholder="Nama Lengkap" required class="w-full border p-3 rounded dark:bg-gray-700 dark:border-gray-600">
                    <input type="text" placeholder="Alamat Lengkap" required class="w-full border p-3 rounded dark:bg-gray-700 dark:border-gray-600">
                    <select class="w-full border p-3 rounded dark:bg-gray-700 dark:border-gray-600">
                        <option>Transfer Bank</option>
                        <option>E-Wallet (Dana/OVO)</option>
                        <option>Bayar di Tempat (COD)</option>
                    </select>
                    <div class="bg-gray-50 dark:bg-gray-700 p-4 rounded-lg">
                        <p class="font-bold">Total Pembayaran: <span id="checkout-total" class="text-primary"></span></p>
                    </div>
                    <button type="submit" class="w-full bg-primary text-white font-bold py-3 rounded-lg">Selesaikan Pesanan</button>
                </form>
            </div>
        </section>

        <!-- 6. HALAMAN TENTANG KAMI -->
        <section id="view-about" class="page-view hidden fade-in">
            <div class="text-center mb-12">
                <h1 class="text-4xl font-bold text-primary mb-4">Tim Kami</h1>
                <p class="text-gray-500">Kelompok 2 - Digital Entrepreneurship</p>
            </div>
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-4">
                <!-- Anggota 1 -->
                <div class="bg-white dark:bg-gray-800 p-6 rounded-xl shadow text-center border dark:border-gray-700">
                    <img src="https://ui-avatars.com/api/?name=Aluna&background=4F46E5&color=fff" class="w-20 h-20 rounded-full mx-auto mb-4" alt="[Foto Aluna]">
                    <h3 class="font-bold">Aluna</h3>
                    <p class="text-xs text-primary font-bold">Project Manager</p>
                </div>
                <!-- Anggota 2 -->
                <div class="bg-white dark:bg-gray-800 p-6 rounded-xl shadow text-center border dark:border-gray-700">
                    <img src="https://ui-avatars.com/api/?name=Juvita&background=10B981&color=fff" class="w-20 h-20 rounded-full mx-auto mb-4" alt="[Foto Juvita]">
                    <h3 class="font-bold">Juvita</h3>
                    <p class="text-xs text-secondary font-bold">Developer</p>
                </div>
                <!-- Anggota 3 -->
                <div class="bg-white dark:bg-gray-800 p-6 rounded-xl shadow text-center border dark:border-gray-700">
                    <img src="https://ui-avatars.com/api/?name=Ghandis&background=F59E0B&color=fff" class="w-20 h-20 rounded-full mx-auto mb-4" alt="[Foto Ghandis]">
                    <h3 class="font-bold">Ghandis</h3>
                    <p class="text-xs text-yellow-600 font-bold">Designer</p>
                </div>
                <!-- Anggota 4 -->
                <div class="bg-white dark:bg-gray-800 p-6 rounded-xl shadow text-center border dark:border-gray-700">
                    <img src="https://ui-avatars.com/api/?name=Anisa&background=EC4899&color=fff" class="w-20 h-20 rounded-full mx-auto mb-4" alt="[Foto Anisa]">
                    <h3 class="font-bold">Anisa</h3>
                    <p class="text-xs text-pink-600 font-bold">Content Creator</p>
                </div>
                <!-- Anggota 5 -->
                <div class="bg-white dark:bg-gray-800 p-6 rounded-xl shadow text-center border dark:border-gray-700">
                    <img src="https://ui-avatars.com/api/?name=Candra&background=8B5CF6&color=fff" class="w-20 h-20 rounded-full mx-auto mb-4" alt="[Foto Candra]">
                    <h3 class="font-bold">Candra</h3>
                    <p class="text-xs text-purple-600 font-bold">Marketing</p>
                </div>
            </div>
            <div class="mt-12 bg-white dark:bg-gray-800 p-8 rounded-xl shadow">
                <h2 class="text-2xl font-bold mb-4">Visi & Misi</h2>
                <p class="mb-4"><b>Visi:</b> Menjadi pilihan utama dalam gaya hidup modern masyarakat Indonesia.</p>
                <p><b>Misi:</b> Menyediakan pakaian berkualitas dengan harga kompetitif dan pelayanan pelanggan yang responsif.</p>
            </div>
        </section>

        <!-- 7. HALAMAN KONTAK -->
        <section id="view-contact" class="page-view hidden fade-in">
            <div class="max-w-2xl mx-auto bg-white dark:bg-gray-800 p-8 rounded-xl shadow-lg">
                <h1 class="text-2xl font-bold mb-6">Hubungi Kami</h1>
                <div class="space-y-4 mb-8">
                    <p><i class="fab fa-whatsapp text-green-500 mr-2"></i> WA: +62 812-3456-7890</p>
                    <p><i class="fas fa-envelope text-red-500 mr-2"></i> Email: halo@gayakita.com</p>
                </div>
                <form onsubmit="event.preventDefault(); showToast('Pesan dikirim!'); this.reset();" class="space-y-4">
                    <input type="text" placeholder="Subjek Pesan" class="w-full border p-3 rounded dark:bg-gray-700 dark:border-gray-600">
                    <textarea placeholder="Pesan Anda..." rows="4" class="w-full border p-3 rounded dark:bg-gray-700 dark:border-gray-600"></textarea>
                    <button class="bg-primary text-white font-bold py-3 px-8 rounded-lg w-full">Kirim</button>
                </form>
            </div>
        </section>

        <!-- LOGIN SIMULASI -->
        <section id="view-login" class="page-view hidden fade-in">
            <div class="max-w-sm mx-auto bg-white dark:bg-gray-800 p-8 rounded-xl shadow-lg mt-10">
                <h1 class="text-2xl font-bold mb-6 text-center">Masuk ke GayaKita</h1>
                <form onsubmit="handleLogin(event)" class="space-y-4">
                    <input type="text" id="login-input" placeholder="Nama/Email" class="w-full border p-3 rounded dark:bg-gray-700">
                    <input type="password" placeholder="Password" class="w-full border p-3 rounded dark:bg-gray-700">
                    <button class="w-full bg-primary text-white font-bold py-3 rounded-lg">Masuk</button>
                </form>
            </div>
        </section>
    </main>

    <footer class="bg-white dark:bg-gray-800 border-t dark:border-gray-700 py-6 text-center text-sm text-gray-500">
        <p>© 2023 GayaKita - Proyek Kelompok Digital</p>
    </footer>

    <div id="toast"></div>

    <script>
        const products = [
            { id: 1, name: "Kemeja Flanel Biru", price: 150000, category: "Pria", stock: 10, img: "https://images.unsplash.com/photo-1598033129183-c4f50c736f10?w=500&q=80", desc: "Bahan nyaman dan motif klasik." },
            { id: 2, name: "T-Shirt Putih Polos", price: 85000, category: "Pria", stock: 25, img: "https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?w=500&q=80", desc: "Cotton combed 30s premium." },
            { id: 3, name: "Blouse Wanita Pink", price: 125000, category: "Wanita", stock: 5, img: "https://images.unsplash.com/photo-1503342217505-b0a15ec3261c?w=500&q=80", desc: "Sempurna untuk acara formal." },
            { id: 4, name: "Jaket Denim", price: 250000, category: "Pria", stock: 8, img: "https://images.unsplash.com/photo-1495105787522-5334e3ffa0ef?w=500&q=80", desc: "Denim tebal dan tahan lama." },
            { id: 5, name: "Topi Baseball", price: 45000, category: "Aksesoris", stock: 50, img: "https://images.unsplash.com/photo-1588850561407-ed78c282e89b?w=500&q=80", desc: "Adjustable strap." },
            { id: 6, name: "Tas Ransel Kanvas", price: 180000, category: "Aksesoris", stock: 12, img: "https://images.unsplash.com/photo-1553062407-98eeb64c6a62?w=500&q=80", desc: "Kapasitas besar 20L." }
        ];

        let state = { cart: [], user: null };

        function navigate(view, id = null) {
            document.querySelectorAll('.page-view').forEach(v => v.classList.add('hidden'));
            document.getElementById('view-' + view).classList.remove('hidden');
            window.scrollTo(0,0);
            if(view === 'detail') renderDetail(id);
            if(view === 'products') renderProducts();
            if(view === 'home') renderHome();
            if(view === 'cart') renderCart();
            if(view === 'checkout') {
                const total = state.cart.reduce((s, i) => s + (i.price * i.qty), 0);
                document.getElementById('checkout-total').innerText = "Rp " + total.toLocaleString();
            }
        }

        function renderHome() {
            const grid = document.getElementById('featured-products-grid');
            grid.innerHTML = products.slice(0,4).map(p => createCard(p)).join('');
        }

        function renderProducts() {
            const grid = document.getElementById('all-products-grid');
            const search = document.getElementById('search-input').value.toLowerCase();
            const cat = document.getElementById('category-filter').value;
            const filtered = products.filter(p => p.name.toLowerCase().includes(search) && (cat === 'all' || p.category === cat));
            grid.innerHTML = filtered.map(p => createCard(p)).join('');
        }

        function createCard(p) {
            return `
                <div class="bg-white dark:bg-gray-800 rounded-xl shadow overflow-hidden border dark:border-gray-700">
                    <img src="${p.img}" class="w-full h-48 object-cover" alt="[Produk ${p.name}]">
                    <div class="p-4">
                        <h3 class="font-bold truncate">${p.name}</h3>
                        <p class="text-secondary font-bold">Rp ${p.price.toLocaleString()}</p>
                        <div class="flex gap-2 mt-4">
                            <button onclick="navigate('detail', ${p.id})" class="flex-1 border border-primary text-primary text-xs py-2 rounded transition hover:bg-primary hover:text-white">Detail</button>
                            <button onclick="addToCart(${p.id})" class="flex-1 bg-primary text-white text-xs py-2 rounded transition hover:bg-indigo-700">Beli</button>
                        </div>
                    </div>
                </div>
            `;
        }

        function renderDetail(id) {
            const p = products.find(x => x.id === id);
            document.getElementById('detail-img').src = p.img;
            document.getElementById('detail-name').innerText = p.name;
            document.getElementById('detail-price').innerText = "Rp " + p.price.toLocaleString();
            document.getElementById('detail-desc').innerText = p.desc;
            document.getElementById('detail-category').innerText = p.category;
            document.getElementById('detail-stock').innerText = p.stock;
            document.getElementById('btn-add-to-cart').onclick = () => addToCart(p.id);
        }

        function addToCart(id) {
            const p = products.find(x => x.id === id);
            const exist = state.cart.find(x => x.id === id);
            if(exist) exist.qty++;
            else state.cart.push({...p, qty: 1});
            updateBadge();
            showToast(p.name + " ditambah ke keranjang!");
        }

        function updateBadge() {
            const count = state.cart.reduce((s, i) => s + i.qty, 0);
            document.getElementById('cart-count').innerText = count;
        }

        function renderCart() {
            const container = document.getElementById('cart-items-container');
            if(state.cart.length === 0) {
                container.innerHTML = "<p class='text-center py-10'>Keranjang kosong.</p>";
                return;
            }
            container.innerHTML = state.cart.map(item => `
                <div class="flex items-center bg-white dark:bg-gray-800 p-4 rounded-xl shadow border dark:border-gray-700">
                    <img src="${item.img}" class="w-16 h-16 object-cover rounded" alt="[Keranjang ${item.name}]">
                    <div class="ml-4 flex-grow">
                        <h4 class="font-bold">${item.name}</h4>
                        <p class="text-sm">Rp ${item.price.toLocaleString()} x ${item.qty}</p>
                    </div>
                    <button onclick="removeFromCart(${item.id})" class="text-red-500 hover:text-red-700 transition"><i class="fas fa-trash"></i></button>
                </div>
            `).join('');
            const total = state.cart.reduce((s, i) => s + (i.price * i.qty), 0);
            document.getElementById('cart-total').innerText = "Rp " + total.toLocaleString();
        }

        function removeFromCart(id) {
            state.cart = state.cart.filter(x => x.id !== id);
            updateBadge(); renderCart();
        }

        function showToast(msg) {
            const t = document.getElementById('toast');
            t.innerText = msg; t.classList.add('show');
            setTimeout(() => t.classList.remove('show'), 2500);
        }

        function toggleDarkMode() {
            document.documentElement.classList.toggle('dark');
            const icon = document.getElementById('theme-icon');
            icon.classList.toggle('fa-moon'); icon.classList.toggle('fa-sun');
        }

        function handleLogin(e) {
            e.preventDefault();
            const val = document.getElementById('login-input').value;
            state.user = val;
            document.getElementById('user-text').innerText = val;
            showToast("Halo, " + val);
            navigate('home');
        }

        function showSuccess() {
            showToast("Pesanan Berhasil!");
            state.cart = []; updateBadge(); navigate('home');
        }

        function toggleMobileMenu() {
            const menu = document.getElementById('mobile-menu');
            menu.classList.toggle('hidden');
        }

        document.getElementById('search-input').addEventListener('input', renderProducts);
        document.getElementById('category-filter').addEventListener('change', renderProducts);
        
        window.onload = renderHome;
    </script>
</body>
</html>
