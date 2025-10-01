<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Test Ishla Platformasi</title>
  <style>
    /* Sizning mavjud CSS stylinglaringiz */
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(-45deg,#1e3c72,#2a5298,#0f2027,#203a43,#2c5364);
      background-size: 400% 400%;
      animation: gradientBG 15s ease infinite;
      color: white;
      margin: 0; padding: 0;
    }
    @keyframes gradientBG {
      0%{background-position:0% 50%;}
      50%{background-position:100% 50%;}
      100%{background-position:0% 50%;}
    }
    header, nav, footer {
      background: rgba(0,0,0,0.6);
      backdrop-filter: blur(10px);
      padding: 1rem;
      text-align: center;
    }
    nav ul {list-style:none;display:flex;justify-content:center;gap:20px;padding:0;}
    nav a {color:white;text-decoration:none;padding:8px 16px;border-radius:6px;}
    nav a:hover {background: rgba(255,255,255,0.2);}
    section {min-height:100vh;display:flex;justify-content:center;align-items:center;flex-direction:column;padding:2rem;}
    .form-box {
      background:rgba(255,255,255,0.1);
      backdrop-filter:blur(15px);
      border-radius:15px;
      padding:2rem;
      max-width:400px;
      width:100%;
      margin:1rem;
    }
    .form-box h2 {color:#4cd137;text-align:center;margin-bottom:1rem;}
    .form-box input, .form-box button {
      width:100%;padding:10px;margin-bottom:1rem;border-radius:8px;border:none;outline:none;
    }
    .form-box button {
      background:#4cd137;color:white;font-weight:bold;cursor:pointer;
    }
    .form-box button:hover {background:#44bd32;}
    .forms {display:flex;flex-wrap:wrap;justify-content:center;gap:20px;}

    /* Til switcher paneli */
    .lang-panel {
      position: fixed;
      top: 50%;
      left: 20px;
      transform: translateY(-50%);
      display: flex;
      flex-direction: column;
      gap: 15px;
      background: rgba(255,255,255,0.1);
      padding: 12px;
      border-radius: 15px;
      backdrop-filter: blur(10px);
      box-shadow: 0 0 15px rgba(0,0,0,0.4);
      z-index: 2000;
    }
    .lang-btn {
      font-size: 28px;
      cursor: pointer;
      transition: transform 0.3s, box-shadow 0.3s;
      border-radius: 50%;
      padding: 5px;
    }
    .lang-btn:hover {
      transform: scale(1.2);
      box-shadow: 0 0 10px rgba(255,255,255,0.7);
    }
    .lang-btn.active {
      background: rgba(76,209,55,0.2);
      box-shadow: 0 0 10px #4cd137;
    }

    /* Xabarlar uchun */
    .message {
      padding: 10px;
      margin: 10px 0;
      border-radius: 5px;
      text-align: center;
    }
    .success {
      background: rgba(76, 209, 55, 0.3);
      border: 1px solid #4cd137;
    }
    .error {
      background: rgba(231, 76, 60, 0.3);
      border: 1px solid #e74c3c;
    }
  </style>
</head>
<body>
  <header>
    <h1>Test Ishla Platformasi</h1>
  </header>

  <!-- Til paneli (bayroqlar) -->
  <div class="lang-panel">
    <div class="lang-btn" data-lang="uz">🇺🇿</div>
    <div class="lang-btn" data-lang="en">🇺🇸</div>
    <div class="lang-btn" data-lang="ru">🇷🇺</div>
  </div>

  <nav>
    <ul>
      <li><a href="#create" data-i18n="menuCreate">Test Yaratish</a></li>
      <li><a href="#work" data-i18n="menuWork">Test ishlash</a></li>
      <li><a href="#register" data-i18n="menuRegister">Ro'yxatdan o'tish</a></li>
    </ul>
  </nav>

  <!-- Ro'yxatdan o'tish va Kirish -->
  <section id="register">
    <div class="forms">
      <!-- Ro'yxatdan o'tish -->
      <div class="form-box">
        <h2 data-i18n="registerTitle">Ro'yxatdan o'tish</h2>
        <div id="regMessage"></div>
        <form id="regForm">
          <label data-i18n="labelSurname">Familiya</label>
          <input type="text" id="surname" required placeholder="Familiyangiz">

          <label data-i18n="labelName">Ism</label>
          <input type="text" id="name" required placeholder="Ismingiz">

          <label data-i18n="labelEmail">Gmail</label>
          <input type="email" id="email" required placeholder="example@gmail.com">

          <button type="submit" data-i18n="btnRegister">Ro'yxatdan o'tish</button>
        </form>
      </div>

      <!-- Kirish -->
      <div class="form-box">
        <h2 data-i18n="loginTitle">Kirish</h2>
        <div id="loginMessage"></div>
        <form id="loginForm">
          <label data-i18n="labelID">ID raqam</label>
          <input type="text" id="loginID" required placeholder="14 xonali ID raqamingiz" maxlength="14">

          <button type="submit" data-i18n="btnLogin">Kirish</button>
        </form>
      </div>
    </div>
  </section>

  <footer>
    <p data-i18n="footer">© 2025 Test Ishla. Barcha huquqlar himoyalangan.</p>
  </footer>

  <!-- Supabase kutubxonasi -->
  <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>

  <script>
    // ==================== SUPABASE SOZLAMALARI ====================
    // BU YERNI O'ZGARTIRING! O'zingizning Supabase ma'lumotlaringizni qo'ying
    const SUPABASE_URL = 'https://xxxxxxxxxxxx.supabase.co';  // O'z project URL ingiz
    const SUPABASE_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...';  // O'z anon key ingiz
    
    const supabase = supabase.createClient(SUPABASE_URL, SUPABASE_KEY);

    // ==================== TIL TARJIMALARI ====================
    const translations = {
      uz:{
        menuCreate:"Test Yaratish",menuWork:"Test ishlash",menuRegister:"Ro'yxatdan o'tish",
        registerTitle:"Ro'yxatdan o'tish",labelSurname:"Familiya",labelName:"Ism",labelEmail:"Gmail",
        btnRegister:"Ro'yxatdan o'tish",loginTitle:"Kirish",labelID:"ID raqam",btnLogin:"Kirish",
        footer:"© 2025 Test Ishla. Barcha huquqlar himoyalangan.",
        regSuccess:"Ro'yxatdan muvaffaqiyatli o'tdingiz! ID raqamingiz: ",
        regError:"Xatolik yuz berdi. Iltimos, qaytadan urinib ko'ring.",
        loginSuccess:"Muvaffaqiyatli kirdingiz!",
        loginError:"Noto'g'ri ID raqam. Iltimos, tekshirib qaytadan urinib ko'ring.",
        emailExists:"Bu email allaqachon ro'yxatdan o'tgan",
        missingFields:"Iltimos, barcha maydonlarni to'ldiring"
      },
      en:{
        menuCreate:"Create Test",menuWork:"Work Test",menuRegister:"Register",
        registerTitle:"Register",labelSurname:"Surname",labelName:"Name",labelEmail:"Email",
        btnRegister:"Register",loginTitle:"Login",labelID:"ID Number",btnLogin:"Login",
        footer:"© 2025 Test Ishla. All rights reserved.",
        regSuccess:"Registration successful! Your ID: ",
        regError:"An error occurred. Please try again.",
        loginSuccess:"Login successful!",
        loginError:"Incorrect ID number. Please check and try again.",
        emailExists:"This email is already registered",
        missingFields:"Please fill all fields"
      },
      ru:{
        menuCreate:"Создать тест",menuWork:"Пройти тест",menuRegister:"Регистрация",
        registerTitle:"Регистрация",labelSurname:"Фамилия",labelName:"Имя",labelEmail:"Почта",
        btnRegister:"Зарегистрироваться",loginTitle:"Вход",labelID:"ID номер",btnLogin:"Войти",
        footer:"© 2025 Test Ishla. Все права защищены.",
        regSuccess:"Регистрация прошла успешно! Ваш ID: ",
        regError:"Произошла ошибка. Пожалуйста, попробуйте еще раз.",
        loginSuccess:"Вход выполнен успешно!",
        loginError:"Неверный ID номер. Пожалуйста, проверьте и попробуйте еще раз.",
        emailExists:"Этот email уже зарегистрирован",
        missingFields:"Пожалуйста, заполните все поля"
      }
    };

    // ==================== FUNKSIYALAR ====================

    // Tarjima qo'llash
    function applyTranslations(lang){
      document.querySelectorAll("[data-i18n]").forEach(el=>{
        const key=el.getAttribute("data-i18n");
        if(translations[lang][key]) el.textContent=translations[lang][key];
      });
      localStorage.setItem("lang",lang);

      document.querySelectorAll(".lang-btn").forEach(btn=>{
        btn.classList.remove("active");
        if(btn.dataset.lang===lang) btn.classList.add("active");
      });
    }

    // 14 xonali ID yaratish
    function generateID() {
      return Math.random().toString().substring(2, 16);
    }

    // Xabar ko'rsatish
    function showMessage(elementId, message, type) {
      const element = document.getElementById(elementId);
      element.innerHTML = `<div class="message ${type}">${message}</div>`;
      setTimeout(() => {
        element.innerHTML = '';
      }, 5000);
    }

    // Email tekshirish
    async function checkEmailExists(email) {
      try {
        const { data, error } = await supabase
          .from('users')
          .select('email')
          .eq('email', email)
          .single();

        return !!data; // Agar data mavjud bo'lsa true, yo'q bo'lsa false
      } catch (error) {
        return false;
      }
    }

    // ==================== RO'YXATDAN O'TISH ====================

    document.getElementById('regForm').addEventListener('submit', async function(e) {
      e.preventDefault();
      
      const surname = document.getElementById('surname').value.trim();
      const name = document.getElementById('name').value.trim();
      const email = document.getElementById('email').value.trim();
      const currentLang = localStorage.getItem('lang') || 'uz';

      // Maydonlarni tekshirish
      if (!surname || !name || !email) {
        showMessage('regMessage', translations[currentLang].missingFields, 'error');
        return;
      }

      try {
        // Email allaqachon mavjudligini tekshirish
        const emailExists = await checkEmailExists(email);
        if (emailExists) {
          showMessage('regMessage', translations[currentLang].emailExists, 'error');
          return;
        }

        // Yangi ID yaratish
        const userId = generateID();

        // Ma'lumotlarni Supabase'ga saqlash
        const { data, error } = await supabase
          .from('users')
          .insert([
            { 
              surname: surname,
              name: name, 
              email: email,
              user_id: userId
            }
          ])
          .select();

        if (error) {
          console.error('Supabase xatosi:', error);
          throw error;
        }

        // Muvaffaqiyatli xabar
        const successMessage = translations[currentLang].regSuccess + userId;
        showMessage('regMessage', successMessage, 'success');
        
        // Formani tozalash
        document.getElementById('regForm').reset();

        // Foydalanuvchiga ID ni ko'rsatish
        alert(`Tabriklaymiz! Ro'yxatdan muvaffaqiyatli o'tdingiz.\nID raqamingiz: ${userId}\nBu ID ni saqlab qo'ying!`);

      } catch (error) {
        console.error('Xatolik:', error);
        showMessage('regMessage', translations[currentLang].regError, 'error');
      }
    });

    // ==================== KIRISH ====================

    document.getElementById('loginForm').addEventListener('submit', async function(e) {
      e.preventDefault();
      
      const loginID = document.getElementById('loginID').value.trim();
      const currentLang = localStorage.getItem('lang') || 'uz';

      if (!loginID) {
        showMessage('loginMessage', translations[currentLang].missingFields, 'error');
        return;
      }

      try {
        // ID ni tekshirish
        const { data, error } = await supabase
          .from('users')
          .select('*')
          .eq('user_id', loginID)
          .single();

        if (error || !data) {
          showMessage('loginMessage', translations[currentLang].loginError, 'error');
          return;
        }

        // Muvaffaqiyatli kirish
        showMessage('loginMessage', translations[currentLang].loginSuccess, 'success');
        
        // Foydalanuvchi ma'lumotlarini saqlash
        localStorage.setItem('currentUser', JSON.stringify(data));
        
        // Kirish muvaffaqiyatli - keyingi sahifaga o'tish
        setTimeout(() => {
          alert(`Xush kelibsiz, ${data.surname} ${data.name}!\nSiz muvaffaqiyatli tizimga kirdingiz.`);
          // Bu yerda foydalanuvchini boshqa sahifaga yo'naltirishingiz mumkin
          // window.location.href = 'dashboard.html';
        }, 1000);

      } catch (error) {
        console.error('Xatolik:', error);
        showMessage('loginMessage', translations[currentLang].loginError, 'error');
      }
    });

    // ==================== BOSHLANG'ICH SOZLAMALAR ====================

    // Bosilganda tilni o'zgartirish
    document.querySelectorAll(".lang-btn").forEach(btn=>{
      btn.addEventListener("click",()=>applyTranslations(btn.dataset.lang));
    });

    // Boshlang'ich til
    document.addEventListener("DOMContentLoaded",()=>{
      const savedLang=localStorage.getItem("lang")||"uz";
      applyTranslations(savedLang);
    });

    // ID input ga faqat raqam kiritish
    document.getElementById('loginID').addEventListener('input', function(e) {
      this.value = this.value.replace(/\D/g, ''); // Faqat raqamlar qoladi
    });
  </script>
</body>
</html>
