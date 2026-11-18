<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Colour Mixing Game</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: system-ui, -apple-system, sans-serif;
        }
        body {
            background: linear-gradient(135deg, #e8f0ff, #f7eef8);
            min-height: 100vh;
            padding: 16px;
            max-width: 480px;
            margin: 0 auto;
        }
        .header-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom:16px;
        }
        .stat-box {
            background: #ffffffdd;
            padding: 8px 16px;
            border-radius: 999px;
            font-size:15px;
            font-weight:500;
        }
        .tabs {
            display:flex;
            background:#fff;
            border-radius: 999px;
            padding:4px;
            margin-bottom:20px;
        }
        .tab {
            flex:1;
            text-align:center;
            padding:12px 0;
            border-radius:999px;
            font-size:16px;
        }
        .tab.active {
            background:#ffb833;
            color:#222;
            font-weight:600;
        }
        .mix-area {
            background:#ffffffdd;
            border-radius:24px;
            padding:24px 16px;
            border:2px dashed #dde4f2;
            display:flex;
            gap:12px;
            justify-content:center;
            align-items:center;
            margin-bottom:20px;
        }
        .color-slot {
            width:110px;
            height:110px;
            border-radius:50%;
            background:#eef2fb;
            display:flex;
            flex-direction:column;
            align-items:center;
            justify-content:center;
            color:#99a4b8;
            font-size:14px;
            transition: all 0.2s;
        }
        .color-slot .plus {
            font-size:36px;
            margin-bottom:6px;
        }
        .result-slot {
            width:110px;
            height:110px;
            border-radius:50%;
            background:#eef2fb;
            display:flex;
            flex-direction:column;
            align-items:center;
            justify-content:center;
            color:#99a4b8;
            font-size:14px;
        }
        .btn-row {
            display:flex;
            gap:12px;
            justify-content:center;
            margin-bottom:24px;
        }
        .mix-btn {
            padding:14px 32px;
            border-radius:999px;
            border:none;
            font-size:17px;
            font-weight:600;
            background:#e1e7f5;
            color:#66728c;
            cursor:pointer;
        }
        .mix-btn.active {
            background:#ffb833;
            color:#222;
        }
        .clear-btn {
            padding:14px 24px;
            border-radius:999px;
            border:none;
            background:#fff;
            color:#555;
            font-size:16px;
            cursor:pointer;
        }
        .pick-title {
            display:flex;
            justify-content:space-between;
            padding:0 4px;
            margin-bottom:16px;
            font-size:16px;
            color:#444;
        }
        .color-grid {
            display:grid;
            grid-template-columns: repeat(3, 1fr);
            gap:14px;
        }
        .color-card {
            background:#ffffffdd;
            border-radius:16px;
            padding:16px 8px;
            display:flex;
            flex-direction:column;
            align-items:center;
            gap:8px;
            cursor:pointer;
        }
        .color-dot {
            width:48px;
            height:48px;
            border-radius:50%;
        }
        .en-name {
            font-weight:600;
            color:#2b5cb8;
            font-size:16px;
        }
        .cn-name {
            color:#777;
            font-size:14px;
        }
    </style>
