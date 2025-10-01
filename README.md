<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Test Ishla Platformasi</title>
  <style>
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
    .form-box input, .form-box button, .form-box textarea {
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

    /* Test yaratish sahifasi uchun */
    .test-creator {
      background: rgba(255,255,255,0.1);
      backdrop-filter: blur(15px);
      border-radius: 15px;
      padding: 2rem;
      max-width: 800px;
      width: 100%;
      margin: 1rem;
    }

    .question-block {
      background: rgba(255,255,255,0.05);
      padding: 1.5rem;
      margin: 1rem 0;
      border-radius: 10px;
      border-left: 4px solid #4cd137;
    }

    .option-row {
      display: flex;
      align-items: center;
      gap: 10px;
      margin: 8px 0;
    }

    .option-row input[type="text"] {
      flex: 1;
      padding: 8px;
      border-radius: 5px;
      border: 1px solid rgba(255,255,255,0.3);
      background: rgba(255,255,255,0.1);
      color: white;
    }

    .option-row input[type="radio"] {
      margin: 0;
    }

    .add-btn, .remove-btn {
      background: #3498db;
      color: white;
      border: none;
      padding: 8px 15px;
      border-radius: 5px;
      cursor: pointer;
      font-size: 14px;
      margin: 5px;
    }

    .remove-btn {
      background: #e74c3c;
    }

    .add-btn:hover {
      background: #2980b9;
    }

    .remove-btn:hover {
      background: #c0392b;
    }

    .test-actions {
      display: flex;
      gap: 10px;
      margin-top: 20px;
      justify-content: center;
      flex-wrap: wrap;
    }

    .test-list {
      background: rgba(255,255,255,0.1);
      backdrop-filter: blur(15px);
      border-radius: 15px;
      padding: 2rem;
      max-width: 800px;
      width: 100%;
      margin: 1rem;
      max-height: 500px;
      overflow-y: auto;
    }

    .test-item {
      background: rgba(255,255,255,0.05);
      padding: 1rem;
      margin: 0.5rem 0;
      border-radius: 8px;
      border-left: 4px solid #9b59b6;
    }

    .hidden {
      display: none;
    }

    .form-group {
      margin-bottom: 1rem;
    }

    .form-group label {
      display: block;
      margin-bottom: 5px;
      font-weight: bold;
    }

    textarea {
      resize: vertical;
      min-height: 80px;
      background: rgba(255,255,255,0.1);
      color: white;
      border: 1px solid rgba(255,255,255,0.3);
    }

    .btn {
      background: #4cd137;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 8px;
      cursor: pointer;
      font-weight: bold;
    }

    .btn:hover {
      background: #44bd32;
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

  <!-- Test Yaratish Sahifasi -->
  <section id="create" class="hidden">
    <div class="test-creator">
      <h2 data-i18n="createTestTitle">Test Yaratish</h2>
      <div id="testMessage"></div>
      
      <form id="testForm">
        <div class="form-group">
          <label data-i18n="labelTestName">Test Nomi</label>
          <input type="text" id="testName" required placeholder="Test nomini kiriting">
        </div>

        <div class="form-group">
          <label data-i18n="labelTestDescription">Test Tavsifi</label>
          <textarea id="testDescription" rows="3" placeholder="Test haqida qisqacha tavsif"></textarea>
        </div>

        <div id="questionsContainer">
          <!-- Savollar shu yerga yuklanadi -->
        </div>

        <button type="button" class="add-btn" onclick="addQuestion()" data-i18n="btnAddQuestion">+ Yangi Savol Qo'shish</button>
        
        <div class="test-actions">
          <button type="submit" class="btn" data-i18n="btnSaveTest">Testni Saqlash</button>
          <button type="button" class="btn" onclick="showTestList()" data-i18n="btnShowTests">Yaratilgan Testlar</button>
          <button type="button" class="btn" onclick="goToRegister()" data-i18n="btnBackRegister">Orqaga</button>
        </div>
      </form>
    </div>
  </section>

  <!-- Testlar Ro'yxati -->
  <section id="testList" class="hidden">
    <div class="test-list">
      <h2 data-i18n="testListTitle">Yaratilgan Testlar</h2>
      <div id="testsContainer">
        <!-- Testlar ro'yxati shu yerga yuklanadi -->
      </div>
      <div class="test-actions">
        <button type="button" class="btn" onclick="goToTestCreator()" data-i18n="btnBackCreate">Test Yaratishga Qaytish</button>
        <button type="button" class="btn" onclick="goToRegister()" data-i18n="btnBackRegister">Bosh Sahifa</button>
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
    const SUPABASE_URL = 'https://fntndvrrovszjftgmjij.supabase.co';
    const SUPABASE_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImZudG5kdnJyb3ZzempmdGdtamlqIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTkzMjEwMjMsImV4cCI6MjA3NDg5NzAyM30.625HTl4HyPqLSpsvuTUPFhjHKNfUbIWx9NWpov8AyTA';
    
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
        missingFields:"Iltimos, barcha maydonlarni to'ldiring",
        createTestTitle:"Test Yaratish",
        testListTitle:"Yaratilgan Testlar",
        labelTestName:"Test Nomi",
        labelTestDescription:"Test Tavsifi", 
        btnAddQuestion:"+ Yangi Savol Qo'shish",
        btnSaveTest:"Testni Saqlash",
        btnShowTests:"Yaratilgan Testlar",
        btnBackRegister:"Orqaga",
        btnBackCreate:"Test Yaratishga Qaytish"
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
        missingFields:"Please fill all fields",
        createTestTitle:"Create Test",
        testListTitle:"Created Tests", 
        labelTestName:"Test Name",
        labelTestDescription:"Test Description",
        btnAddQuestion:"+ Add New Question",
        btnSaveTest:"Save Test",
        btnShowTests:"Created Tests", 
        btnBackRegister:"Back",
        btnBackCreate:"Back to Test Creator"
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
        missingFields:"Пожалуйста, заполните все поля",
        createTestTitle:"Создать тест",
        testListTitle:"Созданные тесты",
        labelTestName:"Название теста", 
        labelTestDescription:"Описание теста",
        btnAddQuestion:"+ Добавить вопрос",
        btnSaveTest:"Сохранить тест",
        btnShowTests:"Созданные тесты",
        btnBackRegister:"Назад",
        btnBackCreate:"Назад к созданию теста"
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

    // ==================== RO'YXATDAN O'TISH ====================

    document.getElementById('regForm').addEventListener('submit', async function(e) {
      e.preventDefault();
      
      const surname = document.getElementById('surname').value.trim();
      const name = document.getElementById('name').value.trim();
      const email = document.getElementById('email').value.trim();
      const currentLang = localStorage.getItem('lang') || 'uz';

      if (!surname || !name || !email) {
        showMessage('regMessage', translations[currentLang].missingFields, 'error');
        return;
      }

      try {
        console.log('🔵 Ro\'yxatdan o\'tish boshlandi...');

        // Email allaqachon mavjudligini tekshirish
        const { data: existingEmail, error: emailError } = await supabase
          .from('users')
          .select('email')
          .eq('email', email);

        if (emailError) {
          console.error('Email tekshirish xatosi:', emailError);
        }

        if (existingEmail && existingEmail.length > 0) {
          showMessage('regMessage', translations[currentLang].emailExists, 'error');
          return;
        }

        // Yangi ID yaratish
        const userId = generateID();
        console.log('🆔 Yaratilgan ID:', userId);

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
          console.error('❌ Supabase INSERT xatosi:', error);
          showMessage('regMessage', 'Server xatosi: ' + error.message, 'error');
          return;
        }

        console.log('✅ Muvaffaqiyatli saqlandi:', data);

        // Muvaffaqiyatli xabar
        const successMessage = translations[currentLang].regSuccess + userId;
        showMessage('regMessage', successMessage, 'success');
        
        // Formani tozalash
        document.getElementById('regForm').reset();

        // Foydalanuvchiga ID ni ko'rsatish
        alert(`Tabriklaymiz! Ro'yxatdan muvaffaqiyatli o'tdingiz.\n\nID raqamingiz: ${userId}\n\nBu ID ni saqlab qo'ying!`);

        // 5 soniyadan keyin ma'lumotlarni tekshirish
        setTimeout(async () => {
          console.log('🔍 Ma\'lumotlarni tekshirish...');
          const { data: checkData, error: checkError } = await supabase
            .from('users')
            .select('*')
            .eq('user_id', userId);
          
          if (checkError) {
            console.error('❌ Tekshirish xatosi:', checkError);
          } else {
            console.log('✅ Tekshirish natijasi:', checkData);
            if (checkData.length > 0) {
              console.log('🎉 Ma\'lumotlar Supabase da mavjud!');
            } else {
              console.log('⚠️ Ma\'lumotlar Supabase da ko\'rinmayapti');
            }
          }
        }, 3000);

      } catch (error) {
        console.error('❌ Umumiy xatolik:', error);
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
        console.log('🔵 Kirish urinilyapti, ID:', loginID);

        // ID ni tekshirish
        const { data, error } = await supabase
          .from('users')
          .select('*')
          .eq('user_id', loginID)
          .single();

        if (error || !data) {
          console.error('❌ Kirish xatosi:', error);
          showMessage('loginMessage', translations[currentLang].loginError, 'error');
          return;
        }

        console.log('✅ Kirish muvaffaqiyatli:', data);
        showMessage('loginMessage', translations[currentLang].loginSuccess, 'success');
        
        // Foydalanuvchi ma'lumotlarini saqlash
        localStorage.setItem('currentUser', JSON.stringify(data));
        
        // Kirish muvaffaqiyatli - keyingi sahifaga o'tish
        setTimeout(() => {
          alert(`Xush kelibsiz, ${data.surname} ${data.name}!\n\nSiz muvaffaqiyatli tizimga kirdingiz.`);
        }, 1000);

      } catch (error) {
        console.error('❌ Kirish xatosi:', error);
        showMessage('loginMessage', translations[currentLang].loginError, 'error');
      }
    });

    // ==================== TEST YARATISH FUNKSIYALARI ====================

    // Sahifalar orasida o'tish
    function showTestCreator() {
      document.getElementById('register').classList.add('hidden');
      document.getElementById('create').classList.remove('hidden');
      document.getElementById('testList').classList.add('hidden');
    }

    function showTestList() {
      document.getElementById('register').classList.add('hidden');
      document.getElementById('create').classList.add('hidden');
      document.getElementById('testList').classList.remove('hidden');
      loadTests();
    }

    function goToRegister() {
      document.getElementById('register').classList.remove('hidden');
      document.getElementById('create').classList.add('hidden');
      document.getElementById('testList').classList.add('hidden');
    }

    function goToTestCreator() {
      document.getElementById('register').classList.add('hidden');
      document.getElementById('create').classList.remove('hidden');
      document.getElementById('testList').classList.add('hidden');
    }

    // Yangi savol qo'shish
    function addQuestion() {
      const questionsContainer = document.getElementById('questionsContainer');
      const questionIndex = questionsContainer.children.length;
      
      const questionHTML = `
        <div class="question-block" id="question-${questionIndex}">
          <h4>Savol ${questionIndex + 1}</h4>
          <input type="text" class="question-text" placeholder="Savol matnini kiriting" required>
          
          <div class="options-container">
            <div class="option-row">
              <input type="radio" name="correct-${questionIndex}" value="0" required>
              <input type="text" class="option-text" placeholder="Variant A" required>
            </div>
            <div class="option-row">
              <input type="radio" name="correct-${questionIndex}" value="1">
              <input type="text" class="option-text" placeholder="Variant B" required>
            </div>
            <div class="option-row">
              <input type="radio" name="correct-${questionIndex}" value="2">
              <input type="text" class="option-text" placeholder="Variant C">
            </div>
            <div class="option-row">
              <input type="radio" name="correct-${questionIndex}" value="3">
              <input type="text" class="option-text" placeholder="Variant D">
            </div>
          </div>
          
          <button type="button" class="remove-btn" onclick="removeQuestion(${questionIndex})">Savolni O'chirish</button>
        </div>
      `;
      
      questionsContainer.insertAdjacentHTML('beforeend', questionHTML);
    }

    // Savolni o'chirish
    function removeQuestion(index) {
      const questionElement = document.getElementById(`question-${index}`);
      if (questionElement) {
        questionElement.remove();
        const questions = document.querySelectorAll('.question-block');
        questions.forEach((question, i) => {
          question.id = `question-${i}`;
          question.querySelector('h4').textContent = `Savol ${i + 1}`;
        });
      }
    }

    // Testni saqlash
    document.getElementById('testForm').addEventListener('submit', async function(e) {
      e.preventDefault();
      
      const currentUser = JSON.parse(localStorage.getItem('currentUser'));
      if (!currentUser) {
        alert('Iltimos, avval tizimga kiring!');
        return;
      }

      const testName = document.getElementById('testName').value.trim();
      const testDescription = document.getElementById('testDescription').value.trim();
      
      if (!testName) {
        showMessage('testMessage', 'Test nomini kiriting!', 'error');
        return;
      }

      const questions = [];
      const questionBlocks = document.querySelectorAll('.question-block');
      
      if (questionBlocks.length === 0) {
        showMessage('testMessage', 'Kamida bitta savol qo\'shing!', 'error');
        return;
      }

      try {
        questionBlocks.forEach((block, index) => {
          const questionText = block.querySelector('.question-text').value.trim();
          const options = Array.from(block.querySelectorAll('.option-text'))
            .map(input => input.value.trim())
            .filter(text => text !== '');
          
          const correctAnswer = block.querySelector('input[type="radio"]:checked');
          
          if (!questionText || options.length < 2 || !correctAnswer) {
            throw new Error(`Savol ${index + 1} to'liq to'ldirilmagan`);
          }

          questions.push({
            question: questionText,
            options: options,
            correct_answer: parseInt(correctAnswer.value)
          });
        });

        const { data, error } = await supabase
          .from('tests')
          .insert([
            {
              test_name: testName,
              description: testDescription,
              questions: questions,
              created_by: currentUser.user_id,
              created_by_name: `${currentUser.surname} ${currentUser.name}`,
              created_at: new Date()
            }
          ])
          .select();

        if (error) throw error;

        showMessage('testMessage', 'Test muvaffaqiyatli saqlandi!', 'success');
        document.getElementById('testForm').reset();
        document.getElementById('questionsContainer').innerHTML = '';
        
        addQuestion();

      } catch (error) {
        console.error('Test saqlash xatosi:', error);
        showMessage('testMessage', 'Xatolik: ' + error.message, 'error');
      }
    });

    // Testlarni yuklash
    async function loadTests() {
      const currentUser = JSON.parse(localStorage.getItem('currentUser'));
      if (!currentUser) return;

      try {
        const { data: tests, error } = await supabase
          .from('tests')
          .select('*')
          .eq('created_by', currentUser.user_id)
          .order('created_at', { ascending: false });

        if (error) throw error;

        const testsContainer = document.getElementById('testsContainer');
        testsContainer.innerHTML = '';

        if (!tests || tests.length === 0) {
          testsContainer.innerHTML = '<p>Hali test yaratilmagan</p>';
          return;
        }

        tests.forEach(test => {
          const testHTML = `
            <div class="test-item">
              <h4>${test.test_name}</h4>
              <p>${test.description || 'Tavsif yo\'q'}</p>
              <p><strong>Savollar soni:</strong> ${test.questions.length}</p>
              <p><strong>Yaratilgan sana:</strong> ${new Date(test.created_at).toLocaleDateString('uz-UZ')}</p>
              <button class="add-btn" onclick="startTest('${test.id}')">Testni Boshlash</button>
              <button class="remove-btn" onclick="deleteTest('${test.id}')">O'chirish</button>
            </div>
          `;
          testsContainer.insertAdjacentHTML('beforeend', testHTML);
        });

      } catch (error) {
        console.error('Testlarni yuklash xatosi:', error);
      }
    }

    // Testni o'chirish
    async function deleteTest(testId) {
      if (!confirm('Bu testni o\'chirishni istaysizmi?')) return;

      try {
        const { error } = await supabase
          .from('tests')
          .delete()
          .eq('id', testId);

        if (error) throw error;

        loadTests();
        alert('Test muvaffaqiyatli o\'chirildi!');

      } catch (error) {
        console.error('Testni o\'chirish xatosi:', error);
        alert('Xatolik: ' + error.message);
      }
    }

    // Testni boshlash
    function startTest(testId) {
      alert('Test ishlash sahifasi tez orada qo\'shiladi!');
    }

    // ==================== BOSHLANG'ICH SOZLAMALAR ====================

    // Navigation linklarini yangilash
    document.addEventListener("DOMContentLoaded", function() {
      document.querySelector('a[href="#create"]').addEventListener('click', function(e) {
        e.preventDefault();
        const currentUser = JSON.parse(localStorage.getItem('currentUser'));
        if (currentUser) {
          showTestCreator();
        } else {
          alert('Iltimos, avval tizimga kiring!');
        }
      });

      document.querySelector('a[href="#work"]').addEventListener('click', function(e) {
        e.preventDefault();
        alert('Test ishlash sahifasi tez orada qo\'shiladi!');
      });

      document.querySelector('a[href="#register"]').addEventListener('click', function(e) {
        e.preventDefault();
        goToRegister();
      });
    });

    // Bosilganda tilni o'zgartirish
    document.querySelectorAll(".lang-btn").forEach(btn=>{
      btn.addEventListener("click",()=>applyTranslations(btn.dataset.lang));
    });

    // Boshlang'ich til
    document.addEventListener("DOMContentLoaded",()=>{
      const savedLang=localStorage.getItem("lang")||"uz";
      applyTranslations(savedLang);
      addQuestion(); // Birinchi savolni qo'shish
    });

    // ID input ga faqat raqam kiritish
    document.getElementById('loginID').addEventListener('input', function(e) {
      this.value = this.value.replace(/\D/g, '');
    });

    // Supabase bog'lanishini test qilish
    async function testSupabaseConnection() {
      try {
        console.log('🔄 Supabase bog\'lanish testi...');
        
        const { data, error } = await supabase
          .from('users')
          .select('count')
          .limit(1);
        
        if (error) {
          console.error('❌ Bog\'lanish xatosi:', error);
          return false;
        }
        
        console.log('✅ Supabase ga muvaffaqiyatli bog\'lanildi!');
        return true;
        
      } catch (error) {
        console.error('❌ Test xatosi:', error);
        return false;
      }
    }

    // Dastur yuklanganda test qilish
    document.addEventListener("DOMContentLoaded", async function() {
      console.log('🚀 Dastur yuklandi, tekshirishlar boshlandi...');
      
      await testSupabaseConnection();
      console.log('🎯 Barcha tekshirishlar tugadi');
    });
  </script>
</body>
</html>
