<!DOCTYPE html>
<html lang="id" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Master Ekspedisi - Cabang Samarinda</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Inter Font -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        body { font-family: 'Inter', sans-serif; }
        ::-webkit-scrollbar { width: 6px; height: 6px; }
        ::-webkit-scrollbar-track { background: #f8fafc; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 9999px; }
        ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }

        /* Subtle glitter / sparkle background pattern on clean white */
        .glitter-bg {
            background-color: #ffffff;
            background-image: 
                radial-gradient(#7c3aed 0.75px, transparent 0.75px), 
                radial-gradient(#a855f7 0.75px, #ffffff 0.75px);
            background-size: 30px 30px;
            background-position: 0 0, 15px 15px;
            background-opacity: 0.05;
        }
    </style>
</head>
<body class="glitter-bg text-slate-800 h-full flex flex-col">

    <!-- Top Navbar -->
    <header class="bg-violet-900 text-white shadow-lg sticky top-0 z-30 border-b border-violet-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="bg-violet-800 p-2 rounded-lg text-violet-200 border border-violet-700">
                    <i data-lucide="truck" class="w-6 h-6"></i>
                </div>
                <div>
                    <h1 class="font-bold text-lg leading-tight tracking-tight text-white">Master Ekspedisi</h1>
                    <p class="text-xs text-violet-300">Pusat Logistik & Jaringan Pengiriman • Cabang Samarinda</p>
                </div>
            </div>
            <div class="flex items-center space-x-3">
                <button onclick="exportPDFReport()" class="text-xs bg-violet-800 hover:bg-violet-700 text-violet-100 px-3.5 py-2 rounded-lg border border-violet-700 transition flex items-center gap-1.5 shadow-sm font-semibold cursor-pointer">
                    <i data-lucide="printer" class="w-4 h-4"></i> Cetak Laporan PDF
                </button>
                <div class="hidden sm:flex items-center bg-violet-800/80 px-3 py-1.5 rounded-lg text-xs border border-violet-700/60 text-white">
                    <i data-lucide="calendar" class="w-3.5 h-3.5 mr-1.5 text-violet-300"></i>
                    <span id="currentDateDisplay"></span>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 flex flex-col gap-6">

        <!-- Summary Cards Grid -->
        <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
            <!-- Card 1: Total Ekspedisi -->
            <div class="bg-white/90 backdrop-blur-md rounded-xl shadow-md border border-violet-100 p-5 flex items-center justify-between">
                <div>
                    <p class="text-xs font-semibold uppercase tracking-wider text-violet-600">Total Mitra Ekspedisi</p>
                    <h3 class="text-2xl font-bold text-slate-900 mt-1" id="statTotalExpeditions">0</h3>
                    <p class="text-xs text-emerald-600 mt-1 flex items-center"><span id="statActiveExpeditions" class="font-semibold mr-1">0</span> Mitra Aktif</p>
                </div>
                <div class="bg-violet-50 text-violet-600 p-3 rounded-xl border border-violet-100">
                    <i data-lucide="building-2" class="w-6 h-6"></i>
                </div>
            </div>
            <!-- Card 2: Active Routes -->
            <div class="bg-white/90 backdrop-blur-md rounded-xl shadow-md border border-violet-100 p-5 flex items-center justify-between">
                <div>
                    <p class="text-xs font-semibold uppercase tracking-wider text-violet-600">Rute Pengiriman Terdaftar</p>
                    <h3 class="text-2xl font-bold text-slate-900 mt-1" id="statTotalRoutes">0</h3>
                    <p class="text-xs text-slate-500 mt-1">Cakupan Antar Kota & Provinsi</p>
                </div>
                <div class="bg-violet-50 text-violet-600 p-3 rounded-xl border border-violet-100">
                    <i data-lucide="map-pin" class="w-6 h-6"></i>
                </div>
            </div>
            <!-- Card 3: Status Terpadu -->
            <div class="bg-white/90 backdrop-blur-md rounded-xl shadow-md border border-violet-100 p-5 flex items-center justify-between">
                <div>
                    <p class="text-xs font-semibold uppercase tracking-wider text-violet-600">Sistem Tarif & Ekspedisi</p>
                    <h3 class="text-2xl font-bold text-slate-900 mt-1">Terpadu</h3>
                    <p class="text-xs text-emerald-600 mt-1 flex items-center"><i data-lucide="check-circle" class="w-3.5 h-3.5 mr-1"></i> Data Aktif & Siap Cetak</p>
                </div>
                <div class="bg-violet-50 text-emerald-600 p-3 rounded-xl border border-violet-100">
                    <i data-lucide="file-text" class="w-6 h-6"></i>
                </div>
            </div>
        </div>

        <!-- Single Unified Content Box -->
        <div class="bg-white/90 backdrop-blur-md rounded-xl shadow-lg border border-violet-100 overflow-hidden flex flex-col">
            <div class="p-6 space-y-6 flex-1">
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 pb-4 border-b border-violet-100">
                    <div>
                        <h2 class="text-lg font-bold text-slate-900">Direktori Perusahaan Ekspedisi & Tarif Terpadu</h2>
                        <p class="text-xs text-slate-500">Kelola informasi dasar ekspedisi, rute, kontak PIC, metode pembayaran, serta rincian tarif per Kg, Koli, dan Kubikasi (m³) dalam satu tampilan.</p>
                    </div>
                    <div class="flex items-center gap-2 w-full sm:w-auto">
                        <div class="relative w-full sm:w-72">
                            <i data-lucide="search" class="w-4 h-4 text-slate-400 absolute left-3 top-2.5"></i>
                            <input type="text" id="searchGlobalEkspedisi" oninput="renderEkspedisiTarifTable()" placeholder="Cari nama, kota, pembayaran, atau PIC..." class="text-xs pl-9 pr-3 py-2 border border-violet-200 bg-white text-slate-800 rounded-lg focus:outline-none focus:ring-2 focus:ring-violet-500 w-full placeholder-slate-400">
                        </div>
                        <button onclick="openEkspedisiModal()" class="bg-violet-600 hover:bg-violet-700 text-white px-3.5 py-2 rounded-lg text-xs font-semibold flex items-center gap-1.5 transition shadow-sm shrink-0 border border-violet-700">
                            <i data-lucide="plus" class="w-4 h-4"></i> Tambah Ekspedisi
                        </button>
                    </div>
                </div>

                <div class="overflow-x-auto rounded-lg border border-violet-100 bg-white">
                    <table class="w-full text-left border-collapse text-xs">
                        <thead class="bg-violet-50 text-violet-900 uppercase font-semibold border-b border-violet-100">
                            <tr>
                                <th class="p-3">Ekspedisi & Layanan</th>
                                <th class="p-3">Kontak & PIC</th>
                                <th class="p-3">Rute (Asal &rarr; Tujuan)</th>
                                <th class="p-3">Rincian Tarif (Kg / Koli / m³)</th>
                                <th class="p-3">Admin, DG & Pembayaran</th>
                                <th class="p-3">Status</th>
                                <th class="p-3 text-right">Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="ekspedisiTarifTableBody" class="divide-y divide-violet-100 text-slate-700">
                            <!-- Populated dynamically -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

    </main>

    <!-- MODAL CONTAINER -->
    <div id="genericModal" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white border border-violet-100 rounded-xl shadow-2xl max-w-lg w-full max-h-[90vh] overflow-y-auto flex flex-col text-slate-800">
            <div class="p-4 border-b border-violet-100 flex items-center justify-between bg-violet-50 rounded-t-xl">
                <h3 id="modalTitle" class="font-bold text-sm text-violet-900 flex items-center gap-2">Form</h3>
                <button onclick="closeModal()" class="text-slate-400 hover:text-slate-700 p-1 rounded-lg">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>
            </div>
            <div id="modalBody" class="p-5 flex-1 space-y-4 text-xs">
                <!-- Dynamic form fields -->
            </div>
        </div>
    </div>

    <!-- Notification Toast -->
    <div id="toast" class="fixed bottom-5 right-5 bg-slate-900 border border-slate-700 text-white px-4 py-3 rounded-xl shadow-2xl text-xs flex items-center gap-2.5 transition-all duration-300 transform translate-y-20 opacity-0 z-50">
        <i data-lucide="check-circle" class="w-4 h-4 text-emerald-400" id="toastIcon"></i>
        <span id="toastMsg">Aksi berhasil dilakukan</span>
    </div>

    <!-- Script Logic -->
    <script>
        // Initial Demo State Data
        const defaultData = {
            ekspedisi: [
                { 
                    id: "EXP-001", 
                    nama: "JNE Express Samarinda", 
                    jenis: "darat", 
                    alamat: "Jl. Ir. H. Juanda No. 45, Samarinda", 
                    pic: "Budi Santoso", 
                    telepon: "081234567890", 
                    status: "aktif", 
                    asal: "samarinda", 
                    tujuan: "balikpapan", 
                    leadTime: "1-2 Hari", 
                    minKirim: "5 Kg", 
                    barang: "Dokumen, Elektronik",
                    tarifKg: 6000,
                    tarifKoli: 25000,
                    tarifKubik: 250000,
                    admin: 5000,
                    handling: 10000,
                    minimCas: 50000,
                    payment: "Transfer Bank / COD",
                    berlaku: "2026-01-01",
                    sumber: "Surat Penawaran Resmi"
                },
                { 
                    id: "EXP-002", 
                    nama: "Samudera Logistik Lines", 
                    jenis: "laut", 
                    alamat: "Pelabuhan Mahakam, Jl. Yos Sudarso, Samarinda", 
                    pic: "Siti Rahma", 
                    telepon: "081398765432", 
                    status: "aktif", 
                    asal: "surabaya", 
                    tujuan: "tarakan", 
                    leadTime: "4-5 Hari", 
                    minKirim: "50 Kg", 
                    barang: "Cargo Industri, Sembako",
                    tarifKg: 4500,
                    tarifKoli: null,
                    tarifKubik: 180000,
                    admin: 10000,
                    handling: 25000,
                    minimCas: 150000,
                    payment: "Tempo 30 Hari",
                    berlaku: "2026-02-15",
                    sumber: "Price List Pelabuhan"
                },
                { 
                    id: "EXP-003", 
                    nama: "Borneo Cargo Trucking", 
                    jenis: "trucking", 
                    alamat: "Jl. Cipto Mangunkusumo No. 12, Samarinda Seberang", 
                    pic: "Joko Widodo", 
                    telepon: "082155556666", 
                    status: "aktif", 
                    asal: "samarinda", 
                    tujuan: "sangatta", 
                    leadTime: "1 Hari", 
                    minKirim: "30 Kg", 
                    barang: "Alat Berat, Material",
                    tarifKg: 7000,
                    tarifKoli: 30000,
                    tarifKubik: null,
                    admin: 5000,
                    handling: 20000,
                    minimCas: 100000,
                    payment: "Transfer Bank",
                    berlaku: "2026-01-10",
                    sumber: "Konfirmasi WhatsApp"
                },
                { 
                    id: "EXP-004", 
                    nama: "Kaltim Indah Bus", 
                    jenis: "bus", 
                    alamat: "Terminal Lempake, Samarinda Utara", 
                    pic: "Ahmad Fauzi", 
                    telepon: "085211112222", 
                    status: "tidak aktif", 
                    asal: "balikpapan", 
                    tujuan: "bontang", 
                    leadTime: "1 Hari", 
                    minKirim: "10 Kg", 
                    barang: "Paket Kilat",
                    tarifKg: 8000,
                    tarifKoli: 35000,
                    tarifKubik: null,
                    admin: 3000,
                    handling: 5000,
                    minimCas: 40000,
                    payment: "Cash / Bayar di Loket",
                    berlaku: "2026-01-05",
                    sumber: "Tarif Loket Terminal"
                }
            ]
        };

        let db = JSON.parse(localStorage.getItem('master_ekspedisi_db')) || defaultData;

        function saveDB() {
            localStorage.setItem('master_ekspedisi_db', JSON.stringify(db));
            initApp();
        }

        window.onload = function() {
            document.getElementById('currentDateDisplay').innerText = new Date().toLocaleDateString('id-ID', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
            initApp();
            lucide.createIcons();
        };

        function initApp() {
            updateDashboardStats();
            renderEkspedisiTarifTable();
            lucide.createIcons();
        }

        function updateDashboardStats() {
            document.getElementById('statTotalExpeditions').innerText = db.ekspedisi.length;
            const activeCount = db.ekspedisi.filter(e => e.status === 'aktif').length;
            document.getElementById('statActiveExpeditions').innerText = activeCount;
            document.getElementById('statTotalRoutes').innerText = db.ekspedisi.length;
        }

        function renderEkspedisiTarifTable() {
            const query = document.getElementById('searchGlobalEkspedisi')?.value.toLowerCase() || '';
            const tbody = document.getElementById('ekspedisiTarifTableBody');
            if (!tbody) return;
            tbody.innerHTML = '';

            const filtered = db.ekspedisi.filter(e => 
                e.nama.toLowerCase().includes(query) || 
                e.pic.toLowerCase().includes(query) || 
                e.tujuan.toLowerCase().includes(query) ||
                e.asal.toLowerCase().includes(query) ||
                e.jenis.toLowerCase().includes(query) ||
                (e.payment && e.payment.toLowerCase().includes(query))
            );

            if (filtered.length === 0) {
                tbody.innerHTML = `<tr><td colspan="7" class="p-6 text-center text-slate-400">Tidak ada data ekspedisi atau tarif ditemukan.</td></tr>`;
                return;
            }

            filtered.forEach(e => {
                const badge = e.status === 'aktif' 
                    ? `<span class="bg-emerald-50 text-emerald-700 px-2.5 py-1 rounded-md font-medium border border-emerald-200 shadow-sm">Aktif</span>`
                    : `<span class="bg-slate-100 text-slate-500 px-2.5 py-1 rounded-md font-medium border border-slate-200 shadow-sm">Tidak Aktif</span>`;
                
                const tKg = (e.tarifKg !== null && e.tarifKg !== undefined && e.tarifKg !== '') ? `Rp ${Number(e.tarifKg).toLocaleString('id-ID')} /kg` : '<span class="text-slate-400 italic">N/A</span>';
                const tKoli = (e.tarifKoli !== null && e.tarifKoli !== undefined && e.tarifKoli !== '') ? `Rp ${Number(e.tarifKoli).toLocaleString('id-ID')} /koli` : '<span class="text-slate-400 italic">N/A</span>';
                const tKubik = (e.tarifKubik !== null && e.tarifKubik !== undefined && e.tarifKubik !== '') ? `Rp ${Number(e.tarifKubik).toLocaleString('id-ID')} /m³` : '<span class="text-slate-400 italic">N/A</span>';
                const paymentInfo = e.payment ? `<div class="text-[11px] font-medium text-violet-800 mt-1 flex items-center gap-1"><i data-lucide="credit-card" class="w-3 h-3"></i> ${e.payment}</div>` : '';

                tbody.innerHTML += `
                    <tr class="hover:bg-violet-50/50 transition">
                        <td class="p-3">
                            <div class="font-semibold text-slate-900">${e.nama}</div>
                            <div class="text-[11px] font-medium text-violet-700 uppercase">Layanan: ${e.jenis}</div>
                            <div class="text-[10px] text-slate-500">${e.alamat}</div>
                        </td>
                        <td class="p-3">
                            <div class="font-medium text-slate-800">${e.pic}</div>
                            <div class="text-slate-500 text-[11px]">${e.telepon}</div>
                        </td>
                        <td class="p-3">
                            <div class="font-bold text-slate-900 uppercase">${e.asal} &rarr; <span class="text-violet-700">${e.tujuan}</span></div>
                            <div class="text-[11px] text-slate-500">Lead Time: ${e.leadTime}</div>
                        </td>
                        <td class="p-3">
                            <div class="font-mono text-violet-900">${tKg}</div>
                            <div class="font-mono text-violet-900">${tKoli}</div>
                            <div class="font-mono text-violet-900">${tKubik}</div>
                        </td>
                        <td class="p-3 text-slate-600">
                            <div>Admin: Rp ${Number(e.admin || 0).toLocaleString('id-ID')}</div>
                            <div>Biaya DG: Rp ${Number(e.handling || 0).toLocaleString('id-ID')}</div>
                            <div>Minim Cas: Rp ${Number(e.minimCas || 0).toLocaleString('id-ID')}</div>
                            ${paymentInfo}
                            <div class="text-[10px] text-slate-400 italic mt-0.5">Sumber: ${e.sumber || '-'}</div>
                        </td>
                        <td class="p-3">${badge}</td>
                        <td class="p-3 text-right space-x-1">
                            <button onclick="openEkspedisiModal('${e.id}')" class="p-1.5 text-slate-500 hover:bg-violet-100 rounded-lg transition" title="Edit"><i data-lucide="edit" class="w-4 h-4"></i></button>
                            <button onclick="deleteEkspedisi('${e.id}')" class="p-1.5 text-rose-500 hover:bg-rose-50 rounded-lg transition" title="Hapus"><i data-lucide="trash-2" class="w-4 h-4"></i></button>
                        </td>
                    </tr>
                `;
            });
            lucide.createIcons();
        }

        function openEkspedisiModal(id = null) {
            const isEdit = id !== null;
            let item = { 
                nama: '', jenis: 'darat', alamat: '', pic: '', telepon: '', status: 'aktif', 
                asal: 'samarinda', tujuan: 'balikpapan', leadTime: '', minKirim: '1 Kg', barang: 'Umum',
                tarifKg: '', tarifKoli: '', tarifKubik: '', admin: 5000, handling: 10000, minimCas: 50000, payment: 'Transfer Bank', berlaku: new Date().toISOString().split('T')[0], sumber: '' 
            };
            if (isEdit) {
                item = db.ekspedisi.find(e => e.id === id);
            }

            const originCities = ['samarinda', 'balikpapan', 'surabaya', 'banjarmasin', 'jakarta'];
            const destCities = ['tarakan', 'malinau', 'nunukan', 'bulungan', 'berau', 'wahau', 'melak', 'sangatta', 'bontang', 'balikpapan', 'samarinda', 'surabaya', 'jakarta'];

            const originOptions = originCities.map(c => `<option value="${c}" ${item.asal === c ? 'selected' : ''}>${c.toUpperCase()}</option>`).join('');
            const destOptions = destCities.map(c => `<option value="${c}" ${item.tujuan === c ? 'selected' : ''}>${c.toUpperCase()}</option>`).join('');

            document.getElementById('modalTitle').innerHTML = `<i data-lucide="building" class="w-4 h-4 text-violet-600"></i> ${isEdit ? 'Edit Data Ekspedisi & Tarif' : 'Tambah Ekspedisi & Tarif Baru'}`;
            document.getElementById('modalBody').innerHTML = `
                <form id="formEkspedisi" onsubmit="saveEkspedisi(event, '${id || ''}')" class="space-y-3">
                    <div>
                        <label class="block font-medium text-slate-700 mb-1">Nama Perusahaan Ekspedisi *</label>
                        <input type="text" id="expNama" required value="${item.nama}" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                    </div>
                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Jenis Layanan *</label>
                            <select id="expJenis" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                                <option value="darat" ${item.jenis === 'darat' ? 'selected' : ''}>Darat</option>
                                <option value="laut" ${item.jenis === 'laut' ? 'selected' : ''}>Laut</option>
                                <option value="trucking" ${item.jenis === 'trucking' ? 'selected' : ''}>Trucking</option>
                                <option value="bus" ${item.jenis === 'bus' ? 'selected' : ''}>Bus</option>
                            </select>
                        </div>
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Status Kerja Sama *</label>
                            <select id="expStatus" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                                <option value="aktif" ${item.status === 'aktif' ? 'selected' : ''}>Aktif</option>
                                <option value="tidak aktif" ${item.status === 'tidak aktif' ? 'selected' : ''}>Tidak Aktif</option>
                            </select>
                        </div>
                    </div>
                    <div>
                        <label class="block font-medium text-slate-700 mb-1">Alamat Kantor / Gudang *</label>
                        <textarea id="expAlamat" rows="2" required class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">${item.alamat}</textarea>
                    </div>
                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Nama PIC *</label>
                            <input type="text" id="expPic" required value="${item.pic}" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                        </div>
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Nomor Telepon / WhatsApp *</label>
                            <input type="text" id="expTelepon" required value="${item.telepon}" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                        </div>
                    </div>
                    <hr class="border-violet-100 my-2">
                    <div class="text-xs font-bold text-violet-800 uppercase">Informasi Rute & Lead Time</div>
                    <div class="grid grid-cols-3 gap-3">
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Kota Asal *</label>
                            <select id="expAsal" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500 uppercase">
                                ${originOptions}
                            </select>
                        </div>
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Kota Tujuan *</label>
                            <select id="expTujuan" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500 uppercase">
                                ${destOptions}
                            </select>
                        </div>
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Lead Time *</label>
                            <input type="text" id="expLeadTime" required placeholder="Cth: 1-2 Hari" value="${item.leadTime || ''}" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                        </div>
                    </div>
                    <hr class="border-violet-100 my-2">
                    <div class="text-xs font-bold text-violet-800 uppercase">Rincian Tarif & Pembayaran (Bisa Dikosongkan)</div>
                    <div class="grid grid-cols-3 gap-3">
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Tarif / Kg (Rp)</label>
                            <input type="number" id="expTarifKg" value="${item.tarifKg !== null && item.tarifKg !== undefined ? item.tarifKg : ''}" placeholder="Kosongkan jika N/A" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                        </div>
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Tarif / Koli (Rp)</label>
                            <input type="number" id="expTarifKoli" value="${item.tarifKoli !== null && item.tarifKoli !== undefined ? item.tarifKoli : ''}" placeholder="Kosongkan jika N/A" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                        </div>
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Tarif / m³ (Rp)</label>
                            <input type="number" id="expTarifKubik" value="${item.tarifKubik !== null && item.tarifKubik !== undefined ? item.tarifKubik : ''}" placeholder="Kosongkan jika N/A" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                        </div>
                    </div>
                    <div class="grid grid-cols-3 gap-3">
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Biaya Admin (Rp)</label>
                            <input type="number" id="expAdmin" value="${item.admin !== undefined ? item.admin : 0}" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                        </div>
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Biaya DG (Rp)</label>
                            <input type="number" id="expHandling" value="${item.handling !== undefined ? item.handling : 0}" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                        </div>
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Minim Cas (Rp)</label>
                            <input type="number" id="expMinimCas" value="${item.minimCas !== undefined ? item.minimCas : 0}" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                        </div>
                    </div>
                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Metode Pembayaran *</label>
                            <input type="text" id="expPayment" required value="${item.payment || 'Transfer Bank'}" placeholder="Cth: Transfer / COD" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                        </div>
                        <div>
                            <label class="block font-medium text-slate-700 mb-1">Sumber Tarif *</label>
                            <input type="text" id="expSumber" required value="${item.sumber || ''}" placeholder="Cth: Surat Penawaran" class="w-full p-2.5 border border-violet-200 bg-white text-slate-800 rounded-lg focus:ring-2 focus:ring-violet-500">
                        </div>
                    </div>
                    <div class="flex justify-end gap-2 pt-3 border-t border-violet-100">
                        <button type="button" onclick="closeModal()" class="px-4 py-2 border border-violet-200 rounded-lg text-slate-600 hover:bg-violet-50">Batal</button>
                        <button type="submit" class="px-4 py-2 bg-violet-600 hover:bg-violet-700 text-white rounded-lg font-semibold shadow-sm border border-violet-700">Simpan</button>
                    </div>
                </form>
            `;
            document.getElementById('genericModal').classList.remove('hidden');
            lucide.createIcons();
        }

        function saveEkspedisi(e, id) {
            e.preventDefault();
            const kgVal = document.getElementById('expTarifKg').value;
            const koliVal = document.getElementById('expTarifKoli').value;
            const kubikVal = document.getElementById('expTarifKubik').value;

            const data = {
                id: id || `EXP-${Date.now().toString().slice(-4)}`,
                nama: document.getElementById('expNama').value,
                jenis: document.getElementById('expJenis').value,
                alamat: document.getElementById('expAlamat').value,
                pic: document.getElementById('expPic').value,
                telepon: document.getElementById('expTelepon').value,
                status: document.getElementById('expStatus').value,
                asal: document.getElementById('expAsal').value,
                tujuan: document.getElementById('expTujuan').value,
                leadTime: document.getElementById('expLeadTime').value,
                minKirim: "1 Kg",
                barang: "Umum",
                tarifKg: kgVal !== '' ? parseFloat(kgVal) : null,
                tarifKoli: koliVal !== '' ? parseFloat(koliVal) : null,
                tarifKubik: kubikVal !== '' ? parseFloat(kubikVal) : null,
                admin: parseFloat(document.getElementById('expAdmin').value) || 0,
                handling: parseFloat(document.getElementById('expHandling').value) || 0,
                minimCas: parseFloat(document.getElementById('expMinimCas').value) || 0,
                payment: document.getElementById('expPayment').value,
                berlaku: new Date().toISOString().split('T')[0],
                sumber: document.getElementById('expSumber').value
            };

            if (id) {
                const idx = db.ekspedisi.findIndex(item => item.id === id);
                db.ekspedisi[idx] = data;
                showToast("Data ekspedisi & tarif berhasil diperbarui!");
            } else {
                db.ekspedisi.push(data);
                showToast("Data ekspedisi & tarif baru berhasil ditambahkan!");
            }

            closeModal();
            saveDB();
        }

        function deleteEkspedisi(id) {
            if (confirm("Apakah Anda yakin ingin menghapus ekspedisi ini?")) {
                db.ekspedisi = db.ekspedisi.filter(e => e.id !== id);
                saveDB();
                showToast("Data ekspedisi berhasil dihapus.");
            }
        }

        function exportPDFReport() {
            const currentDate = new Date().toLocaleDateString('id-ID', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
            
            let htmlContent = `
                <!DOCTYPE html>
                <html lang="id">
                <head>
                    <meta charset="UTF-8">
                    <title>Laporan Master Ekspedisi & Tarif - Cabang Samarinda</title>
                    <style>
                        body { font-family: Arial, sans-serif; color: #1e293b; padding: 25px; font-size: 11px; }
                        h1 { font-size: 16px; margin-bottom: 2px; text-transform: uppercase; color: #581c87; }
                        p.subtitle { font-size: 11px; color: #64748b; margin-top: 0; margin-bottom: 15px; }
                        table { width: 100%; border-collapse: collapse; margin-top: 10px; }
                        th, td { border: 1px solid #cbd5e1; padding: 7px; text-align: left; vertical-align: top; }
                        th { background-color: #f3e8ff; color: #581c87; font-weight: bold; }
                        .badge { padding: 2px 6px; border-radius: 4px; font-size: 9px; font-weight: bold; }
                        .active { background: #d1fae5; color: #065f46; }
                        .inactive { background: #f1f5f9; color: #475569; }
                        .footer { margin-top: 25px; text-align: right; font-size: 10px; color: #64748b; }
                    </style>
                </head>
                <body>
                    <h1>Laporan Master Ekspedisi & Tarif Pengiriman</h1>
                    <p class="subtitle">Pusat Logistik & Jaringan Pengiriman • Cabang Samarinda | Dicetak pada: ${currentDate}</p>
                    
                    <table>
                        <thead>
                            <tr>
                                <th>No</th>
                                <th>Nama Ekspedisi & Layanan</th>
                                <th>Kontak & PIC</th>
                                <th>Rute (Asal &rarr; Tujuan)</th>
                                <th>Tarif (Kg / Koli / m³)</th>
                                <th>Admin, Biaya DG, Minim Cas & Pembayaran</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
            `;

            db.ekspedisi.forEach((e, idx) => {
                const tKg = e.tarifKg !== null && e.tarifKg !== undefined && e.tarifKg !== '' ? `Rp ${Number(e.tarifKg).toLocaleString('id-ID')} /kg` : 'N/A';
                const tKoli = e.tarifKoli !== null && e.tarifKoli !== undefined && e.tarifKoli !== '' ? `Rp ${Number(e.tarifKoli).toLocaleString('id-ID')} /koli` : 'N/A';
                const tKubik = e.tarifKubik !== null && e.tarifKubik !== undefined && e.tarifKubik !== '' ? `Rp ${Number(e.tarifKubik).toLocaleString('id-ID')} /m³` : 'N/A';

                htmlContent += `
                    <tr>
                        <td>${idx + 1}</td>
                        <td>
                            <b>${e.nama}</b><br>
                            <span style="font-size: 10px; color: #7c3aed; text-transform: uppercase;">${e.jenis}</span><br>
                            <span style="font-size: 9px; color: #64748b;">${e.alamat}</span>
                        </td>
                        <td>
                            ${e.pic}<br>
                            <span style="font-size: 10px; color: #64748b;">${e.telepon}</span>
                        </td>
                        <td>
                            <b>${e.asal.toUpperCase()} &rarr; ${e.tujuan.toUpperCase()}</b><br>
                            <span style="font-size: 10px; color: #64748b;">Lead Time: ${e.leadTime}</span>
                        </td>
                        <td>
                            <div>${tKg}</div>
                            <div>${tKoli}</div>
                            <div>${tKubik}</div>
                        </td>
                        <td>
                            Admin: Rp ${Number(e.admin || 0).toLocaleString('id-ID')}<br>
                            Biaya DG: Rp ${Number(e.handling || 0).toLocaleString('id-ID')}<br>
                            Minim Cas: Rp ${Number(e.minimCas || 0).toLocaleString('id-ID')}<br>
                            <b>Pembayaran:</b> ${e.payment || '-'}<br>
                            <span style="font-size: 9px; color: #64748b; font-style: italic;">Sumber: ${e.sumber || '-'}</span>
                        </td>
                        <td><span class="badge ${e.status === 'aktif' ? 'active' : 'inactive'}">${e.status.toUpperCase()}</span></td>
                    </tr>
                `;
            });

            htmlContent += `
                        </tbody>
                    </table>
                    <div class="footer">
                        <p>Dokumen Resmi Logistik Cabang Samarinda — Dicetak dari Sistem Master Ekspedisi</p>
                    </div>
                </body>
                </html>
            `;

            const printWindow = window.open('', '_blank');
            if (printWindow) {
                printWindow.document.write(htmlContent);
                printWindow.document.close();
                printWindow.focus();
                setTimeout(() => {
                    printWindow.print();
                }, 500);
            } else {
                const blob = new Blob([htmlContent], { type: 'text/html;charset=utf-8' });
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = `Laporan_Master_Ekspedisi_${new Date().toISOString().split('T')[0]}.html`;
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                URL.revokeObjectURL(url);
                showToast("Pop-up diblokir browser. Laporan diunduh sebagai file HTML siap cetak.");
            }
        }

        // Modal Utility Helpers
        function closeModal() {
            document.getElementById('genericModal').classList.add('hidden');
        }

        function showToast(msg) {
            const toast = document.getElementById('toast');
            document.getElementById('toastMsg').innerText = msg;
            toast.classList.remove('translate-y-20', 'opacity-0');
            setTimeout(() => {
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }
    </script>
</body>
</html>
