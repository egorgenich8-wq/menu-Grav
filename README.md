<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <title>ГРАВИТАЦИЯ кафе | Меню с выбором порций</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #2a1f17;
            font-family: 'Inter', 'Segoe UI', 'Roboto', system-ui, -apple-system, 'Helvetica Neue', sans-serif;
            padding: 1rem;
            color: #f0e3d4;
            overflow-x: hidden;
        }

        .menu-container {
            max-width: 100%;
            width: 100%;
            margin: 0 auto;
            background: #35281e;
            border-radius: 28px;
            box-shadow: 0 30px 50px -15px rgba(0, 0, 0, 0.6), inset 0 1px 0 rgba(255, 255, 255, 0.05);
            overflow: hidden;
            border: 1px solid #5c4332;
        }

        .cafe-header {
            text-align: center;
            padding: 1.5rem 1rem 1rem 1rem;
            border-bottom: 1px solid #5a3f2e;
            background: linear-gradient(135deg, #2f221b 0%, #3a2a1f 100%);
        }

        .cafe-name {
            font-family: 'Georgia', 'Times New Roman', serif;
            font-size: 2.2rem;
            font-weight: 700;
            letter-spacing: 1px;
            color: #e7bc8e;
            text-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
            margin-bottom: 0.3rem;
        }

        .cafe-slogan {
            font-size: 0.8rem;
            color: #c99f72;
            letter-spacing: 0.5px;
            font-weight: 400;
            border-top: 1px dashed #73543b;
            display: inline-block;
            padding-top: 0.4rem;
        }

        .order-panel {
            background: #2d1f18;
            margin: 1rem 1rem 0 1rem;
            padding: 0.8rem 1rem;
            border-radius: 24px;
            border: 1px solid #6a4d36;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 0.8rem;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
        }

        .total-label {
            font-size: 0.85rem;
            font-weight: 500;
            color: #dbb486;
            letter-spacing: 0.3px;
        }

        .total-amount {
            font-size: 1.6rem;
            font-weight: 800;
            color: #f3c693;
            background: #412f23;
            padding: 0.2rem 1rem;
            border-radius: 50px;
            font-family: 'JetBrains Mono', monospace;
            border: 1px solid #c2824b;
        }

        .reset-btn {
            background: #4f3628;
            border: none;
            color: #f0cfaa;
            padding: 0.4rem 1rem;
            border-radius: 40px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            font-size: 0.8rem;
            font-family: inherit;
            border: 1px solid #7e5b40;
        }

        .reset-btn:active {
            transform: scale(0.96);
            background: #684b36;
        }

        .menu-inner {
            padding: 1.2rem 1rem 2rem 1rem;
        }

        .category {
            margin-bottom: 2rem;
        }

        .category-title {
            font-family: 'Georgia', 'Times New Roman', serif;
            font-size: 1.4rem;
            font-weight: 600;
            color: #e7bc8e;
            text-align: center;
            margin-bottom: 1.2rem;
            border-bottom: 1px solid #5a3f2e;
            padding-bottom: 0.4rem;
            width: fit-content;
            margin-left: auto;
            margin-right: auto;
            letter-spacing: -0.2px;
        }

        .items-grid {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .menu-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #2f221b;
            padding: 12px 14px;
            border-radius: 20px;
            border: 1px solid #5a3f2e;
            transition: all 0.2s ease;
            cursor: pointer;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.3);
            flex-wrap: wrap;
            gap: 10px;
        }

        .menu-item:active {
            background: #3d2c22;
            transform: scale(0.99);
        }

        .item-info {
            flex: 2;
            min-width: 130px;
        }

        .item-name {
            font-weight: 600;
            font-size: 0.95rem;
            color: #f7e9dc;
            letter-spacing: -0.2px;
            word-break: break-word;
        }

        .item-price {
            font-weight: 700;
            font-size: 0.75rem;
            color: #f3c693;
            background: #412f23;
            padding: 2px 10px;
            border-radius: 30px;
            display: inline-block;
            margin-top: 5px;
            font-family: monospace;
        }

        .item-controls {
            display: flex;
            align-items: center;
            gap: 8px;
            background: #241a14;
            padding: 4px 10px;
            border-radius: 50px;
            border: 1px solid #6f4e38;
        }

        .qty-btn {
            background: #5a3f2e;
            border: none;
            color: #f7e5d2;
            width: 32px;
            height: 32px;
            border-radius: 40px;
            font-size: 1.3rem;
            font-weight: bold;
            cursor: pointer;
            transition: 0.05s linear;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            -webkit-tap-highlight-color: transparent;
        }

        .qty-btn:active {
            transform: scale(0.92);
            background: #c2824b;
        }

        .qty-num {
            font-weight: 700;
            min-width: 28px;
            text-align: center;
            color: #f3cfaa;
            font-size: 1rem;
        }

        .item-total {
            font-weight: 700;
            font-size: 0.85rem;
            background: #32221a;
            padding: 4px 10px;
            border-radius: 30px;
            color: #e7bc8e;
            min-width: 70px;
            text-align: center;
        }

        .drinks-wrap {
            background: #2d1f18;
            border-radius: 20px;
            padding: 0.2rem 0.1rem 0.1rem 0.1rem;
            border: 1px solid #654930;
        }

        .footer-thin {
            margin-top: 1.5rem;
            text-align: center;
            font-size: 0.65rem;
            color: #be946e;
            border-top: 1px solid #4f3828;
            padding-top: 1rem;
        }

        @media (max-width: 480px) {
            body {
                padding: 0.6rem;
            }
            .cafe-name {
                font-size: 1.8rem;
            }
            .category-title {
                font-size: 1.2rem;
            }
            .menu-item {
                padding: 10px 12px;
            }
            .item-name {
                font-size: 0.9rem;
            }
            .total-amount {
                font-size: 1.3rem;
            }
            .qty-btn {
                width: 28px;
                height: 28px;
                font-size: 1.2rem;
            }
        }
    </style>
