<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مولّد أسئلة الاختيار من متعدد</title>
    <style>
        body {
            font-family: 'Tahoma', sans-serif;
            background-color: #0f172a;
            color: #f8fafc;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
        }
        .container {
            background-color: #1e293b;
            padding: 30px;
            border-radius: 16px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.3);
            width: 100%;
            max-width: 600px;
            text-align: center;
        }
        h2 {
            margin-bottom: 20px;
            color: #38bdf8;
        }
        textarea {
            width: 100%;
            height: 150px;
            background-color: #0f172a;
            color: #fff;
            border: 1px solid #475569;
            border-radius: 8px;
            padding: 12px;
            font-size: 16px;
            resize: none;
            box-sizing: border-box;
            margin-bottom: 15px;
        }
        textarea:focus {
            outline: none;
            border-color: #38bdf8;
        }
        .controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 10px;
        }
        .buttons-group {
            display: flex;
            gap: 8px;
        }
        .num-btn {
            background-color: #334155;
            color: #fff;
            border: none;
            width: 35px;
            height: 35px;
            border-radius: 50%;
            cursor: pointer;
            font-weight: bold;
            transition: 0.2s;
        }
        .num-btn.active, .num-btn:hover {
            background-color: #38bdf8;
            color: #0f172a;
        }
        .action-btn {
            background-color: #38bdf8;
            color: #0f172a;
            border: none;
            padding: 10px 20px;
            border-radius: 8px;
            font-weight: bold;
            cursor: pointer;
            font-size: 16px;
            transition: 0.2s;
            width: 100%;
        }
        .action-btn:hover {
            background-color: #0ea5e9;
        }
        .secondary-btns {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }
        .sec-btn {
            background-color: #334155;
            color: #cbd5e1;
            border: none;
            padding: 8px 15px;
            border-radius: 6px;
            cursor: pointer;
            flex: 1;
        }
        .sec-btn:hover {
            background-color: #475569;
        }
        #output {
            margin-top: 20px;
            text-align: right;
            background: #0f172a;
            padding: 15px;
            border-radius: 8px;
            max-height: 300px;
            overflow-y: auto;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>مولّد أسئلة الاختيار من متعدد</h2>
    <textarea id="inputText" placeholder="الصق نصاً من كتابك أو ملخصك هنا..."></textarea>
    
    <div class="controls">
        <span>عدد الأسئلة: <span id="selectedCount">5</span></span>
        <div class="buttons-group">
            <button class="num-btn active" onclick="setCount(5, this)">5</button>
            <button class="num-btn" onclick="setCount(10, this)">10</button>
            <button class="num-btn" onclick="setCount(15, this)">15</button>
            <button class="num-btn" onclick="setCount(20, this)">20</button>
            <button class="num-btn" onclick="setCount(30, this)">30</button>
        </div>
    </div>

    <button class="action-btn" onclick="generateQuestions()">ولّد الأسئلة</button>

    <div class="secondary-btns">
        <button class="sec-btn" onclick="loadDemo()">ضع نصاً تجريبياً</button>
        <button class="sec-btn" onclick="clearAll()">امسح</button>
    </div>

    <div id="output"></div>
</div>

<script>
    let questionCount = 5;

    function setCount(num, btn) {
        questionCount = num;
        document.getElementById('selectedCount').innerText = num;
        document.querySelectorAll('.num-btn').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
    }

    function loadDemo() {
        document.getElementById('inputText').value = "يعتبر علم الاقتصاد واحداً من العلوم الاجتماعية المهمة التي تدرس كيفية استغلاب الموارد المحدودة لإشباع الحاجات الإنسانية غير المحدودة. ويعود ظهور علم الاقتصاد الحديث إلى الكاتب الاسكتلندي آدم سميث في كتابه ثروة الأمم سنة 1776.";
    }

    function clearAll() {
        document.getElementById('inputText').value = "";
        document.getElementById('output').innerHTML = "";
    }

    function generateQuestions() {
        const text = document.getElementById('inputText').value;
        const output = document.getElementById('output');
        
        if (!text.trim()) {
            output.innerHTML = "<p style='color: #f87171;'>يرجى لصق نص أولاً!</p>";
            return;
        }

        // تقسيم النص إلى جمل لاستخراج أسئلة منها
        let sentences = text.split(/[.\n]/).filter(s => s.trim().length > 10);
        
        if (sentences.length === 0) {
            output.innerHTML = "<p style='color: #f87171;'>النص قصير جداً، يرجى وضع نص أطول.</p>";
            return;
        }

        let html = "<h3>الأسئلة المتولدة:</h3>";
        let count = Math.min(questionCount, sentences.length);

        for (let i = 0; i < count; i++) {
            let sent = sentences[i].trim();
            html += `<p><strong>س${i+1}:</strong> ما مضمون العبارة: "${sent}"؟</p>`;
            html += `<hr style="border-color: #334155; margin: 10px 0;">`;
        }

        output.innerHTML = html;
    }
</script>

</body>
</html>
