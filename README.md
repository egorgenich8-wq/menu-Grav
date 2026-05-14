<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <title>ГРАВИТАЦИЯ · Горное меню</title>
    <!-- Системные мета-теги для скрытия интерфейса браузера в режиме PWA -->
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="theme-color" content="#2a1f17">
    
    <style>
        /* ---------- ГЛОБАЛЬНЫЙ СБРОС ---------- */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        /* Основной фон страницы — тёмный кофейный с деликатным паттерном */
        body {
            background: #2a1f17;
            background-image: radial-gradient(#c2824b 0.7px, transparent 0.7px);
            background-size: 28px 28px;
            font-family: 'Inter', 'Segoe UI', 'Roboto', system-ui, -apple-system, 'Helvetica Neue', sans-serif;
            padding: 0;
            margin: 0;
            color: #f0e3d4;
            overflow-x: hidden;
            min-height: 100vh;
        }

        /* Контейнер меню — без лишних отступов */
        .menu-container {
            max-width: 100%;
            width: 100%;
            margin: 0 auto;
            background: #35281e;
            border-radius: 0;
            box-shadow: none;
            overflow-x: hidden;
            border: none;
            min-height: 100vh;
        }

        /* ---------- ШАПКА С СИЛУЭТОМ ГОР ---------- */
        .cafe-header {
            position: relative;
            text-align: center;
            background: linear-gradient(145deg, #2f221b 0%, #3a2a1f 100%);
            border-bottom: 1px solid #5a3f2e;
            overflow: hidden;
            padding: 1.2rem 1rem 0.8rem 1rem;
        }

        /* SVG силуэт гор — фоновая графика */
        .mountains-bg {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            opacity: 0.45;
            pointer-events: none;
        }

        .mountains-bg svg {
            width: 100%;
            height: 100%;
            display: block;
        }

        .header-content {
            position: relative;
            z-index: 2;
        }

        /* Название кафе — без переноса строки, поверх гор */
        .cafe-name {
            font-family: 'Georgia', 'Times New Roman', serif;
            font-size: 1.9rem;
            font-weight: 700;
            letter-spacing: 1px;
            color: #f2e2cf;
            text-shadow: 0 4px 12px rgba(0, 0, 0, 0.5), 0 1px 2px rgba(0,0,0,0.8);
            white-space: nowrap;
            display: inline-block;
            background: rgba(0,0,0,0.25);
            backdrop-filter: blur(4px);
            padding: 0.2rem 1.2rem;
            border-radius: 60px;
        }

        @media (max-width: 400px) {
            .cafe-name {
                font-size: 1.5rem;
                letter-spacing: 0.3px;
                padding: 0.1rem 0.9rem;
            }
        }

        .cafe-slogan {
            font-size: 0.75rem;
            color: #f3ddc2;
            letter-spacing: 0.4px;
            font-weight: 500;
            border-top: 1px dashed #dbb07c;
            display: inline-block;
            padding-top: 0.4rem;
            margin-top: 0.4rem;
            text-shadow: 0 1px 2px black;
        }

        /* ---------- ПАНЕЛЬ ЗАКАЗА ---------- */
        .order-panel {
            background: rgba(45, 31, 24, 0.85);
            backdrop-filter: blur(8px);
            margin: 1rem 1rem 0 1rem;
            padding: 0.7rem 1rem;
            border-radius: 28px;
            border: 1px solid rgba(106, 77, 54, 0.6);
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 0.6rem;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4);
        }

        .total-label {
            font-size: 0.85rem;
            font-weight: 600;
            color: #e7bc8e;
            letter-spacing: 0.5px;
        }

        .total-amount {
            font-size: 1.6rem;
            font-weight: 800;
            background: linear-gradient(135deg, #f3c693, #e7bc8e);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            padding: 0.1rem 0.5rem;
            font-family: monospace;
            text-shadow: 0 0 8px rgba(231,188,142,0.3);
        }

        .reset-btn {
            background: rgba(79, 54, 40, 0.9);
            border: 1px solid #c2824b;
            color: #f0cfaa;
            padding: 0.4rem 1.2rem;
            border-radius: 50px;
            font-weight: 600;
            cursor: pointer;
            font-size: 0.75rem;
            font-family: inherit;
            transition: all 0.2s ease;
            backdrop-filter: blur(4px);
        }
        .reset-btn:active {
            transform: scale(0.94);
            background: #c2824b;
            color: #2a1f17;
        }

        /* ---------- ОСНОВНОЕ МЕНЮ ---------- */
        .menu-inner {
            padding: 1rem 1rem 2rem 1rem;
        }

        .category {
            margin-bottom: 2rem;
        }

        /* Градиентные заголовки категорий */
        .category-title {
            font-family: 'Georgia', 'Times New Roman', serif;
            font-size: 1.4rem;
            font-weight: 600;
            background: linear-gradient(135deg, #e7bc8e, #c2824b);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-align: center;
            margin-bottom: 1.2rem;
            border-bottom: 1px solid rgba(90, 63, 46, 0.6);
            padding-bottom: 0.45rem;
            width: fit-content;
            margin-left: auto;
            margin-right: auto;
            letter-spacing: -0.2px;
        }

        .items-grid {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        /* СТЕКЛЯННЫЕ карточки блюд + анимация появления */
        .menu-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: rgba(47, 34, 27, 0.8);
            backdrop-filter: blur(8px);
            padding: 12px 16px;
            border-radius: 24px;
            border: 1px solid rgba(231, 188, 142, 0.2);
            transition: all 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1);
            cursor: pointer;
            box-shadow: 0 6px 14px rgba(0, 0, 0, 0.3), inset 0 1px 0 rgba(255, 255, 255, 0.05);
            flex-wrap: wrap;
            gap: 10px;
            animation: fadeSlideUp 0.35s ease backwards;
        }

        /* Каждая карточка получает задержку через JS (динамически) */
        .menu-item:nth-child(1) { animation-delay: 0.02s; }
        .menu-item:nth-child(2) { animation-delay: 0.05s; }
        .menu-item:nth-child(3) { animation-delay: 0.08s; }
        .menu-item:nth-child(4) { animation-delay: 0.11s; }
        .menu-item:nth-child(5) { animation-delay: 0.14s; }
        .menu-item:nth-child(6) { animation-delay: 0.17s; }
        .menu-item:nth-child(7) { animation-delay: 0.20s; }
        .menu-item:nth-child(8) { animation-delay: 0.23s; }
        .menu-item:nth-child(9) { animation-delay: 0.26s; }
        .menu-item:nth-child(10) { animation-delay: 0.29s; }

        @keyframes fadeSlideUp {
            from {
                opacity: 0;
                transform: translateY(16px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .menu-item:hover {
            background: rgba(61, 44, 34, 0.9);
            border-color: rgba(194, 130, 75, 0.7);
            transform: translateX(4px) scale(1.01);
            box-shadow: 0 12px 24px rgba(0, 0, 0, 0.4), inset 0 0 0 1px rgba(231, 188, 142, 0.2);
        }

        .item-info {
            flex: 2;
            min-width: 140px;
        }

        .item-name {
            font-weight: 600;
            font-size: 0.96rem;
            color: #f7e9dc;
            letter-spacing: -0.2px;
            word-break: break-word;
        }

        .item-price {
            font-weight: 700;
            font-size: 0.7rem;
            background: linear-gradient(135deg, #f3c693, #e7bc8e);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            padding: 2px 9px;
            display: inline-block;
            margin-top: 5px;
            font-family: monospace;
        }

        /* Анимированные кнопки управления количеством */
        .item-controls {
            display: flex;
            align-items: center;
            gap: 10px;
            background: rgba(36, 26, 20, 0.7);
            padding: 4px 12px;
            border-radius: 60px;
            border: 1px solid #6f4e38;
            backdrop-filter: blur(4px);
        }

        .qty-btn {
            background: #5a3f2e;
            border: none;
            color: #f7e5d2;
            width: 32px;
            height: 32px;
            border-radius: 50px;
            font-size: 1.3rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s cubic-bezier(0.2, 0.9, 0.4, 1.1);
            display: inline-flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 2px 4px rgba(0,0,0,0.3);
        }

        .qty-btn:active {
            transform: scale(0.85);
            background: #e7bc8e;
            color: #2a1f17;
        }

        .qty-num {
            font-weight: 800;
            min-width: 28px;
            text-align: center;
            color: #f3cfaa;
            font-size: 1rem;
        }

        .item-total {
            font-weight: 700;
            font-size: 0.85rem;
            background: rgba(50, 34, 26, 0.7);
            padding: 5px 12px;
            border-radius: 40px;
            color: #f3c693;
            min-width: 75px;
            text-align: center;
            backdrop-filter: blur(2px);
        }

        .drinks-wrap {
            background: rgba(45, 31, 24, 0.5);
            border-radius: 24px;
            padding: 0.2rem;
            border: 1px solid #654930;
        }

        .footer-thin {
            margin-top: 1.5rem;
            text-align: center;
            font-size: 0.65rem;
            color: #be946e;
            border-top: 1px solid rgba(79, 56, 40, 0.6);
            padding-top: 1rem;
            letter-spacing: 0.3px;
        }

        @media (max-width: 560px) {
            .menu-inner {
                padding: 0.8rem;
            }
            .total-amount {
                font-size: 1.4rem;
            }
            .qty-btn {
                width: 28px;
                height: 28px;
                font-size: 1.1rem;
            }
            .item-name {
                font-size: 0.88rem;
            }
            .category-title {
                font-size: 1.25rem;
            }
        }

        ::-webkit-scrollbar {
            width: 0;
            background: transparent;
        }
    </style>
</head>
<body>

<!-- ========== ЭКРАН-ЗАГЛУШКА (preloader) ========== -->
<div id="splashScreen" style="
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: #2a1f17;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 10000;
    transition: opacity 0.4s ease-out;
">
    <div style="text-align: center;">
        <div style="font-family: 'Georgia', serif; font-size: 2rem; color: #e7bc8e; text-shadow: 0 2px 12px black; margin-bottom: 0.5rem;">ГРАВИТАЦИЯ</div>
        <div style="font-size: 0.8rem; color: #c99f72;">загружаем меню...</div>
        <div style="margin-top: 1rem;">
            <svg width="42" height="42" viewBox="0 0 40 40" xmlns="http://www.w3.org/2000/svg">
                <circle cx="20" cy="20" r="15" fill="none" stroke="#c2824b" stroke-width="2.5" stroke-dasharray="80" stroke-linecap="round">
                    <animate attributeName="stroke-dashoffset" dur="1s" repeatCount="indefinite" values="80;0" />
                </circle>
            </svg>
        </div>
    </div>
</div>

<div class="menu-container">
    <div class="cafe-header">
        <div class="mountains-bg">
            <svg viewBox="0 0 1200 200" preserveAspectRatio="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M0,160 L80,100 L160,130 L250,70 L340,110 L430,60 L520,95 L610,40 L700,85 L790,50 L880,90 L970,45 L1060,80 L1150,55 L1200,70 L1200,200 L0,200 Z" fill="#4a3122" opacity="0.7"/>
                <path d="M0,180 L100,120 L200,145 L310,90 L420,125 L520,75 L630,110 L740,65 L850,100 L950,70 L1050,95 L1150,65 L1200,80 L1200,200 L0,200 Z" fill="#603f2a" opacity="0.6"/>
                <path d="M0,195 L60,155 L150,170 L220,135 L320,155 L400,130 L500,148 L600,115 L720,140 L820,110 L920,135 L1020,105 L1120,128 L1200,110 L1200,200 L0,200 Z" fill="#7c5a3e" opacity="0.5"/>
            </svg>
        </div>
        <div class="header-content">
            <div class="cafe-name">ГРАВИТАЦИЯ</div>
            <div class="cafe-slogan">притягиваем вкусом</div>
        </div>
    </div>

    <div class="order-panel">
        <span class="total-label">🍽️ ЗАКАЗ</span>
        <span class="total-amount" id="totalSumDisplay">0 ₽</span>
        <button class="reset-btn" id="resetOrderBtn">Очистить</button>
    </div>

    <div class="menu-inner" id="menuRoot"></div>
    <div class="footer-thin">⋆ нажмите + / − чтобы выбрать порции ⋆</div>
</div>

<script>
    // ---------- МЕНЮ (полное соответствие PDF, удалена лишняя позиция хычины в салатах) ----------
    const menuData = [
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Шорпа", price: 400 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Латман", price: 400 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Манты", price: 400 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Омлет", price: 250 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Шакшука", price: 250 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Яичница", price: 150 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Блины 3 шт с ягодами", price: 230 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Сырники", price: 250 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Каши (в ассортименте)", price: 100 },
        
        { category: "ХЫЧИНЫ БАЛКАРСКИЕ", name: "Хычины с мясом", price: 250 },
        { category: "ХЫЧИНЫ БАЛКАРСКИЕ", name: "Хычины (сыр, зелень)", price: 180 },
        { category: "ХЫЧИНЫ БАЛКАРСКИЕ", name: "Хычины (сыр, картошка)", price: 180 },
        
        { category: "САЛАТЫ И НАРЕЗКИ", name: "Овощи (нарезка)", price: 450 },
        { category: "САЛАТЫ И НАРЕЗКИ", name: "Салат овощной", price: 200 },
        { category: "САЛАТЫ И НАРЕЗКИ", name: "Морковный салат", price: 120 },
        { category: "САЛАТЫ И НАРЕЗКИ", name: "Свекольный салат", price: 150 },
        { category: "САЛАТЫ И НАРЕЗКИ", name: "Греческий салат", price: 350 },
        
        { category: "ЧЕБУРЕКИ", name: "Чебуреки с сыром", price: 200 },
        { category: "ЧЕБУРЕКИ", name: "Чебуреки с мясом", price: 230 },
        
        { category: "ШАШЛЫК · БЛЮДА НА МАНГАЛЕ", name: "Баранина мякоть", price: 1000 },
        { category: "ШАШЛЫК · БЛЮДА НА МАНГАЛЕ", name: "Баранина спинка", price: 900 },
        { category: "ШАШЛЫК · БЛЮДА НА МАНГАЛЕ", name: "Тепятина мякоть", price: 1000 },
        { category: "ШАШЛЫК · БЛЮДА НА МАНГАЛЕ", name: "Куриный шашлык", price: 700 },
        { category: "ШАШЛЫК · БЛЮДА НА МАНГАЛЕ", name: "Жау-баур", price: 400 },
        { category: "ШАШЛЫК · БЛЮДА НА МАНГАЛЕ", name: "Форель порц", price: 800 },
        { category: "ШАШЛЫК · БЛЮДА НА МАНГАЛЕ", name: "Люля", price: 300 },
        { category: "ШАШЛЫК · БЛЮДА НА МАНГАЛЕ", name: "Овощи на мангале", price: 450 },
        { category: "ШАШЛЫК · БЛЮДА НА МАНГАЛЕ", name: "Карп", price: 750 },
        { category: "ШАШЛЫК · БЛЮДА НА МАНГАЛЕ", name: "Грибы на мангале", price: 350 },
        
        { category: "НАПИТКИ", name: "Чай облепиховый 500мл", price: 250 },
        { category: "НАПИТКИ", name: "Чай травяной 500мл", price: 200 },
        { category: "НАПИТКИ", name: "Чай черный", price: 30 },
        { category: "НАПИТКИ", name: "Чай зеленый", price: 30 },
        { category: "НАПИТКИ", name: "Кофе", price: 80 },
        { category: "НАПИТКИ", name: "Лимонад", price: 80 },
        { category: "НАПИТКИ", name: "Айран", price: 50 }
    ];

    let quantities = new Map();

    function getItemKey(category, name) {
        return `${category}::${name}`;
    }

    function updateTotalAndRender() {
        let total = 0;
        for (let item of menuData) {
            const key = getItemKey(item.category, item.name);
            const qty = quantities.get(key) || 0;
            total += qty * item.price;
        }
        const totalDisplay = document.getElementById("totalSumDisplay");
        if (totalDisplay) totalDisplay.innerText = `${total} ₽`;

        for (let item of menuData) {
            const key = getItemKey(item.category, item.name);
            const qty = quantities.get(key) || 0;
            const itemTotal = qty * item.price;
            const safeKey = key.replace(/['"\\]/g, '');
            const qtySpan = document.querySelector(`.qty-num[data-key="${CSS.escape(safeKey)}"]`);
            const totalSpan = document.querySelector(`.item-total-val[data-key="${CSS.escape(safeKey)}"]`);
            if (qtySpan) qtySpan.innerText = qty;
            if (totalSpan) totalSpan.innerText = `${itemTotal} ₽`;
        }
    }

    function changeQuantity(category, name, delta) {
        const key = getItemKey(category, name);
        const current = quantities.get(key) || 0;
        let newQty = current + delta;
        if (newQty < 0) newQty = 0;
        if (newQty === 0) {
            quantities.delete(key);
        } else {
            quantities.set(key, newQty);
        }
        updateTotalAndRender();
    }

    function resetOrder() {
        quantities.clear();
        updateTotalAndRender();
    }

    function renderFullMenu() {
        const menuRoot = document.getElementById("menuRoot");
        if (!menuRoot) return;

        const grouped = new Map();
        for (let item of menuData) {
            if (!grouped.has(item.category)) grouped.set(item.category, []);
            grouped.get(item.category).push(item);
        }

        let html = '';
        for (let [category, items] of grouped.entries()) {
            const isDrinks = (category === "НАПИТКИ");
            html += `<div class="category"><div class="category-title">${escapeHtml(category)}</div>`;
            if (isDrinks) html += `<div class="drinks-wrap">`;
            html += `<div class="items-grid">`;

            for (let idx = 0; idx < items.length; idx++) {
                const item = items[idx];
                const key = getItemKey(category, item.name);
                const currentQty = quantities.get(key) || 0;
                const itemTotal = currentQty * item.price;
                const safeKey = key.replace(/['"\\]/g, '');
                const customDelay = (idx * 0.03).toFixed(2);
                html += `
                    <div class="menu-item" style="animation-delay: ${customDelay}s">
                        <div class="item-info">
                            <div class="item-name">${escapeHtml(item.name)}</div>
                            <div class="item-price">${item.price} ₽ / порция</div>
                        </div>
                        <div class="item-controls">
                            <button class="qty-btn" data-category="${escapeHtml(category)}" data-name="${escapeHtml(item.name)}" data-delta="-1">−</button>
                            <span class="qty-num" data-key="${safeKey}">${currentQty}</span>
                            <button class="qty-btn" data-category="${escapeHtml(category)}" data-name="${escapeHtml(item.name)}" data-delta="+1">+</button>
                        </div>
                        <div class="item-total">
                            <span class="item-total-val" data-key="${safeKey}">${itemTotal} ₽</span>
                        </div>
                    </div>
                `;
            }
            html += `</div>`;
            if (isDrinks) html += `</div>`;
            html += `</div>`;
        }
        menuRoot.innerHTML = html;

        document.querySelectorAll('.qty-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                e.stopPropagation();
                const category = btn.getAttribute('data-category');
                const name = btn.getAttribute('data-name');
                const delta = parseInt(btn.getAttribute('data-delta'), 10);
                if (category && name && !isNaN(delta)) {
                    changeQuantity(category, name, delta);
                }
            });
        });
    }

    function escapeHtml(str) {
        return str.replace(/[&<>]/g, function(m) {
            if (m === '&') return '&amp;';
            if (m === '<') return '&lt;';
            if (m === '>') return '&gt;';
            return m;
        });
    }

    renderFullMenu();
    const resetBtn = document.getElementById("resetOrderBtn");
    if (resetBtn) resetBtn.addEventListener("click", resetOrder);
    updateTotalAndRender();

    window.addEventListener('load', function() {
        const splash = document.getElementById('splashScreen');
        if (splash) {
            splash.style.opacity = '0';
            setTimeout(() => {
                splash.style.display = 'none';
            }, 500);
        }
    });
</script>
</body>
</html>
