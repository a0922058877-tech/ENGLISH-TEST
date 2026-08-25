<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>英文單字+文法挑戰 (edge~energy 升級突破版)</title>
    <style>
        * { box-sizing: border-box; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background-color: #e8eaf6; /* 淺靛藍背景 */
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
            box-shadow: 0 6px 20px rgba(63, 81, 181, 0.15);
            margin: 0 auto;
        }
        h1 {
            text-align: center;
            color: #3f51b5; /* 星空靛藍 */
            font-size: 1.2em;
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
            background: #7986cb;
            color: white;
            padding: 6px 12px;
            border: none;
            border-radius: 8px;
            font-size: 0.85em;
            cursor: pointer;
            font-weight: bold;
        }
        #q-counter {
            color: #5c6bc0;
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
            background: #ffb300; /* 溫暖琥珀 */
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
            background: #f8f9fa;
            border: 2px solid #e8eaf6;
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
            background: #e8eaf6;
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
            background-color: #e8eaf6;
            border-left: 4px solid #3f51b5;
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
            background-color: #e3f2fd;
            border-left: 4px solid #1976d2;
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
            background: #3f51b5;
            color: white;
            padding: 14px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-size: 1.05em;
            width: 100%;
            font-weight: bold;
            box-shadow: 0 3px 10px rgba(63, 81, 181, 0.3);
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
            color: #3f51b5;
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
            background: #3f51b5;
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
    <h1>🚀 單字+文法 升級突破版</h1>
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
            q: "1. Chin-chin put a lot of _____ into crocheting the beautiful Pikmin hat.", options: ["emotion", "effort", "effect", "education"], ans: 1, hint: "芩芩投入了很多【努力】來鉤織那頂美麗的皮克敏帽子。",
            exp: "盡力去做某事的「努力」是 effort。put effort into... 意思是「投入努力在...」。",
            grammarTip: "",
            vocab: ["effort (n.) 努力", "crochet (v.) 鉤織", "beautiful (adj.) 美麗的"]
        },
        { 
            q: "2. [文法] The 10-year-old Shiba Inu was looking at _____ in the mirror.", options: ["it", "its", "itself", "him"], ans: 2, hint: "那隻十歲的柴犬正看著鏡子裡的【牠自己】。",
            exp: "主詞是 Shiba Inu (動物用 it)，看的對象也是自己，所以受詞必須用反身代名詞 itself。",
            grammarTip: "反身代名詞就是「...自己」。it (牠) ➔ itself (牠自己)。",
            vocab: ["itself (pron.) 牠自己/它自己", "mirror (n.) 鏡子"]
        },
        { 
            q: "3. After finishing the delicious Korean hotteok, he left the _____ plate on the table.", options: ["electric", "effective", "empty", "elder"], ans: 2, hint: "吃完美味的韓式糖餅後，他把【空的】盤子留在桌上。",
            exp: "裡面什麼都沒有的、「空的」是 empty；它也可以當動詞「倒空」。",
            grammarTip: "",
            vocab: ["empty (adj./v.) 空的/倒空", "plate (n.) 盤子", "delicious (adj.) 美味的"]
        },
        { 
            q: "4. [文法] I don't like the heavy dark sofas. I prefer those cream-colored _____.", options: ["one", "ones", "sofa", "ones'"], ans: 1, hint: "我不喜歡那些笨重的深色沙發。我比較喜歡那些奶油色的【沙發】。",
            exp: "為了不重複說 sofas (複數名詞)，我們可以用不定代名詞 ones 來代替。",
            grammarTip: "單數名詞用 one 代替；複數名詞用 ones 代替。這裡指的是那些「奶油色的沙發們」，所以是 ones。",
            vocab: ["ones (pron.) 那些(東西)", "cream-colored (adj.) 奶油色的", "prefer (v.) 比較喜歡"]
        },
        { 
            q: "5. It really _____ed me when my dog bit the furniture in front of our guests.", options: ["employed", "encouraged", "embarrassed", "elected"], ans: 2, hint: "當我的狗在客人面前咬傢俱時，真的讓我感到很【尷尬 / 難堪】。",
            exp: "讓別人在大庭廣眾下下不了台、「使尷尬」的動詞是 embarrass。",
            grammarTip: "",
            vocab: ["embarrass (v.) 使尷尬", "bite (v.) 咬(過去式bit)", "furniture (n.) 傢俱"]
        },
        { 
            q: "6. I don't like noisy environments, and my boyfriend doesn't like them, _____.", options: ["too", "either", "also", "neither"], ans: 1, hint: "我不喜歡吵鬧的環境，我男朋友【也(不)】喜歡。",
            exp: "這題是必考陷阱！在肯定句中，我們用 too 表示「也」；但在【否定句 (doesn't)】中，我們必須用 either 表示「也不」。",
            grammarTip: "肯定句的也 = too (I like it, too.)；否定句的也不 = either (I don't like it, either.)。",
            vocab: ["either (adv.) 也不", "noisy (adj.) 吵鬧的", "environment (n.) 環境"]
        },
        { 
            q: "7. [文法] The students baked the sausages and bread all by _____.", options: ["them", "their", "themselves", "themself"], ans: 2, hint: "學生們【全靠他們自己】烤了香腸和麵包。",
            exp: "by oneself 是一個非常重要的片語，意思是「獨自、自己一個人/靠自己」。主詞是 The students (他們)，所以搭配 themselves。",
            grammarTip: "課本第 36 頁的必考重點：by + 反身代名詞 = 獨自、靠自己。they 的反身代名詞是 themselves！",
            vocab: ["by themselves (phr.) 靠他們自己", "bake (v.) 烘烤", "sausage (n.) 香腸"]
        },
        { 
            q: "8. When I was struggling with the difficult crochet pattern, my sister _____d me to keep trying.", options: ["employed", "elected", "ended", "encouraged"], ans: 3, hint: "當我在跟困難的鉤織圖解奮戰時，我妹妹【鼓勵】我繼續嘗試。",
            exp: "給予別人勇氣或希望、「鼓勵」的動詞是 encourage。",
            grammarTip: "encourage someone to V... 意思是「鼓勵某人去做某事」。",
            vocab: ["encourage (v.) 鼓勵", "struggle with (phr.) 與...奮戰", "keep trying (phr.) 繼續嘗試"]
        },
        { 
            q: "9. The new minimalist cream style will have a calming _____ on our new home.", options: ["effort", "edge", "education", "effect"], ans: 3, hint: "新的極簡奶油風格將對我們的新家產生平靜的【影響 / 效果】。",
            exp: "產生出來的結果或「影響」是 effect (名詞)；形容詞是 effective (有效的)。",
            grammarTip: "have an effect on... 意思是「對...產生影響」。",
            vocab: ["effect (n.) 影響/效果", "minimalist (adj.) 極簡主義的", "calming (adj.) 令人平靜的"]
        },
        { 
            q: "10. [文法] My old bathroom faucet is broken. I plan to buy a new TOTO _____ during our Tokyo trip in 2026.", options: ["ones", "one", "faucets", "one's"], ans: 1, hint: "我舊的浴室水龍頭壞了。我計畫在2026年的東京之旅買一個新的 TOTO【水龍頭】。",
            exp: "faucet (水龍頭) 這裡指的是「單數」的一個水龍頭，所以用不定代名詞 one 來代替。",
            grammarTip: "單數用 one；複數用 ones。a new TOTO one ＝ 一個新的 TOTO 水龍頭。",
            vocab: ["one (pron.) 一個(東西)", "faucet (n.) 水龍頭", "broken (adj.) 壞掉的"]
        },
        { 
            q: "11. The 10-year-old Shiba Inu is full of _____; he runs around the house all day.", options: ["emotion", "energy", "education", "elephant"], ans: 1, hint: "這隻十歲的柴犬充滿【精力】；他整天在房子裡跑來跑去。",
            exp: "活力、活動力或是物理上的「能量、精力」，英文是 energy。",
            grammarTip: "be full of energy 意思是「充滿活力 / 精力充沛」。",
            vocab: ["energy (n.) 精力/能量", "run around (phr.) 跑來跑去", "all day (phr.) 一整天"]
        },
        { 
            q: "12. [文法] \"Help _____ to some homemade bread, guys!\" said the host.", options: ["yourself", "you", "yours", "yourselves"], ans: 3, hint: "主人說：「大夥們，請【你們自己】隨意吃些自製的麵包吧！」",
            exp: "對象是 guys (大夥們/複數)，所以這裡的 you 是「你們 (複數)」，反身代名詞必須用複數的 yourselves！",
            grammarTip: "Help yourself/yourselves to... 是招待客人的常見用語，意思是「請自行取用...」。單數客人用 yourself，多位客人用 yourselves。",
            vocab: ["yourselves (pron.) 你們自己", "homemade (adj.) 自製的", "host (n.) 主人"]
        },
        { 
            q: "13. We should always respect our _____s and listen to their wise advice.", options: ["elephants", "electrons", "elders", "enemies"], ans: 2, hint: "我們應該永遠尊敬我們的【長輩】，並聽取他們明智的建議。",
            exp: "年紀較長的人、「長輩」是 elder。",
            grammarTip: "elder brother 是「哥哥」；elder sister 是「姊姊」。",
            vocab: ["elder (n.) 長輩", "respect (v.) 尊敬", "advice (n.) 建議"]
        },
        { 
            q: "14. She couldn't hide her _____s when she received the Exemplary Piety award for her sister.", options: ["effects", "emotions", "enemies", "elections"], ans: 1, hint: "當她代替妹妹領取孝行楷模獎時，她無法隱藏她的【情感 / 情緒】。",
            exp: "內心的感受、「情感、情緒」是 emotion。",
            grammarTip: "",
            vocab: ["emotion (n.) 情感/情緒", "hide (v.) 隱藏", "receive (v.) 領取/收到"]
        },
        { 
            q: "15. [文法] I planned the 2026 Tokyo trip itinerary all by _____.", options: ["me", "my", "mine", "myself"], ans: 3, hint: "我【全靠我自己】規畫了2026年東京之旅的行程。",
            exp: "主詞是 I (我)，表示「靠我自己」要用 by myself。",
            grammarTip: "這題是妳在課本第 36 頁完美寫對的喔！I 的反身代名詞就是 myself。",
            vocab: ["by myself (phr.) 靠我自己", "plan (v.) 計畫", "itinerary (n.) 行程"]
        },
        { 
            q: "16. Please remember to turn off the _____ fan before leaving the cream-colored living room.", options: ["empty", "effective", "electric", "elder"], ans: 2, hint: "離開奶油色的客廳前，請記得關掉【電】風扇。",
            exp: "需要用電才能運作的、「電的、電動的」是 electric。",
            grammarTip: "electric fan (電風扇)；electric car (電動車)。",
            vocab: ["electric (adj.) 電的/電動的", "turn off (phr.) 關閉", "fan (n.) 風扇"]
        },
        { 
            q: "17. The Chiayi City Government will _____ more workers for the new transportation project.", options: ["employ", "elect", "eat", "end"], ans: 0, hint: "嘉義市政府將為新的交通專案【僱用】更多工人。",
            exp: "花錢請人來工作、「僱用」的動詞是 employ。員工是 employee。",
            grammarTip: "",
            vocab: ["employ (v.) 僱用", "government (n.) 政府", "transportation (n.) 交通/運輸"]
        },
        { 
            q: "18. [文法] Those red yarn balls are nice, but I need the white _____ for this doll accessory.", options: ["one", "ones", "yarn", "one's"], ans: 1, hint: "那些紅色的毛線球很不錯，但我需要白色的【毛線球】來做這個娃娃配件。",
            exp: "前面提到的是 yarn balls (複數)，為了避免重複，後面要用不定代名詞的複數 ones。",
            grammarTip: "紅色的毛線球們 (red ones) ➔ 白色的毛線球們 (white ones)。",
            vocab: ["ones (pron.) 那些(東西)", "yarn ball (n.) 毛線球", "accessory (n.) 配件"]
        },
        { 
            q: "19. Be careful! Don't put the glass of water too close to the _____ of the dining table.", options: ["education", "edge", "effect", "effort"], ans: 1, hint: "小心！別把水杯放在太靠近餐桌【邊緣】的地方。",
            exp: "物體的邊界或「邊緣」是 edge。",
            grammarTip: "",
            vocab: ["edge (n.) 邊緣", "close to (phr.) 靠近", "dining table (n.) 餐桌"]
        },
        { 
            q: "20. [文法] Chin-chin learned how to make miniature charms all by _____.", options: ["her", "she", "hers", "herself"], ans: 3, hint: "芩芩【全靠她自己】學會了如何製作微型吊飾。",
            exp: "主詞是 Chin-chin (她)，靠她自己要用 by herself。",
            grammarTip: "she 的反身代名詞是 herself。all by herself = 完全靠她自己。",
            vocab: ["by herself (phr.) 靠她自己", "learn (v.) 學習", "miniature charm (n.) 微型吊飾"]
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
            
            var html = '<div class="score-title">🎉 升級測驗完成！<br>你的總分：' + score + ' / ' + quizData.length + '<br><span style="font-size: 0.8em; color: #5c6bc0;">(使用了 ' + hintsUsed + ' 次提示)</span></div>';
            
            if (wrongQuestions.length === 0) {
                html += '<div style="text-align: center; background: #e8f5e9; color: #1e4620; padding: 20px; border-radius: 12px; font-weight: bold; margin-top: 15px;">🌟 完美過關！反身代名詞跟 one/ones 完全難不倒你！恭喜解鎖新成就！🚀💯</div>';
            } else {
                html += '<div class="review-section">';
                html += '<div class="review-title">📕 你的專屬錯題與文法複習 (' + wrongQuestions.length + ' 題)</div>';
                html += '<div style="font-size:0.85em; color:#666; text-align:center; margin-bottom:12px;">把錯題小卡複習一下，下次考試絕對滿分！</div>';
                
                for (var w = 0; w < wrongQuestions.length; w++) {
                    var item = wrongQuestions[w];
                    var correctOpt = item.options[item.ans];
                    html += '<div class="wrong-card">';
                    html += '<div class="wrong-card-q">' + item.q + '</div>';
                    html += '<div class="wrong-card-ans">✅ 正確答案：' + correctOpt + '</div>';
                    html += '<div class="wrong-card-exp">💡 ' + item.exp + '</div>';
                    if (item.grammarTip) {
                        html += '<div style="color:#1976d2; font-size:0.9em; margin-bottom:6px;"><strong>🧑‍🏫 文法小提醒：</strong>' + item.grammarTip + '</div>';
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
            btn.style.background = "#3f51b5";
            btn.style.color = "white";
            feedback.innerHTML = "✅ 答對了！太讚了！🚀";
            feedback.className = "feedback correct";
            score++;
        } else {
            btn.style.background = "#9e9e9e";
            btn.style.color = "white";
            if (options[correctIndex]) {
                options[correctIndex].style.background = "#3f51b5";
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
