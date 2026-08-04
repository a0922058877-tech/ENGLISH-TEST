<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>小學生英文單字挑戰 (boring ~ break 100%相容版)</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f4fbf7; color: #333; line-height: 1.6; padding: 20px; }
        .container { max-width: 600px; margin: 0 auto; background: #fff; padding: 30px; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.08); }
        h1 { text-align: center; color: #38b000; border-bottom: 2px dashed #b7e4c7; padding-bottom: 10px; }
        .question { font-size: 1.2em; font-weight: bold; margin-bottom: 15px; min-height: 50px; color: #111; }
        .options { display: flex; flex-direction: column; gap: 10px; margin-bottom: 20px; }
        .option { padding: 12px 15px; background: #e9f5ed; border: none; border-radius: 8px; cursor: pointer; font-size: 1em; text-align: left; transition: 0.2s; }
        .option:hover { background: #c7f9cc; }
        .hint-btn { background: #ffb703; color: #333; padding: 8px 12px; border: none; border-radius: 6px; cursor: pointer; font-size: 0.9em; margin-bottom: 15px; font-weight: bold; }
        .hint-text { display: none; color: #555; font-size: 0.9em; background: #fefae0; padding: 10px; border-radius: 6px; margin-bottom: 15px; border-left: 4px solid #fb8500; }
        .feedback { font-weight: bold; margin-bottom: 15px; display: none; padding: 10px; border-radius: 6px; }
        .correct { color: #155724; background-color: #d4edda; border: 1px solid #c3e6cb; }
        .wrong { color: #721c24; background-color: #f8d7da; border: 1px solid #f5c6cb; }
        .explanation-box { display: none; background-color: #f0fdf4; border-left: 4px solid #38b000; padding: 15px; margin-bottom: 15px; border-radius: 6px; font-size: 0.95em; }
        .explanation-box h4 { margin: 0 0 10px 0; color: #2b9348; }
        .vocab-list { margin-top: 10px; padding-left: 20px; color: #555; }
        .next-btn { display: none; background: #38b000; color: white; padding: 12px 20px; border: none; border-radius: 8px; cursor: pointer; font-size: 1em; width: 100%; font-weight: bold; }
        .next-btn:hover { background: #2b9348; }
        #result { text-align: center; font-size: 1.5em; font-weight: bold; color: #38b000; display: none; }
        .reload-btn { background: #6c757d; color: white; padding: 6px 10px; border: none; border-radius: 4px; font-size: 0.8em; cursor: pointer; float: left; }
    </style>
</head>
<body>

<div class="container">
    <h1>🌱 英文單字挑戰 (boring ~ break) 🌱</h1>
    <div id="quiz-container">
        <div style="overflow: hidden; margin-bottom: 10px;">
            <button class="reload-btn" onclick="loadQuestion()">🔄 重新載入題目</button>
            <div id="q-counter" style="text-align: right; color: #999; font-size: 0.9em; float: right;">載入中...</div>
        </div>
        
        <div class="question" id="question-text">如果沒有看到題目，請點擊上方「重新載入題目」按鈕。</div>
        
        <button class="hint-btn" onclick="showHint()">👀 點我偷看提示 (整場測驗只能看 5 次喔！)</button>
        <div class="hint-text" id="hint-text"></div>

        <div class="options" id="options-container"></div>
        <div class="feedback" id="feedback-text"></div>
        
        <div class="explanation-box" id="explanation-box">
            <h4>💡 答案詳解</h4>
            <div id="exp-content"></div>
            <h4>📖 順便記單字</h4>
            <ul class="vocab-list" id="vocab-content"></ul>
        </div>

        <button class="next-btn" id="next-btn" onclick="nextQuestion()">下一題 ➔</button>
    </div>
    <div id="result"></div>
</div>

<script>
    var quizData = [
        { 
            q: "1. The speech was so _____ that several students fell asleep in the classroom.", options: ["brave", "boring", "born", "both"], ans: 1, hint: "那場演講太【無聊的 / 枯燥的】了，以至於好幾位學生在教室裡睡著了。",
            exp: "形容事情或演講「令人感到無聊、枯燥的」要用 -ing 結尾的 boring；bored 則是形容人「感到無聊的」。", vocab: ["boring (adj.) 令人無聊的", "speech (n.) 演講", "fall asleep (v.) 睡著"]
        },
        { 
            q: "2. My cousin was _____ in Taiwan, but he grew up in Japan.", options: ["born", "both", "bothered", "bowed"], ans: 0, hint: "我的表弟是在台灣【出生的】，但他是在日本長大的。",
            exp: "be born in + 地點/年份，表示「在...出生」。born 是 bear (生育) 的過去分詞，常作形容詞用。", vocab: ["born (adj.) 出生的", "grow up (v.) 長大", "Taiwan (n.) 台灣"]
        },
        { 
            q: "3. If you _____ money from the bank, you have to pay it back with interest.", options: ["bother", "break", "borrow", "bow"], ans: 2, hint: "如果你向銀行【借入 / 借款】金錢，你就必須連同利息一起還清。",
            exp: "向別人或銀行「借入」是 borrow (borrow ... from ...)；如果是「借出給別人」則是 lend。", vocab: ["borrow (v.) 借入", "bank (n.) 銀行", "pay back (v.) 償還"]
        },
        { 
            q: "4. Mr. Sam quit his job last month and started a new business to be his own _____.", options: ["boy", "boss", "box", "brain"], ans: 1, hint: "山姆先生上個月辭了工作並開始創業，做自己的【老闆】。",
            exp: "公司的主管或「老闆」是 boss；be one's own boss 意思是「自己創業當老闆」。", vocab: ["boss (n.) 老闆", "quit (v.) 辭職", "business (n.) 生意/事業"]
        },
        { 
            q: "5. You will hurt your health if you burn the candle at _____ ends.", options: ["born", "brave", "both", "boring"], ans: 2, hint: "如果你蠟燭【兩者都】燒（兩頭燒），你的健康會出問題的。",
            exp: "both 表示「兩者、雙方」。burn the candle at both ends 是英文成語，指「日夜操勞、過度消耗精力」。", vocab: ["both (adj./pron.) 兩者(都)", "health (n.) 健康", "candle (n.) 蠟燭"]
        },
        { 
            q: "6. Please do not _____ your sister while she is busy doing her English homework.", options: ["bother", "borrow", "break", "bow"], ans: 0, hint: "當你妹妹正在忙著寫英文功課時，請不要【打擾 / 煩擾】她。",
            exp: "bother 當動詞時可以指「打擾、使人煩惱」(Don't bother me!)，也可當「費心、麻煩去作某事」。", vocab: ["bother (v.) 打擾/煩擾", "busy (adj.) 忙碌的", "homework (n.) 功課"]
        },
        { 
            q: "7. Mike picked up the glass _____ and drank directly from it.", options: ["bottom", "bottle", "bowl", "box"], ans: 1, hint: "麥可拿起那只玻璃【瓶子】，直接對著瓶口喝。",
            exp: "裝水或飲料的「瓶子 / 壺」是 bottle；a bottle of wine/water 指「一瓶酒/水」。", vocab: ["bottle (n.) 瓶子", "drank (v.) drink的過去式", "directly (adv.) 直接地"]
        },
        { 
            q: "8. I found an old photo of my grandmother at the _____ of the drawer.", options: ["bottom", "bottle", "branch", "brain"], ans: 0, hint: "我在抽屜的【最底部 / 下端】找到一張我祖母的舊照片。",
            exp: "物體的「底部、下端」是 bottom (at the bottom of...)；相對的「頂部」則是 top。", vocab: ["bottom (n.) 底部", "drawer (n.) 抽屜", "photo (n.) 照片"]
        },
        { 
            q: "9. The singer _____ed to the audience when they clapped loudly after the song.", options: ["bother", "borrow", "bow", "break"], ans: 2, hint: "歌曲結束後觀眾熱烈鼓掌時，歌手向他們【鞠躬 / 致意】。",
            exp: "bow 當動詞讀作 /baʊ/，意思是「鞠躬、低頭致意」；如果是弓或蝴蝶結則讀作 /bo/。", vocab: ["bow (v.) 鞠躬", "audience (n.) 觀眾", "clap (v.) 鼓掌"]
        },
        { 
            q: "10. In Japan, people often greet each other with a _____ rather than shaking hands.", options: ["box", "bow", "bowl", "boss"], ans: 1, hint: "在日本，人們相遇時常常以【鞠躬】互相致意，而不是握手。",
            exp: "bow 也可以當名詞用，make a bow / give a bow 就是「行一鞠躬」。", vocab: ["bow (n.) 鞠躬", "greet (v.) 問候/打招呼", "shake hands (v.) 握手"]
        },
        { 
            q: "11. Remember to lift your _____ towards your mouth while eating rice.", options: ["bottle", "box", "bowl", "bottom"], ans: 2, hint: "吃米飯時，記得把你的【碗】端向嘴邊。",
            exp: "吃飯喝湯用的「碗」是 bowl；一大碗麵可以是 a big bowl of noodles。", vocab: ["bowl (n.) 碗", "lift (v.) 舉起/端起", "mouth (n.) 嘴巴"]
        },
        { 
            q: "12. They go _____ every Saturday afternoon at the sports center.", options: ["boring", "bowling", "boiling", "blowing"], ans: 1, hint: "他們每個星期六下午都會去運動中心打【保齡球】。",
            exp: "一項用球擊倒球瓶的休閒運動「保齡球」是 bowling；go bowling 就是「去打保齡球」。", vocab: ["bowling (n.) 保齡球運動", "Saturday (n.) 星期六", "sports center (n.) 運動中心"]
        },
        { 
            q: "13. I opened the gift _____ and saw a beautiful new watch inside.", options: ["boss", "boy", "box", "bowl"], ans: 2, hint: "我打開禮物【盒子 / 箱子】，看到裡面有一支漂亮的新手錶。",
            exp: "專指方形的「盒子、箱子」是 box (複數形要加上 -es 變成 boxes)。", vocab: ["box (n.) 盒子/箱子", "gift (n.) 禮物", "watch (n.) 手錶"]
        },
        { 
            q: "14. He is just a young _____ who loves playing basketball after school.", options: ["boss", "boy", "brain", "branch"], ans: 1, hint: "他只不過是個放學後喜歡打籃球的年輕【男孩】。",
            exp: "年輕的男性、小學生或中學生「男孩」是 boy；相對的「女孩」是 girl。", vocab: ["boy (n.) 男孩", "young (adj.) 年輕的", "basketball (n.) 籃球"]
        },
        { 
            q: "15. It is wrong to think that people with good looks have no _____s.", options: ["bottle", "bottom", "brain", "branch"], ans: 2, hint: "認為長得好看的人沒有【頭腦 / 腦袋】是錯誤的想法。",
            exp: "人體內負責思考的「腦、頭腦、智力」是 brain；have a good brain 表示「很聰明、頭腦很好」。", vocab: ["brain (n.) 腦/智力", "wrong (adj.) 錯誤的", "good looks (n.) 好看的容貌"]
        },
        { 
            q: "16. Look! Several monkeys are hanging from the tree _____es in the forest.", options: ["branch", "brain", "bottle", "boss"], ans: 0, hint: "看！森林裡有好幾隻猴子吊掛在樹【枝】上。",
            exp: "大樹分杈出去的「樹枝、枝條」是 branch (複數形為 branches)。", vocab: ["branch (n.) 樹枝", "monkey (n.) 猴子", "hang (v.) 懸掛/吊"]
        },
        { 
            q: "17. The bank has just opened a new overseas _____ office in New York.", options: ["brain", "bottom", "branch", "bowl"], ans: 2, hint: "這家銀行剛在紐約開設了一家新的海外【分行 / 分處】。",
            exp: "branch 除了當「樹枝」，在商業與政府機關中也指「分行、分公司、分支機構」(branch office)。", vocab: ["branch (n.) 分公司/分行", "overseas (adj.) 海外的", "office (n.) 辦公室"]
        },
        { 
            q: "18. The _____ firefighter ran into the burning house to save the little puppy.", options: ["boring", "brave", "born", "both"], ans: 1, hint: "那位【勇敢的】消防員衝進火場救出了小狗。",
            exp: "面對危險或困難毫不畏懼的「勇敢的」是 brave；a brave man 就是個勇敢的人。", vocab: ["brave (adj.) 勇敢的", "firefighter (n.) 消防員", "save (v.) 拯救"]
        },
        { 
            q: "19. We bought some fresh _____ and milk from the bakery for breakfast.", options: ["brain", "branch", "bread", "break"], ans: 2, hint: "我們從麵包店買了一些新鮮的【麵包】和牛奶當早餐。",
            exp: "日常飲食主食之一的「麵包」是 bread (不可數名詞)；一片麵包是 a piece/slice of bread。", vocab: ["bread (n.) 麵包", "bakery (n.) 麵包店", "breakfast (n.) 早餐"]
        },
        { 
            q: "20. Please be careful with my camera! Don't drop it and _____ it.", options: ["borrow", "bother", "bow", "break"], ans: 3, hint: "請小心拿我的相機！不要把它摔下去並【弄壞 / 摔爛】它。",
            exp: "把物品「弄壞、打破、折斷」的動詞是 break (過去式是 broke，過去分詞是 broken)。", vocab: ["break (v.) 弄壞/打破", "careful (adj.) 小心的", "camera (n.) 照相機"]
        }
    ];

    var currentQ = 0;
    var score = 0;
    var hintsUsed = 0;

    function loadQuestion() {
        document.getElementById("feedback-text").style.display = "none";
        document.getElementById("explanation-box").style.display = "none";
        document.getElementById("next-btn").style.display = "none";
        document.getElementById("hint-text").style.display = "none";
        
        if (currentQ >= quizData.length) {
            document.getElementById("quiz-container").style.display = "none";
            var resultDiv = document.getElementById("result");
            resultDiv.style.display = "block";
            resultDiv.innerHTML = "🎉 測驗結束！<br>你的總分是：" + score + " / 20<br>使用了 " + hintsUsed + " 次提示！<br><br>" + (score >= 16 ? "太強大啦！從 boring 到 break，還有 branch 的分行和樹枝、bow 的鞠躬都完全搞懂了！🌟" : "很讚的挑戰！再把 branch (樹枝/分行) 和 bow (鞠躬) 的一字多義複習一下就會無敵喔！💪");
            return;
        }

        document.getElementById("q-counter").innerText = "第 " + (currentQ + 1) + " / 20 題";
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
            btn.style.background = "#38b000";
            btn.style.color = "white";
            feedback.innerHTML = "✅ 答對了！太讚了！";
            feedback.className = "feedback correct";
            score++;
        } else {
            btn.style.background = "#e63946";
            btn.style.color = "white";
            if (options[correctIndex]) {
                options[correctIndex].style.background = "#38b000";
                options[correctIndex].style.color = "white";
            }
            feedback.innerHTML = "❌ 答錯囉！正確答案是 " + currentData.options[correctIndex] + "。";
            feedback.className = "feedback wrong";
        }
        
        document.getElementById("exp-content").innerText = currentData.exp;
        
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

    // 雙重保險：網頁載入完畢後自動執行
    window.onload = function() {
        loadQuestion();
    };
</script>

</body>
</html>
