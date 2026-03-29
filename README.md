<!DOCTYPE html>
<html lang="tg">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MKT SHOP | Premium Soft Edition</title>
    
    <script src="https://www.gstatic.com/firebasejs/9.17.1/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.17.1/firebase-database-compat.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;900&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --glass: rgba(255, 255, 255, 0.08);
            --glass-border: rgba(255, 255, 255, 0.15);
            --accent: #00f2fe;
            --premium-gold: #f1c40f;
            --bg-dark: #0f172a;
            --card-bg: #1e293b;
        }

        /* Асосӣ */
        * { 
            margin: 0; 
            padding: 0; 
            box-sizing: border-box; 
            font-family: 'Outfit', sans-serif; 
            -webkit-tap-highlight-color: transparent; 
        }
        
        body { 
            background: var(--bg-dark);
            background-image: radial-gradient(at 0% 0%, rgba(0, 242, 254, 0.12) 0, transparent 50%), 
                              radial-gradient(at 100% 100%, rgba(79, 172, 254, 0.12) 0, transparent 50%);
            color: white;
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* Контейнер барои Full Screen */
        .app-container {
            width: 100%;
            max-width: 1400px; /* Акнун дар компютер васеъ мешавад */
            margin: 0 auto;
            min-height: 100vh;
            position: relative;
            padding-bottom: 110px;
            background: rgba(15, 23, 42, 0.7);
            backdrop-filter: blur(10px);
        }

        /* Шапка */
        header { 
            padding: 20px; 
            position: sticky; 
            top: 0; 
            z-index: 1000; 
            background: rgba(15, 23, 42, 0.95);
            backdrop-filter: blur(25px);
            border-bottom: 1px solid var(--glass-border);
        }

        .header-top { 
            display: flex; 
            justify-content: space-between; 
            align-items: center; 
            max-width: 1200px;
            margin: 0 auto;
        }

        .logo { 
            font-size: 32px; 
            font-weight: 900; 
            background: linear-gradient(45deg, #fff, var(--accent)); 
            -webkit-background-clip: text; 
            -webkit-text-fill-color: transparent;
            letter-spacing: 1px;
        }
        
        .search-wrapper {
            max-width: 600px;
            margin: 15px auto 0;
        }

        .search-box {
            background: var(--glass); 
            border-radius: 20px; 
            padding: 12px 18px; 
            display: flex; 
            align-items: center;
            border: 1px solid var(--glass-border);
            box-shadow: inset 2px 2px 5px rgba(0,0,0,0.2);
            transition: 0.3s;
        }

        .search-box:focus-within {
            border-color: var(--accent);
            box-shadow: 0 0 15px rgba(0, 242, 254, 0.2);
        }

        .search-box input { 
            background: none; 
            border: none; 
            color: white; 
            margin-left: 10px; 
            outline: none; 
            width: 100%; 
            font-size: 16px; 
        }

        /* Категорияҳо */
        .cat-container {
            display: flex; 
            gap: 12px; 
            overflow-x: auto; 
            padding: 20px; 
            justify-content: center;
            scrollbar-width: none;
        }

        .cat-btn { 
            padding: 12px 25px; 
            background: #1e293b; 
            border: 1px solid rgba(255,255,255,0.05); 
            border-radius: 20px; 
            color: #94a3b8; 
            cursor: pointer; 
            white-space: nowrap; 
            font-weight: 600;
            transition: all 0.3s ease;
            box-shadow: 4px 4px 10px rgba(0,0,0,0.2);
        }

        .cat-btn.active { 
            background: var(--accent); 
            color: #0f172a; 
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 242, 254, 0.4);
        }

        /* Сеткаи молҳо - Responsive Grid */
        .product-grid { 
            display: grid; 
            /* Дар телефон 2 мол, дар планшет 3, дар компютер 4-5 */
            grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); 
            gap: 20px; 
            padding: 20px; 
            max-width: 1200px;
            margin: 0 auto;
        }

        @media (max-width: 480px) {
            .product-grid {
                grid-template-columns: 1fr 1fr; /* Барои телефон 2-тогӣ мемонад */
                gap: 12px;
                padding: 12px;
            }
        }

        .card { 
            background: var(--card-bg); 
            border: 1px solid var(--glass-border); 
            border-radius: 24px; 
            padding: 12px; 
            transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1); 
            position: relative;
            display: flex;
            flex-direction: column;
            height: 100%;
        }

        .card:hover { 
            transform: translateY(-8px) scale(1.02); 
            border-color: var(--accent);
            box-shadow: 0 15px 30px rgba(0,0,0,0.4);
        }

        .card img { 
            width: 100%; 
            aspect-ratio: 1/1; 
            object-fit: cover; 
            border-radius: 18px; 
            cursor: pointer; 
            margin-bottom: 10px;
        }
        
        .card h4 {
            font-size: 15px;
            margin-bottom: 8px;
            line-height: 1.3;
            height: 40px;
            overflow: hidden;
        }

        .price-tag { 
            color: var(--accent); 
            font-weight: 800; 
            font-size: 18px; 
            margin-top: auto;
            display: flex; 
            align-items: center; 
            gap: 8px; 
        }

        .old-price { 
            font-size: 13px; 
            color: #94a3b8; 
            text-decoration: line-through; 
            font-weight: 400; 
        }

        .pin-tag { 
            position: absolute; 
            top: 18px; 
            left: 18px; 
            background: var(--premium-gold); 
            color: #000; 
            padding: 4px 12px; 
            border-radius: 12px; 
            font-size: 11px; 
            font-weight: 900; 
            z-index: 5;
            box-shadow: 0 4px 8px rgba(0,0,0,0.3);
        }

        /* Навигатсия */
        nav { 
            position: fixed; 
            bottom: 25px; 
            left: 50%; 
            transform: translateX(-50%); 
            width: 90%; 
            max-width: 400px; 
            background: rgba(30, 41, 59, 0.8); 
            backdrop-filter: blur(20px); 
            border-radius: 30px; 
            border: 1px solid var(--glass-border); 
            display: flex; 
            justify-content: space-around; 
            padding: 15px; 
            z-index: 1000;
            box-shadow: 0 10px 40px rgba(0,0,0,0.5);
        }

        .nav-btn { 
            color: rgba(255,255,255,0.4); 
            font-size: 24px; 
            cursor: pointer; 
            transition: 0.3s;
        }

        .nav-btn.active { 
            color: var(--accent); 
            transform: scale(1.2);
            text-shadow: 0 0 15px var(--accent);
        }

        /* Модал */
        .modal { 
            display: none; 
            position: fixed; 
            inset: 0; 
            background: rgba(15, 23, 42, 0.95); 
            backdrop-filter: blur(15px); 
            z-index: 2000; 
            align-items: center; 
            justify-content: center; 
            padding: 20px; 
        }

        .modal-content { 
            background: #1e293b; 
            border-radius: 35px; 
            padding: 30px; 
            width: 100%; 
            max-width: 500px; 
            text-align: center; 
            border: 1px solid var(--glass-border);
            position: relative;
        }

        .slider-wrapper { 
            position: relative; 
            width: 100%; 
            height: 300px; 
            border-radius: 25px; 
            overflow: hidden; 
            margin-bottom: 20px; 
            box-shadow: 0 15px 35px rgba(0,0,0,0.4);
        }

        #m-img { width: 100%; height: 100%; object-fit: cover; }

        .s-btn-nav { 
            position: absolute; top: 50%; transform: translateY(-50%); 
            background: rgba(255,255,255,0.1); backdrop-filter: blur(10px);
            color: white; border: 1px solid rgba(255,255,255,0.2); 
            width: 45px; height: 45px; border-radius: 50%; cursor: pointer;
            display: flex; align-items: center; justify-content: center;
        }
        .s-prev { left: 15px; } .s-next { right: 15px; }

        .social-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-top: 25px; }
        .s-btn { 
            padding: 15px; border-radius: 20px; text-decoration: none; color: white; 
            font-size: 15px; font-weight: 700; display: flex; align-items: center; 
            justify-content: center; gap: 10px; transition: 0.3s;
        }
        .wa { background: #22c55e; box-shadow: 0 5px 15px rgba(34, 197, 94, 0.3); } 
        .tg { background: #3b82f6; box-shadow: 0 5px 15px rgba(59, 130, 246, 0.3); }
        .s-btn:hover { transform: scale(1.05); filter: brightness(1.1); }

        #news-panel { 
            display: none; 
            position: absolute; 
            top: 90px; 
            right: 20px; 
            width: 320px;
            background: #1e293b; 
            border: 1px solid var(--glass-border); 
            border-radius: 25px; 
            padding: 20px; 
            z-index: 1100;
            box-shadow: 0 20px 50px rgba(0,0,0,0.6);
        }
        
        @media (max-width: 500px) {
            #news-panel { left: 20px; width: auto; }
        }

    </style>
</head>
<body>

<div class="app-container">
    <header>
        <div class="header-top">
            <div class="logo">MKT SHOP</div>
            <div onclick="toggleNews()" style="cursor:pointer; position:relative; padding: 10px;">
                <i class="fas fa-bell" style="font-size: 26px; color: var(--accent);"></i>
                <span id="badge" style="display:none; position:absolute; top:8px; right:8px; background:#ff4757; width:12px; height:12px; border-radius:50%; border:2px solid #0f172a;"></span>
            </div>
        </div>
        
        <div id="news-panel">
            <h3 style="margin-bottom:15px; color:var(--accent); display:flex; align-items:center; gap:10px;"><i class="fas fa-bullhorn"></i> Хабарҳо</h3>
            <div id="news-content" style="max-height:300px; overflow-y:auto; font-size:14px; text-align:left;"></div>
        </div>

        <div class="search-wrapper">
            <div class="search-box">
                <i class="fas fa-search" style="opacity:0.5;"></i>
                <input type="text" id="searchInput" onkeyup="liveSearch()" placeholder="Ҷустуҷӯи мол...">
            </div>
        </div>
    </header>

    <div class="cat-container">
        <button class="cat-btn active" onclick="filterCat('Ҳама', this)">Ҳама</button>
        <button class="cat-btn" onclick="filterCat('Телефон', this)">Телефон</button>
        <button class="cat-btn" onclick="filterCat('Техника', this)">Техника</button>
        <button class="cat-btn" onclick="filterCat('Либос', this)">Либос</button>
    </div>

    <main>
        <div id="home-page" class="page">
            <div id="productGrid" class="product-grid"></div>
        </div>

        <div id="fav-page" class="page" style="display:none; padding:20px;">
            <h2 style="margin-bottom:25px; text-align:center;"><i class="fas fa-heart" style="color:#ff4757;"></i> Интихобшуда</h2>
            <div id="favGrid" class="product-grid"></div>
        </div>
    </main>

    <nav>
        <div class="nav-btn active" onclick="showPage('home-page', this)"><i class="fas fa-grid-2"></i><i class="fas fa-home"></i></div>
        <div class="nav-btn" onclick="showPage('fav-page', this); renderFavs()"><i class="fas fa-heart"></i></div>
    </nav>
</div>

<div id="p-modal" class="modal">
    <div class="modal-content">
        <div class="slider-wrapper">
            <button class="s-btn-nav s-prev" onclick="moveImg(-1)"><i class="fas fa-chevron-left"></i></button>
            <img id="m-img" src="">
            <button class="s-btn-nav s-next" onclick="moveImg(1)"><i class="fas fa-chevron-right"></i></button>
        </div>
        <h2 id="m-name" style="font-weight:800; margin-bottom:10px;"></h2>
        <div id="m-price-box" class="price-tag" style="font-size:28px; margin:15px 0; justify-content:center;"></div>
        <p id="m-desc" style="opacity:0.7; font-size:15px; line-height:1.6; margin-bottom:20px;"></p>
        
        <div class="social-grid">
            <a id="m-wa" href="#" target="_blank" class="s-btn wa"><i class="fab fa-whatsapp"></i> WhatsApp</a>
            <a id="m-tg" href="https://t.me/habib_2026" target="_blank" class="s-btn tg"><i class="fab fa-telegram-plane"></i> Telegram</a>
        </div>
        <button onclick="closeModal()" style="background:none; border:none; color:white; margin-top:30px; cursor:pointer; opacity:0.5; font-weight:600; letter-spacing:2px;">ПУШИДАН</button>
    </div>
</div>

<script>
    // Танзимоти Firebase
    const firebaseConfig = {
        apiKey: "AIzaSyD0bqFLASYLqZG3c0Xn08_Y1HiwSHVWwj4",
        authDomain: "habibjon2026-c7df4.firebaseapp.com",
        projectId: "habibjon2026-c7df4",
        storageBucket: "habibjon2026-c7df4.firebasestorage.app",
        messagingSenderId: "378177007395",
        appId: "1:378177007395:web:e4cfb100c4e3b5a0d52696"
    };
    firebase.initializeApp(firebaseConfig);
    const db = firebase.database();
    
    let allProducts = [];
    let favorites = JSON.parse(localStorage.getItem('mkt_favs')) || [];
    let modalImgs = [];
    let modalIdx = 0;

    // Боркунии маълумот
    window.onload = () => {
        db.ref('products').on('value', snap => {
            allProducts = []; 
            const data = snap.val();
            for(let id in data) allProducts.push({ id, ...data[id] });
            allProducts.sort((a,b) => (b.pinned || false) - (a.pinned || false));
            renderUI(allProducts);
        });

        db.ref('news').on('value', snap => {
            const data = snap.val(); 
            let html = ""; 
            let count = 0;
            for(let id in data) { 
                count++; 
                html += `
                <div style="padding:15px; border-bottom:1px solid rgba(255,255,255,0.05); background:rgba(255,255,255,0.03); border-radius:15px; margin-bottom:10px;">
                    <p style="color:#e2e8f0;">${data[id].txt}</p>
                    <small style="opacity:0.4; font-size:11px; margin-top:5px; display:block;">${data[id].date || ''}</small>
                </div>`; 
            }
            document.getElementById('news-content').innerHTML = html || "Хабарҳои нав нест.";
            document.getElementById('badge').style.display = count > 0 ? 'block' : 'none';
        });
    };

    // Намоиши молҳо
    function renderUI(list) {
        let html = "";
        list.forEach(p => {
            const isFav = favorites.includes(p.id);
            const mainImg = Array.isArray(p.images) ? p.images[0] : (p.img || "");
            let priceDisplay = p.oldPrice 
                ? `<span class="old-price">${p.oldPrice} TJS</span> <span>${p.price} TJS</span>`
                : `<span>${p.price} TJS</span>`;

            html += `
            <div class="card">
                ${p.pinned ? '<div class="pin-tag"><i class="fas fa-crown"></i> TOP</div>' : ''}
                <i class="fa-heart ${isFav ? 'fas' : 'far'}" onclick="toggleFav('${p.id}')" 
                   style="position:absolute; top:15px; right:15px; z-index:10; cursor:pointer; font-size:22px; color:${isFav?'#ff4757':'rgba(255,255,255,0.4)'}"></i>
                <img src="${mainImg}" onclick="openModal('${p.id}')">
                <h4>${p.name}</h4>
                <div class="price-tag">${priceDisplay}</div>
            </div>`;
        });
        document.getElementById('productGrid').innerHTML = html || "<p style='grid-column:1/-1; text-align:center; opacity:0.5; padding:100px;'>Мол ёфт нашуд.</p>";
    }

    // Модал функсияҳо
    function openModal(id) {
        const p = allProducts.find(x => x.id === id);
        modalImgs = Array.isArray(p.images) ? p.images : [p.img];
        modalIdx = 0;
        document.getElementById('m-name').innerText = p.name;
        
        let modalPrice = p.oldPrice 
            ? `<span class="old-price" style="font-size:20px;">${p.oldPrice} TJS</span> <span style="color:var(--accent)">${p.price} TJS</span>`
            : `<span>${p.price} TJS</span>`;
        document.getElementById('m-price-box').innerHTML = modalPrice;

        document.getElementById('m-desc').innerText = p.desc || "Дар бораи ин мол маълумоти иловагӣ нест.";
        document.getElementById('m-wa').href = `https://wa.me/992900000000?text=Салом! Мехоҳам инро харам: ${encodeURIComponent(p.name)}`;
        updateSlider();
        document.getElementById('p-modal').style.display = 'flex';
        document.body.style.overflow = 'hidden';
    }

    function moveImg(s) {
        modalIdx += s;
        if(modalIdx < 0) modalIdx = modalImgs.length - 1;
        if(modalIdx >= modalImgs.length) modalIdx = 0;
        updateSlider();
    }

    function updateSlider() { document.getElementById('m-img').src = modalImgs[modalIdx]; }
    
    function closeModal() { 
        document.getElementById('p-modal').style.display = 'none'; 
        document.body.style.overflow = 'auto';
    }
    
    // Интихобшуда (Favorites)
    function toggleFav(id) {
        if(favorites.includes(id)) favorites = favorites.filter(f => f !== id);
        else favorites.push(id);
        localStorage.setItem('mkt_favs', JSON.stringify(favorites));
        renderUI(allProducts);
    }

    // Навигатсия ва саҳифаҳо
    function showPage(pId, btn) {
        document.querySelectorAll('.page').forEach(p => p.style.display = 'none');
        document.getElementById(pId).style.display = 'block';
        document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
        window.scrollTo(0,0);
    }

    function toggleNews() { 
        const p = document.getElementById('news-panel'); 
        p.style.display = p.style.display === 'block' ? 'none' : 'block'; 
    }

    // Қустуҷӯ ва Филтр
    function liveSearch() { 
        const v = document.getElementById('searchInput').value.toLowerCase(); 
        renderUI(allProducts.filter(p => p.name.toLowerCase().includes(v))); 
    }

    function filterCat(c, b) { 
        document.querySelectorAll('.cat-btn').forEach(x => x.classList.remove('active')); 
        b.classList.add('active'); 
        renderUI(c === 'Ҳама' ? allProducts : allProducts.filter(p => p.cat === c)); 
    }

    function renderFavs() {
        const fData = allProducts.filter(p => favorites.includes(p.id));
        let h = "";
        fData.forEach(p => {
            const mImg = Array.isArray(p.images) ? p.images[0] : (p.img || "");
            h += `
            <div class="card">
                <img src="${mImg}" onclick="openModal('${p.id}')">
                <h4>${p.name}</h4>
                <div class="price-tag">${p.price} TJS</div>
            </div>`;
        });
        document.getElementById('favGrid').innerHTML = h || "<p style='grid-column:1/-1; text-align:center; padding:100px; opacity:0.5;'>Рӯйхат холӣ аст.</p>";
    }
</script>
</body>
</html>
