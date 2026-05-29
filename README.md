# Kinerjaworkshop-kinerjaworkshop-app
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KinerjaWorkshop - Aplikasi Kasir Cuci Kendaraan</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js@3.9.1/dist/chart.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #f0f2f5;
            color: #333;
        }

        .container {
            display: flex;
            height: 100vh;
        }

        /* SIDEBAR */
        .sidebar {
            width: 250px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            overflow-y: auto;
            box-shadow: 2px 0 10px rgba(0,0,0,0.1);
            position: relative;
        }

        .sidebar-header {
            font-size: 18px;
            font-weight: bold;
            margin-bottom: 30px;
            text-align: center;
            padding-bottom: 15px;
            border-bottom: 2px solid rgba(255,255,255,0.3);
        }

        .sidebar-menu {
            list-style: none;
        }

        .sidebar-menu li {
            margin: 10px 0;
        }

        .sidebar-menu a {
            display: block;
            padding: 12px 15px;
            color: white;
            text-decoration: none;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: 500;
        }

        .sidebar-menu a:hover,
        .sidebar-menu a.active {
            background: rgba(255,255,255,0.2);
            padding-left: 25px;
        }

        .toggle-sidebar {
            display: none;
            position: absolute;
            top: 15px;
            right: 15px;
            background: rgba(255,255,255,0.3);
            color: white;
            border: none;
            padding: 8px 12px;
            cursor: pointer;
            border-radius: 5px;
            font-size: 20px;
        }

        /* MAIN CONTENT */
        .main-content {
            flex: 1;
            overflow-y: auto;
            padding: 30px;
        }

        .page {
            display: none;
        }

        .page.active {
            display: block;
        }

        /* HEADER */
        .page-header {
            background: white;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }

        .page-header h1 {
            color: #667eea;
            font-size: 28px;
            margin-bottom: 5px;
        }

        .page-header p {
            color: #999;
            font-size: 14px;
        }

        /* CARDS */
        .card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }

        .card-header {
            font-size: 18px;
            font-weight: bold;
            color: #667eea;
            margin-bottom: 15px;
            border-bottom: 2px solid #f0f2f5;
            padding-bottom: 10px;
        }

        /* FORMS */
        .form-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: #333;
        }

        input, select, textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 14px;
            font-family: inherit;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 5px rgba(102, 126, 234, 0.3);
        }

        /* BUTTONS */
        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
            font-size: 14px;
        }

        .btn-primary {
            background: #667eea;
            color: white;
        }

        .btn-primary:hover {
            background: #5568d3;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }

        .btn-success {
            background: #48bb78;
            color: white;
        }

        .btn-success:hover {
            background: #38a169;
        }

        .btn-danger {
            background: #f56565;
            color: white;
        }

        .btn-danger:hover {
            background: #e53e3e;
        }

        .btn-warning {
            background: #ed8936;
            color: white;
        }

        .btn-secondary {
            background: #718096;
            color: white;
        }

        .btn-secondary:hover {
            background: #4a5568;
        }

        .btn-sm {
            padding: 6px 12px;
            font-size: 12px;
        }

        .btn-group {
            display: flex;
            gap: 10px;
            margin-top: 15px;
            flex-wrap: wrap;
        }

        /* TABLES */
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
        }

        table th {
            background: #f7fafc;
            padding: 12px;
            text-align: left;
            font-weight: 600;
            border-bottom: 2px solid #e2e8f0;
            color: #667eea;
        }

        table td {
            padding: 12px;
            border-bottom: 1px solid #e2e8f0;
        }

        table tr:hover {
            background: #f9fafb;
        }

        /* STAT BOXES */
        .stat-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .stat-box {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
        }

        .stat-box.green {
            background: linear-gradient(135deg, #48bb78 0%, #38a169 100%);
        }

        .stat-box.orange {
            background: linear-gradient(135deg, #ed8936 0%, #dd6b20 100%);
        }

        .stat-box.red {
            background: linear-gradient(135deg, #f56565 0%, #e53e3e 100%);
        }

        .stat-label {
            font-size: 12px;
            opacity: 0.9;
            margin-bottom: 8px;
        }

        .stat-value {
            font-size: 24px;
            font-weight: bold;
        }

        /* MODAL */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            animation: fadeIn 0.3s;
        }

        .modal.show {
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .modal-content {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            width: 90%;
            max-width: 500px;
            max-height: 90vh;
            overflow-y: auto;
            animation: slideIn 0.3s;
        }

        .modal-header {
            font-size: 20px;
            font-weight: bold;
            margin-bottom: 20px;
            color: #667eea;
            border-bottom: 2px solid #f0f2f5;
            padding-bottom: 10px;
        }

        .modal-footer {
            margin-top: 20px;
            display: flex;
            gap: 10px;
            justify-content: flex-end;
        }

        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
            line-height: 20px;
        }

        .close:hover {
            color: #000;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes slideIn {
            from { transform: translateY(-50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        /* GRID */
        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        .grid-3 {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }

        /* RESPONSIVE */
        @media (max-width: 768px) {
            .container {
                flex-direction: column;
            }

            .sidebar {
                width: 100%;
                max-height: 60px;
                overflow: hidden;
                padding: 10px;
                transition: max-height 0.3s;
            }

            .sidebar.open {
                max-height: 500px;
            }

            .sidebar-header {
                margin-bottom: 10px;
            }

            .toggle-sidebar {
                display: block;
            }

            .main-content {
                padding: 15px;
            }

            .grid-2 {
                grid-template-columns: 1fr;
            }

            .page-header h1 {
                font-size: 20px;
            }

            table {
                font-size: 12px;
            }

            table th, table td {
                padding: 8px;
            }

            .btn {
                padding: 8px 12px;
                font-size: 12px;
            }

            .stat-value {
                font-size: 18px;
            }
        }

        /* CART */
        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #f7fafc;
            padding: 10px;
            margin: 5px 0;
            border-radius: 5px;
            border-left: 4px solid #667eea;
        }

        .cart-item-name {
            font-weight: 600;
            flex: 1;
        }

        .cart-item-qty {
            font-size: 12px;
            color: #999;
            margin: 0 10px;
        }

        .cart-item-price {
            font-weight: bold;
            color: #667eea;
            margin: 0 10px;
        }

        .cart-item-remove {
            background: #f56565;
            color: white;
            border: none;
            padding: 4px 8px;
            border-radius: 3px;
            cursor: pointer;
            font-size: 12px;
        }

        /* ALERT */
        .alert {
            padding: 12px 15px;
            margin-bottom: 15px;
            border-radius: 5px;
            border-left: 4px solid;
        }

        .alert-success {
            background: #c6f6d5;
            color: #22543d;
            border-color: #48bb78;
        }

        .alert-danger {
            background: #fed7d7;
            color: #742a2a;
            border-color: #f56565;
        }

        .alert-info {
            background: #bee3f8;
            color: #2c5282;
            border-color: #4299e1;
        }

        /* BADGE */
        .badge {
            display: inline-block;
            padding: 4px 8px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
        }

        .badge-training {
            background: #feebc8;
            color: #7c2d12;
        }

        .badge-staf {
            background: #c6f6d5;
            color: #22543d;
        }

        /* SCROLLBAR */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }

        ::-webkit-scrollbar-track {
            background: #f1f1f1;
        }

        ::-webkit-scrollbar-thumb {
            background: #667eea;
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: #5568d3;
        }

        /* MONOSPACE FOR REPORTS */
        .monospace {
            font-family: 'Courier New', monospace;
            white-space: pre-wrap;
            word-wrap: break-word;
            background: #f7fafc;
            padding: 15px;
            border-radius: 5px;
            overflow-x: auto;
            line-height: 1.6;
        }

        .text-right {
            text-align: right;
        }

        .text-center {
            text-align: center;
        }

        .mt-20 {
            margin-top: 20px;
        }

        .mb-20 {
            margin-bottom: 20px;
        }

        .currency {
            color: #667eea;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- SIDEBAR -->
        <div class="sidebar" id="sidebar">
            <button class="toggle-sidebar" id="toggleBtn">☰</button>
            <div class="sidebar-header">KinerjaWorkshop</div>
            <ul class="sidebar-menu">
                <li><a onclick="showPage('dashboard')" class="menu-item active">📊 Dashboard</a></li>
                <li><a onclick="showPage('penjualan')" class="menu-item">💰 Penjualan & Riwayat</a></li>
                <li><a onclick="showPage('gaji')" class="menu-item">💵 Gaji & Karyawan</a></li>
                <li><a onclick="showPage('laporan')" class="menu-item">📈 Laporan & Grafik</a></li>
                <li><a onclick="showPage('stok')" class="menu-item">📦 Data Master (Stok)</a></li>
            </ul>
        </div>

        <!-- MAIN CONTENT -->
        <div class="main-content">
            <!-- PAGE: DASHBOARD -->
            <div id="dashboard" class="page active">
                <div class="page-header">
                    <h1>📊 Dashboard</h1>
                    <p>Ringkasan bisnis cuci kendaraan Anda</p>
                </div>

                <div class="stat-grid">
                    <div class="stat-box green">
                        <div class="stat-label">Pendapatan Hari Ini</div>
                        <div class="stat-value" id="todayIncome">Rp 0</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-label">Total Kendaraan</div>
                        <div class="stat-value" id="totalVehicles">0</div>
                    </div>
                    <div class="stat-box orange">
                        <div class="stat-label">Total Karyawan</div>
                        <div class="stat-value" id="totalEmployees">0</div>
                    </div>
                    <div class="stat-box red">
                        <div class="stat-label">Total Kasbon</div>
                        <div class="stat-value" id="totalKasbon">Rp 0</div>
                    </div>
                </div>

                <div class="grid-2">
                    <div class="card">
                        <div class="card-header">📋 Transaksi Hari Ini</div>
                        <table id="dashboardTable">
                            <thead>
                                <tr>
                                    <th>Jam</th>
                                    <th>Jenis</th>
                                    <th>Deskripsi</th>
                                    <th>Nominal</th>
                                </tr>
                            </thead>
                            <tbody id="dashboardTableBody">
                            </tbody>
                        </table>
                    </div>

                    <div class="card">
                        <div class="card-header">👥 Status Karyawan</div>
                        <table>
                            <thead>
                                <tr>
                                    <th>Nama</th>
                                    <th>Status</th>
                                    <th>Gaji Hari Ini</th>
                                </tr>
                            </thead>
                            <tbody id="dashboardEmployeeTable">
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- PAGE: PENJUALAN -->
            <div id="penjualan" class="page">
                <div class="page-header">
                    <h1>💰 Penjualan & Riwayat</h1>
                    <p>Kelola transaksi cuci kendaraan, jajan, dan parfum</p>
                </div>

                <div class="grid-2">
                    <!-- FORM CUCI -->
                    <div class="card">
                        <div class="card-header">🚗 Form Cuci Kendaraan</div>
                        <div class="form-group">
                            <label>Tanggal</label>
                            <input type="date" id="washDate" value="">
                        </div>
                        <div class="form-group">
                            <label>Jam</label>
                            <input type="time" id="washTime" value="">
                        </div>
                        <div class="form-group">
                            <label>Jenis Kendaraan</label>
                            <select id="vehicleType">
                                <option value="">-- Pilih --</option>
                                <option value="Mobil">Mobil</option>
                                <option value="Motor">Motor</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>Nama Kendaraan</label>
                            <input type="text" id="vehicleName" placeholder="Misal: Toyota Avanza, Honda Civic">
                        </div>
                        <div class="form-group">
                            <label>Warna</label>
                            <input type="text" id="vehicleColor" placeholder="Misal: Putih, Hitam">
                        </div>
                        <div class="form-group">
                            <label>Harga Jasa (Rp)</label>
                            <input type="number" id="washPrice" placeholder="0" min="0">
                        </div>
                        <div class="form-group">
                            <label>Metode Pembayaran</label>
                            <select id="washPayment">
                                <option value="">-- Pilih --</option>
                                <option value="Cash">Cash</option>
                                <option value="QRIS">QRIS</option>
                                <option value="Lainnya">Lainnya</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>Pilih Karyawan</label>
                            <select id="washEmployee">
                                <option value="">-- Pilih --</option>
                            </select>
                        </div>
                        <button class="btn btn-primary" onclick="addWashTransaction()">Tambah Transaksi Cuci</button>
                    </div>

                    <!-- KERANJANG JAJAN & PARFUM -->
                    <div class="card">
                        <div class="card-header">🛒 Keranjang Jajan & Parfum</div>
                        <div class="form-group">
                            <label>Pilih Produk</label>
                            <select id="productSelect">
                                <option value="">-- Pilih --</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>Jumlah</label>
                            <input type="number" id="productQty" placeholder="1" min="1" value="1">
                        </div>
                        <button class="btn btn-primary" onclick="addToCart()">Tambah ke Keranjang</button>

                        <div style="margin-top: 20px; border-top: 2px solid #f0f2f5; padding-top: 15px;">
                            <div class="card-header" style="margin: 0 0 10px 0;">Daftar Keranjang</div>
                            <div id="cartList"></div>
                            <div style="margin-top: 15px; padding: 15px; background: #f7fafc; border-radius: 5px;">
                                <div style="display: flex; justify-content: space-between; font-weight: bold; margin-bottom: 10px;">
                                    <span>Total:</span>
                                    <span id="cartTotal" class="currency">Rp 0</span>
                                </div>
                                <div class="form-group" style="margin: 0;">
                                    <label>Metode Pembayaran</label>
                                    <select id="cartPayment">
                                        <option value="">-- Pilih --</option>
                                        <option value="Cash">Cash</option>
                                        <option value="QRIS">QRIS</option>
                                        <option value="Lainnya">Lainnya</option>
                                    </select>
                                </div>
                                <button class="btn btn-success" onclick="checkoutCart()" style="margin-top: 10px; width: 100%;">Checkout</button>
                                <button class="btn btn-secondary" onclick="clearCart()" style="margin-top: 5px; width: 100%;">Hapus Semua</button>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- RIWAYAT TRANSAKSI -->
                <div class="card">
                    <div class="card-header">📜 Riwayat Transaksi</div>
                    <table id="transactionTable">
                        <thead>
                            <tr>
                                <th>Tanggal</th>
                                <th>Jam</th>
                                <th>Jenis</th>
                                <th>Deskripsi</th>
                                <th>Jumlah</th>
                                <th>Pembayaran</th>
                                <th>Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="transactionTableBody">
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- PAGE: GAJI -->
            <div id="gaji" class="page">
                <div class="page-header">
                    <h1>💵 Gaji & Karyawan</h1>
                    <p>Kelola karyawan, gaji, dan kasbon</p>
                </div>

                <!-- ADD EMPLOYEE -->
                <div class="card">
                    <div class="card-header">➕ Tambah Karyawan</div>
                    <div class="grid-2">
                        <div>
                            <div class="form-group">
                                <label>Nama Karyawan</label>
                                <input type="text" id="empName" placeholder="Nama lengkap">
                            </div>
                            <div class="form-group">
                                <label>Status Awal</label>
                                <select id="empStatus">
                                    <option value="Training">Training</option>
                                    <option value="Staf">Staf</option>
                                </select>
                            </div>
                        </div>
                        <div>
                            <div class="form-group">
                                <label>Tanggal Bergabung</label>
                                <input type="date" id="empJoinDate">
                            </div>
                            <button class="btn btn-primary" onclick="addEmployee()" style="margin-top: 34px;">Tambah Karyawan</button>
                        </div>
                    </div>
                </div>

                <!-- DAFTAR KARYAWAN -->
                <div class="card">
                    <div class="card-header">👥 Daftar Karyawan</div>
                    <table id="employeeTable">
                        <thead>
                            <tr>
                                <th>Nama</th>
                                <th>Status</th>
                                <th>Tanggal Bergabung</th>
                                <th>Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="employeeTableBody">
                        </tbody>
                    </table>
                </div>

                <!-- GAJI HARIAN -->
                <div class="card">
                    <div class="card-header">📅 Gaji Harian</div>
                    <div class="form-group">
                        <label>Pilih Tanggal</label>
                        <input type="date" id="dailyWageDate" value="">
                    </div>
                    <button class="btn btn-primary" onclick="showDailyWages()">Tampilkan Gaji</button>
                    <table id="dailyWageTable" style="margin-top: 15px;">
                        <thead>
                            <tr>
                                <th>Nama</th>
                                <th>Status</th>
                                <th>Gaji</th>
                            </tr>
                        </thead>
                        <tbody id="dailyWageTableBody">
                        </tbody>
                    </table>
                </div>

                <!-- GAJI PER TANGGAL (BULAN) -->
                <div class="card">
                    <div class="card-header">📊 Gaji per Tanggal (Bulan)</div>
                    <div class="form-group">
                        <label>Pilih Bulan & Tahun</label>
                        <input type="month" id="monthlyWageMonth">
                    </div>
                    <button class="btn btn-primary" onclick="showMonthlyWages()">Tampilkan Gaji Bulanan</button>
                    <div id="monthlyWageTable" style="margin-top: 15px; overflow-x: auto;"></div>
                </div>

                <!-- GAJI MINGGUAN -->
                <div class="card">
                    <div class="card-header">🗓️ Gaji Mingguan (Minggu - Sabtu)</div>
                    <div class="form-group">
                        <label>Pilih Minggu Awal</label>
                        <input type="date" id="weeklyWageDate">
                    </div>
                    <button class="btn btn-primary" onclick="showWeeklyWages()">Tampilkan Gaji Mingguan</button>
                    <table id="weeklyWageTable" style="margin-top: 15px;">
                        <thead>
                            <tr>
                                <th>Nama</th>
                                <th>Total Gaji</th>
                                <th>Total Kasbon</th>
                                <th>Netto</th>
                            </tr>
                        </thead>
                        <tbody id="weeklyWageTableBody">
                        </tbody>
                    </table>
                </div>

                <!-- KASBON -->
                <div class="card">
                    <div class="card-header">💸 Kasbon Karyawan</div>
                    <div class="grid-2">
                        <div>
                            <div class="form-group">
                                <label>Pilih Karyawan</label>
                                <select id="kasyonEmployee">
                                    <option value="">-- Pilih --</option>
                                </select>
                            </div>
                        </div>
                        <div>
                            <div class="form-group">
                                <label>Nominal Kasbon (Rp)</label>
                                <input type="number" id="kasyonAmount" placeholder="0" min="0">
                            </div>
                        </div>
                    </div>
                    <div class="form-group">
                        <label>Keterangan</label>
                        <textarea id="kasyonNote" placeholder="Alasan kasbon" rows="2"></textarea>
                    </div>
                    <button class="btn btn-primary" onclick="addKasyon()">Tambah Kasbon</button>

                    <table id="kasyonTable" style="margin-top: 20px;">
                        <thead>
                            <tr>
                                <th>Tanggal</th>
                                <th>Nama Karyawan</th>
                                <th>Nominal</th>
                                <th>Keterangan</th>
                                <th>Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="kasyonTableBody">
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- PAGE: LAPORAN -->
            <div id="laporan" class="page">
                <div class="page-header">
                    <h1>📈 Laporan & Grafik</h1>
                    <p>Analisis keuangan dan performa bisnis</p>
                </div>

                <!-- LAPORAN HARIAN -->
                <div class="card">
                    <div class="card-header">📋 Laporan Keuangan Harian</div>
                    <div class="form-group">
                        <label>Pilih Tanggal</label>
                        <input type="date" id="laporanDate">
                    </div>
                    <button class="btn btn-primary" onclick="generateLaporan()">Buat Laporan</button>
                    <div id="laporanContent" style="margin-top: 20px;"></div>
                </div>

                <!-- GRAFIK -->
                <div class="grid-2">
                    <div class="card">
                        <div class="card-header">📊 Grafik Penjualan Jajan</div>
                        <div class="form-group">
                            <label>Pilih Bulan & Tahun</label>
                            <input type="month" id="chartMonth1">
                        </div>
                        <button class="btn btn-primary" onclick="updateChart('jajan')">Update Grafik</button>
                        <canvas id="jajanChart" style="margin-top: 15px;"></canvas>
                    </div>

                    <div class="card">
                        <div class="card-header">📊 Grafik Penjualan Parfum</div>
                        <div class="form-group">
                            <label>Pilih Bulan & Tahun</label>
                            <input type="month" id="chartMonth2">
                        </div>
                        <button class="btn btn-primary" onclick="updateChart('parfum')">Update Grafik</button>
                        <canvas id="parfumChart" style="margin-top: 15px;"></canvas>
                    </div>

                    <div class="card">
                        <div class="card-header">📊 Grafik Jumlah Kendaraan</div>
                        <div class="form-group">
                            <label>Pilih Bulan & Tahun</label>
                            <input type="month" id="chartMonth3">
                        </div>
                        <button class="btn btn-primary" onclick="updateChart('vehicle')">Update Grafik</button>
                        <canvas id="vehicleChart" style="margin-top: 15px;"></canvas>
                    </div>

                    <div class="card">
                        <div class="card-header">📊 Grafik Pendapatan</div>
                        <div class="form-group">
                            <label>Pilih Bulan & Tahun</label>
                            <input type="month" id="chartMonth4">
                        </div>
                        <button class="btn btn-primary" onclick="updateChart('income')">Update Grafik</button>
                        <canvas id="incomeChart" style="margin-top: 15px;"></canvas>
                    </div>
                </div>
            </div>

            <!-- PAGE: STOK -->
            <div id="stok" class="page">
                <div class="page-header">
                    <h1>📦 Data Master (Stok)</h1>
                    <p>Kelola stok jajan dan parfum</p>
                </div>

                <!-- JAJAN -->
                <div class="card">
                    <div class="card-header">🍿 Master Jajan</div>
                    <div class="grid-2">
                        <div>
                            <div class="form-group">
                                <label>Nama Jajan</label>
                                <input type="text" id="jajanName" placeholder="Nama produk">
                            </div>
                        </div>
                        <div>
                            <div class="form-group">
                                <label>Harga (Rp)</label>
                                <input type="number" id="jajanPrice" placeholder="0" min="0">
                            </div>
                        </div>
                        <div>
                            <div class="form-group">
                                <label>Stok</label>
                                <input type="number" id="jajanStock" placeholder="0" min="0">
                            </div>
                        </div>
                        <button class="btn btn-primary" onclick="addJajan()" style="margin-top: 34px;">Tambah Jajan</button>
                    </div>

                    <table id="jajanTable" style="margin-top: 20px;">
                        <thead>
                            <tr>
                                <th>Nama</th>
                                <th>Harga (Rp)</th>
                                <th>Stok</th>
                                <th>Total Nilai (Rp)</th>
                                <th>Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="jajanTableBody">
                        </tbody>
                    </table>
                </div>

                <!-- PARFUM -->
                <div class="card">
                    <div class="card-header">💐 Master Parfum</div>
                    <div class="grid-2">
                        <div>
                            <div class="form-group">
                                <label>Nama Parfum</label>
                                <input type="text" id="parfumName" placeholder="Nama produk">
                            </div>
                        </div>
                        <div>
                            <div class="form-group">
                                <label>Harga (Rp)</label>
                                <input type="number" id="parfumPrice" placeholder="0" min="0">
                            </div>
                        </div>
                        <div>
                            <div class="form-group">
                                <label>Stok</label>
                                <input type="number" id="parfumStock" placeholder="0" min="0">
                            </div>
                        </div>
                        <button class="btn btn-primary" onclick="addParfum()" style="margin-top: 34px;">Tambah Parfum</button>
                    </div>

                    <table id="parfumTable" style="margin-top: 20px;">
                        <thead>
                            <tr>
                                <th>Nama</th>
                                <th>Harga (Rp)</th>
                                <th>Stok</th>
                                <th>Total Nilai (Rp)</th>
                                <th>Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="parfumTableBody">
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <!-- MODAL: EDIT TRANSAKSI -->
    <div id="editTransactionModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal('editTransactionModal')">&times;</span>
            <div class="modal-header">Edit Transaksi</div>
            <div class="form-group">
                <label>Jenis</label>
                <input type="text" id="editTransType" disabled>
            </div>
            <div class="form-group">
                <label>Deskripsi</label>
                <input type="text" id="editTransDesc">
            </div>
            <div class="form-group">
                <label>Jumlah (Rp)</label>
                <input type="number" id="editTransAmount" min="0">
            </div>
            <div class="form-group">
                <label>Pembayaran</label>
                <select id="editTransPayment">
                    <option value="Cash">Cash</option>
                    <option value="QRIS">QRIS</option>
                    <option value="Lainnya">Lainnya</option>
                </select>
            </div>
            <div class="modal-footer">
                <button class="btn btn-secondary" onclick="closeModal('editTransactionModal')">Batal</button>
                <button class="btn btn-primary" onclick="saveEditTransaction()">Simpan</button>
            </div>
        </div>
    </div>

    <!-- MODAL: EDIT EMPLOYEE -->
    <div id="editEmployeeModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal('editEmployeeModal')">&times;</span>
            <div class="modal-header">Edit Karyawan</div>
            <div class="form-group">
                <label>Nama</label>
                <input type="text" id="editEmpName">
            </div>
            <div class="form-group">
                <label>Status Saat Ini</label>
                <input type="text" id="editEmpCurrentStatus" disabled>
            </div>
            <div class="form-group">
                <label>Ubah Status ke</label>
                <select id="editEmpNewStatus">
                    <option value="Training">Training</option>
                    <option value="Staf">Staf</option>
                </select>
            </div>
            <div class="form-group">
                <label>Tanggal Perubahan Status</label>
                <input type="date" id="editEmpStatusDate">
            </div>
            <div class="modal-footer">
                <button class="btn btn-danger" onclick="deleteEmployee()" style="margin-right: auto;">Hapus Karyawan</button>
                <button class="btn btn-secondary" onclick="closeModal('editEmployeeModal')">Batal</button>
                <button class="btn btn-primary" onclick="saveEditEmployee()">Simpan</button>
            </div>
        </div>
    </div>

    <!-- MODAL: EDIT JAJAN -->
    <div id="editJajanModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal('editJajanModal')">&times;</span>
            <div class="modal-header">Edit Jajan</div>
            <div class="form-group">
                <label>Nama</label>
                <input type="text" id="editJajanName">
            </div>
            <div class="form-group">
                <label>Harga (Rp)</label>
                <input type="number" id="editJajanPrice" min="0">
            </div>
            <div class="form-group">
                <label>Stok</label>
                <input type="number" id="editJajanStock" min="0">
            </div>
            <div class="modal-footer">
                <button class="btn btn-danger" onclick="deleteJajan()" style="margin-right: auto;">Hapus</button>
                <button class="btn btn-secondary" onclick="closeModal('editJajanModal')">Batal</button>
                <button class="btn btn-primary" onclick="saveEditJajan()">Simpan</button>
            </div>
        </div>
    </div>

    <!-- MODAL: EDIT PARFUM -->
    <div id="editParfumModal" class="modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal('editParfumModal')">&times;</span>
            <div class="modal-header">Edit Parfum</div>
            <div class="form-group">
                <label>Nama</label>
                <input type="text" id="editParfumName">
            </div>
            <div class="form-group">
                <label>Harga (Rp)</label>
                <input type="number" id="editParfumPrice" min="0">
            </div>
            <div class="form-group">
                <label>Stok</label>
                <input type="number" id="editParfumStock" min="0">
            </div>
            <div class="modal-footer">
                <button class="btn btn-danger" onclick="deleteParfum()" style="margin-right: auto;">Hapus</button>
                <button class="btn btn-secondary" onclick="closeModal('editParfumModal')">Batal</button>
                <button class="btn btn-primary" onclick="saveEditParfum()">Simpan</button>
            </div>
        </div>
    </div>

    <script>
        // ===== INITIALIZATION =====
        let currentEditingId = null;
        let chartInstances = {};

        // Set today date
        const today = new Date().toISOString().split('T')[0];
        document.getElementById('washDate').value = today;
        document.getElementById('dailyWageDate').value = today;
        document.getElementById('laporanDate').value = today;
        document.getElementById('weeklyWageDate').value = today;
        document.getElementById('editEmpStatusDate').value = today;

        // Set current month for charts
        const currentMonth = new Date().toISOString().substr(0, 7);
        document.getElementById('chartMonth1').value = currentMonth;
        document.getElementById('chartMonth2').value = currentMonth;
        document.getElementById('chartMonth3').value = currentMonth;
        document.getElementById('chartMonth4').value = currentMonth;
        document.getElementById('monthlyWageMonth').value = currentMonth;

        // Set wash time to current time
        const now = new Date();
        const hours = String(now.getHours()).padStart(2, '0');
        const minutes = String(now.getMinutes()).padStart(2, '0');
        document.getElementById('washTime').value = `${hours}:${minutes}`;

        // ===== DATA MANAGEMENT =====
        const db = {
            transactions: [],
            employees: [],
            statusHistory: [],
            jajan: [],
            parfum: [],
            kasyon: []
        };

        // Load data from localStorage
        function loadData() {
            const saved = localStorage.getItem('kinerjaworkshop_db');
            if (saved) {
                Object.assign(db, JSON.parse(saved));
            }
        }

        // Save data to localStorage
        function saveData() {
            localStorage.setItem('kinerjaworkshop_db', JSON.stringify(db));
        }

        // ===== PAGE NAVIGATION =====
        function showPage(pageId) {
            // Hide all pages
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            // Show selected page
            document.getElementById(pageId).classList.add('active');

            // Update active menu
            document.querySelectorAll('.menu-item').forEach(m => m.classList.remove('active'));
            event.target.classList.add('active');

            // Close sidebar on mobile
            if (window.innerWidth <= 768) {
                document.getElementById('sidebar').classList.remove('open');
            }

            // Update page-specific content
            if (pageId === 'dashboard') updateDashboard();
            if (pageId === 'penjualan') updatePenjualanPage();
            if (pageId === 'gaji') updateGajiPage();
            if (pageId === 'laporan') updateLaporanPage();
            if (pageId === 'stok') updateStokPage();
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.remove('show');
        }

        // ===== SIDEBAR TOGGLE =====
        document.getElementById('toggleBtn').addEventListener('click', function() {
            document.getElementById('sidebar').classList.toggle('open');
        });

        // ===== FORMAT CURRENCY =====
        function formatCurrency(value) {
            return new Intl.NumberFormat('id-ID', {
                style: 'currency',
                currency: 'IDR',
                minimumFractionDigits: 0,
                maximumFractionDigits: 0
            }).format(value);
        }

        // ===== WASH TRANSACTION =====
        function addWashTransaction() {
            const date = document.getElementById('washDate').value;
            const time = document.getElementById('washTime').value;
            const vehicleType = document.getElementById('vehicleType').value;
            const vehicleName = document.getElementById('vehicleName').value;
            const vehicleColor = document.getElementById('vehicleColor').value;
            const price = parseInt(document.getElementById('washPrice').value) || 0;
            const payment = document.getElementById('washPayment').value;
            const employeeId = document.getElementById('washEmployee').value;

            if (!date || !time || !vehicleType || !vehicleName || !vehicleColor || !price || !payment || !employeeId) {
                alert('Semua field harus diisi!');
                return;
            }

            db.transactions.push({
                id: Date.now(),
                date,
                time,
                type: 'Cuci',
                description: `${vehicleType} - ${vehicleName} (${vehicleColor})`,
                amount: price,
                payment,
                employeeId,
                quantity: 1
            });

            saveData();
            alert('Transaksi cuci ditambahkan!');
            
            // Reset form
            document.getElementById('vehicleName').value = '';
            document.getElementById('vehicleColor').value = '';
            document.getElementById('washPrice').value = '';
            document.getElementById('vehicleType').value = '';
            document.getElementById('washPayment').value = '';
            document.getElementById('washEmployee').value = '';

            updateTransactionTable();
            updateDashboard();
        }

        // ===== CART MANAGEMENT =====
        let cart = [];

        function addToCart() {
            const productId = document.getElementById('productSelect').value;
            const qty = parseInt(document.getElementById('productQty').value) || 1;

            if (!productId || qty <= 0) {
                alert('Pilih produk dan jumlah!');
                return;
            }

            let product = db.jajan.find(p => p.id == productId) || db.parfum.find(p => p.id == productId);
            if (!product) {
                alert('Produk tidak ditemukan!');
                return;
            }

            if (product.stock < qty) {
                alert('Stok tidak mencukupi!');
                return;
            }

            // Check if already in cart
            let cartItem = cart.find(item => item.id === productId);
            if (cartItem) {
                cartItem.quantity += qty;
            } else {
                cart.push({
                    id: productId,
                    name: product.name,
                    price: product.price,
                    quantity: qty,
                    type: db.jajan.find(p => p.id == productId) ? 'Jajan' : 'Parfum'
                });
            }

            updateCartDisplay();
            document.getElementById('productQty').value = '1';
            document.getElementById('productSelect').value = '';
        }

        function updateCartDisplay() {
            const cartList = document.getElementById('cartList');
            let html = '';
            let total = 0;

            cart.forEach(item => {
                const itemTotal = item.price * item.quantity;
                total += itemTotal;
                html += `
                    <div class="cart-item">
                        <span class="cart-item-name">${item.name}</span>
                        <span class="cart-item-qty">x${item.quantity}</span>
                        <span class="cart-item-price">${formatCurrency(itemTotal)}</span>
                        <button class="cart-item-remove" onclick="removeFromCart(${item.id})">Hapus</button>
                    </div>
                `;
            });

            cartList.innerHTML = html || '<p style="color: #999; padding: 20px; text-align: center;">Keranjang kosong</p>';
            document.getElementById('cartTotal').textContent = formatCurrency(total);
        }

        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            updateCartDisplay();
        }

        function clearCart() {
            if (confirm('Hapus semua item dari keranjang?')) {
                cart = [];
                updateCartDisplay();
            }
        }

        function checkoutCart() {
            if (cart.length === 0) {
                alert('Keranjang kosong!');
                return;
            }

            const payment = document.getElementById('cartPayment').value;
            if (!payment) {
                alert('Pilih metode pembayaran!');
                return;
            }

            const date = document.getElementById('washDate').value;
            const time = document.getElementById('washTime').value;

            cart.forEach(item => {
                db.transactions.push({
                    id: Date.now() + Math.random(),
                    date,
                    time,
                    type: item.type,
                    description: item.name,
                    amount: item.price * item.quantity,
                    payment,
                    quantity: item.quantity,
                    productId: item.id
                });

                // Reduce stock
                if (db.jajan.find(p => p.id == item.id)) {
                    db.jajan.find(p => p.id == item.id).stock -= item.quantity;
                } else if (db.parfum.find(p => p.id == item.id)) {
                    db.parfum.find(p => p.id == item.id).stock -= item.quantity;
                }
            });

            saveData();
            alert('Checkout berhasil!');
            cart = [];
            updateCartDisplay();
            document.getElementById('cartPayment').value = '';
            updateTransactionTable();
            updateStokPage();
            updateDashboard();
        }

        // ===== TRANSACTION TABLE =====
        function updateTransactionTable() {
            const tbody = document.getElementById('transactionTableBody');
            let html = '';

            if (db.transactions.length === 0) {
                tbody.innerHTML = '<tr><td colspan="7" style="text-align: center; color: #999;">Tidak ada transaksi</td></tr>';
                return;
            }

            // Sort by date and time descending
            const sorted = [...db.transactions].sort((a, b) => {
                return new Date(b.date + ' ' + b.time) - new Date(a.date + ' ' + a.time);
            });

            sorted.forEach(trans => {
                html += `
                    <tr>
                        <td>${trans.date}</td>
                        <td>${trans.time}</td>
                        <td>${trans.type}</td>
                        <td>${trans.description}</td>
                        <td>${trans.quantity}</td>
                        <td>${trans.payment}</td>
                        <td>
                            <button class="btn btn-sm btn-primary" onclick="editTransaction(${trans.id})">Edit</button>
                            <button class="btn btn-sm btn-danger" onclick="deleteTransaction(${trans.id})">Hapus</button>
                        </td>
                    </tr>
                `;
            });

            tbody.innerHTML = html;
        }

        function editTransaction(id) {
            const trans = db.transactions.find(t => t.id === id);
            if (!trans) return;

            currentEditingId = id;
            document.getElementById('editTransType').value = trans.type;
            document.getElementById('editTransDesc').value = trans.description;
            document.getElementById('editTransAmount').value = trans.amount;
            document.getElementById('editTransPayment').value = trans.payment;

            document.getElementById('editTransactionModal').classList.add('show');
        }

        function saveEditTransaction() {
            const trans = db.transactions.find(t => t.id === currentEditingId);
            if (!trans) return;

            trans.description = document.getElementById('editTransDesc').value;
            trans.amount = parseInt(document.getElementById('editTransAmount').value) || 0;
            trans.payment = document.getElementById('editTransPayment').value;

            saveData();
            closeModal('editTransactionModal');
            updateTransactionTable();
            updateDashboard();
            alert('Transaksi diperbarui!');
        }

        function deleteTransaction(id) {
            if (confirm('Hapus transaksi ini?')) {
                const trans = db.transactions.find(t => t.id === id);
                if (trans && trans.productId) {
                    // Return stock
                    const product = db.jajan.find(p => p.id === trans.productId) || db.parfum.find(p => p.id === trans.productId);
                    if (product) product.stock += trans.quantity;
                }

                db.transactions = db.transactions.filter(t => t.id !== id);
                saveData();
                updateTransactionTable();
                updateDashboard();
                alert('Transaksi dihapus!');
            }
        }

        // ===== EMPLOYEE MANAGEMENT =====
        function addEmployee() {
            const name = document.getElementById('empName').value;
            const status = document.getElementById('empStatus').value;
            const joinDate = document.getElementById('empJoinDate').value;

            if (!name || !status || !joinDate) {
                alert('Semua field harus diisi!');
                return;
            }

            const emp = {
                id: Date.now(),
                name,
                joinDate,
                statusHistory: [{ date: joinDate, status }]
            };

            db.employees.push(emp);
            saveData();

            alert('Karyawan ditambahkan!');
            document.getElementById('empName').value = '';
            document.getElementById('empJoinDate').value = today;
            document.getElementById('empStatus').value = 'Training';

            updateEmployeeTable();
            updateEmployeeSelects();
            updateDashboard();
        }

        function updateEmployeeTable() {
            const tbody = document.getElementById('employeeTableBody');
            let html = '';

            db.employees.forEach(emp => {
                const currentStatus = emp.statusHistory[emp.statusHistory.length - 1].status;
                const joinDate = emp.joinDate;
                const statusBadge = `<span class="badge badge-${currentStatus === 'Training' ? 'training' : 'staf'}">${currentStatus}</span>`;

                html += `
                    <tr>
                        <td>${emp.name}</td>
                        <td>${statusBadge}</td>
                        <td>${joinDate}</td>
                        <td>
                            <button class="btn btn-sm btn-primary" onclick="editEmployee(${emp.id})">Edit</button>
                        </td>
                    </tr>
                `;
            });

            tbody.innerHTML = html || '<tr><td colspan="4" style="text-align: center; color: #999;">Tidak ada karyawan</td></tr>';
        }

        function editEmployee(id) {
            const emp = db.employees.find(e => e.id === id);
            if (!emp) return;

            currentEditingId = id;
            const currentStatus = emp.statusHistory[emp.statusHistory.length - 1].status;

            document.getElementById('editEmpName').value = emp.name;
            document.getElementById('editEmpCurrentStatus').value = currentStatus;
            document.getElementById('editEmpNewStatus').value = currentStatus;
            document.getElementById('editEmpStatusDate').value = today;

            document.getElementById('editEmployeeModal').classList.add('show');
        }

        function saveEditEmployee() {
            const emp = db.employees.find(e => e.id === currentEditingId);
            if (!emp) return;

            emp.name = document.getElementById('editEmpName').value;
            const newStatus = document.getElementById('editEmpNewStatus').value;
            const currentStatus = emp.statusHistory[emp.statusHistory.length - 1].status;

            if (newStatus !== currentStatus) {
                const changeDate = document.getElementById('editEmpStatusDate').value;
                emp.statusHistory.push({ date: changeDate, status: newStatus });
            }

            saveData();
            closeModal('editEmployeeModal');
            updateEmployeeTable();
            updateDashboard();
            alert('Karyawan diperbarui!');
        }

        function deleteEmployee() {
            if (confirm('Hapus karyawan ini?')) {
                db.employees = db.employees.filter(e => e.id !== currentEditingId);
                saveData();
                closeModal('editEmployeeModal');
                updateEmployeeTable();
                updateEmployeeSelects();
                alert('Karyawan dihapus!');
            }
        }

        function updateEmployeeSelects() {
            const selects = ['washEmployee', 'kasyonEmployee'];
            selects.forEach(selectId => {
                const select = document.getElementById(selectId);
                const currentValue = select.value;
                select.innerHTML = '<option value="">-- Pilih --</option>';
                db.employees.forEach(emp => {
                    const option = document.createElement('option');
                    option.value = emp.id;
                    option.textContent = emp.name;
                    select.appendChild(option);
                });
                select.value = currentValue;
            });
        }

        // ===== GAJI CALCULATION =====
        function getEmployeeStatusOnDate(empId, date) {
            const emp = db.employees.find(e => e.id == empId);
            if (!emp) return null;

            let status = emp.statusHistory[0].status;
            emp.statusHistory.forEach(history => {
                if (history.date <= date) {
                    status = history.status;
                }
            });
            return status;
        }

        function calculateDailyWage(date, empId) {
            const washTransactions = db.transactions.filter(t => 
                t.date === date && t.type === 'Cuci'
            );

            if (washTransactions.length === 0) return 0;

            const totalWash = washTransactions.reduce((sum, t) => sum + t.amount, 0);
            const employeeShare = totalWash * 0.5;

            const allEmployees = db.employees;
            const trainingEmps = allEmployees.filter(e => getEmployeeStatusOnDate(e.id, date) === 'Training');
            const staffEmps = allEmployees.filter(e => getEmployeeStatusOnDate(e.id, date) === 'Staf');

            let wage = 0;
            const currentEmp = allEmployees.find(e => e.id == empId);
            if (!currentEmp) return 0;

            const currentStatus = getEmployeeStatusOnDate(empId, date);

            if (currentStatus === 'Training') {
                wage = 2500;
                const remainingShare = employeeShare - (trainingEmps.length * 2500);
                if (remainingShare > 0 && staffEmps.length > 0) {
                    wage += remainingShare / staffEmps.length;
                }
            } else {
                const trainingCost = trainingEmps.length * 2500;
                const remainingShare = Math.max(0, employeeShare - trainingCost);
                wage = staffEmps.length > 0 ? remainingShare / staffEmps.length : 0;
            }

            return Math.round(wage);
        }

        function showDailyWages() {
            const date = document.getElementById('dailyWageDate').value;
            const tbody = document.getElementById('dailyWageTableBody');
            let html = '';

            db.employees.forEach(emp => {
                const wage = calculateDailyWage(date, emp.id);
                const status = getEmployeeStatusOnDate(emp.id, date);
                const statusBadge = `<span class="badge badge-${status === 'Training' ? 'training' : 'staf'}">${status}</span>`;

                html += `
                    <tr>
                        <td>${emp.name}</td>
                        <td>${statusBadge}</td>
                        <td class="text-right currency">${formatCurrency(wage)}</td>
                    </tr>
                `;
            });

            tbody.innerHTML = html || '<tr><td colspan="3" style="text-align: center; color: #999;">Tidak ada data</td></tr>';
        }

        function showMonthlyWages() {
            const monthStr = document.getElementById('monthlyWageMonth').value;
            if (!monthStr) {
                alert('Pilih bulan!');
                return;
            }

            const [year, month] = monthStr.split('-');
            const daysInMonth = new Date(year, month, 0).getDate();

            let html = '<table><thead><tr><th>Nama</th>';
            for (let day = 1; day <= daysInMonth; day++) {
                html += `<th>${day}</th>`;
            }
            html += '<th>Total</th></tr></thead><tbody>';

            db.employees.forEach(emp => {
                html += `<tr><td><strong>${emp.name}</strong></td>`;
                let total = 0;
                for (let day = 1; day <= daysInMonth; day++) {
                    const dateStr = `${year}-${month}-${String(day).padStart(2, '0')}`;
                    const wage = calculateDailyWage(dateStr, emp.id);
                    total += wage;
                    html += `<td style="text-align: center;">${wage > 0 ? formatCurrency(wage) : '-'}</td>`;
                }
                html += `<td class="currency">${formatCurrency(total)}</td></tr>`;
            });

            html += '</tbody></table>';
            document.getElementById('monthlyWageTable').innerHTML = html;
        }

        function showWeeklyWages() {
            const startDate = new Date(document.getElementById('weeklyWageDate').value);
            const endDate = new Date(startDate);
            endDate.setDate(endDate.getDate() + 6);

            const startStr = startDate.toISOString().split('T')[0];
            const endStr = endDate.toISOString().split('T')[0];

            const tbody = document.getElementById('weeklyWageTableBody');
            let html = '';

            db.employees.forEach(emp => {
                let weekTotal = 0;
                let currentDate = new Date(startDate);
                while (currentDate <= endDate) {
                    const dateStr = currentDate.toISOString().split('T')[0];
                    weekTotal += calculateDailyWage(dateStr, emp.id);
                    currentDate.setDate(currentDate.getDate() + 1);
                }

                const totalKasyon = db.kasyon
                    .filter(k => k.empId === emp.id && k.date >= startStr && k.date <= endStr)
                    .reduce((sum, k) => sum + k.amount, 0);

                const netto = weekTotal - totalKasyon;

                html += `
                    <tr>
                        <td>${emp.name}</td>
                        <td class="text-right currency">${formatCurrency(weekTotal)}</td>
                        <td class="text-right currency">${formatCurrency(totalKasyon)}</td>
                        <td class="text-right currency">${formatCurrency(netto)}</td>
                    </tr>
                `;
            });

            tbody.innerHTML = html || '<tr><td colspan="4" style="text-align: center; color: #999;">Tidak ada data</td></tr>';
        }

        // ===== KASYON =====
        function addKasyon() {
            const empId = document.getElementById('kasyonEmployee').value;
            const amount = parseInt(document.getElementById('kasyonAmount').value) || 0;
            const note = document.getElementById('kasyonNote').value;

            if (!empId || amount <= 0) {
                alert('Pilih karyawan dan nominal kasbon!');
                return;
            }

            db.kasyon.push({
                id: Date.now(),
                empId: parseInt(empId),
                amount,
                note,
                date: today
            });

            saveData();
            alert('Kasbon ditambahkan!');

            document.getElementById('kasyonEmployee').value = '';
            document.getElementById('kasyonAmount').value = '';
            document.getElementById('kasyonNote').value = '';

            updateKasyonTable();
        }

        function updateKasyonTable() {
            const tbody = document.getElementById('kasyonTableBody');
            let html = '';

            db.kasyon.forEach(k => {
                const emp = db.employees.find(e => e.id === k.empId);
                html += `
                    <tr>
                        <td>${k.date}</td>
                        <td>${emp ? emp.name : '-'}</td>
                        <td class="currency">${formatCurrency(k.amount)}</td>
                        <td>${k.note}</td>
                        <td>
                            <button class="btn btn-sm btn-danger" onclick="deleteKasyon(${k.id})">Hapus</button>
                        </td>
                    </tr>
                `;
            });

            tbody.innerHTML = html || '<tr><td colspan="5" style="text-align: center; color: #999;">Tidak ada kasbon</td></tr>';
        }

        function deleteKasyon(id) {
            if (confirm('Hapus kasbon ini?')) {
                db.kasyon = db.kasyon.filter(k => k.id !== id);
                saveData();
                updateKasyonTable();
            }
        }

        // ===== STOK MANAGEMENT =====
        function addJajan() {
            const name = document.getElementById('jajanName').value;
            const price = parseInt(document.getElementById('jajanPrice').value) || 0;
            const stock = parseInt(document.getElementById('jajanStock').value) || 0;

            if (!name || price <= 0 || stock < 0) {
                alert('Isi semua field dengan benar!');
                return;
            }

            db.jajan.push({
                id: Date.now(),
                name,
                price,
                stock
            });

            saveData();
            alert('Jajan ditambahkan!');

            document.getElementById('jajanName').value = '';
            document.getElementById('jajanPrice').value = '';
            document.getElementById('jajanStock').value = '';

            updateJajanTable();
            updateProductSelects();
        }

        function updateJajanTable() {
            const tbody = document.getElementById('jajanTableBody');
            let html = '';

            db.jajan.forEach(j => {
                const totalValue = j.price * j.stock;
                html += `
                    <tr>
                        <td>${j.name}</td>
                        <td class="text-right currency">${formatCurrency(j.price)}</td>
                        <td class="text-right">${j.stock}</td>
                        <td class="text-right currency">${formatCurrency(totalValue)}</td>
                        <td>
                            <button class="btn btn-sm btn-primary" onclick="editJajan(${j.id})">Edit</button>
                        </td>
                    </tr>
                `;
            });

            tbody.innerHTML = html || '<tr><td colspan="5" style="text-align: center; color: #999;">Tidak ada jajan</td></tr>';
        }

        function editJajan(id) {
            const jajan = db.jajan.find(j => j.id === id);
            if (!jajan) return;

            currentEditingId = id;
            document.getElementById('editJajanName').value = jajan.name;
            document.getElementById('editJajanPrice').value = jajan.price;
            document.getElementById('editJajanStock').value = jajan.stock;

            document.getElementById('editJajanModal').classList.add('show');
        }

        function saveEditJajan() {
            const jajan = db.jajan.find(j => j.id === currentEditingId);
            if (!jajan) return;

            jajan.name = document.getElementById('editJajanName').value;
            jajan.price = parseInt(document.getElementById('editJajanPrice').value) || 0;
            jajan.stock = parseInt(document.getElementById('editJajanStock').value) || 0;

            saveData();
            closeModal('editJajanModal');
            updateJajanTable();
            updateProductSelects();
            alert('Jajan diperbarui!');
        }

        function deleteJajan() {
            if (confirm('Hapus jajan ini?')) {
                db.jajan = db.jajan.filter(j => j.id !== currentEditingId);
                saveData();
                closeModal('editJajanModal');
                updateJajanTable();
                updateProductSelects();
            }
        }

        function addParfum() {
            const name = document.getElementById('parfumName').value;
            const price = parseInt(document.getElementById('parfumPrice').value) || 0;
            const stock = parseInt(document.getElementById('parfumStock').value) || 0;

            if (!name || price <= 0 || stock < 0) {
                alert('Isi semua field dengan benar!');
                return;
            }

            db.parfum.push({
                id: Date.now(),
                name,
                price,
                stock
            });

            saveData();
            alert('Parfum ditambahkan!');

            document.getElementById('parfumName').value = '';
            document.getElementById('parfumPrice').value = '';
            document.getElementById('parfumStock').value = '';

            updateParfumTable();
            updateProductSelects();
        }

        function updateParfumTable() {
            const tbody = document.getElementById('parfumTableBody');
            let html = '';

            db.parfum.forEach(p => {
                const totalValue = p.price * p.stock;
                html += `
                    <tr>
                        <td>${p.name}</td>
                        <td class="text-right currency">${formatCurrency(p.price)}</td>
                        <td class="text-right">${p.stock}</td>
                        <td class="text-right currency">${formatCurrency(totalValue)}</td>
                        <td>
                            <button class="btn btn-sm btn-primary" onclick="editParfum(${p.id})">Edit</button>
                        </td>
                    </tr>
                `;
            });

            tbody.innerHTML = html || '<tr><td colspan="5" style="text-align: center; color: #999;">Tidak ada parfum</td></tr>';
        }

        function editParfum(id) {
            const parfum = db.parfum.find(p => p.id === id);
            if (!parfum) return;

            currentEditingId = id;
            document.getElementById('editParfumName').value = parfum.name;
            document.getElementById('editParfumPrice').value = parfum.price;
            document.getElementById('editParfumStock').value = parfum.stock;

            document.getElementById('editParfumModal').classList.add('show');
        }

        function saveEditParfum() {
            const parfum = db.parfum.find(p => p.id === currentEditingId);
            if (!parfum) return;

            parfum.name = document.getElementById('editParfumName').value;
            parfum.price = parseInt(document.getElementById('editParfumPrice').value) || 0;
            parfum.stock = parseInt(document.getElementById('editParfumStock').value) || 0;

            saveData();
            closeModal('editParfumModal');
            updateParfumTable();
            updateProductSelects();
            alert('Parfum diperbarui!');
        }

        function deleteParfum() {
            if (confirm('Hapus parfum ini?')) {
                db.parfum = db.parfum.filter(p => p.id !== currentEditingId);
                saveData();
                closeModal('editParfumModal');
                updateParfumTable();
                updateProductSelects();
            }
        }

        function updateProductSelects() {
            const select = document.getElementById('productSelect');
            const currentValue = select.value;
            select.innerHTML = '<option value="">-- Pilih --</option>';

            db.jajan.forEach(j => {
                const option = document.createElement('option');
                option.value = j.id;
                option.textContent = `[Jajan] ${j.name} - ${formatCurrency(j.price)}`;
                select.appendChild(option);
            });

            db.parfum.forEach(p => {
                const option = document.createElement('option');
                option.value = p.id;
                option.textContent = `[Parfum] ${p.name} - ${formatCurrency(p.price)}`;
                select.appendChild(option);
            });

            select.value = currentValue;
        }

        // ===== LAPORAN =====
        function generateLaporan() {
            const date = document.getElementById('laporanDate').value;
            const dayTransactions = db.transactions.filter(t => t.date === date);

            const washTrans = dayTransactions.filter(t => t.type === 'Cuci');
            const jajanTrans = dayTransactions.filter(t => t.type === 'Jajan');
            const parfumTrans = dayTransactions.filter(t => t.type === 'Parfum');

            const mobilCount = washTrans.filter(t => t.description.includes('Mobil')).length;
            const motorCount = washTrans.filter(t => t.description.includes('Motor')).length;

            const totalWash = washTrans.reduce((sum, t) => sum + t.amount, 0);
            const totalJajan = jajanTrans.reduce((sum, t) => sum + t.amount, 0);
            const totalParfum = parfumTrans.reduce((sum, t) => sum + t.amount, 0);

            const washCash = washTrans.filter(t => t.payment === 'Cash').reduce((sum, t) => sum + t.amount, 0);
            const washQris = washTrans.filter(t => t.payment === 'QRIS').reduce((sum, t) => sum + t.amount, 0);
            const washOther = washTrans.filter(t => t.payment === 'Lainnya').reduce((sum, t) => sum + t.amount, 0);

            const jajanCash = jajanTrans.filter(t => t.payment === 'Cash').reduce((sum, t) => sum + t.amount, 0);
            const jajanQris = jajanTrans.filter(t => t.payment === 'QRIS').reduce((sum, t) => sum + t.amount, 0);

            const parfumCash = parfumTrans.filter(t => t.payment === 'Cash').reduce((sum, t) => sum + t.amount, 0);
            const parfumQris = parfumTrans.filter(t => t.payment === 'QRIS').reduce((sum, t) => sum + t.amount, 0);

            const employeeShare = totalWash * 0.5;
            const ownerShare = totalWash * 0.5;

            const totalIncome = totalWash + totalJajan + totalParfum;
            const totalCash = washCash + jajanCash + parfumCash;
            const totalQris = washQris + jajanQris + parfumQris;

            let report = `
╔═════════════════════════════════════════════════════════════╗
║                LAPORAN KEUANGAN HARIAN                      ║
║                  KinerjaWorkshop                            ║
║                  Tanggal: ${date}                            ║
╚═════════════════════════════════════════════════════════════╝

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
1. KENDARAAN YANG DICUCI
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   Jumlah Mobil       : ${mobilCount} unit
   Jumlah Motor       : ${motorCount} unit
   ────────────────────────────────
   Total Kendaraan    : ${mobilCount + motorCount} unit

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
2. PENDAPATAN JASA CUCI
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   Total Cuci         : ${formatCurrency(totalWash)}
   ├─ Cash            : ${formatCurrency(washCash)}
   ├─ QRIS            : ${formatCurrency(washQris)}
   └─ Lainnya         : ${formatCurrency(washOther)}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
3. PENDAPATAN JAJAN
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   Total Jajan        : ${formatCurrency(totalJajan)}
   ├─ Cash            : ${formatCurrency(jajanCash)}
   └─ QRIS            : ${formatCurrency(jajanQris)}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
4. PENDAPATAN PARFUM
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   Total Parfum       : ${formatCurrency(totalParfum)}
   ├─ Cash            : ${formatCurrency(parfumCash)}
   └─ QRIS            : ${formatCurrency(parfumQris)}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
5. PEMBAGIAN GAJI CUCI
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   Total Cuci         : ${formatCurrency(totalWash)}
   Bagian Pemilik (50%): ${formatCurrency(ownerShare)}
   Bagian Karyawan (50%): ${formatCurrency(employeeShare)}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
6. RINGKASAN TOTAL UANG
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   Total Pendapatan   : ${formatCurrency(totalIncome)}
   ├─ Uang Tunai      : ${formatCurrency(totalCash)}
   └─ Uang QRIS       : ${formatCurrency(totalQris)}

   Bagian Pemilik     : ${formatCurrency(ownerShare + jajanCash + parfumCash)}
   Bagian Anak        : ${formatCurrency(employeeShare)}

╔═════════════════════════════════════════════════════════════╗
║                    LAPORAN SELESAI                          ║
╚═════════════════════════════════════════════════════════════╝
            `;

            document.getElementById('laporanContent').innerHTML = `<div class="monospace">${report}</div>`;
        }

        // ===== CHARTS =====
        function updateChart(type) {
            const monthStr = document.getElementById(`chartMonth${type === 'jajan' ? '1' : type === 'parfum' ? '2' : type === 'vehicle' ? '3' : '4'}`).value;
            if (!monthStr) return;

            const [year, month] = monthStr.split('-');
            const daysInMonth = new Date(year, month, 0).getDate();

            const labels = Array.from({length: daysInMonth}, (_, i) => i + 1);
            const data = [];

            for (let day = 1; day <= daysInMonth; day++) {
                const dateStr = `${year}-${month}-${String(day).padStart(2, '0')}`;
                let value = 0;

                if (type === 'jajan') {
                    value = db.transactions
                        .filter(t => t.date === dateStr && t.type === 'Jajan')
                        .reduce((sum, t) => sum + t.amount, 0);
                } else if (type === 'parfum') {
                    value = db.transactions
                        .filter(t => t.date === dateStr && t.type === 'Parfum')
                        .reduce((sum, t) => sum + t.amount, 0);
                } else if (type === 'vehicle') {
                    const mobilCount = db.transactions.filter(t => t.date === dateStr && t.type === 'Cuci' && t.description.includes('Mobil')).length;
                    const motorCount = db.transactions.filter(t => t.date === dateStr && t.type === 'Cuci' && t.description.includes('Motor')).length;
                    value = mobilCount + motorCount;
                } else if (type === 'income') {
                    value = db.transactions
                        .filter(t => t.date === dateStr && t.type === 'Cuci')
                        .reduce((sum, t) => sum + t.amount, 0);
                }

                data.push(value);
            }

            const canvasId = `${type}Chart`;
            const ctx = document.getElementById(canvasId);

            if (chartInstances[canvasId]) {
                chartInstances[canvasId].destroy();
            }

            const labels_display = {
                'jajan': 'Penjualan Jajan (Rp)',
                'parfum': 'Penjualan Parfum (Rp)',
                'vehicle': 'Jumlah Kendaraan',
                'income': 'Pendapatan Cuci (Rp)'
            };

            chartInstances[canvasId] = new Chart(ctx, {
                type: 'line',
                data: {
                    labels,
                    datasets: [{
                        label: labels_display[type],
                        data,
                        borderColor: '#667eea',
                        backgroundColor: 'rgba(102, 126, 234, 0.1)',
                        borderWidth: 2,
                        tension: 0.4,
                        fill: true
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: true,
                    plugins: {
                        legend: {
                            display: true,
                            position: 'top'
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                callback: function(value) {
                                    if (type === 'vehicle') return value;
                                    return 'Rp ' + value.toLocaleString('id-ID');
                                }
                            }
                        }
                    }
                }
            });
        }

        // ===== UPDATE PAGES =====
        function updateDashboard() {
            const dayTransactions = db.transactions.filter(t => t.date === today);
            const totalIncome = dayTransactions.reduce((sum, t) => sum + t.amount, 0);
            const vehicleCount = dayTransactions.filter(t => t.type === 'Cuci').length;
            const totalKasyon = db.kasyon.filter(k => k.date === today).reduce((sum, k) => sum + k.amount, 0);

            document.getElementById('todayIncome').textContent = formatCurrency(totalIncome);
            document.getElementById('totalVehicles').textContent = vehicleCount;
            document.getElementById('totalEmployees').textContent = db.employees.length;
            document.getElementById('totalKasbon').textContent = formatCurrency(totalKasyon);

            // Transaction table
            const tbody = document.getElementById('dashboardTableBody');
            let html = '';
            dayTransactions.slice(-10).reverse().forEach(t => {
                html += `
                    <tr>
                        <td>${t.time}</td>
                        <td>${t.type}</td>
                        <td>${t.description}</td>
                        <td class="currency">${formatCurrency(t.amount)}</td>
                    </tr>
                `;
            });
            tbody.innerHTML = html || '<tr><td colspan="4" style="text-align: center; color: #999;">Tidak ada transaksi</td></tr>';

            // Employee table
            const empTbody = document.getElementById('dashboardEmployeeTable');
            let empHtml = '';
            db.employees.forEach(emp => {
                const wage = calculateDailyWage(today, emp.id);
                const status = getEmployeeStatusOnDate(emp.id, today);
                const statusBadge = `<span class="badge badge-${status === 'Training' ? 'training' : 'staf'}">${status}</span>`;
                empHtml += `
                    <tr>
                        <td>${emp.name}</td>
                        <td>${statusBadge}</td>
                        <td class="currency">${formatCurrency(wage)}</td>
                    </tr>
                `;
            });
            empTbody.innerHTML = empHtml || '<tr><td colspan="3" style="text-align: center; color: #999;">Tidak ada karyawan</td></tr>';
        }

        function updatePenjualanPage() {
            updateTransactionTable();
            updateProductSelects();
            updateEmployeeSelects();
            updateCartDisplay();
        }

        function updateGajiPage() {
            updateEmployeeTable();
            updateKasyonTable();
            updateEmployeeSelects();
            showDailyWages();
        }

        function updateLaporanPage() {
            generateLaporan();
            updateChart('jajan');
            updateChart('parfum');
            updateChart('vehicle');
            updateChart('income');
        }

        function updateStokPage() {
            updateJajanTable();
            updateParfumTable();
            updateProductSelects();
        }

        // ===== INITIALIZATION =====
        loadData();
        updateDashboard();
    </script>
</body>
</html>
