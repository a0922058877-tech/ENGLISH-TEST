<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>英文單字+文法挑戰 (bug~by & Which比較級問句)</title>
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
    <h1>🌱 單字+Which比較級挑戰</h1>
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
            q: "1. [文法] Which animal is _____, the panda or the giraffe?", options: ["cute", "cuter", "more cute", "cuter than"], ans: 1, hint: "哪一種動物【比較可愛】，熊貓還是長頸鹿？",
            exp: "句型「Which is + 比較級, A or B?」中，詢問二選一誰比較怎樣，形容詞一定要變成比較級！cute 加上 -r 變成 cuter。",
            grammarTip: "注意課本第6頁 Practice G 第1題陷阱：不能只寫原級 cute，一定要寫比較級 cuter！而且結尾有 or B? 時，切記不可再加 than 喔！",
            vocab: ["cute (adj.) 可愛", "cuter (adj.) 比較可愛的", "giraffe (n.) 長頸鹿"]
        },
        { 
            q: "2. The old man sells steamed _____s at a street market every morning.", options: ["bun", "bug", "bus", "button"], ans: 0, hint: "位老先生每天早上在街頭市場賣蒸【饅頭 / 小圓麵包】。",
            exp: "蒸的包子、饅頭或是漢堡用的小圓麵包，英文都是 bun (steamed buns = 蒸饅頭/包子)。",
            grammarTip: "bun 也可以指女生綁頭髮的「包包頭」，如: have her hair in a bun。",
            vocab: ["bun (n.) 小圓麵包/饅頭", "steamed (adj.) 蒸熟的", "market (n.) 市場"]
        },
        { 
            q: "3. [文法] Which books _____ easier, the blue ones or the yellow ones?", options: ["is", "are", "do", "does"], ans: 1, hint: "哪一些書【是】比較簡單的，藍色的還是黃色的？",
            exp: "主詞 Which books 以及選項 the blue ones 都是「複數」，因此 be 動詞一定要選複數的 are！",
            grammarTip: "如果問 Which book is easier, the blue one or... (單數用 is)；如果是 Which books are... (複數務必用 are)！",
            vocab: ["easy (adj.) 簡單的", "easier (adj.) 比較簡單的", "one / ones (pron.) 代名詞(單/複數)"]
        },
        { 
            q: "4. Our school is a very tall _____ of twelve floors.", options: ["building", "bundle", "business", "butter"], ans: 0, hint: "我們學校是一棟十二層樓高的高大【建築物 / 大樓】。",
            exp: "由動詞 build (蓋/建造) 加上 -ing 變成的名詞 building，意思就是「建築物、大樓」。",
            grammarTip: "動詞三態：build (現在) ➔ built (過去式) ➔ built (過去分詞)，字尾 d 變成 t！",
            vocab: ["building (n.) 建築物", "floor (n.) 樓層", "school (n.) 學校"]
        },
        { 
            q: "5. He carried a heavy _____ of newspapers in his arms to recycle.", options: ["button", "butterfly", "bundle", "bus"], ans: 2, hint: "他懷裡抱著一重【捆 / 束】報紙去回收。",
            exp: "捆在一起的一束、一捆物品叫做 bundle (a bundle of newspapers = 一捆報紙)。",
            grammarTip: "bundle 也常作動詞用，意思是「把...捆紮在一起」(bundle ... up/together)。",
            vocab: ["bundle (n./v.) 捆 / 綁在一起", "newspaper (n.) 報紙", "carry (v.) 攜帶/抱著"]
        },
        { 
            q: "6. [文法] Which camera is _____, the big one or the small one?", options: ["cheap", "more cheap", "cheaper", "cheaper than"], ans: 2, hint: "哪一相機【比較便宜】，大台的還是小台的？",
            exp: "單音節 cheap 的比較級是 cheaper。這是「Which is..., A or B?」比較問句，務必使用比較級 cheaper！",
            grammarTip: "再次提醒：問「哪一個比較便宜」不能寫 Which camera is cheap，一定要加 -er 寫成 cheaper 喔！",
            vocab: ["cheap (adj.) 便宜的", "cheaper (adj.) 比較便宜的", "camera (n.) 相機"]
        },
        { 
            q: "7. Be careful with the hot stove, or you might _____ your finger!", options: ["burn", "build", "burst", "buy"], ans: 0, hint: "小心燙手爐子，否則你可能會【燙傷 / 燒傷】手指！",
            exp: "被火或高溫「燒傷、燙傷、燃燒」的動詞是 burn；過去式為 burned 或 burnt。",
            grammarTip: "burn 除了當動詞，也可當名詞「燙傷傷口」(He has serious burns on his arm.)。",
            vocab: ["burn (v./n.) 燒傷/燙傷", "stove (n.) 爐子", "finger (n.) 手指"]
        },
        { 
            q: "8. There was a sudden _____ in the gas pipe, so we called for help immediately.", options: ["button", "burst", "bus", "butterfly"], ans: 1, hint: "瓦斯管線突然發生【爆裂 / 破裂】，所以我們立刻打電話求助。",
            exp: "水管或氣體管線「爆裂、破裂」是 burst；可以作動詞也可作名詞。",
            grammarTip: "特殊三態不變：burst (現在) ➔ burst (過去) ➔ burst (過去分詞)，三態都長得一模一樣喔！",
            vocab: ["burst (v./n.) 爆裂", "gas pipe (n.) 瓦斯管", "sudden (adj.) 突然的"]
        },
        { 
            q: "9. [文法] Which subject is _____, English or math?", options: ["more easy", "easier", "easy", "easier than"], ans: 1, hint: "哪一門科目【比較簡單】，英文還是數學？",
            exp: "easy 字尾是 y，比較級規則為「去 y 加 ier」變成 easier。絕對不能說 more easy！",
            grammarTip: "易錯陷阱：easy / busy / happy / heavy 這類 y 結尾形容詞，比較級一定都是加 -ier (easier/busier)，不要用 more 喔！",
            vocab: ["subject (n.) 科目", "easier (adj.) 比較簡單的", "math (n.) 數學"]
        },
        { 
            q: "10. Chin-chin got on the _____ at Taipei 101 and went home.", options: ["bus", "bun", "bug", "button"], ans: 0, hint: "芩芩在台北 101 上了【公車 / 巴士】然後回家。",
            exp: "大眾交通工具「公車」是 bus；上公車是 get on the bus，下公車則是 get off the bus。",
            grammarTip: "bus 的複數形記得在字尾加上 -es 變成 buses。",
            vocab: ["bus (n.) 公車", "get on (phr.) 上車", "get off (phr.) 下車"]
        },
        { 
            q: "11. My uncle started his own family _____ when he was only 25 years old.", options: ["building", "business", "butter", "button"], ans: 1, hint: "我叔叔在年僅25歲時就創立了自己的家族【事業 / 生意】。",
            exp: "公司企業或「生意、事業」是 business；start a business 表示「創業」。",
            grammarTip: "on business 是常用片語，意思是「因公出差」(He went to Japan on business.)。",
            vocab: ["business (n.) 生意/事業", "start (v.) 創立/開始", "family (n.) 家族/家庭"]
        },
        { 
            q: "12. A successful _____ often wears a neat suit and carries a briefcase.", options: ["butterfly", "button", "businessman", "bundle"], ans: 2, hint: "位成功的【商人 / 企業家】常穿著整齊西裝並提著公事包。",
            exp: "從事商業活動的男士或「商人」是 businessman (複數把 man 改為 men ➔ businessmen)。",
            grammarTip: "business (商業) + man (男人) = businessman (商人)。",
            vocab: ["businessman (n.) 商人", "successful (adj.) 成功的", "suit (n.) 西裝"]
        },
        { 
            q: "13. [文法] _____ has more windows, the yellow house or the pink house?", options: ["What", "Which", "Who", "Where"], ans: 1, hint: "【哪一個】有比較多窗戶，黃色房子還是粉紅房子？",
            exp: "課本 1-8 單元問句：「Which + has + more + 名詞, A or B?」，詢問二選一「哪一個」必定用疑問詞 Which。",
            grammarTip: "Which 作為疑問代名詞時，可以單獨使用 (Which is better?)，也可接名詞 (Which house has more windows?)。",
            vocab: ["Which (pron./adj.) 哪一個", "window (n.) 窗戶", "more (adj.) 更多的"]
        },
        { 
            q: "14. Most parents are very _____ making money to take care of their children.", options: ["busy", "brief", "brave", "boring"], ans: 0, hint: "大多數父母都非常【忙碌於】賺錢來照顧小孩。",
            exp: "形容事務繁多、沒有空閒的「忙碌的」是 busy；be busy + V-ing 表示「忙著做某事」。",
            grammarTip: "再次複習 busy 的比較級：去 y 加 ier ➔ busier (My father is busier than my mother.)。",
            vocab: ["busy (adj.) 忙碌的", "make money (phr.) 賺錢", "take care of (phr.) 照顧"]
        },
        { 
            q: "15. I wanted to buy that pretty dress, _____ I didn't have enough money.", options: ["but", "by", "or", "so"], ans: 0, hint: "我想買那件漂亮的洋裝，【但是】我沒有足夠的錢。",
            exp: "連接前後兩個語氣轉折或相反的句子，要用表示「但是、卻」的連接詞 but。",
            grammarTip: "英文裡 but (但是) 和 although/though (雖然) 不能同時出現在同一個句子裡喔！",
            vocab: ["but (conj.) 但是", "enough (adj.) 足夠的", "pretty (adj.) 漂亮的"]
        },
        { 
            q: "16. I spread some sweet cream and yellow _____ over my warm toast.", options: ["button", "butterfly", "butter", "bun"], ans: 2, hint: "我在溫熱吐司上塗了一些甜奶油和黃色【奶油 / 牛油】。",
            exp: "用牛奶製成、塗麵包或做甜點的「奶油 / 牛油」是 butter (不可數名詞)。",
            grammarTip: "butter 也可以直接當動詞，意思是「塗奶油於...」(butter the toast)。",
            vocab: ["butter (n.) 奶油/牛油", "spread (v.) 塗抹/鋪開", "toast (n.) 吐司"]
        },
        { 
            q: "17. Look! Two beautiful colorful _____ies are flying among the flowers in the garden.", options: ["button", "butterfly", "business", "bundle"], ans: 1, hint: "看！兩隻美麗多彩的【蝴蝶】正在花園的花朵間飛舞。",
            exp: "有美麗翅膀的昆蟲「蝴蝶」是 butterfly (單數)；複數記得去 y 加 ies ➔ butterflies。",
            grammarTip: "butter (奶油) + fly (飛) 拼在一起就是 butterfly (蝴蝶)！",
            vocab: ["butterfly (n.) 蝴蝶", "colorful (adj.) 多彩的", "garden (n.) 花園"]
        },
        { 
            q: "18. Oh no! A small round _____ came off my school shirt.", options: ["button", "butter", "bus", "bug"], ans: 0, hint: "噢不！一顆圓形小【鈕扣】從我的制服襯衫上掉下來了。",
            exp: "衣服上的「鈕扣」或是機器上面的「按鈕」，英文都是 button。",
            grammarTip: "button 也可以作動詞，button up my coat 意思是「把外套的扣子扣起來」。",
            vocab: ["button (n./v.) 鈕扣 / 扣好", "shirt (n.) 襯衫", "come off (phr.) 脫落/掉下"]
        },
        { 
            q: "19. I _____ a new laptop on the Internet for NT$15,000 yesterday.", options: ["buy", "bought", "build", "built"], ans: 1, hint: "昨天我網路上花了一萬五千元【買了】一台新筆電。",
            exp: "動詞 buy (購買) 的過去式與過去分詞都是 bought (讀作 /bɔt/)；因為有 yesterday (昨天)，務必選過去式 bought。",
            grammarTip: "超級必背三態：buy (現在) ➔ bought (過去) ➔ bought (過去分詞)！切勿寫成 buyed 喔！",
            vocab: ["buy (v.) 購買", "bought (v.) buy的過去式", "Internet (n.) 網際網路"]
        },
        { 
            q: "20. The dress is a good _____ at only NT$500. It's really cheap!", options: ["buy", "by", "but", "bug"], ans: 0, hint: "這件洋裝只要 500 元，真是個劃算的【買賣 / 好貨】！真便宜！",
            exp: "buy 除了當動詞，也可以當名詞。a good buy 意思是「物超所值的好買賣、劃算好貨」。",
            grammarTip: "這題考課本第42頁的最上方標題短句：The dress is a good buy at NT$1,200. (買得真劃算)。",
            vocab: ["a good buy (n.) 劃算的好買賣", "cheap (adj.) 便宜的", "dress (n.) 洋裝"]
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
                html += '<div style="text-align: center; background: #e8f5e9; color: #1e4620; padding: 20px; border-radius: 12px; font-weight: bold; margin-top: 15px;">🌟 太厲害了！全部答對，沒有任何錯題！Which 比較級問句和 B 開頭單字已經完全制霸！💯</div>';
            } else {
                html += '<div class="review-section">';
                html += '<div class="review-title">📕 你的專屬錯題與文法複習 (' + wrongQuestions.length + ' 題)</div>';
                html += '<div style="font-size:0.85em; color:#666; text-align:center; margin-bottom:12px;">把錯題小卡複習一下，下次「Which is + 比較級」絕不再漏掉 -er 囉！</div>';
                
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
