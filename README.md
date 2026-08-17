<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>英文單字+文法挑戰 (contract~courage & No other句型)</title>
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
            font-size: 1.15em;
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
    <h1>🌱 單字+No other句型挑戰</h1>
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
            q: "1. [單字陷阱] James works as a _____ in a famous Chinese restaurant.", options: ["cooker", "cookie", "cook", "count"], ans: 2, hint: "詹姆斯在一家有名的中式餐廳擔任【廚師】。",
            exp: "這是一個超級大陷阱！英文的「廚師」是 cook，而不是 cooker。cooker 指的是廚房裡的「爐具/鍋具」喔！",
            grammarTip: "千萬要記住：He is a good cook. (他是一個好廚師)。絕對不能說 He is a good cooker. (他是一個好瓦斯爐)！",
            vocab: ["cook (n./v.) 廚師 / 煮飯", "restaurant (n.) 餐廳", "cooker (n.) 爐具/廚具"]
        },
        { 
            q: "2. [文法] _____ boys in Class 12 are as handsome as Allen.", options: ["Any other", "All the other", "No other", "Some other"], ans: 2, hint: "12班裡【沒有其他】男孩跟Allen一樣帥。 (表示Allen最帥)",
            exp: "這是課本 2-8 的經典句型。要表達「沒有其他人比得上他」，開頭要使用 No other (沒有其他的)。",
            grammarTip: "No other + 名詞 + is/are as + 形容詞原級 + as... = 沒有其他人跟...一樣...",
            vocab: ["No other (phr.) 沒有其他的", "handsome (adj.) 帥氣的", "class (n.) 班級"]
        },
        { 
            q: "3. It _____ a lot of money to buy an apartment in Taipei.", options: ["costs", "spends", "pays", "takes"], ans: 0, hint: "在台北買一間公寓要【花費】很多錢。",
            exp: "主詞是 It (買公寓這件事)，且花費的是「金錢」，所以動詞要用 cost。It costs + 金錢 + to V。",
            grammarTip: "花錢的動詞選法：主詞是人通常用 spend 或 pay；主詞是物品或 It 通常用 cost。",
            vocab: ["cost (v./n.) 花費(金錢) / 成本", "apartment (n.) 公寓", "buy (v.) 買"]
        },
        { 
            q: "4. He had been _____ing all night because he caught a bad cold.", options: ["counting", "coughing", "cooling", "copying"], ans: 1, hint: "他整晚都在【咳嗽】，因為他得了重感冒。",
            exp: "感冒時發出的聲音「咳嗽」，動詞是 cough (讀作 /kɔf/)。",
            grammarTip: "catch a cold 意思是「感冒」；have a bad cough 意思是「咳得很厲害」。",
            vocab: ["cough (v./n.) 咳嗽", "all night (phr.) 整晚", "catch a cold (phr.) 感冒"]
        },
        { 
            q: "5. [文法] No other cities in Taiwan _____ as convenient as Taipei.", options: ["is", "are", "do", "does"], ans: 1, hint: "台灣沒有其他城市【是】跟台北一樣方便的。",
            exp: "No other 後面接了複數名詞 cities，所以 be 動詞必須跟著使用複數的 are。",
            grammarTip: "No other 後面可以接單數或複數名詞。如果是複數 (cities/boys)，be動詞就要用 are 喔！",
            vocab: ["city (n.) 城市(單數)", "cities (n.) 城市(複數)", "convenient (adj.) 方便的"]
        },
        { 
            q: "6. Tom and Mary are considered to be a well-matched _____.", options: ["courage", "country", "couple", "county"], ans: 2, hint: "湯姆和瑪麗被認為是天作之合的【一對 / 情侶】。",
            exp: "一對伴侶、夫妻或情侶，英文是 couple。",
            grammarTip: "a couple of... 也是常見片語，意思是「幾個、兩三個...」。",
            vocab: ["couple (n.) 一對/情侶", "well-matched (adj.) 相配的", "consider (v.) 認為"]
        },
        { 
            q: "7. Young people move to the city, leaving old people to live alone in the _____.", options: ["corner", "countryside", "cotton", "copy"], ans: 1, hint: "年輕人搬到城市，留下老人獨自住在【鄉下】。",
            exp: "遠離城市的農村或「鄉下」是 countryside。",
            grammarTip: "live in the country 和 live in the countryside 都可以表示住在鄉下。",
            vocab: ["countryside (n.) 鄉下", "leave (v.) 留下/離開", "live alone (phr.) 獨居"]
        },
        { 
            q: "8. [文法] No other student is heavier than Jack. = Jack is heavier than _____ student.", options: ["all other", "no other", "any other", "some other"], ans: 2, hint: "沒有其他學生比傑克重。 = 傑克比【任何其他的】學生都重。",
            exp: "把 No other (沒有其他) 的句型轉換成一般比較級時，後面要搭配 than any other + 單數名詞。",
            grammarTip: "這就是 2-8 單元的替換句型！No other is heavier than Jack = Jack is heavier than any other student.",
            vocab: ["heavy (adj.) 重的", "heavier (adj.) 更重的", "any other (phr.) 任何其他的"]
        },
        { 
            q: "9. There is a large TV set in the _____ of the living room.", options: ["corn", "corner", "copy", "count"], ans: 1, hint: "客廳的【角落】有一台大電視機。",
            exp: "房間、街道的「角落、轉角」是 corner。",
            grammarTip: "in the corner (在室內的角落)；on the corner (在街道的轉角)。",
            vocab: ["corner (n.) 角落", "TV set (n.) 電視機", "living room (n.) 客廳"]
        },
        { 
            q: "10. Mr. Lee showed great _____ in the face of terrible difficulties.", options: ["courage", "couple", "county", "country"], ans: 0, hint: "李先生在面對可怕的困難時展現了極大的【勇氣】。",
            exp: "面對危險或困難時不害怕的「勇氣」是 courage (名詞)。形容詞是 courageous。",
            grammarTip: "in the face of... 意思是「在面對...的時候」。",
            vocab: ["courage (n.) 勇氣", "show (v.) 展現", "difficulty (n.) 困難"]
        },
        { 
            q: "11. [文法] No other runner in the world is _____ Louis.", options: ["faster as", "as faster as", "fast than", "as fast as"], ans: 3, hint: "世界上沒有其他跑者跟 Louis 【一樣快】。",
            exp: "No other 搭配 as...as 句型時，中間一定要用「形容詞原級」，所以是 as fast as！絕對不能加 -er 喔！",
            grammarTip: "as...as 中間只能夾「原級」！(as fast as / as tall as / as beautiful as)。",
            vocab: ["runner (n.) 跑者", "fast (adj.) 快的", "in the world (phr.) 世界上"]
        },
        { 
            q: "12. It is against the law to listen in on other people's private _____s.", options: ["controls", "copies", "conversations", "contracts"], ans: 2, hint: "竊聽別人的私人【對話 / 交談】是違法的。",
            exp: "兩個人或多人之間的交談、對話是 conversation。",
            grammarTip: "listen in on... 意思是「偷聽、竊聽...」。",
            vocab: ["conversation (n.) 對話/交談", "against the law (phr.) 違法", "private (adj.) 私人的"]
        },
        { 
            q: "13. The driver suffered a sudden heart attack and lost _____ of the bus.", options: ["count", "cost", "correct", "control"], ans: 3, hint: "司機突然心臟病發，失去了對公車的【控制】。",
            exp: "能夠操縱或管理事物的能力是 control；lose control of... 意思是「失去對...的控制」。",
            grammarTip: "control 也可以當動詞，過去式要重複字尾 l 加上 ed ➔ controlled。",
            vocab: ["control (n./v.) 控制", "suffer (v.) 遭受", "heart attack (n.) 心臟病發"]
        },
        { 
            q: "14. Please check your test paper for spelling mistakes and _____ them.", options: ["correct", "count", "cost", "copy"], ans: 0, hint: "請檢查你的考卷是否有拼字錯誤，並【改正】它們。",
            exp: "correct 當形容詞是「正確的」，當動詞是「批改、改正(錯誤)」。",
            grammarTip: "correct answer (正確答案)；correct the mistakes (改正錯誤)。",
            vocab: ["correct (v./adj.) 改正/正確的", "check (v.) 檢查", "mistake (n.) 錯誤"]
        },
        { 
            q: "15. Tom dropped off to sleep on the _____, leaving the TV on.", options: ["coach", "couch", "corn", "cookie"], ans: 1, hint: "湯姆在【長沙發】上睡著了，電視機還開著。",
            exp: "可以讓好幾個人坐或躺的「長沙發」是 couch (sofa 也可以)。",
            grammarTip: "couch potato 是一個有趣的俚語，指「整天坐在沙發上看電視的人」。",
            vocab: ["couch (n.) 長沙發", "drop off to sleep (phr.) 睡著", "leave (v.) 讓...保持某狀態"]
        },
        { 
            q: "16. Jimmy likes to have a bowl of hot _____ soup for breakfast.", options: ["corn", "cotton", "coin", "cold"], ans: 0, hint: "吉米早餐喜歡喝一碗熱【玉米】湯。",
            exp: "黃色的一粒粒穀物「玉米」是 corn。",
            grammarTip: "",
            vocab: ["corn (n.) 玉米", "soup (n.) 湯", "breakfast (n.) 早餐"]
        },
        { 
            q: "17. [動詞三態陷阱] The car repair _____ me a lot of money yesterday.", options: ["costed", "cost", "costs", "is costing"], ans: 1, hint: "昨天的汽車修理【花了】我很多錢。",
            exp: "因為有 yesterday (昨天)，所以要用過去式。但 cost 的過去式還是 cost！絕對沒有 costed 這個字！",
            grammarTip: "超愛考的動詞三態：cost (現在) ➔ cost (過去) ➔ cost (過去分詞)。三態同行！",
            vocab: ["cost (v.) 花費", "repair (n.) 修理", "yesterday (adv.) 昨天"]
        },
        { 
            q: "18. I _____ed the chickens in the yard and found out that one was missing.", options: ["coughed", "copied", "cooked", "counted"], ans: 3, hint: "我【數了數】院子裡的雞，發現少了一隻。",
            exp: "計算數量、「數數」的動詞是 count。",
            grammarTip: "count to three and then jump 意思是「數到三然後跳」。",
            vocab: ["count (v.) 計算/數數", "yard (n.) 院子", "missing (adj.) 遺失的"]
        },
        { 
            q: "19. It is very _____ to use a microwave oven to heat up food.", options: ["convenient", "correct", "comfortable", "common"], ans: 0, hint: "用微波爐加熱食物非常【方便的】。",
            exp: "省時省力的「方便的、便利的」是 convenient。",
            grammarTip: "convenience store 就是我們常去的「便利商店」。",
            vocab: ["convenient (adj.) 方便的", "microwave oven (n.) 微波爐", "heat up (phr.) 加熱"]
        },
        { 
            q: "20. I made forty _____ of the English article and gave one to each student.", options: ["cookies", "countries", "copies", "couches"], ans: 2, hint: "我印了四十【份 / 影本】這篇英文文章，發給每位學生一人一份。",
            exp: "名詞 copy 指的是「複製品、影本」。因為是四十份，所以去 y 加 ies 變成 copies。",
            grammarTip: "copy 也可以當動詞，意思是「抄寫、複製」(copying important documents)。",
            vocab: ["copy (n./v.) 影本/複製", "article (n.) 文章", "each (adj.) 每一"]
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
                html += '<div style="text-align: center; background: #e8f5e9; color: #1e4620; padding: 20px; border-radius: 12px; font-weight: bold; margin-top: 15px;">🌟 太神啦！全部答對！No other 句型跟 cost 陷阱完全被你破解了！C 開頭單字正式過關！💯</div>';
            } else {
                html += '<div class="review-section">';
                html += '<div class="review-title">📕 你的專屬錯題與文法複習 (' + wrongQuestions.length + ' 題)</div>';
                html += '<div style="font-size:0.85em; color:#666; text-align:center; margin-bottom:12px;">把錯題小卡複習一下，下次遇到 No other 絕對能秒殺它！</div>';
                
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
