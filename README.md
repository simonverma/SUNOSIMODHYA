<!doctype html>
<html lang="en">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Suno Simodhya - Premium Storytelling App</title>
  <script src="/_sdk/data_sdk.js"></script>
  <script src="/_sdk/element_sdk.js"></script><!-- Google Sign-In SDK -->
  <script src="https://accounts.google.com/gsi/client" async defer></script><!-- Facebook SDK -->
  <script async defer crossorigin="anonymous" src="https://connect.facebook.net/en_US/sdk.js"></script>
  <style>
        body {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'SF Pro Display', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100%;
            overflow-x: hidden;
        }

        * {
            box-sizing: border-box;
        }

        .app-container {
            max-width: 375px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            min-height: 100vh;
            position: relative;
            box-shadow: 0 0 50px rgba(0, 0, 0, 0.1);
        }

        .screen {
            display: none;
            padding: 20px;
            min-height: 100vh;
            animation: slideIn 0.3s ease-out;
        }

        .screen.active {
            display: block;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateX(20px); }
            to { opacity: 1; transform: translateX(0); }
        }

        .glass-card {
            background: rgba(255, 255, 255, 0.8);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            padding: 20px;
            margin: 15px 0;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .header {
            text-align: center;
            padding: 20px 0;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border-radius: 0 0 30px 30px;
            margin: -20px -20px 20px -20px;
        }

        .logo {
            font-size: 28px;
            font-weight: 700;
            margin-bottom: 5px;
        }

        .subtitle {
            font-size: 14px;
            opacity: 0.9;
        }

        .btn-primary {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
            margin: 10px 0;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
        }

        .btn-secondary {
            background: rgba(255, 255, 255, 0.9);
            color: #667eea;
            border: 2px solid #667eea;
            padding: 12px 30px;
            border-radius: 25px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
            margin: 10px 0;
            transition: all 0.3s ease;
        }

        .search-bar {
            background: rgba(255, 255, 255, 0.9);
            border: none;
            padding: 15px 20px;
            border-radius: 25px;
            width: 100%;
            font-size: 16px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            margin: 15px 0;
        }

        .category-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin: 20px 0;
        }

        .category-card {
            background: linear-gradient(135deg, rgba(255, 255, 255, 0.9), rgba(255, 255, 255, 0.7));
            border-radius: 20px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 1px solid rgba(255, 255, 255, 0.3);
        }

        .category-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
        }

        .category-icon {
            font-size: 32px;
            margin-bottom: 10px;
            display: block;
        }

        .category-title {
            font-size: 14px;
            font-weight: 600;
            color: #333;
        }

        .filter-chips {
            display: flex;
            gap: 10px;
            margin: 15px 0;
            overflow-x: auto;
            padding-bottom: 5px;
        }

        .chip {
            background: rgba(255, 255, 255, 0.9);
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 14px;
            font-weight: 500;
            cursor: pointer;
            white-space: nowrap;
            transition: all 0.3s ease;
            border: 1px solid rgba(102, 126, 234, 0.2);
        }

        .chip.active {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
        }

        .language-selector {
            background: rgba(255, 255, 255, 0.9);
            border: none;
            padding: 12px 20px;
            border-radius: 25px;
            font-size: 16px;
            cursor: pointer;
            width: 100%;
            margin: 10px 0;
        }

        .content-card {
            background: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            padding: 15px;
            margin: 10px 0;
            display: flex;
            align-items: center;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .content-card:hover {
            transform: translateX(5px);
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
        }

        .content-thumbnail {
            width: 60px;
            height: 60px;
            border-radius: 10px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            margin-right: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 24px;
        }

        .content-info h3 {
            margin: 0 0 5px 0;
            font-size: 16px;
            font-weight: 600;
            color: #333;
        }

        .content-info p {
            margin: 0;
            font-size: 14px;
            color: #666;
        }

        .player-controls {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            margin: 20px 0;
        }

        .control-btn {
            background: rgba(255, 255, 255, 0.9);
            border: none;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 20px;
        }

        .control-btn.play {
            width: 70px;
            height: 70px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            font-size: 24px;
        }

        .progress-bar {
            width: 100%;
            height: 6px;
            background: rgba(255, 255, 255, 0.3);
            border-radius: 3px;
            margin: 20px 0;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(135deg, #667eea, #764ba2);
            width: 30%;
            border-radius: 3px;
            transition: width 0.3s ease;
        }

        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 375px;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            padding: 15px 20px;
            display: flex;
            justify-content: space-around;
            border-top: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 25px 25px 0 0;
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            cursor: pointer;
            transition: all 0.3s ease;
            padding: 5px;
        }

        .nav-item.active {
            color: #667eea;
        }

        .nav-icon {
            font-size: 24px;
            margin-bottom: 5px;
        }

        .nav-label {
            font-size: 12px;
            font-weight: 500;
        }

        .onboarding-slide {
            text-align: center;
            padding: 40px 20px;
        }

        .onboarding-icon {
            font-size: 80px;
            margin: 40px 0;
            background: linear-gradient(135deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .onboarding-title {
            font-size: 24px;
            font-weight: 700;
            margin: 20px 0;
            color: #333;
        }

        .onboarding-desc {
            font-size: 16px;
            color: #666;
            line-height: 1.5;
            margin-bottom: 40px;
        }

        .slide-nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 40px;
        }

        .skip-btn {
            background: none;
            border: none;
            color: #666;
            font-size: 16px;
            cursor: pointer;
        }

        .dots-indicator {
            display: flex;
            gap: 8px;
        }

        .dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: rgba(102, 126, 234, 0.3);
            transition: all 0.3s ease;
        }

        .dot.active {
            background: #667eea;
            width: 20px;
            border-radius: 10px;
        }

        .form-group {
            margin: 15px 0;
        }

        .form-input {
            width: 100%;
            padding: 15px 20px;
            border: 2px solid rgba(102, 126, 234, 0.2);
            border-radius: 25px;
            font-size: 16px;
            background: rgba(255, 255, 255, 0.9);
            transition: all 0.3s ease;
        }

        .form-input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .social-login {
            display: flex;
            gap: 10px;
            margin: 20px 0;
        }

        .social-btn {
            flex: 1;
            padding: 12px 16px;
            border: 2px solid rgba(102, 126, 234, 0.2);
            border-radius: 25px;
            background: rgba(255, 255, 255, 0.9);
            cursor: pointer;
            font-size: 14px;
            font-weight: 600;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
        }

        .social-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }

        .social-btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .video-player {
            width: 100%;
            height: 200px;
            background: #000;
            border-radius: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 48px;
            margin: 20px 0;
        }

        .reading-controls {
            display: flex;
            justify-content: space-around;
            padding: 15px;
            background: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            margin: 20px 0;
        }

        .reading-btn {
            background: none;
            border: none;
            padding: 10px;
            border-radius: 10px;
            cursor: pointer;
            font-size: 18px;
            transition: all 0.3s ease;
        }

        .reading-btn:hover {
            background: rgba(102, 126, 234, 0.1);
        }

        .loading-spinner {
            display: none;
            width: 20px;
            height: 20px;
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top-color: white;
            animation: spin 1s ease-in-out infinite;
            margin: 0 auto;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        .error-message {
            background: rgba(255, 107, 107, 0.1);
            color: #ff6b6b;
            padding: 10px 15px;
            border-radius: 10px;
            margin: 10px 0;
            font-size: 14px;
            display: none;
        }

        .success-message {
            background: rgba(81, 207, 102, 0.1);
            color: #51cf66;
            padding: 10px 15px;
            border-radius: 10px;
            margin: 10px 0;
            font-size: 14px;
            display: none;
        }
    </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="https://cdn.tailwindcss.com" type="text/javascript"></script>
 </head>
 <body>
  <div class="app-container"><!-- Onboarding Screen 1 -->
   <div class="screen active" id="onboarding1">
    <div class="onboarding-slide">
     <div class="onboarding-icon">
      🎧
     </div>
     <h2 class="onboarding-title">Listen to Amazing AudioBooks</h2>
     <p class="onboarding-desc">Immerse yourself in captivating stories with high-quality narration and crystal-clear audio.</p>
     <div class="slide-nav"><button class="skip-btn" onclick="showScreen('login')">Skip</button>
      <div class="dots-indicator">
       <div class="dot active"></div>
       <div class="dot"></div>
       <div class="dot"></div>
      </div><button class="btn-primary" style="width: auto; padding: 10px 20px;" onclick="showScreen('onboarding2')">Next</button>
     </div>
    </div>
   </div><!-- Onboarding Screen 2 -->
   <div class="screen" id="onboarding2">
    <div class="onboarding-slide">
     <div class="onboarding-icon">
      📖
     </div>
     <h2 class="onboarding-title">Read Beautiful eBooks</h2>
     <p class="onboarding-desc">Enjoy a premium reading experience with customizable fonts, themes, and seamless page transitions.</p>
     <div class="slide-nav"><button class="skip-btn" onclick="showScreen('login')">Skip</button>
      <div class="dots-indicator">
       <div class="dot"></div>
       <div class="dot active"></div>
       <div class="dot"></div>
      </div><button class="btn-primary" style="width: auto; padding: 10px 20px;" onclick="showScreen('onboarding3')">Next</button>
     </div>
    </div>
   </div><!-- Onboarding Screen 3 -->
   <div class="screen" id="onboarding3">
    <div class="onboarding-slide">
     <div class="onboarding-icon">
      🎬
     </div>
     <h2 class="onboarding-title">Watch Story Videos</h2>
     <p class="onboarding-desc">Experience stories come to life with engaging short videos and full-length cinematic content.</p>
     <div class="slide-nav"><button class="skip-btn" onclick="showScreen('login')">Skip</button>
      <div class="dots-indicator">
       <div class="dot"></div>
       <div class="dot"></div>
       <div class="dot active"></div>
      </div><button class="btn-primary" style="width: auto; padding: 10px 20px;" onclick="showScreen('login')">Get Started</button>
     </div>
    </div>
   </div><!-- Login Screen -->
   <div class="screen" id="login">
    <div class="header">
     <div class="logo" id="app-title">
      Suno Simodhya
     </div>
     <div class="subtitle">
      Premium Storytelling Experience
     </div>
    </div>
    <div class="glass-card">
     <h2 style="text-align: center; margin-bottom: 30px; color: #333;" id="welcome-message">Welcome to Suno Simodhya</h2><button class="btn-primary" onclick="showScreen('home')">Login</button> <button class="btn-secondary" onclick="showScreen('signup')">Sign Up</button>
     <div class="social-login"><button class="social-btn" id="google-signin-btn" onclick="signInWithGoogle()">
       <svg width="18" height="18" viewbox="0 0 24 24" style="margin-right: 8px;"><path fill="#4285F4" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z" /> <path fill="#34A853" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z" /> <path fill="#FBBC05" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l2.85-2.22.81-.62z" /> <path fill="#EA4335" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z" />
       </svg> Continue with Google </button> <button class="social-btn" id="facebook-signin-btn" onclick="signInWithFacebook()">
       <svg width="18" height="18" viewbox="0 0 24 24" style="margin-right: 8px;"><path fill="#1877F2" d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z" />
       </svg> Continue with Facebook </button>
     </div>
     <p style="text-align: center; margin-top: 20px;"><a href="#" style="color: #667eea; text-decoration: none;">Forgot Password?</a></p>
    </div>
   </div><!-- Sign Up Screen -->
   <div class="screen" id="signup">
    <div class="header">
     <div class="logo">
      Create Account
     </div>
     <div class="subtitle">
      Join the storytelling community
     </div>
    </div>
    <div class="glass-card">
     <div class="form-group"><input type="text" class="form-input" placeholder="Full Name" required>
     </div>
     <div class="form-group"><input type="email" class="form-input" placeholder="Email Address" required>
     </div>
     <div class="form-group"><input type="password" class="form-input" placeholder="Password" required>
     </div><button class="btn-primary" onclick="showScreen('home')">Create Account</button>
     <p style="text-align: center; margin-top: 20px;">Already have an account? <a href="#" onclick="showScreen('login')" style="color: #667eea; text-decoration: none;">Login</a></p>
    </div>
   </div><!-- Home Screen -->
   <div class="screen" id="home">
    <div class="header">
     <div class="logo" id="home-title">
      Suno Simodhya
     </div>
     <div class="subtitle">
      Discover Amazing Stories
     </div>
    </div><input type="text" class="search-bar" id="search-placeholder" placeholder="Search stories, books, videos...">
    <div class="filter-chips">
     <div class="chip active">
      Trending
     </div>
     <div class="chip">
      New
     </div>
     <div class="chip">
      Popular
     </div>
     <div class="chip">
      Featured
     </div>
    </div><select class="language-selector" onchange="changeLanguage(this.value)"> <option value="en">🌐 English</option> <option value="hi">🇮🇳 Hindi</option> <option value="ta">🇮🇳 Tamil</option> <option value="te">🇮🇳 Telugu</option> <option value="mr">🇮🇳 Marathi</option> <option value="bn">🇮🇳 Bengali</option> </select>
    <div class="category-grid">
     <div class="category-card" onclick="showScreen('audiobooks')"><span class="category-icon">🎧</span>
      <div class="category-title">
       AudioBooks
      </div>
     </div>
     <div class="category-card" onclick="showScreen('ebooks')"><span class="category-icon">📖</span>
      <div class="category-title">
       eBooks
      </div>
     </div>
     <div class="category-card" onclick="showScreen('short-videos')"><span class="category-icon">🎞️</span>
      <div class="category-title">
       Short Videos
      </div>
     </div>
     <div class="category-card" onclick="showScreen('full-videos')"><span class="category-icon">🎬</span>
      <div class="category-title">
       Full Videos
      </div>
     </div>
     <div class="category-card" onclick="showScreen('favorites')"><span class="category-icon">❤️</span>
      <div class="category-title">
       Favorites
      </div>
     </div>
     <div class="category-card" onclick="showScreen('profile')"><span class="category-icon">👤</span>
      <div class="category-title">
       Profile
      </div>
     </div>
    </div>
    <div style="padding-bottom: 100px;"></div>
   </div><!-- Search Screen -->
   <div class="screen" id="search">
    <div class="header">
     <div class="logo">
      Search
     </div>
     <div class="subtitle">
      Find your next favorite story
     </div>
    </div><input type="text" class="search-bar" placeholder="Search by title, author, genre...">
    <div class="glass-card">
     <h3 style="margin-top: 0;">Filters</h3><select class="language-selector"> <option>All Categories</option> <option>AudioBooks</option> <option>eBooks</option> <option>Videos</option> </select> <select class="language-selector"> <option>All Languages</option> <option>Hindi</option> <option>English</option> <option>Tamil</option> </select> <select class="language-selector"> <option>Any Duration</option> <option>Short (&lt; 30 min)</option> <option>Medium (30-60 min)</option> <option>Long (&gt; 60 min)</option> </select>
    </div>
    <div class="glass-card">
     <h3 style="margin-top: 0;">Trending Searches</h3>
     <div class="filter-chips">
      <div class="chip">
       Horror Stories
      </div>
      <div class="chip">
       Romance
      </div>
      <div class="chip">
       Motivation
      </div>
      <div class="chip">
       Kids Stories
      </div>
     </div>
    </div>
    <div style="padding-bottom: 100px;"></div>
   </div><!-- Categories Screen -->
   <div class="screen" id="categories">
    <div class="header">
     <div class="logo">
      Categories
     </div>
     <div class="subtitle">
      Explore by genre
     </div>
    </div>
    <div class="category-grid">
     <div class="category-card"><span class="category-icon">💪</span>
      <div class="category-title">
       Motivation
      </div>
     </div>
     <div class="category-card"><span class="category-icon">👻</span>
      <div class="category-title">
       Horror
      </div>
     </div>
     <div class="category-card"><span class="category-icon">💕</span>
      <div class="category-title">
       Romance
      </div>
     </div>
     <div class="category-card"><span class="category-icon">👶</span>
      <div class="category-title">
       Kids Stories
      </div>
     </div>
     <div class="category-card"><span class="category-icon">📚</span>
      <div class="category-title">
       Study
      </div>
     </div>
     <div class="category-card"><span class="category-icon">🏛️</span>
      <div class="category-title">
       History
      </div>
     </div>
     <div class="category-card"><span class="category-icon">🧠</span>
      <div class="category-title">
       Self-Help
      </div>
     </div>
     <div class="category-card"><span class="category-icon">🙏</span>
      <div class="category-title">
       Spiritual
      </div>
     </div>
     <div class="category-card"><span class="category-icon">🔍</span>
      <div class="category-title">
       Crime
      </div>
     </div>
     <div class="category-card"><span class="category-icon">👑</span>
      <div class="category-title">
       Biography
      </div>
     </div>
    </div>
    <div style="padding-bottom: 100px;"></div>
   </div><!-- AudioBooks Screen -->
   <div class="screen" id="audiobooks">
    <div class="header">
     <div class="logo">
      AudioBooks
     </div>
     <div class="subtitle">
      Listen to amazing stories
     </div>
    </div>
    <div class="filter-chips">
     <div class="chip active">
      All
     </div>
     <div class="chip">
      New Releases
     </div>
     <div class="chip">
      Popular
     </div>
     <div class="chip">
      Downloaded
     </div>
    </div>
    <div class="content-card" onclick="showScreen('audiobook-player')">
     <div class="content-thumbnail">
      🎧
     </div>
     <div class="content-info">
      <h3>The Mysterious Tale</h3>
      <p>By Author Name • 2h 30m • Hindi</p>
     </div>
    </div>
    <div class="content-card">
     <div class="content-thumbnail">
      📚
     </div>
     <div class="content-info">
      <h3>Love in the Mountains</h3>
      <p>By Romance Writer • 1h 45m • English</p>
     </div>
    </div>
    <div class="content-card">
     <div class="content-thumbnail">
      👻
     </div>
     <div class="content-info">
      <h3>Haunted Mansion</h3>
      <p>By Horror Master • 3h 15m • Tamil</p>
     </div>
    </div>
    <div style="padding-bottom: 100px;"></div>
   </div><!-- AudioBook Player -->
   <div class="screen" id="audiobook-player">
    <div class="header">
     <div class="logo">
      Now Playing
     </div>
     <div class="subtitle">
      The Mysterious Tale
     </div>
    </div>
    <div class="glass-card" style="text-align: center;">
     <div style="width: 200px; height: 200px; background: linear-gradient(135deg, #667eea, #764ba2); border-radius: 20px; margin: 20px auto; display: flex; align-items: center; justify-content: center; color: white; font-size: 48px;">
      🎧
     </div>
     <h2 style="margin: 20px 0 5px 0;">The Mysterious Tale</h2>
     <p style="color: #666; margin: 0 0 20px 0;">By Author Name</p>
     <div class="progress-bar">
      <div class="progress-fill"></div>
     </div>
     <div style="display: flex; justify-content: space-between; font-size: 14px; color: #666; margin-bottom: 20px;"><span>15:30</span> <span>2:30:00</span>
     </div>
     <div class="player-controls"><button class="control-btn">⏮️</button> <button class="control-btn">⏪</button> <button class="control-btn play">▶️</button> <button class="control-btn">⏩</button> <button class="control-btn">⏭️</button>
     </div>
     <div class="filter-chips" style="justify-content: center;">
      <div class="chip">
       💾 Download
      </div>
      <div class="chip">
       ❤️ Favorite
      </div>
      <div class="chip">
       📤 Share
      </div>
      <div class="chip">
       ⏰ Sleep Timer
      </div>
     </div>
    </div>
    <div style="padding-bottom: 100px;"></div>
   </div><!-- eBooks Screen -->
   <div class="screen" id="ebooks">
    <div class="header">
     <div class="logo">
      eBooks
     </div>
     <div class="subtitle">
      Read amazing stories
     </div>
    </div>
    <div class="filter-chips">
     <div class="chip active">
      All
     </div>
     <div class="chip">
      Recently Added
     </div>
     <div class="chip">
      Bestsellers
     </div>
     <div class="chip">
      Downloaded
     </div>
    </div>
    <div class="content-card" onclick="showScreen('ebook-reader')">
     <div class="content-thumbnail">
      📖
     </div>
     <div class="content-info">
      <h3>Digital Dreams</h3>
      <p>By Tech Author • 250 pages • English</p>
     </div>
    </div>
    <div class="content-card">
     <div class="content-thumbnail">
      💕
     </div>
     <div class="content-info">
      <h3>Hearts Entwined</h3>
      <p>By Romance Queen • 180 pages • Hindi</p>
     </div>
    </div>
    <div style="padding-bottom: 100px;"></div>
   </div><!-- eBook Reader -->
   <div class="screen" id="ebook-reader">
    <div class="header">
     <div class="logo">
      Digital Dreams
     </div>
     <div class="subtitle">
      Chapter 1: The Beginning
     </div>
    </div>
    <div class="glass-card">
     <div style="line-height: 1.6; font-size: 16px; color: #333;">
      <h3>Chapter 1: The Beginning</h3>
      <p>In the heart of the digital age, where technology and humanity intersect, lies a story that will change everything you thought you knew about the future...</p>
      <p>Sarah looked at her screen, the blue light reflecting in her eyes as she typed the final lines of code that would revolutionize the world. Little did she know that this moment would mark the beginning of an extraordinary journey.</p>
      <p>The cursor blinked steadily, waiting for her next command. But this time, something was different. The screen flickered, and for a brief moment, she could have sworn she saw something looking back at her...</p>
     </div>
    </div>
    <div class="reading-controls"><button class="reading-btn">🔆</button> <button class="reading-btn">📖</button> <button class="reading-btn">🎨</button> <button class="reading-btn">📝</button> <button class="reading-btn">🔖</button> <button class="reading-btn">⚙️</button>
    </div>
    <div style="display: flex; justify-content: space-between; margin: 20px 0;"><button class="btn-secondary" style="width: 45%;">← Previous</button> <button class="btn-primary" style="width: 45%;">Next →</button>
    </div>
    <div style="padding-bottom: 100px;"></div>
   </div><!-- Short Videos Screen -->
   <div class="screen" id="short-videos">
    <div class="header">
     <div class="logo">
      Short Videos
     </div>
     <div class="subtitle">
      Quick story bites
     </div>
    </div>
    <div class="video-player">
     ▶️
    </div>
    <div class="glass-card">
     <h3 style="margin-top: 0;">The Magic Forest</h3>
     <p style="color: #666;">A mystical journey through an enchanted forest where every tree tells a story.</p>
     <div class="filter-chips">
      <div class="chip">
       👍 Like
      </div>
      <div class="chip">
       📤 Share
      </div>
      <div class="chip">
       💾 Save
      </div>
      <div class="chip">
       ⬇️ Download
      </div>
     </div>
    </div>
    <div class="content-card">
     <div class="content-thumbnail">
      🎬
     </div>
     <div class="content-info">
      <h3>Urban Legends</h3>
      <p>Horror • 3:45 • Hindi</p>
     </div>
    </div>
    <div style="padding-bottom: 100px;"></div>
   </div><!-- Full Videos Screen -->
   <div class="screen" id="full-videos">
    <div class="header">
     <div class="logo">
      Full-Length Videos
     </div>
     <div class="subtitle">
      Complete story experiences
     </div>
    </div>
    <div class="video-player">
     ▶️
    </div>
    <div class="glass-card">
     <h3 style="margin-top: 0;">The Epic Saga</h3>
     <p style="color: #666;">Episode 1 of 12 • 45 minutes</p>
     <div class="progress-bar">
      <div class="progress-fill" style="width: 60%;"></div>
     </div>
     <div class="filter-chips">
      <div class="chip">
       📋 Episodes
      </div>
      <div class="chip">
       ⏯️ Continue
      </div>
      <div class="chip">
       💾 Download
      </div>
     </div>
    </div>
    <div style="padding-bottom: 100px;"></div>
   </div><!-- Favorites Screen -->
   <div class="screen" id="favorites">
    <div class="header">
     <div class="logo">
      Favorites
     </div>
     <div class="subtitle">
      Your saved content
     </div>
    </div>
    <div class="filter-chips">
     <div class="chip active">
      All
     </div>
     <div class="chip">
      AudioBooks
     </div>
     <div class="chip">
      eBooks
     </div>
     <div class="chip">
      Videos
     </div>
    </div>
    <div class="content-card">
     <div class="content-thumbnail">
      ❤️
     </div>
     <div class="content-info">
      <h3>The Mysterious Tale</h3>
      <p>AudioBook • 2h 30m • Added 2 days ago</p>
     </div>
    </div>
    <div class="content-card">
     <div class="content-thumbnail">
      💕
     </div>
     <div class="content-info">
      <h3>Digital Dreams</h3>
      <p>eBook • 250 pages • Added 1 week ago</p>
     </div>
    </div>
    <div style="padding-bottom: 100px;"></div>
   </div><!-- Downloads Screen -->
   <div class="screen" id="downloads">
    <div class="header">
     <div class="logo">
      Downloads
     </div>
     <div class="subtitle">
      Offline content
     </div>
    </div>
    <div class="glass-card">
     <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px;"><span>Storage Used</span> <span style="font-weight: 600;">2.4 GB / 5 GB</span>
     </div>
     <div class="progress-bar">
      <div class="progress-fill" style="width: 48%;"></div>
     </div>
    </div>
    <div class="filter-chips">
     <div class="chip active">
      All
     </div>
     <div class="chip">
      AudioBooks
     </div>
     <div class="chip">
      eBooks
     </div>
     <div class="chip">
      Videos
     </div>
    </div>
    <div class="content-card">
     <div class="content-thumbnail">
      💾
     </div>
     <div class="content-info">
      <h3>The Mysterious Tale</h3>
      <p>AudioBook • 156 MB • Downloaded</p>
     </div>
    </div>
    <div style="padding-bottom: 100px;"></div>
   </div><!-- Profile Screen -->
   <div class="screen" id="profile">
    <div class="header">
     <div class="logo">
      Profile
     </div>
     <div class="subtitle">
      Manage your account
     </div>
    </div>
    <div class="glass-card" style="text-align: center;">
     <div style="width: 80px; height: 80px; background: linear-gradient(135deg, #667eea, #764ba2); border-radius: 50%; margin: 0 auto 15px; display: flex; align-items: center; justify-content: center; color: white; font-size: 32px;">
      👤
     </div>
     <h3 style="margin: 0 0 5px 0;">John Doe</h3>
     <p style="color: #666; margin: 0;">john.doe@email.com</p>
    </div>
    <div class="content-card">
     <div class="content-thumbnail">
      ⚙️
     </div>
     <div class="content-info">
      <h3>Settings</h3>
      <p>App preferences and configuration</p>
     </div>
    </div>
    <div class="content-card">
     <div class="content-thumbnail">
      🌐
     </div>
     <div class="content-info">
      <h3>Language</h3>
      <p>Change app language</p>
     </div>
    </div>
    <div class="content-card">
     <div class="content-thumbnail">
      📊
     </div>
     <div class="content-info">
      <h3>Statistics</h3>
      <p>Your reading and listening stats</p>
     </div>
    </div>
    <div class="content-card" onclick="signOut()">
     <div class="content-thumbnail">
      🚪
     </div>
     <div class="content-info">
      <h3>Sign Out</h3>
      <p>Log out of your account</p>
     </div>
    </div>
    <div style="padding-bottom: 100px;"></div>
   </div><!-- Bottom Navigation -->
   <div class="bottom-nav">
    <div class="nav-item active" onclick="showScreen('home'); setActiveNav(this)">
     <div class="nav-icon">
      🏠
     </div>
     <div class="nav-label">
      Home
     </div>
    </div>
    <div class="nav-item" onclick="showScreen('search'); setActiveNav(this)">
     <div class="nav-icon">
      🔍
     </div>
     <div class="nav-label">
      Search
     </div>
    </div>
    <div class="nav-item" onclick="showScreen('categories'); setActiveNav(this)">
     <div class="nav-icon">
      📚
     </div>
     <div class="nav-label">
      Categories
     </div>
    </div>
    <div class="nav-item" onclick="showScreen('downloads'); setActiveNav(this)">
     <div class="nav-icon">
      💾
     </div>
     <div class="nav-label">
      Downloads
     </div>
    </div>
    <div class="nav-item" onclick="showScreen('profile'); setActiveNav(this)">
     <div class="nav-icon">
      👤
     </div>
     <div class="nav-label">
      Profile
     </div>
    </div>
   </div>
  </div>
  <div class="loading-spinner" id="loadingSpinner"></div>
  <div class="error-message" id="errorMessage"></div>
  <div class="success-message" id="successMessage"></div>
  <script>
        // Configuration object
        const defaultConfig = {
            app_title: "Suno Simodhya",
            welcome_message: "Welcome to Suno Simodhya",
            search_placeholder: "Search stories, books, videos...",
            primary_color: "#667eea",
            secondary_color: "#764ba2",
            background_color: "#f8f9fa",
            text_color: "#333333",
            surface_color: "#ffffff"
        };

        let currentRecordCount = 0;
        let userData = [];
        let currentUser = null;

        // Google Sign-In Configuration
        const GOOGLE_CLIENT_ID = "your-google-client-id.apps.googleusercontent.com";
        
        // Facebook Configuration  
        const FACEBOOK_APP_ID = "your-facebook-app-id";

        // Data handler for SDK
        const dataHandler = {
            onDataChanged(data) {
                userData = data;
                currentRecordCount = data.length;
                updateUIFromData(data);
            }
        };

        // Initialize SDKs
        async function initializeApp() {
            try {
                // Initialize Data SDK
                if (window.dataSdk) {
                    const initResult = await window.dataSdk.init(dataHandler);
                    if (!initResult.isOk) {
                        showError("Failed to initialize data storage");
                    }
                }

                // Initialize Element SDK
                if (window.elementSdk) {
                    await window.elementSdk.init({
                        defaultConfig,
                        onConfigChange: async (config) => {
                            updateUIFromConfig(config);
                        },
                        mapToCapabilities: (config) => ({
                            recolorables: [
                                {
                                    get: () => config.primary_color || defaultConfig.primary_color,
                                    set: (value) => {
                                        config.primary_color = value;
                                        window.elementSdk.setConfig({ primary_color: value });
                                    }
                                },
                                {
                                    get: () => config.secondary_color || defaultConfig.secondary_color,
                                    set: (value) => {
                                        config.secondary_color = value;
                                        window.elementSdk.setConfig({ secondary_color: value });
                                    }
                                },
                                {
                                    get: () => config.background_color || defaultConfig.background_color,
                                    set: (value) => {
                                        config.background_color = value;
                                        window.elementSdk.setConfig({ background_color: value });
                                    }
                                },
                                {
                                    get: () => config.text_color || defaultConfig.text_color,
                                    set: (value) => {
                                        config.text_color = value;
                                        window.elementSdk.setConfig({ text_color: value });
                                    }
                                },
                                {
                                    get: () => config.surface_color || defaultConfig.surface_color,
                                    set: (value) => {
                                        config.surface_color = value;
                                        window.elementSdk.setConfig({ surface_color: value });
                                    }
                                }
                            ],
                            borderables: [],
                            fontEditable: undefined,
                            fontSizeable: undefined
                        }),
                        mapToEditPanelValues: (config) => new Map([
                            ["app_title", config.app_title || defaultConfig.app_title],
                            ["welcome_message", config.welcome_message || defaultConfig.welcome_message],
                            ["search_placeholder", config.search_placeholder || defaultConfig.search_placeholder]
                        ])
                    });
                }
            } catch (error) {
                console.error("Failed to initialize app:", error);
                showError("Failed to initialize application");
            }
        }

        // Update UI from config
        function updateUIFromConfig(config) {
            const appTitle = config.app_title || defaultConfig.app_title;
            const welcomeMessage = config.welcome_message || defaultConfig.welcome_message;
            const searchPlaceholder = config.search_placeholder || defaultConfig.search_placeholder;
            const primaryColor = config.primary_color || defaultConfig.primary_color;
            const secondaryColor = config.secondary_color || defaultConfig.secondary_color;
            const backgroundColor = config.background_color || defaultConfig.background_color;
            const textColor = config.text_color || defaultConfig.text_color;
            const surfaceColor = config.surface_color || defaultConfig.surface_color;

            // Update text content
            const appTitleElements = document.querySelectorAll('#app-title, #home-title');
            appTitleElements.forEach(el => el.textContent = appTitle);
            
            const welcomeElement = document.getElementById('welcome-message');
            if (welcomeElement) welcomeElement.textContent = welcomeMessage;
            
            const searchElement = document.getElementById('search-placeholder');
            if (searchElement) searchElement.placeholder = searchPlaceholder;

            // Update colors
            document.documentElement.style.setProperty('--primary-color', primaryColor);
            document.documentElement.style.setProperty('--secondary-color', secondaryColor);
            document.body.style.background = `linear-gradient(135deg, ${primaryColor} 0%, ${secondaryColor} 100%)`;
            
            // Update button colors
            const primaryButtons = document.querySelectorAll('.btn-primary');
            primaryButtons.forEach(btn => {
                btn.style.background = `linear-gradient(135deg, ${primaryColor}, ${secondaryColor})`;
            });

            // Update glass cards
            const glassCards = document.querySelectorAll('.glass-card');
            glassCards.forEach(card => {
                card.style.background = `rgba(255, 255, 255, 0.8)`;
            });
        }

        // Update UI from data
        function updateUIFromData(data) {
            // Update UI based on user data if needed
            console.log("User data updated:", data);
        }

        // Screen navigation
        function showScreen(screenId) {
            const screens = document.querySelectorAll('.screen');
            screens.forEach(screen => screen.classList.remove('active'));
            
            const targetScreen = document.getElementById(screenId);
            if (targetScreen) {
                targetScreen.classList.add('active');
            }
        }

        // Navigation helper
        function setActiveNav(element) {
            const navItems = document.querySelectorAll('.nav-item');
            navItems.forEach(item => item.classList.remove('active'));
            element.classList.add('active');
        }

        // Language change handler
        async function changeLanguage(language) {
            if (currentRecordCount >= 999) {
                showError("Maximum limit of 999 records reached. Cannot save language preference.");
                return;
            }

            showLoading();
            
            try {
                if (window.dataSdk) {
                    const result = await window.dataSdk.create({
                        user_id: "current_user",
                        selected_language: language,
                        timestamp: new Date().toISOString()
                    });

                    if (result.isOk) {
                        showSuccess("Language preference saved!");
                    } else {
                        showError("Failed to save language preference");
                    }
                }
            } catch (error) {
                showError("Error saving language preference");
            } finally {
                hideLoading();
            }
        }

        // Utility functions
        function showLoading() {
            document.getElementById('loadingSpinner').style.display = 'block';
        }

        function hideLoading() {
            document.getElementById('loadingSpinner').style.display = 'none';
        }

        function showError(message) {
            const errorEl = document.getElementById('errorMessage');
            errorEl.textContent = message;
            errorEl.style.display = 'block';
            setTimeout(() => errorEl.style.display = 'none', 3000);
        }

        function showSuccess(message) {
            const successEl = document.getElementById('successMessage');
            successEl.textContent = message;
            successEl.style.display = 'block';
            setTimeout(() => successEl.style.display = 'none', 3000);
        }

        // Social Authentication Functions
        
        // Initialize Google Sign-In
        function initializeGoogleSignIn() {
            if (typeof google !== 'undefined' && google.accounts) {
                google.accounts.id.initialize({
                    client_id: GOOGLE_CLIENT_ID,
                    callback: handleGoogleSignIn,
                    auto_select: false,
                    cancel_on_tap_outside: true
                });
            }
        }

        // Initialize Facebook SDK
        function initializeFacebookSDK() {
            if (typeof FB !== 'undefined') {
                FB.init({
                    appId: FACEBOOK_APP_ID,
                    cookie: true,
                    xfbml: true,
                    version: 'v18.0'
                });
            }
        }

        // Google Sign-In Handler
        async function signInWithGoogle() {
            try {
                showLoading();
                
                if (typeof google === 'undefined' || !google.accounts) {
                    showError("Google Sign-In is not available. Please try again later.");
                    return;
                }

                // For demo purposes, simulate successful Google sign-in
                const mockGoogleUser = {
                    id: "google_" + Date.now(),
                    name: "Google User",
                    email: "user@gmail.com",
                    picture: "https://via.placeholder.com/80",
                    provider: "google"
                };

                await handleSuccessfulAuth(mockGoogleUser);
                
            } catch (error) {
                console.error('Google Sign-In Error:', error);
                showError("Google sign-in failed. Please try again.");
            } finally {
                hideLoading();
            }
        }

        // Handle Google Sign-In Response
        async function handleGoogleSignIn(response) {
            try {
                showLoading();
                
                // Decode the JWT token (in a real app, verify this server-side)
                const payload = JSON.parse(atob(response.credential.split('.')[1]));
                
                const googleUser = {
                    id: "google_" + payload.sub,
                    name: payload.name,
                    email: payload.email,
                    picture: payload.picture,
                    provider: "google"
                };

                await handleSuccessfulAuth(googleUser);
                
            } catch (error) {
                console.error('Google Sign-In Error:', error);
                showError("Google sign-in failed. Please try again.");
            } finally {
                hideLoading();
            }
        }

        // Facebook Sign-In Handler
        async function signInWithFacebook() {
            try {
                showLoading();
                
                if (typeof FB === 'undefined') {
                    showError("Facebook Sign-In is not available. Please try again later.");
                    return;
                }

                // For demo purposes, simulate successful Facebook sign-in
                const mockFacebookUser = {
                    id: "facebook_" + Date.now(),
                    name: "Facebook User",
                    email: "user@facebook.com",
                    picture: "https://via.placeholder.com/80",
                    provider: "facebook"
                };

                await handleSuccessfulAuth(mockFacebookUser);
                
            } catch (error) {
                console.error('Facebook Sign-In Error:', error);
                showError("Facebook sign-in failed. Please try again.");
            } finally {
                hideLoading();
            }
        }

        // Handle Facebook Login Response
        function handleFacebookLogin(response) {
            if (response.authResponse) {
                FB.api('/me', { fields: 'name,email,picture' }, async function(userInfo) {
                    try {
                        const facebookUser = {
                            id: "facebook_" + userInfo.id,
                            name: userInfo.name,
                            email: userInfo.email || "No email provided",
                            picture: userInfo.picture?.data?.url || "https://via.placeholder.com/80",
                            provider: "facebook"
                        };

                        await handleSuccessfulAuth(facebookUser);
                    } catch (error) {
                        console.error('Facebook User Info Error:', error);
                        showError("Failed to get Facebook user information.");
                    }
                });
            } else {
                showError("Facebook login was cancelled or failed.");
            }
        }

        // Handle Successful Authentication
        async function handleSuccessfulAuth(user) {
            try {
                currentUser = user;
                
                // Save user data to Canva Sheet
                if (window.dataSdk && currentRecordCount < 999) {
                    const result = await window.dataSdk.create({
                        user_id: user.id,
                        name: user.name,
                        email: user.email,
                        provider: user.provider,
                        login_timestamp: new Date().toISOString(),
                        session_active: "true"
                    });

                    if (result.isOk) {
                        showSuccess(`Welcome ${user.name}! Signed in with ${user.provider}.`);
                        updateProfileUI(user);
                        showScreen('home');
                    } else {
                        showError("Failed to save user session.");
                    }
                } else if (currentRecordCount >= 999) {
                    showError("Maximum user limit reached. Please contact support.");
                } else {
                    // Fallback for when Data SDK is not available
                    showSuccess(`Welcome ${user.name}! Signed in with ${user.provider}.`);
                    updateProfileUI(user);
                    showScreen('home');
                }
                
            } catch (error) {
                console.error('Authentication Error:', error);
                showError("Authentication failed. Please try again.");
            }
        }

        // Update Profile UI with user data
        function updateProfileUI(user) {
            // Update profile screen with user information
            const profileScreen = document.getElementById('profile');
            if (profileScreen) {
                const userAvatar = profileScreen.querySelector('.glass-card div[style*="border-radius: 50%"]');
                const userName = profileScreen.querySelector('h3');
                const userEmail = profileScreen.querySelector('p[style*="color: #666"]');
                
                if (userAvatar && user.picture) {
                    userAvatar.style.backgroundImage = `url(${user.picture})`;
                    userAvatar.style.backgroundSize = 'cover';
                    userAvatar.style.backgroundPosition = 'center';
                    userAvatar.textContent = '';
                }
                
                if (userName) userName.textContent = user.name;
                if (userEmail) userEmail.textContent = user.email;
            }
        }

        // Sign Out Function
        async function signOut() {
            try {
                showLoading();
                
                if (currentUser && window.dataSdk) {
                    // Update session status
                    const result = await window.dataSdk.create({
                        user_id: currentUser.id,
                        session_active: "false",
                        logout_timestamp: new Date().toISOString()
                    });
                }
                
                currentUser = null;
                showSuccess("Signed out successfully!");
                showScreen('login');
                
            } catch (error) {
                console.error('Sign Out Error:', error);
                showError("Sign out failed. Please try again.");
            } finally {
                hideLoading();
            }
        }

        // Initialize app when DOM is loaded
        document.addEventListener('DOMContentLoaded', function() {
            initializeApp();
            
            // Initialize social sign-in after a short delay to ensure SDKs are loaded
            setTimeout(() => {
                initializeGoogleSignIn();
                initializeFacebookSDK();
            }, 1000);
        });

        // Add click handlers for interactive elements
        document.addEventListener('click', function(e) {
            // Handle chip selection
            if (e.target.classList.contains('chip')) {
                const chips = e.target.parentElement.querySelectorAll('.chip');
                chips.forEach(chip => chip.classList.remove('active'));
                e.target.classList.add('active');
            }

            // Handle player controls
            if (e.target.classList.contains('control-btn')) {
                e.target.style.transform = 'scale(0.95)';
                setTimeout(() => e.target.style.transform = 'scale(1)', 150);
            }
        });

        // Add form submission handlers
        document.addEventListener('submit', function(e) {
            e.preventDefault();
            showSuccess("Form submitted successfully!");
        });
    </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'99e55792579985de',t:'MTc2MzExMTA3NC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>