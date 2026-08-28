<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>英文單字+文法挑戰 (everywhere~eye & 不定代名詞)</title>
    <style>
        * { box-sizing: border-box; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background-color: #fdf5e6; /* 溫暖的晨曦橘背景 */
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
            box-shadow: 0 8px 24px rgba(230, 81, 0, 0.15);
            margin: 0 auto;
        }
        h1 {
            text-align: center;
            color: #e65100; /* 深橘色 */
            font-size: 1.18em;
            border-bottom: 2px dashed #ffcc80;
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
            background: #1565c0; /* 深海藍 */
            color: white;
            padding: 6px 12px;
            border: none;
            border-radius: 8px;
            font-size: 0.85em;
            cursor: pointer;
            font-weight: bold;
        }
        #q-counter {
            color: #e65100;
            font-size: 0.85em;
            font-weight: bold;
        }
        .question {
            font-size: 1.12em;
            font-weight: bold;
            margin-bottom: 16px;
            min-height: 54px;
            color: #0d47a1;
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
            background: #e3f2fd;
            border: 2px solid transparent;
            border-radius: 12px;
            cursor: pointer;
            font-size: 0.98em;
            text-align: left;
            color: #0d47a1;
            transition: all 0.2s;
            -webkit-tap-highlight-color: transparent;
        }
        .option:active {
            transform: scale(0.98);
            background: #bbdefb;
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
            background-color: #fff3e0;
            border-left: 4px solid #e65100;
            padding: 14px;
            margin-bottom: 18px;
            border-radius: 8px;
            font-size: 0.9em;
            line-height: 1.6;
        }
        .explanation-box h4 {
            margin: 0 0 8px 0;
            color: #e65100;
            font-size: 1.02em;
        }
        .grammar-tip {
            background-color: #e3f2fd;
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
            background: #e65100;
            color: white;
            padding: 14px;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-size: 1.05em;
            width: 100%;
            font-weight: bold;
            box-shadow: 0 3px 10px rgba(230, 81, 0, 0.3);
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
            color: #e65100;
            margin-bottom: 15px;
        }
        .review-section {
            margin-top: 20px;
            border-top: 2px dashed #ffcc80;
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
            background: #e65100;
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
    <h1>🌅 單字+文法 特訓挑戰</h1>
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
            q: "1. You must pass the entrance _____ if you want to be admitted to the university.", options: ["example", "exam", "excuse", "eye"], ans: 1, hint: "如果你想被大學錄取，你必須通過入學【考試】。",
            exp: "用來測驗能力的「考試、測驗」是 exam (或 examination)。",
            grammarTip: "",
            vocab: ["exam (n.) 考試", "entrance exam (n.) 入學考試", "pass (v.) 通過"]
        },
        { 
            q: "2. [文法] Raise your right hand, and wave _____ hand.", options: ["another", "other", "the other", "others"], ans: 2, hint: "舉起你的右手，並揮動【另一隻】手。",
            exp: "人只有兩隻手，所以「除了右手之外的另一隻手」，就是「兩者之中特定的另一個」，必須用 the other。",
            grammarTip: "身體部位陷阱題！因為手只有兩隻，所以「另一隻手」一定是 the other hand。",
            vocab: ["the other (pron.) 兩者中的另一個", "raise (v.) 舉起", "wave (v.) 揮動"]
        },
        { 
            q: "3. Chin-chin is an _____ in making miniature crochet charms. They are beautiful!", options: ["example", "expert", "export", "exercise"], ans: 1, hint: "芩芩是製作微型鉤織吊飾的【專家】。它們好漂亮！",
            exp: "在某個領域非常有經驗或技術的人、「專家」是 expert。",
            grammarTip: "be an expert in/on... 意思是「是...方面的專家」。",
            vocab: ["expert (n.) 專家", "crochet (v./n.) 鉤織", "miniature charm (n.) 微型吊飾"]
        },
        { 
            q: "4. The doctor _____ed me to see whether there was anything wrong with my heart.", options: ["excited", "excused", "examined", "expressed"], ans: 2, hint: "醫生【檢查】我，看看我的心臟是否有什麼毛病。",
            exp: "仔細查看或「檢查、診察」的動詞是 examine。",
            grammarTip: "examine someone (檢查某人身體)。",
            vocab: ["examine (v.) 檢查", "doctor (n.) 醫生", "heart (n.) 心臟"]
        },
        { 
            q: "5. [文法] Here are three hats. One is orange, _____ is blue, and the other is white.", options: ["another", "the other", "other", "any"], ans: 0, hint: "這裡有三頂帽子。一頂是橘色，【另一頂】是藍色，最後一頂是白色。",
            exp: "在「三個」物品中，第一個是 One，第二個(不特定的另一個) 是 another，最後剩下那一個(特定的) 則是 the other。",
            grammarTip: "三個物品的順序公式：One..., another..., and the other...！",
            vocab: ["another (pron.) 另一個(不特定)", "hat (n.) 帽子", "orange (adj.) 橘色的"]
        },
        { 
            q: "6. We are going to Tokyo in 2026! But I heard the hotels there can be very _____.", options: ["excellent", "exciting", "expensive", "exact"], ans: 2, hint: "我們2026年要去東京！但我聽說那裡的飯店可能會非常【昂貴的】。",
            exp: "花費很多錢、「昂貴的」形容詞是 expensive。",
            grammarTip: "",
            vocab: ["expensive (adj.) 昂貴的", "hotel (n.) 飯店", "hear (v.) 聽說"]
        },
        { 
            q: "7. Jane sounded really _____ to learn that you are going to invite her out.", options: ["exciting", "excited", "excellent", "extra"], ans: 1, hint: "珍聽起來真的感到很【興奮的】，當她得知你要邀請她出去。",
            exp: "形容「人」感到興奮的，要用 -ed 結尾的 excited。",
            grammarTip: "人 + be/sound excited (人感到興奮)；事/物 + be exciting (令人興奮的)。",
            vocab: ["excited (adj.) 感到興奮的", "invite (v.) 邀請", "sound (v.) 聽起來"]
        },
        { 
            q: "8. [文法] Can you close one eye and open _____ one?", options: ["another", "other", "others", "the other"], ans: 3, hint: "你能閉上一隻眼睛並睜開【另一隻】眼睛嗎？",
            exp: "跟手一樣，人只有兩隻眼睛，所以「另一隻眼睛」是兩者中特定剩下的那一個，要用 the other。",
            grammarTip: "妳在課本第 40 頁完美寫對的題目！身體器官(一對的) = the other。",
            vocab: ["the other (pron.) 兩者中的另一個", "close (v.) 閉上", "open (v.) 睜開/打開"]
        },
        { 
            q: "9. The museum is open every day _____ Mondays. It is closed on Mondays.", options: ["except", "exact", "expect", "excuse"], ans: 0, hint: "這家博物館每天都開放，【除了】星期一之外。它在星期一休館。",
            exp: "表示「除...之外」的介系詞是 except。",
            grammarTip: "",
            vocab: ["except (prep.) 除了...之外", "museum (n.) 博物館", "open (adj.) 開放的"]
        },
        { 
            q: "10. He took himself as an _____ of why working hard does not necessarily lead to success.", options: ["exercise", "exam", "exit", "example"], ans: 3, hint: "他以自己為【例子 / 範例】，說明努力工作未必會帶來成功。",
            exp: "用來說明情況的「例子、範例」是 example。",
            grammarTip: "for example 意思是「舉例來說」；set an example 意思是「樹立典範」。",
            vocab: ["example (n.) 例子/範例", "working hard (phr.) 努力工作", "success (n.) 成功"]
        },
        { 
            q: "11. [文法] I only had one slice of the bread we baked. It's so good! Let's have _____.", options: ["another", "the other", "other", "the others"], ans: 0, hint: "我只吃了一片我們烤的麵包。太好吃了！我們【再來一片】吧。",
            exp: "想要在眾多麵包中「再來一片/再吃一個」，表示「不特定的另一個」，要用 another。",
            grammarTip: "想要「再來一個 (one more)」，請記得用 another 喔！",
            vocab: ["another (pron.) 另一個(不特定)", "slice (n.) 一片", "bake (v.) 烘烤"]
        },
        { 
            q: "12. I couldn't _____ what a surprise it was to see that you had aged so much.", options: ["export", "expect", "express", "examine"], ans: 2, hint: "看到你變得這麼蒼老，我無法【表達】這有多麼令人驚訝。",
            exp: "把心裡的想法說出來、「表達」的動詞是 express。",
            grammarTip: "express 也可以當形容詞「快速的」，如 express train (快車)。",
            vocab: ["express (v.) 表達", "surprise (n.) 驚訝", "age (v.) 老化"]
        },
        { 
            q: "13. In order to stay healthy, we must _____ regularly instead of sitting all day.", options: ["excuse", "exercise", "exist", "expect"], ans: 1, hint: "為了保持健康，我們必須規律地【運動】，而不是整天坐著。",
            exp: "進行體能活動、「運動、鍛鍊」是 exercise。",
            grammarTip: "exercise 當作「運動」時通常是不可數名詞；當作「習題 (exercises)」時可數。",
            vocab: ["exercise (v./n.) 運動", "regularly (adv.) 規律地", "healthy (adj.) 健康的"]
        },
        { 
            q: "14. Please _____ me for calling you so late. I have an emergency.", options: ["excuse", "examine", "export", "eye"], ans: 0, hint: "請【原諒 / 寬恕】我這麼晚打電話給你。我有緊急情況。",
            exp: "原諒別人的小過失是 excuse。",
            grammarTip: "Excuse me. (不好意思 / 請問一下) 就是從這個字來的。",
            vocab: ["excuse (v./n.) 原諒/藉口", "call (v.) 打電話", "emergency (n.) 緊急情況"]
        },
        { 
            q: "15. [文法] I don't like this cream-colored hat. Show me _____.", options: ["another", "the other", "other", "any"], ans: 0, hint: "我不喜歡這頂奶油色的帽子。給我看【另一頂】帽子。",
            exp: "店裡的帽子有很多頂，想看「不特定的另一頂」，所以要用 another。",
            grammarTip: "「給我看另一個」通常是在眾多選擇中再挑一個，所以是 Show me another。",
            vocab: ["another (pron.) 另一個(不特定)", "cream-colored (adj.) 奶油色的", "hat (n.) 帽子"]
        },
        { 
            q: "16. The wine was _____, so we drank into the night.", options: ["evil", "exact", "excellent", "extra"], ans: 2, hint: "那酒棒極了 / 非常【優秀的】，所以我們喝到深夜。",
            exp: "極好的、非常棒的形容詞是 excellent。",
            grammarTip: "",
            vocab: ["excellent (adj.) 優秀的/極好的", "wine (n.) 葡萄酒", "drank (v.) drink的過去式"]
        },
        { 
            q: "17. The job requires not only skills but also at least three years' work _____.", options: ["exam", "exit", "experience", "example"], ans: 2, hint: "這份工作不僅需要技能，還需要至少三年的工作【經驗】。",
            exp: "親身經歷或做過的事、「經驗」是 experience。",
            grammarTip: "experience 當作「經驗」是不可數名詞；當作「經歷的事件 (experiences)」時可數。",
            vocab: ["experience (n.) 經驗/經歷", "require (v.) 需要", "skill (n.) 技能"]
        },
        { 
            q: "18. The doctor _____ed to me what I should do when my child is running a fever.", options: ["expected", "explained", "exported", "exited"], ans: 1, hint: "醫生向我【解釋】當我的孩子發燒時我該怎麼辦。",
            exp: "把事情說清楚讓人明白、「解釋、說明」的動詞是 explain。",
            grammarTip: "explain something to someone (向某人解釋某事)。",
            vocab: ["explain (v.) 解釋", "run a fever (phr.) 發燒", "child (n.) 孩子"]
        },
        { 
            q: "19. We need an _____ three people to play baseball. We only have six now.", options: ["extra", "exact", "evil", "expert"], ans: 0, hint: "我們需要【額外的】三個人才能打棒球。我們現在只有六個。",
            exp: "超出原本數量的、「額外的、多加的」是 extra。",
            grammarTip: "an extra three people 意思是「額外再加三個人」。",
            vocab: ["extra (adj.) 額外的", "play baseball (phr.) 打棒球", "people (n.) 人們"]
        },
        { 
            q: "20. We quickly _____ed through the back door when the fire alarm rang.", options: ["existed", "exited", "excited", "exercised"], ans: 1, hint: "當火災警報響起時，我們迅速從後門【離開 / 退出】。",
            exp: "離開建築物或「退出、出去」的動詞是 exit。",
            grammarTip: "exit 當名詞時就是我們常在門口看到的「出口」標示。",
            vocab: ["exit (v./n.) 離開/出口", "back door (n.) 後門", "fire alarm (n.) 火災警報"]
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
            
            var html = '<div class="score-title">🎉 測驗完成！<br>你的總分：' + score + ' / ' + quizData.length + '<br><span style="font-size: 0.8em; color: #e65100;">(使用了 ' + hintsUsed + ' 次提示)</span></div>';
            
            if (wrongQuestions.length === 0) {
                html += '<div style="text-align: center; background: #e3f2fd; color: #0d47a1; padding: 20px; border-radius: 12px; font-weight: bold; margin-top: 15px;">🌟 完美過關！another 和 the other 這些魔王陷阱完全被你破解了！🚀💯</div>';
            } else {
                html += '<div class="review-section">';
                html += '<div class="review-title">📕 你的專屬錯題與文法複習 (' + wrongQuestions.length + ' 題)</div>';
                html += '<div style="font-size:0.85em; color:#666; text-align:center; margin-bottom:12px;">把錯題小卡複習一下，下次遇到 another 絕對能秒殺它！</div>';
                
                for (var w = 0; w < wrongQuestions.length; w++) {
                    var item = wrongQuestions[w];
                    var correctOpt = item.options[item.ans];
                    html += '<div class="wrong-card">';
                    html += '<div class="wrong-card-q">' + item.q + '</div>';
                    html += '<div class="wrong-card-ans">✅ 正確答案：' + correctOpt + '</div>';
                    html += '<div class="wrong-card-exp">💡 ' + item.exp + '</div>';
                    if (item.grammarTip) {
                        html += '<div style="color:#0d47a1; font-size:0.9em; margin-bottom:6px;"><strong>🧑‍🏫 文法小提醒：</strong>' + item.grammarTip + '</div>';
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
            btn.style.background = "#1565c0";
            btn.style.color = "white";
            feedback.innerHTML = "✅ 答對了！太讚了！🚀";
            feedback.className = "feedback correct";
            score++;
        } else {
            btn.style.background = "#9e9e9e";
            btn.style.color = "white";
            if (options[correctIndex]) {
                options[correctIndex].style.background = "#1565c0";
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
