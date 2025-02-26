<!DOCTYPE html>
<html dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>הוכחה ש-1+1=2</title>
    <style>
        :root {
            --primary-color: #4361ee;
            --secondary-color: #3a0ca3;
            --accent-color: #f72585;
            --background-color: #f8f9fa;
            --card-color: #ffffff;
            --text-color: #333333;
            --shadow: 0 4px 6px rgba(0, 0, 0, 0.1), 0 1px 3px rgba(0, 0, 0, 0.08);
            --transition: all 0.3s ease;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            text-align: center;
            margin: 0;
            padding: 0;
            background-color: var(--background-color);
            color: var(--text-color);
            line-height: 1.6;
        }
        
        .container {
            max-width: 800px;
            margin: 20px auto;
            background-color: var(--card-color);
            padding: 30px;
            border-radius: 15px;
            box-shadow: var(--shadow);
        }
        
        h1 {
            color: var(--secondary-color);
            margin-bottom: 20px;
            font-size: 2.2rem;
            position: relative;
            padding-bottom: 10px;
        }
        
        h1::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 100px;
            height: 4px;
            background: linear-gradient(90deg, var(--primary-color), var(--accent-color));
            border-radius: 2px;
        }
        
        .demo-area {
            margin: 40px 0;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        
        .counter {
            font-size: 1.5rem;
            margin-bottom: 20px;
            padding: 10px 20px;
            background-color: #f0f0f0;
            border-radius: 50px;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);
        }
        
        .counter span {
            font-weight: bold;
            color: var(--accent-color);
        }
        
        .objects-container {
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 30px 0;
            flex-wrap: wrap;
            gap: 20px;
        }
        
        .group {
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: rgba(67, 97, 238, 0.1);
            border-radius: 15px;
            padding: 20px;
            transition: var(--transition);
        }
        
        .group:hover {
            transform: translateY(-5px);
            box-shadow: var(--shadow);
        }
        
        .apple {
            position: relative;
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, #ff416c, #ff4b2b);
            border-radius: 50%;
            margin: 5px;
            cursor: pointer;
            transition: var(--transition);
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .apple::before {
            content: '';
            position: absolute;
            top: -10px;
            left: 50%;
            width: 8px;
            height: 15px;
            background-color: #5c5c5c;
            border-radius: 10px 10px 0 0;
            transform: translateX(-50%) rotate(-15deg);
        }
        
        .apple::after {
            content: '';
            position: absolute;
            top: 25%;
            right: 25%;
            width: 10px;
            height: 10px;
            background-color: rgba(255, 255, 255, 0.4);
            border-radius: 50%;
        }
        
        .apple:hover {
            transform: scale(1.1);
        }
        
        .apple.clicked {
            box-shadow: 0 0 0 4px rgba(67, 97, 238, 0.5);
        }
        
        .operator, .equals {
            font-size: 2.5rem;
            margin: 0 10px;
            color: var(--secondary-color);
            font-weight: bold;
        }
        
        .result-container {
            display: flex;
            align-items: center;
            justify-content: center;
            min-width: 60px;
            min-height: 60px;
            background-color: var(--secondary-color);
            color: white;
            border-radius: 50%;
            font-size: 2rem;
            font-weight: bold;
            transition: var(--transition);
        }
        
        .button-group {
            display: flex;
            gap: 15px;
            margin-top: 30px;
            flex-wrap: wrap;
            justify-content: center;
        }
        
        button {
            padding: 12px 24px;
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: bold;
            transition: var(--transition);
            box-shadow: var(--shadow);
            min-width: 150px;
        }
        
        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 7px 14px rgba(0, 0, 0, 0.15), 0 3px 6px rgba(0, 0, 0, 0.1);
        }
        
        button:active {
            transform: translateY(1px);
        }
        
        .reset-btn {
            background: linear-gradient(135deg, #e5e5e5, #d0d0d0);
            color: var(--text-color);
        }
        
        .result {
            font-size: 1.5rem;
            margin-top: 30px;
            font-weight: bold;
            padding: 15px 30px;
            background-color: #f0f8ff;
            border-radius: 10px;
            border-left: 5px solid var(--primary-color);
            transition: var(--transition);
            opacity: 0;
            transform: translateY(20px);
        }
        
        .result.show {
            opacity: 1;
            transform: translateY(0);
        }
        
        .explanation {
            margin-top: 40px;
            text-align: right;
            background-color: #f9f9f9;
            padding: 25px;
            border-radius: 15px;
            box-shadow: var(--shadow);
        }
        
        .explanation h3 {
            color: var(--secondary-color);
            margin-bottom: 15px;
            font-size: 1.3rem;
            border-bottom: 2px solid #eee;
            padding-bottom: 8px;
        }
        
        .explanation ul {
            padding-right: 20px;
        }
        
        .explanation li {
            margin-bottom: 8px;
        }
        
        .tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid #ddd;
        }
        
        .tab {
            padding: 10px 20px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            transition: var(--transition);
        }
        
        .tab.active {
            border-bottom: 3px solid var(--primary-color);
            color: var(--primary-color);
            font-weight: bold;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #f0f;
            opacity: 0;
            animation: confetti-fall 3s ease-in-out;
            z-index: 100;
        }
        
        @keyframes confetti-fall {
            0% { transform: translateY(-100px) rotate(0deg); opacity: 1; }
            100% { transform: translateY(500px) rotate(720deg); opacity: 0; }
        }
        
        .visual-proof {
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 30px 0;
            gap: 40px;
            flex-wrap: wrap;
        }
        
        .set {
            border: 2px solid #ddd;
            border-radius: 15px;
            padding: 20px;
            min-width: 150px;
            position: relative;
        }
        
        .set-label {
            position: absolute;
            top: -15px;
            right: 20px;
            background-color: white;
            padding: 5px 10px;
            font-weight: bold;
            color: var(--secondary-color);
        }
        
        @media (max-width: 768px) {
            .container {
                margin: 10px;
                padding: 20px;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            .objects-container {
                flex-direction: column;
            }
            
            .operator, .equals {
                margin: 10px 0;
            }
            
            .explanation {
                padding: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>הוכחה אינטראקטיבית ש-1+1=2</h1>
        
        <div class="tabs">
            <div class="tab active" onclick="switchTab('demo')">הדגמה חזותית</div>
            <div class="tab" onclick="switchTab('set')">תורת הקבוצות</div>
            <div class="tab" onclick="switchTab('formal')">הוכחה פורמלית</div>
        </div>
        
        <div id="demo" class="tab-content active">
            <div class="demo-area">
                <div class="counter">ספירת עצמים: <span id="count">0</span></div>
                
                <div class="objects-container">
                    <div class="group group-1">
                        <div class="apple" onclick="countObject(this)"></div>
                    </div>
                    
                    <div class="operator">+</div>
                    
                    <div class="group group-2">
                        <div class="apple" onclick="countObject(this)"></div>
                    </div>
                    
                    <div class="equals">=</div>
                    
                    <div class="result-container">
                        <div id="result">?</div>
                    </div>
                </div>
                
                <div class="button-group">
                    <button onclick="calculate()">חשב את התוצאה</button>
                    <button class="reset-btn" onclick="reset()">נסה שוב</button>
                </div>
                
                <div class="result" id="calculation-result"></div>
            </div>
        </div>
        
        <div id="set" class="tab-content">
            <h3>הוכחה באמצעות תורת הקבוצות</h3>
            <p>בתורת הקבוצות, ניתן להגדיר את המספרים הטבעיים באמצעות קבוצות:</p>
            
            <div class="visual-proof">
                <div class="set">
                    <div class="set-label">קבוצה A</div>
                    <div class="apple"></div>
                </div>
                
                <div class="operator">∪</div>
                
                <div class="set">
                    <div class="set-label">קבוצה B</div>
                    <div class="apple"></div>
                </div>
                
                <div class="equals">=</div>
                
                <div class="set">
                    <div class="set-label">A ∪ B</div>
                    <div class="apple"></div>
                    <div class="apple"></div>
                </div>
            </div>
            
            <div class="explanation">
                <p>לפי תורת הקבוצות:</p>
                <ul>
                    <li>הגדרת המספר 1 היא קבוצה עם איבר אחד</li>
                    <li>הגדרת המספר 2 היא קבוצה עם שני איברים</li>
                    <li>כאשר אנו מאחדים שתי קבוצות זרות בנות איבר אחד כל אחת, אנו מקבלים קבוצה בת שני איברים</li>
                    <li>לכן, 1 + 1 = 2</li>
                </ul>
            </div>
        </div>
        
        <div id="formal" class="tab-content">
            <h3>הוכחה פורמלית באמצעות אקסיומות פאנו</h3>
            
            <div class="explanation">
                <p>באמצעות אקסיומות פאנו ניתן להוכיח באופן פורמלי ש-1+1=2:</p>
                <ol>
                    <li>נגדיר את המספר 0</li>
                    <li>נגדיר את פונקצית היורש S(n), כך ש-S(n) = n + 1</li>
                    <li>נגדיר את המספר 1 כ-S(0)</li>
                    <li>נגדיר את המספר 2 כ-S(1) או S(S(0))</li>
                    <li>לפי הגדרת החיבור: a + 0 = a</li>
                    <li>לפי הגדרת החיבור: a + S(b) = S(a + b)</li>
                    <li>לכן: 1 + 1 = 1 + S(0) = S(1 + 0) = S(1) = 2</li>
                </ol>
                
                <h3>הוכחה בתחשיב למבדה</h3>
                <p>ניתן להגדיר מספרים באמצעות תחשיב למבדה של Church:</p>
                <ul>
                    <li>0 = λf.λx.x</li>
                    <li>1 = λf.λx.f x</li>
                    <li>2 = λf.λx.f (f x)</li>
                    <li>חיבור: + = λm.λn.λf.λx.m f (n f x)</li>
                    <li>כאשר נחשב 1+1 נקבל: (λm.λn.λf.λx.m f (n f x)) 1 1 = λf.λx.f (f x) = 2</li>
                </ul>
            </div>
        </div>
    </div>

    <script>
        let counted = 0;
        let clickedApples = [];
        
        function countObject(apple) {
            if (!clickedApples.includes(apple)) {
                clickedApples.push(apple);
                counted++;
                document.getElementById('count').textContent = counted;
                
                // Animate the apple and add clicked class
                apple.classList.add('clicked');
                apple.style.transform = 'scale(1.2)';
                setTimeout(() => {
                    apple.style.transform = 'scale(1)';
                }, 200);
            }
        }
        
        function calculate() {
            const result = 1 + 1;
            document.getElementById('result').textContent = result;
            
            const resultElement = document.getElementById('calculation-result');
            const message = counted === 2 ? 
                "נכון מאוד! ספרת 2 עצמים, כך ש-1+1=2" : 
                `ספרת ${counted} עצמים, והחישוב המתמטי 1+1=2`;
            
            resultElement.textContent = message;
            resultElement.classList.add('show');
            
            // Celebrate with confetti if correct
            if (counted === 2) {
                createConfetti();
            }
        }
        
        function reset() {
            counted = 0;
            clickedApples = [];
            document.getElementById('count').textContent = counted;
            document.getElementById('result').textContent = "?";
            
            const resultElement = document.getElementById('calculation-result');
            resultElement.textContent = "";
            resultElement.classList.remove('show');
            
            // Remove clicked class from all apples
            const apples = document.querySelectorAll('.apple');
            apples.forEach(apple => {
                apple.classList.remove('clicked');
            });
        }
        
        function switchTab(tabId) {
            // Hide all tabs
            const tabContents = document.querySelectorAll('.tab-content');
            tabContents.forEach(tab => {
                tab.classList.remove('active');
            });
            
            // Remove active class from tab buttons
            const tabs = document.querySelectorAll('.tab');
            tabs.forEach(tab => {
                tab.classList.remove('active');
            });
            
            // Show selected tab
            document.getElementById(tabId).classList.add('active');
            
            // Add active class to selected tab button
            const activeTab = Array.from(document.querySelectorAll('.tab')).find(
                tab => tab.innerText.includes(tabId === 'demo' ? 'הדגמה' : 
                                             (tabId === 'set' ? 'קבוצות' : 'פורמלית'))
            );
            if (activeTab) {
                activeTab.classList.add('active');
            }
        }
        
        function createConfetti() {
            const colors = ['#f94144', '#f3722c', '#f8961e', '#f9c74f', '#90be6d', '#43aa8b', '#577590'];
            
            for (let i = 0; i < 50; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.width = Math.random() * 10 + 5 + 'px';
                confetti.style.height = Math.random() * 10 + 5 + 'px';
                confetti.style.animationDuration = Math.random() * 2 + 2 + 's';
                document.body.appendChild(confetti);
                
                // Remove confetti after animation
                setTimeout(() => {
                    confetti.remove();
                }, 3000);
            }
        }
    </script>
</body>
</html>
