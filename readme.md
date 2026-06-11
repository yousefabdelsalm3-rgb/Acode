<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fly for Change | ط¹ط§ظ„ظ…ظƒ ظٹط¨ط¯ط£ ظ…ظ† ظ‡ظ†ط§</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;800&family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --bg-primary: #FFFFFF;
            --bg-secondary: #F0F9FF;
            --sky-blue: #87CEEB;
            --deep-blue: #1E3A8A;
            --gold: #D4AF37;
            --text-dark: #0F172A;
            --text-light: #64748B;
            --card-bg: #FFFFFF;
            --shadow: rgba(30, 58, 138, 0.1);
            --gradient-start: #87CEEB;
            --gradient-end: #1E3A8A;
        }
        [data-theme="dark"] {
            --bg-primary: #0F172A;
            --bg-secondary: #1E293B;
            --sky-blue: #0E4A6B;
            --deep-blue: #60A5FA;
            --gold: #D4AF37;
            --text-dark: #F8FAFC;
            --text-light: #94A3B8;
            --card-bg: #1E293B;
            --shadow: rgba(0, 0, 0, 0.3);
            --gradient-start: #0E4A6B;
            --gradient-end: #1E3A8A;
        }
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Cairo', 'Poppins', sans-serif;
            background: var(--bg-primary);
            color: var(--text-dark);
            transition: all 0.3s ease;
            overflow-x: hidden;
        }

        /* ====== ADMIN BUTTONS ====== */
        .admin-btn {
            position: fixed;
            bottom: 30px;
            left: 30px;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: var(--gold);
            color: white;
            border: none;
            font-size: 28px;
            cursor: pointer;
            box-shadow: 0 6px 20px rgba(212, 175, 55, 0.4);
            z-index: 999;
            transition: all 0.3s ease;
            display: none;
            align-items: center;
            justify-content: center;
        }
        .admin-btn:hover {
            transform: scale(1.1) rotate(90deg);
            box-shadow: 0 8px 25px rgba(212, 175, 55, 0.6);
        }
        .admin-btn.show { display: flex; }
        #adminEditBtn.show { display: flex; }

        .admin-login-btn {
            position: fixed;
            bottom: 30px;
            left: 30px;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: rgba(30, 58, 138, 0.3);
            color: white;
            border: 2px solid rgba(255,255,255,0.3);
            font-size: 18px;
            cursor: pointer;
            z-index: 998;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(10px);
        }
        .admin-login-btn:hover {
            background: var(--gold);
            border-color: var(--gold);
        }

        /* ====== MODALS ====== */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0,0,0,0.6);
            backdrop-filter: blur(5px);
            z-index: 2000;
            display: none;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        .modal-overlay.active { display: flex; }
        .modal-box {
            background: var(--card-bg);
            border-radius: 24px;
            padding: 35px;
            width: 100%;
            max-width: 550px;
            max-height: 90vh;
            overflow-y: auto;
            position: relative;
            box-shadow: 0 25px 50px rgba(0,0,0,0.3);
            animation: modalSlide 0.4s ease;
        }
        @keyframes modalSlide {
            from { opacity: 0; transform: translateY(30px) scale(0.95); }
            to { opacity: 1; transform: translateY(0) scale(1); }
        }
        .modal-close {
            position: absolute;
            top: 15px; left: 15px;
            width: 36px; height: 36px;
            border-radius: 50%;
            background: rgba(30, 58, 138, 0.1);
            border: none;
            color: var(--text-dark);
            font-size: 18px;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .modal-close:hover { background: #ef4444; color: white; }
        .modal-title {
            font-size: 1.5rem;
            font-weight: 800;
            color: var(--deep-blue);
            margin-bottom: 25px;
            text-align: center;
        }
        .form-group { margin-bottom: 18px; }
        .form-label {
            display: block;
            font-weight: 700;
            color: var(--text-dark);
            margin-bottom: 8px;
            font-size: 0.95rem;
        }
        .form-input, .form-select, .form-textarea {
            width: 100%;
            padding: 14px 18px;
            border: 2px solid #e2e8f0;
            border-radius: 14px;
            font-family: 'Cairo', sans-serif;
            font-size: 15px;
            background: var(--bg-primary);
            color: var(--text-dark);
            transition: all 0.3s;
            outline: none;
        }
        .form-input:focus, .form-select:focus, .form-textarea:focus {
            border-color: var(--gold);
            box-shadow: 0 0 0 4px rgba(212, 175, 55, 0.15);
        }
        .form-textarea { min-height: 100px; resize: vertical; }

        /* Image Upload */
        .image-upload-area {
            border: 3px dashed #cbd5e1;
            border-radius: 16px;
            padding: 30px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            background: var(--bg-primary);
            position: relative;
            overflow: hidden;
        }
        .image-upload-area:hover {
            border-color: var(--gold);
            background: rgba(212, 175, 55, 0.05);
        }
        .image-upload-area.has-image {
            border-style: solid;
            border-color: var(--gold);
            padding: 0;
        }
        .image-upload-area i {
            font-size: 40px;
            color: var(--text-light);
            margin-bottom: 10px;
        }
        .image-upload-area p {
            color: var(--text-light);
            font-size: 0.9rem;
        }
        .image-upload-area input[type="file"] {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            opacity: 0;
            cursor: pointer;
        }
        .preview-image {
            width: 100%;
            height: 200px;
            object-fit: cover;
            border-radius: 13px;
            display: none;
        }
        .preview-image.show { display: block; }
        .upload-placeholder { display: block; }
        .upload-placeholder.hide { display: none; }

        .submit-btn {
            width: 100%;
            padding: 16px;
            background: linear-gradient(135deg, var(--gold), #B8941F);
            color: white;
            border: none;
            border-radius: 14px;
            font-family: 'Cairo', sans-serif;
            font-size: 1.1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            margin-top: 10px;
        }
        .submit-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(212, 175, 55, 0.4);
        }
        .submit-btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }
        .pin-inputs {
            display: flex;
            gap: 12px;
            justify-content: center;
            margin: 25px 0;
        }
        .pin-inputs input {
            width: 55px;
            height: 65px;
            text-align: center;
            font-size: 1.8rem;
            font-weight: 800;
            border: 2px solid #e2e8f0;
            border-radius: 14px;
            background: var(--bg-primary);
            color: var(--text-dark);
            outline: none;
            transition: all 0.3s;
        }
        .pin-inputs input:focus {
            border-color: var(--gold);
            box-shadow: 0 0 0 4px rgba(212, 175, 55, 0.15);
        }
        .pin-error {
            color: #ef4444;
            text-align: center;
            font-size: 0.9rem;
            margin-top: 10px;
            display: none;
        }
        .pin-error.show { display: block; }
        .success-msg { text-align: center; padding: 20px; }
        .success-msg i {
            font-size: 60px;
            color: #22c55e;
            margin-bottom: 15px;
        }
        .success-msg h3 {
            font-size: 1.3rem;
            color: var(--text-dark);
            margin-bottom: 10px;
        }
        .success-msg p { color: var(--text-light); }

        /* ====== ADDED OPPORTUNITIES SECTION ====== */
        .added-section {
            padding: 60px 20px;
            background: var(--bg-secondary);
            display: none;
        }
        .added-section.has-items { display: block; }
        .added-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
            max-width: 1200px;
            margin: 0 auto;
        }
        .added-card {
            background: var(--card-bg);
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 10px 30px var(--shadow);
            transition: all 0.3s;
            position: relative;
        }
        .added-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 40px var(--shadow);
        }
        .added-card-image {
            width: 100%;
            height: 220px;
            object-fit: cover;
            background: linear-gradient(135deg, var(--sky-blue), var(--deep-blue));
        }
        .added-card-content { padding: 25px; }
        .added-card-badge {
            display: inline-block;
            background: var(--gold);
            color: white;
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
            margin-bottom: 10px;
        }
        .added-card-title {
            font-size: 1.2rem;
            font-weight: 700;
            color: var(--text-dark);
            margin-bottom: 10px;
        }
        .added-card-desc {
            color: var(--text-light);
            font-size: 0.95rem;
            margin-bottom: 15px;
            line-height: 1.6;
        }
        .added-card-meta {
            display: flex;
            gap: 15px;
            color: var(--text-light);
            font-size: 0.85rem;
            flex-wrap: wrap;
        }
        .added-card-meta i {
            color: var(--deep-blue);
            margin-left: 5px;
        }
        .delete-card-btn {
            position: absolute;
            top: 10px; left: 10px;
            width: 32px; height: 32px;
            border-radius: 50%;
            background: rgba(239, 68, 68, 0.9);
            color: white;
            border: none;
            cursor: pointer;
            font-size: 14px;
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 10;
        }
        .added-card:hover .delete-card-btn { display: flex; }
        .delete-card-btn:hover { background: #dc2626; }

        /* ====== HERO ====== */
        .hero-section {
            position: relative;
            min-height: 100vh;
            background: linear-gradient(135deg, var(--gradient-start) 0%, var(--gradient-end) 100%);
            overflow: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        .cloud {
            position: absolute;
            background: rgba(255, 255, 255, 0.8);
            border-radius: 100px;
            opacity: 0.6;
            animation: float linear infinite;
        }
        .cloud::before {
            content: '';
            position: absolute;
            background: rgba(255, 255, 255, 0.8);
            border-radius: 100px;
        }
        .cloud1 { width: 100px; height: 40px; top: 20%; left: -100px; animation-duration: 25s; }
        .cloud1::before { width: 50px; height: 50px; top: -25px; left: 10px; }
        .cloud2 { width: 80px; height: 35px; top: 40%; left: -80px; animation-duration: 30s; animation-delay: 5s; }
        .cloud2::before { width: 60px; height: 40px; top: -20px; right: 15px; }
        .cloud3 { width: 120px; height: 45px; top: 60%; left: -120px; animation-duration: 35s; animation-delay: 10s; }
        .cloud3::before { width: 70px; height: 55px; top: -30px; left: 20px; }
        .cloud4 { width: 90px; height: 38px; top: 15%; left: -90px; animation-duration: 28s; animation-delay: 15s; }
        .cloud5 { width: 110px; height: 42px; top: 75%; left: -110px; animation-duration: 32s; animation-delay: 8s; }
        @keyframes float {
            from { transform: translateX(0); }
            to { transform: translateX(calc(100vw + 200px)); }
        }
        .plane-container {
            position: absolute;
            top: 25%; right: -200px;
            animation: flyPlane 20s linear infinite;
            z-index: 2;
        }
        .plane {
            font-size: 80px;
            color: white;
            filter: drop-shadow(0 4px 8px rgba(0,0,0,0.2));
            transform: scaleX(-1);
        }
        @keyframes flyPlane {
            from { transform: translateX(0); }
            to { transform: translateX(calc(-100vw - 300px)); }
        }
        .logo-section {
            text-align: center;
            z-index: 10;
            padding: 20px;
            margin-top: -50px;
        }
        .logo-icon {
            font-size: 100px;
            color: var(--gold);
            margin-bottom: 20px;
            animation: pulse 2s ease-in-out infinite;
            text-shadow: 0 0 30px rgba(212, 175, 55, 0.5);
        }
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }
        .site-title {
            font-size: clamp(2.5rem, 8vw, 5rem);
            font-weight: 800;
            color: white;
            text-shadow: 2px 2px 10px rgba(0,0,0,0.3);
            margin-bottom: 10px;
            letter-spacing: 2px;
        }
        .site-subtitle {
            font-size: clamp(1rem, 3vw, 1.5rem);
            color: rgba(255,255,255,0.9);
            font-weight: 300;
            margin-bottom: 30px;
        }
        .search-container {
            width: 90%;
            max-width: 700px;
            margin: 0 auto 40px;
            position: relative;
            z-index: 10;
        }
        .search-box {
            display: flex;
            background: white;
            border-radius: 50px;
            overflow: hidden;
            box-shadow: 0 10px 40px rgba(0,0,0,0.2);
            transition: transform 0.3s;
        }
        .search-box:focus-within { transform: scale(1.02); }
        .search-input {
            flex: 1;
            border: none;
            padding: 18px 25px;
            font-size: 16px;
            font-family: 'Cairo', sans-serif;
            outline: none;
            background: transparent;
        }
        .search-btn {
            background: var(--gold);
            border: none;
            padding: 18px 30px;
            color: white;
            font-size: 18px;
            cursor: pointer;
            transition: background 0.3s;
        }
        .search-btn:hover { background: #B8941F; }

        .lang-switcher {
            position: fixed;
            top: 20px; left: 20px;
            z-index: 1000;
            display: flex;
            gap: 8px;
            flex-wrap: wrap;
            max-width: 200px;
        }
        .lang-btn {
            background: rgba(255,255,255,0.2);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255,255,255,0.3);
            color: white;
            padding: 8px 14px;
            border-radius: 20px;
            cursor: pointer;
            font-size: 12px;
            font-weight: 600;
            transition: all 0.3s;
            font-family: 'Cairo', sans-serif;
        }
        .lang-btn:hover, .lang-btn.active {
            background: var(--gold);
            border-color: var(--gold);
            transform: translateY(-2px);
        }
        .theme-toggle {
            position: fixed;
            top: 20px; right: 20px;
            z-index: 1000;
            background: rgba(255,255,255,0.2);
            backdrop-filter: blur(10px);
            border: 2px solid rgba(255,255,255,0.3);
            color: white;
            width: 50px; height: 50px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 20px;
            transition: all 0.3s;
        }
        .theme-toggle:hover {
            background: var(--gold);
            transform: rotate(180deg);
        }
        .stats-bar {
            display: flex;
            justify-content: center;
            gap: 40px;
            padding: 30px;
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            margin: 20px auto;
            max-width: 800px;
            z-index: 10;
            position: relative;
            flex-wrap: wrap;
        }
        .stat-item { text-align: center; color: white; }
        .stat-number { font-size: 2rem; font-weight: 800; color: var(--gold); }
        .stat-label { font-size: 0.9rem; opacity: 0.9; }

        .content-section { padding: 60px 20px; background: var(--bg-primary); }
        .section-title {
            text-align: center;
            font-size: clamp(1.8rem, 5vw, 2.5rem);
            color: var(--deep-blue);
            margin-bottom: 15px;
            font-weight: 700;
        }
        .section-desc {
            text-align: center;
            color: var(--text-light);
            margin-bottom: 50px;
            font-size: 1.1rem;
        }
        .categories-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 25px;
            max-width: 1200px;
            margin: 0 auto 60px;
        }
        .category-card {
            background: var(--card-bg);
            border-radius: 20px;
            padding: 30px;
            text-align: center;
            box-shadow: 0 10px 30px var(--shadow);
            transition: all 0.3s;
            cursor: pointer;
            border: 2px solid transparent;
        }
        .category-card:hover {
            transform: translateY(-10px);
            border-color: var(--gold);
            box-shadow: 0 20px 40px var(--shadow);
        }
        .category-icon { font-size: 50px; margin-bottom: 15px; color: var(--deep-blue); }
        .category-title { font-size: 1.3rem; font-weight: 700; color: var(--text-dark); margin-bottom: 10px; }
        .category-count { color: var(--gold); font-weight: 600; font-size: 0.95rem; }

        .programs-section { background: var(--bg-secondary); padding: 60px 20px; }
        .programs-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
            max-width: 1200px;
            margin: 0 auto;
        }
        .program-card {
            background: var(--card-bg);
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 10px 30px var(--shadow);
            transition: all 0.3s;
        }
        .program-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 40px var(--shadow);
        }
        .program-image {
            height: 200px;
            background: linear-gradient(135deg, var(--sky-blue), var(--deep-blue));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 60px;
            color: white;
        }
        .program-content { padding: 25px; }
        .program-badge {
            display: inline-block;
            background: var(--gold);
            color: white;
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
            margin-bottom: 10px;
        }
        .program-title { font-size: 1.2rem; font-weight: 700; color: var(--text-dark); margin-bottom: 10px; }
        .program-desc { color: var(--text-light); font-size: 0.95rem; margin-bottom: 15px; }
        .program-meta {
            display: flex;
            gap: 15px;
            color: var(--text-light);
            font-size: 0.85rem;
        }
        .program-meta i { color: var(--deep-blue); }

        .specialties-section { padding: 60px 20px; background: var(--bg-primary); }
        .specialties-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            max-width: 1000px;
            margin: 0 auto;
        }
        .specialty-item {
            background: var(--card-bg);
            border-radius: 15px;
            padding: 25px;
            text-align: center;
            box-shadow: 0 5px 20px var(--shadow);
            transition: all 0.3s;
            cursor: pointer;
            border-left: 4px solid var(--deep-blue);
        }
        .specialty-item:hover {
            transform: scale(1.05);
            border-left-color: var(--gold);
        }
        .specialty-icon { font-size: 40px; margin-bottom: 10px; }
        .specialty-name { font-weight: 700; color: var(--text-dark); }

        .footer {
            background: var(--deep-blue);
            color: white;
            padding: 50px 20px 20px;
            text-align: center;
        }
        .footer-logo { font-size: 40px; color: var(--gold); margin-bottom: 15px; }
        .footer-title { font-size: 1.5rem; font-weight: 700; margin-bottom: 10px; }
        .footer-links {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin: 30px 0;
            flex-wrap: wrap;
        }
        .footer-links a {
            color: rgba(255,255,255,0.8);
            text-decoration: none;
            transition: color 0.3s;
        }
        .footer-links a:hover { color: var(--gold); }
        .social-links {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 20px 0;
        }
        .social-links a {
            width: 45px; height: 45px;
            background: rgba(255,255,255,0.1);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 20px;
            transition: all 0.3s;
        }
        .social-links a:hover { background: var(--gold); transform: translateY(-3px); }
        .copyright {
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px solid rgba(255,255,255,0.1);
            color: rgba(255,255,255,0.6);
            font-size: 0.9rem;
        }
        .fade-in {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.6s ease;
        }
        .fade-in.visible { opacity: 1; transform: translateY(0); }
        .loading {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: linear-gradient(135deg, var(--sky-blue), var(--deep-blue));
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 9999;
            transition: opacity 0.5s;
        }
        .loading.hidden { opacity: 0; pointer-events: none; }
        .loading-spinner {
            width: 60px; height: 60px;
            border: 5px solid rgba(255,255,255,0.3);
            border-top-color: var(--gold);
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }
        @keyframes spin { to { transform: rotate(360deg); } }

        @media (max-width: 768px) {
            .stats-bar { gap: 20px; padding: 20px; }
            .stat-number { font-size: 1.5rem; }
            .lang-switcher { top: 10px; left: 10px; max-width: 150px; }
            .lang-btn { padding: 6px 10px; font-size: 10px; }
            .theme-toggle { top: 10px; right: 10px; width: 40px; height: 40px; font-size: 16px; }
            .plane { font-size: 50px; }
            .admin-btn, .admin-login-btn { bottom: 20px; left: 20px; }
            .modal-box { padding: 25px 20px; }
            .pin-inputs input { width: 45px; height: 55px; font-size: 1.5rem; }
        }
    
        /* ====== EDIT/DASHBOARD MODAL ====== */
        .edit-modal-box {
            max-width: 900px !important;
            width: 95%;
        }
        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        .dashboard-card {
            background: var(--bg-secondary);
            border-radius: 16px;
            padding: 25px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            border: 2px solid transparent;
        }
        .dashboard-card:hover {
            border-color: var(--gold);
            transform: translateY(-5px);
            box-shadow: 0 10px 30px var(--shadow);
        }
        .dashboard-card i {
            font-size: 40px;
            color: var(--deep-blue);
            margin-bottom: 15px;
        }
        .dashboard-card h3 {
            font-size: 1.1rem;
            color: var(--text-dark);
            margin-bottom: 8px;
        }
        .dashboard-card p {
            font-size: 0.85rem;
            color: var(--text-light);
        }
        .edit-section {
            display: none;
            margin-top: 20px;
            padding: 20px;
            background: var(--bg-secondary);
            border-radius: 16px;
        }
        .edit-section.active { display: block; }
        .edit-section-title {
            font-size: 1.2rem;
            font-weight: 700;
            color: var(--deep-blue);
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .edit-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 12px;
            background: var(--card-bg);
            border-radius: 12px;
            margin-bottom: 10px;
            flex-wrap: wrap;
            gap: 10px;
        }
        .edit-item-label {
            font-weight: 600;
            color: var(--text-dark);
        }
        .edit-item-input {
            flex: 1;
            min-width: 200px;
            padding: 10px 14px;
            border: 2px solid #e2e8f0;
            border-radius: 10px;
            font-family: 'Cairo', sans-serif;
            background: var(--bg-primary);
            color: var(--text-dark);
            outline: none;
        }
        .edit-item-input:focus {
            border-color: var(--gold);
        }
        .edit-save-btn {
            background: linear-gradient(135deg, var(--gold), #B8941F);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 12px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            margin-top: 15px;
        }
        .edit-save-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(212, 175, 55, 0.4);
        }
        .back-btn {
            background: var(--text-light);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 10px;
            cursor: pointer;
            margin-bottom: 15px;
            transition: all 0.3s;
        }
        .back-btn:hover { background: var(--deep-blue); }
        .color-picker-wrapper {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .color-picker-wrapper input[type="color"] {
            width: 50px;
            height: 40px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
        }
        .stats-editor {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
        }
        @media (max-width: 768px) {
            .dashboard-grid { grid-template-columns: 1fr; }
            .stats-editor { grid-template-columns: 1fr; }
            .edit-item { flex-direction: column; align-items: stretch; }
            .edit-item-input { min-width: 100%; }
        }

    </style>
</head>
<body>
    <!-- Loading Screen -->
    <div class="loading" id="loading">
        <div class="loading-spinner"></div>
    </div>

    <!-- Admin Login Button -->
    <button class="admin-login-btn" id="adminLoginBtn" onclick="openPinModal()" title="Admin Login">
        <i class="fas fa-lock"></i>
    </button>

    <!-- Admin Add Button (hidden until PIN correct) -->
    <button class="admin-btn" id="adminAddBtn" onclick="openAddModal()" title="ط¥ط¶ط§ظپط© ظپط±طµط© ط¬ط¯ظٹط¯ط©">
        <i class="fas fa-plus"></i>
    </button>
    <!-- Admin Edit/Dashboard Button (hidden until PIN correct) -->
    <button class="admin-btn" id="adminEditBtn" onclick="openEditModal()" title="ظ„ظˆط­ط© ط§ظ„طھط­ظƒظ… - طھط¹ط¯ظٹظ„ ط§ظ„ظ…ظˆظ‚ط¹" style="bottom: 100px; background: linear-gradient(135deg, #1E3A8A, #0E4A6B);">
        <i class="fas fa-cog"></i>
    </button>

    <!-- PIN MODAL -->
    <div class="modal-overlay" id="pinModal">
        <div class="modal-box">
            <button class="modal-close" onclick="closePinModal()"><i class="fas fa-times"></i></button>
            <h2 class="modal-title">ًں”گ طھط³ط¬ظٹظ„ ط¯ط®ظˆظ„ ط§ظ„ظ…ط´ط±ظپ</h2>
            <p style="text-align:center; color: var(--text-light); margin-bottom: 20px;">ط£ط¯ط®ظ„ ط±ظ…ط² PIN ط§ظ„ظ…ظƒظˆظ† ظ…ظ† 4 ط£ط±ظ‚ط§ظ…</p>
            <div class="pin-inputs" id="pinInputs">
                <input type="password" maxlength="1" data-index="0" oninput="handlePinInput(this, 0)" onkeydown="handlePinKeydown(event, 0)">
                <input type="password" maxlength="1" data-index="1" oninput="handlePinInput(this, 1)" onkeydown="handlePinKeydown(event, 1)">
                <input type="password" maxlength="1" data-index="2" oninput="handlePinInput(this, 2)" onkeydown="handlePinKeydown(event, 2)">
                <input type="password" maxlength="1" data-index="3" oninput="handlePinInput(this, 3)" onkeydown="handlePinKeydown(event, 3)">
            </div>
            <p class="pin-error" id="pinError">ط±ظ…ط² PIN ط؛ظٹط± طµط­ظٹط­. ط­ط§ظˆظ„ ظ…ط±ط© ط£ط®ط±ظ‰.</p>
            <button class="submit-btn" onclick="verifyPin()">طھط£ظƒظٹط¯</button>
        </div>
    </div>

    <!-- ADD OPPORTUNITY MODAL -->
    <div class="modal-overlay" id="addModal">
        <div class="modal-box">
            <button class="modal-close" onclick="closeAddModal()"><i class="fas fa-times"></i></button>
            <h2 class="modal-title">âœ¨ ط¥ط¶ط§ظپط© ظپط±طµط© ط¬ط¯ظٹط¯ط©</h2>
            <form id="addForm" onsubmit="submitOpportunity(event)">
                <div class="form-group">
                    <label class="form-label">ًں“· طµظˆط±ط© ط§ظ„ظپط±طµط©</label>
                    <div class="image-upload-area" id="imageUploadArea" onclick="document.getElementById('imageInput').click()">
                        <div class="upload-placeholder" id="uploadPlaceholder">
                            <i class="fas fa-cloud-upload-alt"></i>
                            <p>ط§ط¶ط؛ط· ظ‡ظ†ط§ ط£ظˆ ط§ط³ط­ط¨ طµظˆط±ط© ظ„ط±ظپط¹ظ‡ط§</p>
                            <p style="font-size: 0.8rem; margin-top: 5px;">(JPEG, PNG, WebP - max 5MB)</p>
                        </div>
                        <img class="preview-image" id="previewImage" alt="Preview">
                        <input type="file" id="imageInput" accept="image/*" onchange="handleImageUpload(event)">
                    </div>
                </div>
                <div class="form-group">
                    <label class="form-label">ًں“Œ ظ†ظˆط¹ ط§ظ„ظپط±طµط©</label>
                    <select class="form-select" id="oppType" required>
                        <option value="">ط§ط®طھط± ط§ظ„ظ†ظˆط¹...</option>
                        <option value="scholarship">ظ…ظ†ط­ط© ط¯ط±ط§ط³ظٹط©</option>
                        <option value="conference">ظ…ط¤طھظ…ط±</option>
                        <option value="volunteer">طھط·ظˆط¹</option>
                        <option value="job">ظˆط¸ظٹظپط© ط¯ظˆظ„ظٹط©</option>
                        <option value="internship">طھط¯ط±ظٹط¨ ط¹ظ…ظ„ظٹ</option>
                        <option value="exchange">طھط¨ط§ط¯ظ„ ط«ظ‚ط§ظپظٹ</option>
                    </select>
                </div>
                <div class="form-group">
                    <label class="form-label">ًںڈ·ï¸ڈ ط¹ظ†ظˆط§ظ† ط§ظ„ظپط±طµط©</label>
                    <input type="text" class="form-input" id="oppTitle" placeholder="ظ…ط«ط§ظ„: ظ…ظ†ط­ط© ط¬ط§ظ…ط¹ط© ظ‡ط§ط±ظپط§ط±ط¯ 2026" required>
                </div>
                <div class="form-group">
                    <label class="form-label">ًں“‌ ظˆطµظپ ط§ظ„ظپط±طµط©</label>
                    <textarea class="form-textarea" id="oppDesc" placeholder="ط§ظƒطھط¨ ظˆطµظپط§ظ‹ طھظپطµظٹظ„ظٹط§ظ‹ ط¹ظ† ط§ظ„ظپط±طµط©..." required></textarea>
                </div>
                <div class="form-group">
                    <label class="form-label">ًںژ“ ط§ظ„طھط®طµطµ / ط§ظ„ظ…ط¬ط§ظ„</label>
                    <input type="text" class="form-input" id="oppField" placeholder="ظ…ط«ط§ظ„: ط§ظ„ط·ط¨طŒ ط§ظ„ظ‡ظ†ط¯ط³ط©طŒ طھظƒظ†ظˆظ„ظˆط¬ظٹط§ ط§ظ„ظ…ط¹ظ„ظˆظ…ط§طھ..." required>
                </div>
                <div class="form-group">
                    <label class="form-label">ًںŒچ ط§ظ„ط¯ظˆظ„ط©</label>
                    <input type="text" class="form-input" id="oppCountry" placeholder="ظ…ط«ط§ظ„: ط§ظ„ظˆظ„ط§ظٹط§طھ ط§ظ„ظ…طھط­ط¯ط©طŒ ط¨ط±ظٹط·ط§ظ†ظٹط§طŒ ط£ظ„ظ…ط§ظ†ظٹط§..." required>
                </div>
                <div class="form-group">
                    <label class="form-label">ًں“… ط¢ط®ط± ظ…ظˆط¹ط¯ ظ„ظ„طھظ‚ط¯ظٹظ…</label>
                    <input type="date" class="form-input" id="oppDeadline" required>
                </div>
                <div class="form-group">
                    <label class="form-label">ًں”— ط±ط§ط¨ط· ط§ظ„طھظ‚ط¯ظٹظ… (ط§ط®طھظٹط§ط±ظٹ)</label>
                    <input type="url" class="form-input" id="oppLink" placeholder="https://example.com/apply">
                </div>
                <button type="submit" class="submit-btn" id="submitBtn">
                    <i class="fas fa-paper-plane"></i> ط¥ط¶ط§ظپط© ظˆط¥ط±ط³ط§ظ„ ظ„ظ„ط¥ظٹظ…ظٹظ„
                </button>
            </form>
        </div>
    </div>

    <!-- SUCCESS MODAL -->
    <div class="modal-overlay" id="successModal">
        <div class="modal-box" style="max-width: 400px;">
            <div class="success-msg">
                <i class="fas fa-check-circle"></i>
                <h3>طھظ…طھ ط§ظ„ط¥ط¶ط§ظپط© ط¨ظ†ط¬ط§ط­!</h3>
                <p>طھظ… ط¥ط±ط³ط§ظ„ طھظپط§طµظٹظ„ ط§ظ„ظپط±طµط© ط¥ظ„ظ‰ ط¨ط±ظٹط¯ظƒ ط§ظ„ط¥ظ„ظƒطھط±ظˆظ†ظٹ.</p>
                <button class="submit-btn" style="margin-top: 20px;" onclick="closeSuccessModal()">
                    <i class="fas fa-thumbs-up"></i> طھظ…ط§ظ…
                </button>
            </div>
        </div>
    </div>

    <!-- EDIT/DASHBOARD MODAL -->
    <div class="modal-overlay" id="editModal">
        <div class="modal-box edit-modal-box">
            <button class="modal-close" onclick="closeEditModal()"><i class="fas fa-times"></i></button>
            <h2 class="modal-title">âڑ™ï¸ڈ ظ„ظˆط­ط© ط§ظ„طھط­ظƒظ…</h2>

            <!-- Main Dashboard -->
            <div id="dashboardMain">
                <p style="text-align:center; color: var(--text-light); margin-bottom: 20px;">ط§ط®طھط± ظ…ط§ طھط±ظٹط¯ طھط¹ط¯ظٹظ„ظ‡ ظپظٹ ط§ظ„ظ…ظˆظ‚ط¹</p>
                <div class="dashboard-grid">
                    <div class="dashboard-card" onclick="showEditSection('hero')">
                        <i class="fas fa-image"></i>
                        <h3>ط§ظ„ظ‡ظٹط¯ط± ظˆط§ظ„طµظˆط±</h3>
                        <p>طھط¹ط¯ظٹظ„ ط§ظ„ط´ط¹ط§ط±طŒ ط§ظ„ط¹ظ†ظˆط§ظ†طŒ ظˆط§ظ„طµظˆط±</p>
                    </div>
                    <div class="dashboard-card" onclick="showEditSection('stats')">
                        <i class="fas fa-chart-bar"></i>
                        <h3>ط§ظ„ط¥ط­طµط§ط¦ظٹط§طھ</h3>
                        <p>طھط¹ط¯ظٹظ„ ط§ظ„ط£ط±ظ‚ط§ظ… ظˆط§ظ„ط¥ط­طµط§ط¦ظٹط§طھ</p>
                    </div>
                    <div class="dashboard-card" onclick="showEditSection('colors')">
                        <i class="fas fa-palette"></i>
                        <h3>ط§ظ„ط£ظ„ظˆط§ظ† ظˆط§ظ„طھطµظ…ظٹظ…</h3>
                        <p>طھط؛ظٹظٹط± ط£ظ„ظˆط§ظ† ط§ظ„ظ…ظˆظ‚ط¹</p>
                    </div>
                    <div class="dashboard-card" onclick="showEditSection('content')">
                        <i class="fas fa-edit"></i>
                        <h3>ط§ظ„ظ…ط­طھظˆظ‰ ظˆط§ظ„ظ†طµظˆطµ</h3>
                        <p>طھط¹ط¯ظٹظ„ ط§ظ„ظ†طµظˆطµ ظˆط§ظ„ط¹ظ†ط§ظˆظٹظ†</p>
                    </div>
                    <div class="dashboard-card" onclick="showEditSection('links')">
                        <i class="fas fa-link"></i>
                        <h3>ط§ظ„ط±ظˆط§ط¨ط· ظˆط§ظ„طھظˆط§طµظ„</h3>
                        <p>طھط¹ط¯ظٹظ„ ط±ظˆط§ط¨ط· ط§ظ„طھظˆط§طµظ„ ط§ظ„ط§ط¬طھظ…ط§ط¹ظٹ</p>
                    </div>
                    <div class="dashboard-card" onclick="showEditSection('seo')">
                        <i class="fas fa-globe"></i>
                        <h3>SEO ظˆط§ظ„ط¯ظˆظ…ظٹظ†</h3>
                        <p>ط±ط¨ط· ط§ظ„ط¯ظˆظ…ظٹظ† ظˆط§ظ„ظ…ظٹطھط§ طھط§ط¬</p>
                    </div>
                </div>
            </div>

            <!-- Hero Edit Section -->
            <div class="edit-section" id="editHero">
                <button class="back-btn" onclick="backToDashboard()"><i class="fas fa-arrow-right"></i> ط±ط¬ظˆط¹</button>
                <h3 class="edit-section-title"><i class="fas fa-image"></i> طھط¹ط¯ظٹظ„ ط§ظ„ظ‡ظٹط¯ط± ظˆط§ظ„طµظˆط±</h3>
                <div class="edit-item">
                    <span class="edit-item-label">ط¹ظ†ظˆط§ظ† ط§ظ„ظ…ظˆظ‚ط¹ ط§ظ„ط±ط¦ظٹط³ظٹ:</span>
                    <input type="text" class="edit-item-input" id="editSiteTitle" value="FLY FOR CHANGE">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ط§ظ„ط¹ظ†ظˆط§ظ† ط§ظ„ظپط±ط¹ظٹ:</span>
                    <input type="text" class="edit-item-input" id="editSiteSubtitle" value="ط¹ط§ظ„ظ…ظƒ ظٹط¨ط¯ط£ ظ…ظ† ظ‡ظ†ط§ - ظ…ظ†ط­طŒ ظ…ط¤طھظ…ط±ط§طھطŒ طھط·ظˆط¹">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ط£ظٹظ‚ظˆظ†ط© ط§ظ„ط´ط¹ط§ط± (Font Awesome):</span>
                    <input type="text" class="edit-item-input" id="editLogoIcon" value="fa-globe-americas">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">طµظˆط±ط© ط®ظ„ظپظٹط© ط§ظ„ظ‡ظٹط¯ط± (ط±ط§ط¨ط·):</span>
                    <input type="text" class="edit-item-input" id="editHeroBg" placeholder="ط§طھط±ظƒظ‡ ظپط§ط±ط؛ط§ظ‹ ظ„ظ„طھط¯ط±ط¬ ط§ظ„ظ„ظˆظ†ظٹ">
                </div>
                <button class="edit-save-btn" onclick="saveHeroChanges()">
                    <i class="fas fa-save"></i> ط­ظپط¸ ط§ظ„طھط؛ظٹظٹط±ط§طھ
                </button>
            </div>

            <!-- Stats Edit Section -->
            <div class="edit-section" id="editStats">
                <button class="back-btn" onclick="backToDashboard()"><i class="fas fa-arrow-right"></i> ط±ط¬ظˆط¹</button>
                <h3 class="edit-section-title"><i class="fas fa-chart-bar"></i> طھط¹ط¯ظٹظ„ ط§ظ„ط¥ط­طµط§ط¦ظٹط§طھ</h3>
                <div class="stats-editor">
                    <div class="edit-item">
                        <span class="edit-item-label">ط§ظ„ظ…ظ†ط­ ط§ظ„ط¯ط±ط§ط³ظٹط©:</span>
                        <input type="text" class="edit-item-input" id="editStatScholarships" value="500+">
                    </div>
                    <div class="edit-item">
                        <span class="edit-item-label">ط§ظ„ظ…ط¤طھظ…ط±ط§طھ:</span>
                        <input type="text" class="edit-item-input" id="editStatConferences" value="200+">
                    </div>
                    <div class="edit-item">
                        <span class="edit-item-label">ظپط±طµ ط§ظ„طھط·ظˆط¹:</span>
                        <input type="text" class="edit-item-input" id="editStatVolunteering" value="150+">
                    </div>
                    <div class="edit-item">
                        <span class="edit-item-label">ط§ظ„ط¯ظˆظ„:</span>
                        <input type="text" class="edit-item-input" id="editStatCountries" value="50+">
                    </div>
                </div>
                <button class="edit-save-btn" onclick="saveStatsChanges()">
                    <i class="fas fa-save"></i> ط­ظپط¸ ط§ظ„طھط؛ظٹظٹط±ط§طھ
                </button>
            </div>

            <!-- Colors Edit Section -->
            <div class="edit-section" id="editColors">
                <button class="back-btn" onclick="backToDashboard()"><i class="fas fa-arrow-right"></i> ط±ط¬ظˆط¹</button>
                <h3 class="edit-section-title"><i class="fas fa-palette"></i> طھط¹ط¯ظٹظ„ ط§ظ„ط£ظ„ظˆط§ظ†</h3>
                <div class="edit-item">
                    <span class="edit-item-label">ط§ظ„ظ„ظˆظ† ط§ظ„ط£ط²ط±ظ‚ ط§ظ„ط³ظ…ط§ظˆظٹ:</span>
                    <div class="color-picker-wrapper">
                        <input type="color" id="editColorSky" value="#87CEEB">
                        <span id="editColorSkyVal">#87CEEB</span>
                    </div>
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ط§ظ„ظ„ظˆظ† ط§ظ„ط£ط²ط±ظ‚ ط§ظ„ط¹ظ…ظٹظ‚:</span>
                    <div class="color-picker-wrapper">
                        <input type="color" id="editColorDeep" value="#1E3A8A">
                        <span id="editColorDeepVal">#1E3A8A</span>
                    </div>
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ظ„ظˆظ† ط§ظ„ط°ظ‡ط¨:</span>
                    <div class="color-picker-wrapper">
                        <input type="color" id="editColorGold" value="#D4AF37">
                        <span id="editColorGoldVal">#D4AF37</span>
                    </div>
                </div>
                <button class="edit-save-btn" onclick="saveColorChanges()">
                    <i class="fas fa-save"></i> ط­ظپط¸ ط§ظ„طھط؛ظٹظٹط±ط§طھ
                </button>
            </div>

            <!-- Content Edit Section -->
            <div class="edit-section" id="editContent">
                <button class="back-btn" onclick="backToDashboard()"><i class="fas fa-arrow-right"></i> ط±ط¬ظˆط¹</button>
                <h3 class="edit-section-title"><i class="fas fa-edit"></i> طھط¹ط¯ظٹظ„ ط§ظ„ظ…ط­طھظˆظ‰</h3>
                <div class="edit-item">
                    <span class="edit-item-label">ط¹ظ†ظˆط§ظ† ط§ظ„ظپط¦ط§طھ:</span>
                    <input type="text" class="edit-item-input" id="editCatTitle" value="ط§ط³طھظƒط´ظپ ط§ظ„ظپط±طµ">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ظˆطµظپ ط§ظ„ظپط¦ط§طھ:</span>
                    <input type="text" class="edit-item-input" id="editCatDesc" value="ط§ط®طھط± ط§ظ„ظپط¦ط© ط§ظ„ظ…ظ†ط§ط³ط¨ط© ظ„ظƒ ظˆط§ط¨ط¯ط£ ط±ط­ظ„طھظƒ">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ط¹ظ†ظˆط§ظ† ط§ظ„ط¨ط±ط§ظ…ط¬:</span>
                    <input type="text" class="edit-item-input" id="editProgTitle" value="ط§ظ„ط¨ط±ط§ظ…ط¬ ط§ظ„ط¯ط±ط§ط³ظٹط©">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ط¹ظ†ظˆط§ظ† ط§ظ„طھط®طµطµط§طھ:</span>
                    <input type="text" class="edit-item-input" id="editSpecTitle" value="ط§ظ„طھط®طµطµط§طھ">
                </div>
                <button class="edit-save-btn" onclick="saveContentChanges()">
                    <i class="fas fa-save"></i> ط­ظپط¸ ط§ظ„طھط؛ظٹظٹط±ط§طھ
                </button>
            </div>

            <!-- Links Edit Section -->
            <div class="edit-section" id="editLinks">
                <button class="back-btn" onclick="backToDashboard()"><i class="fas fa-arrow-right"></i> ط±ط¬ظˆط¹</button>
                <h3 class="edit-section-title"><i class="fas fa-link"></i> ط±ظˆط§ط¨ط· ط§ظ„طھظˆط§طµظ„ ط§ظ„ط§ط¬طھظ…ط§ط¹ظٹ</h3>
                <div class="edit-item">
                    <span class="edit-item-label">ط¥ظ†ط³طھط¬ط±ط§ظ…:</span>
                    <input type="text" class="edit-item-input" id="editLinkInsta" value="https://www.instagram.com/flyforchange33">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ظٹظˆطھظٹظˆط¨:</span>
                    <input type="text" class="edit-item-input" id="editLinkYoutube" value="https://youtube.com/@flyforchange">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">طھظٹظƒ طھظˆظƒ:</span>
                    <input type="text" class="edit-item-input" id="editLinkTiktok" value="https://tiktok.com/@fly.for.change">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ظپظٹط³ط¨ظˆظƒ:</span>
                    <input type="text" class="edit-item-input" id="editLinkFacebook" placeholder="ط£ط¶ظپ ط±ط§ط¨ط· ظپظٹط³ط¨ظˆظƒ">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">طھظˆظٹطھط±/X:</span>
                    <input type="text" class="edit-item-input" id="editLinkTwitter" placeholder="ط£ط¶ظپ ط±ط§ط¨ط· طھظˆظٹطھط±">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ظ„ظٹظ†ظƒط¯ ط¥ظ†:</span>
                    <input type="text" class="edit-item-input" id="editLinkLinkedin" placeholder="ط£ط¶ظپ ط±ط§ط¨ط· ظ„ظٹظ†ظƒط¯ ط¥ظ†">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ط§ظ„ط¨ط±ظٹط¯ ط§ظ„ط¥ظ„ظƒطھط±ظˆظ†ظٹ:</span>
                    <input type="text" class="edit-item-input" id="editEmail" value="flyforchange33@gmail.com">
                </div>
                <button class="edit-save-btn" onclick="saveLinksChanges()">
                    <i class="fas fa-save"></i> ط­ظپط¸ ط§ظ„طھط؛ظٹظٹط±ط§طھ
                </button>
            </div>

            <!-- SEO/Domain Section -->
            <div class="edit-section" id="editSeo">
                <button class="back-btn" onclick="backToDashboard()"><i class="fas fa-arrow-right"></i> ط±ط¬ظˆط¹</button>
                <h3 class="edit-section-title"><i class="fas fa-globe"></i> SEO ظˆط±ط¨ط· ط§ظ„ط¯ظˆظ…ظٹظ†</h3>
                <div style="background: var(--bg-primary); padding: 20px; border-radius: 12px; margin-bottom: 20px;">
                    <h4 style="color: var(--deep-blue); margin-bottom: 10px;"><i class="fas fa-info-circle"></i> ظƒظٹظپظٹط© ط±ط¨ط· ط§ظ„ط¯ظˆظ…ظٹظ†:</h4>
                    <ol style="color: var(--text-light); line-height: 2; padding-right: 20px; text-align: right;">
                        <li>ط§ط´طھط± ط¯ظˆظ…ظٹظ† ظ…ظ† Namecheap, GoDaddy, ط£ظˆ Cloudflare</li>
                        <li>ظپظٹ ط¥ط¹ط¯ط§ط¯ط§طھ DNSطŒ ط£ط¶ظپ CNAME Record ظٹط´ظٹط± ط¥ظ„ظ‰ ط§ط³طھط¶ط§ظپطھظƒ</li>
                        <li>ط£ظˆ ط§ط³طھط®ط¯ظ… Netlify/Vercel (ظ…ط¬ط§ظ†ظٹ) ظˆط§ط±ظپط¹ ط§ظ„ظ…ظ„ظپط§طھ ظ‡ظ†ط§ظƒ</li>
                        <li>ط£ط¶ظپ ط§ط³ظ… ط§ظ„ط¯ظˆظ…ظٹظ† ظپظٹ ط§ظ„ط­ظ‚ظ„ ط£ط¯ظ†ط§ظ‡</li>
                    </ol>
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ط¹ظ†ظˆط§ظ† ط§ظ„ظ…ظˆظ‚ط¹ (Title):</span>
                    <input type="text" class="edit-item-input" id="editSeoTitle" value="Fly for Change | ط¹ط§ظ„ظ…ظƒ ظٹط¨ط¯ط£ ظ…ظ† ظ‡ظ†ط§">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ظˆطµظپ ط§ظ„ظ…ظˆظ‚ط¹ (Meta Description):</span>
                    <input type="text" class="edit-item-input" id="editSeoDesc" value="ظ…ظ†طµط© Fly for Change - ظ…ظ†ط­ ط¯ط±ط§ط³ظٹط©طŒ ظ…ط¤طھظ…ط±ط§طھطŒ طھط·ظˆط¹طŒ ظˆظپط±طµ ط¹ظ…ظ„ ط¯ظˆظ„ظٹط©">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ط§ظ„ظƒظ„ظ…ط§طھ ط§ظ„ظ…ظپطھط§ط­ظٹط©:</span>
                    <input type="text" class="edit-item-input" id="editSeoKeywords" value="ظ…ظ†ط­, ظ…ط¤طھظ…ط±ط§طھ, طھط·ظˆط¹, ط¨ظƒط§ظ„ظˆط±ظٹظˆط³, ظ…ط§ط¬ط³طھظٹط±, ط¯ظƒطھظˆط±ط§ظ‡">
                </div>
                <div class="edit-item">
                    <span class="edit-item-label">ط§ط³ظ… ط§ظ„ط¯ظˆظ…ظٹظ†:</span>
                    <input type="text" class="edit-item-input" id="editDomain" placeholder="ظ…ط«ط§ظ„: flyforchange.com">
                </div>
                <button class="edit-save-btn" onclick="saveSeoChanges()">
                    <i class="fas fa-save"></i> ط­ظپط¸ ط¥ط¹ط¯ط§ط¯ط§طھ SEO
                </button>
                <div style="margin-top: 20px; padding: 15px; background: rgba(34, 197, 94, 0.1); border-radius: 12px; border: 1px solid rgba(34, 197, 94, 0.3);">
                    <p style="color: #16a34a; font-size: 0.9rem;"><i class="fas fa-lightbulb"></i> <strong>ظ†طµظٹط­ط©:</strong> ط§ط³طھط®ط¯ظ… Netlify ط£ظˆ Vercel ظ„ط±ظپط¹ ط§ظ„ظ…ظˆظ‚ط¹ ظˆط±ط¨ط· ط§ظ„ط¯ظˆظ…ظٹظ† ط¨ط³ظ‡ظˆظ„ط©. ظپظ‚ط· ط§ط³ط­ط¨ ط§ظ„ظ…ظ„ظپط§طھ ط£ظˆ ط§ط±ظپط¹ظ‡ط§ ط¹ط¨ط± GitHub.</p>
                </div>
            </div>
        </div>
    </div>

    <!-- Language Switcher -->
    <div class="lang-switcher">
        <button class="lang-btn active" onclick="changeLang('ar')">ط§ظ„ط¹ط±ط¨ظٹط©</button>
        <button class="lang-btn" onclick="changeLang('en')">English</button>
        <button class="lang-btn" onclick="changeLang('fr')">Franأ§ais</button>
        <button class="lang-btn" onclick="changeLang('es')">Espaأ±ol</button>
        <button class="lang-btn" onclick="changeLang('it')">Italiano</button>
        <button class="lang-btn" onclick="changeLang('de')">Deutsch</button>
        <button class="lang-btn" onclick="changeLang('ru')">ذ رƒرپرپذ؛ذ¸ذ¹</button>
    </div>

    <!-- Theme Toggle -->
    <button class="theme-toggle" onclick="toggleTheme()" title="طھط¨ط¯ظٹظ„ ط§ظ„ظˆط¶ط¹">
        <i class="fas fa-moon" id="themeIcon"></i>
    </button>

    <!-- Hero Section -->
    <section class="hero-section">
        <div class="cloud cloud1"></div>
        <div class="cloud cloud2"></div>
        <div class="cloud cloud3"></div>
        <div class="cloud cloud4"></div>
        <div class="cloud cloud5"></div>
        <div class="plane-container">
            <div class="plane"><i class="fas fa-plane"></i></div>
        </div>
        <div class="logo-section">
            <div class="logo-icon"><i class="fas fa-globe-americas"></i></div>
            <h1 class="site-title" data-lang="title">FLY FOR CHANGE</h1>
            <p class="site-subtitle" data-lang="subtitle">ط¹ط§ظ„ظ…ظƒ ظٹط¨ط¯ط£ ظ…ظ† ظ‡ظ†ط§ - ظ…ظ†ط­طŒ ظ…ط¤طھظ…ط±ط§طھطŒ طھط·ظˆط¹</p>
        </div>
        <div class="search-container">
            <div class="search-box">
                <input type="text" class="search-input" placeholder="ط§ط¨ط­ط« ط¹ظ† ظ…ظ†ط­ط©طŒ ظ…ط¤طھظ…ط±طŒ ط£ظˆ ظپط±طµط© طھط·ظˆط¹..." data-lang="searchPlaceholder">
                <button class="search-btn"><i class="fas fa-search"></i></button>
            </div>
        </div>
        <div class="stats-bar">
            <div class="stat-item">
                <div class="stat-number">500+</div>
                <div class="stat-label" data-lang="scholarships">ظ…ظ†ط­ط© ط¯ط±ط§ط³ظٹط©</div>
            </div>
            <div class="stat-item">
                <div class="stat-number">200+</div>
                <div class="stat-label" data-lang="conferences">ظ…ط¤طھظ…ط± ط¯ظˆظ„ظٹ</div>
            </div>
            <div class="stat-item">
                <div class="stat-number">150+</div>
                <div class="stat-label" data-lang="volunteering">ظپط±طµط© طھط·ظˆط¹</div>
            </div>
            <div class="stat-item">
                <div class="stat-number">50+</div>
                <div class="stat-label" data-lang="countries">ط¯ظˆظ„ط© ظ…ط´ط§ط±ظƒط©</div>
            </div>
        </div>
    </section>

    <!-- Categories Section -->
    <section class="content-section">
        <h2 class="section-title fade-in" data-lang="categoriesTitle">ط§ط³طھظƒط´ظپ ط§ظ„ظپط±طµ</h2>
        <p class="section-desc fade-in" data-lang="categoriesDesc">ط§ط®طھط± ط§ظ„ظپط¦ط© ط§ظ„ظ…ظ†ط§ط³ط¨ط© ظ„ظƒ ظˆط§ط¨ط¯ط£ ط±ط­ظ„طھظƒ</p>
        <div class="categories-grid">
            <div class="category-card fade-in" onclick="showCategory('scholarships')">
                <div class="category-icon"><i class="fas fa-graduation-cap"></i></div>
                <h3 class="category-title" data-lang="catScholarships">ط§ظ„ظ…ظ†ط­ ط§ظ„ط¯ط±ط§ط³ظٹط©</h3>
                <p class="category-count">500+ ظپط±طµط©</p>
            </div>
            <div class="category-card fade-in" onclick="showCategory('conferences')">
                <div class="category-icon"><i class="fas fa-users"></i></div>
                <h3 class="category-title" data-lang="catConferences">ط§ظ„ظ…ط¤طھظ…ط±ط§طھ</h3>
                <p class="category-count">200+ ظ…ط¤طھظ…ط±</p>
            </div>
            <div class="category-card fade-in" onclick="showCategory('volunteering')">
                <div class="category-icon"><i class="fas fa-hand-holding-heart"></i></div>
                <h3 class="category-title" data-lang="catVolunteering">ط§ظ„طھط·ظˆط¹</h3>
                <p class="category-count">150+ ظپط±طµط©</p>
            </div>
            <div class="category-card fade-in" onclick="showCategory('jobs')">
                <div class="category-icon"><i class="fas fa-briefcase"></i></div>
                <h3 class="category-title" data-lang="catJobs">ط§ظ„ظˆط¸ط§ط¦ظپ ط§ظ„ط¯ظˆظ„ظٹط©</h3>
                <p class="category-count">300+ ظˆط¸ظٹظپط©</p>
            </div>
        </div>
    </section>

    <!-- ADDED OPPORTUNITIES SECTION (Dynamic) -->
    <section class="added-section" id="addedSection">
        <h2 class="section-title fade-in">ًں“Œ ط§ظ„ظپط±طµ ط§ظ„ظ…ط¶ط§ظپط© ط­ط¯ظٹط«ط§ظ‹</h2>
        <p class="section-desc fade-in">ظپط±طµ طھظ… ط¥ط¶ط§ظپطھظ‡ط§ ظ…ط¤ط®ط±ط§ظ‹ ط¹ظ„ظ‰ ط§ظ„ظ…ظ†طµط©</p>
        <div class="added-grid" id="addedGrid"></div>
    </section>

    <!-- Programs Section -->
    <section class="programs-section">
        <h2 class="section-title fade-in" data-lang="programsTitle">ط§ظ„ط¨ط±ط§ظ…ط¬ ط§ظ„ط¯ط±ط§ط³ظٹط©</h2>
        <p class="section-desc fade-in" data-lang="programsDesc">ظ…ظ†ط­ ظپظٹ ط¬ظ…ظٹط¹ ط§ظ„ظ…ط±ط§ط­ظ„ ط§ظ„ط¯ط±ط§ط³ظٹط©</p>
        <div class="programs-grid">
            <div class="program-card fade-in">
                <div class="program-image"><i class="fas fa-book"></i></div>
                <div class="program-content">
                    <span class="program-badge">ط¨ظƒط§ظ„ظˆط±ظٹظˆط³</span>
                    <h3 class="program-title" data-lang="bachelorTitle">ظ…ظ†ط­ ط§ظ„ط¨ظƒط§ظ„ظˆط±ظٹظˆط³</h3>
                    <p class="program-desc" data-lang="bachelorDesc">ظپط±طµ ط¯ط±ط§ط³ظٹط© ظƒط§ظ…ظ„ط© ظپظٹ ط£ظپط¶ظ„ ط§ظ„ط¬ط§ظ…ط¹ط§طھ ط§ظ„ط¹ط§ظ„ظ…ظٹط© ظ„ط¬ظ…ظٹط¹ ط§ظ„طھط®طµطµط§طھ</p>
                    <div class="program-meta">
                        <span><i class="fas fa-globe"></i> 45 ط¯ظˆظ„ط©</span>
                        <span><i class="fas fa-calendar"></i> 2026-2027</span>
                    </div>
                </div>
            </div>
            <div class="program-card fade-in">
                <div class="program-image"><i class="fas fa-user-graduate"></i></div>
                <div class="program-content">
                    <span class="program-badge">ظ…ط§ط¬ط³طھظٹط±</span>
                    <h3 class="program-title" data-lang="masterTitle">ظ…ظ†ط­ ط§ظ„ظ…ط§ط¬ط³طھظٹط±</h3>
                    <p class="program-desc" data-lang="masterDesc">ط¨ط±ط§ظ…ط¬ ط¯ط±ط§ط³ط§طھ ط¹ظ„ظٹط§ ظ…طھظ‚ط¯ظ…ط© ظ…ط¹ طھظ…ظˆظٹظ„ ظƒط§ظ…ظ„ ظˆط¨ط¯ظ„ ظ…ط¹ظٹط´ط©</p>
                    <div class="program-meta">
                        <span><i class="fas fa-globe"></i> 38 ط¯ظˆظ„ط©</span>
                        <span><i class="fas fa-calendar"></i> 2026-2027</span>
                    </div>
                </div>
            </div>
            <div class="program-card fade-in">
                <div class="program-image"><i class="fas fa-award"></i></div>
                <div class="program-content">
                    <span class="program-badge">ط¯ظƒطھظˆط±ط§ظ‡</span>
                    <h3 class="program-title" data-lang="phdTitle">ظ…ظ†ط­ ط§ظ„ط¯ظƒطھظˆط±ط§ظ‡</h3>
                    <p class="program-desc" data-lang="phdDesc">ط¨ط±ط§ظ…ط¬ ط¨ط­ط«ظٹط© ظ…طھظ‚ط¯ظ…ط© ظ…ط¹ ط¥ط´ط±ط§ظپ ط¯ظˆظ„ظٹ ظˆطھظ…ظˆظٹظ„ ظƒط§ظ…ظ„</p>
                    <div class="program-meta">
                        <span><i class="fas fa-globe"></i> 32 ط¯ظˆظ„ط©</span>
                        <span><i class="fas fa-calendar"></i> 2026-2027</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Specialties Section -->
    <section class="specialties-section">
        <h2 class="section-title fade-in" data-lang="specialtiesTitle">ط§ظ„طھط®طµطµط§طھ</h2>
        <p class="section-desc fade-in" data-lang="specialtiesDesc">ط§ط®طھط± طھط®طµطµظƒ ظˆط§ط¨ط­ط« ط¹ظ† ط§ظ„ظپط±طµ ط§ظ„ظ…ظ†ط§ط³ط¨ط©</p>
        <div class="specialties-grid">
            <div class="specialty-item fade-in"><div class="specialty-icon">ًںڈ¥</div><div class="specialty-name" data-lang="specMedicine">ط§ظ„ط·ط¨</div></div>
            <div class="specialty-item fade-in"><div class="specialty-icon">ًں”§</div><div class="specialty-name" data-lang="specEngineering">ط§ظ„ظ‡ظ†ط¯ط³ط©</div></div>
            <div class="specialty-item fade-in"><div class="specialty-icon">ًں’°</div><div class="specialty-name" data-lang="specAccounting">ط§ظ„ظ…ط­ط§ط³ط¨ط©</div></div>
            <div class="specialty-item fade-in"><div class="specialty-icon">ًں“ڑ</div><div class="specialty-name" data-lang="specArts">ط§ظ„ط¢ط¯ط§ط¨</div></div>
            <div class="specialty-item fade-in"><div class="specialty-icon">âڑ–ï¸ڈ</div><div class="specialty-name" data-lang="specLaw">ط§ظ„ظ‚ط§ظ†ظˆظ†</div></div>
            <div class="specialty-item fade-in"><div class="specialty-icon">ًں’»</div><div class="specialty-name" data-lang="specIT">طھظƒظ†ظˆظ„ظˆط¬ظٹط§ ط§ظ„ظ…ط¹ظ„ظˆظ…ط§طھ</div></div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
        <div class="footer-logo"><i class="fas fa-plane"></i></div>
        <h3 class="footer-title">FLY FOR CHANGE</h3>
        <p>ط¹ط§ظ„ظ…ظƒ ظٹط¨ط¯ط£ ظ…ظ† ظ‡ظ†ط§</p>
        <div class="footer-links">
            <a href="#" data-lang="linkAbout">ظ…ظ† ظ†ط­ظ†</a>
            <a href="#" data-lang="linkContact">ط§طھطµظ„ ط¨ظ†ط§</a>
            <a href="#" data-lang="linkPrivacy">ط³ظٹط§ط³ط© ط§ظ„ط®طµظˆطµظٹط©</a>
            <a href="#" data-lang="linkTerms">ط§ظ„ط´ط±ظˆط· ظˆط§ظ„ط£ط­ظƒط§ظ…</a>
        </div>
        <div class="social-links">
            <a href="#"><i class="fab fa-facebook-f"></i></a>
            <a href="#"><i class="fab fa-twitter"></i></a>
            <a href="https://www.instagram.com/flyforchange33?utm_source=qr&igsh=MTc5bzZpd2RxMzl0Yw==" target="_blank"><i class="fab fa-instagram"></i></a>
            <a href="https://tiktok.com/@fly.for.change" target="_blank"><i class="fab fa-tiktok"></i></a>
            <a href="https://youtube.com/@flyforchange?si=qYwvQlc65AB0jn1d" target="_blank"><i class="fab fa-youtube"></i></a>
        </div>
        <div class="copyright">
            <p>آ© 2026 Fly for Change. ط¬ظ…ظٹط¹ ط§ظ„ط­ظ‚ظˆظ‚ ظ…ط­ظپظˆط¸ط©.</p>
        </div>
    </footer>

    <script>
        // ====== ADMIN SYSTEM ======
        const ADMIN_PIN = '1717';
        let isAdmin = false;
        let uploadedImageBase64 = null;
        let opportunities = JSON.parse(localStorage.getItem('flyforchange_opportunities') || '[]');

        // PIN Modal
        function openPinModal() {
            document.getElementById('pinModal').classList.add('active');
            document.getElementById('pinError').classList.remove('show');
            setTimeout(() => document.querySelector('#pinModal input[data-index="0"]').focus(), 100);
        }
        function closePinModal() {
            document.getElementById('pinModal').classList.remove('active');
            document.querySelectorAll('#pinModal input').forEach(i => i.value = '');
            document.getElementById('pinError').classList.remove('show');
        }
        function handlePinInput(input, index) {
            const val = input.value;
            if (val && index < 3) {
                document.querySelector(`#pinModal input[data-index="${index + 1}"]`).focus();
            }
            if (val && index === 3) {
                setTimeout(verifyPin, 100);
            }
        }
        function handlePinKeydown(e, index) {
            if (e.key === 'Backspace' && !e.target.value && index > 0) {
                document.querySelector(`#pinModal input[data-index="${index - 1}"]`).focus();
            }
        }
        function verifyPin() {
            const inputs = document.querySelectorAll('#pinModal input');
            const entered = Array.from(inputs).map(i => i.value).join('');
            if (entered === ADMIN_PIN) {
                isAdmin = true;
                closePinModal();
                document.getElementById('adminLoginBtn').style.display = 'none';
                document.getElementById('adminAddBtn').classList.add('show');
                document.querySelectorAll('.delete-card-btn').forEach(btn => btn.style.display = 'flex');
                alert('âœ… طھظ… طھط³ط¬ظٹظ„ ط§ظ„ط¯ط®ظˆظ„ ظƒظ…ط´ط±ظپ ط¨ظ†ط¬ط§ط­!');
            } else {
                document.getElementById('pinError').classList.add('show');
                inputs.forEach(i => { i.value = ''; i.style.borderColor = '#ef4444'; });
                setTimeout(() => {
                    inputs.forEach(i => i.style.borderColor = '');
                    inputs[0].focus();
                }, 500);
            }
        }

        // Add Modal
        function openAddModal() {
            if (!isAdmin) { openPinModal(); return; }
            document.getElementById('addModal').classList.add('active');
            document.body.style.overflow = 'hidden';
        }
        function closeAddModal() {
            document.getElementById('addModal').classList.remove('active');
            document.body.style.overflow = '';
            document.getElementById('addForm').reset();
            resetImageUpload();
        }

        // Image Upload
        function handleImageUpload(e) {
            const file = e.target.files[0];
            if (!file) return;
            if (file.size > 5 * 1024 * 1024) {
                alert('ط­ط¬ظ… ط§ظ„طµظˆط±ط© ظƒط¨ظٹط± ط¬ط¯ط§ظ‹. ط§ظ„ط­ط¯ ط§ظ„ط£ظ‚طµظ‰ 5 ظ…ظٹط¬ط§ط¨ط§ظٹطھ.');
                return;
            }
            const reader = new FileReader();
            reader.onload = function(event) {
                uploadedImageBase64 = event.target.result;
                document.getElementById('previewImage').src = uploadedImageBase64;
                document.getElementById('previewImage').classList.add('show');
                document.getElementById('uploadPlaceholder').classList.add('hide');
                document.getElementById('imageUploadArea').classList.add('has-image');
            };
            reader.readAsDataURL(file);
        }
        function resetImageUpload() {
            uploadedImageBase64 = null;
            document.getElementById('previewImage').classList.remove('show');
            document.getElementById('uploadPlaceholder').classList.remove('hide');
            document.getElementById('imageUploadArea').classList.remove('has-image');
            document.getElementById('imageInput').value = '';
        }

        const typeLabels = {
            scholarship: 'ظ…ظ†ط­ط© ط¯ط±ط§ط³ظٹط©',
            conference: 'ظ…ط¤طھظ…ط±',
            volunteer: 'طھط·ظˆط¹',
            job: 'ظˆط¸ظٹظپط© ط¯ظˆظ„ظٹط©',
            internship: 'طھط¯ط±ظٹط¨ ط¹ظ…ظ„ظٹ',
            exchange: 'طھط¨ط§ط¯ظ„ ط«ظ‚ط§ظپظٹ'
        };

        // Submit Opportunity
        function submitOpportunity(e) {
            e.preventDefault();
            const btn = document.getElementById('submitBtn');
            btn.disabled = true;
            btn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> ط¬ط§ط±ظٹ ط§ظ„ط¥ط¶ط§ظپط©...';

            const opp = {
                id: Date.now(),
                type: document.getElementById('oppType').value,
                title: document.getElementById('oppTitle').value,
                desc: document.getElementById('oppDesc').value,
                field: document.getElementById('oppField').value,
                country: document.getElementById('oppCountry').value,
                deadline: document.getElementById('oppDeadline').value,
                link: document.getElementById('oppLink').value,
                image: uploadedImageBase64,
                dateAdded: new Date().toLocaleDateString('ar-EG')
            };

            opportunities.unshift(opp);
            localStorage.setItem('flyforchange_opportunities', JSON.stringify(opportunities));
            renderOpportunities();
        loadSavedSettings();

            const emailBody = `
ظپط±طµط© ط¬ط¯ظٹط¯ط© طھظ…طھ ط¥ط¶ط§ظپطھظ‡ط§ ط¹ظ„ظ‰ Fly for Change:

ًں“Œ ط§ظ„ط¹ظ†ظˆط§ظ†: ${opp.title}
ًں“‌ ط§ظ„ظ†ظˆط¹: ${typeLabels[opp.type]}
ًںژ“ ط§ظ„طھط®طµطµ: ${opp.field}
ًںŒچ ط§ظ„ط¯ظˆظ„ط©: ${opp.country}
ًں“… ط¢ط®ط± ظ…ظˆط¹ط¯: ${opp.deadline}
ًں”— ط§ظ„ط±ط§ط¨ط·: ${opp.link || 'ط؛ظٹط± ظ…طھظˆظپط±'}

ط§ظ„ظˆطµظپ:
${opp.desc}

طھظ…طھ ط§ظ„ط¥ط¶ط§ظپط© ط¨طھط§ط±ظٹط®: ${opp.dateAdded}
            `.trim();

            const mailtoLink = `mailto:flyforchange33@gmail.com?subject=ظپط±طµط© ط¬ط¯ظٹط¯ط©: ${encodeURIComponent(opp.title)}&body=${encodeURIComponent(emailBody)}`;

            setTimeout(() => {
                closeAddModal();
                document.getElementById('successModal').classList.add('active');
                btn.disabled = false;
                btn.innerHTML = '<i class="fas fa-paper-plane"></i> ط¥ط¶ط§ظپط© ظˆط¥ط±ط³ط§ظ„ ظ„ظ„ط¥ظٹظ…ظٹظ„';
                setTimeout(() => {
                    window.open(mailtoLink, '_blank');
                }, 800);
            }, 800);
        }

        function closeSuccessModal() {
            document.getElementById('successModal').classList.remove('active');
        }

        // Render Opportunities
        function renderOpportunities() {
            const grid = document.getElementById('addedGrid');
            const section = document.getElementById('addedSection');
            if (opportunities.length === 0) {
                section.classList.remove('has-items');
                return;
            }
            section.classList.add('has-items');
            grid.innerHTML = opportunities.map(opp => `
                <div class="added-card" data-id="${opp.id}">
                    <button class="delete-card-btn" onclick="deleteOpportunity(${opp.id})" title="ط­ط°ظپ">
                        <i class="fas fa-trash"></i>
                    </button>
                    <img class="added-card-image" src="${opp.image || 'https://images.unsplash.com/photo-1523050854058-8df90110c9f1?w=600&h=400&fit=crop'}" alt="${opp.title}">
                    <div class="added-card-content">
                        <span class="added-card-badge">${typeLabels[opp.type] || opp.type}</span>
                        <h3 class="added-card-title">${opp.title}</h3>
                        <p class="added-card-desc">${opp.desc}</p>
                        <div class="added-card-meta">
                            <span><i class="fas fa-graduation-cap"></i> ${opp.field}</span>
                            <span><i class="fas fa-globe"></i> ${opp.country}</span>
                            <span><i class="fas fa-calendar-alt"></i> ${opp.deadline}</span>
                        </div>
                        ${opp.link ? `<a href="${opp.link}" target="_blank" style="display:inline-block; margin-top:12px; color:var(--gold); font-weight:700; text-decoration:none;"><i class="fas fa-external-link-alt"></i> ط§ظ„طھظ‚ط¯ظٹظ… ط§ظ„ط¢ظ†</a>` : ''}
                    </div>
                </div>
            `).join('');
            if (isAdmin) {
                document.querySelectorAll('.delete-card-btn').forEach(btn => btn.style.display = 'flex');
            }
        }

        function deleteOpportunity(id) {
            if (!confirm('ظ‡ظ„ ط£ظ†طھ ظ…طھط£ظƒط¯ ظ…ظ† ط­ط°ظپ ظ‡ط°ظ‡ ط§ظ„ظپط±طµط©طں')) return;
            opportunities = opportunities.filter(o => o.id !== id);
            localStorage.setItem('flyforchange_opportunities', JSON.stringify(opportunities));
            renderOpportunities();
        loadSavedSettings();
        }

        // ====== TRANSLATIONS ======
        const translations = {
            ar: {
                title: "FLY FOR CHANGE", subtitle: "ط¹ط§ظ„ظ…ظƒ ظٹط¨ط¯ط£ ظ…ظ† ظ‡ظ†ط§ - ظ…ظ†ط­طŒ ظ…ط¤طھظ…ط±ط§طھطŒ طھط·ظˆط¹",
                searchPlaceholder: "ط§ط¨ط­ط« ط¹ظ† ظ…ظ†ط­ط©طŒ ظ…ط¤طھظ…ط±طŒ ط£ظˆ ظپط±طµط© طھط·ظˆط¹...",
                scholarships: "ظ…ظ†ط­ط© ط¯ط±ط§ط³ظٹط©", conferences: "ظ…ط¤طھظ…ط± ط¯ظˆظ„ظٹ", volunteering: "ظپط±طµط© طھط·ظˆط¹", countries: "ط¯ظˆظ„ط© ظ…ط´ط§ط±ظƒط©",
                categoriesTitle: "ط§ط³طھظƒط´ظپ ط§ظ„ظپط±طµ", categoriesDesc: "ط§ط®طھط± ط§ظ„ظپط¦ط© ط§ظ„ظ…ظ†ط§ط³ط¨ط© ظ„ظƒ ظˆط§ط¨ط¯ط£ ط±ط­ظ„طھظƒ",
                catScholarships: "ط§ظ„ظ…ظ†ط­ ط§ظ„ط¯ط±ط§ط³ظٹط©", catConferences: "ط§ظ„ظ…ط¤طھظ…ط±ط§طھ", catVolunteering: "ط§ظ„طھط·ظˆط¹", catJobs: "ط§ظ„ظˆط¸ط§ط¦ظپ ط§ظ„ط¯ظˆظ„ظٹط©",
                programsTitle: "ط§ظ„ط¨ط±ط§ظ…ط¬ ط§ظ„ط¯ط±ط§ط³ظٹط©", programsDesc: "ظ…ظ†ط­ ظپظٹ ط¬ظ…ظٹط¹ ط§ظ„ظ…ط±ط§ط­ظ„ ط§ظ„ط¯ط±ط§ط³ظٹط©",
                bachelorTitle: "ظ…ظ†ط­ ط§ظ„ط¨ظƒط§ظ„ظˆط±ظٹظˆط³", bachelorDesc: "ظپط±طµ ط¯ط±ط§ط³ظٹط© ظƒط§ظ…ظ„ط© ظپظٹ ط£ظپط¶ظ„ ط§ظ„ط¬ط§ظ…ط¹ط§طھ ط§ظ„ط¹ط§ظ„ظ…ظٹط© ظ„ط¬ظ…ظٹط¹ ط§ظ„طھط®طµطµط§طھ",
                masterTitle: "ظ…ظ†ط­ ط§ظ„ظ…ط§ط¬ط³طھظٹط±", masterDesc: "ط¨ط±ط§ظ…ط¬ ط¯ط±ط§ط³ط§طھ ط¹ظ„ظٹط§ ظ…طھظ‚ط¯ظ…ط© ظ…ط¹ طھظ…ظˆظٹظ„ ظƒط§ظ…ظ„ ظˆط¨ط¯ظ„ ظ…ط¹ظٹط´ط©",
                phdTitle: "ظ…ظ†ط­ ط§ظ„ط¯ظƒطھظˆط±ط§ظ‡", phdDesc: "ط¨ط±ط§ظ…ط¬ ط¨ط­ط«ظٹط© ظ…طھظ‚ط¯ظ…ط© ظ…ط¹ ط¥ط´ط±ط§ظپ ط¯ظˆظ„ظٹ ظˆطھظ…ظˆظٹظ„ ظƒط§ظ…ظ„",
                specialtiesTitle: "ط§ظ„طھط®طµطµط§طھ", specialtiesDesc: "ط§ط®طھط± طھط®طµطµظƒ ظˆط§ط¨ط­ط« ط¹ظ† ط§ظ„ظپط±طµ ط§ظ„ظ…ظ†ط§ط³ط¨ط©",
                specMedicine: "ط§ظ„ط·ط¨", specEngineering: "ط§ظ„ظ‡ظ†ط¯ط³ط©", specAccounting: "ط§ظ„ظ…ط­ط§ط³ط¨ط©", specArts: "ط§ظ„ط¢ط¯ط§ط¨", specLaw: "ط§ظ„ظ‚ط§ظ†ظˆظ†", specIT: "طھظƒظ†ظˆظ„ظˆط¬ظٹط§ ط§ظ„ظ…ط¹ظ„ظˆظ…ط§طھ",
                linkAbout: "ظ…ظ† ظ†ط­ظ†", linkContact: "ط§طھطµظ„ ط¨ظ†ط§", linkPrivacy: "ط³ظٹط§ط³ط© ط§ظ„ط®طµظˆطµظٹط©", linkTerms: "ط§ظ„ط´ط±ظˆط· ظˆط§ظ„ط£ط­ظƒط§ظ…"
            },
            en: {
                title: "FLY FOR CHANGE", subtitle: "Your World Starts Here - Scholarships, Conferences, Volunteering",
                searchPlaceholder: "Search for scholarships, conferences, or volunteering opportunities...",
                scholarships: "Scholarships", conferences: "Conferences", volunteering: "Volunteering", countries: "Countries",
                categoriesTitle: "Explore Opportunities", categoriesDesc: "Choose the right category and start your journey",
                catScholarships: "Scholarships", catConferences: "Conferences", catVolunteering: "Volunteering", catJobs: "International Jobs",
                programsTitle: "Academic Programs", programsDesc: "Scholarships at all academic levels",
                bachelorTitle: "Bachelor's Scholarships", bachelorDesc: "Full scholarships at top world universities for all majors",
                masterTitle: "Master's Scholarships", masterDesc: "Advanced graduate programs with full funding and living allowance",
                phdTitle: "PhD Scholarships", phdDesc: "Advanced research programs with international supervision and full funding",
                specialtiesTitle: "Specialties", specialtiesDesc: "Choose your specialty and find suitable opportunities",
                specMedicine: "Medicine", specEngineering: "Engineering", specAccounting: "Accounting", specArts: "Arts", specLaw: "Law", specIT: "Information Technology",
                linkAbout: "About Us", linkContact: "Contact Us", linkPrivacy: "Privacy Policy", linkTerms: "Terms & Conditions"
            },
            fr: {
                title: "FLY FOR CHANGE", subtitle: "Votre Monde Commence Ici - Bourses, Confأ©rences, Bأ©nأ©volat",
                searchPlaceholder: "Rechercher des bourses, confأ©rences ou opportunitأ©s de bأ©nأ©volat...",
                scholarships: "Bourses", conferences: "Confأ©rences", volunteering: "Bأ©nأ©volat", countries: "Pays",
                categoriesTitle: "Explorer les Opportunitأ©s", categoriesDesc: "Choisissez la bonne catأ©gorie et commencez votre voyage",
                catScholarships: "Bourses d'أ‰tudes", catConferences: "Confأ©rences", catVolunteering: "Bأ©nأ©volat", catJobs: "Emplois Internationaux",
                programsTitle: "Programmes Acadأ©miques", programsDesc: "Bourses أ  tous les niveaux acadأ©miques",
                bachelorTitle: "Bourses de Licence", bachelorDesc: "Bourses complأ¨tes dans les meilleures universitأ©s mondiales",
                masterTitle: "Bourses de Master", masterDesc: "Programmes d'أ©tudes supأ©rieures avancأ©s avec financement complet",
                phdTitle: "Bourses de Doctorat", phdDesc: "Programmes de recherche avancأ©s avec supervision internationale",
                specialtiesTitle: "Spأ©cialitأ©s", specialtiesDesc: "Choisissez votre spأ©cialitأ© et trouvez des opportunitأ©s",
                specMedicine: "Mأ©decine", specEngineering: "Ingأ©nierie", specAccounting: "Comptabilitأ©", specArts: "Arts", specLaw: "Droit", specIT: "Technologie de l'Information",
                linkAbout: "أ€ Propos", linkContact: "Contactez-Nous", linkPrivacy: "Politique de Confidentialitأ©", linkTerms: "Conditions Gأ©nأ©rales"
            },
            es: {
                title: "FLY FOR CHANGE", subtitle: "Tu Mundo Comienza Aquأ­ - Becas, Conferencias, Voluntariado",
                searchPlaceholder: "Buscar becas, conferencias o oportunidades de voluntariado...",
                scholarships: "Becas", conferences: "Conferencias", volunteering: "Voluntariado", countries: "Paأ­ses",
                categoriesTitle: "Explorar Oportunidades", categoriesDesc: "Elige la categorأ­a adecuada y comienza tu viaje",
                catScholarships: "Becas de Estudio", catConferences: "Conferencias", catVolunteering: "Voluntariado", catJobs: "Empleos Internacionales",
                programsTitle: "Programas Acadأ©micos", programsDesc: "Becas en todos los niveles acadأ©micos",
                bachelorTitle: "Becas de Grado", bachelorDesc: "Becas completas en las mejores universidades del mundo",
                masterTitle: "Becas de Mأ،ster", masterDesc: "Programas de posgrado avanzados con financiaciأ³n completa",
                phdTitle: "Becas de Doctorado", phdDesc: "Programas de investigaciأ³n avanzados con supervisiأ³n internacional",
                specialtiesTitle: "Especialidades", specialtiesDesc: "Elige tu especialidad y encuentra oportunidades",
                specMedicine: "Medicina", specEngineering: "Ingenierأ­a", specAccounting: "Contabilidad", specArts: "Artes", specLaw: "Derecho", specIT: "Tecnologأ­a de la Informaciأ³n",
                linkAbout: "Sobre Nosotros", linkContact: "Contأ،ctenos", linkPrivacy: "Polأ­tica de Privacidad", linkTerms: "Tأ©rminos y Condiciones"
            },
            it: {
                title: "FLY FOR CHANGE", subtitle: "Il Tuo Mondo Inizia Qui - Borse di Studio, Conferenze, Volontariato",
                searchPlaceholder: "Cerca borse di studio, conferenze o opportunitأ  di volontariato...",
                scholarships: "Borse", conferences: "Conferenze", volunteering: "Volontariato", countries: "Paesi",
                categoriesTitle: "Esplora le Opportunitأ ", categoriesDesc: "Scegli la categoria giusta e inizia il tuo viaggio",
                catScholarships: "Borse di Studio", catConferences: "Conferenze", catVolunteering: "Volontariato", catJobs: "Lavori Internazionali",
                programsTitle: "Programmi Accademici", programsDesc: "Borse di studio a tutti i livelli accademici",
                bachelorTitle: "Borse di Laurea", bachelorDesc: "Borse complete nelle migliori universitأ  mondiali",
                masterTitle: "Borse di Master", masterDesc: "Programmi avanzati con finanziamento completo",
                phdTitle: "Borse di Dottorato", phdDesc: "Programmi di ricerca avanzati con supervisione internazionale",
                specialtiesTitle: "Specializzazioni", specialtiesDesc: "Scegli la tua specializzazione e trova opportunitأ ",
                specMedicine: "Medicina", specEngineering: "Ingegneria", specAccounting: "Contabilitأ ", specArts: "Arti", specLaw: "Giurisprudenza", specIT: "Tecnologia dell'Informazione",
                linkAbout: "Chi Siamo", linkContact: "Contattaci", linkPrivacy: "Privacy Policy", linkTerms: "Termini e Condizioni"
            },
            de: {
                title: "FLY FOR CHANGE", subtitle: "Ihre Welt Beginnt Hier - Stipendien, Konferenzen, Freiwilligenarbeit",
                searchPlaceholder: "Suchen Sie Stipendien, Konferenzen oder Freiwilligenmأ¶glichkeiten...",
                scholarships: "Stipendien", conferences: "Konferenzen", volunteering: "Freiwilligenarbeit", countries: "Lأ¤nder",
                categoriesTitle: "Mأ¶glichkeiten Entdecken", categoriesDesc: "Wأ¤hlen Sie die richtige Kategorie und starten Sie Ihre Reise",
                catScholarships: "Studienstipendien", catConferences: "Konferenzen", catVolunteering: "Freiwilligenarbeit", catJobs: "Internationale Jobs",
                programsTitle: "Akademische Programme", programsDesc: "Stipendien auf allen akademischen Ebenen",
                bachelorTitle: "Bachelor-Stipendien", bachelorDesc: "Vollstipendien an den besten Universitأ¤ten der Welt",
                masterTitle: "Master-Stipendien", masterDesc: "Fortgeschrittene Graduiertenprogramme mit voller Finanzierung",
                phdTitle: "PhD-Stipendien", phdDesc: "Fortgeschrittene Forschungsprogramme mit internationaler Betreuung",
                specialtiesTitle: "Fachrichtungen", specialtiesDesc: "Wأ¤hlen Sie Ihre Fachrichtung und finden Sie Mأ¶glichkeiten",
                specMedicine: "Medizin", specEngineering: "Ingenieurwesen", specAccounting: "Buchhaltung", specArts: "Geisteswissenschaften", specLaw: "Recht", specIT: "Informationstechnologie",
                linkAbout: "أœber Uns", linkContact: "Kontakt", linkPrivacy: "Datenschutz", linkTerms: "Nutzungsbedingungen"
            },
            ru: {
                title: "FLY FOR CHANGE", subtitle: "ذ’ذ°رˆ ذœذ¸ر€ ذ‌ذ°ر‡ذ¸ذ½ذ°ذµر‚رپرڈ ذ—ذ´ذµرپرŒ - ذ،ر‚ذ¸ذ؟ذµذ½ذ´ذ¸ذ¸, ذڑذ¾ذ½ر„ذµر€ذµذ½ر†ذ¸ذ¸, ذ’ذ¾ذ»ذ¾ذ½ر‚ر‘ر€رپر‚ذ²ذ¾",
                searchPlaceholder: "ذںذ¾ذ¸رپذ؛ رپر‚ذ¸ذ؟ذµذ½ذ´ذ¸ذ¹, ذ؛ذ¾ذ½ر„ذµر€ذµذ½ر†ذ¸ذ¹ ذ¸ذ»ذ¸ ذ²ذ¾ذ»ذ¾ذ½ر‚ر‘ر€رپذ؛ذ¸ر… ذ²ذ¾ذ·ذ¼ذ¾ذ¶ذ½ذ¾رپر‚ذµذ¹...",
                scholarships: "ذ،ر‚ذ¸ذ؟ذµذ½ذ´ذ¸ذ¸", conferences: "ذڑذ¾ذ½ر„ذµر€ذµذ½ر†ذ¸ذ¸", volunteering: "ذ’ذ¾ذ»ذ¾ذ½ر‚ر‘ر€رپر‚ذ²ذ¾", countries: "ذ،ر‚ر€ذ°ذ½ر‹",
                categoriesTitle: "ذکرپرپذ»ذµذ´رƒذ¹ر‚ذµ ذ’ذ¾ذ·ذ¼ذ¾ذ¶ذ½ذ¾رپر‚ذ¸", categoriesDesc: "ذ’ر‹ذ±ذµر€ذ¸ر‚ذµ ذ؟ذ¾ذ´ر…ذ¾ذ´رڈر‰رƒرژ ذ؛ذ°ر‚ذµذ³ذ¾ر€ذ¸رژ ذ¸ ذ½ذ°ر‡ذ½ذ¸ر‚ذµ رپذ²ذ¾ر‘ ذ؟رƒر‚ذµرˆذµرپر‚ذ²ذ¸ذµ",
                catScholarships: "ذ£ر‡ذµذ±ذ½ر‹ذµ ذ،ر‚ذ¸ذ؟ذµذ½ذ´ذ¸ذ¸", catConferences: "ذڑذ¾ذ½ر„ذµر€ذµذ½ر†ذ¸ذ¸", catVolunteering: "ذ’ذ¾ذ»ذ¾ذ½ر‚ر‘ر€رپر‚ذ²ذ¾", catJobs: "ذœذµذ¶ذ´رƒذ½ذ°ر€ذ¾ذ´ذ½ر‹ذµ ذ’ذ°ذ؛ذ°ذ½رپذ¸ذ¸",
                programsTitle: "ذگذ؛ذ°ذ´ذµذ¼ذ¸ر‡ذµرپذ؛ذ¸ذµ ذںر€ذ¾ذ³ر€ذ°ذ¼ذ¼ر‹", programsDesc: "ذ،ر‚ذ¸ذ؟ذµذ½ذ´ذ¸ذ¸ ذ½ذ° ذ²رپذµر… ذ°ذ؛ذ°ذ´ذµذ¼ذ¸ر‡ذµرپذ؛ذ¸ر… رƒر€ذ¾ذ²ذ½رڈر…",
                bachelorTitle: "ذ،ر‚ذ¸ذ؟ذµذ½ذ´ذ¸ذ¸ ذ‘ذ°ذ؛ذ°ذ»ذ°ذ²ر€ذ¸ذ°ر‚ذ°", bachelorDesc: "ذںذ¾ذ»ذ½ر‹ذµ رپر‚ذ¸ذ؟ذµذ½ذ´ذ¸ذ¸ ذ² ذ»رƒر‡رˆذ¸ر… رƒذ½ذ¸ذ²ذµر€رپذ¸ر‚ذµر‚ذ°ر… ذ¼ذ¸ر€ذ°",
                masterTitle: "ذ،ر‚ذ¸ذ؟ذµذ½ذ´ذ¸ذ¸ ذœذ°ذ³ذ¸رپر‚ر€ذ°ر‚رƒر€ر‹", masterDesc: "ذںر€ذ¾ذ´ذ²ذ¸ذ½رƒر‚ر‹ذµ ذ؟ر€ذ¾ذ³ر€ذ°ذ¼ذ¼ر‹ رپ ذ؟ذ¾ذ»ذ½ر‹ذ¼ ر„ذ¸ذ½ذ°ذ½رپذ¸ر€ذ¾ذ²ذ°ذ½ذ¸ذµذ¼",
                phdTitle: "ذ،ر‚ذ¸ذ؟ذµذ½ذ´ذ¸ذ¸ ذگرپذ؟ذ¸ر€ذ°ذ½ر‚رƒر€ر‹", phdDesc: "ذںر€ذ¾ذ´ذ²ذ¸ذ½رƒر‚ر‹ذµ ذ¸رپرپذ»ذµذ´ذ¾ذ²ذ°ر‚ذµذ»رŒرپذ؛ذ¸ذµ ذ؟ر€ذ¾ذ³ر€ذ°ذ¼ذ¼ر‹ رپ ذ¼ذµذ¶ذ´رƒذ½ذ°ر€ذ¾ذ´ذ½ر‹ذ¼ ر€رƒذ؛ذ¾ذ²ذ¾ذ´رپر‚ذ²ذ¾ذ¼",
                specialtiesTitle: "ذ،ذ؟ذµر†ذ¸ذ°ذ»رŒذ½ذ¾رپر‚ذ¸", specialtiesDesc: "ذ’ر‹ذ±ذµر€ذ¸ر‚ذµ رپذ²ذ¾رژ رپذ؟ذµر†ذ¸ذ°ذ»رŒذ½ذ¾رپر‚رŒ ذ¸ ذ½ذ°ذ¹ذ´ذ¸ر‚ذµ ذ²ذ¾ذ·ذ¼ذ¾ذ¶ذ½ذ¾رپر‚ذ¸",
                specMedicine: "ذœذµذ´ذ¸ر†ذ¸ذ½ذ°", specEngineering: "ذکذ½ذ¶ذµذ½ذµر€ذ¸رڈ", specAccounting: "ذ‘رƒر…ذ³ذ°ذ»ر‚ذµر€ذ¸رڈ", specArts: "ذ“رƒذ¼ذ°ذ½ذ¸ر‚ذ°ر€ذ½ر‹ذµ ذ‌ذ°رƒذ؛ذ¸", specLaw: "ذںر€ذ°ذ²ذ¾", specIT: "ذکذ½ر„ذ¾ر€ذ¼ذ°ر†ذ¸ذ¾ذ½ذ½ر‹ذµ ذ¢ذµر…ذ½ذ¾ذ»ذ¾ذ³ذ¸ذ¸",
                linkAbout: "ذ‍ ذ‌ذ°رپ", linkContact: "ذ،ذ²رڈذ¶ذ¸ر‚ذµرپرŒ رپ ذ‌ذ°ذ¼ذ¸", linkPrivacy: "ذںذ¾ذ»ذ¸ر‚ذ¸ذ؛ذ° ذڑذ¾ذ½ر„ذ¸ذ´ذµذ½ر†ذ¸ذ°ذ»رŒذ½ذ¾رپر‚ذ¸", linkTerms: "ذ£رپذ»ذ¾ذ²ذ¸رڈ ذکرپذ؟ذ¾ذ»رŒذ·ذ¾ذ²ذ°ذ½ذ¸رڈ"
            }
        };

        let currentLang = 'ar';
        function changeLang(lang) {
            currentLang = lang;
            document.documentElement.lang = lang;
            document.documentElement.dir = lang === 'ar' ? 'rtl' : 'ltr';
            document.querySelectorAll('.lang-btn').forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');
            document.querySelectorAll('[data-lang]').forEach(el => {
                const key = el.getAttribute('data-lang');
                if (translations[lang] && translations[lang][key]) {
                    el.textContent = translations[lang][key];
                }
            });
            const searchInput = document.querySelector('.search-input');
            if (searchInput && translations[lang].searchPlaceholder) {
                searchInput.placeholder = translations[lang].searchPlaceholder;
            }
        }

        function toggleTheme() {
            const html = document.documentElement;
            const icon = document.getElementById('themeIcon');
            if (html.getAttribute('data-theme') === 'dark') {
                html.removeAttribute('data-theme');
                icon.classList.remove('fa-sun');
                icon.classList.add('fa-moon');
            } else {
                html.setAttribute('data-theme', 'dark');
                icon.classList.remove('fa-moon');
                icon.classList.add('fa-sun');
            }
        }

        function handleScrollAnimation() {
            document.querySelectorAll('.fade-in').forEach(el => {
                if (el.getBoundingClientRect().top < window.innerHeight - 100) {
                    el.classList.add('visible');
                }
            });
        }
        window.addEventListener('scroll', handleScrollAnimation);
        window.addEventListener('load', handleScrollAnimation);

        window.addEventListener('load', () => {
            setTimeout(() => {
                document.getElementById('loading').classList.add('hidden');
            }, 1500);
        });

        function showCategory(category) {
            alert('ط³ظٹطھظ… ط¹ط±ط¶ ' + category + ' ظ‚ط±ظٹط¨ط§ظ‹!');
        }

        document.querySelector('.search-btn').addEventListener('click', function() {
            const query = document.querySelector('.search-input').value;
            if (query) alert('ط¬ط§ط±ظٹ ط§ظ„ط¨ط­ط« ط¹ظ†: ' + query);
        });
        document.querySelector('.search-input').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') document.querySelector('.search-btn').click();
        });

        // Close modals on overlay click
        document.querySelectorAll('.modal-overlay').forEach(overlay => {
            overlay.addEventListener('click', function(e) {
                if (e.target === this) {
                    this.classList.remove('active');
                    if (this.id === 'addModal') {
                        document.body.style.overflow = '';
                        document.getElementById('addForm').reset();
                        resetImageUpload();
                    }
                    if (this.id === 'pinModal') {
                        document.querySelectorAll('#pinModal input').forEach(i => i.value = '');
                        document.getElementById('pinError').classList.remove('show');
                    }
                }
            });
        });


        // ====== EDIT/DASHBOARD SYSTEM ======
        function openEditModal() {
            if (!isAdmin) { openPinModal(); return; }
            document.getElementById('editModal').classList.add('active');
            document.body.style.overflow = 'hidden';
            backToDashboard();
        }
        function closeEditModal() {
            document.getElementById('editModal').classList.remove('active');
            document.body.style.overflow = '';
        }
        function showEditSection(section) {
            document.getElementById('dashboardMain').style.display = 'none';
            document.querySelectorAll('.edit-section').forEach(s => s.classList.remove('active'));
            document.getElementById('edit' + section.charAt(0).toUpperCase() + section.slice(1)).classList.add('active');
        }
        function backToDashboard() {
            document.getElementById('dashboardMain').style.display = 'block';
            document.querySelectorAll('.edit-section').forEach(s => s.classList.remove('active'));
        }

        // Load saved settings
        function loadSavedSettings() {
            const settings = JSON.parse(localStorage.getItem('flyforchange_settings') || '{}');
            if (settings.siteTitle) document.querySelector('.site-title').textContent = settings.siteTitle;
            if (settings.siteSubtitle) document.querySelector('.site-subtitle').textContent = settings.siteSubtitle;
            if (settings.logoIcon) {
                document.querySelector('.logo-icon i').className = 'fas ' + settings.logoIcon;
            }
            if (settings.stats) {
                const statItems = document.querySelectorAll('.stat-number');
                if (settings.stats.scholarships) statItems[0].textContent = settings.stats.scholarships;
                if (settings.stats.conferences) statItems[1].textContent = settings.stats.conferences;
                if (settings.stats.volunteering) statItems[2].textContent = settings.stats.volunteering;
                if (settings.stats.countries) statItems[3].textContent = settings.stats.countries;
            }
            if (settings.colors) {
                const root = document.documentElement;
                if (settings.colors.sky) root.style.setProperty('--sky-blue', settings.colors.sky);
                if (settings.colors.deep) root.style.setProperty('--deep-blue', settings.colors.deep);
                if (settings.colors.gold) root.style.setProperty('--gold', settings.colors.gold);
            }
            if (settings.content) {
                if (settings.content.catTitle) document.querySelector('[data-lang="categoriesTitle"]').textContent = settings.content.catTitle;
                if (settings.content.catDesc) document.querySelector('[data-lang="categoriesDesc"]').textContent = settings.content.catDesc;
                if (settings.content.progTitle) document.querySelector('[data-lang="programsTitle"]').textContent = settings.content.progTitle;
                if (settings.content.specTitle) document.querySelector('[data-lang="specialtiesTitle"]').textContent = settings.content.specTitle;
            }
            if (settings.links) {
                const socialLinks = document.querySelectorAll('.social-links a');
                if (settings.links.instagram) socialLinks[0].href = settings.links.instagram;
                if (settings.links.youtube) socialLinks[1].href = settings.links.youtube;
                if (settings.links.tiktok) socialLinks[2].href = settings.links.tiktok;
                if (settings.links.facebook) {
                    if (socialLinks[3]) socialLinks[3].href = settings.links.facebook;
                }
                if (settings.links.twitter) {
                    if (socialLinks[4]) socialLinks[4].href = settings.links.twitter;
                }
            }
            if (settings.seo) {
                if (settings.seo.title) document.title = settings.seo.title;
                if (settings.seo.desc) {
                    let metaDesc = document.querySelector('meta[name="description"]');
                    if (!metaDesc) {
                        metaDesc = document.createElement('meta');
                        metaDesc.name = 'description';
                        document.head.appendChild(metaDesc);
                    }
                    metaDesc.content = settings.seo.desc;
                }
            }
        }

        // Save functions
        function saveHeroChanges() {
            const settings = JSON.parse(localStorage.getItem('flyforchange_settings') || '{}');
            settings.siteTitle = document.getElementById('editSiteTitle').value;
            settings.siteSubtitle = document.getElementById('editSiteSubtitle').value;
            settings.logoIcon = document.getElementById('editLogoIcon').value;

            document.querySelector('.site-title').textContent = settings.siteTitle;
            document.querySelector('.site-subtitle').textContent = settings.siteSubtitle;
            document.querySelector('.logo-icon i').className = 'fas ' + settings.logoIcon;

            localStorage.setItem('flyforchange_settings', JSON.stringify(settings));
            alert('âœ… طھظ… ط­ظپط¸ طھط؛ظٹظٹط±ط§طھ ط§ظ„ظ‡ظٹط¯ط± ط¨ظ†ط¬ط§ط­!');
            backToDashboard();
        }
        function saveStatsChanges() {
            const settings = JSON.parse(localStorage.getItem('flyforchange_settings') || '{}');
            settings.stats = {
                scholarships: document.getElementById('editStatScholarships').value,
                conferences: document.getElementById('editStatConferences').value,
                volunteering: document.getElementById('editStatVolunteering').value,
                countries: document.getElementById('editStatCountries').value
            };
            const statItems = document.querySelectorAll('.stat-number');
            statItems[0].textContent = settings.stats.scholarships;
            statItems[1].textContent = settings.stats.conferences;
            statItems[2].textContent = settings.stats.volunteering;
            statItems[3].textContent = settings.stats.countries;
            localStorage.setItem('flyforchange_settings', JSON.stringify(settings));
            alert('âœ… طھظ… ط­ظپط¸ ط§ظ„ط¥ط­طµط§ط¦ظٹط§طھ ط¨ظ†ط¬ط§ط­!');
            backToDashboard();
        }
        function saveColorChanges() {
            const settings = JSON.parse(localStorage.getItem('flyforchange_settings') || '{}');
            settings.colors = {
                sky: document.getElementById('editColorSky').value,
                deep: document.getElementById('editColorDeep').value,
                gold: document.getElementById('editColorGold').value
            };
            const root = document.documentElement;
            root.style.setProperty('--sky-blue', settings.colors.sky);
            root.style.setProperty('--deep-blue', settings.colors.deep);
            root.style.setProperty('--gold', settings.colors.gold);
            root.style.setProperty('--gradient-start', settings.colors.sky);
            root.style.setProperty('--gradient-end', settings.colors.deep);
            localStorage.setItem('flyforchange_settings', JSON.stringify(settings));
            alert('âœ… طھظ… ط­ظپط¸ ط§ظ„ط£ظ„ظˆط§ظ† ط¨ظ†ط¬ط§ط­!');
            backToDashboard();
        }
        function saveContentChanges() {
            const settings = JSON.parse(localStorage.getItem('flyforchange_settings') || '{}');
            settings.content = {
                catTitle: document.getElementById('editCatTitle').value,
                catDesc: document.getElementById('editCatDesc').value,
                progTitle: document.getElementById('editProgTitle').value,
                specTitle: document.getElementById('editSpecTitle').value
            };
            document.querySelector('[data-lang="categoriesTitle"]').textContent = settings.content.catTitle;
            document.querySelector('[data-lang="categoriesDesc"]').textContent = settings.content.catDesc;
            document.querySelector('[data-lang="programsTitle"]').textContent = settings.content.progTitle;
            document.querySelector('[data-lang="specialtiesTitle"]').textContent = settings.content.specTitle;
            localStorage.setItem('flyforchange_settings', JSON.stringify(settings));
            alert('âœ… طھظ… ط­ظپط¸ ط§ظ„ظ…ط­طھظˆظ‰ ط¨ظ†ط¬ط§ط­!');
            backToDashboard();
        }
        function saveLinksChanges() {
            const settings = JSON.parse(localStorage.getItem('flyforchange_settings') || '{}');
            settings.links = {
                instagram: document.getElementById('editLinkInsta').value,
                youtube: document.getElementById('editLinkYoutube').value,
                tiktok: document.getElementById('editLinkTiktok').value,
                facebook: document.getElementById('editLinkFacebook').value,
                twitter: document.getElementById('editLinkTwitter').value,
                linkedin: document.getElementById('editLinkLinkedin').value,
                email: document.getElementById('editEmail').value
            };
            const socialLinks = document.querySelectorAll('.social-links a');
            if (settings.links.instagram) socialLinks[0].href = settings.links.instagram;
            if (settings.links.youtube) socialLinks[1].href = settings.links.youtube;
            if (settings.links.tiktok) socialLinks[2].href = settings.links.tiktok;
            if (settings.links.facebook && socialLinks[3]) socialLinks[3].href = settings.links.facebook;
            if (settings.links.twitter && socialLinks[4]) socialLinks[4].href = settings.links.twitter;
            if (settings.links.linkedin && socialLinks[5]) socialLinks[5].href = settings.links.linkedin;
            localStorage.setItem('flyforchange_settings', JSON.stringify(settings));
            alert('âœ… طھظ… ط­ظپط¸ ط§ظ„ط±ظˆط§ط¨ط· ط¨ظ†ط¬ط§ط­!');
            backToDashboard();
        }
        function saveSeoChanges() {
            const settings = JSON.parse(localStorage.getItem('flyforchange_settings') || '{}');
            settings.seo = {
                title: document.getElementById('editSeoTitle').value,
                desc: document.getElementById('editSeoDesc').value,
                keywords: document.getElementById('editSeoKeywords').value,
                domain: document.getElementById('editDomain').value
            };
            document.title = settings.seo.title;
            let metaDesc = document.querySelector('meta[name="description"]');
            if (!metaDesc) {
                metaDesc = document.createElement('meta');
                metaDesc.name = 'description';
                document.head.appendChild(metaDesc);
            }
            metaDesc.content = settings.seo.desc;
            let metaKeywords = document.querySelector('meta[name="keywords"]');
            if (!metaKeywords) {
                metaKeywords = document.createElement('meta');
                metaKeywords.name = 'keywords';
                document.head.appendChild(metaKeywords);
            }
            metaKeywords.content = settings.seo.keywords;
            localStorage.setItem('flyforchange_settings', JSON.stringify(settings));
            alert('âœ… طھظ… ط­ظپط¸ ط¥ط¹ط¯ط§ط¯ط§طھ SEO ط¨ظ†ط¬ط§ط­!\n\nظ„ط±ط¨ط· ط§ظ„ط¯ظˆظ…ظٹظ†: ط§ط³طھط®ط¯ظ… Netlify ط£ظˆ Vercel ظˆط§ط±ظپط¹ ط§ظ„ظ…ظ„ظپط§طھ ظ‡ظ†ط§ظƒ.');
            backToDashboard();
        }

        // Color picker listeners
        document.addEventListener('DOMContentLoaded', function() {
            const colorInputs = ['editColorSky', 'editColorDeep', 'editColorGold'];
            const colorVals = ['editColorSkyVal', 'editColorDeepVal', 'editColorGoldVal'];
            colorInputs.forEach((id, idx) => {
                const input = document.getElementById(id);
                if (input) {
                    input.addEventListener('input', function() {
                        document.getElementById(colorVals[idx]).textContent = this.value;
                    });
                }
            });
        });

        // Show admin buttons when logged in
        const originalVerifyPin = verifyPin;
        verifyPin = function() {
            const inputs = document.querySelectorAll('#pinModal input');
            const entered = Array.from(inputs).map(i => i.value).join('');
            if (entered === ADMIN_PIN) {
                isAdmin = true;
                closePinModal();
                document.getElementById('adminLoginBtn').style.display = 'none';
                document.getElementById('adminAddBtn').classList.add('show');
                document.getElementById('adminEditBtn').classList.add('show');
                document.querySelectorAll('.delete-card-btn').forEach(btn => btn.style.display = 'flex');
                alert('âœ… طھظ… طھط³ط¬ظٹظ„ ط§ظ„ط¯ط®ظˆظ„ ظƒظ…ط´ط±ظپ ط¨ظ†ط¬ط§ط­!');
            } else {
                document.getElementById('pinError').classList.add('show');
                inputs.forEach(i => { i.value = ''; i.style.borderColor = '#ef4444'; });
                setTimeout(() => {
                    inputs.forEach(i => i.style.borderColor = '');
                    inputs[0].focus();
                }, 500);
            }
        };

        // Initialize
        renderOpportunities();
        loadSavedSettings();
    </script>
</body>
</html>
