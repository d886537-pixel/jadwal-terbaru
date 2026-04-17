<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jadwal Pelajaran Digital</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #f8fafc;
        }
        .schedule-card {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .schedule-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }
        .hide-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .hide-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
    </style>
</head>
<body class="p-4 md:p-8">

    <div class="max-w-7xl mx-auto">
        <!-- Header -->
        <header class="mb-8 flex flex-col md:flex-row md:items-center justify-between gap-4">
            <div>
                <h1 class="text-3xl font-bold text-slate-900 tracking-tight">Jadwal Pelajaran</h1>
                <p class="text-slate-500">Kelola rutinitas akademik Anda dengan mudah.</p>
            </div>
            <button onclick="openModal()" class="bg-indigo-600 hover:bg-indigo-700 text-white px-6 py-2.5 rounded-xl font-semibold shadow-lg shadow-indigo-200 transition-all flex items-center justify-center gap-2">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="12 4v16m8-8H4" />
                </svg>
                Tambah Jadwal
            </button>
        </header>

        <!-- Hari Selector (Mobile) -->
        <div class="flex overflow-x-auto gap-2 mb-6 pb-2 hide-scrollbar md:hidden">
            <button onclick="scrollToDay('Senin')" class="whitespace-nowrap px-4 py-2 bg-white rounded-full text-sm font-medium border border-slate-200">Senin</button>
            <button onclick="scrollToDay('Selasa')" class="whitespace-nowrap px-4 py-2 bg-white rounded-full text-sm font-medium border border-slate-200">Selasa</button>
            <button onclick="scrollToDay('Rabu')" class="whitespace-nowrap px-4 py-2 bg-white rounded-full text-sm font-medium border border-slate-200">Rabu</button>
            <button onclick="scrollToDay('Kamis')" class="whitespace-nowrap px-4 py-2 bg-white rounded-full text-sm font-medium border border-slate-200">Kamis</button>
            <button onclick="scrollToDay('Jumat')" class="whitespace-nowrap px-4 py-2 bg-white rounded-full text-sm font-medium border border-slate-200">Jumat</button>
        </div>

        <!-- Grid Jadwal -->
        <div class="grid grid-cols-1 md:grid-cols-5 gap-6">
            <!-- Senin -->
            <div id="Senin" class="space-y-4">
                <h2 class="flex items-center gap-2 text-lg font-bold text-slate-800 border-b-2 border-indigo-500 pb-2 mb-4">
                    <span class="w-2 h-2 rounded-full bg-indigo-500"></span> Senin
                </h2>
                <div id="list-Senin" class="space-y-3"></div>
            </div>

            <!-- Selasa -->
            <div id="Selasa" class="space-y-4">
                <h2 class="flex items-center gap-2 text-lg font-bold text-slate-800 border-b-2 border-emerald-500 pb-2 mb-4">
                    <span class="w-2 h-2 rounded-full bg-emerald-500"></span> Selasa
                </h2>
                <div id="list-Selasa" class="space-y-3"></div>
            </div>

            <!-- Rabu -->
            <div id="Rabu" class="space-y-4">
                <h2 class="flex items-center gap-2 text-lg font-bold text-slate-800 border-b-2 border-amber-500 pb-2 mb-4">
                    <span class="w-2 h-2 rounded-full bg-amber-500"></span> Rabu
                </h2>
                <div id="list-Rabu" class="space-y-3"></div>
            </div>

            <!-- Kamis -->
            <div id="Kamis" class="space-y-4">
                <h2 class="flex items-center gap-2 text-lg font-bold text-slate-800 border-b-2 border-rose-500 pb-2 mb-4">
                    <span class="w-2 h-2 rounded-full bg-rose-500"></span> Kamis
                </h2>
                <div id="list-Kamis" class="space-y-3"></div>
            </div>

            <!-- Jumat -->
            <div id="Jumat" class="space-y-4">
                <h2 class="flex items-center gap-2 text-lg font-bold text-slate-800 border-b-2 border-sky-500 pb-2 mb-4">
                    <span class="w-2 h-2 rounded-full bg-sky-500"></span> Jumat
                </h2>
                <div id="list-Jumat" class="space-y-3"></div>
            </div>
        </div>
    </div>

    <!-- Modal Form -->
    <div id="modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm hidden flex items-center justify-center p-4 z-50">
        <div class="bg-white rounded-2xl w-full max-w-md shadow-2xl">
            <div class="p-6 border-b border-slate-100 flex justify-between items-center">
                <h3 class="text-xl font-bold text-slate-800">Tambah Mata Pelajaran</h3>
                <button onclick="closeModal()" class="text-slate-400 hover:text-slate-600">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>
            <form id="scheduleForm" class="p-6 space-y-4">
                <div>
                    <label class="block text-sm font-semibold text-slate-700 mb-1">Mata Pelajaran</label>
                    <input type="text" id="subject" required placeholder="Contoh: Matematika" class="w-full px-4 py-2 rounded-lg border border-slate-200 focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500 outline-none transition-all">
                </div>
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-semibold text-slate-700 mb-1">Waktu Mulai</label>
                        <input type="time" id="startTime" required class="w-full px-4 py-2 rounded-lg border border-slate-200 focus:ring-2 focus:ring-indigo-500 outline-none">
                    </div>
                    <div>
                        <label class="block text-sm font-semibold text-slate-700 mb-1">Waktu Selesai</label>
                        <input type="time" id="endTime" required class="w-full px-4 py-2 rounded-lg border border-slate-200 focus:ring-2 focus:ring-indigo-500 outline-none">
                    </div>
                </div>
                <div>
                    <label class="block text-sm font-semibold text-slate-700 mb-1">Hari</label>
                    <select id="day" class="w-full px-4 py-2 rounded-lg border border-slate-200 focus:ring-2 focus:ring-indigo-500 outline-none">
                        <option value="Senin">Senin</option>
                        <option value="Selasa">Selasa</option>
                        <option value="Rabu">Rabu</option>
                        <option value="Kamis">Kamis</option>
                        <option value="Jumat">Jumat</option>
                    </select>
                </div>
                <div>
                    <label class="block text-sm font-semibold text-slate-700 mb-1">Warna Label</label>
                    <div class="flex gap-3">
                        <input type="radio" name="color" value="bg-indigo-50" checked class="hidden peer/blue" id="c-blue">
                        <label for="c-blue" class="w-8 h-8 rounded-full bg-indigo-500 cursor-pointer peer-checked/blue:ring-4 ring-indigo-200"></label>
                        
                        <input type="radio" name="color" value="bg-emerald-50" class="hidden peer/green" id="c-green">
                        <label for="c-green" class="w-8 h-8 rounded-full bg-emerald-500 cursor-pointer peer-checked/green:ring-4 ring-emerald-200"></label>
                        
                        <input type="radio" name="color" value="bg-rose-50" class="hidden peer/red" id="c-red">
                        <label for="c-red" class="w-8 h-8 rounded-full bg-rose-500 cursor-pointer peer-checked/red:ring-4 ring-rose-200"></label>
                        
                        <input type="radio" name="color" value="bg-amber-50" class="hidden peer/yellow" id="c-yellow">
                        <label for="c-yellow" class="w-8 h-8 rounded-full bg-amber-500 cursor-pointer peer-checked/yellow:ring-4 ring-amber-200"></label>
                    </div>
                </div>
                <div class="pt-4">
                    <button type="submit" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 rounded-xl transition-colors">Simpan Jadwal</button>
                </div>
            </form>
        </div>
    </div>

    <script>
        let schedules = JSON.parse(localStorage.getItem('mySchedules')) || [];

        function openModal() {
            document.getElementById('modal').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('modal').classList.add('hidden');
            document.getElementById('scheduleForm').reset();
        }

        function scrollToDay(id) {
            document.getElementById(id).scrollIntoView({ behavior: 'smooth' });
        }

        document.getElementById('scheduleForm').addEventListener('submit', (e) => {
            e.preventDefault();
            
            const newSchedule = {
                id: Date.now(),
                subject: document.getElementById('subject').value,
                startTime: document.getElementById('startTime').value,
                endTime: document.getElementById('endTime').value,
                day: document.getElementById('day').value,
                color: document.querySelector('input[name="color"]:checked').value
            };

            schedules.push(newSchedule);
            saveData();
            renderSchedules();
            closeModal();
        });

        function deleteSchedule(id) {
            schedules = schedules.filter(s => s.id !== id);
            saveData();
            renderSchedules();
        }

        function saveData() {
            // Sort by time before saving
            schedules.sort((a, b) => a.startTime.localeCompare(b.startTime));
            localStorage.setItem('mySchedules', JSON.stringify(schedules));
        }

        function renderSchedules() {
            const days = ['Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat'];
            
            days.forEach(day => {
                const list = document.getElementById(`list-${day}`);
                list.innerHTML = '';
                
                const filtered = schedules.filter(s => s.day === day);
                
                if (filtered.length === 0) {
                    list.innerHTML = `
                        <div class="py-8 text-center border-2 border-dashed border-slate-200 rounded-xl">
                            <p class="text-xs text-slate-400">Belum ada jadwal</p>
                        </div>
                    `;
                    return;
                }

                filtered.forEach(item => {
                    const textColor = item.color.replace('bg-', 'text-').replace('-50', '-700');
                    const borderColor = item.color.replace('bg-', 'border-').replace('-50', '-200');
                    
                    list.innerHTML += `
                        <div class="schedule-card ${item.color} ${borderColor} border p-4 rounded-xl group relative">
                            <div class="flex justify-between items-start mb-1">
                                <h4 class="font-bold ${textColor} truncate pr-6">${item.subject}</h4>
                                <button onclick="deleteSchedule(${item.id})" class="opacity-0 group-hover:opacity-100 absolute top-3 right-3 text-slate-400 hover:text-rose-500 transition-all">
                                    <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" viewBox="0 0 20 20" fill="currentColor">
                                        <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd" />
                                    </svg>
                                </button>
                            </div>
                            <div class="flex items-center gap-1.5 text-xs font-semibold ${textColor} opacity-75">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-3.5 w-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                                </svg>
                                ${item.startTime} - ${item.endTime}
                            </div>
                        </div>
                    `;
                });
            });
        }

        // Initial Render
        renderSchedules();
    </script>
</body>
</html>
