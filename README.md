<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>英文單字+文法挑戰 (cabbage~carpet & 比較級副詞)</title>
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
            font-size: 1.22em;
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
    <h1>🌱 單字+比較級副詞挑戰</h1>
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
            q: "1. Chin-chin baked a delicious chocolate _____ for her boyfriend's birthday.", options: ["cabbage", "cake", "candy", "candle"], ans: 1, hint: "芩芩為男朋友的生日烤了一個好吃的巧克力【蛋糕】。",
            exp: "生日慶祝時吃的甜點是「蛋糕 (cake)」。",
            grammarTip: "",
            vocab: ["cake (n.) 蛋糕", "bake (v.) 烘烤", "birthday (n.) 生日"]
        },
        { 
            q: "2. [文法] The BTS concert tickets are _____ more expensive than normal tickets.", options: ["very", "much", "too", "quite"], ans: 1, hint: "BTS 的演唱會門票【比】一般門票貴【得多】。",
            exp: "more expensive 是「比較級」，要用 much, a lot, even, far, a little 來修飾，絕對不能用 very 喔！",
            grammarTip: "複習課本 1-9 單元：very 只能修飾「原級」(very expensive)；比較級前面要用 much (much more expensive)！",
            vocab: ["expensive (adj.) 昂貴的", "concert ticket (n.) 演唱會門票", "normal (adj.) 一般的"]
        },
        { 
            q: "3. We are going to travel to Japan in 2026. Don't forget to bring your _____ to take beautiful photos!", options: ["cable", "calendar", "camera", "cage"], ans: 2, hint: "我們 2026 年要去日本旅行。別忘了帶你的【相機】去拍漂亮的照片！",
            exp: "用來拍照的機器是「照相機 (camera)」。",
            grammarTip: "",
            vocab: ["camera (n.) 照相機", "take photos (phr.) 拍照", "beautiful (adj.) 美麗的"]
        },
        { 
            q: "4. Because of the heavy typhoon, we had to _____ our trip to Osaka.", options: ["call", "cancel", "care", "camp"], ans: 1, hint: "因為強烈颱風的關係，我們不得不【取消】去大阪的行程。",
            exp: "把預定好的計畫或行程「取消」，動詞是 cancel。",
            grammarTip: "cancel 的過去式是 canceled (美式) 或 cancelled (英式)，字尾要加 ed。",
            vocab: ["cancel (v.) 取消", "typhoon (n.) 颱風", "trip (n.) 旅行"]
        },
        { 
            q: "5. [文法] 選出文法與語序【正確】的句子：", options: ["The much camera is more expensive than the cell phone.", "The camera is even more expensive than the cell phone.", "The camera is more expensive much than the cell phone.", "The camera is very more expensive than the cell phone."], ans: 1, hint: "修飾比較級的副詞 (even/much/a lot) 要放在「比較級形容詞」的正前方！",
            exp: "這題針對 Practice J 第 4 題的陷阱：even 必須緊緊貼在 more expensive 的前面，不能放在名詞 camera 前面喔！",
            grammarTip: "修飾語要當小跟班：The camera is [even] [more expensive]... (O)；The [even] camera is... (X)。",
            vocab: ["even (adv.) 甚至更...", "cell phone (n.) 手機", "expensive (adj.) 昂貴的"]
        },
        { 
            q: "6. When there is a big earthquake, you need to stay _____ and not run around.", options: ["careful", "careless", "calm", "brief"], ans: 2, hint: "當發生大地震時，你需要保持【冷靜】，不要到處亂跑。",
            exp: "遇到危險時保持「冷靜的、鎮定的」是 calm；calm down 則是「冷靜下來」。",
            grammarTip: "calm 的 l 不發音喔！讀作 /kɑm/。",
            vocab: ["calm (adj./v.) 冷靜的", "earthquake (n.) 地震", "stay (v.) 保持"]
        },
        { 
            q: "7. Smoking is strictly not allowed on the school _____.", options: ["carpet", "campus", "cabinet", "captain"], ans: 1, hint: "學校【校園】內嚴格禁止抽菸。",
            exp: "學校的「校園、校區」是 campus；on campus 意思是「在校園裡」。",
            grammarTip: "campus (校園) 的介系詞習慣搭配 on (on campus)。",
            vocab: ["campus (n.) 校園", "smoke (v.) 抽菸", "allow (v.) 允許"]
        },
        { 
            q: "8. [文法] _____ meat you eat, _____ you will become.", options: ["The less, the healthy", "The less, the healthier", "Less, healthier", "The less, healthier"], ans: 1, hint: "你吃【越少】的肉，就會變得【越健康】。",
            exp: "這題針對 Practice K 第 5 題的陷阱：「The + 比較級..., the + 比較級...」。less 是 little 的比較級，healthier 是 healthy 的比較級，兩個前面都要有 The！",
            grammarTip: "句型公式：The + 比較級(less) + 主詞 + 動詞, the + 比較級(healthier) + 主詞 + 動詞。",
            vocab: ["less (adj.) 較少的", "healthier (adj.) 較健康的", "meat (n.) 肉類"]
        },
        { 
            q: "9. It was very _____ of you to break the glass cup. Please pay more attention next time.", options: ["careful", "careless", "calm", "brief"], ans: 1, hint: "你打破玻璃杯真是太【粗心的 / 不小心的】了。下次請多加注意。",
            exp: "care (小心) 加上 -less (缺乏...的)，就變成了「粗心的、不小心的 (careless)」。",
            grammarTip: "形容詞字尾 -less 表示「沒有、缺乏」。例如：careless (不小心的)、homeless (無家可歸的)。",
            vocab: ["careless (adj.) 粗心的", "break (v.) 打破", "pay attention (phr.) 注意"]
        },
        { 
            q: "10. My family went _____ in the mountains last weekend and slept in a tent.", options: ["calling", "canceling", "camping", "caring"], ans: 2, hint: "我家人上週末去山裡【露營】，並且睡在帳篷裡。",
            exp: "camp 當名詞是露營地，當動詞是露營；go camping 是「去露營」。",
            grammarTip: "go + V-ing 表示從事某項戶外活動，例如 go camping (去露營)、go swimming (去游泳)。",
            vocab: ["camp (v./n.) 露營", "mountain (n.) 山", "tent (n.) 帳篷"]
        },
        { 
            q: "11. [文法] The weather in Tokyo is _____ colder than the weather in Taipei.", options: ["very", "a lot", "too", "so"], ans: 1, hint: "東京的天氣比台北的天氣冷【得多】。",
            exp: "colder 是比較級，只能用 much, even, a lot, far, a little 來修飾；不能用 very 喔！",
            grammarTip: "a lot colder = much colder (冷得多)。",
            vocab: ["weather (n.) 天氣", "a lot (adv.) 許多/得多", "colder (adj.) 比較冷的"]
        },
        { 
            q: "12. I struck a match and lit the _____, but it was blown out by the wind.", options: ["candy", "cabbage", "candle", "carpet"], ans: 2, hint: "我劃了一根火柴點燃【蠟燭】，但它被風吹熄了。",
            exp: "停電或慶生時點燃的「蠟燭」是 candle。",
            grammarTip: "blow out a candle 意思是「吹熄蠟燭」。",
            vocab: ["candle (n.) 蠟燭", "match (n.) 火柴", "light (v.) 點燃(過去式lit)"]
        },
        { 
            q: "13. I want to lay a soft, warm _____ in my bedroom for the winter.", options: ["carpet", "cabinet", "cable", "cage"], ans: 0, hint: "我想在臥室裡鋪一塊柔軟溫暖的【地毯】好過冬。",
            exp: "鋪在地板上用來裝飾或保暖的「地毯」是 carpet。",
            grammarTip: "car (車子) + pet (寵物) = carpet (地毯)！這是一個很好記的聯想方法喔！",
            vocab: ["carpet (n.) 地毯", "soft (adj.) 柔軟的", "lay (v.) 鋪放"]
        },
        { 
            q: "14. [文法] How do you like your coffee? \"_____, _____.\"", options: ["The stronger, the better", "Stronger, better", "The strong, the good", "The stronger, the good"], ans: 0, hint: "你喜歡怎樣的咖啡？「【越濃，越好】。」",
            exp: "這是課本 Practice K 第 3 題的經典對話：The + 比較級, the + 比較級 (越...越...)。",
            grammarTip: "The stronger (越濃), the better (越好)。兩個逗號前後都要有 The 跟比較級！",
            vocab: ["stronger (adj.) 較濃的/較強的", "better (adj.) 較好的", "coffee (n.) 咖啡"]
        },
        { 
            q: "15. The police _____ was driving fast along the mountain road to catch the bad guy.", options: ["car", "cap", "card", "cage"], ans: 0, hint: "警【車】沿著山路快速行駛以抓住壞人。",
            exp: "警察開的巡邏車就是 police car。",
            grammarTip: "",
            vocab: ["car (n.) 車子", "police (n.) 警察", "catch (v.) 抓住"]
        },
        { 
            q: "16. Mom is cooking dinner. She chopped up some pork and _____ to make dumplings.", options: ["candies", "cabbages", "candles", "calendars"], ans: 1, hint: "媽媽正在煮晚餐。她切碎了一些豬肉和【高麗菜】來包水餃。",
            exp: "一種常見的綠色葉菜類蔬菜「高麗菜 / 甘藍菜」是 cabbage。",
            grammarTip: "",
            vocab: ["cabbage (n.) 高麗菜", "chop up (phr.) 切碎", "dumpling (n.) 水餃"]
        },
        { 
            q: "17. [文法] 選出文法與語序【正確】的句子：", options: ["The weather in New York is much colder than in California.", "The much weather in New York is colder than in California.", "The weather in New York is very colder than in California.", "The weather in New York is colder much than in California."], ans: 0, hint: "修飾比較級的副詞 (much) 要放在「比較級形容詞」的正前方！",
            exp: "這題針對 Practice J 第 5 題的陷阱：much 必須緊緊貼在 colder 的前面，不能放在名詞 weather 前面喔！",
            grammarTip: "The weather is [much] [colder]... (O)；The [much] weather is... (X)。",
            vocab: ["much (adv.) 得多/非常", "California (n.) 加州", "colder (adj.) 比較冷的"]
        },
        { 
            q: "18. After finishing college, Amy started her _____ as an English teacher.", options: ["cancer", "career", "calendar", "cable"], ans: 1, hint: "大學畢業後，艾美開始了她身為英文老師的【職業生涯】。",
            exp: "一個人一生的工作或「職業、事業生涯」是 career。",
            grammarTip: "start one's career as... 意思是「開始擔任...的職業生涯」。",
            vocab: ["career (n.) 職業/生涯", "finish (v.) 完成", "college (n.) 大學"]
        },
        { 
            q: "19. We are going to buy a lot of _____ned food like peaches and meat before the typhoon comes.", options: ["called", "canceled", "canned", "cared"], ans: 2, hint: "在颱風來之前，我們打算買很多【罐裝的】食物，例如水蜜桃和肉類。",
            exp: "can 當名詞是「罐頭」，加了 -ed 變成形容詞 canned，意思是「罐裝的」。",
            grammarTip: "注意 canned 的拼法，母音 + 子音結尾，要重複字尾 n 再加 ed 喔！",
            vocab: ["canned (adj.) 罐裝的", "can (n.) 罐頭", "peach (n.) 水蜜桃"]
        },
        { 
            q: "20. The cute little yellow bird is kept in a bird _____ in the living room.", options: ["cap", "cage", "camp", "card"], ans: 1, hint: "那隻可愛的小黃鳥被養在客廳的鳥【籠】裡。",
            exp: "用來關動物或鳥類的「籠子」是 cage (bird cage = 鳥籠)。",
            grammarTip: "",
            vocab: ["cage (n.) 籠子", "keep (v.) 飼養(被動式為is kept)", "living room (n.) 客廳"]
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
                html += '<div style="text-align: center; background: #e8f5e9; color: #1e4620; padding: 20px; border-radius: 12px; font-weight: bold; margin-top: 15px;">🌟 太厲害了！全部答對，沒有任何錯題！連比較級修飾語的位置都擺得超級完美！💯</div>';
            } else {
                html += '<div class="review-section">';
                html += '<div class="review-title">📕 你的專屬錯題與文法複習 (' + wrongQuestions.length + ' 題)</div>';
                html += '<div style="font-size:0.85em; color:#666; text-align:center; margin-bottom:12px;">把錯題小卡複習一下，下次「even/much」絕對會當個稱職的比較級小跟班！</div>';
                
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
