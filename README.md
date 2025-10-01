<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <title data-i18n="title">Bosh sahifa - Test Ishla</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
                  url('https://images.unsplash.com/photo-1501785888041-af3ef285b470?ixlib=rb-4.0.3&auto=format&fit=crop&w=1600&q=80') no-repeat center center fixed;
      background-size: cover;
      color: rgb(255, 255, 255);
    }
    header {
      background: rgba(0, 0, 0, 0.6);
      padding: 20px;
      text-align: center;
      border-bottom: 2px solid #ffd700;
      position: relative;
    }
    header h1 {
      margin: 0;
      font-size: 36px;
      color: #00ffcc;
      text-shadow: 2px 2px 4px black;
    }
    .clock {
      position: absolute;
      top: 20px;
      right: 20px;
      background: rgba(255, 255, 255, 0.15);
      padding: 10px 20px;
      border-radius: 12px;
      backdrop-filter: blur(8px);
      font-size: 16px;
      color: #ffffff;
      font-weight: bold;
      box-shadow: 0 0 10px rgba(0,0,0,0.6);
    }
    .lang-switcher {
      position: absolute;
      top: 20px;
      left: 20px;
      background: rgba(200, 200, 200, 0.3);
      padding: 8px 12px;
      border-radius: 8px;
      backdrop-filter: blur(6px);
      box-shadow: 0 0 8px rgba(0,0,0,0.4);
    }
    .lang-switcher select {
      background: transparent;
      border: none;
      color: #000000;
      font-weight: bold;
      font-size: 14px;
      outline: none;
      cursor: pointer;
    }
    .lang-switcher select option {
      background: #f0f0f0;
      color: #000;
    }
    nav {
      background: rgba(255, 255, 255, 0.2);
      padding: 15px;
      text-align: center;
      backdrop-filter: blur(6px);
    }
    nav a {
      color: #ffffff;
      text-decoration: none;
      margin: 0 15px;
      font-weight: bold;
      transition: 0.3s;
    }
    nav a:hover {
      color: #ffd700;
      text-shadow: 1px 1px 5px #000;
    }
    .content {
      max-width: 800px;
      margin: 50px auto;
      background: rgba(255, 255, 255, 0.1);
      padding: 30px;
      border-radius: 15px;
      backdrop-filter: blur(8px);
      box-shadow: 0 0 15px rgba(0,0,0,0.6);
    }
    .content h2 {
      color: #00ffcc;
      text-align: center;
    }
    .content p {
      line-height: 1.6;
      font-size: 18px;
      color: #ffffff;
    }
    footer {
      text-align: center;
      padding: 15px;
      background: rgba(0, 0, 0, 0.7);
      border-top: 2px solid #ffd700;
      margin-top: 50px;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <header>
    <div class="lang-switcher">
      <select id="lang">
        <option value="uz">Oʻzbek</option>
        <option value="en">English</option>
        <option value="ru">Русский</option>
      </select>
    </div>
    <h1 data-i18n="headerTitle">Test Ishla</h1>
    <div class="clock" id="clock">Yuklanmoqda...</div>
  </header>

  <nav>
    <a href="index.html" data-i18n="menuHome">Bosh sahifa</a>
    <a href="page2.html" data-i18n="menuPage2">2-sahifa</a>
    <a href="page3.html" data-i18n="menuPage3">3-sahifa</a>
  </nav>

  <div class="content">
    <h2 data-i18n="homeTitle">Bosh sahifa</h2>
    <p data-i18n="homeText">
      Ushbu sayt orqali siz turli testlarni tuzishingiz va ularni ishlatishingiz mumkin. 
      Har bir sahifa alohida bo'lim sifatida xizmat qiladi: savollar yaratish, testlarni sinash va natijalarni ko'rish imkoniyati mavjud. 
      Bu kichik loyiha keyinchalik yanada rivojlantirib, ta'lim yoki mashq qilish jarayonida foydali bo'lishi mumkin.
    </p>
  </div>

  <footer>
    <span data-i18n="footer">© 2025 TestMakerAFU. Barcha huquqlar himoyalangan.</span>
  </footer>

  <script>
    const translations = {
      uz: {
        title: "Bosh sahifa - Test Ishla",
        headerTitle: "Test Ishla",
        menuHome: "Bosh sahifa",
        menuPage2: "2-sahifa",
        menuPage3: "3-sahifa",
        homeTitle: "Bosh sahifa",
        homeText: "Ushbu sayt orqali siz turli testlarni tuzishingiz va ularni ishlatishingiz mumkin. Har bir sahifa alohida bo'lim sifatida xizmat qiladi: savollar yaratish, testlarni sinash va natijalarni ko'rish imkoniyati mavjud. Bu kichik loyiha keyinchalik yanada rivojlantirib, ta'lim yoki mashq qilish jarayonida foydali bo'lishi mumkin.",
        footer: "© 2025 TestMakerAFU. Barcha huquqlar himoyalangan."
      },
      en: {
        title: "Home - Test Ishla",
        headerTitle: "Test Ishla",
        menuHome: "Home",
        menuPage2: "Page 2",
        menuPage3: "Page 3",
        homeTitle: "Home",
        homeText: "On this website you can create different tests and try them out. Each page serves as a separate section: creating questions, testing them, and viewing results. This small project can later be expanded and become useful for education or practice.",
        footer: "© 2025 TestMakerAFU. All rights reserved."
      },
      ru: {
        title: "Главная - Test Ishla",
        headerTitle: "Test Ishla",
        menuHome: "Главная",
        menuPage2: "Страница 2",
        menuPage3: "Страница 3",
        homeTitle: "Главная",
        homeText: "На этом сайте вы можете создавать различные тесты и проходить их. Каждая страница служит отдельным разделом: создание вопросов, проверка тестов и просмотр результатов. Этот небольшой проект в дальнейшем можно развивать и использовать для обучения или практики.",
        footer: "© 2025 TestMakerAFU. Все права защищены."
      }
    };

    function applyTranslations(lang) {
      document.querySelectorAll("[data-i18n]").forEach(el => {
        let key = el.getAttribute("data-i18n");
        if (translations[lang][key]) {
          el.textContent = translations[lang][key];
        }
      });
      document.title = translations[lang].title;
      localStorage.setItem("lang", lang);
    }

    document.getElementById("lang").addEventListener("change", (e) => {
      applyTranslations(e.target.value);
    });

    let savedLang = localStorage.getItem("lang") || "uz";
    document.getElementById("lang").value = savedLang;
    applyTranslations(savedLang);

    function updateClock() {
      let now = new Date();
      let lang = localStorage.getItem("lang") || "uz";
      let locales = { uz: "uz-UZ", en: "en-GB", ru: "ru-RU" };
      let options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
      let date = now.toLocaleDateString(locales[lang], options);
      let time = now.toLocaleTimeString(locales[lang]);
      document.getElementById('clock').innerHTML = time + " | " + date;
    }
    setInterval(updateClock, 1000);
    updateClock();
  </script>
</body>
</html>