</head>
<body>
<div class="menu-container">
    <div class="cafe-header">
        <div class="cafe-name">ГРАВИТАЦИЯ</div>
        <div class="cafe-slogan">притягиваем вкусом</div>
    </div>

    <div class="order-panel">
        <span class="total-label">🍽️ ЗАКАЗ</span>
        <span class="total-amount" id="totalSumDisplay">0 ₽</span>
        <button class="reset-btn" id="resetOrderBtn">Очистить</button>
    </div>

    <div class="menu-inner" id="menuRoot">
        <!-- меню генерируется js -->
    </div>
    <div class="footer-thin">
        ⋆ нажмите + / − чтобы выбрать порции ⋆
    </div>
</div>

<script>
    // ---------- МЕНЮ (удалена лишняя позиция "Хычины (сыр, картошка)" из раздела САЛАТЫ) ----------
    const menuData = [
        // ЗАВТРАКИ / СУПЫ / ГОРЯЧЕЕ
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Шорпа", price: 400 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Латман", price: 400 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Манты", price: 400 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Омлет", price: 250 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Шакшука", price: 250 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Яичница", price: 150 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Блины 3 шт с ягодами", price: 230 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Сырники", price: 250 },
        { category: "ЗАВТРАКИ · СУПЫ · ГОРЯЧИЕ БЛЮДА", name: "Каши (в ассортименте)", price: 100 },
        
        // ХЫЧИНЫ
        { category: "ХЫЧИНЫ БАЛКАРСКИЕ", name: "Хычины с мясом", price: 250 },
        { category: "ХЫЧИНЫ БАЛКАРСКИЕ", name: "Хычины (сыр, зелень)", price: 180 },
        { category: "ХЫЧИНЫ БАЛКАРСКИЕ", name: "Хычины (сыр, картошка)", price: 180 },
        
        // САЛАТЫ (убрана дублирующая позиция "Хычины (сыр, картошка)" — только овощные салаты и нарезки)
        { category: "САЛАТЫ И НАРЕЗКИ", name: "Овощи (нарезка)", price: 450 },
        { category: "САЛАТЫ И НАРЕЗКИ", name: "Салат овощной", price: 200 },
        { category: "САЛАТЫ И НАРЕЗКИ", name: "Морковный салат", price: 120 },
        { category: "САЛАТЫ И НАРЕЗКИ", name: "Свекольный салат", price: 150 },
        { category: "САЛАТЫ И НАРЕЗКИ", name: "Греческий салат", price: 350 },
        
        // ЧЕБУРЕКИ
        { category: "ЧЕБУРЕКИ", name: "Чебуреки с сыром", price: 200 },
        { category: "ЧЕБУРЕКИ", name: "Чебуреки с мясом", price: 230 },
        
        // ШАШЛЫК / МАНГАЛ
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
        
        // НАПИТКИ
        { category: "НАПИТКИ", name: "Чай облепиховый 500мл", price: 250 },
        { category: "НАПИТКИ", name: "Чай травяной 500мл", price: 200 },
        { category: "НАПИТКИ", name: "Чай черный", price: 30 },
        { category: "НАПИТКИ", name: "Чай зеленый", price: 30 },
        { category: "НАПИТКИ", name: "Кофе", price: 80 },
        { category: "НАПИТКИ", name: "Лимонад", price: 80 },
        { category: "НАПИТКИ", name: "Айран", price: 50 }
    ];

    // состояние количества порций
    let quantities = new Map();

    function getItemKey(category, name) {
        return `${category}::${name}`;
    }

    // обновить итоговую сумму и перерисовать цифры у блюд
    function updateTotalAndRender() {
        let total = 0;
        for (let item of menuData) {
            const key = getItemKey(item.category, item.name);
            const qty = quantities.get(key) || 0;
            total += qty * item.price;
        }
        const totalDisplay = document.getElementById("totalSumDisplay");
        if (totalDisplay) totalDisplay.innerText = `${total} ₽`;

        // обновляем каждый блок количества и суммы в DOM
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

            for (let item of items) {
                const key = getItemKey(category, item.name);
                const currentQty = quantities.get(key) || 0;
                const itemTotal = currentQty * item.price;
                const safeKey = key.replace(/['"\\]/g, '');
                html += `
                    <div class="menu-item">
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

        // обработчики для кнопок + / -
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
</script>
</body>
</html>
