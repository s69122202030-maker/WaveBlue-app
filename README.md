<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>WaveBlue Waterpark - Interactive Discrete Math Portal</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Font Inter / Sarabun -->
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Kanit', 'sans-serif'],
                    },
                    colors: {
                        wave: {
                            50: '#f0f9ff',
                            100: '#e0f2fe',
                            200: '#bae6fd',
                            300: '#7dd3fc',
                            400: '#38bdf8',
                            500: '#0284c7',
                            600: '#0369a1',
                            700: '#075985',
                            800: '#0c4a6e',
                            900: '#0a3651',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Kanit', sans-serif;
            background-color: #f8fafc;
        }
        .glass-panel {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(224, 242, 254, 0.6);
        }
        .gradient-text {
            background: linear-gradient(135deg, #0284c7, #06b6d4);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 4px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #38bdf8;
            border-radius: 4px;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col text-slate-800 bg-slate-50">

    <!-- Navigation Header -->
    <header class="sticky top-0 z-50 glass-panel shadow-md border-b border-wave-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <!-- Brand Logo -->
            <div class="flex items-center space-x-3 cursor-pointer" onclick="switchPage('page1')">
                <div class="relative w-12 h-12 flex items-center justify-center bg-gradient-to-tr from-wave-600 to-cyan-400 rounded-2xl shadow-lg text-white">
                    <svg class="w-8 h-8 stroke-current" viewBox="0 0 24 24" fill="none" stroke-width="2">
                        <!-- Node Circles -->
                        <circle cx="5" cy="12" r="2" fill="white"/>
                        <circle cx="12" cy="5" r="2" fill="white"/>
                        <circle cx="19" cy="12" r="2" fill="white"/>
                        <circle cx="12" cy="19" r="2" fill="white"/>
                        <!-- Edges Graph -->
                        <path d="M5 12 Q12 2 19 12 Q12 22 5 12" stroke="white" stroke-width="1.5" fill="none"/>
                        <!-- Wave Line inside -->
                        <path d="M7 12 C9 10, 11 14, 13 12 C15 10, 17 14, 18 12" stroke="#bae6fd" stroke-width="2" stroke-linecap="round"/>
                    </svg>
                </div>
                <div>
                    <div class="text-2xl font-extrabold tracking-wider text-wave-800">WAVE<span class="text-cyan-500">BLUE</span></div>
                    <div class="text-xs text-wave-500 font-medium tracking-tight">WATERPARK & DISCRETE MATH LAB</div>
                </div>
            </div>

            <!-- Desktop Navigation Tabs -->
            <nav class="hidden md:flex items-center space-x-2 bg-wave-50/80 p-1.5 rounded-2xl border border-wave-200">
                <button id="nav-page1" onclick="switchPage('page1')" class="px-4 py-2 rounded-xl text-sm font-semibold transition-all duration-200 text-wave-700 hover:bg-white hover:shadow-sm">
                    <i class="fa-solid fa-water mr-2"></i>หน้าแรก & เครื่องเล่น
                </button>
                <button id="nav-page2" onclick="switchPage('page2')" class="px-4 py-2 rounded-xl text-sm font-semibold transition-all duration-200 text-wave-700 hover:bg-white hover:shadow-sm">
                    <i class="fa-solid fa-ticket mr-2"></i>จองบัตร (Decision Tree)
                </button>
                <button id="nav-page3" onclick="switchPage('page3')" class="px-4 py-2 rounded-xl text-sm font-semibold transition-all duration-200 text-wave-700 hover:bg-white hover:shadow-sm">
                    <i class="fa-solid fa-map-location-dot mr-2"></i>แผนผัง & Graph Path
                </button>
                <button id="nav-page4" onclick="switchPage('page4')" class="px-4 py-2 rounded-xl text-sm font-semibold transition-all duration-200 text-wave-700 hover:bg-white hover:shadow-sm relative">
                    <i class="fa-solid fa-receipt mr-2"></i>คำสั่งซื้อ & สถานะ
                    <span id="cart-badge" class="hidden absolute -top-1 -right-1 bg-rose-500 text-white text-xs w-5 h-5 rounded-full flex items-center justify-center font-bold">0</span>
                </button>
            </nav>

            <!-- Mobile Menu Toggle Button -->
            <button onclick="toggleMobileMenu()" class="md:hidden text-wave-700 text-2xl p-2 focus:outline-none">
                <i class="fa-solid fa-bars"></i>
            </button>
        </div>

        <!-- Mobile Navigation Drawer -->
        <div id="mobile-menu" class="hidden md:hidden bg-white border-b border-wave-200 px-4 pt-2 pb-4 space-y-2">
            <button onclick="switchPage('page1'); toggleMobileMenu()" class="w-full text-left px-4 py-2.5 rounded-xl text-sm font-semibold text-wave-800 hover:bg-wave-50">
                <i class="fa-solid fa-water w-6 text-wave-500"></i>หน้าแรก & เครื่องเล่น
            </button>
            <button onclick="switchPage('page2'); toggleMobileMenu()" class="w-full text-left px-4 py-2.5 rounded-xl text-sm font-semibold text-wave-800 hover:bg-wave-50">
                <i class="fa-solid fa-ticket w-6 text-wave-500"></i>จองบัตร (Decision Tree)
            </button>
            <button onclick="switchPage('page3'); toggleMobileMenu()" class="w-full text-left px-4 py-2.5 rounded-xl text-sm font-semibold text-wave-800 hover:bg-wave-50">
                <i class="fa-solid fa-map-location-dot w-6 text-wave-500"></i>แผนผัง & Graph Path
            </button>
            <button onclick="switchPage('page4'); toggleMobileMenu()" class="w-full text-left px-4 py-2.5 rounded-xl text-sm font-semibold text-wave-800 hover:bg-wave-50">
                <i class="fa-solid fa-receipt w-6 text-wave-500"></i>คำสั่งซื้อ & สถานะ
            </button>
        </div>
    </header>

    <!-- Main Content Area Container -->
    <main class="flex-grow max-w-7xl w-full mx-auto p-4 sm:p-6 lg:p-8">

        <!-- PAGE 1: HOME & ATTRACTIONS -->
        <section id="page1" class="page-content space-y-10">
            <!-- Hero Banner -->
            <div class="relative rounded-3xl overflow-hidden shadow-2xl bg-gradient-to-r from-wave-900 via-wave-700 to-cyan-600 text-white p-8 sm:p-12 lg:p-16">
                <div class="absolute inset-0 opacity-20 bg-[radial-gradient(#fff_1px,transparent_1px)] [background-size:16px_16px]"></div>
                <div class="relative z-10 max-w-2xl space-y-4">
                    <span class="inline-block px-3 py-1 rounded-full bg-cyan-400/20 text-cyan-200 border border-cyan-300/30 text-xs font-semibold tracking-wider">
                        DISCRETE MATHEMATICS IN REAL WORLD
                    </span>
                    <h1 class="text-4xl sm:text-5xl font-black leading-tight">
                        ผจญภัยในสวนน้ำ <br><span class="text-cyan-300">WaveBlue Waterpark</span>
                    </h1>
                    <p class="text-wave-100 text-base sm:text-lg leading-relaxed">
                        สัมผัสความตื่นเต้นของเครื่องเล่นมาตรฐานโลก พร้อมเรียนรู้การประยุกต์ใช้ **Graph Theory, Weighted Graph และ Tree Structures** ในการบริหารจัดการเส้นทางและแพ็กเกจสวนน้ำอย่างมีประสิทธิภาพ
                    </p>
                    <div class="pt-4 flex flex-wrap gap-4">
                        <button onclick="switchPage('page2')" class="px-6 py-3 rounded-2xl bg-cyan-400 hover:bg-cyan-300 text-wave-950 font-bold shadow-lg shadow-cyan-500/30 transition-all">
                            <i class="fa-solid fa-ticket mr-2"></i>ซื้อบัตรเข้าเล่น
                        </button>
                        <button onclick="switchPage('page3')" class="px-6 py-3 rounded-2xl bg-white/10 hover:bg-white/20 text-white font-bold backdrop-blur-md border border-white/20 transition-all">
                            <i class="fa-solid fa-route mr-2"></i>สำรวจแผนผังโซน (Graph)
                        </button>
                    </div>
                </div>
            </div>

            <!-- Attractions Showcase -->
            <div>
                <div class="flex items-center justify-between mb-6">
                    <div>
                        <h2 class="text-2xl font-bold text-wave-900">เครื่องเล่นไฮไลท์ของสวนน้ำ</h2>
                        <p class="text-slate-500 text-sm">โซนเครื่องเล่นจำลอง Vertex หลักในระบบกราฟสวนน้ำ</p>
                    </div>
                    <span class="text-xs bg-wave-100 text-wave-700 font-semibold px-3 py-1 rounded-full">
                        6 Main Zones / Vertices
                    </span>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <!-- Attraction Card 1 -->
                    <div class="bg-white rounded-2xl overflow-hidden shadow-md border border-wave-100 hover:shadow-xl transition duration-300 group">
                        <div class="relative h-48 overflow-hidden">
                            <img src="https://images.unsplash.com/photo-1582650625119-3a31f8fa2699?auto=format&fit=crop&w=800&q=80" alt="Wave Pool" class="w-full h-full object-cover group-hover:scale-105 transition duration-500">
                            <span class="absolute top-3 left-3 bg-wave-800/80 backdrop-blur-md text-white text-xs font-bold px-2.5 py-1 rounded-lg">Vertex B</span>
                        </div>
                        <div class="p-5 space-y-2">
                            <h3 class="text-lg font-bold text-wave-900">Giant Wave Pool (ทะเลจำลอง)</h3>
                            <p class="text-slate-600 text-sm">คลื่นยักษ์จำลองความสูงกว่า 2.5 เมตร ให้คุณสนุกคลายร้อนเหมือนอยู่กลางมหาสมุทร</p>
                            <div class="pt-2 flex items-center justify-between text-xs text-slate-500 font-medium">
                                <span><i class="fa-solid fa-clock text-cyan-500 mr-1"></i>รอคิว ~10 นาที</span>
                                <span class="text-cyan-600 font-bold">ระดับความตื่นเต้น: ปานกลาง</span>
                            </div>
                        </div>
                    </div>

                    <!-- Attraction Card 2 -->
                    <div class="bg-white rounded-2xl overflow-hidden shadow-md border border-wave-100 hover:shadow-xl transition duration-300 group">
                        <div class="relative h-48 overflow-hidden">
                            <img src="https://images.unsplash.com/photo-1519046904884-53103b34b206?auto=format&fit=crop&w=800&q=80" alt="Extreme Slide" class="w-full h-full object-cover group-hover:scale-105 transition duration-500">
                            <span class="absolute top-3 left-3 bg-wave-800/80 backdrop-blur-md text-white text-xs font-bold px-2.5 py-1 rounded-lg">Vertex C</span>
                        </div>
                        <div class="p-5 space-y-2">
                            <h3 class="text-lg font-bold text-wave-900">Extreme Slide Tower (สไลเดอร์ยักษ์)</h3>
                            <p class="text-slate-600 text-sm">ทาวเวอร์สไลเดอร์ความสูง 20 เมตร ท้าทายความเร็วและทิศทางแบบหมุนเกลียว 360 องศา</p>
                            <div class="pt-2 flex items-center justify-between text-xs text-slate-500 font-medium">
                                <span><i class="fa-solid fa-clock text-cyan-500 mr-1"></i>รอคิว ~25 นาที</span>
                                <span class="text-rose-600 font-bold">ระดับความตื่นเต้น: สูงมาก</span>
                            </div>
                        </div>
                    </div>

                    <!-- Attraction Card 3 -->
                    <div class="bg-white rounded-2xl overflow-hidden shadow-md border border-wave-100 hover:shadow-xl transition duration-300 group">
                        <div class="relative h-48 overflow-hidden">
                            <img src="https://images.unsplash.com/photo-1507525428034-b723cf961d3e?auto=format&fit=crop&w=800&q=80" alt="Lazy River" class="w-full h-full object-cover group-hover:scale-105 transition duration-500">
                            <span class="absolute top-3 left-3 bg-wave-800/80 backdrop-blur-md text-white text-xs font-bold px-2.5 py-1 rounded-lg">Vertex D</span>
                        </div>
                        <div class="p-5 space-y-2">
                            <h3 class="text-lg font-bold text-wave-900">Lazy River Wave (สายน้ำไหลชิล)</h3>
                            <p class="text-slate-600 text-sm">ล่องห่วงยางไปตามสายน้ำความยาว 500 เมตร ไหลผ่านถ้ำน้ำตกและสวนเขตร้อน</p>
                            <div class="pt-2 flex items-center justify-between text-xs text-slate-500 font-medium">
                                <span><i class="fa-solid fa-clock text-cyan-500 mr-1"></i>รอคิว ~5 นาที</span>
                                <span class="text-emerald-600 font-bold">ระดับความตื่นเต้น: ผ่อนคลาย</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Theory Connection Concept Card -->
            <div class="bg-white rounded-3xl p-6 sm:p-8 border border-wave-200 shadow-md">
                <h2 class="text-2xl font-bold text-wave-900 mb-4 flex items-center">
                    <i class="fa-solid fa-graduation-cap text-wave-600 mr-3"></i>การประยุกต์ใช้คณิตศาสตร์ดิสครีต (Discrete Mathematics)
                </h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="bg-wave-50/70 p-5 rounded-2xl border border-wave-100">
                        <h3 class="font-bold text-wave-800 mb-2 flex items-center">
                            <i class="fa-solid fa-diagram-project text-cyan-600 mr-2"></i>1. Graph Theory (ทฤษฎีกราฟ)
                        </h3>
                        <p class="text-sm text-slate-600 leading-relaxed">
                            เราแทนจุดสำคัญต่างๆ เช่น ทางเข้า โซนเครื่องเล่น และศูนย์อาหาร เป็น **Vertex (โหนด)** และแทนทางเดินระหว่างโซนเป็น **Edge (เส้นเชื่อม)** โดยระบุ Weight เป็น **ระยะทาง (เมตร)** ทำให้สามารถประมวลผลหาเส้นทางเดินที่สั้นที่สุด (Shortest Path) ด้วย Dijkstra Algorithm หรือใช้ BFS/DFS ในการวางแผนทัวร์สวนน้ำ
                        </p>
                    </div>

                    <div class="bg-cyan-50/70 p-5 rounded-2xl border border-cyan-100">
                        <h3 class="font-bold text-cyan-900 mb-2 flex items-center">
                            <i class="fa-solid fa-sitemap text-cyan-600 mr-2"></i>2. Tree Structure (โครงสร้างต้นไม้)
                        </h3>
                        <p class="text-sm text-slate-600 leading-relaxed">
                            ระบบเลือกแพ็กเกจตั๋วเข้าเล่น ถูกออกแบบในรูปแบบ **Decision Tree** ที่มี **Root** คือ ตัวเลือกสวนน้ำ WaveBlue แตกกิ่งไปยัง **Parent (ประเภทผู้เข้าชม)** และสิ้นสุดที่ **Leaf (บัตรเข้าเล่น & สิทธิพิเศษ)** โดยสามารถท่องโหนดได้ผ่านอัลกอริทึม **Preorder, Postorder และ BFS Tree Traversal**
                        </p>
                    </div>
                </div>
            </div>
        </section>

        <!-- PAGE 2: TICKET BOOKING & DECISION TREE -->
        <section id="page2" class="page-content hidden space-y-8">
            <div class="bg-white rounded-3xl p-6 sm:p-8 border border-wave-200 shadow-sm space-y-6">
                <div>
                    <span class="text-xs font-bold text-cyan-600 bg-cyan-100 px-3 py-1 rounded-full uppercase tracking-wider">Tree Structure Concept</span>
                    <h1 class="text-3xl font-extrabold text-wave-900 mt-2">การจองบัตรด้วย Decision Tree (ต้นไม้ตัดสินใจ)</h1>
                    <p class="text-slate-600 text-sm">เลือกแพ็กเกจบัตรผ่านโครงสร้างลำดับชั้น (Hierarchical Data Model: Root -> Parent -> Child/Leaf)</p>
                </div>

                <!-- Tree Navigation Interactive Widget -->
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                    <!-- Tree Visualizer & Interactive Selection -->
                    <div class="lg:col-span-2 bg-slate-900 text-white p-6 rounded-2xl space-y-6 relative overflow-hidden">
                        <div class="flex items-center justify-between border-b border-slate-700 pb-4">
                            <h2 class="text-lg font-bold text-cyan-400"><i class="fa-solid fa-network-wired mr-2"></i>Decision Tree Navigation</h2>
                            <div class="flex gap-2 text-xs">
                                <button onclick="runTreeTraversal('preorder')" class="px-3 py-1.5 bg-wave-700 hover:bg-wave-600 rounded-lg transition">Preorder</button>
                                <button onclick="runTreeTraversal('postorder')" class="px-3 py-1.5 bg-wave-700 hover:bg-wave-600 rounded-lg transition">Postorder</button>
                                <button onclick="runTreeTraversal('bfs')" class="px-3 py-1.5 bg-cyan-600 hover:bg-cyan-500 rounded-lg transition">BFS Traversal</button>
                            </div>
                        </div>

                        <!-- Visual Tree Canvas / Container -->
                        <div id="tree-container" class="min-h-[320px] flex flex-col justify-between space-y-6 relative">
                            <!-- Level 0: Root -->
                            <div class="flex justify-center">
                                <div id="node-root" class="tree-node border-2 border-cyan-400 bg-cyan-950 px-6 py-2.5 rounded-2xl text-center cursor-pointer hover:scale-105 transition shadow-lg">
                                    <span class="text-xs text-cyan-300 font-semibold block">[Root]</span>
                                    <span class="font-bold text-white">WaveBlue Waterpark</span>
                                </div>
                            </div>

                            <!-- Lines Connectors Level 0 to 1 -->
                            <div class="w-full flex justify-around px-12 opacity-40">
                                <div class="w-0.5 h-6 bg-cyan-400"></div>
                                <div class="w-0.5 h-6 bg-cyan-400"></div>
                                <div class="w-0.5 h-6 bg-cyan-400"></div>
                            </div>

                            <!-- Level 1: Parent Nodes -->
                            <div class="grid grid-cols-3 gap-2 sm:gap-4 text-center">
                                <div id="node-adult" onclick="selectTreeNode('adult')" class="tree-node border border-slate-600 bg-slate-800 p-3 rounded-xl cursor-pointer hover:border-cyan-400 transition">
                                    <span class="text-[10px] text-slate-400 block">[Parent] Level 1</span>
                                    <span class="font-bold text-sm text-cyan-200"><i class="fa-solid fa-user mr-1"></i>ผู้ใหญ่ (Adult)</span>
                                </div>
                                <div id="node-child" onclick="selectTreeNode('child')" class="tree-node border border-slate-600 bg-slate-800 p-3 rounded-xl cursor-pointer hover:border-cyan-400 transition">
                                    <span class="text-[10px] text-slate-400 block">[Parent] Level 1</span>
                                    <span class="font-bold text-sm text-cyan-200"><i class="fa-solid fa-child mr-1"></i>เด็ก (Child)</span>
                                </div>
                                <div id="node-vip" onclick="selectTreeNode('vip')" class="tree-node border border-slate-600 bg-slate-800 p-3 rounded-xl cursor-pointer hover:border-cyan-400 transition">
                                    <span class="text-[10px] text-slate-400 block">[Parent] Level 1</span>
                                    <span class="font-bold text-sm text-cyan-200"><i class="fa-solid fa-crown mr-1"></i>VIP Express</span>
                                </div>
                            </div>

                            <!-- Lines Connectors Level 1 to 2 -->
                            <div class="w-full flex justify-around px-8 opacity-40">
                                <div class="w-0.5 h-6 bg-slate-500"></div>
                                <div class="w-0.5 h-6 bg-slate-500"></div>
                                <div class="w-0.5 h-6 bg-slate-500"></div>
                            </div>

                            <!-- Level 2: Leaf Nodes -->
                            <div class="grid grid-cols-3 gap-2 text-center text-xs">
                                <div id="leaf-adult-pkg" class="tree-node bg-slate-800/80 p-2 rounded-lg border border-slate-700">
                                    <span class="text-[9px] text-amber-400 block">[Leaf] ฿850</span>
                                    <span>Standard Pass</span>
                                </div>
                                <div id="leaf-child-pkg" class="tree-node bg-slate-800/80 p-2 rounded-lg border border-slate-700">
                                    <span class="text-[9px] text-amber-400 block">[Leaf] ฿450</span>
                                    <span>Kid Fun Pass</span>
                                </div>
                                <div id="leaf-vip-pkg" class="tree-node bg-slate-800/80 p-2 rounded-lg border border-slate-700">
                                    <span class="text-[9px] text-amber-400 block">[Leaf] ฿1,500</span>
                                    <span>FastPass Unlimited</span>
                                </div>
                            </div>
                        </div>

                        <!-- Traversal Output Log -->
                        <div class="bg-slate-950 p-3 rounded-xl border border-slate-800 text-xs font-mono">
                            <span class="text-cyan-400 font-bold">Traversal Log: </span>
                            <span id="traversal-output" class="text-slate-300">คลิกปุ่มเลือกแบบสอบ traversal เพื่อดูเส้นทางการท่องโหนด</span>
                        </div>
                    </div>

                    <!-- Booking Form Box -->
                    <div class="bg-wave-50/80 p-6 rounded-2xl border border-wave-200 flex flex-col justify-between space-y-4">
                        <div class="space-y-4">
                            <h2 class="text-xl font-bold text-wave-900 border-b border-wave-200 pb-2">
                                <i class="fa-solid fa-cart-plus text-wave-600 mr-2"></i>จองบัตรเข้าสวนน้ำ
                            </h2>

                            <!-- Selected Path Display -->
                            <div class="bg-white p-3 rounded-xl border border-wave-200 space-y-1">
                                <span class="text-xs text-slate-500 block">Selected Decision Path (โหนด):</span>
                                <div id="selected-tree-path" class="text-sm font-bold text-wave-700 flex items-center">
                                    Root <i class="fa-solid fa-chevron-right text-xs mx-1"></i> Adult <i class="fa-solid fa-chevron-right text-xs mx-1"></i> Standard Pass
                                </div>
                            </div>

                            <!-- Category Selection Form -->
                            <div class="space-y-2">
                                <label class="text-sm font-semibold text-slate-700">เลือกประเภทบัตร (Parent Node):</label>
                                <select id="ticket-type-select" onchange="updateBookingForm()" class="w-full p-3 rounded-xl border border-wave-200 bg-white font-medium focus:ring-2 focus:ring-wave-500 outline-none">
                                    <option value="adult" selected>ผู้ใหญ่ (Standard Pass) - ฿850</option>
                                    <option value="child">เด็ก / สูงไม่เกิน 120 cm (Kid Fun) - ฿450</option>
                                    <option value="vip">VIP FastPass Unlimited - ฿1,500</option>
                                </select>
                            </div>

                            <!-- Quantity Input -->
                            <div class="space-y-2">
                                <label class="text-sm font-semibold text-slate-700">จำนวนบัตร (ใบ):</label>
                                <div class="flex items-center space-x-3">
                                    <button onclick="adjustQty(-1)" class="w-10 h-10 rounded-xl bg-white border border-wave-200 font-bold text-lg hover:bg-wave-100 flex items-center justify-center">-</button>
                                    <input type="number" id="ticket-qty" value="1" min="1" max="20" class="w-20 text-center p-2 rounded-xl border border-wave-200 font-bold bg-white" readonly>
                                    <button onclick="adjustQty(1)" class="w-10 h-10 rounded-xl bg-white border border-wave-200 font-bold text-lg hover:bg-wave-100 flex items-center justify-center">+</button>
                                </div>
                            </div>

                            <!-- Summary Price Calculation -->
                            <div class="bg-white p-4 rounded-xl border border-wave-200 flex justify-between items-center">
                                <span class="font-semibold text-slate-700">ราคารวมทั้งสิ้น:</span>
                                <span id="total-price" class="text-2xl font-black text-cyan-600">฿850</span>
                            </div>
                        </div>

                        <!-- Submit Booking Button -->
                        <button onclick="processBooking()" class="w-full py-3.5 bg-gradient-to-r from-wave-600 to-cyan-500 hover:from-wave-700 hover:to-cyan-600 text-white font-bold rounded-xl shadow-lg shadow-cyan-500/20 transition-all flex items-center justify-center">
                            <i class="fa-solid fa-credit-card mr-2"></i>ยืนยันการจอง / ชำระเงิน
                        </button>
                    </div>
                </div>

                <!-- Tree Theory Terminology Report -->
                <div class="bg-slate-50 p-5 rounded-2xl border border-slate-200">
                    <h3 class="font-bold text-slate-800 text-sm mb-3">สรุปองค์ประกอบโครงสร้าง Tree ในระบบ</h3>
                    <div class="grid grid-cols-2 md:grid-cols-4 gap-4 text-xs">
                        <div class="bg-white p-3 rounded-xl border border-slate-200">
                            <span class="font-bold text-wave-700 block mb-1"> Root Node</span>
                            <p class="text-slate-600">จุดเริ่มต้นของระบบ decision tree คือ "WaveBlue Waterpark"</p>
                        </div>
                        <div class="bg-white p-3 rounded-xl border border-slate-200">
                            <span class="font-bold text-wave-700 block mb-1"> Parent Nodes</span>
                            <p class="text-slate-600">โหนดแบ่งหมวดหมู่ เช่น Adult, Child และ VIP</p>
                        </div>
                        <div class="bg-white p-3 rounded-xl border border-slate-200">
                            <span class="font-bold text-wave-700 block mb-1"> Leaf Nodes</span>
                            <p class="text-slate-600">โหนดปลายทาง (ใบ) คือ แพ็กเกจราคาบัตรแต่ละประเภท</p>
                        </div>
                        <div class="bg-white p-3 rounded-xl border border-slate-200">
                            <span class="font-bold text-wave-700 block mb-1"> Path</span>
                            <p class="text-slate-600">เส้นทางเลือก เช่น Root -> Parent(Adult) -> Leaf(Standard 850)</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- PAGE 3: INTERACTIVE GRAPH & ROUTE FINDER -->
        <section id="page3" class="page-content hidden space-y-8">
            <div class="bg-white rounded-3xl p-6 sm:p-8 border border-wave-200 shadow-sm space-y-6">
                <div>
                    <span class="text-xs font-bold text-cyan-600 bg-cyan-100 px-3 py-1 rounded-full uppercase tracking-wider">Weighted Graph & Pathfinding</span>
                    <h1 class="text-3xl font-extrabold text-wave-900 mt-2">แผนผังโซน & เส้นทางสวนน้ำ (Graph Theory)</h1>
                    <p class="text-slate-600 text-sm">การหาเส้นทางเดินในสวนน้ำด้วย BFS, DFS และ Shortest Path (Dijkstra Algorithm)</p>
                </div>

                <!-- Canvas Visualizer and Graph Controls -->
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                    <!-- Interactive Graph Canvas (2 Columns) -->
                    <div class="lg:col-span-2 space-y-4">
                        <div class="relative bg-slate-900 rounded-2xl overflow-hidden shadow-inner border border-slate-800">
                            <!-- Canvas Header Overlay -->
                            <div class="absolute top-4 left-4 z-10 flex gap-2">
                                <span class="bg-slate-800/90 text-cyan-400 text-xs font-mono px-3 py-1.5 rounded-lg border border-slate-700">
                                    <i class="fa-solid fa-circle-nodes mr-1"></i>Vertices: 6 | Edges: 8
                                </span>
                            </div>

                            <!-- Canvas Element -->
                            <canvas id="graphCanvas" class="w-full h-[420px] block cursor-pointer"></canvas>

                            <!-- Legend Overlay -->
                            <div class="absolute bottom-4 left-4 right-4 z-10 bg-slate-900/90 backdrop-blur-md p-3 rounded-xl border border-slate-800 flex flex-wrap gap-4 text-xs text-slate-300">
                                <div class="flex items-center"><span class="w-3 h-3 rounded-full bg-cyan-400 inline-block mr-1.5"></span> Normal Vertex</div>
                                <div class="flex items-center"><span class="w-3 h-3 rounded-full bg-emerald-400 inline-block mr-1.5"></span> Start (ทางเข้า)</div>
                                <div class="flex items-center"><span class="w-3 h-3 rounded-full bg-rose-500 inline-block mr-1.5"></span> Target / Visited</div>
                                <div class="flex items-center"><span class="w-3.5 h-1 bg-amber-400 inline-block mr-1.5"></span> Shortest Edge Path</div>
                            </div>
                        </div>

                        <!-- Graph Execution Control Panel -->
                        <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
                            <button onclick="runGraphBFS()" class="py-2.5 px-4 bg-wave-600 hover:bg-wave-700 text-white rounded-xl font-bold text-sm shadow transition">
                                <i class="fa-solid fa-wave-square mr-2"></i>Run BFS Traversal
                            </button>
                            <button onclick="runGraphDFS()" class="py-2.5 px-4 bg-indigo-600 hover:bg-indigo-700 text-white rounded-xl font-bold text-sm shadow transition">
                                <i class="fa-solid fa-network-wired mr-2"></i>Run DFS Traversal
                            </button>
                            <button onclick="runDijkstra()" class="py-2.5 px-4 bg-emerald-600 hover:bg-emerald-700 text-white rounded-xl font-bold text-sm shadow transition">
                                <i class="fa-solid fa-route mr-2"></i>Shortest Path (Dijkstra)
                            </button>
                        </div>
                    </div>

                    <!-- Pathfinding Settings & Adjacency List (1 Column) -->
                    <div class="space-y-4 flex flex-col justify-between">
                        <!-- Shortest Path Route Picker -->
                        <div class="bg-wave-50/80 p-5 rounded-2xl border border-wave-200 space-y-4">
                            <h3 class="font-bold text-wave-900 text-sm border-b border-wave-200 pb-2">
                                <i class="fa-solid fa-sliders mr-2 text-wave-600"></i>คำนวณเส้นทางระหว่างโซน
                            </h3>
                            <div class="grid grid-cols-2 gap-3">
                                <div>
                                    <label class="text-xs font-semibold text-slate-600 block mb-1">จุดเริ่มต้น (Start):</label>
                                    <select id="start-node-select" class="w-full p-2 rounded-lg bg-white border border-wave-200 text-xs font-bold">
                                        <option value="A">A: Entrance (ทางเข้า)</option>
                                        <option value="B">B: Wave Pool</option>
                                        <option value="C">C: Extreme Slide</option>
                                        <option value="D">D: Lazy River</option>
                                        <option value="E">E: Kids Zone</option>
                                        <option value="F">F: Food Court</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="text-xs font-semibold text-slate-600 block mb-1">จุดหมาย (Destination):</label>
                                    <select id="end-node-select" class="w-full p-2 rounded-lg bg-white border border-wave-200 text-xs font-bold">
                                        <option value="A">A: Entrance</option>
                                        <option value="B">B: Wave Pool</option>
                                        <option value="C">C: Extreme Slide</option>
                                        <option value="D">D: Lazy River</option>
                                        <option value="E">E: Kids Zone</option>
                                        <option value="F" selected>F: Food Court</option>
                                    </select>
                                </div>
                            </div>

                            <div id="path-result-box" class="bg-white p-3 rounded-xl border border-wave-200 space-y-1">
                                <span class="text-xs font-semibold text-slate-500 block">ผลการคำนวณ Path:</span>
                                <div id="path-result-text" class="text-xs font-bold text-slate-800">กดปุ่ม Shortest Path เพื่อคำนวณ</div>
                                <div id="path-distance-text" class="text-xs text-emerald-600 font-extrabold mt-1"></div>
                            </div>
                        </div>

                        <!-- JavaScript Adjacency List Structure Display -->
                        <div class="bg-slate-900 p-4 rounded-2xl border border-slate-800 text-white space-y-2">
                            <div class="flex justify-between items-center">
                                <span class="text-xs font-bold text-cyan-400 font-mono"><i class="fa-solid fa-code mr-1"></i>Adjacency List Data</span>
                                <span class="text-[10px] text-slate-400">JS Object</span>
                            </div>
                            <pre id="adj-list-code" class="text-[11px] font-mono text-cyan-200 bg-slate-950 p-3 rounded-xl overflow-x-auto max-h-[160px] custom-scrollbar border border-slate-800 leading-relaxed"></pre>
                        </div>
                    </div>
                </div>

                <!-- Detailed Report Graph Theory Requirements -->
                <div class="bg-slate-50 p-6 rounded-2xl border border-slate-200 space-y-4">
                    <h3 class="font-bold text-wave-900 text-base">คำอธิบายโครงสร้าง Graph Theory ในสวนน้ำ WaveBlue</h3>
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4 text-xs">
                        <div class="bg-white p-4 rounded-xl border border-slate-200 space-y-2">
                            <span class="font-bold text-cyan-700 block text-sm"><i class="fa-solid fa-circle mr-1 text-xs"></i>Vertex Meaning (โหนด)</span>
                            <p class="text-slate-600 leading-relaxed">
                                แทนสถานที่หลักและโซนเครื่องเล่นในสวนน้ำ จำนวน 6 จุด (A: Entrance, B: Wave Pool, C: Extreme Slide, D: Lazy River, E: Kids Zone, F: Food Court)
                            </p>
                        </div>
                        <div class="bg-white p-4 rounded-xl border border-slate-200 space-y-2">
                            <span class="font-bold text-cyan-700 block text-sm"><i class="fa-solid fa-arrows-left-right mr-1 text-xs"></i>Edge & Weight (เส้นเชื่อม)</span>
                            <p class="text-slate-600 leading-relaxed">
                                แทนทางเดินเชื่อมระหว่างโซน โดย **Weight (น้ำหนัก)** คือ ระยะทางเดินจริงเป็น **เมตร (Meters)** เช่น Edge(A,B) Weight = 120m
                            </p>
                        </div>
                        <div class="bg-white p-4 rounded-xl border border-slate-200 space-y-2">
                            <span class="font-bold text-cyan-700 block text-sm"><i class="fa-solid fa-route mr-1 text-xs"></i>Path & Applications</span>
                            <p class="text-slate-600 leading-relaxed">
                                **Path** คือ ลำดับโหนดการเดินทางจากจุดเริ่มต้น เช่น A -> B -> C ช่วยให้นักท่องเที่ยวใช้เวลาเดินน้อยที่สุด และช่วยเจ้าหน้าที่วางแผนการสัญจร
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- PAGE 4: ORDERS & PAYMENT STATUS -->
        <section id="page4" class="page-content hidden space-y-8">
            <div class="bg-white rounded-3xl p-6 sm:p-8 border border-wave-200 shadow-sm space-y-6">
                <div class="flex flex-wrap justify-between items-center gap-4 border-b border-wave-100 pb-4">
                    <div>
                        <span class="text-xs font-bold text-cyan-600 bg-cyan-100 px-3 py-1 rounded-full uppercase tracking-wider">Order Management System</span>
                        <h1 class="text-3xl font-extrabold text-wave-900 mt-2">รายการสั่งซื้อ & สถานะการชำระเงิน</h1>
                        <p class="text-slate-600 text-sm">ตรวจสอบตั๋วที่ชำระเงินแล้วและรับ QR Code สำหรับผ่านประตูสวนน้ำ</p>
                    </div>
                    <button onclick="switchPage('page2')" class="px-4 py-2 bg-wave-600 hover:bg-wave-700 text-white font-bold rounded-xl text-sm shadow transition">
                        <i class="fa-solid fa-plus mr-2"></i>จองบัตรเพิ่ม
                    </button>
                </div>

                <!-- Orders Table -->
                <div class="overflow-x-auto rounded-2xl border border-wave-200">
                    <table class="w-full text-left text-sm text-slate-600">
                        <thead class="bg-wave-50 text-wave-900 uppercase text-xs font-bold">
                            <tr>
                                <th class="p-4">รหัสการสั่งซื้อ</th>
                                <th class="p-4">รายการบัตร</th>
                                <th class="p-4">จำนวน</th>
                                <th class="p-4">ราคารวม</th>
                                <th class="p-4">สถานะชำระเงิน</th>
                                <th class="p-4 text-center">QR Pass</th>
                            </tr>
                        </thead>
                        <tbody id="orders-table-body" class="divide-y divide-wave-100 bg-white">
                            <!-- Dynamic Content Inserted Here -->
                        </tbody>
                    </table>
                </div>

                <!-- Pass Ticket Simulation Detail View Modal / Card -->
                <div id="active-pass-card" class="bg-gradient-to-br from-wave-900 via-slate-900 to-cyan-900 text-white p-6 sm:p-8 rounded-3xl shadow-xl relative overflow-hidden hidden">
                    <div class="relative z-10 grid grid-cols-1 md:grid-cols-3 gap-6 items-center">
                        <div class="md:col-span-2 space-y-3">
                            <div class="flex items-center space-x-2">
                                <span class="bg-emerald-500 text-slate-950 font-extrabold text-xs px-3 py-1 rounded-full uppercase">Active Pass</span>
                                <span id="pass-order-id" class="text-xs text-wave-200 font-mono">#WB-88291</span>
                            </div>
                            <h2 id="pass-ticket-name" class="text-2xl font-bold text-white">บัตรผู้ใหญ่ Standard Pass</h2>
                            <p class="text-xs text-wave-100">ใช้เข้าสวนน้ำ WaveBlue Waterpark ได้ทุกโซนพร้อมสิทธิ์ FastPass</p>
                            
                            <!-- Path Recommendation Based on Discrete Graph -->
                            <div class="pt-2 bg-white/10 p-3 rounded-xl border border-white/10 space-y-1">
                                <span class="text-[11px] text-cyan-300 font-semibold block"><i class="fa-solid fa-compass mr-1"></i>แนะนำเส้นทางเดินจาก Graph Theory:</span>
                                <p id="pass-recommended-path" class="text-xs text-slate-200 font-medium">Entrance (A) ➔ Wave Pool (B) ➔ Extreme Slide (C) ➔ Food Court (F)</p>
                            </div>
                        </div>

                        <!-- Barcode / QR Code Simulation -->
                        <div class="flex flex-col items-center justify-center bg-white p-4 rounded-2xl text-slate-900 space-y-2">
                            <!-- Fake QR Code Grid SVG -->
                            <svg class="w-32 h-32" viewBox="0 0 100 100" fill="currentColor">
                                <rect width="100" height="100" fill="white"/>
                                <path d="M0 0h30v30H0zM10 10h10v10H10zM70 0h30v30H70zM80 10h10v10H80zM0 70h30v30H0zM10 80h10v10H10zM40 10h10v10H40zM50 30h20v10H50zM30 50h30v10H30zM70 70h20v20H70z" fill="black"/>
                            </svg>
                            <span class="text-[10px] font-mono text-slate-500 tracking-widest">SCAN AT GATE</span>
                        </div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- Application Footer -->
    <footer class="bg-wave-950 text-wave-200 border-t border-wave-900 mt-12 py-8 px-4">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-center gap-4 text-xs">
            <div class="flex items-center space-x-3">
                <div class="w-8 h-8 rounded-lg bg-cyan-500 flex items-center justify-center text-wave-950 font-bold">WB</div>
                <div>
                    <div class="font-bold text-white text-sm">WaveBlue Waterpark</div>
                    <p class="text-wave-400">Discrete Mathematics Project for Information Technology</p>
                </div>
            </div>
            <div class="text-center md:text-right text-wave-400">
                <p>โครงงานประยุกต์ทฤษฎีกราฟ Graph Theory & Tree Structure</p>
                <p class="mt-1 text-[11px] text-wave-500">© 2026 WaveBlue Inc. All rights reserved.</p>
            </div>
        </div>
    </footer>

    <script>
        /* ==========================================================================
           GLOBAL STATE & DATA STRUCTURES
           ========================================================================== */

        // 1. Graph Data Structure Representation (Adjacency List with Weights)
        const waterparkGraph = {
            'A': [{ node: 'B', weight: 120 }, { node: 'D', weight: 200 }, { node: 'E', weight: 150 }],
            'B': [{ node: 'A', weight: 120 }, { node: 'C', weight: 180 }, { node: 'F', weight: 250 }],
            'C': [{ node: 'B', weight: 180 }, { node: 'F', weight: 100 }],
            'D': [{ node: 'A', weight: 200 }, { node: 'E', weight: 90 }, { node: 'F', weight: 300 }],
            'E': [{ node: 'A', weight: 150 }, { node: 'D', weight: 90 }, { node: 'C', weight: 220 }],
            'F': [{ node: 'B', weight: 250 }, { node: 'C', weight: 100 }, { node: 'D', weight: 300 }]
        };

        // Node Positions for Canvas Rendering
        const nodePositions = {
            'A': { x: 100, y: 210, name: 'Entrance (A)' },
            'B': { x: 260, y: 90,  name: 'Wave Pool (B)' },
            'C': { x: 480, y: 90,  name: 'Extreme Slide (C)' },
            'D': { x: 260, y: 330, name: 'Lazy River (D)' },
            'E': { x: 480, y: 330, name: 'Kids Zone (E)' },
            'F': { x: 620, y: 210, name: 'Food Court (F)' }
        };

        // 2. Decision Tree Structure for Tickets
        const ticketTree = {
            name: 'WaveBlue Waterpark',
            id: 'root',
            children: [
                {
                    name: 'Adult (ผู้ใหญ่)',
                    id: 'adult',
                    children: [{ name: 'Standard Pass', price: 850, id: 'adult-pkg' }]
                },
                {
                    name: 'Child (เด็ก)',
                    id: 'child',
                    children: [{ name: 'Kid Fun Pass', price: 450, id: 'child-pkg' }]
                },
                {
                    name: 'VIP Express',
                    id: 'vip',
                    children: [{ name: 'FastPass Unlimited', price: 1500, id: 'vip-pkg' }]
                }
            ]
        };

        // Sample initial orders in state
        let orderHistory = [
            {
                id: 'WB-94812',
                item: 'บัตรผู้ใหญ่ (Standard Pass)',
                qty: 2,
                total: 1700,
                status: 'ชำระเงินแล้ว (Paid)',
                path: 'Entrance (A) ➔ Wave Pool (B) ➔ Extreme Slide (C) ➔ Food Court (F)'
            }
        ];

        let selectedTreeNodeId = 'adult';
        let highlightedPathEdges = [];
        let visitedNodesAnimation = [];

        /* ==========================================================================
           PAGE NAVIGATION & INITIALIZATION
           ========================================================================== */

        function switchPage(pageId) {
            // Hide all pages
            document.querySelectorAll('.page-content').forEach(p => p.classList.add('hidden'));
            
            // Show selected page
            const target = document.getElementById(pageId);
            if (target) target.classList.remove('hidden');

            // Update Tab styles
            ['page1', 'page2', 'page3', 'page4'].forEach(id => {
                const navBtn = document.getElementById(`nav-${id}`);
                if (navBtn) {
                    if (id === pageId) {
                        navBtn.className = "px-4 py-2 rounded-xl text-sm font-bold bg-white text-wave-800 shadow-sm border border-wave-200";
                    } else {
                        navBtn.className = "px-4 py-2 rounded-xl text-sm font-semibold text-wave-700 hover:bg-white hover:shadow-sm";
                    }
                }
            });

            // Re-render Canvas if Page 3 is active
            if (pageId === 'page3') {
                setTimeout(drawGraphCanvas, 100);
            }

            // Update Orders if Page 4 is active
            if (pageId === 'page4') {
                renderOrdersTable();
            }

            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function toggleMobileMenu() {
            const menu = document.getElementById('mobile-menu');
            menu.classList.toggle('hidden');
        }

        /* ==========================================================================
           PAGE 2: DECISION TREE LOGIC & TRAVERSALS
           ========================================================================== */

        function selectTreeNode(type) {
            selectedTreeNodeId = type;
            document.getElementById('ticket-type-select').value = type;
            updateBookingForm();

            // Highlight node visually
            document.querySelectorAll('.tree-node').forEach(el => {
                el.classList.remove('border-cyan-400', 'bg-cyan-900/50');
            });
            const selectedElem = document.getElementById(`node-${type}`);
            if (selectedElem) {
                selectedElem.classList.add('border-cyan-400', 'bg-cyan-900/50');
            }
        }

        function updateBookingForm() {
            const type = document.getElementById('ticket-type-select').value;
            const qty = parseInt(document.getElementById('ticket-qty').value) || 1;
            const pathElem = document.getElementById('selected-tree-path');
            const priceElem = document.getElementById('total-price');

            let unitPrice = 850;
            let pathText = "";

            if (type === 'adult') {
                unitPrice = 850;
                pathText = `Root ➔ Parent(Adult) ➔ Leaf(Standard Pass ฿850)`;
            } else if (type === 'child') {
                unitPrice = 450;
                pathText = `Root ➔ Parent(Child) ➔ Leaf(Kid Fun Pass ฿450)`;
            } else if (type === 'vip') {
                unitPrice = 1500;
                pathText = `Root ➔ Parent(VIP) ➔ Leaf(FastPass ฿1,500)`;
            }

            const totalPrice = unitPrice * qty;
            pathElem.innerHTML = pathText;
            priceElem.textContent = `฿${totalPrice.toLocaleString()}`;
        }

        function adjustQty(delta) {
            const input = document.getElementById('ticket-qty');
            let current = parseInt(input.value) || 1;
            current = Math.max(1, Math.min(20, current + delta));
            input.value = current;
            updateBookingForm();
        }

        // Tree Traversal Algorithms (Preorder, Postorder, BFS)
        function runTreeTraversal(mode) {
            let result = [];
            
            if (mode === 'preorder') {
                // Root -> Left -> Right
                function preorder(node) {
                    if (!node) return;
                    result.push(node.name);
                    if (node.children) {
                        node.children.forEach(c => preorder(c));
                    }
                }
                preorder(ticketTree);
            } else if (mode === 'postorder') {
                // Children -> Root
                function postorder(node) {
                    if (!node) return;
                    if (node.children) {
                        node.children.forEach(c => postorder(c));
                    }
                    result.push(node.name);
                }
                postorder(ticketTree);
            } else if (mode === 'bfs') {
                // Level-order
                let queue = [ticketTree];
                while (queue.length > 0) {
                    let curr = queue.shift();
                    result.push(curr.name);
                    if (curr.children) {
                        curr.children.forEach(c => queue.push(c));
                    }
                }
            }

            document.getElementById('traversal-output').innerHTML = 
                `<span class="text-amber-400 font-bold">[${mode.toUpperCase()}]</span>: ${result.join(' ➔ ')}`;
        }

        function processBooking() {
            const type = document.getElementById('ticket-type-select').value;
            const qty = parseInt(document.getElementById('ticket-qty').value) || 1;
            
            let name = "บัตรผู้ใหญ่ Standard Pass";
            let price = 850;
            let recPath = "Entrance (A) ➔ Wave Pool (B) ➔ Extreme Slide (C) ➔ Food Court (F)";

            if (type === 'child') {
                name = "บัตรเด็ก Kid Fun Pass";
                price = 450;
                recPath = "Entrance (A) ➔ Kids Zone (E) ➔ Lazy River (D) ➔ Food Court (F)";
            } else if (type === 'vip') {
                name = "บัตร VIP FastPass Unlimited";
                price = 1500;
                recPath = "Entrance (A) ➔ Extreme Slide (C) ➔ Wave Pool (B) ➔ Food Court (F)";
            }

            const newOrder = {
                id: `WB-${Math.floor(10000 + Math.random() * 90000)}`,
                item: name,
                qty: qty,
                total: price * qty,
                status: 'ชำระเงินแล้ว (Paid)',
                path: recPath
            };

            orderHistory.unshift(newOrder);
            updateCartBadge();
            switchPage('page4');
        }

        function updateCartBadge() {
            const badge = document.getElementById('cart-badge');
            if (badge) {
                badge.textContent = orderHistory.length;
                badge.classList.remove('hidden');
            }
        }

        /* ==========================================================================
           PAGE 3: GRAPH THEORY CANVAS & ALGORITHMS (BFS, DFS, DIJKSTRA)
           ========================================================================== */

        function drawGraphCanvas() {
            const canvas = document.getElementById('graphCanvas');
            if (!canvas) return;
            const ctx = canvas.getContext('2d');

            // Handle High-DPI Scaling
            const rect = canvas.getBoundingClientRect();
            canvas.width = rect.width;
            canvas.height = rect.height;

            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Scale coordinates dynamically according to canvas width
            const scaleX = canvas.width / 720;
            const scaleY = canvas.height / 420;

            // Draw Edges (Lines & Weights)
            const drawnEdges = new Set();

            for (let u in waterparkGraph) {
                waterparkGraph[u].forEach(neighbor => {
                    let v = neighbor.weight;
                    let edgeKey = [u, neighbor.node].sort().join('-');

                    if (!drawnEdges.has(edgeKey)) {
                        drawnEdges.add(edgeKey);

                        const p1 = nodePositions[u];
                        const p2 = nodePositions[neighbor.node];

                        const x1 = p1.x * scaleX;
                        const y1 = p1.y * scaleY;
                        const x2 = p2.x * scaleX;
                        const y2 = p2.y * scaleY;

                        // Check if part of highlighted shortest path
                        const isHighlighted = highlightedPathEdges.some(
                            e => (e[0] === u && e[1] === neighbor.node) || (e[0] === neighbor.node && e[1] === u)
                        );

                        // Draw Edge Line
                        ctx.beginPath();
                        ctx.moveTo(x1, y1);
                        ctx.lineTo(x2, y2);
                        ctx.lineWidth = isHighlighted ? 5 : 2;
                        ctx.strokeStyle = isHighlighted ? '#f59e0b' : '#334155';
                        ctx.stroke();

                        // Draw Weight Tag
                        const midX = (x1 + x2) / 2;
                        const midY = (y1 + y2) / 2;

                        ctx.fillStyle = '#1e293b';
                        ctx.beginPath();
                        ctx.arc(midX, midY, 14, 0, 2 * Math.PI);
                        ctx.fill();
                        ctx.strokeStyle = '#475569';
                        ctx.lineWidth = 1;
                        ctx.stroke();

                        ctx.fillStyle = '#38bdf8';
                        ctx.font = 'bold 10px Kanit';
                        ctx.textAlign = 'center';
                        ctx.textBaseline = 'middle';
                        ctx.fillText(`${neighbor.weight}m`, midX, midY);
                    }
                });
            }

            // Draw Vertices (Nodes)
            for (let key in nodePositions) {
                const pos = nodePositions[key];
                const cx = pos.x * scaleX;
                const cy = pos.y * scaleY;

                const isVisited = visitedNodesAnimation.includes(key);
                const isStart = key === 'A';

                ctx.beginPath();
                ctx.arc(cx, cy, 22, 0, 2 * Math.PI);

                if (isVisited) {
                    ctx.fillStyle = '#f43f5e'; // Visited Rose
                } else if (isStart) {
                    ctx.fillStyle = '#10b981'; // Start Emerald
                } else {
                    ctx.fillStyle = '#0284c7'; // Normal Wave Blue
                }
                ctx.fill();

                ctx.lineWidth = 3;
                ctx.strokeStyle = '#ffffff';
                ctx.stroke();

                // Draw Node Label Inner
                ctx.fillStyle = '#ffffff';
                ctx.font = 'bold 14px Kanit';
                ctx.textAlign = 'center';
                ctx.textBaseline = 'middle';
                ctx.fillText(key, cx, cy);

                // Draw Node Label Title
                ctx.fillStyle = '#94a3b8';
                ctx.font = '11px Kanit';
                ctx.fillText(pos.name, cx, cy + 34);
            }
        }

        // BFS Traversal Simulation
        function runGraphBFS() {
            highlightedPathEdges = [];
            visitedNodesAnimation = [];
            let queue = ['A'];
            let visited = new Set(['A']);

            function step() {
                if (queue.length === 0) return;
                let curr = queue.shift();
                visitedNodesAnimation.push(curr);
                drawGraphCanvas();

                waterparkGraph[curr].forEach(neighbor => {
                    if (!visited.has(neighbor.node)) {
                        visited.add(neighbor.node);
                        queue.push(neighbor.node);
                    }
                });

                setTimeout(step, 600);
            }
            step();
        }

        // DFS Traversal Simulation
        function runGraphDFS() {
            highlightedPathEdges = [];
            visitedNodesAnimation = [];
            let visited = new Set();

            function dfs(node) {
                visited.add(node);
                visitedNodesAnimation.push(node);
                waterparkGraph[node].forEach(neighbor => {
                    if (!visited.has(neighbor.node)) {
                        dfs(neighbor.node);
                    }
                });
            }

            dfs('A');
            
            // Animate Visited Step-by-Step
            let fullVisited = [...visitedNodesAnimation];
            visitedNodesAnimation = [];
            let idx = 0;

            let interval = setInterval(() => {
                if (idx >= fullVisited.length) {
                    clearInterval(interval);
                    return;
                }
                visitedNodesAnimation.push(fullVisited[idx]);
                drawGraphCanvas();
                idx++;
            }, 600);
        }

        // Dijkstra's Shortest Path Algorithm
        function runDijkstra() {
            const startNode = document.getElementById('start-node-select').value;
            const endNode = document.getElementById('end-node-select').value;

            let distances = {};
            let previous = {};
            let nodes = new Set();

            for (let node in waterparkGraph) {
                distances[node] = node === startNode ? 0 : Infinity;
                nodes.add(node);
            }

            while (nodes.size > 0) {
                // Get node with smallest distance
                let smallest = Array.from(nodes).reduce((minNode, node) => 
                    distances[node] < distances[minNode] ? node : minNode, Array.from(nodes)[0]);

                if (smallest === endNode || distances[smallest] === Infinity) break;

                nodes.delete(smallest);

                for (let neighbor of waterparkGraph[smallest]) {
                    let alt = distances[smallest] + neighbor.weight;
                    if (alt < distances[neighbor.node]) {
                        distances[neighbor.node] = alt;
                        previous[neighbor.node] = smallest;
                    }
                }
            }

            // Reconstruct Path
            let path = [];
            let curr = endNode;
            while (curr) {
                path.unshift(curr);
                curr = previous[curr];
            }

            // Construct highlighted edges
            highlightedPathEdges = [];
            for (let i = 0; i < path.length - 1; i++) {
                highlightedPathEdges.push([path[i], path[i + 1]]);
            }

            visitedNodesAnimation = [...path];
            drawGraphCanvas();

            // Display Results
            document.getElementById('path-result-text').textContent = path.join(' ➔ ');
            document.getElementById('path-distance-text').textContent = `ระยะทางรวมสั้นที่สุด: ${distances[endNode]} เมตร`;
        }

        /* ==========================================================================
           PAGE 4: ORDERS & PAYMENT RENDER
           ========================================================================== */

        function renderOrdersTable() {
            const tbody = document.getElementById('orders-table-body');
            tbody.innerHTML = '';

            orderHistory.forEach((order, index) => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-wave-50/50 transition cursor-pointer";
                tr.onclick = () => showActivePassCard(order);

                tr.innerHTML = `
                    <td class="p-4 font-mono font-bold text-wave-800">${order.id}</td>
                    <td class="p-4 font-semibold text-slate-800">${order.item}</td>
                    <td class="p-4 text-center font-bold">${order.qty}</td>
                    <td class="p-4 font-bold text-cyan-600">฿${order.total.toLocaleString()}</td>
                    <td class="p-4"><span class="bg-emerald-100 text-emerald-800 text-xs font-extrabold px-2.5 py-1 rounded-full">${order.status}</span></td>
                    <td class="p-4 text-center"><button class="text-wave-600 hover:text-wave-800 font-bold text-xs"><i class="fa-solid fa-qrcode mr-1"></i>แสดง QR</button></td>
                `;
                tbody.appendChild(tr);
            });

            if (orderHistory.length > 0) {
                showActivePassCard(orderHistory[0]);
            }
        }

        function showActivePassCard(order) {
            const card = document.getElementById('active-pass-card');
            card.classList.remove('hidden');

            document.getElementById('pass-order-id').textContent = `#${order.id}`;
            document.getElementById('pass-ticket-name').textContent = order.item;
            document.getElementById('pass-recommended-path').textContent = order.path;
        }

        /* ==========================================================================
           APPLICATION INITIALIZATION ON LOAD
           ========================================================================== */

        window.onload = function () {
            // Render Adjacency List Object in Code Block
            document.getElementById('adj-list-code').textContent = 
                JSON.stringify(waterparkGraph, null, 2);

            // Initialize Booking Form
            updateBookingForm();

            // Default Canvas Render
            drawGraphCanvas();

            // Window Resize Listener for Canvas
            window.addEventListener('resize', drawGraphCanvas);
        };
    </script>
</body>
</html>
