<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>哪吒2之魔童闹海 - 拼音配对游戏</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Microsoft YaHei', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #1a2a6c);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            color: #fff;
        }
        
        .container {
            width: 100%;
            max-width: 900px;
            background: rgba(10, 15, 40, 0.85);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.6);
            overflow: hidden;
            padding: 30px;
            position: relative;
            border: 2px solid #ff5722;
        }
        
        .game-header {
            text-align: center;
            margin-bottom: 30px;
            position: relative;
        }
        
        .game-title {
            font-size: 2.8rem;
            color: #ffeb3b;
            text-shadow: 0 0 10px #ff5722, 0 0 20px #ff5722;
            margin-bottom: 10px;
            letter-spacing: 2px;
            font-weight: bold;
            background: linear-gradient(to right, #ff9800, #ffeb3b, #ff9800);
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .ne-zha {
            position: absolute;
            top: 0;
            right: 20px;
            font-size: 3rem;
            color: #ff5722;
            animation: float 3s ease-in-out infinite;
        }
        
        .game-instructions {
            background: rgba(255, 87, 34, 0.2);
            padding: 15px;
            border-radius: 10px;
            margin: 20px 0;
            font-size: 1.1rem;
            line-height: 1.6;
            border: 1px solid #ff5722;
        }
        
        .game-instructions i {
            color: #ffeb3b;
            margin-right: 8px;
        }
        
        .monsters-row {
            display: flex;
            justify-content: space-around;
            margin-bottom: 40px;
            flex-wrap: wrap;
        }
        
        .monster-card {
            background: rgba(25, 35, 70, 0.8);
            border-radius: 15px;
            padding: 15px;
            width: 150px;
            text-align: center;
            margin: 10px;
            border: 2px solid #4a9fe3;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.4);
            transition: transform 0.3s, box-shadow 0.3s;
        }
        
        .monster-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(74, 159, 227, 0.6);
        }
        
        .monster-img {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            background: linear-gradient(45deg, #2c3e50, #4a9fe3);
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 0 auto 15px;
            font-size: 3.5rem;
            color: #fff;
            border: 3px solid #ffeb3b;
        }
        
        .monster-name {
            font-size: 1.4rem;
            color: #ffeb3b;
            font-weight: bold;
            margin-bottom: 15px;
        }
        
        .drop-zone {
            background: rgba(255, 255, 255, 0.1);
            height: 50px;
            border-radius: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.2rem;
            border: 2px dashed #4a9fe3;
            transition: background 0.3s;
        }
        
        .drop-zone.highlight {
            background: rgba(74, 159, 227, 0.3);
            border-color: #ffeb3b;
        }
        
        .pinyin-row {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            margin-bottom: 30px;
        }
        
        .pinyin-item {
            background: linear-gradient(45deg, #ff9800, #ff5722);
            color: white;
            font-size: 1.4rem;
            padding: 15px 25px;
            margin: 10px;
            border-radius: 50px;
            cursor: grab;
            box-shadow: 0 5px 15px rgba(255, 87, 34, 0.4);
            transition: transform 0.2s, box-shadow 0.2s;
            user-select: none;
            font-weight: bold;
        }
        
        .pinyin-item:active {
            cursor: grabbing;
        }
        
        .pinyin-item:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 20px rgba(255, 87, 34, 0.6);
        }
        
        .controls {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 20px;
        }
        
        .btn {
            padding: 14px 35px;
            font-size: 1.2rem;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        
        .submit-btn {
            background: linear-gradient(45deg, #4caf50, #8bc34a);
            color: white;
        }
        
        .reset-btn {
            background: linear-gradient(45deg, #f44336, #ff9800);
            color: white;
        }
        
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.4);
        }
        
        .btn:active {
            transform: translateY(1px);
        }
        
        .result-container {
            text-align: center;
            margin-top: 30px;
            padding: 20px;
            border-radius: 15px;
            background: rgba(0, 0, 0, 0.3);
            display: none;
        }
        
        .score-display {
            font-size: 2.5rem;
            color: #ffeb3b;
            margin: 15px 0;
            font-weight: bold;
            text-shadow: 0 0 10px rgba(255, 235, 59, 0.7);
        }
        
        .message {
            font-size: 1.4rem;
            margin-top: 10px;
        }
        
        .perfect {
            color: #4caf50;
        }
        
        .good {
            color: #ffc107;
        }
        
        .poor {
            color: #f44336;
        }
        
        .fire-effect {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 30px;
            background: linear-gradient(to top, rgba(255, 87, 34, 0.6), transparent);
            z-index: -1;
        }
        
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
            100% { transform: translateY(0px); }
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .pulse {
            animation: pulse 2s infinite;
        }
        
        @media (max-width: 768px) {
            .monsters-row {
                flex-direction: column;
                align-items: center;
            }
            
            .monster-card {
                width: 80%;
                max-width: 250px;
            }
            
            .game-title {
                font-size: 2.2rem;
            }
            
            .ne-zha {
                position: relative;
                right: 0;
                margin-top: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="fire-effect"></div>
        <div class="game-header">
            <h1 class="game-title">哪吒2之魔童闹海</h1>
            <div class="ne-zha">
                <i class="fas fa-fire"></i>
            </div>
        </div>
        
        <div class="game-instructions">
            <p><i class="fas fa-dragon"></i> <strong>游戏规则：</strong>将下方的拼音拖拽到对应的怪兽图片下方。每正确匹配一个得2分，满分10分！</p>
            <p><i class="fas fa-exclamation-circle"></i> 提示：龙 → long, 豹 → bao, 鼠 → shu, 虎 → hu, 牛 → niu</p>
        </div>
        
        <div class="monsters-row" id="monstersRow">
            <!-- 怪兽卡片将由JS动态生成 -->
        </div>
        
        <div class="pinyin-row" id="pinyinRow">
            <!-- 拼音将由JS动态生成 -->
        </div>
        
        <div class="controls">
            <button class="btn submit-btn" id="submitBtn">提交答案</button>
            <button class="btn reset-btn" id="resetBtn">重新开始</button>
        </div>
        
        <div class="result-container" id="resultContainer">
            <h2>游戏得分</h2>
            <div class="score-display" id="scoreDisplay">0分</div>
            <div class="message" id="message"></div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // 游戏数据
            const monsters = [
                { name: '龙', pinyin: 'long', icon: 'dragon' },
                { name: '豹', pinyin: 'bao', icon: 'paw' },
                { name: '鼠', pinyin: 'shu', icon: 'mouse' },
                { name: '虎', pinyin: 'hu', icon: 'paw' },
                { name: '牛', pinyin: 'niu', icon: 'cow' }
            ];
            
            // 打乱数组顺序的函数
            function shuffleArray(array) {
                for (let i = array.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [array[i], array[j]] = [array[j], array[i]];
                }
                return array;
            }
            
            // 生成怪兽卡片
            function createMonsterCards() {
                const monstersRow = document.getElementById('monstersRow');
                monstersRow.innerHTML = '';
                
                // 打乱顺序
                const shuffledMonsters = shuffleArray([...monsters]);
                
                shuffledMonsters.forEach(monster => {
                    const card = document.createElement('div');
                    card.className = 'monster-card';
                    card.dataset.name = monster.name;
                    
                    card.innerHTML = `
                        <div class="monster-img">
                            <i class="fas fa-${monster.icon}"></i>
                        </div>
                        <div class="monster-name">${monster.name}</div>
                        <div class="drop-zone" data-pinyin="${monster.pinyin}"></div>
                    `;
                    
                    monstersRow.appendChild(card);
                });
            }
            
            // 生成拼音元素
            function createPinyinItems() {
                const pinyinRow = document.getElementById('pinyinRow');
                pinyinRow.innerHTML = '';
                
                // 获取所有拼音并打乱顺序
                const allPinyin = monsters.map(m => m.pinyin);
                const shuffledPinyin = shuffleArray([...allPinyin]);
                
                shuffledPinyin.forEach(py => {
                    const pinyinItem = document.createElement('div');
                    pinyinItem.className = 'pinyin-item';
                    pinyinItem.textContent = py;
                    pinyinItem.draggable = true;
                    pinyinItem.dataset.pinyin = py;
                    
                    pinyinItem.addEventListener('dragstart', handleDragStart);
                    
                    pinyinRow.appendChild(pinyinItem);
                });
            }
            
            // 拖拽事件处理
            let draggedItem = null;
            
            function handleDragStart(e) {
                draggedItem = e.target;
                e.dataTransfer.effectAllowed = 'move';
                setTimeout(() => e.target.classList.add('dragging'), 0);
            }
            
            // 放置区域事件处理
            function setupDropZones() {
                const dropZones = document.querySelectorAll('.drop-zone');
                
                dropZones.forEach(zone => {
                    zone.addEventListener('dragover', function(e) {
                        e.preventDefault();
                        this.classList.add('highlight');
                        return false;
                    });
                    
                    zone.addEventListener('dragleave', function() {
                        this.classList.remove('highlight');
                    });
                    
                    zone.addEventListener('drop', function(e) {
                        e.preventDefault();
                        this.classList.remove('highlight');
                        
                        if (draggedItem) {
                            // 移除当前区域已有的拼音
                            while (this.firstChild) {
                                this.removeChild(this.firstChild);
                            }
                            
                            // 添加新拖拽的拼音
                            const clonedItem = draggedItem.cloneNode(true);
                            clonedItem.classList.remove('dragging');
                            clonedItem.draggable = false;
                            clonedItem.style.cursor = 'default';
                            clonedItem.style.boxShadow = 'none';
                            this.appendChild(clonedItem);
                            
                            // 从拼音行移除被拖拽的元素
                            draggedItem.parentNode.removeChild(draggedItem);
                            draggedItem = null;
                        }
                        
                        return false;
                    });
                });
            }
            
            // 提交答案
            function submitAnswers() {
                const dropZones = document.querySelectorAll('.drop-zone');
                let correctCount = 0;
                
                dropZones.forEach(zone => {
                    const correctPinyin = zone.dataset.pinyin;
                    const child = zone.firstChild;
                    
                    if (child && child.dataset.pinyin === correctPinyin) {
                        correctCount++;
                        zone.style.borderColor = '#4CAF50';
                    } else if (child) {
                        zone.style.borderColor = '#F44336';
                    }
                });
                
                const score = correctCount * 2;
                const scoreDisplay = document.getElementById('scoreDisplay');
                const message = document.getElementById('message');
                const resultContainer = document.getElementById('resultContainer');
                
                scoreDisplay.textContent = `${score}分`;
                resultContainer.style.display = 'block';
                
                if (score === 10) {
                    scoreDisplay.classList.add('pulse');
                    message.textContent = '太棒了！哪吒都被你的智慧震惊了！';
                    message.className = 'message perfect';
                } else if (score >= 6) {
                    message.textContent = '干得不错！继续努力！';
                    message.className = 'message good';
                } else {
                    message.textContent = '再接再厉！哪吒相信你可以做得更好！';
                    message.className = 'message poor';
                }
                
                // 滚动到结果区域
                resultContainer.scrollIntoView({ behavior: 'smooth' });
            }
            
            // 重置游戏
            function resetGame() {
                createMonsterCards();
                createPinyinItems();
                setupDropZones();
                
                const resultContainer = document.getElementById('resultContainer');
                resultContainer.style.display = 'none';
                
                const scoreDisplay = document.getElementById('scoreDisplay');
                scoreDisplay.classList.remove('pulse');
            }
            
            // 初始化游戏
            createMonsterCards();
            createPinyinItems();
            setupDropZones();
            
            // 事件监听
            document.getElementById('submitBtn').addEventListener('click', submitAnswers);
            document.getElementById('resetBtn').addEventListener('click', resetGame);
        });
    </script>
</body>
</html>