</head>
<body>
    <div class="header-top">
        <div class="stat-box">⭐ STARS 16</div>
        <div class="stat-box">MIXED 6</div>
        <div class="stat-box">LEVEL 1</div>
    </div>
    <div class="tabs">
        <div class="tab active">🧪 Mix Lab</div>
        <div class="tab">🎯 Quiz</div>
        <div class="tab">📖 Colour Chart</div>
    </div>
    <div class="mix-area">
        <div class="color-slot" id="slot1">
            <div class="plus">+</div>
            <div>点颜色选</div>
        </div>
        <span style="font-size:24px;color:#b8c2d6">+</span>
        <div class="color-slot" id="slot2">
            <div class="plus">+</div>
            <div>点颜色选</div>
        </div>
        <span style="font-size:24px;color:#b8c2d6">=</span>
        <div class="result-slot" id="resultSlot">
            <div>结果</div>
        </div>
    </div>
    <div class="btn-row">
        <button class="mix-btn" id="mixBtn">✨ Mix them!</button>
        <button class="clear-btn" id="clearBtn">↺ Clear</button>
    </div>
    <div class="pick-title">
        <span>🎨 Pick your colours — 点一下加进去</span>
        <span id="count">0 / 3</span>
    </div>
    <div class="color-grid">
        <div class="color-card" data-colour="#e63946">
            <div class="color-dot" style="background:#e63946"></div>
            <div class="en-name">Red</div>
            <div class="cn-name">红色</div>
        </div>
        <div class="color-card" data-colour="#facc15">
            <div class="color-dot" style="background:#facc15"></div>
            <div class="en-name">Yellow</div>
            <div class="cn-name">黄色</div>
        </div>
        <div class="color-card" data-colour="#2563eb">
            <div class="color-dot" style="background:#2563eb"></div>
            <div class="en-name">Blue</div>
            <div class="cn-name">蓝色</div>
        </div>
        <div class="color-card" data-colour="#22c55e">
            <div class="color-dot" style="background:#22c55e"></div>
            <div class="en-name">Green</div>
            <div class="cn-name">绿色</div>
        </div>
        <div class="color-card" data-colour="#f97316">
            <div class="color-dot" style="background:#f97316"></div>
            <div class="en-name">Orange</div>
            <div class="cn-name">橙色</div>
        </div>
        <div class="color-card" data-colour="#9333ea">
            <div class="color-dot" style="background:#9333ea"></div>
            <div class="en-name">Purple</div>
            <div class="cn-name">紫色</div>
        </div>
        <div class="color-card" data-colour="#f472b6">
            <div class="color-dot" style="background:#f472b6"></div>
            <div class="en-name">Pink</div>
            <div class="cn-name">粉色</div>
        </div>
        <div class="color-card" data-colour="#92400e">
            <div class="color-dot" style="background:#92400e"></div>
            <div class="en-name">Brown</div>
            <div class="cn-name">棕色</div>
        </div>
        <div class="color-card" data-colour="#94a3b8">
            <div class="color-dot" style="background:#94a3b8"></div>
            <div class="en-name">Grey</div>
            <div class="cn-name">灰色</div>
        </div>
        <div class="color-card" data-colour="#ffffff">
            <div class="color-dot" style="background:#ffffff;border:1px solid #ddd"></div>
            <div class="en-name">White</div>
            <div class="cn-name">白色</div>
        </div>
        <div class="color-card" data-colour="#1f2937">
            <div class="color-dot" style="background:#1f2937"></div>
            <div class="en-name">Black</div>
            <div class="cn-name">黑色</div>
        </div>
    </div>

<script>
    const slot1 = document.getElementById('slot1');
    const slot2 = document.getElementById('slot2');
    const resultSlot = document.getElementById('resultSlot');
    const mixBtn = document.getElementById('mixBtn');
    const clearBtn = document.getElementById('clearBtn');
    const countText = document.getElementById('count');
    const cards = document.querySelectorAll('.color-card');

    let selected = [];
    let slotFocus = 1;

    function updateCount() {
        countText.textContent = `${selected.length} / 3`;
    }
    function resetSlots() {
        slot1.style.background = "#eef2fb";
        slot1.innerHTML = `<div class="plus">+</div><div>点颜色选</div>`;
        slot2.style.background = "#eef2fb";
        slot2.innerHTML = `<div class="plus">+</div><div>点颜色选</div>`;
        resultSlot.style.background = "#eef2fb";
        resultSlot.innerHTML = `<div>结果</div>`;
        selected = [];
        slotFocus = 1;
        updateCount();
        mixBtn.classList.remove('active');
    }
    function hexToRgb(hex) {
        hex = hex.replace('#','');
        const r = parseInt(hex.substring(0,2),16);
        const g = parseInt(hex.substring(2,4),16);
        const b = parseInt(hex.substring(4,6),16);
        return {r,g,b};
    }
    function mixColour(list) {
        let totalR = 0, totalG = 0, totalB = 0;
        list.forEach(hex=>{
            const c = hexToRgb(hex);
            totalR += c.r;
            totalG += c.g;
            totalB += c.b;
        })
        const n = list.length;
        const r = Math.round(totalR / n);
        const g = Math.round(totalG / n);
        const b = Math.round(totalB / n);
        return `rgb(${r},${g},${b})`;
    }

    slot1.onclick = ()=> slotFocus=1;
    slot2.onclick = ()=> slotFocus=2;

    cards.forEach(card=>{
        card.onclick = ()=>{
            if(selected.length >=3) return;
            const col = card.dataset.colour;
            selected.push(col);
            if(slotFocus ===1){
                slot1.style.background = col;
                slot1.innerHTML = '';
                slotFocus=2;
            }else{
                slot2.style.background = col;
                slot2.innerHTML = '';
                slotFocus=1;
            }
            updateCount();
            if(selected.length >=2) mixBtn.classList.add('active');
        }
    })

    mixBtn.onclick = ()=>{
        if(selected.length<2) return;
        const mixedColor = mixColour(selected);
        resultSlot.style.background = mixedColor;
        resultSlot.innerHTML = '';
    }
    clearBtn.onclick = resetSlots;
</script>
</body>
</html>
