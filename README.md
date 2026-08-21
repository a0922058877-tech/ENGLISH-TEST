<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>英文單字+文法挑戰 (desert~direct & 副詞比較級)</title>
    <style>
        * { box-sizing: border-box; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background-color: #f4f5f0;
            color: #333333;
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
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.06);
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
            background: #8d6e63;
            color: white;
            padding: 6px 10px;
            border: none;
            border-radius: 6px;
            font-size: 0.8em;
            cursor: pointer;
        }
        #q-counter {
            color: #795548;
            font-size: 0.85em;
            font-weight: bold;
        }
        .question {
            font-size: 1.12em;
            font-weight: bold;
            margin-bottom: 16px;
            min-height: 54px;
            color: #222222;
            line-height: 1.5;
        }
        .hint-btn {
            background: #ffb703;
            color: #333333;
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
            color: #444444;
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
            color: #333333;
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
            color: #444444;
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
            color: #444444;
            margin-bottom: 8px;
            font-size: 0.95em;
        }
        .wrong-card-vocab {
            background: #ffffff;
            border-radius: 6px;
            padding: 8px 8px 8px 24px;
            margin: 0;
            color: #444444;
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
    <h1>🌱 單字+副詞比較級特訓</h1>
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
            q: "1. [單字陷阱] I usually have a piece of sweet cake for _____ after dinner.", options: ["desert", "design", "dessert", "diary"], ans: 2, hint: "我通常在晚飯後吃一塊甜蛋糕當作【甜點】。",
            exp: "這是一個拼字大陷阱！甜點因為太好吃想多吃一點，所以有兩個 s (dessert)。只有一個 s 的是沙漠 (desert)。",
            grammarTip: "記憶口訣：Dessert (甜點) 有兩個 s；Desert (沙漠) 很乾旱，所以只有一個 s！",
            vocab: ["dessert (n.) 甜點", "desert (n.) 沙漠", "dinner (n.) 晚餐"]
        },
        { 
            q: "2. [文法大魔王] I have very little money. The poor man has _____ money than I do.", options: ["littler", "less", "more little", "least"], ans: 1, hint: "我只有很少的錢。那個可憐的男人擁有的錢【比】我【更少】。",
            exp: "這題是妳在課本第 20 頁訂正過的大魔王！little (少) 的比較級是不規則變化，要變成 less。",
            grammarTip: "千萬不要加 -er 變成 littler！little 的比較級是大變身的 less，最高級是 least 喔！",
            vocab: ["little (adj./adv.) 少的", "less (adj./adv.) 更少的", "poor (adj.) 貧窮的/可憐的"]
        },
        { 
            q: "3. Amy's boyfriend asked her to marry him and gave her a beautiful _____ ring.", options: ["diamond", "dinner", "diplomat", "diary"], ans: 0, hint: "艾美的男友向她求婚，並給了她一枚美麗的【鑽石】戒指。",
            exp: "最堅硬的寶石「鑽石」是 diamond。",
            grammarTip: "",
            vocab: ["diamond (n.) 鑽石", "ring (n.) 戒指", "marry (v.) 結婚"]
        },
        { 
            q: "4. [文法] The eagle is flying _____ in the sky. (越飛越高)", options: ["higher and higher", "high and high", "more high and more high", "higher and highest"], ans: 0, hint: "老鷹在天空中飛得【越來越高】。",
            exp: "「越來越...」的句型是「比較級 + and + 比較級」。high 的比較級是 higher。",
            grammarTip: "這是妳在課本第 21 頁 Practice H 的句型喔！比較級 + and + 比較級 ＝ 越來越... (higher and higher)。",
            vocab: ["high (adv./adj.) 高高地", "eagle (n.) 老鷹", "sky (n.) 天空"]
        },
        { 
            q: "5. He is a really _____ student. He studies English for three hours every night.", options: ["difficult", "different", "diligent", "direct"], ans: 2, hint: "他是個非常【勤奮的】學生。他每晚讀英文三個小時。",
            exp: "形容人做事認真、努力不懈的「勤奮的」是 diligent。",
            grammarTip: "",
            vocab: ["diligent (adj.) 勤奮的", "student (n.) 學生", "every night (phr.) 每晚"]
        },
        { 
            q: "6. [文法] Mark studied _____ than before to pass the difficult exam.", options: ["more hard", "harder", "hardly", "more hardly"], ans: 1, hint: "馬克為了通過困難的考試，讀得【比】以前【更努力】。",
            exp: "hard 當副詞意思是「努力地」，它的比較級是直接加 -er 變成 harder。",
            grammarTip: "永遠記住：hardly 是「幾乎不」的意思，不是 hard 的副詞！努力的比較級是 harder！",
            vocab: ["hard (adv.) 努力地", "harder (adv.) 更努力地", "pass (v.) 通過"]
        },
        { 
            q: "7. Long ago, huge _____s like the T-Rex ruled the earth.", options: ["diplomats", "deserts", "dinosaurs", "differences"], ans: 2, hint: "很久以前，像暴龍這樣的巨大【恐龍】統治著地球。",
            exp: "史前爬行動物「恐龍」是 dinosaur。",
            grammarTip: "dinosaur 唸作 /ˈdaɪnəˌsɔr/，是小學生最喜歡的單字之一喔！",
            vocab: ["dinosaur (n.) 恐龍", "huge (adj.) 巨大的", "earth (n.) 地球"]
        },
        { 
            q: "8. I don't know the meaning of this new word. I need to look it up in the _____.", options: ["diary", "dictionary", "dial", "design"], ans: 1, hint: "我不知道這個新單字的意思。我需要在【字典】裡查一下。",
            exp: "用來查單字意思的「字典」是 dictionary。",
            grammarTip: "look it up 是很常用的片語，意思是「(在書或電腦中) 查閱」。",
            vocab: ["dictionary (n.) 字典", "meaning (n.) 意思", "look up (phr.) 查閱"]
        },
        { 
            q: "9. [文法] Sue writes _____ than Lisa. (Lisa 寫字寫得很小心，但 Sue 寫得更小心)", options: ["more carefully", "carefullyer", "carefullier", "much careful"], ans: 0, hint: "Sue 寫字寫得【比】Lisa【更小心】。",
            exp: "carefully 是由形容詞加 -ly 變來的副詞。這類副詞的比較級，必須在前面加 more (more carefully)。",
            grammarTip: "妳在課本第 20 頁寫得很棒喔！字尾是 -ly 的長副詞，比較級都是在前面加 more！",
            vocab: ["carefully (adv.) 小心地", "write (v.) 寫字"]
        },
        { 
            q: "10. Because of the terrible drought, most parts of the land became a dry _____.", options: ["dessert", "desert", "diet", "dinner"], ans: 1, hint: "因為可怕的乾旱，大部分的土地變成了乾燥的【沙漠】。",
            exp: "這題再考一次陷阱！乾燥、有很多沙子的地方是 desert (只有一個 s)。",
            grammarTip: "desert 當名詞是「沙漠」，當動詞是「拋棄 (deserted her)」。",
            vocab: ["desert (n.) 沙漠", "drought (n.) 乾旱", "dry (adj.) 乾燥的"]
        },
        { 
            q: "11. We use a pencil to _____ a picture, and use a computer to _____ a website.", options: ["develop", "determine", "design", "die"], ans: 2, hint: "我們用鉛筆畫圖，並用電腦來【設計】網站。",
            exp: "規劃並畫出事物外觀或運作方式的「設計」，動詞是 design。",
            grammarTip: "design 的 g 是不發音的喔！讀作 /dɪˈzaɪn/。",
            vocab: ["design (v./n.) 設計", "website (n.) 網站", "picture (n.) 圖片"]
        },
        { 
            q: "12. [文法] The little puppy is getting _____ and _____. (越來越大)", options: ["big / big", "bigger / bigger", "more big / more big", "biger / biger"], ans: 1, hint: "小狗變得【越來越大】了。",
            exp: "「越來越...」是比較級 + and + 比較級。big 是短母音加子音，要重複字尾 g 再加 er (bigger)。",
            grammarTip: "重複字尾再加 er！bigger and bigger (越來越大)。",
            vocab: ["puppy (n.) 小狗", "get (v.) 變得", "bigger (adj.) 更大的"]
        },
        { 
            q: "13. There are many _____s between your car and my car. They look nothing alike.", options: ["difficulties", "diets", "diplomats", "differences"], ans: 3, hint: "你的車和我的車之間有許多【不同之處 / 差異】。它們看起來一點也不像。",
            exp: "different (不同的) 的名詞是 difference (差異)。",
            grammarTip: "tell the difference 意思是「分辨出差異」。",
            vocab: ["difference (n.) 差異/不同之處", "between (prep.) 在...之間", "alike (adj.) 相像的"]
        },
        { 
            q: "14. A farmer _____ a dead body out of his field and reported it to the police.", options: ["dug", "digged", "directed", "developed"], ans: 0, hint: "一位農夫在他的田裡【挖出】了一具屍體並向警方報案。",
            exp: "用鏟子或手把土翻開的「挖掘」是 dig。過去式是不規則變化的 dug。",
            grammarTip: "動詞三態必背：dig (現在) ➔ dug (過去) ➔ dug (過去分詞)。",
            vocab: ["dig (v.) 挖掘", "dug (v.) dig的過去式", "field (n.) 田地"]
        },
        { 
            q: "15. [文法] A rabbit runs _____ than a turtle.", options: ["more fast", "fastly", "faster", "fast"], ans: 2, hint: "兔子跑得比烏龜【更快】。",
            exp: "fast 的副詞還是 fast (沒有 fastly)；它的比較級直接加 -er 變成 faster。",
            grammarTip: "fast 的形容詞和副詞同行，比較級直接加 -er (faster)。",
            vocab: ["fast (adv.) 快速地", "faster (adv.) 更快速地", "turtle (n.) 烏龜"]
        },
        { 
            q: "16. Look at these two rings carefully. Can you spot the _____ between them?", options: ["difficulty", "difference", "diet", "dinner"], ans: 1, hint: "仔細看這兩枚戒指。你能看出它們之間的【差異】嗎？",
            exp: "找出不相同的地方，就是找 difference (差異)。",
            grammarTip: "spot the difference 是一個常見的用法，意思是「發現/看出差異 (也就是大家愛玩的大家來找碴)」。",
            vocab: ["difference (n.) 差異", "carefully (adv.) 仔細地", "spot (v.) 發現/看出"]
        },
        { 
            q: "17. A _____ deals with foreign affairs on the international stage.", options: ["dinosaur", "diplomat", "diet", "diamond"], ans: 1, hint: "【外交官】在國際舞台上處理外國事務。",
            exp: "代表國家與其他國家打交道的官員是 diplomat (外交官)。",
            grammarTip: "",
            vocab: ["diplomat (n.) 外交官", "foreign (adj.) 外國的", "affair (n.) 事務"]
        },
        { 
            q: "18. [文法] He is writing his homework _____ and _____ carefully. (越來越小心)", options: ["more / more", "much / much", "careful / careful", "carefully / carefully"], ans: 0, hint: "他寫作業寫得【越來越】小心了。",
            exp: "長副詞 (carefully) 的「越來越...」句型是「more and more + 副詞」(more and more carefully)。",
            grammarTip: "如果是長單字，不用寫兩次 carefully，只要寫 more and more carefully 就可以了！",
            vocab: ["carefully (adv.) 小心地", "more and more (phr.) 越來越", "homework (n.) 作業"]
        },
        { 
            q: "19. Don't _____ the bright light at my eyes. It hurts!", options: ["die", "direct", "develop", "determine"], ans: 1, hint: "不要把那道強光【導向 / 直射】我的眼睛。很痛！",
            exp: "direct 當形容詞是直接的，當動詞是「導向、指引、導演」。",
            grammarTip: "direct a movie 意思是「導演一部電影」；director 就是「導演」。",
            vocab: ["direct (v./adj.) 導向/直接的", "bright light (n.) 強光", "hurt (v.) 疼痛/傷害"]
        },
        { 
            q: "20. The poor cat _____d of hunger in the cold winter. It was very sad.", options: ["dug", "developed", "died", "dialed"], ans: 2, hint: "那隻可憐的貓在寒冬中因飢餓而【死】了。那非常令人難過。",
            exp: "失去生命、「死亡」的動詞是 die；過去式是 died。",
            grammarTip: "die of... 意思是「死於... (如疾病、飢餓)」。(dead 是形容詞，die 是動詞喔！)",
            vocab: ["die (v.) 死亡", "died (v.) die的過去式", "hunger (n.) 飢餓"]
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
            
            var html = '<div class="score-title">🎉 測驗完成！<br>你的總分：' + score + ' / ' + quizData.length + '<br><span style="font-size: 0.8em; color: #795548;">(使用了 ' + hintsUsed + ' 次提示)</span></div>';
            
            if (wrongQuestions.length === 0) {
                html += '<div style="text-align: center; background: #e8f5e9; color: #1e4620; padding: 20px; border-radius: 12px; font-weight: bold; margin-top: 15px;">🌟 太厲害了！全部答對！desert 陷阱跟 less 不規則變化完全考不倒妳！💯</div>';
            } else {
                html += '<div class="review-section">';
                html += '<div class="review-title">📕 你的專屬錯題與文法複習 (' + wrongQuestions.length + ' 題)</div>';
                html += '<div style="font-size:0.85em; color:#666; text-align:center; margin-bottom:12px;">把錯題小卡複習一下，下次遇到 little 變 less 就能秒殺它！</div>';
                
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
            btn.style.background = "#c62828";
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
