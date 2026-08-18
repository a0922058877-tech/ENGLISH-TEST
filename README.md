<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>英文單字+文法挑戰 (course~customer & 情態副詞)</title>
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
    <h1>🌱 單字+情態副詞挑戰</h1>
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
            q: "1. [文法] The boy is coloring the picture _____ with his new crayons.", options: ["happy", "happily", "happyly", "happilily"], ans: 1, hint: "小男孩正【快樂地】用他的新蠟筆幫圖畫上色。",
            exp: "修飾動詞「著色 (coloring)」必須使用情態副詞。happy 字尾是 y，要「去 y 加 ily」變成 happily。",
            grammarTip: "情態副詞用來修飾「動詞」。happy ➔ happily；angry ➔ angrily。妳在課本第 22 頁寫得完全正確喔！",
            vocab: ["color (v.) 著色", "happily (adv.) 快樂地", "crayon (n.) 蠟筆"]
        },
        { 
            q: "2. We often have four-_____ meals for our family dinner at the restaurant.", options: ["court", "cover", "course", "crowd"], ans: 2, hint: "我們在餐廳吃家庭晚餐時，通常會吃四【道菜】的餐點。",
            exp: "course 除了當「課程」，也可以當「一道菜」。four-course meals 就是指四道菜的餐點。",
            grammarTip: "take a course in cooking 意思是「上烹飪課」；main course 指的是「主菜」。",
            vocab: ["course (n.) 課程/一道菜", "meal (n.) 餐點", "dinner (n.) 晚餐"]
        },
        { 
            q: "3. My uncle's sons are my _____s. We always play together on Chinese New Year.", options: ["customs", "cousins", "customers", "crimes"], ans: 1, hint: "我叔叔的兒子們是我的【堂表兄弟】。我們總是在過年時一起玩。",
            exp: "叔伯阿姨的小孩、「堂兄弟姊妹、表兄弟姊妹」統稱 cousin。",
            grammarTip: "",
            vocab: ["cousin (n.) 堂/表兄弟姊妹", "uncle (n.) 叔叔/舅舅", "Chinese New Year (n.) 農曆新年"]
        },
        { 
            q: "4. [文法陷阱] The 10-year-old Shiba Inu runs very _____ to catch the ball.", options: ["fast", "fastly", "fasts", "faster"], ans: 0, hint: "這隻十歲的柴犬跑得非常【快】去接球。",
            exp: "這題是超級陷阱！fast 的形容詞和副詞是「同一個字」，絕對沒有 fastly 這個字！",
            grammarTip: "妳在課本第 22 頁完全沒被騙！fast 的副詞還是 fast；high 的副詞還是 high！",
            vocab: ["fast (adv.) 快速地", "Shiba Inu (n.) 柴犬", "catch (v.) 抓住/接住"]
        },
        { 
            q: "5. You shouldn't judge a book by its _____. The inside is what matters.", options: ["course", "cover", "cross", "culture"], ans: 1, hint: "你不應該以【封面】來評斷一本書。內在才是重要的。",
            exp: "書本的「封面」或物品的「蓋子」是 cover。",
            grammarTip: "Don't judge a book by its cover. 是一句有名的英文諺語，意思是「勿以貌取人」。",
            vocab: ["cover (n./v.) 封面/覆蓋", "judge (v.) 評斷", "matter (v.) 要緊/重要"]
        },
        { 
            q: "6. Robbing banks and hurting people are very serious _____s.", options: ["crimes", "crabs", "cups", "cures"], ans: 0, hint: "搶劫銀行和傷害別人是非常嚴重的【犯罪】。",
            exp: "違反法律的「罪、犯罪行為」是 crime。",
            grammarTip: "turn to crime 意思是「走向犯罪之路、誤入歧途」。",
            vocab: ["crime (n.) 犯罪", "rob (v.) 搶劫", "serious (adj.) 嚴重的"]
        },
        { 
            q: "7. [文法] The man waited for a long time and shouted _____ at the clerk.", options: ["angry", "angrily", "angryly", "more angry"], ans: 1, hint: "那個男人等了很久，然後對著店員【生氣地】大叫。",
            exp: "修飾動詞「大叫 (shouted)」要用副詞。angry 必須去 y 加 ily 變成 angrily。",
            grammarTip: "又是一個 y 結尾的字！angry ➔ angrily。副詞就像小跟班，用來修飾動詞的動作狀態。",
            vocab: ["shout (v.) 大叫", "angrily (adv.) 生氣地", "clerk (n.) 店員"]
        },
        { 
            q: "8. The MRT trains are usually very _____ with people during rush hours.", options: ["cruel", "crowded", "curious", "current"], ans: 1, hint: "捷運列車在尖峰時間通常擠滿了人，非常【擁擠的】。",
            exp: "充滿人的、「擁擠的」是 crowded。名詞 crowd 是指「群眾」。",
            grammarTip: "be crowded with... 意思是「擠滿了...」。",
            vocab: ["crowded (adj.) 擁擠的", "MRT (n.) 捷運", "rush hour (n.) 尖峰時間"]
        },
        { 
            q: "9. It was _____ of you to leave the poor little dog waiting outside in the cold rain.", options: ["crazy", "curious", "crowded", "cruel"], ans: 3, hint: "你把可憐的小狗留在外面淋冷雨，真是太【殘忍的】了。",
            exp: "沒有同情心、會傷害別人的「殘忍的、殘酷的」是 cruel。",
            grammarTip: "It is cruel to + V... 意思是「做某件事是殘忍的」。",
            vocab: ["cruel (adj.) 殘忍的", "poor (adj.) 可憐的/貧窮的", "outside (adv.) 在外面"]
        },
        { 
            q: "10. [文法陷阱] She works very _____ every day to make money for her family.", options: ["hardly", "hard", "harder", "hards"], ans: 1, hint: "她每天【努力地】工作，為家人賺錢。",
            exp: "這是國中會考必考題！「努力地」副詞就是 hard；hardly 意思是「幾乎不」，意思完全不一樣喔！",
            grammarTip: "妳在筆記寫對了！hard = 努力地/困難地；hardly = 幾乎不。千萬不要選錯喔！",
            vocab: ["hard (adv.) 努力地", "hardly (adv.) 幾乎不", "make money (phr.) 賺錢"]
        },
        { 
            q: "11. The scientist is trying to _____ a new way to clean the polluted river.", options: ["cross", "create", "cry", "cure"], ans: 1, hint: "科學家正試圖【創造 / 發明】一種清理受污染河流的新方法。",
            exp: "無中生有、發明或「創造」的動詞是 create。",
            grammarTip: "",
            vocab: ["create (v.) 創造", "scientist (n.) 科學家", "polluted (adj.) 受污染的"]
        },
        { 
            q: "12. Doctors are still working hard to find a _____ for the terrible disease.", options: ["cup", "cure", "curve", "crisis"], ans: 1, hint: "醫生們仍在努力尋找治療這種可怕疾病的【解藥 / 療法】。",
            exp: "cure 當動詞是治療，當名詞是「療法、解藥」(a cure for cancer)。",
            grammarTip: "",
            vocab: ["cure (n./v.) 療法/治療", "disease (n.) 疾病", "terrible (adj.) 可怕的"]
        },
        { 
            q: "13. [文法] He went to bed very _____ last night, so he is tired now.", options: ["late", "lately", "later", "lates"], ans: 0, hint: "他昨晚很【晚】睡，所以他現在很累。",
            exp: "跟 hard 的陷阱一樣！「晚地」副詞就是 late；lately 意思是「最近」。",
            grammarTip: "筆記神救援！late = 晚的/晚地；lately = 最近。所以「很晚睡」只能選 late！",
            vocab: ["late (adv.) 晚地", "lately (adv.) 最近", "go to bed (phr.) 睡覺"]
        },
        { 
            q: "14. A successful business always puts its _____s first to provide good service.", options: ["customs", "cousins", "customers", "courses"], ans: 2, hint: "一家成功的企業總是把【顧客】放在第一位，以提供良好的服務。",
            exp: "來買東西的「顧客、消費者」是 customer。",
            grammarTip: "custom 是「習俗 / 海關」，加上 er 變 customer 就是「顧客」。",
            vocab: ["customer (n.) 顧客", "successful (adj.) 成功的", "provide (v.) 提供"]
        },
        { 
            q: "15. We follow the _____ of giving red envelopes to children on Chinese New Year.", options: ["custom", "culture", "customer", "crisis"], ans: 0, hint: "我們遵循在農曆新年發紅包給小孩的【習俗】。",
            exp: "社會群體長期以來的「習俗、慣例」是 custom。",
            grammarTip: "red envelope 就是過年拿的「紅包」。",
            vocab: ["custom (n.) 習俗", "red envelope (n.) 紅包", "follow (v.) 遵循/跟隨"]
        },
        { 
            q: "16. [文法] My father speaks English very _____, but I can only speak a little.", options: ["good", "goodly", "well", "better"], ans: 2, hint: "我爸爸英文說得非常【好】，但我只會說一點點。",
            exp: "修飾動詞 (speaks) 必須用副詞。good 是形容詞，它的不規則副詞是 well！",
            grammarTip: "妳在課本第 22 頁寫得超漂亮！good 的副詞是不規則變化的 well，絕對不能說 speak English good！",
            vocab: ["well (adv.) 很好地", "speak (v.) 說/講", "a little (phr.) 一點點"]
        },
        { 
            q: "17. The little boy was very _____ about the big box and wanted to open it.", options: ["cruel", "curious", "crowded", "current"], ans: 1, hint: "小男孩對那個大箱子感到非常【好奇】，想要打開它。",
            exp: "對未知的東西想了解、「好奇的」是 curious；be curious about... 意思是「對...感到好奇」。",
            grammarTip: "",
            vocab: ["curious (adj.) 好奇的", "open (v.) 打開", "box (n.) 箱子/盒子"]
        },
        { 
            q: "18. [文法] The dog was sleeping _____ on the sofa when I came home.", options: ["comfortable", "comfortably", "comfort", "comfortabily"], ans: 1, hint: "我回家時，那隻狗正【舒服地】在沙發上睡覺。",
            exp: "修飾 sleeping (睡覺) 要用副詞。字尾是 le 的形容詞 (comfortable)，要去 e 加 y 變成 comfortably。",
            grammarTip: "字尾是 le 的形容詞，副詞要把 e 改成 y！(comfortable ➔ comfortably / terrible ➔ terribly)。",
            vocab: ["comfortably (adv.) 舒服地", "sleep (v.) 睡覺", "sofa (n.) 沙發"]
        },
        { 
            q: "19. The mother opened the _____s to let the morning sunlight come into the room.", options: ["curves", "cups", "curtains", "courses"], ans: 2, hint: "媽媽拉開【窗簾】，讓早晨的陽光照進房間。",
            exp: "掛在窗戶上遮光的「窗簾」是 curtain (通常會用複數 curtains)。",
            grammarTip: "draw/pull the curtains 意思是「拉上/拉開窗簾」。",
            vocab: ["curtain (n.) 窗簾", "sunlight (n.) 陽光", "let (v.) 讓"]
        },
        { 
            q: "20. The path _____ed down the hill, making it difficult to drive fast.", options: ["cried", "crossed", "curved", "covered"], ans: 2, hint: "這條小路沿著山丘【彎曲】而下，使得開快車變得很困難。",
            exp: "curve 當名詞是曲線，當動詞是「彎曲、轉彎」。",
            grammarTip: "curve 跟前面學過的 coast (海岸) 很像，driving on a curved coast road (開在彎曲的海岸公路上)。",
            vocab: ["curve (v./n.) 彎曲/曲線", "path (n.) 小路", "hill (n.) 山丘"]
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
                html += '<div style="text-align: center; background: #e8f5e9; color: #1e4620; padding: 20px; border-radius: 12px; font-weight: bold; margin-top: 15px;">🌟 太神啦！全部答對！C 開頭所有單字跟「情態副詞」的變形陷阱全被你破解了！💯</div>';
            } else {
                html += '<div class="review-section">';
                html += '<div class="review-title">📕 你的專屬錯題與文法複習 (' + wrongQuestions.length + ' 題)</div>';
                html += '<div style="font-size:0.85em; color:#666; text-align:center; margin-bottom:12px;">把錯題小卡複習一下，下次遇到 fast 和 hard 絕對能秒殺它們！</div>';
                
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
