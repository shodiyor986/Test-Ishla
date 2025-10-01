import os
import requests
import json
from base64 import b64encode

class GitHubUploader:
    def __init__(self, token, username):
        self.token = token
        self.username = username
        self.headers = {
            'Authorization': f'token {token}',
            'Accept': 'application/vnd.github.v3+json'
        }
        self.base_url = 'https://api.github.com'
    
    def create_repository(self, repo_name, description="Test Ishla Platformasi"):
        """Yangi repository yaratish"""
        url = f'{self.base_url}/user/repos'
        data = {
            'name': repo_name,
            'description': description,
            'auto_init': True,
            'private': False
        }
        
        response = requests.post(url, headers=self.headers, json=data)
        
        if response.status_code == 201:
            print(f"✅ Repository '{repo_name}' muvaffaqiyatli yaratildi!")
            return response.json()
        else:
            print(f"❌ Xatolik: {response.json()}")
            return None
    
    def create_file(self, repo_name, file_path, content, commit_message):
        """Fayl yaratish yoki yangilash"""
        url = f'{self.base_url}/repos/{self.username}/{repo_name}/contents/{file_path}'
        
        # Content ni base64 ga o'tkazish
        content_bytes = content.encode('utf-8')
        content_b64 = b64encode(content_bytes).decode('utf-8')
        
        data = {
            'message': commit_message,
            'content': content_b64,
            'branch': 'main'
        }
        
        response = requests.put(url, headers=self.headers, json=data)
        
        if response.status_code in [200, 201]:
            print(f"✅ Fayl '{file_path}' muvaffaqiyatli yuklandi!")
            return response.json()
        else:
            print(f"❌ Xatolik: {response.json()}")
            return None
    
    def enable_pages(self, repo_name):
        """GitHub Pages ni yoqish"""
        url = f'{self.base_url}/repos/{self.username}/{repo_name}/pages'
        data = {
            'source': {
                'branch': 'main',
                'path': '/'
            }
        }
        
        response = requests.post(url, headers=self.headers, json=data)
        
        if response.status_code == 201:
            print("✅ GitHub Pages muvaffaqiyatli yoqildi!")
            return response.json()
        else:
            print(f"⚠️ GitHub Pages yoqishda xatolik: {response.json()}")
            return None

