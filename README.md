<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>英文單字+文法挑戰 (break~buffet & 比較級than)</title>
    <style>
        * { box-sizing: border-box; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background-color: #f0f3f6;
            color: #2c3e50;
            margin: 0;
            padding: 10px;
            display: flex;
            justify-content: center;
        }
        .container {
            width: 100%;
            max-width: 400px;
            background: #ffffff;
            padding: 20px 16px;
            border-radius: 18px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
            margin: 0 auto;
        }
        h1 {
            text-align: center;
            color: #2e7d32;
            font-size: 1.25em;
            border-bottom: 2px dashed #c8e6c9;
            padding-bottom: 12px;
            margin-top: 5px;
            margin-bottom: 15px;
        }
        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
        }
        .reload-btn {
            background: #78909c;
            color: white;
            padding: 6px 10px;
            border: none;
            border-radius: 6px;
            font-size: 0.8em;
            cursor: pointer;
        }
        #q-counter {
            color: #7f8c8d;
            font-size: 0.85em;
            font-weight: bold;
        }
        .question {
            font-size: 1.15em;
            font-weight: bold;
            margin-bottom: 16px;
            min-height: 54px;
            color: #1a252f;
            line-height: 1.5;
        }
        .hint-btn {
            background: #ffb703;
            color: #2c3e50;
            padding: 10px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-size: 0.9em;
            margin-bottom: 15px;
            font-weight: bold;
            width: 100%;
            text-align: center;
        }
        .hint-text {
            display: none;
            color: #4f5f6f;
            font-size: 0.9em;
            background: #fefae0;
            padding: 12px;
            border-radius: 8px;
            margin-bottom: 15px;
            border-left: 4px solid #fb8500;
            line-height: 1.5;
        }
        .options {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-bottom: 18px;
        }
        .option {
            padding: 14px 16px;
            background: #e8f5e9;
            border: 2px solid transparent;
            border-radius: 12px;
            cursor: pointer;
            font-size: 0.98em;
            text-align: left;
            color: #2c3e50;
            transition: background 0.15s, transform 0.1s;
            -webkit-tap-highlight-color: transparent;
        }
        .option:active {
            transform: scale(0.98);
        }
        .feedback {
            font-weight: bold;
            margin-bottom: 15px;
            display: none;
            padding: 12px;
            border-radius: 10px;
            font-size: 0.95em;
        }
        .correct { color: #155724; background-color: #d4edda; border: 1px solid #c3e6cb; }
        .wrong { color: #721c24; background-color: #f8d7da; border: 1px solid #f5c6cb; }
        
        .explanation-box {
            display: none;
            background-color: #f0fdf4;
            border-left: 4px solid #2e7d32;
            padding: 14px;
            margin-bottom: 18px;
            border-radius: 8px;
            font-size: 0.9em;
            line-height: 1.6;
        }
        .explanation-box h4 {
            margin: 0 0 8px 0;
            color: #2b9348;
            font-size: 1.02em;
        }
        .grammar-tip {
            background-color: #fff3cd;
            border-left: 4px solid #ffc107;
            padding: 10px 12px;
            margin: 10px 0;
            border-radius: 6px;
            color: #664d03;
            font-size: 0.9em;
        }
        .vocab-list {
            margin: 8px 0 0 0;
            padding-left: 18px;
            color: #34495e;
        }
        .next-btn {
            display: none;
            background: #2e7d32;
            color: white;
            padding: 14px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-size: 1.05em;
            width: 100%;
            font-weight: bold;
            box-shadow: 0 3px 10px rgba(46, 125, 50, 0.3);
        }
        #result {
            display: none;
            padding: 10px 0;
            line-height: 1.6;
        }
        .score-title {
            text-align: center;
            font-size: 1.3em;
            font-weight: bold;
            color: #2e7d32;
            margin-bottom: 15px;
        }
        .review-section {
            margin-top: 20px;
            border-top: 2px dashed #c8e6c9;
            padding-top: 15px;
        }
        .review-title {
            font-size: 1.1em;
            font-weight: bold;
            color: #e63946;
            margin-bottom: 12px;
            text-align: center;
        }
        .wrong-card {
            background: #fff5f5;
            border-left: 4px solid #e63946;
            border-radius: 8px;
            padding: 12px;
            margin-bottom: 15px;
            font-size: 0.9em;
        }
        .wrong-card-q {
            font-weight: bold;
            color: #b7094c;
            margin-bottom: 6px;
        }
        .wrong-card-ans {
            color: #2e7d32;
            font-weight: bold;
            margin-bottom: 6px;
        }
        .wrong-card-exp {
            color: #495057;
            margin-bottom: 8px;
            font-size: 0.95em;
        }
        .wrong-card-vocab {
            background: #ffffff;
            border-radius: 6px;
            padding: 8px 8px 8px 24px;
            margin: 0;
            color: #34495e;
            border: 1px solid #ffe3e3;
        }
        .restart-btn {
            background: #2e7d32;
            color: white;
            padding: 12px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-size: 1em;
            width: 100%;
            font-weight: bold;
            margin-top: 15px;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>🌱 單字+比較級文法挑戰</h1>
    <div id="quiz-container">
        <div class="top-bar">
            <button class="reload-btn" onclick="loadQuestion()">🔄 重整</button>
            <div id="q-counter">載入中...</div>
        </div>
        
        <div class="question" id="question-text">如果沒有看到題目，請點擊上方「重整」按鈕。</div>
        
        <button class="hint-btn" onclick="showHint()">👀 點我偷看提示 (只能看 5 次喔！)</button>
        <div class="hint-text" id="hint-text"></div>

        <div class="options" id="options-container"></div>
        <div class="feedback" id="feedback-text"></div>
        
        <div class="explanation-box" id="explanation-box">
            <h4>💡 答案詳解</h4>
            <div id="exp-content"></div>
            <div id="grammar-tip-box" class="grammar-tip" style="display:none;">
                <strong>🧑‍🏫 老師文法小提醒：</strong><br><span id="grammar-tip-content"></span>
            </div>
            <h4 style="margin-top: 12px;">📖 順便記單字</h4>
            <ul class="vocab-list" id="vocab-content"></ul>
        </div>

        <button class="next-btn" id="next-btn" onclick="nextQuestion()">下一題 ➔</button>
    </div>
    
    <div id="result"></div>
</div>

<script>
    var quizData = [
        { 
            q: "1. The _____ sunlight streamed into my room early this morning.", options: ["bright", "brief", "broad", "brown"], ans: 0, hint: "清晨【明亮的】日光照進了我的房間。",
            exp: "bright 當形容詞是「明亮的、鮮豔的、聰明的」意思；a bright idea 指聰明點子。",
            grammarTip: "形容詞原級 bright 比較級為 brighter，最高級為 brightest。",
            vocab: ["bright (adj.) 明亮的/聰明的", "sunlight (n.) 日光", "stream (v.) 流入/照進"]
        },
        { 
            q: "2. [文法] This camera is NT$18,000, and that camera is NT$20,000. This camera is _____ that one.", options: ["cheap than", "cheaper than", "cheaper then", "more cheap than"], ans: 1, hint: "這台相機是18000元，另一台是20000元。這台相機【比】那一台【便宜】。",
            exp: "單音節形容詞 cheap 的比較級要加 -er 變成 cheaper；而「比...」必須用 than (a)，絕對不能用 then (e)！",
            grammarTip: "千萬記得比大小的「比」拼法是 than！then 的意思是「然後/那個時候」，兩個音很像但字不同喔！",
            vocab: ["cheap (adj.) 便宜的", "cheaper (adj.) 更便宜的", "camera (n.) 照相機"]
        },
        { 
            q: "3. I woke up late on Sunday, so I had a quick _____ at 11:00 AM instead of breakfast and lunch.", options: ["brick", "buffet", "brunch", "bucket"], ans: 2, hint: "我星期天睡很晚，所以在早上十點半迅速吃了一頓【早午餐】。",
            exp: "結合 breakfast (早餐) + lunch (午餐) 的詞就是 brunch (早午餐)。",
            grammarTip: "have brunch / breakfast / lunch 前面通常不需要加冠詞 (a/the)，例如: I had brunch at 11.",
            vocab: ["brunch (n.) 早午餐", "wake up late (phr.) 晚起", "instead of (prep.) 取代/而不是"]
        },
        { 
            q: "4. [文法] My father works 10 hours a day, and my mother works 8 hours. My father is _____ my mother.", options: ["busy than", "busier then", "busier than", "more busy than"], ans: 2, hint: "爸爸一天工作10小時，媽媽8小時。爸爸【比】媽媽【忙碌】。",
            exp: "字尾是「子音 + y」的形容詞 (busy)，比較級一定要「去 y 加 ier」變成 busier；同時搭配 than。",
            grammarTip: "形容詞變化規則：busy ➔ busier；pretty ➔ prettier；dirty ➔ dirtier。記得搭配 than 喔！",
            vocab: ["busy (adj.) 忙碌的", "busier (adj.) 更忙碌的", "work (v.) 工作"]
        },
        { 
            q: "5. The manager paid us a _____ visit and had a short talk with everyone.", options: ["bright", "broad", "British", "brief"], ans: 3, hint: "經理短暫拜訪了我們，並跟每個人簡短交談了一會兒。brief 表示【短暫的/簡短的】。",
            exp: "brief 作形容詞意思是「短暫的、簡短的」；a brief talk 意思是簡短的談話。",
            grammarTip: "in brief 是實用片語，意思是「簡而言之 / 總而言之」。",
            vocab: ["brief (adj.) 短暫的/簡短的", "visit (n./v.) 拜訪", "manager (n.) 經理"]
        },
        { 
            q: "6. [文法] The desk is 15 kilos, and the chair is 9 kilos. The desk is _____ the chair.", options: ["heavy than", "heavier then", "heavier than", "more heavy than"], ans: 2, hint: "書桌重 15 公斤，椅子重 9 公斤。書桌【比】椅子【重】。",
            exp: "heavy (重的) 字尾是 y，比較級要「去 y 加 ier」變成 heavier，後面加上 than (比)。",
            grammarTip: "複習課本第30頁：The desk is heavier than the chair. (heavier 不要忘記去 y，而且要寫 than 不是 then喔！)",
            vocab: ["heavy (adj.) 重的", "heavier (adj.) 更重的", "kilo (n.) 公斤"]
        },
        { 
            q: "7. We walked across a wooden _____ over the stream to get to the other side of the park.", options: ["brick", "bridge", "bucket", "brother"], ans: 1, hint: "我們走過溪流上方的一座木【橋】，來到公園的另一邊。",
            exp: "橫跨河流或道路的「橋梁」是 bridge；cross a bridge 意思是過了那座橋。",
            grammarTip: "wooden (木製的) 是由 wood (木頭) 加上 -en 變成的形容詞。",
            vocab: ["bridge (n.) 橋梁", "wooden (adj.) 木製的", "stream (n.) 溪流"]
        },
        { 
            q: "8. [文法] The green CD player is very popular, but the red one is not. The green CD player is _____ the red one.", options: ["more popular than", "popularer than", "more popular then", "popular than"], ans: 0, hint: "綠色CD播放機很受歡迎，紅色的不會。綠色的【比】紅色的【更受歡迎】。",
            exp: "popular 是三個音節的長形容詞，比較級必須在前面加 more (more popular)；比...一樣要配 than。",
            grammarTip: "長字不加 -er！例如：more popular, more expensive, more beautiful, more interesting。",
            vocab: ["popular (adj.) 受歡迎的", "more popular (adj.) 更受歡迎的", "CD player (n.) CD播放機"]
        },
        { 
            q: "9. Please remember to _____ your English textbook and workbook to class tomorrow!", options: ["bring", "brush", "break", "broadcast"], ans: 0, hint: "明天請記得把你的英文課本和習作薄【帶來】教室！",
            exp: "bring 當動詞是「帶來、拿來」，過去式與過去分詞都是 brought (bring, brought, brought)。",
            grammarTip: "bring (帶來這裡) vs take (帶去別處)：bring 往說話者靠近，take 是遠離說話者。",
            vocab: ["bring (v.) 帶來", "remember (v.) 記得", "workbook (n.) 習作薄"]
        },
        { 
            q: "10. [文法] Tiffany is 12 years old, and Tina is 10 years old. Tiffany is _____ Tina.", options: ["older then the", "older than", "more old than", "older then"], ans: 1, hint: "Tiffany 12 歲，Tina 10 歲。Tiffany 【比】 Tina 【年長 / 大】。",
            exp: "old 的比較級是 older；連接比較對象直接用 than Tina 即可，名字前面不需要加 the。",
            grammarTip: "注意課本 Practice E 第2題小圈套：人名 Tina 前面不能加 the！且一定要用 than，不是 then！",
            vocab: ["old (adj.) 年老的/大歲數的", "older (adj.) 年紀更大的", "year old (phr.) ...歲"]
        },
        { 
            q: "11. Remember to _____ your teeth thoroughly after eating breakfast every day.", options: ["bring", "brush", "broad", "break"], ans: 1, hint: "每天吃完早餐後，記得要認真【刷】牙。",
            exp: "brush 可以當動詞「刷清」(brush my shoes / teeth)，也可以當名詞「刷子、牙刷」(a brush)。",
            grammarTip: "brush 的第三人稱單數現在式記得要加 -es (brushes)；過去式則是 brushed。",
            vocab: ["brush (v./n.) 刷 / 刷子", "teeth (n.) 牙齒(複數)", "thoroughly (adv.) 徹底地"]
        },
        { 
            q: "12. [文法-同類比較] 選出文法完全正確的句子：", options: ["Lily's math is better than Mandy.", "Lily's math is better than Mandy's math.", "Lily's math is better then Mandy's.", "Lily's math is gooder than Mandy's math."], ans: 1, hint: "Lily 的數學不能跟 Mandy 「這個人」比，要跟 Mandy 的「數學」比喔！",
            exp: "根據課本 1-6 重點：同類事物才可以相比！Lily's math 要比的是 Mandy's math (或簡寫 Mandy's)；且 good 的比較級是不規則的 better。",
            grammarTip: "錯誤分析：(A) 不能把數學跟人比；(C) then 拼錯了；(D) good 的比較級是 better 不是 gooder！",
            vocab: ["better (adj.) 更好的(good的比較級)", "math (n.) 數學", "correct (adj.) 正確的"]
        },
        { 
            q: "13. He is a very tall man with _____ shoulders, so he looks strong.", options: ["bright", "brief", "broad", "British"], ans: 2, hint: "他是個個子很高、肩膀【寬闊的】男人，所以看起來很強壯。",
            exp: "broad 當形容詞是「寬闊的、廣大的」；broad shoulders 意思是寬肩；窄肩則是 narrow shoulders。",
            grammarTip: "road (道路) 前面加上一個 b，就成了 broad (寬廣的)，可以聯想「寬廣的道路」來記憶喔！",
            vocab: ["broad (adj.) 寬廣的/寬闊的", "shoulder (n.) 肩膀", "strong (adj.) 強壯的"]
        },
        { 
            q: "14. [文法] Kevin's computer games are _____ Ken's computer games.", options: ["more interesting than", "interestinger than", "more interesting then", "interesting than"], ans: 0, hint: "Kevin 的電腦遊戲【比】 Ken 的電腦遊戲【更有趣】。",
            exp: "interesting 是長形容詞，比較級為 more interesting than。這題你在 Practice F 第1題寫得完全正確，太厲害啦！",
            grammarTip: "超級讚！妳已經很熟練「more + 長形容詞 + than」以及「遊戲比遊戲 (同類比)」的精髓囉！",
            vocab: ["interesting (adj.) 有趣的", "more interesting (adj.) 更有趣的", "computer game (n.) 電腦遊戲"]
        },
        { 
            q: "15. We used a plastic _____ filled with soapy water to wash the family car.", options: ["buffet", "brunch", "bucket", "brick"], ans: 2, hint: "我們用一個裝滿肥皂水的塑膠【水桶】來洗家裡的車。",
            exp: "有提把、可以用來裝水或沙子的「水桶 / 桶子」是 bucket (同義字是 pail)。",
            grammarTip: "kick the bucket 是英文裡很有名的諺語，字面是踢水桶，其實指「翹辮子 / 去世」。",
            vocab: ["bucket (n.) 水桶", "plastic (adj.) 塑膠的", "soapy water (n.) 肥皂水"]
        },
        { 
            q: "16. [文法] Those slippers are size 6, and these slippers are size 7. Those slippers _____ these slippers.", options: ["is smaller than", "are smaller than", "are small then", "are smaller then"], ans: 1, hint: "那雙拖鞋是 6 號，這雙是 7 號。那雙拖鞋【比】這雙【較小】。",
            exp: "slippers (拖鞋) 是複數，be 動詞必須用 are；small 的比較級是 smaller；搭配 than。",
            grammarTip: "注意兩點：1. 複數主詞用 are；2. 寫完 smaller 後一定要檢查寫的是 than，不是 then！",
            vocab: ["small (adj.) 小的", "smaller (adj.) 更小的", "slipper (n.) 拖鞋"]
        },
        { 
            q: "17. The hotel restaurant offers a delicious breakfast _____ where you can eat as much as you want.", options: ["buffet", "brick", "bridge", "brush"], ans: 0, hint: "這家飯店餐廳提供美味的早餐【自助餐 / 吃到飽】，想吃多少就吃多少。",
            exp: "自己拿取食物的「自助餐」是 buffet，讀作 /bəˈfeɪ/ (字尾 t 不發音喔！)。",
            grammarTip: "發音小提醒：buffet 作為自助餐時，發音類似「巴費」，字尾的 t 是安靜不發音的喔！",
            vocab: ["buffet (n.) 自助餐", "restaurant (n.) 餐廳", "offer (v.) 提供"]
        },
        { 
            q: "18. The exciting baseball game will be _____ live on the sports channel tonight.", options: ["brought", "broadcast", "brushed", "broken"], ans: 1, hint: "這場刺激的棒球賽今晚將在運動頻道現場【轉播 / 播送】。",
            exp: "廣播或電視「轉播、播放」是 broadcast；特別注意動詞三態同行：broadcast, broadcast, broadcast。",
            grammarTip: "特殊動詞三態：broadcast 的過去式和過去分詞不用加 -ed，維持原形 broadcast 即可！",
            vocab: ["broadcast (v./n.) 轉播/播送", "baseball game (n.) 棒球比賽", "channel (n.) 頻道"]
        },
        { 
            q: "19. The three little pigs built a strong _____ house that the wolf could not blow down.", options: ["brunch", "brief", "brick", "British"], ans: 2, hint: "三隻小豬蓋了一棟大野狼吹不倒的堅固【磚頭】屋。",
            exp: "建築用的「磚塊、磚頭」是 brick；a brick wall 就是磚牆；lay bricks 指砌磚。",
            grammarTip: "brick 當名詞是磚塊，也可直接作形容詞，如 a brick wall (磚牆)、a brick house (磚房)。",
            vocab: ["brick (n.) 磚塊", "wolf (n.) 狼", "blow down (phr.) 吹倒"]
        },
        { 
            q: "20. [文法] The washing machine is very clean, but the refrigerator is dirty. The washing machine is _____ the refrigerator.", options: ["cleaner than", "cleaner then", "clean than", "more clean than"], ans: 0, hint: "洗衣機很乾淨，但冰箱很髒。洗衣機【比】冰箱【乾淨】。",
            exp: "clean 的比較級是 cleaner，後面一定要接比...的 than。",
            grammarTip: "複習第30頁第6題：clean 比較級直接加 -er (cleaner)，千萬別忘記把 e 改為 a 寫成 than 喔！",
            vocab: ["clean (adj.) 乾淨的", "cleaner (adj.) 更乾淨的", "refrigerator (n.) 冰箱"]
        }
    ];

    var currentQ = 0;
    var score = 0;
    var hintsUsed = 0;
    var wrongQuestions = [];

    function loadQuestion() {
        document.getElementById("feedback-text").style.display = "none";
        document.getElementById("explanation-box").style.display = "none";
        document.getElementById("next-btn").style.display = "none";
        document.getElementById("hint-text").style.display = "none";
        document.getElementById("grammar-tip-box").style.display = "none";
        
        if (currentQ >= quizData.length) {
            document.getElementById("quiz-container").style.display = "none";
            var resultDiv = document.getElementById("result");
            resultDiv.style.display = "block";
            
            var html = '<div class="score-title">🎉 測驗完成！<br>你的總分：' + score + ' / ' + quizData.length + '<br><span style="font-size: 0.8em; color: #6c757d;">(使用了 ' + hintsUsed + ' 次提示)</span></div>';
            
            if (wrongQuestions.length === 0) {
                html += '<div style="text-align: center; background: #e8f5e9; color: #1e4620; padding: 20px; border-radius: 12px; font-weight: bold; margin-top: 15px;">🌟 太厲害了！全部答對，沒有任何錯題！連 than 和 then 都分得一清二楚！💯</div>';
            } else {
                html += '<div class="review-section">';
                html += '<div class="review-title">📕 你的專屬錯題與文法複習 (' + wrongQuestions.length + ' 題)</div>';
                html += '<div style="font-size:0.85em; color:#666; text-align:center; margin-bottom:12px;">把錯題小卡看一下，下次 than 跟 -er 絕對不會再錯囉！</div>';
                
                for (var w = 0; w < wrongQuestions.length; w++) {
                    var item = wrongQuestions[w];
                    var correctOpt = item.options[item.ans];
                    html += '<div class="wrong-card">';
                    html += '<div class="wrong-card-q">' + item.q + '</div>';
                    html += '<div class="wrong-card-ans">✅ 正確答案：' + correctOpt + '</div>';
                    html += '<div class="wrong-card-exp">💡 ' + item.exp + '</div>';
                    if (item.grammarTip) {
                        html += '<div style="color:#856404; font-size:0.9em; margin-bottom:6px;"><strong>🧑‍🏫 文法小提醒：</strong>' + item.grammarTip + '</div>';
                    }
                    html += '<ul class="wrong-card-vocab">';
                    for (var v = 0; v < item.vocab.length; v++) {
                        html += '<li>' + item.vocab[v] + '</li>';
                    }
                    html += '</ul>';
                    html += '</div>';
                }
                html += '</div>';
            }
            
            html += '<button class="restart-btn" onclick="location.reload()">🔄 重新挑戰一次</button>';
            resultDiv.innerHTML = html;
            return;
        }

        document.getElementById("q-counter").innerText = "第 " + (currentQ + 1) + " / " + quizData.length + " 題";
        document.getElementById("question-text").innerText = quizData[currentQ].q;
        document.getElementById("hint-text").innerText = quizData[currentQ].hint;

        var optionsDiv = document.getElementById("options-container");
        optionsDiv.innerHTML = "";
        
        for (var i = 0; i < quizData[currentQ].options.length; i++) {
            (function(index){
                var btn = document.createElement("button");
                btn.className = "option";
                btn.innerText = quizData[currentQ].options[index];
                btn.onclick = function() { checkAnswer(index, btn); };
                optionsDiv.appendChild(btn);
            })(i);
        }
    }

    function showHint() {
        if (hintsUsed < 5) {
            document.getElementById("hint-text").style.display = "block";
            hintsUsed++;
            alert("你已經用了 " + hintsUsed + " 次提示，剩下 " + (5 - hintsUsed) + " 次喔！");
        } else {
            alert("❌ 你的 5 次提示額度已經用完囉！請試著自己挑戰看看！");
        }
    }

    function checkAnswer(selectedIndex, btn) {
        var currentData = quizData[currentQ];
        var correctIndex = currentData.ans;
        var feedback = document.getElementById("feedback-text");
        var options = document.getElementsByClassName("option");
        
        for (var i = 0; i < options.length; i++) {
            options[i].disabled = true;
        }

        if (selectedIndex === correctIndex) {
            btn.style.background = "#2e7d32";
            btn.style.color = "white";
            feedback.innerHTML = "✅ 答對了！太讚了！";
            feedback.className = "feedback correct";
            score++;
        } else {
            btn.style.background = "#e63946";
            btn.style.color = "white";
            if (options[correctIndex]) {
                options[correctIndex].style.background = "#2e7d32";
                options[correctIndex].style.color = "white";
            }
            feedback.innerHTML = "❌ 答錯囉！正確答案是 " + currentData.options[correctIndex] + "。";
            feedback.className = "feedback wrong";
            wrongQuestions.push(currentData);
        }
        
        document.getElementById("exp-content").innerText = currentData.exp;
        
        if (currentData.grammarTip) {
            document.getElementById("grammar-tip-content").innerText = currentData.grammarTip;
            document.getElementById("grammar-tip-box").style.display = "block";
        }
        
        var vocabList = document.getElementById("vocab-content");
        vocabList.innerHTML = "";
        for (var j = 0; j < currentData.vocab.length; j++) {
            var li = document.createElement("li");
            li.innerText = currentData.vocab[j];
            vocabList.appendChild(li);
        }

        document.getElementById("explanation-box").style.display = "block";
        feedback.style.display = "block";
        document.getElementById("next-btn").style.display = "block";
    }

    function nextQuestion() {
        currentQ++;
        loadQuestion();
    }

    window.onload = function() {
        loadQuestion();
    };
</script>

</body>
</html>
