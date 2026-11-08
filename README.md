<html lang="ms">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>e-PENCAPAIAN - SJK (C) PEI HUA SEREMBAN</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#f0f5fa',
                            100: '#e1ebd6',
                            500: '#1d4ed8',
                            600: '#1e40af',
                            700: '#1d3557',
                            800: '#0f4c81',
                            900: '#0a2540',
                        },
                        flame: {
                            400: '#f87171',
                            500: '#ef4444',
                            600: '#dc2626',
                            700: '#b91c1c'
                        }
                    }
                }
            }
        }
    </script>
    <style>
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 9999px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
        .logo-font {
            font-family: 'Times New Roman', serif;
        }
    </style>
</head>
<body class="bg-slate-50 font-sans text-slate-800 antialiased min-h-screen flex flex-col">

    <!-- Toast Notification Container -->
    <div id="toast-container" class="fixed top-5 right-5 z-50 flex flex-col gap-2 pointer-events-none"></div>

    <!-- HEADER / NAVIGATION -->
    <header class="bg-gradient-to-r from-brand-900 via-brand-800 to-blue-900 text-white shadow-xl sticky top-0 z-40 border-b-2 border-flame-600">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-24">
                
                <!-- Logo & School Crest (Exact Match to SJKC PEI HUA SEREMBAN Logo) -->
                <div class="flex items-center space-x-4">
                    <div class="bg-white rounded-full p-1.5 shadow-lg border-2 border-amber-300 flex-shrink-0 flex items-center justify-center w-16 h-16 sm:w-20 sm:h-20 hover:scale-105 transition-transform duration-300">
                        <!-- Vector Replica of SJK (C) PEI HUA SEREMBAN Emblem -->
                        <svg viewBox="0 0 400 320" class="w-full h-full">
                            <!-- Left Chinese Character 培 -->
                            <text x="15" y="170" font-family="'Kaiti SC', 'SimSun', serif" font-weight="bold" font-size="65" fill="#0f4c81">培</text>
                            
                            <!-- Center Emblem Circle -->
                            <g transform="translate(70, 0)">
                                <!-- Outer Blue Ring -->
                                <circle cx="130" cy="130" r="125" fill="none" stroke="#0f4c81" stroke-width="12" />
                                <circle cx="130" cy="130" r="113" fill="#ffffff" />
                                <circle cx="130" cy="130" r="105" fill="#0f4c81" />
                                
                                <!-- Open Book (White Curves) -->
                                <path d="M 35 155 Q 130 195 130 255 Q 130 195 225 155 Q 130 180 35 155 Z" fill="#ffffff" />
                                <path d="M 45 160 Q 130 198 130 250 Q 130 198 215 160 Q 130 182 45 160 Z" fill="#0f4c81" />
                                <path d="M 55 165 Q 130 200 130 245 Q 130 200 205 165 Z" fill="#ffffff" />

                                <!-- Torch Base -->
                                <path d="M 115 155 C 115 145, 145 145, 145 155 L 138 175 C 138 178, 122 178, 122 175 Z" fill="#ffffff" />
                                
                                <!-- Red Flame -->
                                <path d="M 130 60 C 145 90, 155 105, 145 135 C 140 145, 120 145, 115 135 C 105 110, 120 95, 130 60 Z" fill="#dc2626" />
                                <path d="M 134 75 C 142 95, 148 108, 140 130 C 136 138, 126 138, 124 130 C 118 112, 128 100, 134 75 Z" fill="#ffffff" opacity="0.3" />

                                <!-- Bottom Text Arc: SJK (C) PEI HUA SEREMBAN -->
                                <path id="textArc" d="M 20 155 A 115 115 0 0 0 240 155" fill="none" />
                                <text font-family="Arial, sans-serif" font-weight="900" font-size="16" fill="#0f4c81">
                                    <textPath href="#textArc" startOffset="50%" text-anchor="middle">
                                        SJK (C) PEI HUA SEREMBAN
                                    </textPath>
                                </text>
                            </g>

                            <!-- Right Chinese Character 華 -->
                            <text x="325" y="170" font-family="'Kaiti SC', 'SimSun', serif" font-weight="bold" font-size="65" fill="#0f4c81">華</text>
                        </svg>
                    </div>

                    <div>
                        <div class="flex items-center gap-2">
                            <h1 class="text-xl sm:text-3xl font-extrabold tracking-tight text-white drop-shadow">e-PENCAPAIAN</h1>
                            <span class="bg-flame-600 text-white text-[10px] sm:text-xs font-bold px-2.5 py-0.5 rounded-full uppercase tracking-wider shadow">Sistem Kokurikulum</span>
                        </div>
                        <p class="text-xs sm:text-sm font-semibold text-blue-200 tracking-wide mt-0.5">
                            SJK (C) PEI HUA SEREMBAN <span class="hidden sm:inline text-blue-300 font-normal">|( 芙蓉培华国民型华文小学 )</span>
                        </p>
                    </div>
                </div>

                <!-- Header Actions -->
                <div class="hidden md:flex items-center space-x-5">
                    <div class="text-right">
                        <p class="text-[11px] text-blue-200 uppercase tracking-widest font-bold">Penggal Sesi</p>
                        <p class="text-sm font-extrabold text-amber-300">2026 / 2027</p>
                    </div>
                    <div class="h-8 w-px bg-blue-700"></div>
                    <a href="#pendaftaran" class="bg-flame-600 hover:bg-flame-700 text-white font-bold px-4 py-2.5 rounded-xl shadow-lg hover:shadow-xl transition flex items-center gap-2 text-xs uppercase tracking-wider">
                        <i class="fa-solid fa-plus-circle text-sm"></i>
                        <span>Daftar Aktiviti</span>
                    </a>
                </div>
            </div>
        </div>
    </header>

    <!-- MAIN DASHBOARD CONTENT -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-8">

        <!-- FILTER BAR SECTION -->
        <section class="bg-white rounded-2xl shadow-sm border border-slate-200/80 p-5">
            <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-4">
                <div class="flex items-center space-x-3">
                    <div class="p-3 bg-brand-50 text-brand-800 rounded-xl">
                        <i class="fa-solid fa-filter text-lg"></i>
                    </div>
                    <div>
                        <h2 class="text-xs font-bold text-slate-800 uppercase tracking-wider">Penapis Peringkat Rekod</h2>
                        <p class="text-xs text-slate-500">Pilih peringkat pertandingan untuk menapis paparan statistik dan pencapaian.</p>
                    </div>
                </div>

                <!-- Level Filter Buttons -->
                <div class="flex flex-wrap gap-2" id="filter-container">
                    <button onclick="setFilter('SEMUA')" data-filter="SEMUA" class="filter-btn px-4 py-2 rounded-xl text-xs font-bold transition shadow-sm bg-brand-800 text-white border border-brand-800">
                        SEMUA REKOD
                    </button>
                    <button onclick="setFilter('INT')" data-filter="INT" class="filter-btn px-3.5 py-2 rounded-xl text-xs font-bold transition bg-slate-100 text-slate-700 hover:bg-slate-200 border border-slate-200">
                        INT <span class="text-[10px] font-normal opacity-75">(Antarabangsa)</span>
                    </button>
                    <button onclick="setFilter('KEB')" data-filter="KEB" class="filter-btn px-3.5 py-2 rounded-xl text-xs font-bold transition bg-slate-100 text-slate-700 hover:bg-slate-200 border border-slate-200">
                        KEB <span class="text-[10px] font-normal opacity-75">(Kebangsaan)</span>
                    </button>
                    <button onclick="setFilter('NEG')" data-filter="NEG" class="filter-btn px-3.5 py-2 rounded-xl text-xs font-bold transition bg-slate-100 text-slate-700 hover:bg-slate-200 border border-slate-200">
                        NEG <span class="text-[10px] font-normal opacity-75">(Negeri)</span>
                    </button>
                    <button onclick="setFilter('ZON')" data-filter="ZON" class="filter-btn px-3.5 py-2 rounded-xl text-xs font-bold transition bg-slate-100 text-slate-700 hover:bg-slate-200 border border-slate-200">
                        ZON <span class="text-[10px] font-normal opacity-75">(Zon)</span>
                    </button>
                    <button onclick="setFilter('D')" data-filter="D" class="filter-btn px-3.5 py-2 rounded-xl text-xs font-bold transition bg-slate-100 text-slate-700 hover:bg-slate-200 border border-slate-200">
                        D <span class="text-[10px] font-normal opacity-75">(Daerah)</span>
                    </button>
                    <button onclick="setFilter('SEK')" data-filter="SEK" class="filter-btn px-3.5 py-2 rounded-xl text-xs font-bold transition bg-slate-100 text-slate-700 hover:bg-slate-200 border border-slate-200">
                        SEK <span class="text-[10px] font-normal opacity-75">(Sekolah)</span>
                    </button>
                </div>
            </div>

            <!-- Dynamic Filter Status -->
            <div class="mt-4 pt-3 border-t border-slate-100 flex items-center justify-between text-xs">
                <span class="text-slate-600 font-medium">Status Penapis Semasa: <strong id="filter-status-text" class="text-brand-800 font-bold uppercase">SEMUA REKOD</strong></span>
                <span id="filtered-count-badge" class="bg-blue-50 text-brand-800 px-3 py-1 rounded-full font-extrabold border border-blue-100">0 Rekod Ditemui</span>
            </div>
        </section>

        <!-- DASHBOARD GRID LAYOUT -->
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            
            <!-- LEFT COLUMN: TOP 10 STUDENTS & TEACHERS -->
            <div class="space-y-8 lg:col-span-1">
                
                <!-- TOP 10 PELAJAR AKTIF -->
                <div class="bg-white rounded-2xl shadow-sm border border-slate-200/80 p-6">
                    <div class="flex items-center justify-between pb-4 border-b border-slate-100 mb-4">
                        <div class="flex items-center space-x-3">
                            <div class="p-2.5 bg-amber-50 text-amber-600 rounded-xl">
                                <i class="fa-solid fa-trophy text-lg"></i>
                            </div>
                            <div>
                                <h3 class="font-bold text-slate-800 text-base">Top 10 Pelajar Aktif</h3>
                                <p class="text-xs text-slate-500">Mengikut Pengumpulan Merit</p>
                            </div>
                        </div>
                        <span class="text-[11px] font-extrabold text-amber-600 bg-amber-50 px-2.5 py-1 rounded-lg">MERIT</span>
                    </div>

                    <div id="top-students-list" class="space-y-3 overflow-y-auto max-h-[380px] pr-1">
                        <!-- Dynamic Student Content -->
                    </div>
                </div>

                <!-- GURU PALING AKTIF -->
                <div class="bg-white rounded-2xl shadow-sm border border-slate-200/80 p-6">
                    <div class="flex items-center space-x-3 pb-4 border-b border-slate-100 mb-4">
                        <div class="p-2.5 bg-indigo-50 text-indigo-600 rounded-xl">
                            <i class="fa-solid fa-chalkboard-user text-lg"></i>
                        </div>
                        <div>
                            <h3 class="font-bold text-slate-800 text-base">Guru Paling Aktif</h3>
                            <p class="text-xs text-slate-500">Guru Pembimbing Pertandingan</p>
                        </div>
                    </div>

                    <div id="top-teachers-list" class="space-y-3">
                        <!-- Dynamic Teacher List -->
                    </div>
                </div>

            </div>

            <!-- RIGHT COLUMN: SPOTLIGHT, METRICS & CHARTS -->
            <div class="space-y-8 lg:col-span-2">
                
                <!-- TOP PERFORMER SPOTLIGHT & METRICS -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    
                    <!-- Top Performer Hero Card -->
                    <div class="md:col-span-2 bg-gradient-to-br from-brand-900 via-brand-800 to-blue-900 rounded-2xl shadow-lg p-6 text-white relative overflow-hidden flex flex-col justify-between border border-brand-700">
                        <div class="absolute -right-8 -bottom-8 w-36 h-36 bg-amber-400/10 rounded-full blur-2xl pointer-events-none"></div>
                        <div class="absolute top-4 right-4 text-amber-400 opacity-20 text-7xl font-black">#1</div>
                        
                        <div class="flex items-center space-x-2 text-amber-300 font-semibold text-xs uppercase tracking-wider mb-2">
                            <i class="fa-solid fa-crown text-amber-400"></i>
                            <span>Pelajar Cemerlang SJKC Pei Hua</span>
                        </div>

                        <div class="flex flex-col sm:flex-row items-center gap-5 z-10 my-2">
                            <div class="relative">
                                <img id="top-performer-avatar" src="https://api.dicebear.com/7.x/avataaars/svg?seed=TanWeiMing" alt="Top Performer Avatar" class="w-20 h-20 sm:w-22 sm:h-22 rounded-2xl bg-white p-1 border-2 border-amber-400 shadow-xl object-cover">
                            </div>
                            <div class="text-center sm:text-left space-y-1">
                                <h4 id="top-performer-name" class="text-xl sm:text-2xl font-extrabold text-white">Lim Jia Wei</h4>
                                <p id="top-performer-class" class="text-blue-200 text-xs font-semibold">Tahun 6 Hwa • SJK (C) Pei Hua Seremban</p>
                                <div class="inline-flex items-center gap-2 bg-white/10 backdrop-blur-md px-3 py-1 rounded-xl text-xs font-medium text-amber-300 mt-2">
                                    <i class="fa-solid fa-medal"></i>
                                    <span id="top-performer-achievements-count">Kejayaan Terbanyak Peringkat Tinggi</span>
                                </div>
                            </div>
                        </div>

                        <div class="mt-4 pt-3 border-t border-white/10 flex items-center justify-between text-xs text-blue-100 z-10">
                            <span>Jumlah Merit Terumpul:</span>
                            <span id="top-performer-merit" class="text-xl font-extrabold text-amber-300">0 Merit</span>
                        </div>
                    </div>

                    <!-- Summary Stats Cards -->
                    <div class="space-y-4 flex flex-col justify-between">
                        <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200/80 flex items-center space-x-4">
                            <div class="p-3 bg-blue-50 text-brand-800 rounded-xl">
                                <i class="fa-solid fa-award text-xl"></i>
                            </div>
                            <div>
                                <p class="text-[11px] text-slate-500 font-bold uppercase">Jumlah Kejayaan</p>
                                <p id="stat-total-achievements" class="text-xl font-extrabold text-slate-800">0</p>
                                <p class="text-[10px] text-brand-600 font-medium">Rekod Berdaftar</p>
                            </div>
                        </div>

                        <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200/80 flex items-center space-x-4">
                            <div class="p-3 bg-purple-50 text-purple-600 rounded-xl">
                                <i class="fa-solid fa-users text-xl"></i>
                            </div>
                            <div>
                                <p class="text-[11px] text-slate-500 font-bold uppercase">Pelajar Terlibat</p>
                                <p id="stat-total-students" class="text-xl font-extrabold text-slate-800">0</p>
                                <p class="text-[10px] text-purple-600 font-medium">Penerima Merit</p>
                            </div>
                        </div>

                        <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200/80 flex items-center space-x-4">
                            <div class="p-3 bg-flame-50 text-flame-600 rounded-xl">
                                <i class="fa-solid fa-fire text-xl"></i>
                            </div>
                            <div>
                                <p class="text-[11px] text-slate-500 font-bold uppercase">Purata Merit</p>
                                <p id="stat-avg-merit" class="text-xl font-extrabold text-slate-800">0</p>
                                <p class="text-[10px] text-flame-600 font-medium">Skor Per Aktiviti</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- GRAF RINGKASAN PENCAPAIAN CHART -->
                <div class="bg-white rounded-2xl shadow-sm border border-slate-200/80 p-6">
                    <div class="flex flex-col sm:flex-row sm:items-center justify-between pb-4 border-b border-slate-100 gap-2 mb-4">
                        <div class="flex items-center space-x-3">
                            <div class="p-2.5 bg-blue-50 text-brand-800 rounded-xl">
                                <i class="fa-solid fa-chart-column text-lg"></i>
                            </div>
                            <div>
                                <h3 class="font-bold text-slate-800 text-base">Graf Ringkasan Pencapaian</h3>
                                <p class="text-xs text-slate-500">Agihan Program Mengikut Peringkat Pertandingan</p>
                            </div>
                        </div>
                    </div>

                    <!-- Dynamic Chart Container -->
                    <div class="relative h-64 sm:h-72 w-full">
                        <canvas id="chartCanvas"></canvas>
                    </div>
                </div>

                <!-- PENCAPAIAN TERKINI FEED -->
                <div class="bg-white rounded-2xl shadow-sm border border-slate-200/80 p-6">
                    <div class="flex items-center space-x-3 pb-4 border-b border-slate-100 mb-4">
                        <div class="p-2.5 bg-emerald-50 text-emerald-600 rounded-xl">
                            <i class="fa-solid fa-bolt text-lg"></i>
                        </div>
                        <div>
                            <h3 class="font-bold text-slate-800 text-base">Pencapaian Terkini</h3>
                            <p class="text-xs text-slate-500">Kemas kini langsung penglibatan & kejayaan pelajar SJKC Pei Hua</p>
                        </div>
                    </div>

                    <div id="recent-achievements-feed" class="space-y-3">
                        <!-- Dynamic Feed Loaded Via JS -->
                    </div>
                </div>

            </div>
        </div>

        <!-- SECTION: PANGKALAN DATA PELAJAR (DATABASE TABLE) -->
        <section class="bg-white rounded-2xl shadow-sm border border-slate-200/80 p-6 space-y-6">
            <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 pb-4 border-b border-slate-100">
                <div class="flex items-center space-x-3">
                    <div class="p-2.5 bg-brand-50 text-brand-800 rounded-xl">
                        <i class="fa-solid fa-database text-lg"></i>
                    </div>
                    <div>
                        <h2 class="text-lg font-bold text-slate-800">Pangkalan Data Pelajar</h2>
                        <p class="text-xs text-slate-500">Senarai rekod lengkap pencapaian murid SJK (C) Pei Hua Seremban</p>
                    </div>
                </div>

                <!-- Actions, Search & Filters -->
                <div class="flex flex-wrap items-center gap-3">
                    <button onclick="loadSampleData()" class="px-3 py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 rounded-xl text-xs font-bold transition flex items-center gap-1.5">
                        <i class="fa-solid fa-folder-plus text-brand-800"></i>
                        <span>Muat Contoh Data</span>
                    </button>
                    <button onclick="clearAllDataConfirm()" class="px-3 py-2 bg-red-50 hover:bg-red-100 text-flame-600 rounded-xl text-xs font-bold transition flex items-center gap-1.5 border border-red-200">
                        <i class="fa-solid fa-trash"></i>
                        <span>Kosongkan Semua Data</span>
                    </button>
                    <div class="relative w-full sm:w-52">
                        <i class="fa-solid fa-magnifying-glass absolute left-3 top-1/2 -translate-y-1/2 text-slate-400 text-xs"></i>
                        <input type="text" id="table-search" placeholder="Cari nama, program..." class="w-full pl-9 pr-4 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs focus:outline-none focus:ring-2 focus:ring-brand-800 focus:bg-white transition">
                    </div>
                    <select id="category-filter" onchange="renderTable()" class="w-full sm:w-auto bg-slate-50 border border-slate-200 rounded-xl text-xs font-semibold text-slate-700 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-brand-800">
                        <option value="ALL">Semua Kategori</option>
                        <option value="Akademik">Akademik / STEM</option>
                        <option value="Sukan">Sukan & Permainan</option>
                        <option value="Seni">Seni & Kebudayaan</option>
                        <option value="Ko-Kurikulum">Ko-Kurikulum / Kelab</option>
                    </select>
                </div>
            </div>

            <!-- Responsive Table -->
            <div class="overflow-x-auto rounded-xl border border-slate-100">
                <table class="w-full text-left border-collapse">
                    <thead>
                        <tr class="bg-slate-50 text-slate-500 text-[11px] font-extrabold uppercase tracking-wider border-b border-slate-200">
                            <th class="py-3.5 px-4">Pelajar</th>
                            <th class="py-3.5 px-4">Program / Pertandingan</th>
                            <th class="py-3.5 px-4">Pencapaian</th>
                            <th class="py-3.5 px-4">Peringkat</th>
                            <th class="py-3.5 px-4 text-center">Merit</th>
                            <th class="py-3.5 px-4 text-center">Tarikh</th>
                            <th class="py-3.5 px-4 text-center">Aksi</th>
                        </tr>
                    </thead>
                    <tbody id="student-table-body" class="divide-y divide-slate-100 text-xs font-medium text-slate-700">
                        <!-- Dynamic Rows loaded via JS -->
                    </tbody>
                </table>
            </div>

            <!-- Table Pagination -->
            <div class="flex flex-col sm:flex-row items-center justify-between text-xs text-slate-500 gap-3 pt-2">
                <p id="table-pagination-info">Menunjukkan 0 daripada 0 rekod</p>
                <div class="flex items-center space-x-1">
                    <button onclick="prevPage()" id="btn-prev-page" class="px-3 py-1.5 rounded-lg border border-slate-200 hover:bg-slate-50 font-bold disabled:opacity-50 disabled:cursor-not-allowed">Sebelumnya</button>
                    <span id="page-num-display" class="px-3 py-1 bg-brand-50 text-brand-800 font-extrabold rounded-lg">1</span>
                    <button onclick="nextPage()" id="btn-next-page" class="px-3 py-1.5 rounded-lg border border-slate-200 hover:bg-slate-50 font-bold disabled:opacity-50 disabled:cursor-not-allowed">Seterusnya</button>
                </div>
            </div>
        </section>

        <!-- SECTION: PENDAFTARAN AKTIVITI (REGISTRATION FORM) -->
        <section id="pendaftaran" class="bg-white rounded-2xl shadow-sm border border-slate-200/80 p-6">
            <div class="flex items-center space-x-3 pb-4 border-b border-slate-100 mb-6">
                <div class="p-2.5 bg-flame-50 text-flame-600 rounded-xl">
                    <i class="fa-solid fa-pen-to-square text-lg"></i>
                </div>
                <div>
                    <h2 class="text-lg font-bold text-slate-800">Pendaftaran Aktiviti Baru</h2>
                    <p class="text-xs text-slate-500">Borang pendaftaran rekod pencapaian pelajar SJK (C) Pei Hua Seremban</p>
                </div>
            </div>

            <form id="activity-form" onsubmit="handleFormSubmit(event)" class="space-y-6">
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <!-- Nama Pelajar -->
                    <div class="space-y-1.5">
                        <label class="text-xs font-bold text-slate-700">Nama Pelajar <span class="text-flame-600">*</span></label>
                        <div class="relative">
                            <i class="fa-solid fa-user absolute left-3 top-1/2 -translate-y-1/2 text-slate-400 text-xs"></i>
                            <input type="text" id="form-student" required placeholder="Cth: Tan Wei Ming" class="w-full pl-9 pr-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-xs focus:ring-2 focus:ring-brand-800 focus:bg-white focus:outline-none transition">
                        </div>
                    </div>

                    <!-- Kelas -->
                    <div class="space-y-1.5">
                        <label class="text-xs font-bold text-slate-700">Tahun / Kelas <span class="text-flame-600">*</span></label>
                        <select id="form-class" required class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs font-medium text-slate-700 px-3 py-2.5 focus:ring-2 focus:ring-brand-800 focus:bg-white focus:outline-none transition">
                            <option value="">Pilih Kelas</option>
                            <option value="Tahun 4 Zhong">Tahun 4 Zhong (培)</option>
                            <option value="Tahun 4 Xiao">Tahun 4 Xiao (华)</option>
                            <option value="Tahun 5 Ren">Tahun 5 Ren (仁)</option>
                            <option value="Tahun 5 Ai">Tahun 5 Ai (爱)</option>
                            <option value="Tahun 6 Hwa">Tahun 6 Hwa (华)</option>
                            <option value="Tahun 6 Ping">Tahun 6 Ping (平)</option>
                        </select>
                    </div>

                    <!-- Nama Program -->
                    <div class="space-y-1.5">
                        <label class="text-xs font-bold text-slate-700">Nama Program / Pertandingan <span class="text-flame-600">*</span></label>
                        <div class="relative">
                            <i class="fa-solid fa-trophy absolute left-3 top-1/2 -translate-y-1/2 text-slate-400 text-xs"></i>
                            <input type="text" id="form-program" required placeholder="Cth: Kejohanan Ping Pong MSSNS Negeri Sembilan" class="w-full pl-9 pr-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-xs focus:ring-2 focus:ring-brand-800 focus:bg-white focus:outline-none transition">
                        </div>
                    </div>

                    <!-- Peringkat -->
                    <div class="space-y-1.5">
                        <label class="text-xs font-bold text-slate-700">Peringkat <span class="text-flame-600">*</span></label>
                        <select id="form-level" required class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs font-medium text-slate-700 px-3 py-2.5 focus:ring-2 focus:ring-brand-800 focus:bg-white focus:outline-none transition">
                            <option value="INT">Antarabangsa (INT)</option>
                            <option value="KEB">Kebangsaan (KEB)</option>
                            <option value="NEG">Negeri (NEG)</option>
                            <option value="ZON">Zon (ZON)</option>
                            <option value="D">Daerah (D)</option>
                            <option value="SEK" selected>Sekolah (SEK)</option>
                        </select>
                    </div>

                    <!-- Pencapaian / Kedudukan -->
                    <div class="space-y-1.5">
                        <label class="text-xs font-bold text-slate-700">Pencapaian / Kedudukan <span class="text-flame-600">*</span></label>
                        <select id="form-position" required class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs font-medium text-slate-700 px-3 py-2.5 focus:ring-2 focus:ring-brand-800 focus:bg-white focus:outline-none transition">
                            <option value="Johan (Tempat Pertama)">Johan (Tempat Pertama)</option>
                            <option value="Naib Johan (Tempat Kedua)">Naib Johan (Tempat Kedua)</option>
                            <option value="Ketiga (Tempat Ketiga)">Ketiga (Tempat Ketiga)</option>
                            <option value="Pingat Emas / Tempat Ke-4">Pingat Emas / Tempat Ke-4</option>
                            <option value="Pingat Perak / Tempat Ke-5">Pingat Perak / Tempat Ke-5</option>
                            <option value="Pingat Gangsa / Saguhati">Pingat Gangsa / Saguhati</option>
                            <option value="Penyertaan">Penyertaan Sahaja</option>
                        </select>
                    </div>

                    <!-- Kategori -->
                    <div class="space-y-1.5">
                        <label class="text-xs font-bold text-slate-700">Kategori <span class="text-flame-600">*</span></label>
                        <select id="form-category" required class="w-full bg-slate-50 border border-slate-200 rounded-xl text-xs font-medium text-slate-700 px-3 py-2.5 focus:ring-2 focus:ring-brand-800 focus:bg-white focus:outline-none transition">
                            <option value="Akademik">Akademik / STEM</option>
                            <option value="Sukan">Sukan & Permainan</option>
                            <option value="Seni">Seni & Kebudayaan</option>
                            <option value="Ko-Kurikulum">Ko-Kurikulum / Kelab</option>
                        </select>
                    </div>

                    <!-- Merit Points & Guru -->
                    <div class="grid grid-cols-2 gap-3">
                        <div class="space-y-1.5">
                            <label class="text-xs font-bold text-slate-700">Markah Merit <span class="text-flame-600">*</span></label>
                            <input type="number" id="form-merit" required min="5" max="300" value="50" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-xs font-semibold focus:ring-2 focus:ring-brand-800 focus:bg-white focus:outline-none transition">
                        </div>
                        <div class="space-y-1.5">
                            <label class="text-xs font-bold text-slate-700">Guru Pembimbing</label>
                            <input type="text" id="form-teacher" placeholder="Cth: Cikgu Lee Kah Sheng" class="w-full px-3 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-xs focus:ring-2 focus:ring-brand-800 focus:bg-white focus:outline-none transition">
                        </div>
                    </div>
                </div>

                <!-- Form Submit Action -->
                <div class="flex items-center justify-end space-x-3 pt-4 border-t border-slate-100">
                    <button type="reset" class="px-5 py-2.5 rounded-xl border border-slate-200 text-slate-600 hover:bg-slate-100 text-xs font-bold transition">
                        Reset Borang
                    </button>
                    <button type="submit" class="px-6 py-2.5 bg-brand-800 hover:bg-brand-900 text-white rounded-xl text-xs font-bold shadow-md hover:shadow-lg transition flex items-center space-x-2">
                        <i class="fa-solid fa-paper-plane"></i>
                        <span>Simpan & Kemaskini Pangkalan Data</span>
                    </button>
                </div>
            </form>
        </section>

    </main>

    <!-- FOOTER -->
    <footer class="bg-slate-900 text-slate-400 text-xs py-8 border-t border-slate-800 mt-12">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center space-y-3">
            <div class="flex items-center justify-center space-x-2 text-white font-bold text-sm">
                <span>SJK (C) PEI HUA SEREMBAN</span>
                <span>•</span>
                <span class="text-amber-400">芙蓉培华国民型华文小学</span>
            </div>
            <p>© 2026 SJK (C) Pei Hua Seremban. Portal e-PENCAPAIAN Pengurusan Merit & Rekod Kokurikulum.</p>
        </div>
    </footer>

    <!-- JAVASCRIPT LOGIC -->
    <script>
        // Initial Empty Dataset for SJK (C) PEI HUA SEREMBAN
        let achievementsData = [];

        // Global State
        let currentFilter = 'SEMUA';
        let currentPage = 1;
        const rowsPerPage = 5;
        let chartInstance = null;

        // Badge Styling Mapping
        const levelBadges = {
            'INT': { bg: 'bg-purple-100', text: 'text-purple-700', border: 'border-purple-300', full: 'Antarabangsa' },
            'KEB': { bg: 'bg-red-100', text: 'text-red-700', border: 'border-red-300', full: 'Kebangsaan' },
            'NEG': { bg: 'bg-amber-100', text: 'text-amber-700', border: 'border-amber-300', full: 'Negeri' },
            'ZON': { bg: 'bg-blue-100', text: 'text-blue-700', border: 'border-blue-300', full: 'Zon' },
            'D':   { bg: 'bg-emerald-100', text: 'text-emerald-700', border: 'border-emerald-300', full: 'Daerah' },
            'SEK': { bg: 'bg-slate-100', text: 'text-slate-700', border: 'border-slate-300', full: 'Sekolah' }
        };

        // DOM Loaded Init
        window.addEventListener('DOMContentLoaded', () => {
            initChart();
            refreshDashboard();

            document.getElementById('table-search').addEventListener('input', () => {
                currentPage = 1;
                renderTable();
            });
        });

        // Level Filter Action
        function setFilter(level) {
            currentFilter = level;
            currentPage = 1;

            document.querySelectorAll('#filter-container button').forEach(btn => {
                if (btn.dataset.filter === level) {
                    btn.className = "filter-btn px-4 py-2 rounded-xl text-xs font-bold transition shadow-sm bg-brand-800 text-white border border-brand-800";
                } else {
                    btn.className = "filter-btn px-3.5 py-2 rounded-xl text-xs font-bold transition bg-slate-100 text-slate-700 hover:bg-slate-200 border border-slate-200";
                }
            });

            const statusText = level === 'SEMUA' ? 'SEMUA REKOD' : `PERINGKAT ${levelBadges[level].full.toUpperCase()} (${level})`;
            document.getElementById('filter-status-text').innerText = statusText;

            refreshDashboard();
            showToast(`Menapis mengikut: ${statusText}`);
        }

        function getFilteredData() {
            if (currentFilter === 'SEMUA') return achievementsData;
            return achievementsData.filter(item => item.level === currentFilter);
        }

        function refreshDashboard() {
            const data = getFilteredData();
            document.getElementById('filtered-count-badge').innerText = `${data.length} Rekod Ditemui`;

            renderStats(data);
            renderTopStudents(data);
            renderTopTeachers(data);
            renderTopPerformer(data);
            renderRecentFeed(data);
            renderTable();
            updateChart();
        }

        // Summary Statistics
        function renderStats(data) {
            document.getElementById('stat-total-achievements').innerText = data.length;

            const uniqueStudents = new Set(data.map(d => d.student));
            document.getElementById('stat-total-students').innerText = uniqueStudents.size;

            const totalMerit = data.reduce((acc, curr) => acc + curr.merit, 0);
            const avgMerit = data.length > 0 ? Math.round(totalMerit / data.length) : 0;
            document.getElementById('stat-avg-merit').innerText = avgMerit;
        }

        // Top 10 Active Students Leaderboard
        function renderTopStudents(data) {
            const container = document.getElementById('top-students-list');
            container.innerHTML = '';

            const studentMeritMap = {};
            data.forEach(item => {
                if (!studentMeritMap[item.student]) {
                    studentMeritMap[item.student] = { name: item.student, class: item.class, totalMerit: 0, count: 0 };
                }
                studentMeritMap[item.student].totalMerit += item.merit;
                studentMeritMap[item.student].count += 1;
            });

            const sortedStudents = Object.values(studentMeritMap)
                .sort((a, b) => b.totalMerit - a.totalMerit)
                .slice(0, 10);

            if (sortedStudents.length === 0) {
                container.innerHTML = `
                    <div class="text-center py-8 text-xs text-slate-400">
                        <i class="fa-solid fa-inbox text-2xl text-slate-300 mb-2 block"></i>
                        Pangkalan data kosong. Tiada rekod pelajar aktif.
                    </div>
                `;
                return;
            }

            sortedStudents.forEach((st, idx) => {
                const rankColor = idx === 0 ? 'bg-amber-400 text-brand-900 font-extrabold shadow' : 
                                  idx === 1 ? 'bg-slate-300 text-slate-800 font-bold' : 
                                  idx === 2 ? 'bg-amber-700 text-white font-bold' : 'bg-slate-100 text-slate-600 font-medium';

                const avatarSeed = encodeURIComponent(st.name);

                container.innerHTML += `
                    <div class="flex items-center justify-between p-2 rounded-xl hover:bg-slate-50 transition">
                        <div class="flex items-center space-x-3">
                            <span class="w-6 h-6 rounded-full flex items-center justify-center text-xs ${rankColor}">
                                ${idx + 1}
                            </span>
                            <img src="https://api.dicebear.com/7.x/avataaars/svg?seed=${avatarSeed}" class="w-8 h-8 rounded-full bg-slate-100 border border-slate-200" alt="Avatar">
                            <div>
                                <h4 class="text-xs font-bold text-slate-800">${st.name}</h4>
                                <p class="text-[10px] text-slate-500">${st.class} • ${st.count} Penyertaan</p>
                            </div>
                        </div>
                        <span class="bg-emerald-50 text-emerald-700 font-extrabold text-xs px-2.5 py-1 rounded-lg border border-emerald-100">
                            +${st.totalMerit}
                        </span>
                    </div>
                `;
            });
        }

        // Active Teachers
        function renderTopTeachers(data) {
            const container = document.getElementById('top-teachers-list');
            container.innerHTML = '';

            const teacherMap = {};
            data.forEach(item => {
                const tName = item.teacher || "Guru Pembimbing";
                if (!teacherMap[tName]) teacherMap[tName] = 0;
                teacherMap[tName] += 1;
            });

            const sortedTeachers = Object.entries(teacherMap)
                .map(([name, count]) => ({ name, count }))
                .sort((a, b) => b.count - a.count)
                .slice(0, 4);

            if (sortedTeachers.length === 0) {
                container.innerHTML = `
                    <div class="text-center py-6 text-xs text-slate-400">
                        <i class="fa-solid fa-chalkboard text-xl text-slate-300 mb-1 block"></i>
                        Tiada rekod guru pembimbing.
                    </div>
                `;
                return;
            }

            sortedTeachers.forEach((t) => {
                container.innerHTML += `
                    <div class="flex items-center justify-between p-2.5 bg-slate-50 rounded-xl border border-slate-100">
                        <div class="flex items-center space-x-3">
                            <div class="w-8 h-8 rounded-full bg-blue-100 text-brand-800 flex items-center justify-center text-xs font-bold">
                                <i class="fa-solid fa-user-tie"></i>
                            </div>
                            <div>
                                <p class="text-xs font-bold text-slate-800">${t.name}</p>
                                <p class="text-[10px] text-slate-500">Guru Pembimbing SJKC Pei Hua</p>
                            </div>
                        </div>
                        <span class="bg-blue-50 text-brand-800 font-bold text-[11px] px-2.5 py-0.5 rounded-md border border-blue-100">
                            ${t.count} Program
                        </span>
                    </div>
                `;
            });
        }

        // Top Performer Hero Card
        function renderTopPerformer(data) {
            const studentMap = {};
            achievementsData.forEach(item => {
                if (!studentMap[item.student]) {
                    studentMap[item.student] = { name: item.student, class: item.class, merit: 0, highCount: 0 };
                }
                studentMap[item.student].merit += item.merit;
                if (['INT', 'KEB', 'NEG'].includes(item.level)) {
                    studentMap[item.student].highCount += 1;
                }
            });

            const top = Object.values(studentMap).sort((a, b) => b.merit - a.merit)[0];

            if (top) {
                document.getElementById('top-performer-name').innerText = top.name;
                document.getElementById('top-performer-class').innerText = `${top.class} • SJK (C) Pei Hua Seremban`;
                document.getElementById('top-performer-merit').innerText = `${top.merit} Merit`;
                document.getElementById('top-performer-achievements-count').innerText = `${top.highCount} Kejayaan Utama (INT/KEB/NEG)`;
                document.getElementById('top-performer-avatar').src = `https://api.dicebear.com/7.x/avataaars/svg?seed=${encodeURIComponent(top.name)}`;
            } else {
                document.getElementById('top-performer-name').innerText = "Belum Ada Pelajar";
                document.getElementById('top-performer-class').innerText = "SJK (C) Pei Hua Seremban";
                document.getElementById('top-performer-merit').innerText = "0 Merit";
                document.getElementById('top-performer-achievements-count').innerText = "Daftar rekod baru di bawah";
                document.getElementById('top-performer-avatar').src = `https://api.dicebear.com/7.x/avataaars/svg?seed=PeiHuaUser`;
            }
        }

        // Recent Achievements Activity Feed
        function renderRecentFeed(data) {
            const container = document.getElementById('recent-achievements-feed');
            container.innerHTML = '';

            const recentList = [...data].slice(0, 4);

            if (recentList.length === 0) {
                container.innerHTML = `
                    <div class="text-center py-6 text-xs text-slate-400">
                        <i class="fa-solid fa-clock-rotate-left text-xl text-slate-300 mb-1 block"></i>
                        Tiada aktiviti terkini. Gunakan borang pendaftaran di bawah.
                    </div>
                `;
                return;
            }

            recentList.forEach(item => {
                const badge = levelBadges[item.level] || levelBadges['SEK'];
                container.innerHTML += `
                    <div class="flex items-start justify-between p-3 bg-slate-50 rounded-xl border border-slate-100 hover:border-slate-200 transition">
                        <div class="space-y-1">
                            <div class="flex items-center space-x-2">
                                <span class="font-bold text-xs text-slate-800">${item.student}</span>
                                <span class="text-[10px] text-slate-500">(${item.class})</span>
                            </div>
                            <p class="text-xs font-semibold text-brand-800">${item.program}</p>
                            <p class="text-[10px] font-bold text-amber-600">${item.position || 'Pencapaian'} • Merit: +${item.merit}</p>
                            <p class="text-[10px] text-slate-400">Tarikh: ${item.date} • Guru: ${item.teacher || '-'}</p>
                        </div>
                        <span class="px-2 py-0.5 rounded text-[10px] font-bold border ${badge.bg} ${badge.text} ${badge.border}">
                            ${item.level}
                        </span>
                    </div>
                `;
            });
        }

        // Dynamic Table Render
        function renderTable() {
            const tbody = document.getElementById('student-table-body');
            tbody.innerHTML = '';

            let data = getFilteredData();

            const searchVal = document.getElementById('table-search').value.toLowerCase().trim();
            if (searchVal) {
                data = data.filter(d => 
                    d.student.toLowerCase().includes(searchVal) ||
                    d.program.toLowerCase().includes(searchVal) ||
                    d.class.toLowerCase().includes(searchVal)
                );
            }

            const catVal = document.getElementById('category-filter').value;
            if (catVal !== 'ALL') {
                data = data.filter(d => d.category === catVal);
            }

            const totalRecords = data.length;
            const totalPages = Math.ceil(totalRecords / rowsPerPage) || 1;
            if (currentPage > totalPages) currentPage = totalPages;

            const startIdx = (currentPage - 1) * rowsPerPage;
            const paginatedData = data.slice(startIdx, startIdx + rowsPerPage);

            document.getElementById('table-pagination-info').innerText = `Menunjukkan ${totalRecords === 0 ? 0 : startIdx + 1} hingga ${Math.min(startIdx + rowsPerPage, totalRecords)} daripada ${totalRecords} rekod`;
            document.getElementById('page-num-display').innerText = `${currentPage} / ${totalPages}`;

            document.getElementById('btn-prev-page').disabled = currentPage === 1;
            document.getElementById('btn-next-page').disabled = currentPage === totalPages;

            if (paginatedData.length === 0) {
                tbody.innerHTML = `
                    <tr>
                        <td colspan="7" class="py-12 text-center text-slate-400">
                            <i class="fa-solid fa-folder-open text-3xl text-slate-300 mb-2 block"></i>
                            <span class="font-bold text-slate-600">Pangkalan Data Pelajar Kosong</span>
                            <p class="text-xs text-slate-400 mt-1">Sila isi "Pendaftaran Aktiviti Baru" atau klik "Muat Contoh Data" untuk memulakan.</p>
                        </td>
                    </tr>
                `;
                return;
            }

            paginatedData.forEach(item => {
                const badge = levelBadges[item.level] || levelBadges['SEK'];
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50 transition border-b border-slate-100";
                tr.innerHTML = `
                    <td class="py-3 px-4">
                        <div class="flex items-center space-x-2.5">
                            <img src="https://api.dicebear.com/7.x/avataaars/svg?seed=${encodeURIComponent(item.student)}" class="w-7 h-7 rounded-full bg-slate-100 border border-slate-200" alt="avatar">
                            <div>
                                <span class="font-bold text-slate-800 block">${item.student}</span>
                                <span class="text-[10px] text-slate-500">${item.class}</span>
                            </div>
                        </div>
                    </td>
                    <td class="py-3 px-4">
                        <p class="font-semibold text-slate-800">${item.program}</p>
                        <span class="text-[10px] text-slate-400">${item.category} • Pembimbing: ${item.teacher || '-'}</span>
                    </td>
                    <td class="py-3 px-4">
                        <span class="text-xs font-bold text-slate-700 bg-slate-100 px-2 py-0.5 rounded border border-slate-200">
                            ${item.position || 'Penyertaan'}
                        </span>
                    </td>
                    <td class="py-3 px-4">
                        <span class="px-2.5 py-1 rounded-md text-[11px] font-bold border ${badge.bg} ${badge.text} ${badge.border}">
                            ${item.level}
                        </span>
                    </td>
                    <td class="py-3 px-4 text-center font-extrabold text-emerald-600">
                        +${item.merit}
                    </td>
                    <td class="py-3 px-4 text-center text-[11px] text-slate-500">
                        ${item.date}
                    </td>
                    <td class="py-3 px-4 text-center">
                        <button onclick="deleteRecord(${item.id})" class="text-slate-400 hover:text-flame-600 p-1.5 rounded-lg hover:bg-red-50 transition" title="Padam Rekod">
                            <i class="fa-solid fa-trash-can"></i>
                        </button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function prevPage() {
            if (currentPage > 1) {
                currentPage--;
                renderTable();
            }
        }

        function nextPage() {
            const data = getFilteredData();
            const totalPages = Math.ceil(data.length / rowsPerPage);
            if (currentPage < totalPages) {
                currentPage++;
                renderTable();
            }
        }

        function deleteRecord(id) {
            achievementsData = achievementsData.filter(d => d.id !== id);
            refreshDashboard();
            showToast("Rekod berjaya dipadam daripada pangkalan data.", "danger");
        }

        function clearAllDataConfirm() {
            if (achievementsData.length === 0) {
                showToast("Pangkalan data memang sedia kosong.", "info");
                return;
            }
            if (confirm("Adakah anda pasti mahu mengosongkan SEMUA rekod pangkalan data? Action ini tidak boleh diundurkan.")) {
                achievementsData = [];
                refreshDashboard();
                showToast("Semua data pangkalan data telah dikosongkan.", "danger");
            }
        }

        function loadSampleData() {
            achievementsData = [
                {
                    id: 1,
                    student: "Lim Jia Wei",
                    class: "Tahun 6 Hwa",
                    program: "World International Mathematical Olympiad (WIMO)",
                    level: "INT",
                    position: "Pingat Emas / Tempat Ke-4",
                    category: "Akademik",
                    merit: 150,
                    teacher: "Cikgu Tan Bee Leng",
                    date: "2026-03-12"
                },
                {
                    id: 2,
                    student: "Chong Ming Jun",
                    class: "Tahun 5 Ren",
                    program: "Kejohanan Ping Pong MSSM Kebangsaan",
                    level: "KEB",
                    position: "Johan (Tempat Pertama)",
                    category: "Sukan",
                    merit: 120,
                    teacher: "Encik Lee Kah Sheng",
                    date: "2026-03-18"
                },
                {
                    id: 3,
                    student: "Khoo Zi Ying",
                    class: "Tahun 6 Ping",
                    program: "Pertandingan Tarian Kebudayaan Negeri Sembilan",
                    level: "NEG",
                    position: "Naib Johan (Tempat Kedua)",
                    category: "Seni",
                    merit: 90,
                    teacher: "Puan Lim Mei Ling",
                    date: "2026-02-10"
                }
            ];
            refreshDashboard();
            showToast("Contoh data berjaya dimuatkan ke dalam pangkalan data!", "success");
        }

        // Registration Form Submit Handler
        function handleFormSubmit(e) {
            e.preventDefault();

            const student = document.getElementById('form-student').value.trim();
            const studentClass = document.getElementById('form-class').value;
            const program = document.getElementById('form-program').value.trim();
            const level = document.getElementById('form-level').value;
            const position = document.getElementById('form-position').value;
            const category = document.getElementById('form-category').value;
            const merit = parseInt(document.getElementById('form-merit').value, 10);
            const teacher = document.getElementById('form-teacher').value.trim() || "Cikgu SJKC Pei Hua Seremban";

            const newRecord = {
                id: Date.now(),
                student,
                class: studentClass,
                program,
                level,
                position,
                category,
                merit,
                teacher,
                date: new Date().toISOString().split('T')[0]
            };

            achievementsData.unshift(newRecord);
            document.getElementById('activity-form').reset();
            
            refreshDashboard();
            showToast(`Rekod baru untuk "${student}" telah didaftarkan!`, "success");
        }

        // Chart Initialization
        function initChart() {
            const ctx = document.getElementById('chartCanvas').getContext('2d');
            chartInstance = new Chart(ctx, {
                type: 'bar',
                data: getChartData(),
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: { display: false },
                        tooltip: {
                            backgroundColor: '#0a2540',
                            padding: 12,
                            titleFont: { family: 'Plus Jakarta Sans', size: 13, weight: 'bold' },
                            bodyFont: { family: 'Plus Jakarta Sans', size: 12 },
                            cornerRadius: 8
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: { precision: 0, font: { family: 'Plus Jakarta Sans', size: 11 } },
                            grid: { color: '#f1f5f9' }
                        },
                        x: {
                            ticks: { font: { family: 'Plus Jakarta Sans', size: 11, weight: 'bold' } },
                            grid: { display: false }
                        }
                    }
                }
            });
        }

        function getChartData() {
            const levels = ['INT', 'KEB', 'NEG', 'ZON', 'D', 'SEK'];
            const counts = levels.map(lvl => achievementsData.filter(item => item.level === lvl).length);

            return {
                labels: ['Antarabangsa (INT)', 'Kebangsaan (KEB)', 'Negeri (NEG)', 'Zon (ZON)', 'Daerah (D)', 'Sekolah (SEK)'],
                datasets: [{
                    label: 'Bilangan Kejayaan',
                    data: counts,
                    backgroundColor: [
                        '#8b5cf6',
                        '#dc2626',
                        '#f59e0b',
                        '#1d4ed8',
                        '#10b981',
                        '#64748b'
                    ],
                    borderRadius: 8,
                    borderSkipped: false
                }]
            };
        }

        function updateChart() {
            if (chartInstance) {
                chartInstance.data = getChartData();
                chartInstance.update();
            }
        }

        // Toast Messages
        function showToast(message, type = "info") {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            const bgClass = type === "danger" ? "bg-flame-600" : type === "success" ? "bg-emerald-600" : "bg-brand-900";

            toast.className = `${bgClass} text-white px-4 py-3 rounded-xl shadow-xl text-xs font-semibold flex items-center space-x-2 transition-all transform translate-y-2 opacity-0 pointer-events-auto`;
            toast.innerHTML = `
                <i class="fa-solid ${type === 'danger' ? 'fa-circle-exclamation' : type === 'success' ? 'fa-circle-check' : 'fa-circle-info'} text-sm"></i>
                <span>${message}</span>
            `;

            container.appendChild(toast);
            setTimeout(() => toast.classList.remove('translate-y-2', 'opacity-0'), 10);
            setTimeout(() => {
                toast.classList.add('opacity-0', '-translate-y-2');
                setTimeout(() => toast.remove(), 300);
            }, 3000);
        }
    </script>
</body>
</html>
