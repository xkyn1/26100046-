<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-width=1.0">
    <title>오늘 뭐 먹지? - 결정장애 해결사</title>
    <style>
        body { font-family: 'Malgun Gothic', sans-serif; background-color: #f4f7f6; margin: 0; padding: 20px; display: flex; justify-content: center; }
        .app-container { background-color: white; max-width: 400px; width: 100%; border-radius: 20px; box-shadow: 0 10px 20px rgba(0,0,0,0.1); padding: 30px; text-align: center; }
        h1 { color: #333; font-size: 24px; margin-bottom: 5px; }
        p { color: #777; font-size: 14px; margin-bottom: 25px; }
        .btn-group { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 15px; }
        button { padding: 15px; border: none; border-radius: 12px; font-size: 16px; font-weight: bold; color: white; cursor: pointer; transition: all 0.2s; }
        button:hover { transform: scale(1.05); }
        button:active { transform: scale(0.95); }
        .btn-kr { background-color: #ff6b6b; } .btn-cn { background-color: #feca57; }
        .btn-jp { background-color: #48dbfb; } .btn-us { background-color: #1dd1a1; }
        .btn-all { background-color: #5f27cd; grid-column: span 2; }
        .result-box { margin: 25px 0; padding: 20px; background-color: #fff9e6; border: 2px dashed #feca57; border-radius: 15px; font-size: 22px; font-weight: bold; color: #ff9f43; min-height: 30px; }
        .add-menu-box { margin-top: 30px; padding-top: 20px; border-top: 1px solid #eee; }
        .add-menu-box h3 { font-size: 16px; color: #555; margin-bottom: 10px;}
        select, input { padding: 10px; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 8px; width: calc(100% - 24px); font-size: 14px; }
        .btn-add { background-color: #c8d6e5; color: #222; width: 100%; }
    </style>
</head>
<body>
    <div class="app-container">
        <h1>🍽️ 오늘 뭐 먹지?</h1>
        <p>카테고리를 선택하면 메뉴를 추천해 드려요!</p>
        <div class="btn-group">
            <button class="btn-kr" onclick="pickMenu('한식')">🍚 한식</button>
            <button class="btn-cn" onclick="pickMenu('중식')">🥢 중식</button>
            <button class="btn-jp" onclick="pickMenu('일식')">🍣 일식</button>
            <button class="btn-us" onclick="pickMenu('양식')">🍕 양식</button>
            <button class="btn-all" onclick="pickMenu('전체')">🎲 아무거나 (전체)</button>
        </div>
        <div class="result-box" id="resultText">메뉴를 선택해주세요!</div>
        <div class="add-menu-box">
            <h3>✨ 나만의 메뉴 추가하기</h3>
            <select id="newCat">
                <option value="한식">한식</option><option value="중식">중식</option>
                <option value="일식">일식</option><option value="양식">양식</option>
            </select>
            <input type="text" id="newMenu" placeholder="새로운 메뉴 이름을 입력하세요">
            <button class="btn-add" onclick="addMenu()">➕ 리스트에 추가하기</button>
        </div>
    </div>

    <script>
        let menus = {
            "한식": ["국밥", "제육덮밥", "김치찌개", "비빔밥", "된장찌개"],
            "중식": ["짜장면", "짬뽕", "마라탕", "볶음밥", "탕수육"],
            "일식": ["돈까스", "초밥", "우동", "라멘", "규동"],
            "양식": ["파스타", "햄버거", "피자", "샐러드", "스테이크"]
        };
        let isPicking = false;

        function pickMenu(category) {
            if(isPicking) return;
            const resultBox = document.getElementById('resultText');
            let targetList = category === '전체' ? [].concat(menus["한식"], menus["중식"], menus["일식"], menus["양식"]) : menus[category];
            isPicking = true;
            let count = 0;
            resultBox.style.color = "#777";
            
            let interval = setInterval(() => {
                resultBox.innerText = `고르는 중... ${targetList[Math.floor(Math.random() * targetList.length)]}`;
                count++;
                if (count > 10) {
                    clearInterval(interval);
                    resultBox.innerHTML = `🎉 오늘의 추천: <span style="color:#e15f41;">${targetList[Math.floor(Math.random() * targetList.length)]}</span> 🎉`;
                    resultBox.style.color = "#222";
                    isPicking = false;
                }
            }, 100);
        }

        function addMenu() {
            const cat = document.getElementById('newCat').value;
            const menuInput = document.getElementById('newMenu');
            const menuName = menuInput.value.trim();
            if (menuName === "") { alert("❌ 메뉴 이름을 입력해주세요!"); return; }
            menus[cat].push(menuName);
            alert(`✅ [${cat}] 카테고리에 '${menuName}'이(가) 추가되었습니다!`);
            menuInput.value = "";
        }
    </script>
</body>
</html>
