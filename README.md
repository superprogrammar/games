<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>حاسبة العمر الأسطورية 🧙‍♂️</title>
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet" />
<style>
  @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');

  * {
    box-sizing: border-box;
  }

  body {
    margin: 0; padding: 0;
    font-family: 'Cairo', sans-serif;
    background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
    color: #eee;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
    transition: background 0.5s ease;
  }

  .container {
    background: rgba(255,255,255,0.1);
    backdrop-filter: blur(15px);
    border-radius: 20px;
    padding: 35px 25px;
    width: 100%;
    max-width: 480px;
    box-shadow: 0 0 25px rgba(0,0,0,0.7);
    text-align: center;
    position: relative;
  }

  h1 {
    font-size: 28px;
    margin-bottom: 10px;
  }

  .greeting {
    font-size: 16px;
    margin-bottom: 25px;
    color: #ddd;
  }

  label {
    font-weight: 700;
    display: block;
    margin-bottom: 8px;
    font-size: 15px;
    color: #fff;
  }

  input[type="date"] {
    width: 100%;
    padding: 14px 12px;
    border-radius: 12px;
    border: none;
    font-size: 16px;
    outline: none;
    background: rgba(255,255,255,0.9);
    color: #222;
    margin-bottom: 25px;
    transition: box-shadow 0.3s ease;
  }

  input[type="date"]:focus {
    box-shadow: 0 0 8px 2px #4a90e2;
  }

  button {
    background: #4a90e2;
    color: #fff;
    border: none;
    padding: 14px 25px;
    font-size: 17px;
    border-radius: 12px;
    cursor: pointer;
    transition: background 0.3s ease, transform 0.3s ease;
  }

  button:hover {
    background: #357ABD;
    transform: scale(1.07);
  }

  #resultat {
    margin-top: 30px;
    font-size: 19px;
    line-height: 1.7;
    color: #fafafa;
    min-height: 140px;
    white-space: pre-line;
  }

  .copy-btn {
    background: #7ed6df;
    color: #222;
    padding: 8px 16px;
    font-size: 14px;
    border-radius: 10px;
    cursor: pointer;
    margin-top: 15px;
    border: none;
    box-shadow: 0 3px 10px rgba(0,0,0,0.15);
    transition: background 0.3s ease;
  }

  .copy-btn:hover {
    background: #4ecdc4;
  }

  /* الوضع الليلي والعادي */
  @media (prefers-color-scheme: light) {
    body {
      background: linear-gradient(135deg, #74ebd5, #ACB6E5);
      color: #222;
    }
    .container {
      background: rgba(255,255,255,0.9);
      color: #222;
      box-shadow: 0 0 25px rgba(0,0,0,0.1);
    }
    input[type="date"] {
      background: #fff;
      color: #222;
    }
    button {
      background: #007bff;
      color: #fff;
    }
    button:hover {
      background: #0056b3;
    }
    .copy-btn {
      background: #4ecdc4;
      color: #222;
    }
    .copy-btn:hover {
      background: #2c9c94;
    }
  }
</style>
</head>
<body>

<div class="container">
  <h1>حاسبة العمر الأسطورية 🧙‍♂️</h1>
  <p class="greeting" id="greeting">مرحبًا! أدخل تاريخ ميلادك لمعرفة عمرك بدقة كاملة.</p>

  <label for="dob">📅 اختر تاريخ ميلادك:</label>
  <input type="date" id="dob" max="" />

  <button id="calcBtn">احسب عمري الآن</button>

  <div id="resultat"></div>
  <button class="copy-btn" id="copyBtn" style="display:none;">نسخ النتيجة 📋</button>
</div>

<script>
  // تعيين الحد الأقصى لتاريخ الميلاد (اليوم)
  const dobInput = document.getElementById('dob');
  const todayISO = new Date().toISOString().split('T')[0];
  dobInput.setAttribute('max', todayISO);

  // تحديث رسالة الترحيب حسب الوقت
  function updateGreeting() {
    const hour = new Date().getHours();
    const greeting = document.getElementById('greeting');
    if (hour < 12) greeting.textContent = "☀️ صباح الخير! أدخل تاريخ ميلادك لحساب عمرك.";
    else if (hour < 18) greeting.textContent = "🌤️ مساء الخير! لنحسب عمرك الآن.";
    else greeting.textContent = "🌙 مساء الخير! هل تريد معرفة عمرك بدقة؟";
  }
  updateGreeting();

  // دالة حساب العمر والوقت المتبقي لعيد الميلاد
  function calculerAge() {
    const dob = dobInput.value;
    const resultat = document.getElementById('resultat');
    const copyBtn = document.getElementById('copyBtn');

    if (!dob) {
      resultat.textContent = "⚠️ الرجاء إدخال تاريخ ميلاد صالح.";
      copyBtn.style.display = 'none';
      return;
    }

    const birthDate = new Date(dob);
    const now = new Date();

    if (birthDate > now) {
      resultat.textContent = "❗ لا يمكن أن يكون تاريخ الميلاد في المستقبل!";
      copyBtn.style.display = 'none';
      return;
    }

    // حساب العمر التفصيلي
    let years = now.getFullYear() - birthDate.getFullYear();
    let months = now.getMonth() - birthDate.getMonth();
    let days = now.getDate() - birthDate.getDate();
    let hours = now.getHours() - birthDate.getHours();
    let minutes = now.getMinutes() - birthDate.getMinutes();
    let seconds = now.getSeconds() - birthDate.getSeconds();

    if (seconds < 0) {
      seconds += 60;
      minutes--;
    }
    if (minutes < 0) {
      minutes += 60;
      hours--;
    }
    if (hours < 0) {
      hours += 24;
      days--;
    }
    if (days < 0) {
      months--;
      const prevMonth = new Date(now.getFullYear(), now.getMonth(), 0).getDate();
      days += prevMonth;
    }
    if (months < 0) {
      years--;
      months += 12;
    }

    // حساب الوقت المتبقي لعيد الميلاد القادم
    let nextBirthday = new Date(now.getFullYear(), birthDate.getMonth(), birthDate.getDate(),
                                birthDate.getHours(), birthDate.getMinutes(), birthDate.getSeconds());
    if (now > nextBirthday) {
      nextBirthday.setFullYear(nextBirthday.getFullYear() + 1);
    }

    let diffToNextBirthday = nextBirthday - now;

    let remDays = Math.floor(diffToNextBirthday / (1000 * 60 * 60 * 24));
    let remHours = Math.floor((diffToNextBirthday / (1000 * 60 * 60)) % 24);
    let remMinutes = Math.floor((diffToNextBirthday / (1000 * 60)) % 60);
    let remSeconds = Math.floor((diffToNextBirthday / 1000) % 60);

    // النتيجة بصيغة نصية مرتبة
    const resultText = 
      `🕒 عمرك الآن:\n` +
      `${years} سنة، ${months} شهر، ${days} يوم\n` +
      `${hours} ساعة، ${minutes} دقيقة، ${seconds} ثانية\n\n` +
      `🎉 الوقت المتبقي لعيد ميلادك القادم:\n` +
      `${remDays} يوم، ${remHours} ساعة، ${remMinutes} دقيقة، ${remSeconds} ثانية\n\n` +
      `تمنياتي لك بسنة جديدة مليئة بالفرح والنجاح! 🎈`;

    resultat.textContent = resultText;
    copyBtn.style.display = 'inline-block';
  }

  document.getElementById('calcBtn').addEventListener('click', calculerAge);

  // زر النسخ
  document.getElementById('copyBtn').addEventListener('click', () => {
    const text = document.getElementById('resultat').textContent;
    navigator.clipboard.writeText(text).then(() => {
      alert('تم نسخ النتيجة إلى الحافظة!');
    });
  });
</script>

</body>
</html>
