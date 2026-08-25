<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>英文單字+文法挑戰 (柔萱生日派對版 🎂)</title>
    <style>
        * { box-sizing: border-box; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background-color: #fff0f5; /* 派對粉色背景 */
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
            border-radius: 24px;
            box-shadow: 0 8px 25px rgba(233, 30, 99, 0.15);
            margin: 0 auto;
            border: 2px solid #fce4ec;
        }
        h1 {
            text-align: center;
            color: #c2185b;
            font-size: 1.15em;
            border-bottom: 2px dashed #f8bbd0;
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
            background: #f06292;
            color: white;
            padding: 6px 12px;
            border: none;
            border-radius: 8px;
            font-size: 0.85em;
            cursor: pointer;
            font-weight: bold;
        }
        #q-counter {
            color: #ad1457;
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
            border-left: 4px solid #ffc107;
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
            background: #fce4ec;
            border: 2px solid transparent;
            border-radius: 12px;
            cursor: pointer;
            font-size: 0.98em;
            text-align: left;
            color: #333333;
            transition: all 0.2s;
            -webkit-tap-highlight-color: transparent;
        }
        .option:active {
            transform: scale(0.98);
            background: #f8bbd0;
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
            background-color: #fcf3f6;
            border-left: 4px solid #d81b60;
            padding: 14px;
            margin-bottom: 18px;
            border-radius: 8px;
            font-size: 0.9em;
            line-height: 1.6;
        }
        .explanation-box h4 {
            margin: 0 0 8px 0;
            color: #ad1457;
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
            background: #d81b60;
            color: white;
            padding: 14px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-size: 1.05em;
            width: 100%;
            font-weight: bold;
            box-shadow: 0 3px 10px rgba(216, 27, 96, 0.3);
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
            color: #d81b60;
            margin-bottom: 15px;
        }
        .review-section {
            margin-top: 20px;
            border-top: 2px dashed #f8bbd0;
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
            background: #d81b60;
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
    <h1>🎈 柔萱生日派對特訓版 🎂</h1>
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
            q: "1. I sat on a bench, watching several ducks hanging around the _____ of the lake.", options: ["education", "edge", "effect", "effort"], ans: 1, hint: "我坐在長凳上，看著幾隻鴨子在湖的【邊緣】盪。",
            exp: "物體的邊界或「邊緣」是 edge。",
            grammarTip: "",
            vocab: ["edge (n.) 邊緣", "bench (n.) 長凳", "lake (n.) 湖"]
        },
        { 
            q: "2. [文法] The girl was not careful when cutting the birthday cake, so she cut _____.", options: ["her", "she", "hers", "herself"], ans: 3, hint: "那個女孩切生日蛋糕時不小心，所以割傷了【她自己】。",
            exp: "主詞是 The girl (她)，割傷的對象也是自己，所以受詞必須用反身代名詞 herself。",
            grammarTip: "這題妳在課本第 36 頁完美寫對了喔！She cut herself. (她割傷了她自己)。",
            vocab: ["herself (pron.) 她自己", "cut (v.) 割傷", "careful (adj.) 小心的"]
        },
        { 
            q: "3. Many people work hard in an _____ to save enough money to own their own homes.", options: ["emotion", "effect", "effort", "enemy"], ans: 2, hint: "很多人辛勤工作【努力】存足夠的錢，好擁有自己的家。",
            exp: "盡力去做某事的「努力」是 effort。in an effort to... 意思是「努力為了去...」。",
            grammarTip: "spare no effort 意思是「不遺餘力」。",
            vocab: ["effort (n.) 努力", "save money (phr.) 存錢", "own (v.) 擁有"]
        },
        { 
            q: "4. [文法] The red apples are sour (酸的). I want to buy those green _____.", options: ["one", "ones", "apple", "ones'"], ans: 1, hint: "紅蘋果很酸。我想買那些綠色的【蘋果】。",
            exp: "為了不重複說 apples (複數名詞)，我們可以用不定代名詞 ones 來代替。",
            grammarTip: "單數名詞用 one 代替；複數名詞用 ones 代替。這裡指的是那些「綠色的蘋果們」，所以是 ones。",
            vocab: ["ones (pron.) 那些(東西)", "sour (adj.) 酸的"]
        },
        { 
            q: "5. He drank all the milk and handed the _____ glass to his mother.", options: ["electric", "empty", "effective", "elder"], ans: 1, hint: "他喝光了所有的牛奶，並把【空的】杯子遞給他的媽媽。",
            exp: "裡面什麼都沒有的、「空的」是 empty；它也可以當動詞「倒空」。",
            grammarTip: "",
            vocab: ["empty (adj./v.) 空的/倒空", "hand (v.) 遞給", "glass (n.) 玻璃杯"]
        },
        { 
            q: "6. [文法] The old man's family lived far away, so he lived in the house all by _____.", options: ["him", "his", "himself", "he"], ans: 2, hint: "老先生的家人住得很遠，所以他【自己一個人】住在那棟房子裡。",
            exp: "by oneself 是一個非常重要的片語，意思是「獨自、自己一個人」。主詞是 he，所以搭配 by himself。",
            grammarTip: "課本第 36 頁的必考重點：by + 反身代名詞 = 獨自、靠自己。He lives by himself.",
            vocab: ["by himself (phr.) 他自己一個人", "far away (adv.) 遙遠地"]
        },
        { 
            q: "7. When I am feeling down, my best friend often _____s me to keep going.", options: ["employs", "elects", "ends", "encourages"], ans: 3, hint: "當我情緒低落時，我最好的朋友經常【鼓勵】我繼續前進。",
            exp: "給予別人勇氣或希望、「鼓勵」的動詞是 encourage。",
            grammarTip: "encourage someone to V... 意思是「鼓勵某人去做某事」。",
            vocab: ["encourage (v.) 鼓勵", "feel down (phr.) 情緒低落", "keep going (phr.) 繼續前進"]
        },
        { 
            q: "8. [文法] This dictionary is too heavy to carry. I need a lighter _____.", options: ["ones", "one", "dictionarys", "one's"], ans: 1, hint: "這本字典太重了帶不動。我需要一本比較輕的【字典】。",
            exp: "dictionary (字典) 這裡指的是「單數」的一本字典，所以用不定代名詞 one 來代替。",
            grammarTip: "單數用 one；複數用 ones。a lighter one ＝ 一本比較輕的字典。",
            vocab: ["one (pron.) 一個(東西)", "heavy (adj.) 重的", "lighter (adj.) 較輕的"]
        },
        { 
            q: "9. I don't like to drink black coffee, and my little sister doesn't like it, _____.", options: ["too", "either", "also", "neither"], ans: 1, hint: "我不喜歡喝黑咖啡，我妹妹【也(不)】喜歡。",
            exp: "這題是必考陷阱！在肯定句中，我們用 too 表示「也」；但在【否定句 (doesn't)】中，我們必須用 either 表示「也不」。",
            grammarTip: "肯定句的也 = too (I like it, too.)；否定句的也不 = either (I don't like it, either.)。",
            vocab: ["either (adv.) 也不", "black coffee (n.) 黑咖啡"]
        },
        { 
            q: "10. [文法] We sang songs, ate a lot of cake, and really enjoyed _____ at Rou-xuan's birthday party.", options: ["our", "us", "ourselves", "ours"], ans: 2, hint: "我們在柔萱的生日派對上唱歌、吃了很多蛋糕，真的【玩得很開心】。",
            exp: "enjoy oneself 是固定片語，意思是「玩得很開心」。主詞是 We，所以要配 ourselves。",
            grammarTip: "enjoy oneself = have a good time。We enjoyed ourselves ＝ 我們玩得很開心！",
            vocab: ["enjoy ourselves (phr.) 我們玩得很開心", "birthday party (n.) 生日派對"]
        },
        { 
            q: "11. Children are full of _____. They can run and play all day long without feeling tired.", options: ["emotion", "energy", "education", "effect"], ans: 1, hint: "孩子們充滿【精力】。他們可以跑來跑去玩一整天都不會覺得累。",
            exp: "活力、活動力或是物理上的「能量、精力」，英文是 energy。",
            grammarTip: "be full of energy 意思是「充滿活力 / 精力充沛」。",
            vocab: ["energy (n.) 精力/能量", "all day long (phr.) 一整天", "tired (adj.) 疲累的"]
        },
        { 
            q: "12. [文法] Mom asked the two boys, \"Did you clean the messy room all by _____? Good job!\"", options: ["yourself", "you", "yours", "yourselves"], ans: 3, hint: "媽媽問那兩個男孩：「你們是【靠你們自己】打掃這間亂七八糟的房間的嗎？做得好！」",
            exp: "句子的對象是 the two boys (兩個男孩)，所以這裡的 you 是「你們 (複數)」，反身代名詞必須用複數的 yourselves！",
            grammarTip: "妳在課本第 36 頁寫得超棒：you (單數) ➔ yourself；you (複數) ➔ yourselves。",
            vocab: ["yourselves (pron.) 你們自己", "messy (adj.) 凌亂的", "all by yourselves (phr.) 全靠你們自己"]
        },
        { 
            q: "13. She really _____ed me by shouting at me in front of all my classmates.", options: ["employed", "encouraged", "emphasized", "embarrassed"], ans: 3, hint: "她在所有同學面前對我大吼大叫，真的讓我感到很【尷尬 / 難堪】。",
            exp: "讓別人在大庭廣眾下下不了台、「使尷尬」的動詞是 embarrass。",
            grammarTip: "in public 是「在公開場合、在大庭廣眾之下」。",
            vocab: ["embarrass (v.) 使尷尬", "shout at (phr.) 對...大吼", "in front of (phr.) 在...面前"]
        },
        { 
            q: "14. [文法] I don't like these long novels. How about those short _____?", options: ["one", "ones", "novel", "one's"], ans: 1, hint: "我不喜歡這些長篇小說。那些短的【小說】如何？",
            exp: "前面提到的是 long novels (複數)，為了避免重複，後面要用不定代名詞的複數 ones。",
            grammarTip: "這題是妳在課本第 37 頁寫對的題目！long novels ➔ short ones。",
            vocab: ["ones (pron.) 那些(東西)", "novel (n.) 小說", "How about...? (phr.) ...如何？"]
        },
        { 
            q: "15. When he heard the sad news, he had trouble hiding his _____s and started to cry.", options: ["effects", "emotions", "enemies", "elections"], ans: 1, hint: "當他聽到那個壞消息時，他難以隱藏他的【情感 / 情緒】，開始哭了起來。",
            exp: "內心的感受、「情感、情緒」是 emotion。",
            grammarTip: "have trouble + V-ing 意思是「做某事有困難 / 難以...」。",
            vocab: ["emotion (n.) 情感/情緒", "hide (v.) 隱藏", "sad news (n.) 壞消息"]
        },
        { 
            q: "16. [文法] The cat is washing _____ after eating the delicious fish.", options: ["it", "its", "itself", "it's"], ans: 2, hint: "貓咪在吃完美味的魚後正在清洗【牠自己】。",
            exp: "主詞是 The cat (動物用 it)，清洗的對象也是自己，所以受詞要用反身代名詞 itself。",
            grammarTip: "it 的反身代名詞是 itself (牠自己 / 它自己)。",
            vocab: ["itself (pron.) 牠自己", "wash (v.) 清洗", "delicious (adj.) 美味的"]
        },
        { 
            q: "17. The new supermarket will _____ twenty people to work as cashiers and clerks.", options: ["employ", "elect", "eat", "end"], ans: 0, hint: "這家新超市將【僱用】二十人來擔任收銀員和店員。",
            exp: "花錢請人來工作、「僱用」的動詞是 employ。員工是 employee，老闆是 employer。",
            grammarTip: "",
            vocab: ["employ (v.) 僱用", "cashier (n.) 收銀員", "clerk (n.) 店員"]
        },
        { 
            q: "18. Climate change is sure to produce direct _____s on our environment.", options: ["efforts", "edges", "educations", "effects"], ans: 3, hint: "氣候變遷肯定會對我們的環境產生直接的【影響 / 效果】。",
            exp: "產生出來的結果或「影響」是 effect (名詞)；形容詞是 effective (有效的)。",
            grammarTip: "produce effects on... 意思是「對...產生影響」。",
            vocab: ["effect (n.) 影響/效果", "climate change (n.) 氣候變遷", "environment (n.) 環境"]
        },
        { 
            q: "19. Everything is funny as long as it is happening to somebody _____.", options: ["else", "either", "elder", "empty"], ans: 0, hint: "只要是發生在【其他人】身上，每件事情都是可笑的。",
            exp: "表示「其他的、另外的」副詞是 else，通常放在 somebody/nobody/who/what 等字詞的後面。",
            grammarTip: "somebody else 意思是「其他人」；what else 意思是「還有什麼其他的」。",
            vocab: ["else (adv.) 其他的/另外的", "funny (adj.) 好笑的", "happen to (phr.) 發生在...身上"]
        },
        { 
            q: "20. Most parents work hard to make money because they want their children to get a good _____.", options: ["election", "emotion", "education", "element"], ans: 2, hint: "多數父母努力賺錢，因為他們希望他們的小孩能接受良好的【教育】。",
            exp: "在學校學習知識的過程、「教育」是 education。",
            grammarTip: "receive/get a good education 意思是「接受良好的教育」。",
            vocab: ["education (n.) 教育", "parent (n.) 父母", "make money (phr.) 賺錢"]
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
            
            var html = '<div class="score-title">🎉 派對測驗完成！<br>你的總分：' + score + ' / ' + quizData.length + '<br><span style="font-size: 0.8em; color: #ad1457;">(使用了 ' + hintsUsed + ' 次提示)</span></div>';
            
            if (wrongQuestions.length === 0) {
                html += '<div style="text-align: center; background: #fce4ec; color: #ad1457; padding: 20px; border-radius: 12px; font-weight: bold; margin-top: 15px;">🌟 完美過關！反身代名詞跟 one/ones 完全難不倒你！祝柔萱生日快樂！🎂🎁💯</div>';
            } else {
                html += '<div class="review-section">';
                html += '<div class="review-title">📕 你的專屬錯題與文法複習 (' + wrongQuestions.length + ' 題)</div>';
                html += '<div style="font-size:0.85em; color:#666; text-align:center; margin-bottom:12px;">吃完蛋糕再來把錯題小卡複習一下，下次考試絕對滿分！</div>';
                
                for (var w = 0; w < wrongQuestions.length; w++) {
                    var item = wrongQuestions[w];
                    var correctOpt = item.options[item.ans];
                    html += '<div class="wrong-card">';
                    html += '<div class="wrong-card-q">' + item.q + '</div>';
                    html += '<div class="wrong-card-ans">✅ 正確答案：' + correctOpt + '</div>';
                    html += '<div class="wrong-card-exp">💡 ' + item.exp + '</div>';
                    if (item.grammarTip) {
                        html += '<div style="color:#c62828; font-size:0.9em; margin-bottom:6px;"><strong>🧑‍🏫 文法小提醒：</strong>' + item.grammarTip + '</div>';
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
            btn.style.background = "#d81b60";
            btn.style.color = "white";
            feedback.innerHTML = "✅ 答對了！太讚了！🎉";
            feedback.className = "feedback correct";
            score++;
        } else {
            btn.style.background = "#6c757d";
            btn.style.color = "white";
            if (options[correctIndex]) {
                options[correctIndex].style.background = "#d81b60";
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
