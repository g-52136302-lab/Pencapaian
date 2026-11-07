<html lang="ms">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>e-Pencapaian - SMKA Tun Ahmadshah</title>
    
    <!-- SDK & Frameworks -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.28/jspdf.plugin.autotable.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;700&family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
 
    <style>
        :root {
            --neon-cyan: #06b6d4;
            --neon-blue: #3b82f6;
            --neon-purple: #a855f7;
            --glass-bg: rgba(15, 23, 42, 0.45);
            --glass-border: rgba(255, 255, 255, 0.1);
        }
        
        body { 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            background-color: #020617;
            color: #f8fafc;
            overflow: hidden;
            height: 100vh; /* Fallback */
            height: 100dvh;
        }
 
        .font-header { font-family: 'Space Grotesk', sans-serif; }
        
        .bg-cyber {
            background: 
                radial-gradient(circle at 20% 30%, rgba(6, 182, 212, 0.15) 0%, transparent 40%),
                radial-gradient(circle at 80% 70%, rgba(99, 102, 241, 0.15) 0%, transparent 40%),
                linear-gradient(to bottom, #020617, #0f172a);
        }
        
        .dot-grid {
            background-image: radial-gradient(rgba(255,255,255,0.05) 1px, transparent 1px);
            background-size: 30px 30px;
        }
        
        .silhouette {
            position: absolute;
            left: 50%; top: 50%;
            transform: translate(-50%, -50%);
            width: 700px;
            opacity: 0.4;
            mask-image: radial-gradient(circle, black 55%, transparent 95%);
            pointer-events: none;
            z-index: 0;
            filter: drop-shadow(0 0 40px rgba(6, 182, 212, 0.4)) saturate(1.5);
        }
 
        .glass {
            background: var(--glass-bg);
            backdrop-filter: blur(25px);
            -webkit-backdrop-filter: blur(25px);
            border: 1px solid var(--glass-border);
            box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.7);
        }
 
        .orb {
            width: 80px; height: 80px; border-radius: 50%;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            font-weight: 800; cursor: pointer; transition: all 0.4s ease;
            position: absolute; z-index: 10;
        }
        
        @media (max-width: 640px) {
            .orb { width: 55px; height: 55px; font-size: 8px; }
            .silhouette { width: 400px; }
            .center-hub { padding: 1rem; transform: scale(0.9); }
        }
 
        .orb:hover { transform: scale(1.15) translateY(-5px); box-shadow: 0 0 25px var(--neon-cyan); }
        .orb-active { box-shadow: 0 0 35px var(--neon-cyan); border: 2px solid var(--neon-cyan); transform: scale(1.1); background: rgba(6, 182, 212, 0.2); }
 
        .custom-scroll { overflow-y: auto; scrollbar-gutter: stable; }
        .custom-scroll::-webkit-scrollbar { width: 5px; }
        .custom-scroll::-webkit-scrollbar-track { background: transparent; }
        .custom-scroll::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.1); border-radius: 10px; }
        .custom-scroll::-webkit-scrollbar-thumb:hover { background: var(--neon-cyan); }
 
        .loading-overlay {
            position: fixed; inset: 0; background: rgba(2, 6, 23, 0.95);
            z-index: 999; display: none; align-items: center; justify-content: center; flex-direction: column;
        }
 
        .float-anim { animation: subtle-float 5s ease-in-out infinite; }
        @keyframes subtle-float { 0%, 100% { transform: translateY(0px); } 50% { transform: translateY(-15px); } }
 
        @keyframes shine {
            0% { filter: brightness(1) drop-shadow(0 0 5px #fbbf24); transform: scale(1); }
            50% { filter: brightness(1.8) drop-shadow(0 0 25px #fbbf24); transform: scale(1.1); }
            100% { filter: brightness(1) drop-shadow(0 0 5px #fbbf24); transform: scale(1); }
        }
        .shiny-star { animation: shine 2s infinite ease-in-out; }
        
        .log-item { transition: all 0.3s ease; border-left-width: 4px; }
        .log-item:hover { transform: translateX(5px); background: rgba(255,255,255,0.05); }
 
        .center-hub { cursor: pointer; transition: all 0.3s ease; }
        .center-hub:hover { transform: scale(1.05); background: rgba(15, 23, 42, 0.9); border-color: var(--neon-cyan); }
    </style>
</head>
<body class="bg-cyber flex flex-col">
 
    <div id="loading" class="loading-overlay">
        <div class="w-14 h-14 border-4 border-cyan-500 border-t-transparent rounded-full animate-spin mb-4"></div>
        <p class="text-cyan-400 font-bold tracking-widest text-xs uppercase animate-pulse">Menghubungkan ke Pangkalan Data...</p>
    </div>
 
    <div class="dot-grid fixed inset-0 pointer-events-none"></div>
    <img src="https://i.postimg.cc/K8JqhPCn/b57f0c8f43f3dc7b6b0de661b0be3c3a.png" class="silhouette" alt="Silhouette">
 
    <div class="relative z-10 flex flex-col h-full p-2 sm:p-5 space-y-4">
        
        <!-- HEADER -->
        <header class="flex flex-col sm:flex-row items-center justify-between px-3 sm:px-6 py-3 sm:py-0 sm:h-[80px] glass rounded-2xl shrink-0 gap-3 sm:gap-0">
            <div class="flex items-center space-x-3 w-full sm:w-auto justify-center sm:justify-start">
                <img src="https://i.postimg.cc/ZqnQWKv3/Smkatunas-(1)-LOGO.jpg" class="h-10 w-10 sm:h-11 sm:w-11 rounded-lg border border-white/10 shadow-lg shadow-cyan-500/20" alt="Logo">
                <div class="overflow-hidden text-center sm:text-left">
                    <h1 class="text-xl sm:text-2xl font-header font-bold tracking-tighter text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-indigo-400 leading-none uppercase">e-PENCAPAIAN</h1>
                    <p class="text-[9px] sm:text-[10px] text-slate-400 font-bold uppercase tracking-[0.1em] sm:tracking-[0.2em] mt-1 whitespace-nowrap">SMKA Tun Ahmadshah</p>
                </div>
            </div>
            
            <!-- Navigation (Buttons: Dashboard, Senarai, Borang) -->
            <nav class="flex space-x-1 sm:space-x-2 bg-slate-950/40 p-1.5 rounded-xl border border-white/5 shrink-0 w-full sm:w-auto justify-center overflow-x-auto">
                <button onclick="switchView('dashboard')" id="btn-dashboard" class="px-3 sm:px-5 py-2.5 bg-cyan-500/20 rounded-lg transition-all text-cyan-400 font-bold text-[10px] sm:text-xs uppercase whitespace-nowrap flex-1 sm:flex-none">Dashboard</button>
                <button onclick="switchView('list')" id="btn-list" class="px-3 sm:px-5 py-2.5 hover:bg-white/5 rounded-lg transition-all text-slate-400 font-bold text-[10px] sm:text-xs uppercase whitespace-nowrap flex-1 sm:flex-none">Senarai</button>
                <button onclick="switchView('form')" id="btn-form" class="px-3 sm:px-5 py-2.5 hover:bg-white/5 rounded-lg transition-all text-slate-400 font-bold text-[10px] sm:text-xs uppercase whitespace-nowrap flex-1 sm:flex-none">Borang</button>
            </nav>
        </header>
 
        <main class="flex-1 min-h-0 relative">
            
            <!-- VIEW 1: DASHBOARD -->
            <section id="view-dashboard" class="h-full overflow-y-auto custom-scroll pr-1 sm:pr-3 space-y-4">
                <div class="grid grid-cols-12 gap-4">
                    <div class="col-span-12 lg:col-span-3 glass rounded-2xl p-4 sm:p-5 h-[350px] sm:h-[400px] flex flex-col">
                        <h3 class="text-[10px] font-bold text-cyan-400 mb-4 tracking-widest uppercase shrink-0">Top 10 Pelajar Aktif</h3>
                        <div id="top-students-list" class="flex-1 custom-scroll space-y-2 pr-2 text-xs"></div>
                    </div>
 
                    <!-- CENTRAL RADAR HUB -->
                    <div class="col-span-12 lg:col-span-6 glass rounded-2xl h-[350px] sm:h-[400px] relative">
                        <div id="orbit-container" class="relative w-full h-full flex items-center justify-center">
                            <div id="orb-Antarabangsa" onclick="filterByOrb('Antarabangsa')" class="orb bg-cyan-900/40 border border-cyan-400 text-cyan-300" style="left: 42%; top: 5%;">INT</div>
                            <div id="orb-Kebangsaan" onclick="filterByOrb('Kebangsaan')" class="orb bg-blue-900/40 border border-blue-400 text-blue-300" style="right: 15%; top: 25%;">KEB</div>
                            <div id="orb-Negeri" onclick="filterByOrb('Negeri')" class="orb bg-purple-900/40 border border-purple-400 text-purple-300" style="right: 15%; bottom: 25%;">NEG</div>
                            <div id="orb-Zon" onclick="filterByOrb('Zon')" class="orb bg-pink-900/40 border border-pink-400 text-pink-300" style="left: 42%; bottom: 5%;">ZON</div>
                            <div id="orb-Daerah" onclick="filterByOrb('Daerah')" class="orb bg-orange-900/40 border border-orange-400 text-orange-300" style="left: 10%; bottom: 25%;">D</div>
                            <div id="orb-Sekolah" onclick="filterByOrb('Sekolah')" class="orb bg-emerald-900/40 border border-emerald-400 text-emerald-300" style="left: 10%; top: 25%;">SEK</div>
                           
                            <div onclick="filterByOrb('SEMUA')" class="center-hub text-center p-4 sm:p-8 bg-slate-950/70 rounded-full border border-white/10 float-anim shadow-2xl">
                                <p class="text-[7px] sm:text-[8px] font-bold text-slate-500 uppercase tracking-widest mb-1">Status Penapis</p>
                                <p id="current-filter-label" class="text-[10px] sm:text-xs font-black text-cyan-400 uppercase italic">SEMUA REKOD</p>
                            </div>
                        </div>
                    </div>
 
                    <div class="col-span-12 lg:col-span-3 glass rounded-2xl p-4 sm:p-5 h-[350px] sm:h-[400px] flex flex-col">
                        <h3 class="text-[10px] font-bold text-emerald-400 mb-4 tracking-widest uppercase shrink-0">Pencapaian Terkini</h3>
                        <div id="recent-logs" class="flex-1 custom-scroll space-y-3 pr-2 text-xs"></div>
                    </div>
                </div>
 
                <div class="grid grid-cols-12 gap-4 pb-4">
                    <div class="col-span-12 lg:col-span-6 glass rounded-2xl p-4 sm:p-5 h-[300px]">
                        <h3 class="text-[10px] font-bold text-slate-400 mb-2 uppercase tracking-widest">Graf Ringkasan Pencapaian</h3>
                        <div class="h-[220px]"><canvas id="achievementsChart"></canvas></div>
                    </div>
 
                    <div class="col-span-12 lg:col-span-3 glass rounded-2xl p-4 sm:p-5 flex flex-col items-center justify-center text-center h-[250px] sm:h-[300px]">
                        <h3 class="text-[10px] font-bold text-amber-400 mb-4 tracking-widest uppercase shrink-0">Top Performer</h3>
                        <div class="bg-gradient-to-br from-amber-400/20 to-yellow-600/20 p-4 sm:p-6 rounded-full border border-amber-400/40 mb-3 shadow-2xl relative">
                            <svg class="w-8 h-8 sm:w-12 sm:h-12 text-amber-400 shiny-star relative z-10" fill="currentColor" viewBox="0 0 20 20">
                                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"></path>
                            </svg>
                        </div>
                        <p id="tokoh-nama" class="text-sm font-bold uppercase text-white truncate w-full px-2">Memuatkan...</p>
                        <p id="tokoh-merit" class="text-[11px] text-amber-400 font-black mt-1 uppercase">0 Merit</p>
                    </div>
 
                    <div class="col-span-12 lg:col-span-3 glass rounded-2xl p-4 sm:p-5 h-[250px] sm:h-[300px] flex flex-col">
                        <h3 class="text-[10px] font-bold text-purple-400 mb-4 tracking-widest uppercase shrink-0">Guru Paling Aktif</h3>
                        <div id="top-teachers-list" class="flex-1 custom-scroll space-y-2 pr-2 text-xs"></div>
                    </div>
                </div>
            </section>
 
            <!-- VIEW 2: SENARAI PELAJAR -->
            <section id="view-list" class="glass rounded-2xl p-4 sm:p-6 hidden flex flex-col h-full overflow-hidden text-xs">
                <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center mb-6 shrink-0 gap-4">
                    <h2 class="text-lg sm:text-xl font-header font-bold text-cyan-400 uppercase tracking-tighter">Pangkalan Data Pelajar</h2>
                    <div class="flex flex-col sm:flex-row gap-3 w-full sm:w-auto">
                        <input type="text" id="search-input" onkeyup="searchTable()" placeholder="Cari murid..." class="bg-slate-950/50 border border-white/10 rounded-xl px-4 py-3 sm:py-2 text-sm sm:text-xs text-white outline-none focus:border-cyan-400 flex-1 sm:w-64 transition-all order-2 sm:order-1">
                        <button onclick="generatePDFReport()" class="bg-emerald-600 hover:bg-emerald-500 text-white px-4 sm:px-5 py-3 sm:py-2 rounded-xl text-[10px] sm:text-[10px] font-bold uppercase transition-all shadow-lg shrink-0 order-1 sm:order-2 w-full sm:w-auto">Jana PDF</button>
                    </div>
                </div>
                <div class="flex-1 overflow-x-auto overflow-y-auto custom-scroll border border-white/5 rounded-xl">
                    <table class="w-full text-left min-w-[500px] sm:min-w-full" id="dataTable">
                        <thead class="sticky top-0 z-20 bg-[#0f172a]/95 backdrop-blur-md">
                            <tr class="text-[8px] sm:text-[10px] font-bold text-slate-500 uppercase tracking-widest border-b border-white/10">
                                <th class="p-3 sm:p-4">Pelajar</th>
                                <th class="p-3 sm:p-4 hidden sm:table-cell">Program</th>
                                <th class="p-3 sm:p-4">Peringkat</th>
                                <th class="p-3 sm:p-4 text-center">Merit</th>
                                <th class="p-3 sm:p-4 text-right">Aksi</th>
                            </tr>
                        </thead>
                        <tbody id="pangkalan-data-body" class="divide-y divide-white/5"></tbody>
                    </table>
                </div>
            </section>
 
            <!-- VIEW 3: BORANG LAPORAN -->
            <section id="view-form" class="h-full hidden overflow-y-auto custom-scroll p-2 sm:p-4">
                <div class="min-h-full flex items-center justify-center py-6">
                    <div class="glass rounded-3xl p-6 sm:p-10 w-full max-w-2xl my-auto shadow-2xl">
                        <h2 class="text-xl sm:text-2xl font-black mb-6 sm:mb-8 text-cyan-400 uppercase text-center tracking-widest leading-tight">Pendaftaran Aktiviti</h2>
                        <form id="entry-form" class="grid grid-cols-2 gap-4 sm:gap-5 text-xs">
                            <div class="col-span-2 space-y-2">
                                <label class="text-[9px] font-bold text-slate-500 uppercase tracking-widest ml-1">Senarai Murid (Huruf Besar)</label>
                                <div id="student-name-container" class="space-y-3">
                                    <div class="flex space-x-2">
                                        <input type="text" placeholder="NAMA PENUH MURID" class="student-name-input flex-1 bg-slate-950/40 border border-white/10 rounded-xl p-3 sm:p-4 outline-none focus:border-cyan-400 font-bold text-sm sm:text-[11px] uppercase text-white">
                                        <button type="button" onclick="addNameField()" class="bg-cyan-500/10 text-cyan-400 w-12 rounded-xl hover:bg-cyan-500 hover:text-white transition-all font-bold text-xl">+</button>
                                    </div>
                                </div>
                            </div>
                            <div class="col-span-2">
                                <label class="text-[9px] font-bold text-slate-500 uppercase tracking-widest ml-1">Program / Aktiviti</label>
                                <input type="text" id="f_program" required class="w-full bg-slate-950/40 border border-white/10 rounded-xl p-3 sm:p-4 outline-none focus:border-cyan-400 uppercase text-white text-sm sm:text-xs">
                            </div>
                            <div class="col-span-2 sm:col-span-1">
                                <label class="text-[9px] font-bold text-slate-500 uppercase tracking-widest ml-1">Peringkat</label>
                                <select id="f_peringkat" class="w-full bg-slate-900 border border-white/10 rounded-xl p-3 sm:p-4 outline-none focus:border-cyan-400 text-white text-sm sm:text-xs">
                                    <option value="Antarabangsa">Antarabangsa</option>
                                    <option value="Kebangsaan">Kebangsaan</option>
                                    <option value="Negeri">Negeri</option>
                                    <option value="Zon">Zon</option>
                                    <option value="Daerah">Daerah</option>
                                    <option value="Sekolah">Sekolah</option>
                                </select>
                            </div>
                            <div class="col-span-2 sm:col-span-1">
                                <label class="text-[9px] font-bold text-slate-500 uppercase tracking-widest ml-1">Pencapaian</label>
                                <select id="f_pencapaian" class="w-full bg-slate-900 border border-white/10 rounded-xl p-3 sm:p-4 outline-none focus:border-cyan-400 text-white text-sm sm:text-xs">
                                    <option value="Johan">Emas / Johan</option>
                                    <option value="Naib Johan">Perak / Naib Johan</option>
                                    <option value="Ketiga">Gangsa / Ketiga</option>
                                    <option value="Penyertaan">Penyertaan</option>
                                </select>
                            </div>
                            <div class="col-span-2 sm:col-span-1">
                                <label class="text-[9px] font-bold text-slate-500 uppercase tracking-widest ml-1">Tarikh Aktiviti</label>
                                <input type="date" id="f_tarikh" required class="w-full bg-slate-900 border border-white/10 rounded-xl p-3 sm:p-4 outline-none focus:border-cyan-400 text-white text-sm sm:text-xs">
                            </div>
                            <div class="col-span-2 sm:col-span-1">
                                <label class="text-[9px] font-bold text-slate-500 uppercase tracking-widest ml-1">Guru Pengiring</label>
                                <input type="text" id="f_guru" placeholder="NAMA GURU" required class="w-full bg-slate-900 border border-white/10 rounded-xl p-3 sm:p-4 outline-none focus:border-cyan-400 uppercase text-white text-sm sm:text-xs">
                            </div>
                            <div class="col-span-2 pt-6 sm:pt-8">
                                <button type="button" onclick="saveAktiviti()" class="w-full bg-gradient-to-r from-cyan-600 to-indigo-600 hover:from-cyan-500 hover:to-indigo-500 text-white font-black py-4 sm:py-5 rounded-2xl transition-all shadow-xl uppercase tracking-widest">Simpan Data Sistem</button>
                            </div>
                        </form>
                    </div>
                </div>
            </section>
        </main>
    </div>
 
    <script>
        const SCRIPT_URL = "https://script.google.com/macros/s/AKfycbxnPlSUkaMQztd9PJsO4OOGagOpU1MVQpiaDyBroQ-jO2fiSA3bG7HcqdyC-1v-0W4r/exec";
 
        let studentsData = [];
        let currentFilter = 'SEMUA';
        let chartInstance = null;

        function showLoading(isLoading) {
            document.getElementById('loading').style.display = isLoading ? 'flex' : 'none';
        }
 
        async function fetchDataFromGoogle() {
            showLoading(true);
            try {
                const response = await fetch(SCRIPT_URL + "?action=read");
                const result = await response.json();
                studentsData = result.data || [];
                updateUI();
            } catch (error) {
                console.error("Sync Error:", error);
                alert("Gagal menyambung ke Cloud. Sila muat semula.");
            } finally {
                showLoading(false);
            }
        }
 
        async function saveAktiviti() {
            const meritMap = { "Antarabangsa": 17, "Kebangsaan": 14, "Negeri": 11, "Zon": 8, "Daerah": 8, "Sekolah": 5 };
            const program = document.getElementById('f_program').value.toUpperCase();
            const peringkat = document.getElementById('f_peringkat').value;
            const pencapaian = document.getElementById('f_pencapaian').value;
            const tarikh = document.getElementById('f_tarikh').value;
            const guru = document.getElementById('f_guru').value.toUpperCase();
            const inputs = document.querySelectorAll('.student-name-input');
            
            const records = [];
            inputs.forEach(input => {
                const nama = input.value.trim().toUpperCase();
                if (nama && program && tarikh) {
                    records.push({ nama, program, peringkat, pencapaian, merit: meritMap[peringkat], tarikh, guru });
                }
            });
 
            if (records.length === 0) return alert("Sila isi maklumat murid.");
 
            showLoading(true);
            try {
                await fetch(SCRIPT_URL, {
                    method: "POST",
                    mode: "no-cors",
                    headers: { "Content-Type": "application/json" },
                    body: JSON.stringify({ action: "create", data: records })
                });
 
                alert("Data Berhasil Dihantar!");
                document.getElementById('entry-form').reset();
                setTimeout(fetchDataFromGoogle, 2000);
                switchView('dashboard');
            } catch (error) {
                alert("Ralat penghantaran.");
            } finally {
                showLoading(false);
            }
        }
 
        async function deleteRecord(nama, program) {
            if(!confirm(`Padam rekod ${nama} - ${program}?`)) return;
            showLoading(true);
            try {
                await fetch(SCRIPT_URL, {
                    method: "POST",
                    mode: "no-cors",
                    headers: { "Content-Type": "application/json" },
                    body: JSON.stringify({ action: "delete", nama: nama, program: program })
                });
                setTimeout(fetchDataFromGoogle, 2000);
            } catch (error) {
                alert("Gagal memadam.");
                showLoading(false);
            }
        }
 
        async function generatePDFReport() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF('l', 'mm', 'a4');
            doc.text("LAPORAN PENCAPAIAN KOKURIKULUM SMKA TUN AHMADSHAH", 14, 20);
            const rows = studentsData.map(s => [s.nama, s.program, s.peringkat, s.tarikh, s.merit]);
            doc.autoTable({ startY: 30, head: [['Pelajar', 'Program', 'Peringkat', 'Tarikh', 'Merit']], body: rows, theme: 'grid' });
            const pdfBase64 = doc.output('datauristring').split(',')[1];
            if (confirm("Hantar salinan ke Drive?")) {
                showLoading(true);
                try {
                    await fetch(SCRIPT_URL, {
                        method: "POST",
                        mode: "no-cors",
                        body: JSON.stringify({ action: "uploadPDF", file: pdfBase64, filename: `Report_${Date.now()}.pdf` })
                    });
                    doc.save("Laporan_Koku.pdf");
                } catch (e) { console.error(e); } finally { showLoading(false); }
            } else {
                doc.save("Laporan_Koku.pdf");
            }
        }
 
        function updateUI() {
            const filtered = currentFilter === 'SEMUA' ? studentsData : studentsData.filter(d => d.peringkat === currentFilter);
            
            let counts = {}; filtered.forEach(s => counts[s.nama] = (counts[s.nama] || 0) + 1);
            let sortedS = Object.entries(counts).sort((a,b) => b[1]-a[1]).slice(0, 10);
            document.getElementById('top-students-list').innerHTML = sortedS.map(([n, c], i) => `
                <div class="flex items-center space-x-3 p-3 bg-white/10 rounded-xl border border-white/5">
                    <span class="text-cyan-600 font-black">${i+1}</span>
                    <p class="flex-1 font-bold uppercase truncate text-slate-100">${n}</p>
                    <span class="text-cyan-400 font-bold">${c} AKT</span>
                </div>
            `).join('');
 
            let tCounts = {}; filtered.forEach(s => tCounts[s.guru] = (tCounts[s.guru] || 0) + 1);
            let sortedT = Object.entries(tCounts).sort((a,b) => b[1]-a[1]).slice(0, 5);
            document.getElementById('top-teachers-list').innerHTML = sortedT.map(([n, c]) => `
                <div class="p-2.5 border-b border-white/10 flex justify-between text-slate-300"><span>${n}</span><span class="text-purple-400 font-bold">${c} PROG</span></div>
            `).join('');
 
            let merits = {}; studentsData.forEach(s => merits[s.nama] = (merits[s.nama] || 0) + Number(s.merit));
            let tokoh = Object.entries(merits).sort((a,b) => b[1]-a[1])[0];
            if(tokoh) {
                document.getElementById('tokoh-nama').innerText = tokoh[0];
                document.getElementById('tokoh-merit').innerText = tokoh[1] + " MERIT KESELURUHAN";
            } else {
                document.getElementById('tokoh-nama').innerText = "Tiada Rekod";
                document.getElementById('tokoh-merit').innerText = "0 Merit";
            }
 
            const logColors = { "Antarabangsa": "border-amber-500 text-amber-400", "Kebangsaan": "border-blue-500 text-blue-400", "Negeri": "border-purple-500 text-purple-400", "Zon": "border-pink-500 text-pink-400", "Daerah": "border-orange-500 text-orange-400", "Sekolah": "border-emerald-500 text-emerald-400" };
            document.getElementById('recent-logs').innerHTML = filtered.slice(-8).reverse().map(l => `
                <div class="p-3 log-item bg-slate-900/60 rounded-r-xl shadow-lg border-l-4 ${logColors[l.peringkat] || 'border-slate-500 text-slate-400'} mb-2">
                    <div class="flex justify-between items-center mb-1">
                        <span class="text-[8px] font-black uppercase tracking-tighter">${l.peringkat}</span>
                        <span class="text-[8px] opacity-60 font-mono">${l.tarikh}</span>
                    </div>
                    <b class="text-white text-[10px] uppercase block truncate">${l.program}</b>
                    <span class="uppercase text-[9px] block truncate opacity-90 font-bold">${l.nama}</span>
                </div>
            `).join('');
 
            updateChart(filtered);
            renderTable();
        }
 
        function updateChart(data) {
            const stats = { Johan: 0, "Naib Johan": 0, Ketiga: 0, Penyertaan: 0 };
            data.forEach(d => { if(stats[d.pencapaian] !== undefined) stats[d.pencapaian]++; });
            const ctx = document.getElementById('achievementsChart').getContext('2d');
            if (chartInstance) chartInstance.destroy();
            
            const goldGrad = ctx.createLinearGradient(0, 0, 0, 200); goldGrad.addColorStop(0, '#fbbf24'); goldGrad.addColorStop(1, 'rgba(251, 191, 36, 0.05)');
            const silverGrad = ctx.createLinearGradient(0, 0, 0, 200); silverGrad.addColorStop(0, '#94a3b8'); silverGrad.addColorStop(1, 'rgba(148, 163, 184, 0.05)');
            const bronzeGrad = ctx.createLinearGradient(0, 0, 0, 200); bronzeGrad.addColorStop(0, '#b45309'); bronzeGrad.addColorStop(1, 'rgba(180, 83, 9, 0.05)');
            const blueGrad = ctx.createLinearGradient(0, 0, 0, 200); blueGrad.addColorStop(0, '#06b6d4'); blueGrad.addColorStop(1, 'rgba(6, 182, 212, 0.05)');
 
            chartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['EMAS', 'PERAK', 'GANGSA', 'PENY.'],
                    datasets: [{
                        data: [stats.Johan, stats["Naib Johan"], stats.Ketiga, stats.Penyertaan],
                        backgroundColor: [goldGrad, silverGrad, bronzeGrad, blueGrad],
                        borderColor: ['#fbbf24', '#94a3b8', '#b45309', '#06b6d4'],
                        borderWidth: 1,
                        borderRadius: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: { legend: { display: false } },
                    scales: {
                        y: { 
                            beginAtZero: true, 
                            grid: { color: 'rgba(255,255,255,0.05)' }, 
                            ticks: { color: '#94a3b8', stepSize: 1 } 
                        },
                        x: { 
                            grid: { display: false }, 
                            ticks: { color: '#94a3b8', font: { size: 10, weight: 'bold' } } 
                        }
                    }
                }
            });
        }

        function renderTable() {
            const tbody = document.getElementById('pangkalan-data-body');
            const filtered = currentFilter === 'SEMUA' ? studentsData : studentsData.filter(d => d.peringkat === currentFilter);
            
            tbody.innerHTML = filtered.map(d => `
                <tr class="hover:bg-white/5 transition-colors">
                    <td class="p-3 sm:p-4 text-white font-bold uppercase truncate max-w-[150px]">${d.nama}</td>
                    <td class="p-3 sm:p-4 hidden sm:table-cell text-slate-300 uppercase truncate max-w-[200px]" title="${d.program}">${d.program}</td>
                    <td class="p-3 sm:p-4">
                        <span class="bg-cyan-900/40 text-cyan-300 border border-cyan-500/30 px-2 py-1 rounded-md text-[9px] font-bold uppercase">${d.peringkat}</span>
                    </td>
                    <td class="p-3 sm:p-4 text-center font-black text-amber-400">${d.merit}</td>
                    <td class="p-3 sm:p-4 text-right">
                        <button onclick="deleteRecord('${d.nama}', '${d.program}')" class="text-red-400 hover:text-red-300 bg-red-400/10 hover:bg-red-400/20 px-3 py-1.5 rounded-lg transition-all text-[9px] font-bold uppercase tracking-wider">Padam</button>
                    </td>
                </tr>
            `).join('');
        }

        function searchTable() {
            const input = document.getElementById("search-input").value.toUpperCase();
            const tr = document.getElementById("pangkalan-data-body").getElementsByTagName("tr");
            for (let i = 0; i < tr.length; i++) {
                let tdName = tr[i].getElementsByTagName("td")[0];
                let tdProg = tr[i].getElementsByTagName("td")[1];
                if (tdName || tdProg) {
                    let txtValue = (tdName.textContent || tdName.innerText) + " " + (tdProg ? (tdProg.textContent || tdProg.innerText) : "");
                    if (txtValue.toUpperCase().indexOf(input) > -1) {
                        tr[i].style.display = "";
                    } else {
                        tr[i].style.display = "none";
                    }
                }
            }
        }

        function switchView(view) {
            ['dashboard', 'list', 'form'].forEach(v => {
                document.getElementById(`view-${v}`).classList.add('hidden');
                document.getElementById(`btn-${v}`).classList.replace('bg-cyan-500/20', 'hover:bg-white/5');
                document.getElementById(`btn-${v}`).classList.replace('text-cyan-400', 'text-slate-400');
            });
            
            document.getElementById(`view-${view}`).classList.remove('hidden');
            document.getElementById(`btn-${view}`).classList.replace('hover:bg-white/5', 'bg-cyan-500/20');
            document.getElementById(`btn-${view}`).classList.replace('text-slate-400', 'text-cyan-400');

            if(view === 'dashboard' || view === 'list') {
                updateUI();
            }
        }

        function filterByOrb(level) {
            currentFilter = level;
            document.getElementById('current-filter-label').innerText = level === 'SEMUA' ? 'SEMUA REKOD' : level;
            
            document.querySelectorAll('.orb').forEach(el => el.classList.remove('orb-active'));
            if(level !== 'SEMUA' && document.getElementById(`orb-${level}`)) {
                document.getElementById(`orb-${level}`).classList.add('orb-active');
            }
            
            if (typeof gsap !== 'undefined') {
                gsap.fromTo("#current-filter-label", { y: -10, opacity: 0 }, { y: 0, opacity: 1, duration: 0.3 });
            }
            updateUI();
        }

        function addNameField() {
            const container = document.getElementById('student-name-container');
            const div = document.createElement('div');
            div.className = 'flex space-x-2 mt-2';
            div.innerHTML = `
                <input type="text" placeholder="NAMA PENUH MURID" class="student-name-input flex-1 bg-slate-950/40 border border-white/10 rounded-xl p-3 sm:p-4 outline-none focus:border-cyan-400 font-bold text-sm sm:text-[11px] uppercase text-white">
                <button type="button" onclick="this.parentElement.remove()" class="bg-red-500/10 text-red-400 w-12 rounded-xl hover:bg-red-500 hover:text-white transition-all font-bold text-xl">-</button>
            `;
            container.appendChild(div);
        }

        // Init Data Fetching on load
        window.addEventListener('DOMContentLoaded', fetchDataFromGoogle);

    </script>
</body>
</html>
