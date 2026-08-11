<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>英文單字+文法挑戰 (carrot~chapter & 雙重比較級陷阱)</title>
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
            font-size: 1.2em;
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
            font-size: 1.12em;
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
    <h1>🌱 單字+雙重比較級挑戰</h1>
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
            q: "1. The little rabbit likes to eat sweet orange _____s.", options: ["cabbages", "carrots", "candies", "candles"], ans: 1, hint: "小兔子喜歡吃甜甜的橘色【紅蘿蔔】。",
            exp: "橘色、兔子愛吃的蔬菜是「紅蘿蔔 (carrot)」。",
            grammarTip: "",
            vocab: ["carrot (n.) 紅蘿蔔", "rabbit (n.) 兔子", "sweet (adj.) 甜的"]
        },
        { 
            q: "2. I have to go now so that I can _____ the 2:00 train to Taipei.", options: ["carry", "cause", "catch", "camp"], ans: 2, hint: "我現在必須走了，這樣我才能【趕上】兩點往台北的火車。",
            exp: "catch 除了「抓住」，也很常當作「趕上 (公車、火車)」。",
            grammarTip: "catch 的過去式和過去分詞都是 caught，讀作 /kɔt/，要特別記住拼法喔！",
            vocab: ["catch (v.) 趕上/抓住", "train (n.) 火車", "go now (phr.) 現在離開"]
        },
        { 
            q: "3. We always _____ the Dragon Boat Festival by eating rice dumplings.", options: ["celebrate", "cancel", "call", "change"], ans: 0, hint: "我們總是藉由吃粽子來【慶祝】端午節。",
            exp: "遇到節日或生日時，「慶祝」的動詞是 celebrate。",
            grammarTip: "celebrate + 節慶/生日。例如：celebrate my birthday (慶祝我的生日)。",
            vocab: ["celebrate (v.) 慶祝", "Dragon Boat Festival (n.) 端午節", "rice dumpling (n.) 粽子"]
        },
        { 
            q: "4. [文法] The red dress is more _____ than the blue one.", options: ["beautifuler", "beautiful", "more beautiful", "very beautiful"], ans: 1, hint: "紅色洋裝比藍色洋裝【更美麗】。",
            exp: "這題是 Unit 1 Review 第 2 題的大陷阱！句子裡【已經有 more 了】，所以後面只需要放長形容詞的「原級」beautiful，不能再寫 more beautiful 變成雙重比較級喔！",
            grammarTip: "陷阱口訣：看到 more 就別再加 more！(more beautiful ✓ / more more beautiful ❌)",
            vocab: ["beautiful (adj.) 美麗的", "dress (n.) 洋裝", "than (prep.) 比"]
        },
        { 
            q: "5. We stand a good _____ of winning the basketball game today!", options: ["change", "chapter", "center", "chance"], ans: 3, hint: "我們今天很有【機會 / 勝算】贏得這場籃球賽！",
            exp: "stand a good chance 是固定片語，意思是「很有機會、勝算很大」。chance 是機會。",
            grammarTip: "",
            vocab: ["chance (n.) 機會", "win (v.) 贏", "basketball game (n.) 籃球比賽"]
        },
        { 
            q: "6. There was a sudden _____ in the weather, and it started to rain heavily.", options: ["change", "chance", "chalk", "chair"], ans: 0, hint: "天氣突然發生了【改變 / 變化】，然後開始下起大雨。",
            exp: "change 當動詞是改變，當名詞是「變化」或「零錢」。這裡是指天氣的突然變化。",
            grammarTip: "change for a $100 bill 意思是「換一百元的零錢」。",
            vocab: ["change (n./v.) 變化/改變", "sudden (adj.) 突然的", "heavily (adv.) 猛烈地"]
        },
        { 
            q: "7. [文法] Chin-chin's new bicycle is _____ faster than her old one.", options: ["very", "much", "too", "many"], ans: 1, hint: "芩芩的新腳踏車比舊的快【得多】。",
            exp: "faster 是比較級，比較級前面只能用 much, a lot, even, far, a little 來修飾，絕對不能用 very 喔！",
            grammarTip: "very 只能配原級 (very fast)；much 才能配比較級 (much faster)！",
            vocab: ["fast (adj.) 快的", "faster (adj.) 更快的", "bicycle (n.) 腳踏車"]
        },
        { 
            q: "8. I usually eat a bowl of _____ with cold milk in the morning.", options: ["cell", "cent", "cereal", "century"], ans: 2, hint: "我早上通常吃一碗加冷牛奶的【麥片 / 穀物】。",
            exp: "加牛奶吃的早餐「麥片、穀物」是 cereal。",
            grammarTip: "cereal 發音類似 /ˋsɪrɪəl/，不要跟 serial (連續的) 搞混囉！",
            vocab: ["cereal (n.) 麥片", "bowl (n.) 碗", "milk (n.) 牛奶"]
        },
        { 
            q: "9. This famous university was built at the turn of the _____.", options: ["center", "cell", "cereal", "century"], ans: 3, hint: "這所著名的大學建於【世紀】之交 (約一百年前)。",
            exp: "一百年的時間稱為「一世紀 (century)」。",
            grammarTip: "century 的複數要去 y 加 ies ➔ centuries。",
            vocab: ["century (n.) 世紀", "famous (adj.) 著名的", "university (n.) 大學"]
        },
        { 
            q: "10. Children love to watch _____s like Mickey Mouse on TV after school.", options: ["cartoon", "castle", "cash", "case"], ans: 0, hint: "小孩子放學後喜歡在電視上看像米老鼠之類的【卡通】。",
            exp: "動畫片、卡通影片是 cartoon。",
            grammarTip: "Mickey Mouse 是他們最愛的 cartoon characters (卡通人物)。",
            vocab: ["cartoon (n.) 卡通", "watch (v.) 觀看", "after school (phr.) 放學後"]
        },
        { 
            q: "11. [文法] Chin-chin's English is better than _____.", options: ["Kevin", "Kevin is", "Kevin's", "the Kevin"], ans: 2, hint: "芩芩的英文比【Kevin的(英文)】更好。",
            exp: "同類才能做比較！「芩芩的英文」不能跟「Kevin (人)」比，必須跟「Kevin的 (Kevin's)」比。",
            grammarTip: "Kevin's 後面其實省略了 English (Kevin's English)，這是為了避免重複的漂亮寫法！",
            vocab: ["English (n.) 英文", "better (adj.) 更好的", "than (prep.) 比"]
        },
        { 
            q: "12. I am quite _____ that I will pass the math test tomorrow.", options: ["central", "certain", "careful", "calm"], ans: 1, hint: "我相當【確定 / 肯定】我明天會通過數學考試。",
            exp: "對某件事情有把握、「確定的、肯定的」是 certain。",
            grammarTip: "certainly (adv.) 意思是「必定地、當然」，常在對話中用來答應別人 (Certainly!)。",
            vocab: ["certain (adj.) 確定的", "quite (adv.) 相當地", "pass (v.) 通過"]
        },
        { 
            q: "13. Look! There is a beautiful lamp hanging from the _____.", options: ["cell", "ceiling", "center", "castle"], ans: 1, hint: "看！【天花板】上懸掛著一盞美麗的燈。",
            exp: "房間頂部的「天花板」是 ceiling。",
            grammarTip: "hang from the ceiling 意思是「懸掛在天花板上」。",
            vocab: ["ceiling (n.) 天花板", "lamp (n.) 燈", "hang (v.) 懸掛"]
        },
        { 
            q: "14. We'll knock 20% off the price if you pay in _____ instead of a credit card.", options: ["cash", "card", "case", "catch"], ans: 0, hint: "如果你用【現金】而不是信用卡付款，我們會打八折。",
            exp: "紙鈔和硬幣等「現金」是 cash；pay in cash 就是「付現」。",
            grammarTip: "信用卡是 credit card。knock 20% off 是指打八折 (減掉 20%)。",
            vocab: ["cash (n.) 現金", "pay (v.) 付款", "credit card (n.) 信用卡"]
        },
        { 
            q: "15. The baby was crying, so Amy _____ her one-year-old daughter in her arms.", options: ["caught", "caused", "carried", "cared"], ans: 2, hint: "小嬰兒在哭，所以 Amy 把她一歲的女兒【抱】在懷裡。",
            exp: "carry 除了「攜帶、搬運」，也常指「抱著 (小孩)」。",
            grammarTip: "carry 的過去式要去 y 加 ied ➔ carried。",
            vocab: ["carry (v.) 攜帶/抱著", "daughter (n.) 女兒", "in her arms (phr.) 在懷裡"]
        },
        { 
            q: "16. Our guide took us to an old _____ where ghosts were reported to appear.", options: ["cartoon", "castle", "camp", "campus"], ans: 1, hint: "我們的導遊帶我們去了一座據說有鬼魂出現的古老【城堡】。",
            exp: "古代國王或貴族居住的「城堡」是 castle。",
            grammarTip: "castle 的 t 不發音喔！讀作 /ˈkæsəl/。",
            vocab: ["castle (n.) 城堡", "guide (n.) 導遊", "ghost (n.) 鬼魂"]
        },
        { 
            q: "17. I called her on her _____ phone, but it went straight to voice mail.", options: ["cereal", "cent", "center", "cell"], ans: 3, hint: "我打她的【手機】，但直接進入了語音信箱。",
            exp: "cell 除了指細胞 (cancer cells) 或牢房，最常指「手機 (cell phone)」。",
            grammarTip: "",
            vocab: ["cell phone (n.) 手機", "straight (adv.) 直接地", "voice mail (n.) 語音信箱"]
        },
        { 
            q: "18. [文法] This comic book is more _____ than that one.", options: ["interesting", "more interesting", "interestinger", "very interesting"], ans: 0, hint: "這本漫畫書比那一本【更有趣】。",
            exp: "這跟第 4 題一樣是雙重比較級大陷阱！句子前面【已經有 more】了，所以我們只要選原級的 interesting 就好，絕對不能選 more interesting！",
            grammarTip: "陷阱口訣再複習：看到 more 就別再加 more！",
            vocab: ["interesting (adj.) 有趣的", "comic book (n.) 漫畫書", "than (prep.) 比"]
        },
        { 
            q: "19. The doctor said that smoking may _____ lung cancer.", options: ["catch", "carry", "cause", "cancel"], ans: 2, hint: "醫生說抽菸可能【導致 / 引起】肺癌。",
            exp: "引起某事發生的「導致、造成」是 cause。",
            grammarTip: "cause 也可以當名詞，意思是「原因 (the cause of...)」。",
            vocab: ["cause (v.) 導致/引起", "smoking (n.) 抽菸", "cancer (n.) 癌症"]
        },
        { 
            q: "20. The third _____ of this book discusses the history of Taiwan.", options: ["chance", "change", "chair", "chapter"], ans: 3, hint: "這本書的第三【章 / 章節】討論了台灣的歷史。",
            exp: "書本裡的「章節」是 chapter。",
            grammarTip: "",
            vocab: ["chapter (n.) 章節", "discuss (v.) 討論", "history (n.) 歷史"]
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
                html += '<div style="text-align: center; background: #e8f5e9; color: #1e4620; padding: 20px; border-radius: 12px; font-weight: bold; margin-top: 15px;">🌟 太神啦！全部答對！C 開頭單字跟「雙重比較級陷阱」完全被你破解了！💯</div>';
            } else {
                html += '<div class="review-section">';
                html += '<div class="review-title">📕 你的專屬錯題與文法複習 (' + wrongQuestions.length + ' 題)</div>';
                html += '<div style="font-size:0.85em; color:#666; text-align:center; margin-bottom:12px;">把錯題小卡複習一下，下次看到 more 後面一定不會再上當囉！</div>';
                
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
