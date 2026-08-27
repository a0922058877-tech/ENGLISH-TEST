<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>英文單字+文法挑戰 (engine~every & 雙重所有格)</title>
    <style>
        * { box-sizing: border-box; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background-color: #f0f4f8;
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
            border-radius: 20px;
            box-shadow: 0 8px 24px rgba(40, 53, 147, 0.12);
            margin: 0 auto;
        }
        h1 {
            text-align: center;
            color: #283593;
            font-size: 1.18em;
            border-bottom: 2px dashed #c5cae9;
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
            background: #5c6bc0;
            color: white;
            padding: 6px 12px;
            border: none;
            border-radius: 8px;
            font-size: 0.85em;
            cursor: pointer;
            font-weight: bold;
        }
        #q-counter {
            color: #3f51b5;
            font-size: 0.85em;
            font-weight: bold;
        }
        .question {
            font-size: 1.12em;
            font-weight: bold;
            margin-bottom: 16px;
            min-height: 54px;
            color: #1a237e;
            line-height: 1.5;
        }
        .hint-btn {
            background: #ffb300;
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
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .hint-text {
            display: none;
            color: #444444;
            font-size: 0.9em;
            background: #fff8e1;
            padding: 12px;
            border-radius: 8px;
            margin-bottom: 15px;
            border-left: 4px solid #ffb300;
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
            background: #e8eaf6;
            border: 2px solid transparent;
            border-radius: 12px;
            cursor: pointer;
            font-size: 0.98em;
            text-align: left;
            color: #1a237e;
            transition: all 0.2s;
            -webkit-tap-highlight-color: transparent;
        }
        .option:active {
            transform: scale(0.98);
            background: #c5cae9;
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
            background-color: #f8f9fa;
            border-left: 4px solid #283593;
            padding: 14px;
            margin-bottom: 18px;
            border-radius: 8px;
            font-size: 0.9em;
            line-height: 1.6;
        }
        .explanation-box h4 {
            margin: 0 0 8px 0;
            color: #283593;
            font-size: 1.02em;
        }
        .grammar-tip {
            background-color: #ffe0b2;
            border-left: 4px solid #1565c0;
            padding: 10px 12px;
            margin: 10px 0;
            border-radius: 6px;
            color: #0d47a1;
            font-size: 0.9em;
        }
        .vocab-list {
            margin: 8px 0 0 0;
            padding-left: 18px;
            color: #444444;
        }
        .next-btn {
            display: none;
            background: #283593;
            color: white;
            padding: 14px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-size: 1.05em;
            width: 100%;
            font-weight: bold;
            box-shadow: 0 3px 10px rgba(40, 53, 147, 0.3);
        }
        #result {
            display: none;
            padding: 10px 0;
            line-height: 1.6;
        }
        .score-title {
            text-align: center;
            font-size: 1.4em;
            font-weight: bold;
            color: #283593;
            margin-bottom: 15px;
        }
        .review-section {
            margin-top: 20px;
            border-top: 2px dashed #c5cae9;
            padding-top: 15px;
        }
        .review-title {
            font-size: 1.1em;
            font-weight: bold;
            color: #d32f2f;
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
            background: #283593;
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
    <h1>🚀 單字+文法 雙重所有格特訓</h1>
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
            q: "1. [文法大魔王] Snoopy is one of his dogs. = Snoopy is _____.", options: ["a dogs of his", "a dog of him", "a dog of his", "dogs of his"], ans: 2, hint: "史努比是他其中一隻狗。 = 史努比是他的【一隻狗】。",
            exp: "這題是針對課本第 38 頁 Practice G 第 3 題的超級陷阱！a/an 後面的名詞必須是「單數」！所以 a dogs 是錯的，一定要改成 a dog。",
            grammarTip: "雙重所有格公式：a/an/one + 單數名詞 + of + 所有格代名詞 (mine/his/hers/theirs)。記得名詞不能加 s 喔！",
            vocab: ["dog (n.) 狗", "his (pron.) 他的(東西)"]
        },
        { 
            q: "2. My uncle is an _____. He knows a lot about how a car _____ works.", options: ["engine / engineer", "engineer / engine", "English / Englishman", "Englishman / English"], ans: 1, hint: "我叔叔是個【工程師】。他很了解汽車【引擎】是如何運作的。",
            exp: "設計、修理機器的人是「工程師 (engineer)」，機器的動力來源是「引擎 (engine)」。",
            grammarTip: "engine (引擎) 加上 -er 變成 engineer (工程師)。",
            vocab: ["engineer (n.) 工程師", "engine (n.) 引擎", "work (v.) 運作"]
        },
        { 
            q: "3. I put a ticket for the concert inside an _____ and sent it to my sister.", options: ["engine", "entrance", "eraser", "envelope"], ans: 3, hint: "我把演唱會門票裝進一個【信封】裡，然後寄給了我妹妹。",
            exp: "用來裝信件的紙套是「信封 (envelope)」。",
            grammarTip: "",
            vocab: ["envelope (n.) 信封", "ticket (n.) 門票", "send (v.) 寄送"]
        },
        { 
            q: "4. [文法大魔王] She is one of her great teachers. = She is _____.", options: ["a great teachers of her", "a great teacher of her", "a great teacher of hers", "great teachers of hers"], ans: 2, hint: "她是她的一位好老師。 = 她是她的【一位好老師】。",
            exp: "課本第 38 頁 Practice G 第 2 題的陷阱！第一：a 後面的 teacher 不能加 s。第二：of 後面必須接「所有格代名詞 (hers)」，不能只寫 her (受格)。",
            grammarTip: "雙殺陷阱！a 搭配單數名詞 (teacher)；of 後面接所有格代名詞 (hers)！",
            vocab: ["great (adj.) 棒的/偉大的", "teacher (n.) 老師", "hers (pron.) 她的(人事物)"]
        },
        { 
            q: "5. We really _____ed traveling to Tokyo, Japan. It was so much fun!", options: ["entered", "envied", "enjoyed", "equaled"], ans: 2, hint: "我們真的非常【享受】去日本東京旅行。那實在太有趣了！",
            exp: "喜愛、享受做某事的動詞是 enjoy。",
            grammarTip: "enjoy 後面必須接動名詞 (V-ing)，所以是 enjoyed traveling。",
            vocab: ["enjoy (v.) 享受", "travel (v.) 旅行", "fun (n.) 樂趣"]
        },
        { 
            q: "6. Don't worry. We have _____ food and drinks to see us through the long holiday.", options: ["equal", "empty", "entire", "enough"], ans: 3, hint: "別擔心。我們有【足夠的】食物和飲料度過這個長假。",
            exp: "數量或程度滿足需求的「足夠的」是 enough。",
            grammarTip: "enough 可以當形容詞放在名詞前 (enough food)，也可以當副詞放在形容詞後 (rich enough)。",
            vocab: ["enough (adj./adv.) 足夠的", "worry (v.) 擔心", "holiday (n.) 假日"]
        },
        { 
            q: "7. To protect the natural _____ is to protect ourselves and our future.", options: ["entrance", "environment", "envelope", "emotion"], ans: 1, hint: "保護自然【環境】就是保護我們自己和我們的未來。",
            exp: "周遭的自然生態或條件、「環境」是 environment。",
            grammarTip: "",
            vocab: ["environment (n.) 環境", "protect (v.) 保護", "natural (adj.) 自然的"]
        },
        { 
            q: "8. [文法大魔王] Harry Potter is one of their favorite books. = Harry Potter is _____.", options: ["a favorite books of them", "a favorite book of them", "favorite books of theirs", "a favorite book of theirs"], ans: 3, hint: "哈利波特是他們最喜歡的書之一。 = 哈利波特是他們的【一本愛書】。",
            exp: "課本第 38 頁 Practice G 第 4 題的陷阱！第一：a 後面的 book 不能加 s。第二：of 後面必須接「所有格代名詞 (theirs)」，不能用 them (受格)。",
            grammarTip: "完美訂正公式：a favorite book (單數) + of + theirs (所有格代名詞)！",
            vocab: ["favorite (adj.) 最喜愛的", "book (n.) 書", "theirs (pron.) 他們的(東西)"]
        },
        { 
            q: "9. Young people, _____ those who lack skills, have trouble finding jobs.", options: ["even", "ever", "exactly", "especially"], ans: 3, hint: "年輕人，【特別是 / 尤其是】那些缺乏技能的人，找工作有困難。",
            exp: "特別強調某事物的副詞「尤其是、特別是」是 especially。",
            grammarTip: "have trouble + V-ing 意思是「做某事有困難 (have trouble finding)」。",
            vocab: ["especially (adv.) 尤其是", "young (adj.) 年輕的", "lack (v.) 缺乏"]
        },
        { 
            q: "10. An artist has no home in _____ except in Paris.", options: ["Europe", "English", "England", "Eve"], ans: 0, hint: "一位藝術家在【歐洲】沒有家，除了在巴黎。",
            exp: "位於亞洲西邊的大洲「歐洲」是 Europe。歐洲人/歐洲的是 European。",
            grammarTip: "",
            vocab: ["Europe (n.) 歐洲", "artist (n.) 藝術家", "except (prep.) 除了...之外"]
        },
        { 
            q: "11. The 2026 trip will be a big _____ for our family. We are so excited!", options: ["error", "eraser", "event", "entrance"], ans: 2, hint: "2026年的旅行將是我們家的一件大【事件 / 活動】。我們好興奮！",
            exp: "重要的事情或舉辦的活動、「事件、活動」是 event。",
            grammarTip: "social events 指的是「社交活動」。",
            vocab: ["event (n.) 事件/活動", "excited (adj.) 感到興奮的", "family (n.) 家庭"]
        },
        { 
            q: "12. [文法] _____ of my best friends _____ a cute 10-year-old Shiba Inu.", options: ["One / have", "One / has", "Any / has", "All / has"], ans: 1, hint: "我最好的朋友【其中之一】【有】一隻可愛的十歲柴犬。",
            exp: "這題是課本第 38 頁上方 4-4 的重點喔！One of + 複數名詞 (my best friends) 的主詞其實是前面的 One (一個人)！所以動詞要用「單數動詞 (has)」。",
            grammarTip: "One of (其中之一) 真正的主詞是 One！所以動詞一定要配單數的 is 或 has！",
            vocab: ["best friend (n.) 最好的朋友", "Shiba Inu (n.) 柴犬", "cute (adj.) 可愛"]
        },
        { 
            q: "13. It was the happiest day of my _____ life. I won't forget it.", options: ["equal", "entire", "enough", "electric"], ans: 1, hint: "那是我【整個】人生中最快樂的一天。我不會忘記它。",
            exp: "全部的、完整的、「整個的」形容詞是 entire (同義字是 whole)。",
            grammarTip: "my entire life = my whole life (我的一生 / 我整個生命)。",
            vocab: ["entire (adj.) 整個的/全部的", "happiest (adj.) 最快樂的", "forget (v.) 忘記"]
        },
        { 
            q: "14. Excuse me. Can you tell me where the _____ to the movie theater is?", options: ["entrance", "envelope", "engine", "environment"], ans: 0, hint: "不好意思。你能告訴我電影院的【入口】在哪裡嗎？",
            exp: "進入建築物或地點的門口、「入口」是 entrance。",
            grammarTip: "enter (進入) 的名詞就是 entrance (入口)。",
            vocab: ["entrance (n.) 入口", "movie theater (n.) 電影院", "excuse me (phr.) 不好意思"]
        },
        { 
            q: "15. There are several spelling _____s in your paper. You can use an _____ to correct them.", options: ["events / envelope", "errors / eraser", "envies / engine", "equals / entrance"], ans: 1, hint: "你的報告裡有幾個拼字【錯誤】。你可以用【橡皮擦】來改正它們。",
            exp: "不正確的地方、「錯誤」是 error (同義字是 mistake)；擦掉筆跡的文具是 eraser。",
            grammarTip: "",
            vocab: ["error (n.) 錯誤", "eraser (n.) 橡皮擦", "spelling (n.) 拼字"]
        },
        { 
            q: "16. Her beautiful new crochet hat inspires _____ in her friends. They all want one!", options: ["envy", "entrance", "error", "event"], ans: 0, hint: "她那頂美麗的全新鉤織帽子引起了她朋友們的【羨慕 / 嫉妒】。他們都想要一頂！",
            exp: "看到別人有好事而產生的「羨慕、嫉妒」，名詞和動詞都是 envy。",
            grammarTip: "inspire envy 意思是「引起羨慕」。",
            vocab: ["envy (n./v.) 羨慕/嫉妒", "crochet (v./n.) 鉤織", "inspire (v.) 激發/引起"]
        },
        { 
            q: "17. Three plus two _____s five. It's a very easy math problem.", options: ["enters", "enjoys", "equals", "envies"], ans: 2, hint: "三加二【等於】五。這是一個非常簡單的數學問題。",
            exp: "數量上相同、「等於」的動詞是 equal (這裡加上 s 是因為主詞看作單數的算式)；也可以當形容詞「平等的」。",
            grammarTip: "All animals are created equal. (所有動物生而平等)。",
            vocab: ["equal (v./adj.) 等於/平等的", "plus (prep.) 加上", "math problem (n.) 數學問題"]
        },
        { 
            q: "18. People might lose their money, their families, _____ their lives during a war.", options: ["ever", "even", "every", "else"], ans: 1, hint: "在戰爭期間，人們可能會失去金錢、家庭，【甚至】他們的生命。",
            exp: "用來強調令人驚訝或極端情況的副詞「甚至」是 even。",
            grammarTip: "even 也可以用來修飾比較級，even better = 甚至更好。",
            vocab: ["even (adv.) 甚至", "lose (v.) 失去", "war (n.) 戰爭"]
        },
        { 
            q: "19. Please take off your shoes before you _____ the house.", options: ["enjoy", "enter", "envy", "empty"], ans: 1, hint: "在妳【進入】房子之前，請脫掉妳的鞋子。",
            exp: "從外面進到裡面的動詞「進入」是 enter。",
            grammarTip: "enter 是一個及物動詞，後面直接加地點 (enter the house)，不需要加 into 喔！",
            vocab: ["enter (v.) 進入", "take off (phr.) 脫下", "shoe (n.) 鞋子"]
        },
        { 
            q: "20. [文法] _____ the doctors is my father. He works very hard.", options: ["One", "One of", "A one of", "Any"], ans: 1, hint: "這些醫生【其中之一】是我的爸爸。他非常努力工作。",
            exp: "要表達「群體中的其中一個」，必須使用 One of + 限定詞 (the/these/my) + 複數名詞 的句型。",
            grammarTip: "這是課本第 38 頁 Practice F 的重點！One 必須搭配 of 才能接後面的群體 (the doctors)。",
            vocab: ["One of (phr.) ...其中之一", "doctor (n.) 醫生", "hard (adv.) 努力地"]
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
            
            var html = '<div class="score-title">🎉 雙重所有格特訓完成！<br>你的總分：' + score + ' / ' + quizData.length + '<br><span style="font-size: 0.8em; color: #5c6bc0;">(使用了 ' + hintsUsed + ' 次提示)</span></div>';
            
            if (wrongQuestions.length === 0) {
                html += '<div style="text-align: center; background: #e8f5e9; color: #1e4620; padding: 20px; border-radius: 12px; font-weight: bold; margin-top: 15px;">🌟 完美過關！a friend of mine 這種雙重所有格陷阱完全被你破解了！🚀💯</div>';
            } else {
                html += '<div class="review-section">';
                html += '<div class="review-title">📕 你的專屬錯題與文法複習 (' + wrongQuestions.length + ' 題)</div>';
                html += '<div style="font-size:0.85em; color:#666; text-align:center; margin-bottom:12px;">把錯題小卡複習一下，下次遇到 a ... of mine 絕對能秒殺它！</div>';
                
                for (var w = 0; w < wrongQuestions.length; w++) {
                    var item = wrongQuestions[w];
                    var correctOpt = item.options[item.ans];
                    html += '<div class="wrong-card">';
                    html += '<div class="wrong-card-q">' + item.q + '</div>';
                    html += '<div class="wrong-card-ans">✅ 正確答案：' + correctOpt + '</div>';
                    html += '<div class="wrong-card-exp">💡 ' + item.exp + '</div>';
                    if (item.grammarTip) {
                        html += '<div style="color:#1565c0; font-size:0.9em; margin-bottom:6px;"><strong>🧑‍🏫 文法小提醒：</strong>' + item.grammarTip + '</div>';
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
            
            html += '<button class="restart-btn" onclick="location.reload()">🔄 再挑戰一次</button>';
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
            btn.style.background = "#283593";
            btn.style.color = "white";
            feedback.innerHTML = "✅ 答對了！太讚了！🚀";
            feedback.className = "feedback correct";
            score++;
        } else {
            btn.style.background = "#9e9e9e";
            btn.style.color = "white";
            if (options[correctIndex]) {
                options[correctIndex].style.background = "#283593";
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