def main():
    # GitHub Token o'rnating (GitHub -> Settings -> Developer settings -> Personal access tokens)
    GITHUB_TOKEN = "your_github_token_here"
    GITHUB_USERNAME = "your_username_here"
    REPO_NAME = "test-ishla"
    
    # HTML kod
    html_content = '''<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test Ishla - Bosh Sahifa</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: white;
            min-height: 100vh;
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        header {
            background: rgba(0, 0, 0, 0.7);
            padding: 1rem 0;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
            position: relative;
        }
        
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: relative;
            min-height: 60px;
        }
        
        .logo {
            font-size: 2rem;
            font-weight: bold;
            color: #4cd137;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
        }
        
        .lang-switcher {
            position: absolute;
            left: 0;
            top: 50%;
            transform: translateY(-50%);
        }
        
        .lang-switcher select {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.3);
            color: white;
            padding: 8px 12px;
            border-radius: 5px;
            outline: none;
            cursor: pointer;
        }
        
        .lang-switcher select option {
            background: #2a5298;
            color: white;
        }
        
        .clock {
            position: absolute;
            right: 0;
            top: 50%;
            transform: translateY(-50%);
            background: rgba(255, 255, 255, 0.1);
            padding: 8px 15px;
            border-radius: 5px;
            font-size: 0.9rem;
            backdrop-filter: blur(10px);
        }
        
        nav {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            padding: 1rem 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .nav-links {
            display: flex;
            justify-content: center;
            list-style: none;
        }
        
        .nav-links li {
            margin: 0 15px;
        }
        
        .nav-links a {
            color: white;
            text-decoration: none;
            font-weight: 500;
            padding: 8px 16px;
            border-radius: 5px;
            transition: all 0.3s ease;
            display: block;
        }
        
        .nav-links a:hover {
            background: rgba(255, 255, 255, 0.2);
            color: #4cd137;
        }
        
        .hero {
            padding: 4rem 0;
            text-align: center;
        }
        
        .hero h1 {
            font-size: 3rem;
            margin-bottom: 1.5rem;
            color: #4cd137;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
        }
        
        .hero p {
            font-size: 1.2rem;
            max-width: 800px;
            margin: 0 auto 2rem;
            opacity: 0.9;
            line-height: 1.8;
        }
        
        .features {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin: 3rem 0;
        }
        
        .feature-card {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 2rem;
            text-align: center;
            transition: all 0.3s ease;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .feature-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }
        
        .feature-icon {
            font-size: 3.5rem;
            margin-bottom: 1.5rem;
            display: block;
        }
        
        .feature-card h3 {
            margin-bottom: 1rem;
            color: #4cd137;
            font-size: 1.5rem;
        }
        
        .feature-card p {
            opacity: 0.9;
            line-height: 1.6;
        }
        
        footer {
            background: rgba(0, 0, 0, 0.7);
            padding: 2rem 0;
            text-align: center;
            margin-top: 4rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        footer p {
            opacity: 0.8;
        }
        
        @media (max-width: 768px) {
            .header-content {
                flex-direction: column;
                text-align: center;
                gap: 15px;
            }
            
            .logo {
                position: static;
                transform: none;
                order: 1;
            }
            
            .lang-switcher {
                position: static;
                transform: none;
                order: 2;
            }
            
            .clock {
                position: static;
                transform: none;
                order: 3;
            }
            
            .hero h1 {
                font-size: 2.2rem;
            }
            
            .hero p {
                font-size: 1.1rem;
                padding: 0 15px;
            }
            
            .nav-links {
                flex-direction: column;
                gap: 10px;
            }
            
            .nav-links li {
                margin: 0;
            }
            
            .features {
                grid-template-columns: 1fr;
                padding: 0 15px;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <div class="header-content">
                <div class="lang-switcher">
                    <select id="lang">
                        <option value="uz">O'zbek</option>
                        <option value="en">English</option>
                        <option value="ru">Русский</option>
                    </select>
                </div>
                <div class="logo">Test Ishla</div>
                <div class="clock" id="clock">Yuklanmoqda...</div>
            </div>
        </div>
    </header>
    
    <nav>
        <div class="container">
            <ul class="nav-links">
                <li><a href="#" data-i18n="menuHome">Bosh Sahifa</a></li>
                <li><a href="#" data-i18n="menuPage2">Test Yaratish</a></li>
                <li><a href="#" data-i18n="menuPage3">Natijalar</a></li>
            </ul>
        </div>
    </nav>
    
    <main class="container">
        <section class="hero">
            <h1 data-i18n="homeTitle">Test Ishla Platformasi</h1>
            <p data-i18n="homeText">
                Ushbu platforma orqali siz turli testlarni yaratishingiz, ularni boshqalar bilan ulashingiz va natijalarni kuzatishingiz mumkin. 
                O'quv jarayonini qiziqarli va samarali qilish uchun mo'ljallangan.
            </p>
        </section>
        
        <section class="features">
            <div class="feature-card">
                <div class="feature-icon">📝</div>
                <h3>Test Yaratish</h3>
                <p>Oson va tez testlar yarating. Turli savol turlaridan foydalaning. Har qanday mavzuda test tuzing.</p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">🔗</div>
                <h3>Ulashish</h3>
                <p>Yaratgan testingizni boshqalar bilan ulashing va natijalarni kuzating. O'quvchilar bilan baham ko'ring.</p>
            </div>
            
            <div class="feature-card">
                <div class="feature-icon">📊</div>
                <h3>Natijalar Tahlili</h3>
                <p>Batafsil natijalar tahlili va statistik ma'lumotlar oling. O'quvchilarning rivojlanishini kuzating.</p>
            </div>
        </section>
    </main>
    
    <footer>
        <div class="container">
            <p data-i18n="footer">© 2025 Test Ishla. Barcha huquqlar himoyalangan.</p>
        </div>
    </footer>
    
    <script>
        // Tillar matnlari
        const translations = {
            uz: {
                menuHome: "Bosh Sahifa",
                menuPage2: "Test Yaratish",
                menuPage3: "Natijalar",
                homeTitle: "Test Ishla Platformasi",
                homeText: "Ushbu platforma orqali siz turli testlarni yaratishingiz, ularni boshqalar bilan ulashingiz va natijalarni kuzatishingiz mumkin. O'quv jarayonini qiziqarli va samarali qilish uchun mo'ljallangan.",
                footer: "© 2025 Test Ishla. Barcha huquqlar himoyalangan."
            },
            en: {
                menuHome: "Home",
                menuPage2: "Create Test",
                menuPage3: "Results",
                homeTitle: "Test Ishla Platform",
                homeText: "With this platform, you can create various tests, share them with others, and monitor results. Designed to make the learning process interesting and effective.",
                footer: "© 2025 Test Ishla. All rights reserved."
            },
            ru: {
                menuHome: "Главная",
                menuPage2: "Создать Тест",
                menuPage3: "Результаты",
                homeTitle: "Платформа Test Ishla",
                homeText: "С этой платформой вы можете создавать различные тесты, делиться ими с другими и отслеживать результаты. Разработано, чтобы сделать процесс обучения интересным и эффективным.",
                footer: "© 2025 Test Ishla. Все права защищены."
            }
        };

        // Tarjima funksiyasi
        function applyTranslations(lang) {
            document.querySelectorAll("[data-i18n]").forEach(el => {
                const key = el.getAttribute("data-i18n");
                if (translations[lang] && translations[lang][key]) {
                    el.textContent = translations[lang][key];
                }
            });
            document.title = translations[lang].homeTitle + " - Test Ishla";
            localStorage.setItem("lang", lang);
        }

        // Tilni tanlash
        document.getElementById("lang").addEventListener("change", (e) => {
            applyTranslations(e.target.value);
        });

        // Dastlabki tilni yuklash
        function initializeLanguage() {
            const savedLang = localStorage.getItem("lang") || "uz";
            const langSelect = document.getElementById("lang");
            
            if (langSelect) {
                langSelect.value = savedLang;
                applyTranslations(savedLang);
            }
        }

        // Soat va sana
        function updateClock() {
            const now = new Date();
            const lang = localStorage.getItem("lang") || "uz";
            
            // Soat va sana formatlari
            const timeOptions = {
                hour: '2-digit',
                minute: '2-digit',
                second: '2-digit'
            };
            
            const dateOptions = {
                weekday: 'long',
                year: 'numeric',
                month: 'long',
                day: 'numeric'
            };
            
            let timeString, dateString;
            
            try {
                // Soatni formatlash
                timeString = now.toLocaleTimeString(lang === 'uz' ? 'uz-UZ' : lang, timeOptions);
                
                // Sanani formatlash
                dateString = now.toLocaleDateString(lang === 'uz' ? 'uz-UZ' : lang, dateOptions);
                
                document.getElementById('clock').textContent = `${timeString} | ${dateString}`;
            } catch (error) {
                // Agar lokal muammo bo'lsa, oddiy formatda ko'rsatamiz
                document.getElementById('clock').textContent = now.toLocaleString();
            }
        }

        // DOM yuklanganida ishga tushirish
        document.addEventListener('DOMContentLoaded', function() {
            initializeLanguage();
            updateClock();
            setInterval(updateClock, 1000);
        });

        // Agar DOM allaqachon yuklangan bo'lsa
        if (document.readyState === 'loading') {
            document.addEventListener('DOMContentLoaded', initializeLanguage);
        } else {
            initializeLanguage();
        }
    </script>
</body>
</html>'''
    
    # README.md kontenti
    readme_content = '''# Test Ishla Platformasi 🚀

## 🌐 Saytni Ko'rish
**[Live Demo](https://{username}.github.io/{repo_name})**

## 📋 Loyiha Haqida

"Test Ishla" - bu turli testlar yaratish, ulashish va natijalarni tahlil qilish uchun mo'ljallangan innovatsion platforma.

### ✨ Asosiy Xususiyatlar

- 📝 **Test Yaratish** - Oson va tez testlar yarating
- 🔗 **Ulashish** - Testlarni boshqalar bilan baham ko'ring  
- 📊 **Natijalar Tahlili** - Batafsil statistik ma'lumotlar
- 🌐 **Ko'p Tillik** - O'zbek, Ingliz, Rus tillarida
- ⏰ **Real Vaqt** - Soat va sana ko'rsatkichi

## 🛠 Texnologiyalar

- **HTML5** - Semantik struktur
- **CSS3** - Zamonaviy dizayn va animatsiyalar
- **JavaScript** - Interaktiv funksionallik
- **GitHub Pages** - Hosting

## 🚀 O'rnatish

1. Repository ni klon qiling:
```bash
git clone https://github.com/{username}/{repo_name}.git
