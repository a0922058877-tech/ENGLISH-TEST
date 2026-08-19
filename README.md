<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>英文單字+文法挑戰 (cut~deal & How問句特訓)</title>
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
            background: #8d6e63; /* 暖棕色取代原本的藍灰色 */
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
    <h1>🌱 單字+How問句特訓挑戰</h1>
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
            q: "1. The little boy looked so _____ when a broad smile spread over his face.", options: ["cute", "cut", "cruel", "curious"], ans: 0, hint: "那個小男孩滿臉微笑時看起來好【可愛】。",
            exp: "惹人喜愛的、「可愛的」形容詞是 cute。",
            grammarTip: "",
            vocab: ["cute (adj.) 可愛的", "smile (n.) 微笑", "spread (v.) 散開/展開"]
        },
        { 
            q: "2. [文法大魔王] Tom dances very well. ➔ _____ Tom _____?", options: ["How is / dances", "How does / dance", "How is / dance", "How does / dances"], ans: 1, hint: "湯姆跳舞跳得很好。 ➔ 湯姆跳舞跳得【如何】？",
            exp: "這題是課本第 25 頁妳訂正過的題目喔！問「一般動作(dance)」的狀況，一定要請助動詞 does 來幫忙，而且後面的動詞要打回原形 dance！",
            grammarTip: "陷阱口訣：有動作(dance)就不能用 is！用 does 幫忙後，動詞記得不加 s 喔！",
            vocab: ["dance (v.) 跳舞", "well (adv.) 很好地"]
        },
        { 
            q: "3. The old man is _____ in his left ear. You should speak louder.", options: ["dead", "dark", "deaf", "dangerous"], ans: 2, hint: "那位老先生左耳【耳聾 / 聽不見】了。你應該說大聲一點。",
            exp: "聽力受損、「耳聾的」形容詞是 deaf。",
            grammarTip: "speak louder 意思是「說大聲一點」。",
            vocab: ["deaf (adj.) 耳聾的", "speak (v.) 說話", "louder (adv.) 更大聲地"]
        },
        { 
            q: "4. Amy accidentally had a deep _____ on her chin when she fell down.", options: ["cute", "cut", "cup", "curve"], ans: 1, hint: "Amy 跌倒時，下巴不小心有了一道很深的【割傷】。",
            exp: "cut 當動詞是切或割，當名詞就是指「割傷、傷口」。",
            grammarTip: "cut 的動詞三態是同行：cut (現在) ➔ cut (過去) ➔ cut (過去分詞)。",
            vocab: ["cut (n./v.) 割傷 / 切割", "deep (adj.) 深的", "chin (n.) 下巴"]
        },
        { 
            q: "5. [文法大魔王] She teaches English happily. ➔ _____ she _____ English?", options: ["How is / teaches", "How do / teach", "How does / teach", "How is / teach"], ans: 2, hint: "她快樂地教英文。 ➔ 她【如何】教英文？",
            exp: "這題也是課本第 25 頁的重點！教書 (teaches) 是一般動詞，主詞是 She，所以要請 does 幫忙，然後把 teaches 打回原形 teach！",
            grammarTip: "絕對不能寫 How is she teaches 喔！記得是 How does she teach！",
            vocab: ["teach (v.) 教導", "happily (adv.) 快樂地"]
        },
        { 
            q: "6. She cried over her lost dog all night until _____ broke.", options: ["day", "date", "dawn", "dark"], ans: 2, hint: "她為走失的狗哭了一整晚，直到【破曉 / 黎明】。",
            exp: "清晨太陽剛出來的時候、「破曉、黎明」是 dawn。",
            grammarTip: "dawn broke 是一個很美的文學用法，意思是「破曉了、天亮了」。",
            vocab: ["dawn (n.) 破曉/黎明", "cry (v.) 哭泣", "until (prep.) 直到"]
        },
        { 
            q: "7. Some young people don't seem to care about the _____s of drug use.", options: ["dances", "dangers", "dates", "daughters"], ans: 1, hint: "有些年輕人似乎不在乎吸毒的【危險】。",
            exp: "可能會造成傷害的事物或「危險」名詞是 danger；dangerous 則是形容詞。",
            grammarTip: "in danger 意思是「處於危險之中」。",
            vocab: ["danger (n.) 危險", "care about (phr.) 在乎/關心", "drug use (n.) 吸毒"]
        },
        { 
            q: "8. [文法大魔王] The singer sang English songs well. ➔ _____ the singer _____ English songs?", options: ["How did / sing", "How is / sang", "How does / sing", "How did / sang"], ans: 0, hint: "歌手英文歌唱得很好。 ➔ 歌手【如何】唱英文歌？",
            exp: "這題是課本第 25 頁第 3 題的超級陷阱！因為 sang 是「過去式」，所以要請助動詞 did 來幫忙，而且後面的動詞要打回原形 sing！",
            grammarTip: "看到過去式 (sang) ➔ 請 did 幫忙 ➔ 動詞變回原形 (sing)！千萬不能寫 How is the singer sang 喔！",
            vocab: ["sing (v.) 唱歌", "sang (v.) sing的過去式", "well (adv.) 很好地"]
        },
        { 
            q: "9. Sam hates the life he is living: _____ in, _____ out, driving around town looking for passengers.", options: ["dawn", "date", "dark", "day"], ans: 0, hint: "Sam 討厭他現在的生活：【日】復一【日】，開車在城裡繞來繞去尋找乘客。",
            exp: "day in, day out 是一個固定片語，意思是「日復一日、天天如此」。",
            grammarTip: "day by day 意思是「一天天地」；day in, day out 強調枯燥重複的「日復一日」。",
            vocab: ["day in, day out (phr.) 日復一日", "drive around (phr.) 四處開車", "passenger (n.) 乘客"]
        },
        { 
            q: "10. Sticking your head out of the car window is very _____.", options: ["dangerous", "dead", "deaf", "dark"], ans: 0, hint: "把頭伸出車窗外是非常【危險的】。",
            exp: "會造成危險的、「危險的」形容詞是 dangerous。",
            grammarTip: "",
            vocab: ["dangerous (adj.) 危險的", "stick (v.) 伸出", "window (n.) 窗戶"]
        },
        { 
            q: "11. [文法] How are Kitty and Lily talking to each other? ➔ They are talking to each other _____.", options: ["happyly", "happy", "happily", "happyily"], ans: 2, hint: "Kitty 和 Lily 聊得如何？ ➔ 她們【快樂地】聊天。",
            exp: "這題是課本第 25 頁 Practice E 第 2 題的拼字陷阱！happy 的副詞必須「去 y 加 ily」，變成 happily。",
            grammarTip: "記得是 happily！絕對不能多留一個 y 寫成 happyily 喔！",
            vocab: ["talk (v.) 說話/聊天", "happily (adv.) 快樂地", "each other (pron.) 彼此"]
        },
        { 
            q: "12. Mr. Lee married his only _____ off to a rich man last month.", options: ["daughter", "date", "dance", "danger"], ans: 0, hint: "李先生上個月把他唯一的【女兒】嫁給了一個有錢人。",
            exp: "父母所生的女孩、「女兒」是 daughter。",
            grammarTip: "marry someone off 意思是「把...嫁出去」。",
            vocab: ["daughter (n.) 女兒", "marry (v.) 結婚/嫁娶", "rich (adj.) 富有的"]
        },
        { 
            q: "13. There are many difficulties and problem students to be _____ with in this school.", options: ["deaf", "dead", "dealt", "dawned"], ans: 2, hint: "這所學校裡有許多困難和問題學生需要被【處理 / 應付】。",
            exp: "deal with 意思是「處理、應付」。被動語態要用過去分詞 dealt (讀作 /dɛlt/)。",
            grammarTip: "動詞三態：deal (現在) ➔ dealt (過去) ➔ dealt (過去分詞)。",
            vocab: ["deal with (phr.) 處理/應付", "difficulty (n.) 困難", "student (n.) 學生"]
        },
        { 
            q: "14. [文法] How is Emily doing at school? ➔ She is doing _____ at school.", options: ["good", "well", "goodly", "better"], ans: 1, hint: "Emily 在學校表現如何？ ➔ 她在學校表現得【很好】。",
            exp: "修飾動詞 doing (表現) 必須用副詞！good 是形容詞，它的副詞是不規則變化的 well。",
            grammarTip: "這是妳在課本第 25 頁訂正過的題目！不能說 doing good，要說 doing well 喔！",
            vocab: ["do well (phr.) 表現良好", "school (n.) 學校"]
        },
        { 
            q: "15. The _____ collected from the samples are considered very useful for the report.", options: ["dates", "daughters", "data", "deals"], ans: 2, hint: "從樣本中收集到的【資料 / 數據】被認為對報告非常有用。",
            exp: "電腦資訊或實驗的「資料、數據」是 data。",
            grammarTip: "data 本身通常當作「複數名詞」使用，所以後面的 be 動詞是 are considered (被認為)。",
            vocab: ["data (n.) 資料/數據", "collect (v.) 收集", "useful (adj.) 有用的"]
        },
        { 
            q: "16. My sister is afraid of the _____, so she always leaves a small lamp on when she sleeps.", options: ["dance", "dawn", "day", "dark"], ans: 3, hint: "我妹妹怕【黑 / 黑暗】，所以她睡覺時總是留著一盞小燈。",
            exp: "沒有光線的「黑暗」是 dark；也可以當形容詞「黑暗的、深色的」。",
            grammarTip: "be afraid of the dark 意思是「怕黑」。",
            vocab: ["dark (n./adj.) 黑暗/深色的", "afraid (adj.) 害怕的", "lamp (n.) 燈"]
        },
        { 
            q: "17. [文法] I study hard. Kitty studies hard. ➔ I study _____ Kitty.", options: ["as hard as", "so hard as", "as hardly as", "hard as"], ans: 0, hint: "我用功讀書。Kitty 也用功讀書。 ➔ 我讀得【跟】Kitty【一樣用功】。",
            exp: "表示兩者程度一樣，要用 as + 副詞原形 + as 句型。",
            grammarTip: "副詞 hard (努力地) 本身就是原形，不需要改變。所以是 as hard as。不能寫 hardly 喔，hardly 是「幾乎不」的意思！",
            vocab: ["study (v.) 讀書/學習", "hard (adv.) 努力地/用功地"]
        },
        { 
            q: "18. The poor man was shot _____ at close range by the bad guy.", options: ["deaf", "dead", "dark", "dangerous"], ans: 1, hint: "那個可憐的男人在近距離被壞人開槍打【死】了。",
            exp: "失去生命、「死亡的」形容詞是 dead。",
            grammarTip: "die 是動詞 (死亡)；dead 是形容詞 (死亡的)；death 是名詞 (死亡)。",
            vocab: ["dead (adj.) 死亡的", "shoot (v.) 開槍(被動式was shot)", "close range (n.) 近距離"]
        },
        { 
            q: "19. They had only _____ed for three months before they got married.", options: ["danced", "dawned", "dated", "dealt"], ans: 2, hint: "他們在結婚前只【約會】了三個月。",
            exp: "date 當名詞是日期或約會，當動詞時就是「約會、交往」。",
            grammarTip: "have a date with... 是跟某人有個約會。",
            vocab: ["date (v./n.) 約會 / 日期", "get married (phr.) 結婚", "month (n.) 月"]
        },
        { 
            q: "20. [文法] He can run fast. I can run fast. ➔ He can run _____.", options: ["as fast as I", "as fast as me", "as fast as my", "fast as I"], ans: 0, hint: "他跑得快。我跑得快。 ➔ 他跑得【跟我一樣快】。",
            exp: "這題是妳在課本第 23 頁寫對的題目！as fast as 後面要接主格代名詞 I (因為其實是省略了 as I can)。",
            grammarTip: "在正式文法中，as fast as 後面接主詞 I (He can run as fast as I) 才是最標準的寫法喔！",
            vocab: ["run (v.) 跑步", "fast (adv.) 快速地"]
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
                html += '<div style="text-align: center; background: #e8f5e9; color: #1e4620; padding: 20px; border-radius: 12px; font-weight: bold; margin-top: 15px;">🌟 太神啦！全部答對！How 問句的大魔王陷阱完全被你破解了！💯</div>';
            } else {
                html += '<div class="review-section">';
                html += '<div class="review-title">📕 你的專屬錯題與文法複習 (' + wrongQuestions.length + ' 題)</div>';
                html += '<div style="font-size:0.85em; color:#666; text-align:center; margin-bottom:12px;">把錯題小卡複習一下，下次遇到 How 問句一定會記得找 do/does/did 幫忙！</div>';
                
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
