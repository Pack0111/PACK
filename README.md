<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบวิเคราะห์และจองรถขนส่ง | RISEN</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500;600;700&display=swap" rel="stylesheet">

    <style>
        body { 
            font-family: 'Kanit', sans-serif; 
            background-color: #f1f5f9; 
            min-height: 100vh;
            scroll-behavior: smooth;
            font-size: 1.1rem;
        }
        
        .glass-card {
            background: #ffffff;
            border: 1px solid #e2e8f0;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.05);
            border-radius: 1.5rem;
        }

        .input-professional {
            border: 2px solid #e2e8f0;
            background: #ffffff;
            border-radius: 0.85rem;
            padding: 0.85rem 1.1rem;
            transition: all 0.2s;
            width: 100%;
            font-size: 1.1rem;
        }

        .input-professional:focus {
            border-color: #2563eb; 
            outline: none;
            box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1);
        }

        .label-bold {
            font-size: 1rem;
            font-weight: 600;
            color: #475569;
            margin-bottom: 0.5rem;
            display: block;
        }

        .section-header {
            font-size: 1.5rem;
            font-weight: 700;
            color: #0f172a;
            margin-bottom: 1.5rem;
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .type-btn {
            transition: all 0.2s;
            border: 2px solid #e2e8f0;
            background: #ffffff;
            color: #64748b;
            font-size: 1rem;
            font-weight: 600;
        }
        .type-btn.active {
            background: #2563eb; 
            color: white;
            border-color: #2563eb;
            box-shadow: 0 4px 6px -1px rgba(37, 99, 235, 0.2);
        }

        .vehicle-card {
            transition: all 0.2s;
            border: 2px solid #f1f5f9;
            cursor: pointer;
            padding: 1.5rem;
            border-radius: 1.25rem;
            background: #f8fafc;
            text-align: center;
        }
        .vehicle-card:hover {
            border-color: #cbd5e1;
            transform: translateY(-2px);
        }
        .vehicle-card.active {
            border-color: #2563eb; 
            background: #eff6ff;
            box-shadow: 0 10px 15px -3px rgba(37, 99, 235, 0.1);
        }

        .modal-overlay {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(15, 23, 42, 0.7);
            backdrop-filter: blur(8px);
            z-index: 100;
            align-items: center;
            justify-content: center;
            padding: 1rem;
        }
        .modal-overlay.active { display: flex; }

        .preview-box {
            background: #fdfdfd;
            border: 2px solid #e2e8f0;
            border-radius: 1.25rem;
            font-family: 'Kanit', sans-serif;
            white-space: pre-wrap;
            line-height: 1.6;
            font-size: 1.15rem;
            color: #1e293b;
            width: 100%;
            min-height: 600px;
            padding: 1.75rem;
            outline: none;
            resize: vertical;
        }

        .risen-badge {
            font-size: 0.85rem;
            padding: 0.25rem 0.75rem;
            border-radius: 9999px;
            font-weight: 700;
            text-transform: uppercase;
            margin-bottom: 0.5rem;
            display: inline-block;
        }

        .delete-item-btn {
            opacity: 0;
            transition: opacity 0.2s;
        }
        .history-item:hover .delete-item-btn {
            opacity: 1;
        }
    </style>
</head>
<body class="text-slate-800 pb-12">

    <div id="top" class="max-w-7xl mx-auto p-4 lg:p-8">
        
        <header class="mb-10 flex flex-col md:flex-row justify-between items-start md:items-center gap-6">
            <div class="flex items-center gap-6">
                <div class="bg-blue-600 p-5 rounded-3xl shadow-xl shadow-blue-200">
                    <svg class="w-12 h-12 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M13 10V3L4 14h7v7l9-11h-7z"></path></svg>
                </div>
                <div>
                    <h1 class="text-4xl font-black text-slate-900 leading-tight flex items-center gap-3">
                        ระบบจัดการขนส่งสินค้า
                    </h1>
                    <div class="flex gap-2 items-center mt-2">
                        <span class="bg-blue-100 text-blue-700 text-xs font-bold px-3 py-1 rounded-full uppercase tracking-tighter">มาตรฐาน RISEN</span>
                        <p class="text-slate-500 font-medium text-sm">กลยุทธ์ลอจิสติกส์และระบบจองรถอัตโนมัติ</p>
                    </div>
                </div>
            </div>
            <div class="flex flex-wrap gap-3">
                <a href="https://xn--42cah7d0cxcvbbb9x.com/%E0%B8%A3%E0%B8%B2%E0%B8%84%E0%B8%B2%E0%B8%99%E0%B9%89%E0%B8%B3%E0%B8%A1%E0%B8%B1%E0%B8%99%E0%B8%A7%E0%B8%B1%E0%B8%99%E0%B8%99%E0%B8%B5%E0%B9%89/" target="_blank" class="bg-orange-500 text-white px-6 py-3 rounded-2xl font-bold flex items-center gap-2 hover:bg-orange-600 transition-all shadow-lg shadow-orange-200 text-base">
                    ⛽ เช็คราคาน้ำมัน
                </a>
                <button onclick="toggleHistory(true)" class="bg-white border-2 border-slate-200 text-slate-700 px-6 py-3 rounded-2xl font-bold flex items-center gap-2 hover:bg-slate-50 transition-all shadow-sm text-base">
                    📂 ประวัติงาน
                </button>
            </div>
        </header>

        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8">

            <div class="lg:col-span-5 space-y-8">
                <div class="glass-card p-8">
                    <span class="risen-badge bg-purple-100 text-purple-600 font-bold">บทบาทและพาหนะ</span>
                    <h2 class="section-header">
                        <span class="bg-blue-100 text-blue-600 p-2.5 rounded-xl"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 17a2 2 0 11-4 0 2 2 0 014 0zM19 17a2 2 0 11-4 0 2 2 0 014 0z"></path></svg></span>
                        ประเภทรถขนส่ง
                    </h2>
                    <div class="grid grid-cols-2 gap-4" id="vehicle-grid"></div>
                </div>

                <div class="glass-card p-8">
                    <span class="risen-badge bg-blue-100 text-blue-600 font-bold">รายละเอียดและขอบเขตงาน</span>
                    <h2 class="section-header">
                        <span class="bg-orange-100 text-orange-600 p-2.5 rounded-xl"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"></path></svg></span>
                        ข้อมูลรายละเอียดงาน
                    </h2>
                    
                    <div class="flex gap-3 p-1.5 bg-slate-100 rounded-2xl mb-8">
                        <button onclick="setJob('ขาเข้า (Import)')" id="job-Import" class="type-btn active flex-1 py-3 rounded-xl text-sm">Import</button>
                        <button onclick="setJob('ขาออก (Export)')" id="job-Export" class="type-btn flex-1 py-3 rounded-xl text-sm">Export</button>
                        <button onclick="setJob('งานทั่วไป (General)')" id="job-General" class="type-btn flex-1 py-3 rounded-xl text-sm">General</button>
                    </div>

                    <div class="space-y-6">
                        <div>
                            <label class="label-bold">ชื่อลูกค้า / ชื่องาน</label>
                            <input type="text" id="ref-name" oninput="updateBookingPreview()" placeholder="ระบุชื่องาน..." class="input-professional font-bold text-xl">
                        </div>

                        <div id="date-grid" class="grid grid-cols-2 gap-4"></div>

                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label class="label-bold">จำนวน (Qty)</label>
                                <input type="number" id="qty" value="1" oninput="updateBookingPreview()" class="input-professional text-center font-bold text-xl">
                            </div>
                            <div>
                                <label class="label-bold">น้ำหนักรวม</label>
                                <input type="text" id="weight" value="25 ตัน" oninput="updateBookingPreview()" class="input-professional text-xl">
                            </div>
                        </div>

                        <div>
                            <label class="label-bold">รายละเอียดงาน (เช่น ขนาดตู้/สินค้า)</label>
                            <input type="text" id="size" value="40'HQ" oninput="updateBookingPreview()" class="input-professional text-xl">
                        </div>

                        <div>
                            <label class="label-bold text-blue-600">📝 หมายเหตุเพิ่มเติม</label>
                            <textarea id="job-notes" rows="3" oninput="updateBookingPreview()" class="input-professional text-base" placeholder="เช่น ขอคนขับมีใบขับขี่ประเภท 4, คลุมผ้าใบ..."></textarea>
                        </div>

                        <div id="location-fields" class="space-y-4 pt-4 border-t-2 border-slate-100"></div>
                    </div>
                </div>
            </div>

            <div class="lg:col-span-7 space-y-8">
                <div class="glass-card p-8">
                    <div class="flex justify-between items-center mb-8">
                        <div>
                            <span class="risen-badge bg-orange-100 text-orange-600 font-bold">วิเคราะห์ต้นทุน</span>
                            <h2 class="section-header mb-0">
                                <span class="bg-indigo-100 text-indigo-600 p-2.5 rounded-xl"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path></svg></span>
                                คำนวณกำไรเบื้องต้น
                            </h2>
                        </div>
                    </div>
                    
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
                        <div class="bg-slate-50 p-6 rounded-3xl border-2 border-slate-100">
                            <label class="label-bold text-slate-500 uppercase text-xs">ระยะทางรวม (กม.)</label>
                            <input type="number" id="distance" value="0" class="bg-transparent text-5xl font-black text-slate-900 w-full outline-none mt-2">
                        </div>
                        <div class="bg-blue-600 p-6 rounded-3xl text-white shadow-xl shadow-blue-100">
                            <label class="label-bold text-blue-200 uppercase text-xs">ราคาที่เสนอขาย (บาท)</label>
                            <input type="number" id="revenue" value="0" class="bg-transparent text-5xl font-black text-white w-full outline-none mt-2">
                        </div>
                    </div>

                    <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-6">
                        <div>
                            <label class="label-bold text-sm">ราคาน้ำมัน</label>
                            <input type="number" id="fuel-price" value="33" class="input-professional text-lg font-bold">
                        </div>
                        <div>
                            <label class="label-bold text-sm">อัตราสิ้นเปลือง</label>
                            <input type="number" id="fuel-rate" value="3.5" class="input-professional text-lg font-bold">
                        </div>
                        <div>
                            <label class="label-bold text-orange-600 text-sm">ค่าน้ำมัน (Auto)</label>
                            <input type="number" id="fuel-cost-manual" value="0" class="input-professional text-lg font-bold bg-orange-50/50">
                        </div>
                        <div>
                            <label class="label-bold text-blue-600 text-sm">หักบริหาร (%)</label>
                            <input type="number" id="admin-percent" value="40" class="input-professional text-lg font-bold border-blue-200 bg-blue-50/30">
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-4 gap-4">
                        <div>
                            <label class="label-bold text-sm">ค่าเสื่อม (บาท/กม.)</label>
                            <input type="number" id="maint-rate" value="2.5" class="input-professional text-base">
                        </div>
                        <div>
                            <label class="label-bold text-sm">ค่าเที่ยวพนักงาน</label>
                            <input type="number" id="driver-fee" value="1500" class="input-professional text-base">
                        </div>
                        <div>
                            <label class="label-bold text-sm">ค่าทางด่วน/อื่นๆ</label>
                            <input type="number" id="toll-fee" value="0" class="input-professional text-base">
                        </div>
                        <div>
                            <label class="label-bold text-sm text-purple-600">ต้นทุนอื่นๆ</label>
                            <input type="number" id="other-cost" value="0" class="input-professional text-base border-purple-200">
                        </div>
                    </div>
                </div>

                <div class="bg-slate-900 rounded-[3rem] p-10 text-white relative overflow-hidden shadow-2xl">
                    <div class="absolute right-0 top-0 w-80 h-80 bg-blue-500/10 rounded-full blur-[100px]"></div>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-10 items-center relative z-10">
                        <div>
                            <p class="text-blue-400 font-bold uppercase tracking-widest text-xs mb-3">กำไรสุทธิโดยประมาณ</p>
                            <div class="flex items-baseline gap-3">
                                <span id="profit-val" class="text-7xl font-black">0</span>
                                <span class="text-2xl text-slate-500 font-bold">฿</span>
                            </div>
                            
                            <div class="mt-10 pt-8 border-t border-white/10 flex gap-10">
                                <div>
                                    <p class="text-slate-500 text-xs font-bold uppercase mb-2 text-center">ต้นทุนรวม</p>
                                    <p class="text-3xl font-bold" id="total-cost-val">0</p>
                                </div>
                                <div>
                                    <p class="text-slate-500 text-xs font-bold uppercase mb-2 text-center">ต้นทุน/กม.</p>
                                    <p class="text-3xl font-bold text-blue-400" id="cpk-val">0.00</p>
                                </div>
                            </div>
                        </div>
                        
                        <div class="flex flex-col gap-4">
                            <button id="copy-btn" onclick="copyText()" class="bg-blue-600 hover:bg-blue-500 text-white py-5 rounded-2xl font-black text-xl flex items-center justify-center gap-4 transition-all active:scale-95 shadow-xl shadow-blue-600/20">
                                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M8 5H6a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2v-1M8 5a2 2 0 002 2h2a2 2 0 002-2M8 5a2 2 0 002 2h2a2 2 0 002-2m0 0h2a2 2 0 012 2v3m2 4H10m0 0l3-3m-3 3l3 3"></path></svg>
                                คัดลอกข้อความ
                            </button>
                            <button onclick="saveToHistory()" class="bg-slate-800 hover:bg-slate-700 text-white py-4 rounded-xl font-bold text-base flex items-center justify-center gap-3 transition-all">
                                💾 บันทึกเก็บประวัติ
                            </button>
                            <button onclick="toggleModal(true)" class="bg-white/5 hover:bg-white/10 text-white py-3.5 rounded-xl font-bold text-xs transition-all text-center border border-white/10 uppercase tracking-widest">
                                ดูรายละเอียดต้นทุน →
                            </button>
                        </div>
                    </div>
                </div>

                <div class="glass-card p-8 border-blue-100 bg-blue-50/10">
                    <div class="flex justify-between items-center mb-6">
                        <div>
                            <span class="risen-badge bg-green-100 text-green-600 font-bold">ผลลัพธ์การจอง</span>
                            <h2 class="section-header mb-0">
                                <span class="bg-emerald-500 text-white p-2 rounded-lg"><svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7"></path></svg></span>
                                แพทเทิร์น เช็คราคา/จองรถ
                            </h2>
                        </div>
                        <button onclick="resetBookingPreview()" class="text-xs font-bold text-slate-400 hover:text-blue-600 transition-colors uppercase tracking-widest flex items-center gap-1">
                            รีเซ็ตข้อความ
                        </button>
                    </div>
                    <textarea id="booking-preview" class="preview-box border-slate-200" spellcheck="false" placeholder="ข้อมูลจะปรากฏที่นี่..."></textarea>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal รายละเอียดต้นทุน -->
    <div id="modal-summary" class="modal-overlay" onclick="if(event.target == this) toggleModal(false)">
        <div class="bg-white rounded-[2.5rem] w-full max-w-md overflow-hidden shadow-2xl">
            <div class="bg-slate-900 p-10 text-white text-center">
                <div class="bg-blue-500 w-16 h-16 rounded-2xl flex items-center justify-center mx-auto mb-4 shadow-lg">
                    <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z"></path></svg>
                </div>
                <h3 class="text-3xl font-black">รายละเอียดต้นทุน</h3>
                <p class="text-slate-500 text-xs mt-2 uppercase tracking-widest font-bold">การคำนวณตามจริง</p>
            </div>
            <div class="p-8 space-y-3" id="modal-list"></div>
            <div class="px-8 pb-10">
                <div class="bg-slate-50 p-6 rounded-3xl border-2 border-slate-100 flex justify-between items-center">
                    <div>
                        <p class="text-slate-400 text-xs font-black uppercase mb-1">รวมต้นทุนสุทธิ</p>
                        <p class="text-3xl font-black text-slate-900" id="modal-total">0.-</p>
                    </div>
                    <button onclick="toggleModal(false)" class="bg-blue-600 text-white px-8 py-4 rounded-2xl font-bold shadow-lg shadow-blue-100 text-base">ปิดหน้าต่าง</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal ประวัติงาน -->
    <div id="modal-history" class="modal-overlay" onclick="if(event.target == this) toggleHistory(false)">
        <div class="bg-white rounded-[2.5rem] w-full max-w-3xl overflow-hidden shadow-2xl flex flex-col max-h-[85vh]">
            <div class="p-8 border-b-2 border-slate-100 flex justify-between items-center bg-slate-50">
                <h3 class="text-2xl font-black text-slate-900">ประวัติงานย้อนหลัง</h3>
                <button onclick="clearHistory()" class="text-rose-500 font-bold text-sm hover:bg-rose-50 px-4 py-2 rounded-lg transition-all">ล้างทั้งหมด</button>
            </div>
            <div id="history-content" class="p-8 overflow-y-auto flex-1 space-y-4 bg-white"></div>
            <div class="p-6 bg-slate-50 text-center border-t-2 border-slate-100">
                <button onclick="toggleHistory(false)" class="bg-slate-900 text-white px-10 py-3 rounded-xl font-bold text-base">ปิดหน้าต่าง</button>
            </div>
        </div>
    </div>

    <script>
        const vehicles = [
            { id: 'v1', name: 'สิบล้อ 3 เพลา', icon: '🚛', fuel: 3.5, maint: 2.5, driver: 1500 },
            { id: 'v2', name: 'หกล้อ 2 เพลา', icon: '🚚', fuel: 4.8, maint: 1.8, driver: 1200 },
            { id: 'v3', name: 'หัวลาก/เทรลเลอร์', icon: '🚜', fuel: 3.2, maint: 3.5, driver: 1800 },
            { id: 'v4', name: 'รถกระบะ/LCL', icon: '📦', fuel: 8.5, maint: 1.2, driver: 1000 }
        ];

        let state = { 
            vehicle: vehicles[0], 
            job: 'ขาเข้า (Import)', 
            isManualFuel: false, 
            isUserEditing: false 
        };

        function init() {
            renderVehicles();
            setJob('ขาเข้า (Import)');
            setupListeners();
            calculate();
            
            document.getElementById('booking-preview').addEventListener('input', () => {
                state.isUserEditing = true;
            });
        }

        function renderVehicles() {
            const container = document.getElementById('vehicle-grid');
            container.innerHTML = vehicles.map(v => `
                <div class="vehicle-card ${state.vehicle.id === v.id ? 'active' : ''}" onclick="selectVehicle('${v.id}')">
                    <div class="text-4xl mb-2">${v.icon}</div>
                    <p class="text-sm font-bold text-slate-800 uppercase tracking-tight">${v.name}</p>
                </div>
            `).join('');
        }

        function selectVehicle(id) {
            state.vehicle = vehicles.find(v => v.id === id);
            document.getElementById('fuel-rate').value = state.vehicle.fuel;
            document.getElementById('maint-rate').value = state.vehicle.maint;
            document.getElementById('driver-fee').value = state.vehicle.driver;
            state.isManualFuel = false;
            state.isUserEditing = false;
            renderVehicles();
            calculate();
            updateBookingPreview();
        }

        function setJob(type, initialData = {}) {
            state.job = type;
            state.isUserEditing = false;
            document.querySelectorAll('.type-btn').forEach(b => {
                const btnLabel = b.innerText.toLowerCase();
                if(type.toLowerCase().includes(btnLabel)) b.classList.add('active');
                else b.classList.remove('active');
            });
            
            const dateGrid = document.getElementById('date-grid');
            if(type === 'ขาออก (Export)') {
                dateGrid.className = "grid grid-cols-1 gap-4";
                dateGrid.innerHTML = `
                    <div class="grid grid-cols-2 gap-4">
                        <div>
                            <label class="label-bold text-blue-600 text-sm">🗓️ รับตู้เปล่า</label>
                            <input type="text" id="date-pickup" oninput="updateBookingPreview()" placeholder="วว/ดด/ปป" value="${initialData.datePickup || ''}" class="input-professional text-base">
                        </div>
                        <div>
                            <label class="label-bold text-blue-600 text-sm">🗓️ วันบรรจุ</label>
                            <input type="text" id="date-stuff" oninput="updateBookingPreview()" placeholder="วว/ดด/ปป" value="${initialData.dateStuff || ''}" class="input-professional text-base">
                        </div>
                    </div>
                    <div>
                        <label class="label-bold text-blue-600 text-sm">🚢 วันคืนตู้/ลงท่า</label>
                        <input type="text" id="date-return" oninput="updateBookingPreview()" placeholder="วว/ดด/ปป" value="${initialData.dateReturn || ''}" class="input-professional text-base">
                    </div>
                `;
            } else {
                dateGrid.className = "grid grid-cols-2 gap-4";
                const label1 = type === 'ขาเข้า (Import)' ? '🗓️ วันรับตู้/สินค้า' : '🗓️ วันไปรับงาน';
                const label2 = type === 'ขาเข้า (Import)' ? '🚚 วันส่งตู้/สินค้า' : '🚚 วันที่ไปส่ง';
                dateGrid.innerHTML = `
                    <div>
                        <label class="label-bold text-blue-600 text-sm">${label1}</label>
                        <input type="text" id="date-start" oninput="updateBookingPreview()" placeholder="วว/ดด/ปป" value="${initialData.dateStart || ''}" class="input-professional text-base">
                    </div>
                    <div>
                        <label class="label-bold text-blue-600 text-sm">${label2}</label>
                        <input type="text" id="date-end" oninput="updateBookingPreview()" placeholder="วว/ดด/ปป" value="${initialData.dateEnd || ''}" class="input-professional text-base">
                    </div>
                `;
            }

            const locContainer = document.getElementById('location-fields');
            let fields = [];
            if(type === 'ขาเข้า (Import)') fields = ['ลานรับตู้ (Port/Yard)', 'สถานที่ส่งของ (Factory)', 'ลานคืนตู้ (Return Yard)'];
            else if(type === 'ขาออก (Export)') fields = ['ลานรับตู้เปล่า (Yard)', 'สถานที่บรรจุ (Factory)', 'สถานที่คืนตู้ (Port)'];
            else fields = ['สถานที่ต้นทาง (Pickup)', 'จุดแวะพัก (Stopover)', 'สถานที่ปลายทาง (Destination)'];

            locContainer.innerHTML = fields.map((f, i) => `
                <div>
                    <label class="label-bold text-slate-400 font-medium text-sm">${f}</label>
                    <input type="text" id="loc-${i}" oninput="updateBookingPreview()" value="${(initialData.locations && initialData.locations[i]) || ''}" placeholder="..." class="input-professional bg-slate-50/50 text-base">
                </div>
            `).join('');
            
            updateBookingPreview();
        }

        function calculate() {
            const dist = parseFloat(document.getElementById('distance').value) || 0;
            const rev = parseFloat(document.getElementById('revenue').value) || 0;
            const fPrice = parseFloat(document.getElementById('fuel-price').value) || 0;
            const fRate = parseFloat(document.getElementById('fuel-rate').value) || 1;
            const mRate = parseFloat(document.getElementById('maint-rate').value) || 0;
            const driver = parseFloat(document.getElementById('driver-fee').value) || 0;
            const toll = parseFloat(document.getElementById('toll-fee').value) || 0;
            const other = parseFloat(document.getElementById('other-cost').value) || 0;
            const adminPct = parseFloat(document.getElementById('admin-percent').value) || 0;
            
            let fuelCost = 0;
            if (state.isManualFuel) {
                fuelCost = parseFloat(document.getElementById('fuel-cost-manual').value) || 0;
            } else {
                fuelCost = dist > 0 ? (dist / fRate) * fPrice : 0;
                document.getElementById('fuel-cost-manual').value = Math.round(fuelCost);
            }

            const maintCost = dist * mRate;
            const fieldCost = fuelCost + maintCost + driver + toll + other;
            const adminFee = fieldCost * (adminPct / 100);
            const totalCost = fieldCost + adminFee;
            const profit = rev - totalCost;

            const profitEl = document.getElementById('profit-val');
            profitEl.innerText = Math.round(profit).toLocaleString();
            profitEl.className = `text-7xl font-black ${profit >= 0 ? 'text-emerald-500' : 'text-rose-500'}`;

            document.getElementById('total-cost-val').innerText = Math.round(totalCost).toLocaleString();
            document.getElementById('cpk-val').innerText = dist > 0 ? (totalCost / dist).toFixed(2) : "0.00";

            const items = [
                { l: '⛽ ค่าน้ำมัน', v: fuelCost },
                { l: '🛠️ ค่าเสื่อมและบำรุงรักษา', v: maintCost },
                { l: '👤 ค่าเที่ยวพนักงาน', v: driver },
                { l: '🛣️ ค่าทางด่วน/จิปาถะ', v: toll },
                { l: '📦 ต้นทุนอื่นๆ', v: other },
                { l: `📊 ค่าบริหารจัดการ (${adminPct}%)`, v: adminFee }
            ];
            
            document.getElementById('modal-list').innerHTML = items.map(i => `
                <div class="flex justify-between items-center p-4 bg-slate-50 rounded-2xl border-2 border-slate-100">
                    <span class="text-slate-500 font-bold text-xs uppercase">${i.l}</span>
                    <span class="text-slate-900 font-black text-lg">${Math.round(i.v).toLocaleString()}.-</span>
                </div>
            `).join('');
            document.getElementById('modal-total').innerText = Math.round(totalCost).toLocaleString() + ".-";
            return { totalCost, profit };
        }

        function setupListeners() {
            ['distance', 'revenue', 'fuel-price', 'fuel-rate', 'maint-rate', 'driver-fee', 'toll-fee', 'other-cost', 'admin-percent'].forEach(id => {
                document.getElementById(id).addEventListener('input', () => {
                    if(id !== 'admin-percent') state.isManualFuel = false;
                    state.isUserEditing = false;
                    calculate();
                    updateBookingPreview();
                });
            });
            document.getElementById('fuel-cost-manual').addEventListener('input', () => {
                state.isManualFuel = true;
                calculate();
            });
        }

        function generateBookingText() {
            const refName = document.getElementById('ref-name').value || 'ยังไม่ได้ระบุ';
            const qty = document.getElementById('qty').value;
            const size = document.getElementById('size').value;
            const weight = document.getElementById('weight').value;
            const note = document.getElementById('job-notes').value || '-';
            const loc0 = document.getElementById('loc-0')?.value || '-';
            const loc1 = document.getElementById('loc-1')?.value || '-';
            const loc2 = document.getElementById('loc-2')?.value || '-';

            const locs = [loc0, loc1, loc2].filter(l => l && l !== '-' && l !== '');
            let gpsLink = "ยังไม่มีข้อมูลสถานที่";
            if (locs.length >= 2) {
                gpsLink = `https://www.google.com/maps/dir/${locs.map(l => encodeURIComponent(l)).join('/')}`;
            }

            let dateBlock = "";
            if(state.job === 'ขาออก (Export)') {
                const d1 = document.getElementById('date-pickup')?.value || '-';
                const d2 = document.getElementById('date-stuff')?.value || '-';
                const d3 = document.getElementById('date-return')?.value || '-';
                dateBlock = `🗓️ รับตู้เปล่า: ${d1}\n🗓️ วันบรรจุ: ${d2}\n🚢 วันคืนตู้/ลงท่า: ${d3}`;
            } else {
                const dStart = document.getElementById('date-start')?.value || '-';
                const dEnd = document.getElementById('date-end')?.value || '-';
                const label1 = state.job === 'ขาเข้า (Import)' ? 'รับตู้' : 'รับงาน';
                const label2 = state.job === 'ขาเข้า (Import)' ? 'ส่งตู้' : 'ไปส่ง';
                dateBlock = `🗓️ วัน${label1}: ${dStart}\n🚚 วัน${label2}: ${dEnd}`;
            }

            return `✨ [เช็คราคาขนส่ง / จองรถ] ✨
-------------------------------------
📋 ชื่องาน: ${refName}
💼 ประเภท: ${state.job}
🚛 ประเภทรถ: ${state.vehicle.name}
📦 รายละเอียด: ${qty} x ${size} (${weight})

${dateBlock}

📍 เส้นทาง (Location):
   1. ${loc0}
   2. ${loc1}
   3. ${loc2}

📝 หมายเหตุ: 
   ${note}

🔗 GPS แผนที่เส้นทาง: 
   ${gpsLink}
-------------------------------------`;
        }

        function updateBookingPreview() {
            if (state.isUserEditing) return;
            document.getElementById('booking-preview').value = generateBookingText();
        }

        function resetBookingPreview() {
            state.isUserEditing = false;
            updateBookingPreview();
        }

        function copyText() {
            const previewEl = document.getElementById('booking-preview');
            previewEl.select();
            document.execCommand('copy');
            const btn = document.getElementById('copy-btn');
            const old = btn.innerHTML;
            btn.innerHTML = `✅ คัดลอกแล้ว!`;
            setTimeout(() => btn.innerHTML = old, 1500);
        }

        function saveToHistory() {
            const ref = document.getElementById('ref-name').value;
            if(!ref) { alert("กรุณาระบุชื่องานเพื่อบันทึก"); return; }
            const results = calculate();
            const jobData = {
                id: Date.now(),
                date: new Date().toLocaleString('th-TH'),
                ref: ref,
                rev: document.getElementById('revenue').value,
                dist: document.getElementById('distance').value,
                qty: document.getElementById('qty').value,
                size: document.getElementById('size').value,
                weight: document.getElementById('weight').value,
                datePickup: document.getElementById('date-pickup')?.value || '',
                dateStuff: document.getElementById('date-stuff')?.value || '',
                dateReturn: document.getElementById('date-return')?.value || '',
                dateStart: document.getElementById('date-start')?.value || '',
                dateEnd: document.getElementById('date-end')?.value || '',
                note: document.getElementById('job-notes').value,
                jobType: state.job,
                vehicleId: state.vehicle.id,
                adminPct: document.getElementById('admin-percent').value,
                otherCost: document.getElementById('other-cost').value,
                locations: [
                    document.getElementById('loc-0')?.value || '',
                    document.getElementById('loc-1')?.value || '',
                    document.getElementById('loc-2')?.value || ''
                ],
                profit: results.profit
            };
            let history = JSON.parse(localStorage.getItem('ma_history') || '[]');
            history.unshift(jobData);
            localStorage.setItem('ma_history', JSON.stringify(history.slice(0, 100)));
            alert('บันทึกข้อมูลเรียบร้อยแล้ว!');
        }

        function deleteJob(e, id) {
            e.stopPropagation(); // หยุดการโหลดงานขึ้นมาทำงานเมื่อกดปุ่มลบ
            if(!confirm('คุณต้องการลบประวัติงานนี้ใช่หรือไม่?')) return;
            
            let history = JSON.parse(localStorage.getItem('ma_history') || '[]');
            history = history.filter(h => h.id !== id);
            localStorage.setItem('ma_history', JSON.stringify(history));
            renderHistory();
        }

        function loadHistoryJob(id) {
            const history = JSON.parse(localStorage.getItem('ma_history') || '[]');
            const job = history.find(h => h.id === id);
            if(!job) return;
            document.getElementById('ref-name').value = job.ref;
            document.getElementById('distance').value = job.dist;
            document.getElementById('revenue').value = job.rev;
            document.getElementById('qty').value = job.qty;
            document.getElementById('size').value = job.size;
            document.getElementById('weight').value = job.weight;
            document.getElementById('job-notes').value = job.note;
            document.getElementById('admin-percent').value = job.adminPct || 40;
            document.getElementById('other-cost').value = job.otherCost || 0;
            state.isUserEditing = false;
            selectVehicle(job.vehicleId);
            setJob(job.jobType, job);
            calculate();
            toggleHistory(false);
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function toggleHistory(s) {
            document.getElementById('modal-history').classList.toggle('active', s);
            if(s) renderHistory();
        }

        function renderHistory() {
            const container = document.getElementById('history-content');
            const history = JSON.parse(localStorage.getItem('ma_history') || '[]');
            if(history.length === 0) { 
                container.innerHTML = '<div class="text-center text-slate-400 py-12"><p class="text-5xl mb-4">📂</p><p class="text-sm font-bold">ไม่พบประวัติงาน</p></div>'; 
                return; 
            }
            container.innerHTML = history.map(h => `
                <div class="history-item bg-slate-50 p-6 rounded-3xl border-2 border-slate-100 flex justify-between items-center group cursor-pointer hover:bg-white hover:border-blue-300 transition-all" onclick="loadHistoryJob(${h.id})">
                    <div class="flex items-center gap-6">
                        <div class="bg-blue-600 text-white p-3.5 rounded-2xl">
                            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"></path></svg>
                        </div>
                        <div>
                            <h4 class="font-bold text-slate-900 text-lg">${h.ref}</h4>
                            <p class="text-xs text-slate-500 font-bold uppercase tracking-tight">${h.jobType} • ${h.dist} กม. • ${h.date}</p>
                        </div>
                    </div>
                    <div class="flex items-center gap-6">
                        <div class="text-right">
                            <p class="text-xl font-black ${h.profit >= 0 ? 'text-emerald-500' : 'text-rose-500'}">${Math.round(h.profit).toLocaleString()}.-</p>
                            <p class="text-[10px] text-slate-400 uppercase font-black">กำไร</p>
                        </div>
                        <button onclick="deleteJob(event, ${h.id})" class="delete-item-btn p-3 bg-rose-50 text-rose-500 rounded-xl hover:bg-rose-500 hover:text-white transition-all">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg>
                        </button>
                    </div>
                </div>
            `).join('');
        }

        function clearHistory() {
            if(confirm('คุณแน่ใจหรือไม่ว่าต้องการลบประวัติงานทั้งหมด?')) { localStorage.removeItem('ma_history'); renderHistory(); }
        }

        function toggleModal(s) { document.getElementById('modal-summary').classList.toggle('active', s); }

        window.onload = init;
    </script>
</body>
</html>
