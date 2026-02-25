<!DOCTYPE html>
<html lang="vi" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background: #020617; color: white; font-family: 'Inter', sans-serif; overflow-x: hidden; }
        .glass { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(15px); border: 1px solid rgba(255, 255, 255, 0.1); }
        .icon-fall { position: fixed; top: -50px; pointer-events: none; animation: fall linear infinite; z-index: 100; }
        @keyframes fall { to { transform: translateY(110vh) rotate(360deg); } }
    </style>
</head>
<body>

    <script>
        function createIcon() {
            const icon = document.createElement('div');
            icon.innerHTML = '⚡'; icon.className = 'icon-fall text-xl text-yellow-500';
            icon.style.left = Math.random() * 100 + 'vw';
            icon.style.animationDuration = Math.random() * 3 + 4 + 's';
            document.body.appendChild(icon);
            setTimeout(() => icon.remove(), 7000);
        }
        setInterval(createIcon, 800);
    </script>

    <section class="py-20 text-center">
        <h1 class="text-6xl font-black uppercase text-indigo-500">HOANGDZ VIP</h1>
        <p class="text-slate-400 mt-4">Chọn gói Key - Tự động tính giá - Bảo mật tuyệt đối</p>
    </section>

    <section class="max-w-6xl mx-auto px-4 grid grid-cols-1 md:grid-cols-3 gap-6 mb-20">
        <script>
            const packs = [
                {t: '1 Giờ', p: 10000, s: '0%'}, {t: '3 Giờ', p: 15000, s: '25%'}, 
                {t: '12 Giờ', p: 25000, s: '40%'}, {t: '1 Ngày', p: 40000, s: '50%'}, 
                {t: '3 Ngày', p: 65000, s: '60%'}, {t: '1 Tuần', p: 100000, s: '70%'}, 
                {t: '1 Tháng', p: 150000, s: '85%'}
            ];
            packs.forEach((item, i) => {
                document.write(`
                    <div class="glass p-6 rounded-3xl text-center hover:border-indigo-500 transition border border-transparent">
                        <h3 class="text-xl font-bold">${item.t}</h3>
                        <div class="text-3xl font-black my-4 text-indigo-400">${item.p.toLocaleString()}đ</div>
                        <div class="text-green-400 text-sm font-bold mb-6">Tiết kiệm: ${item.s}</div>
                        <button onclick="openModal('${item.t}', ${item.p})" class="w-full py-3 bg-white text-black font-bold rounded-xl hover:bg-indigo-500 transition">MUA NGAY</button>
                    </div>
                `);
            });
        </script>
    </section>

    <div id="modal" class="fixed inset-0 hidden flex items-center justify-center bg-black/95 p-4 z-[200]">
        <div class="glass p-8 rounded-3xl w-full max-w-lg border border-indigo-500 text-center">
            <h2 id="modal-title" class="text-2xl font-bold mb-4">Mua Key</h2>
            
            <div class="flex items-center justify-center gap-6 mb-6">
                <button onclick="changeQty(-1)" class="bg-indigo-600 px-6 py-2 rounded-lg font-bold">-</button>
                <span id="qty-display" class="text-4xl font-black">1</span>
                <button onclick="changeQty(1)" class="bg-indigo-600 px-6 py-2 rounded-lg font-bold">+</button>
            </div>

            <div class="text-left bg-red-900/20 p-4 rounded-xl border border-red-500/30 mb-6 text-sm">
                <p class="text-red-400 font-bold">⚠️ CẢNH BÁO BẢO MẬT:</p>
                <p>Key chỉ dùng cho 01 thiết bị. Nếu dùng chung/thiết bị thứ 2, Key sẽ bị <b>KHÓA VĨNH VIỄN</b>. Không hoàn tiền!</p>
            </div>

            <img id="qr-code" class="mx-auto mb-4 rounded-xl border-4 border-white" width="200">
            <div class="text-xl font-bold mb-2">Thanh toán: <span id="total-price" class="text-yellow-400"></span>đ</div>
            <p class="text-slate-400 text-xs mb-4" id="bank-info">STK: 3382962182 - VCB - TRAN NHAT HOANG  LIÊN HỆ ADMIN ĐỂ NHẬN KEY @tranhoang2286</p>
            
            <button onclick="closeModal()" class="w-full py-3 bg-indigo-600 rounded-xl font-bold">ĐÃ CHUYỂN TIỀN & ĐÓNG</button>
        </div>
    </div>

    <script>
        let currentPrice = 0, currentQty = 1, currentTime = "";
        
        function openModal(t, p) {
            currentTime = t; currentPrice = p; currentQty = 1;
            document.getElementById('modal-title').innerText = "Số lượng: " + t;
            updateUI();
            document.getElementById('modal').classList.remove('hidden');
        }

        function changeQty(d) {
            currentQty = Math.max(1, Math.min(10, currentQty + d));
            updateUI();
        }

        function updateUI() {
            let total = currentPrice * currentQty;
            if(currentQty > 3) total = total * 0.65; // Giảm 35%
            document.getElementById('qty-display').innerText = currentQty;
            document.getElementById('total-price').innerText = total.toLocaleString();
            let msg = `BILL ${currentTime} ${currentQty}Cai`;
            document.getElementById('qr-code').src = `https://api.vietqr.io/image/970436-3382962182-vY9i32B.jpg?amount=${total}&addInfo=${msg}`;
        }

        function closeModal() { document.getElementById('modal').classList.add('hidden'); }
    </script>
</body>
</html>
