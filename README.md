# Nur-mia<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Teman Sejati</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #f4fbf7; /* Putih kehijauan yang lembut */
            color: #2d4a3e;
            overflow: hidden;
        }

        .card {
            background-color: #ffffff;
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(45, 74, 62, 0.1);
            text-align: center;
            max-width: 450px;
            width: 90%;
            border: 2px solid #e2f3ec;
            position: relative;
            transition: all 0.3s ease;
        }

        .sticker-container {
            font-size: 70px;
            margin-bottom: 20px;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        h1 {
            font-size: 1.8rem;
            margin-bottom: 15px;
            color: #1b4332;
        }

        p {
            font-size: 1rem;
            line-height: 1.5;
            margin-bottom: 30px;
            color: #52796f;
        }

        .btn-group {
            display: flex;
            justify-content: center;
            gap: 20px;
            position: relative;
            min-height: 50px;
        }

        button {
            padding: 12px 30px;
            font-size: 1rem;
            font-weight: 600;
            border-radius: 50px;
            cursor: pointer;
            border: none;
            transition: all 0.2s ease;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
        }

        #btn-oke {
            background-color: #40916c; /* Hijau Utama */
            color: white;
        }

        #btn-oke:hover {
            background-color: #2d6a4f;
            transform: scale(1.05);
        }

        #btn-tidak {
            background-color: #e9ecef;
            color: #495057;
            position: absolute;
            /* Inisialisasi posisi awal di kanan tombol Oke */
            left: calc(50% + 10px); 
        }

        /* Kelas modifikasi saat tombol "Tidak" mulai menghindar */
        #btn-tidak.running {
            position: fixed;
            z-index: 999;
            transition: all 0.1s ease;
        }

        /* Tampilan Pesan Sukses */
        .pesan-sukses {
            display: none;
        }

        .pesan-sukses h2 {
            color: #2d6a4f;
            margin-bottom: 15px;
        }
    </style>
</head>
<body>

    <div class="card">
        <!-- Konten Utama -->
        <div id="konten-pertanyaan">
            <div class="sticker-container" id="sticker">🤝</div>
            <h1>Apakah Kamu Teman Sejatiku?</h1>
            <p>Seorang teman sejati selalu ada di kala senang maupun susah, saling mendukung, dan bertumbuh bersama. Bagaimana denganmu?</p>
            
            <div class="btn-group">
                <button id="btn-oke">Oke</button>
                <button id="btn-tidak">Tidak</button>
            </div>
        </div>

        <!-- Konten Pesan Positif (Disembunyikan di awal) -->
        <div id="konten-sukses" class="pesan-sukses">
            <div class="sticker-container">🌱✨</div>
            <h2>Terima Kasih, Sahabat!</h2>
            <p>"Teman sejati bukanlah mereka yang membuat masalahmu runtuh, melainkan mereka yang tidak akan runtuh saat kamu menghadapi masalah." Terima kasih telah menjadi bagian penting dalam cerita hidup ini! 💚</p>
        </div>
    </div>

    <script>
        const btnTidak = document.getElementById('btn-tidak');
        const btnOke = document.getElementById('btn-oke');
        const kontenPertanyaan = document.getElementById('konten-pertanyaan');
        const kontenSukses = document.getElementById('konten-sukses');
        const sticker = document.getElementById('sticker');

        // Daftar emoji yang akan berganti secara acak saat tombol "Tidak" didekati
        const daftarSticker = ['🤨', '🧐', '👀', '🏃‍♂️', '💨'];

        // Fungsi untuk memindahkan tombol "Tidak" secara acak
        function pindahTombol() {
            // Aktifkan mode posisi fixed agar bisa bergerak bebas di seluruh layar
            if (!btnTidak.classList.contains('running')) {
                btnTidak.classList.add('running');
            }

            // Batasan layar agar tombol tidak keluar dari area pandang browser
            const padding = 20;
            const maxX = window.innerWidth - btn離開 = btnTidak.offsetWidth - padding;
            const maxY = window.innerHeight - btnTidak.offsetHeight - padding;

            // Hitung posisi acak baru
            const randomX = Math.max(padding, Math.floor(Math.random() * maxX));
            const randomY = Math.max(padding, Math.floor(Math.random() * maxY));

            btnTidak.style.left = `${randomX}px`;
            btnTidak.style.top = `${randomY}px`;

            // Iseng mengganti stiker/emoji saat user mencoba klik "Tidak"
            const emojiAcak = daftarSticker[Math.floor(Math.random() * daftarSticker.length)];
            sticker.textContent = emojiAcak;
        }

        // Jalankan fungsi pindah baik saat kursor mendekat (PC) atau disentuh (HP)
        btnTidak.addEventListener('mouseover', pindahTombol);
        btnTidak.addEventListener('touchstart', function(e) {
            e.preventDefault(); // Mencegah klik tidak sengaja pada mobile perangkat
            pindahTombol();
        });

        // Ketika tombol Oke diklik
        btnOke.addEventListener('click', () => {
            kontenPertanyaan.style.display = 'none';
            kontenSukses.style.display = 'block';
            
            // Jika tombol 'Tidak' sempat kabur, kita sembunyikan sepenuhnya
            btnTidak.style.display = 'none'; 
        });
    </script>
</body>
</html>
