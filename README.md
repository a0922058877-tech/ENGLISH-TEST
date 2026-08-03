<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>小學生英文單字挑戰 (blank ~ bored 100%相容版)</title>
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
    <h1>🌱 英文單字挑戰 (blank ~ bored) 🌱</h1>
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
            q: "1. It is cold tonight. Pull the warm _____ up to your chin and go to sleep.", options: ["blouse", "blanket", "board", "body"], ans: 1, hint: "今晚很冷。把溫暖的【毯子】拉到下巴然後睡覺。",
            exp: "晚上睡覺蓋在身上禦寒的「毛毯 / 毯子」是 blanket。", vocab: ["blanket (n.) 毯子", "cold (adj.) 寒冷的", "sleep (v.) 睡覺"]
        },
        { 
            q: "2. The sky is very clear and _____ today. Let's go to the beach!", options: ["blue", "blind", "bored", "blank"], ans: 0, hint: "今天的天空非常晴朗且呈現【藍色】。我們去海灘吧！",
            exp: "天空與海洋常見的顏色「藍色的」是 blue。這裡也是標準的 be + very + 形容詞原級喔！", vocab: ["blue (adj.) 藍色的", "sky (n.) 天空", "beach (n.) 海灘"]
        },
        { 
            q: "3. A guide dog can help a _____ person walk safely on the street.", options: ["bored", "blank", "blind", "blue"], ans: 2, hint: "導盲犬可以幫助【失明的 / 看不見的】人在街上安全地行走。",
            exp: "眼睛看不見、失明的人稱為 blind person；導盲犬則是 guide dog。", vocab: ["blind (adj.) 失明的", "safely (adv.) 安全地", "street (n.) 街道"]
        },
        { 
            q: "4. He cut his finger on broken glass and lost a lot of red _____.", options: ["body", "bone", "bomb", "blood"], ans: 3, hint: "他被碎玻璃割傷手指，流了很多紅色的【血】。",
            exp: "受傷流出來的「血液」是 blood (不可數名詞)；lose blood 表示「失血」。", vocab: ["blood (n.) 血", "cut (v.) 割傷", "finger (n.) 手指"]
        },
        { 
            q: "5. Mom bought a pretty white _____ with small buttons to wear to work.", options: ["blouse", "blanket", "bookcase", "boat"], ans: 0, hint: "媽媽買了一件有小鈕扣的漂亮白色【女用襯衫】穿去上班。",
            exp: "專指女性穿的「女裝襯衫 / 上衣」稱為 blouse。", vocab: ["blouse (n.) 女用襯衫", "button (n.) 鈕扣", "pretty (adj.) 漂亮的"]
        },
        { 
            q: "6. Please move your car! It is _____ing the road and we can't pass.", options: ["boil", "block", "blow", "board"], ans: 1, hint: "請把你的車移開！它【擋住 / 阻塞】了道路，我們無法通過。",
            exp: "block 當動詞時，意思是「阻塞、擋住 (道路或視線)」。", vocab: ["block (v.) 擋住/阻塞", "road (n.) 道路", "move (v.) 移動"]
        },
        { 
            q: "7. Be careful! The soup is very hot, so _____ on it before you eat.", options: ["boil", "block", "blow", "book"], ans: 2, hint: "小心！湯很熱，吃之前先在上面【吹氣】使它涼一點。",
            exp: "用嘴巴「吹氣 (讓他降溫或吹熄蠟燭)」的動詞是 blow (過去式是 blew)。", vocab: ["blow (v.) 吹", "soup (n.) 湯", "careful (adj.) 小心的"]
        },
        { 
            q: "8. I was so nervous during the test that my mind went completely _____.", options: ["blue", "blind", "bored", "blank"], ans: 3, hint: "我在考試時太緊張了，腦袋一片【空白】。",
            exp: "one's mind went blank 是固定說法，形容緊張到「腦袋一片空白、什麼都想不起來」。", vocab: ["blank (adj.) 空白的", "mind (n.) 心智/腦海", "nervous (adj.) 緊張的"]
        },
        { 
            q: "9. Jimmy exercises every day, so he has a very strong and healthy _____.", options: ["body", "bone", "boat", "block"], ans: 0, hint: "吉米每天運動，所以他有一個很強壯健康的【身體】。",
            exp: "經由運動鍛鍊得強壯健康的「身體」是 body。", vocab: ["body (n.) 身體", "exercise (v.) 運動", "strong (adj.) 強壯的"]
        },
        { 
            q: "10. We took a small wooden _____ to cross the wide river.", options: ["bomb", "boat", "body", "book"], ans: 1, hint: "我們搭乘一艘木製小【船】渡過寬闊的河流。",
            exp: "在河面上航行的小船是 boat；大客船或貨輪則是 ship。", vocab: ["boat (n.) 小船", "river (n.) 河流", "wooden (adj.) 木頭製的"]
        },
        { 
            q: "11. Please keep the water _____ing for three more minutes to make tea.", options: ["blowing", "blocking", "boiling", "boarding"], ans: 2, hint: "請讓水繼續【沸騰 / 煮滾】三分多鐘來泡茶。",
            exp: "讓水「煮滾、沸騰」的動詞是 boil；boiling water 就是滾燙的熱水。", vocab: ["boil (v.) 沸騰/煮", "water (n.) 水", "minute (n.) 分鐘"]
        },
        { 
            q: "12. Our dog loves to chew on a big beef _____ after dinner.", options: ["boat", "bomb", "body", "bone"], ans: 3, hint: "我們的狗喜歡在晚餐後啃一支大大的牛肉【骨頭】。",
            exp: "動物或人體內的「骨頭」是 bone；破了骨頭 (骨折) 是 break a bone。", vocab: ["bone (n.) 骨頭", "chew (v.) 咀嚼/啃", "dinner (n.) 晚餐"]
        },
        { 
            q: "13. Chin-chin felt _____ because it rained all day and she had nothing to do.", options: ["bored", "blind", "blank", "blue"], ans: 0, hint: "芩芩感到很【無聊 / 厭煩】，因為下了一整天的雨，她沒事可做。",
            exp: "形容人的感受「感到無聊、無趣的」要用字尾 -ed 的 bored (主詞通常是人)。", vocab: ["bored (adj.) 感到無聊的", "rain (v.) 下雨", "nothing (pron.) 沒什麼事"]
        },
        { 
            q: "14. We need to buy a new wooden _____ to put all these comic books.", options: ["blanket", "bookcase", "blouse", "body"], ans: 1, hint: "我們需要買一個新的木頭【書架 / 書櫃】來放這些漫畫書。",
            exp: "專門用來擺放書本的「書櫃 / 書架」是 bookcase (也叫做 bookshelf)。", vocab: ["bookcase (n.) 書櫃", "comic book (n.) 漫畫書", "wooden (adj.) 木製的"]
        },
        { 
            q: "15. All passengers must hold their tickets and wait to _____ the train to Kaohsiung.", options: ["boil", "blow", "board", "block"], ans: 2, hint: "所有乘客必須拿著車票，等候【登上】往高雄的火車。",
            exp: "board 當動詞時，意思是「登上 (火車、公車、飛機或船隻)」。", vocab: ["board (v.) 登上(車船)", "passenger (n.) 乘客", "ticket (n.) 車票"]
        },
        { 
            q: "16. We are planning a trip to Hualien, so Dad called to _____ two train tickets.", options: ["boil", "block", "blow", "book"], ans: 3, hint: "我們正在計畫去花蓮旅行，所以爸爸打電話【預訂】了兩張火車票。",
            exp: "book 除了當「書本」，當動詞時是非常重要的單字，意思是「預訂 (車票、餐廳、房間)」。", vocab: ["book (v.) 預訂 (n.) 書", "trip (n.) 旅行", "train ticket (n.) 火車票"]
        },
        { 
            q: "17. The police found a dangerous _____ in the building and asked everyone to leave.", options: ["bomb", "bone", "boat", "body"], ans: 0, hint: "警察在大樓裡發現了一枚危險的【炸彈】，並請所有人離開。",
            exp: "會爆炸的「炸彈」是 bomb (注意最後面的字母 b 不發音喔！讀作 /bɑm/)。", vocab: ["bomb (n.) 炸彈", "dangerous (adj.) 危險的", "police (n.) 警察"]
        },
        { 
            q: "18. Mom cut some fresh apples and oranges on the wooden cutting _____.", options: ["boat", "board", "bone", "bookcase"], ans: 1, hint: "媽媽在木製的切菜【砧板】上切了一些新鮮蘋果和柳丁。",
            exp: "cutting board 就是廚房裡用來切菜的「砧板」；board 本身有「木板、板子」的意思。", vocab: ["board (n.) 板子", "cutting board (n.) 砧板", "fresh (adj.) 新鮮的"]
        },
        { 
            q: "19. The little boy sat on the floor playing with colorful wooden _____s.", options: ["body", "blouse", "block", "blanket"], ans: 2, hint: "小男孩坐在地板上玩著五顏六色的木頭【積木】。",
            exp: "block 當名詞時，小孩子玩的「積木」就是 wooden blocks；在街區也常當作「街區 / 街角」。", vocab: ["block (n.) 積木/街區", "colorful (adj.) 五顏六色的", "floor (n.) 地板"]
        },
        { 
            q: "20. The boxer landed a heavy _____ on his opponent's head.", options: ["body",
