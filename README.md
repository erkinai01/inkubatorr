DOCTYPE html>
<html lang="kk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Инкубатор Мониторингі - Исаханова Еркинай</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap');
        
        body {
            /* Темный көк фон */
            background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
            font-family: 'Inter', sans-serif;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0;
            color: #f1f5f9;
        }

        .glass-card {
            background: rgba(30, 41, 59, 0.7);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        #main-content {
            display: none;
            width: 100%;
            max-width: 1100px;
            animation: fadeIn 0.5s ease-out;
        }

        #login-screen {
            width: 100%;
            max-width: 400px;
            animation: slideUp 0.4s ease-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes slideUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .day-card {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            cursor: pointer;
            background: rgba(255, 255, 255, 0.05);
        }

        .day-card:hover {
            transform: scale(1.02);
            background-color: rgba(59, 130, 246, 0.15);
            border-color: #3b82f6;
        }

        .progress-line {
            position: absolute;
            left: 28px;
            top: 0;
            bottom: 0;
            width: 2px;
            background: #334155;
            z-index: 0;
        }

        /* Modal Styles */
        #modal-overlay {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(8px);
            z-index: 50;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }

        .modal-container {
            max-width: 500px;
            width: 100%;
            background: #1e293b;
            animation: modalPop 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        @keyframes modalPop {
            from { transform: scale(0.9); opacity: 0; }
            to { transform: scale(1); opacity: 1; }
        }

        .custom-scroll::-webkit-scrollbar {
            width: 6px;
        }
        .custom-scroll::-webkit-scrollbar-track {
            background: #0f172a;
        }
        .custom-scroll::-webkit-scrollbar-thumb {
            background: #3b82f6;
            border-radius: 10px;
        }

        input {
            background: rgba(15, 23, 42, 0.6) !important;
            color: white !important;
            border: 1px solid #334155 !important;
        }
    </style>
</head>
<body class="p-4">

    <!-- Login Screen -->
    <div id="login-screen" class="glass-card rounded-3xl p-8 shadow-2xl text-center border-t-8 border-blue-500">
        <div class="mb-6">
            <div class="w-20 h-20 bg-blue-500/20 rounded-full flex items-center justify-center mx-auto mb-4 border border-blue-500/30">
                <i class="fas fa-egg text-blue-400 text-4xl animate-bounce"></i>
            </div>
            <h2 class="text-2xl font-bold text-white">Жүйеге кіру</h2>
            <p class="text-gray-400 text-sm">Инкубаторды бақылау үшін авторлық рұқсат қажет</p>
        </div>
        
        <form id="login-form" class="space-y-4">
            <div class="text-left">
                <label class="block text-xs font-bold text-gray-400 uppercase ml-1 mb-1">Пайдаланушы</label>
                <input type="text" id="username" placeholder="Атыңыз" class="w-full px-4 py-3 rounded-xl outline-none transition focus:ring-2 focus:ring-blue-500" required>
            </div>
            <div class="text-left">
                <label class="block text-xs font-bold text-gray-400 uppercase ml-1 mb-1">Құпия сөз</label>
                <input type="password" id="password" placeholder="••••••••" class="w-full px-4 py-3 rounded-xl outline-none transition focus:ring-2 focus:ring-blue-500" required>
            </div>
            <button type="submit" class="w-full bg-blue-600 hover:bg-blue-500 text-white font-bold py-3 rounded-xl shadow-lg transition transform hover:-translate-y-1">
                Кіру <i class="fas fa-sign-in-alt ml-2"></i>
            </button>
        </form>
        <p class="mt-6 text-[10px] text-gray-500 uppercase tracking-widest">Исаханова Еркинай К. жобасы</p>
    </div>

    <!-- Main Content -->
    <div id="main-content">
        <!-- Header -->
        <div class="glass-card rounded-3xl p-8 mb-8 shadow-2xl flex flex-col md:flex-row justify-between items-center border-b-4 border-blue-600">
            <div>
                <h1 class="text-4xl font-extrabold text-white tracking-tight">
                    <i class="fas fa-egg text-yellow-400 mr-2"></i>Smart Incubator
                </h1>
                <p class="text-blue-400 font-medium mt-1 uppercase text-xs tracking-wider">Даму деңгейін бақылау панели</p>
            </div>
            <div class="mt-6 md:mt-0 text-right">
                <div class="text-xs text-gray-400 italic">Жоба авторы:</div>
                <div class="text-xl font-bold text-blue-100 uppercase">Исаханова Еркинай</div>
                <button onclick="logout()" class="text-xs text-red-400 font-bold mt-2 hover:text-red-300">Шығу <i class="fas fa-power-off ml-1"></i></button>
            </div>
        </div>

        <!-- Dashboard Stats -->
        <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-8">
            <div class="glass-card p-6 rounded-2xl shadow-lg border-l-4 border-orange-500">
                <span class="text-gray-400 font-semibold block mb-1 text-sm uppercase">Ағымдағы күн</span>
                <div class="text-3xl font-bold text-white" id="stat-day">1/21</div>
            </div>
            <div class="glass-card p-6 rounded-2xl shadow-lg border-l-4 border-red-500">
                <span class="text-gray-400 font-semibold block mb-1 text-sm uppercase">Температура</span>
                <div class="text-3xl font-bold text-white">37.8°C</div>
            </div>
            <div class="glass-card p-6 rounded-2xl shadow-lg border-l-4 border-blue-500">
                <span class="text-gray-400 font-semibold block mb-1 text-sm uppercase">Ылғалдылық</span>
                <div class="text-3xl font-bold text-white">55%</div>
            </div>
            <div class="glass-card p-6 rounded-2xl shadow-lg border-l-4 border-green-500">
                <span class="text-gray-400 font-semibold block mb-1 text-sm uppercase">Жағдайы</span>
                <div class="text-3xl font-bold text-green-400">Қалыпты</div>
            </div>
        </div>

        <!-- Timeline -->
        <div class="glass-card rounded-3xl shadow-2xl overflow-hidden mb-10">
            <div class="p-6 border-b border-white/5 bg-white/5">
                <h2 class="text-2xl font-bold text-white">Даму хронологиясы</h2>
                <p class="text-sm text-gray-400 mt-1">Күннің үстінен басып, толық мәлімет алыңыз</p>
            </div>
            <div class="p-6 custom-scroll overflow-y-auto max-h-[600px] relative">
                <div class="progress-line"></div>
                <div id="timeline-container" class="space-y-6"></div>
            </div>
        </div>
    </div>

    <!-- Modal for Day Details -->
    <div id="modal-overlay" onclick="closeModal()">
        <div class="modal-container rounded-3xl overflow-hidden shadow-2xl" onclick="event.stopPropagation()">
            <div id="modal-header" class="bg-blue-700 p-6 text-white flex justify-between items-center">
                <h3 class="text-2xl font-bold" id="modal-title">Күн мәліметі</h3>
                <button onclick="closeModal()" class="text-white hover:text-gray-300 text-3xl font-light">&times;</button>
            </div>
            <div class="p-8">
                <div class="w-32 h-32 bg-slate-900 rounded-full flex items-center justify-center mx-auto mb-6 border-4 border-blue-500/30">
                    <i id="modal-icon" class="fas fa-egg text-blue-400 text-5xl"></i>
                </div>
                <div class="text-center mb-6">
                    <span id="modal-day-badge" class="bg-blue-500/20 text-blue-400 text-xs font-bold px-3 py-1 rounded-full border border-blue-500/30 uppercase">1-күн</span>
                    <h4 id="modal-subtitle" class="text-xl font-bold text-white mt-2">Даму сатысы</h4>
                </div>
                <div class="space-y-4 text-left">
                    <div class="bg-slate-800/50 p-5 rounded-2xl border border-white/5">
                        <p id="modal-description" class="text-gray-300 leading-relaxed italic text-sm"></p>
                    </div>
                    <div class="grid grid-cols-2 gap-4 text-sm">
                        <div class="p-4 bg-blue-900/30 rounded-xl border border-blue-500/20">
                            <span class="block text-blue-400 font-bold uppercase text-[10px] mb-1">Кеңес</span>
                            <span id="modal-tip" class="text-blue-100 text-xs"></span>
                        </div>
                        <div class="p-4 bg-green-900/30 rounded-xl border border-green-500/20">
                            <span class="block text-green-400 font-bold uppercase text-[10px] mb-1">Статус</span>
                            <span class="text-green-100 text-xs">Тұрақты даму</span>
                        </div>
                    </div>
                </div>
                <button onclick="closeModal()" class="w-full mt-8 bg-blue-600 text-white font-bold py-3 rounded-xl hover:bg-blue-500 transition shadow-lg">Түсінікті</button>
            </div>
        </div>
    </div>

    <script>
        const developmentStages = [
            { day: 1, icon: "fa-seedling", title: "Бастапқы кезең", desc: "Ұрықтану процесі басталады. Алғашқы жасушалар бөлінеді. Жұмыртқа ішінде өмір нышандары пайда бола бастаған сәт.", tip: "Ылғалдылықты 55% деңгейінде ұстаңыз." },
            { day: 2, icon: "fa-microscope", title: "Қан тамырлары", desc: "Жұмыртқа сарыуызында қан тамырларының алғашқы торы (area vasculosa) пайда болады.", tip: "Температура 37.8°C болуы шарт." },
            { day: 3, icon: "fa-heartbeat", title: "Жүрек соғысы", desc: "Жүрек соға бастайды. Аяқ пен қанаттың негізі қаланады. Эмбрион айнала бастайды.", tip: "Жұмыртқаны күніне 4-6 рет аударыңыз." },
            { day: 4, icon: "fa-eye", title: "Көздің дамуы", desc: "Көздің пигментациясы басталып, анық көрінетін қара нүкте пайда болады. Ми бөліктері бөлінеді.", tip: "Желдету жүйесін тексеріңіз." },
            { day: 5, icon: "fa-shapes", title: "Эмбрион пішіні", desc: "Эмбрион C-тәрізді иіледі, буындар мен саусақтардың негізі қаланады.", tip: "Су деңгейін тексеруді ұмытпаңыз." },
            { day: 6, icon: "fa-crow", title: "Тұмсық бастамасы", desc: "Тұмсықтың алғашқы белгілері мен ерікті қозғалыс элементтері көрінеді.", tip: "Инкубаторды артық ашпаңыз." },
            { day: 7, icon: "fa-feather-alt", title: "Қауырсын негізі", desc: "Тұмсық қатая бастайды, денесінде қауырсын фолликулалары пайда болады.", tip: "Ауа алмасуын қадағалаңыз." },
            { day: 8, icon: "fa-ear-listen", title: "Есту мүшесі", desc: "Құлақ тесіктері пайда болып, сыртқы дыбыстарға сезімталдық артады.", tip: "Жарықпен тексеруге болады (овоскопия)." },
            { day: 9, icon: "fa-fingerprint", title: "Тырнақтар", desc: "Аяқ саусақтарында тырнақтардың дамуы басталады. Балапан белсенді қозғалады.", tip: "Температура тұрақтылығы маңызды." },
            { day: 10, icon: "fa-running", title: "Белсенді қозғалыс", desc: "Эмбрионның қозғалысы күшейеді, тұмсық толық қалыптасады. Сарыуыз азаяды.", tip: "Инкубаторды таза ұстаңыз." },
            { day: 11, icon: "fa-feather", title: "Қауырсын жамылғысы", desc: "Алғашқы мамықтар көріне бастайды, денесі мамықпен жабыла бастайды.", tip: "Аударған кезде абай болыңыз." },
            { day: 12, icon: "fa-expand-arrows-alt", title: "Жылдам өсу", desc: "Эмбрион мөлшері күрт өседі, сүйектері қатая бастайды.", tip: "Желдетуді сәл арттыруға болады." },
            { day: 13, icon: "fa-shield-alt", title: "Қорғаныс", desc: "Тырнақтар мен қабыршақтар мүйізденіп, қорғаныс қабаты нығаяды.", tip: "Ылғалдылықты тексеріңіз." },
            { day: 14, icon: "fa-sync", title: "Бағытты өзгерту", desc: "Балапан басын жұмыртқаның доғал ұшына (ауа камерасына) қарай бұрады.", tip: "Балапанның орналасуы маңызды кезең." },
            { day: 15, icon: "fa-vial", title: "Ағзалардың пісуі", desc: "Барлық ішкі мүшелер толық қалыптасып, өз қызметін бастайды.", tip: "Тыныштық сақтаңыз." },
            { day: 16, icon: "fa-drumstick-bite", title: "Белокты игеру", desc: "Ақуыз (белок) толығымен эмбрионның қорегі ретінде жұмсалып бітеді.", tip: "Энергия жинақтау кезеңі." },
            { day: 17, icon: "fa-compress-alt", title: "Тығыз кеңістік", desc: "Балапан жұмыртқа ішін толық толтырады, қозғалыс шектеледі.", tip: "Аударуды жалғастырыңыз." },
            { day: 18, icon: "fa-wind", title: "Тыныс алуға дайындық", desc: "Өсу тоқтап, балапан сыртқы тыныс алуға дайындала бастайды.", tip: "Соңғы рет аудару күні (кешке тоқтатыңыз)." },
            { day: 19, icon: "fa-battery-half", title: "Энергия жинақтау", desc: "Сарыуыз қапшығы балапанның ішкі қуысына тартыла бастайды. Аудару тоқтатылады.", tip: "Ылғалдылықты 70%-ға дейін көтеріңіз." },
            { day: 20, icon: "fa-bullhorn", title: "Алғашқы дыбыс", desc: "Сарыуыз толық тартылды. Балапан тұмсығымен ауа камерасын теседі. Шиқыл естілуі мүмкін.", tip: "Инкубаторды мүлдем ашпаңыз!" },
            { day: 21, icon: "fa-birthday-cake", title: "Шығу кезеңі!", desc: "Балапан қабықты жарып, сыртқа шығады. Құттықтаймыз! Бұл үлкен жеңіс.", tip: "Балапандардың кебуін күтіңіз." }
        ];

        const currentDay = 10;

        const loginForm = document.getElementById('login-form');
        const loginScreen = document.getElementById('login-screen');
        const mainContent = document.getElementById('main-content');
        const timelineContainer = document.getElementById('timeline-container');
        const modal = document.getElementById('modal-overlay');

        loginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const pass = document.getElementById('password').value;
            if (pass === "123" || pass === "admin") {
                loginScreen.style.display = 'none';
                mainContent.style.display = 'block';
                document.body.style.display = 'block';
                initTimeline();
            } else {
                alert("Құпия сөз қате!");
            }
        });

        function logout() { location.reload(); }

        function initTimeline() {
            timelineContainer.innerHTML = '';
            developmentStages.forEach(stage => {
                const isCompleted = stage.day <= currentDay;
                const isCurrent = stage.day === currentDay;
                
                const card = document.createElement('div');
                card.className = `day-card relative z-10 flex items-start gap-6 p-4 rounded-2xl border border-white/5 shadow-lg ${isCurrent ? 'bg-blue-500/20 border-blue-500/50' : ''}`;
                card.onclick = () => showDayDetails(stage);
                
                card.innerHTML = `
                    <div class="flex-shrink-0 w-8 h-8 rounded-full flex items-center justify-center ring-4 ring-[#0f172a] ${isCompleted ? 'bg-green-500' : 'bg-slate-700'}">
                        <i class="fas ${isCompleted ? 'fa-check' : 'fa-lock'} text-white text-[10px]"></i>
                    </div>
                    <div class="flex-shrink-0 w-12 text-center">
                        <span class="text-[9px] font-bold text-gray-500 uppercase tracking-tighter">Күн</span>
                        <div class="text-xl font-black text-white">${stage.day}</div>
                    </div>
                    <div class="flex-grow">
                        <div class="flex items-center gap-2 mb-1">
                            <i class="fas ${stage.icon} text-blue-400 text-sm"></i>
                            <h3 class="font-bold text-blue-100 text-sm">${stage.title}</h3>
                        </div>
                        <p class="text-[11px] text-gray-400 line-clamp-1 italic">${stage.desc}</p>
                    </div>
                    <i class="fas fa-chevron-right text-slate-700 self-center text-xs"></i>
                `;
                timelineContainer.appendChild(card);
            });
            document.getElementById('stat-day').textContent = `${currentDay}/21`;
        }

        function showDayDetails(stage) {
            document.getElementById('modal-title').textContent = `${stage.day}-күн мәліметі`;
            document.getElementById('modal-day-badge').textContent = `${stage.day}-КҮН`;
            document.getElementById('modal-subtitle').textContent = stage.title;
            document.getElementById('modal-description').textContent = stage.desc;
            document.getElementById('modal-tip').textContent = stage.tip;
            
            const iconEl = document.getElementById('modal-icon');
            iconEl.className = `fas ${stage.icon} text-blue-400 text-5xl`;
            
            modal.style.display = 'flex';
        }

        function closeModal() {
            modal.style.display = 'none';
        }
    </script>
</body>
</html>
