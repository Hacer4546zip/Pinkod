<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>COSMIC PORTAL - Koinot Sayohati</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: #000;
            color: white;
            overflow-x: hidden;
        }

        /* Landing Page Styles */
        .landing-page {
            min-height: 100vh;
            background: linear-gradient(to bottom, rgba(30, 27, 75, 0.5), rgba(88, 28, 135, 0.3), #000);
            position: relative;
            overflow: hidden;
        }

        .stars {
            position: absolute;
            width: 100%;
            height: 100%;
            overflow: hidden;
        }

        .star {
            position: absolute;
            background: white;
            border-radius: 50%;
            opacity: 0.8;
            animation: moveStars 10s linear infinite, twinkle 2s ease-in-out infinite alternate;
        }

        @keyframes moveStars {
            from { transform: translateY(100vh) translateX(0); }
            to { transform: translateY(-100vh) translateX(50px); }
        }

        @keyframes twinkle {
            from { opacity: 0.3; }
            to { opacity: 1; }
        }

        .nebula {
            position: absolute;
            border-radius: 50%;
            filter: blur(60px);
            animation: pulse 2s ease-in-out infinite alternate;
        }

        .nebula1 {
            top: 0;
            left: 0;
            width: 384px;
            height: 384px;
            background: rgba(168, 85, 247, 0.1);
        }

        .nebula2 {
            top: 50%;
            right: 0;
            width: 320px;
            height: 320px;
            background: rgba(6, 182, 212, 0.1);
            animation-delay: 1s;
        }

        .nebula3 {
            bottom: 0;
            left: 33%;
            width: 288px;
            height: 288px;
            background: rgba(236, 72, 153, 0.1);
            animation-delay: 2s;
        }

        @keyframes pulse {
            from { opacity: 0.3; }
            to { opacity: 0.8; }
        }

        .main-content {
            position: relative;
            z-index: 10;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            padding: 20px;
            text-align: center;
        }

        .logo-section {
            margin-bottom: 50px;
            opacity: 0;
            transform: translateY(40px);
            animation: fadeInUp 1s ease-out 0.5s forwards;
        }

        @keyframes fadeInUp {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .logo {
            width: 128px;
            height: 128px;
            margin: 0 auto 24px;
            position: relative;
        }

        .logo-ring {
            position: absolute;
            inset: 0;
            background: linear-gradient(to right, #06b6d4, #a855f7, #ec4899);
            border-radius: 50%;
            filter: blur(2px);
            animation: spin 4s linear infinite;
        }

        .logo-inner {
            position: absolute;
            inset: 8px;
            background: linear-gradient(to bottom right, #1f2937, #000);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px solid rgba(6, 182, 212, 0.3);
        }

        .logo-icon {
            width: 48px;
            height: 48px;
            color: #06b6d4;
            animation: pulse 2s ease-in-out infinite alternate;
        }

        .logo-dot {
            position: absolute;
            top: -8px;
            right: -8px;
            width: 24px;
            height: 24px;
            background: #fbbf24;
            border-radius: 50%;
            animation: ping 1s cubic-bezier(0, 0, 0.2, 1) infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        @keyframes ping {
            75%, 100% {
                transform: scale(2);
                opacity: 0;
            }
        }

        .main-title {
            font-size: 3rem;
            font-weight: bold;
            background: linear-gradient(to right, #a7f3d0, #c084fc, #f9a8d4);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 16px;
            animation: pulse 3s ease-in-out infinite alternate;
        }

        .subtitle {
            font-size: 1.25rem;
            background: linear-gradient(to right, #34d399, #06b6d4);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            font-weight: 600;
            margin-bottom: 32px;
            max-width: 768px;
            animation: pulse 2.5s ease-in-out infinite alternate;
        }

        .buttons-container {
            width: 100%;
            max-width: 512px;
            display: flex;
            flex-direction: column;
            gap: 24px;
            opacity: 0;
            transform: translateY(40px);
            animation: fadeInUp 1s ease-out 0.8s forwards;
        }

        .spaceship-button {
            position: relative;
            group: true;
        }

        .button-glow {
            position: absolute;
            inset: -4px;
            border-radius: 24px;
            filter: blur(4px);
            opacity: 0.75;
            animation: pulse 2s ease-in-out infinite alternate;
            transition: opacity 1s;
        }

        .button-glow.cyan {
            background: linear-gradient(to right, #06b6d4, #3b82f6, #8b5cf6);
        }

        .button-glow.pink {
            background: linear-gradient(to right, #ec4899, #a855f7, #6366f1);
        }

        .button-glow.emerald {
            background: linear-gradient(to right, #10b981, #059669, #0d9488);
        }

        .spaceship-button:hover .button-glow {
            opacity: 1;
        }

        .button-card {
            position: relative;
            padding: 8px;
            background: linear-gradient(to right, #1f2937, #000);
            border-radius: 24px;
            border: 1px solid rgba(6, 182, 212, 0.3);
        }

        .button-main {
            width: 100%;
            height: 80px;
            background: rgba(6, 182, 212, 0.2);
            border: 1px solid rgba(6, 182, 212, 0.5);
            border-radius: 16px;
            color: white;
            font-weight: bold;
            font-size: 1.125rem;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            backdrop-filter: blur(4px);
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 16px;
        }

        .button-main:hover {
            transform: scale(1.05);
        }

        .button-main.pink {
            background: rgba(236, 72, 153, 0.2);
            border-color: rgba(236, 72, 153, 0.5);
        }

        .button-main.emerald {
            background: rgba(16, 185, 129, 0.2);
            border-color: rgba(16, 185, 129, 0.5);
        }

        .button-shine {
            position: absolute;
            inset: 0;
            background: linear-gradient(to right, transparent, rgba(6, 182, 212, 0.2), transparent);
            transform: translateX(-100%) skewX(-12deg);
            transition: transform 1s;
        }

        .button-main:hover .button-shine {
            transform: translateX(100%) skewX(-12deg);
        }

        .button-content {
            display: flex;
            align-items: center;
            gap: 16px;
            position: relative;
            z-index: 10;
        }

        .button-icon-container {
            padding: 12px;
            border-radius: 50%;
            border: 1px solid rgba(6, 182, 212, 0.5);
            backdrop-filter: blur(4px);
        }

        .button-icon-container.cyan {
            background: rgba(6, 182, 212, 0.2);
        }

        .button-icon-container.pink {
            background: rgba(236, 72, 153, 0.2);
            border-color: rgba(236, 72, 153, 0.5);
        }

        .button-icon-container.emerald {
            background: rgba(16, 185, 129, 0.2);
            border-color: rgba(16, 185, 129, 0.5);
        }

        .button-icon {
            width: 32px;
            height: 32px;
            animation: pulse 2s ease-in-out infinite alternate;
        }

        .button-text {
            text-align: left;
        }

        .button-label {
            font-size: 0.875rem;
            font-weight: 500;
            margin-bottom: 4px;
        }

        .button-label.cyan { color: #67e8f9; }
        .button-label.pink { color: #f9a8d4; }
        .button-label.emerald { color: #6ee7b7; }

        .button-title {
            font-weight: bold;
            color: white;
            font-size: 1.125rem;
        }

        .button-indicators {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .indicator-icon {
            width: 24px;
            height: 24px;
            color: #fbbf24;
        }

        .indicator-icon.spin {
            animation: spin 3s linear infinite;
        }

        .indicator-icon.bounce {
            animation: bounce 1s ease-in-out infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-25%); }
        }

        .indicator-bar {
            width: 8px;
            height: 32px;
            border-radius: 4px;
            animation: pulse 1.5s ease-in-out infinite alternate;
        }

        .indicator-bar.cyan {
            background: linear-gradient(to top, #06b6d4, transparent);
        }

        .indicator-bar.pink {
            background: linear-gradient(to top, #ec4899, transparent);
        }

        .indicator-bar.emerald {
            background: linear-gradient(to top, #10b981, transparent);
        }

        .footer {
            margin-top: 48px;
            opacity: 0;
            transform: translateY(40px);
            animation: fadeInUp 1s ease-out 1.1s forwards;
        }

        .footer-content {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            background: linear-gradient(to right, #10b981, #06b6d4);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            font-size: 1.125rem;
            font-weight: 600;
        }

        .footer-star {
            width: 20px;
            height: 20px;
            color: #fbbf24;
            animation: pulse 2s ease-in-out infinite alternate;
        }

        .footer-text {
            font-size: 0.875rem;
            color: #9ca3af;
            margin-top: 12px;
        }

        /* Chat Page Styles */
        .chat-page {
            display: none;
            height: 100vh;
            background: #1f2937;
            flex-direction: column;
        }

        .chat-header {
            background: #374151;
            border-bottom: 1px solid #4b5563;
            padding: 16px;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .back-button {
            background: transparent;
            border: none;
            color: #9ca3af;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 8px;
            padding: 8px;
            border-radius: 8px;
            transition: color 0.3s;
        }

        .back-button:hover {
            color: white;
        }

        .operator-info {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .operator-avatar {
            width: 40px;
            height: 40px;
            background: linear-gradient(to right, #10b981, #059669);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: black;
            font-weight: bold;
            font-size: 1.125rem;
        }

        .operator-details h2 {
            color: white;
            font-weight: bold;
            font-size: 1.125rem;
            margin-bottom: 4px;
        }

        .operator-status {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .status-dot {
            width: 8px;
            height: 8px;
            background: #10b981;
            border-radius: 50%;
            animation: pulse 1s ease-in-out infinite;
        }

        .status-text {
            color: #10b981;
            font-size: 0.875rem;
        }

        .messages-container {
            flex: 1;
            overflow-y: auto;
            padding: 16px;
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        .welcome-message {
            text-align: center;
            color: #9ca3af;
            margin-top: 32px;
        }

        .welcome-message p:first-child {
            font-size: 1.125rem;
            margin-bottom: 8px;
        }

        .message {
            display: flex;
            animation: slideIn 0.6s ease-out;
        }

        .message.user {
            justify-content: flex-end;
        }

        .message.bot {
            justify-content: flex-start;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .message-bubble {
            max-width: 80%;
            padding: 12px;
            border-radius: 16px;
            position: relative;
            transition: transform 0.3s;
        }

        .message-bubble:hover {
            transform: scale(1.02);
        }

        .message-bubble.user {
            background: linear-gradient(to right, #2563eb, #1d4ed8);
            color: white;
            box-shadow: 0 4px 6px rgba(37, 99, 235, 0.2);
        }

        .message-bubble.bot {
            background: linear-gradient(to right, #374151, #1f2937);
            color: white;
            border: 1px solid #4b5563;
            box-shadow: 0 4px 6px rgba(75, 85, 99, 0.1);
        }

        .message-text {
            font-size: 0.875rem;
            line-height: 1.5;
            white-space: pre-wrap;
        }

        .url-section {
            margin-top: 12px;
        }

        .url-label {
            font-size: 0.75rem;
            color: #d1d5db;
            margin-bottom: 8px;
        }

        .url-button {
            width: 100%;
            padding: 12px;
            border: none;
            border-radius: 12px;
            color: white;
            font-weight: bold;
            cursor: pointer;
            position: relative;
            overflow: hidden;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            border: 2px solid rgba(255, 255, 255, 0.2);
        }

        .url-button:hover {
            transform: scale(1.05);
        }

        .url-button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .loading-message {
            display: flex;
            justify-content: flex-start;
        }

        .loading-bubble {
            background: linear-gradient(to right, #374151, #1f2937);
            color: white;
            border: 1px solid #4b5563;
            padding: 12px;
            border-radius: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .loading-spinner {
            width: 16px;
            height: 16px;
            border: 2px solid #10b981;
            border-top: 2px solid transparent;
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        .loading-dots {
            display: flex;
            gap: 4px;
        }

        .loading-dot {
            width: 4px;
            height: 4px;
            background: #9ca3af;
            border-radius: 50%;
            animation: bounce 1s ease-in-out infinite;
        }

        .loading-dot:nth-child(2) { animation-delay: 0.2s; }
        .loading-dot:nth-child(3) { animation-delay: 0.4s; }

        .input-area {
            background: #374151;
            border-top: 1px solid #4b5563;
            padding: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .image-button {
            background: transparent;
            border: none;
            color: #9ca3af;
            cursor: pointer;
            padding: 8px;
            border-radius: 8px;
            transition: all 0.2s;
        }

        .image-button:hover {
            color: white;
            background: #4b5563;
        }

        .message-input {
            flex: 1;
            background: #4b5563;
            border: 1px solid #6b7280;
            color: white;
            padding: 12px;
            border-radius: 12px;
            font-size: 16px;
            outline: none;
            transition: border-color 0.2s;
        }

        .message-input:focus {
            border-color: #10b981;
        }

        .message-input::placeholder {
            color: #9ca3af;
        }

        .send-button {
            background: linear-gradient(to right, #10b981, #059669);
            border: none;
            color: white;
            padding: 12px;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.2s;
        }

        .send-button:hover {
            transform: scale(1.05);
        }

        .send-button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        /* Modal Styles */
        .modal {
            position: fixed;
            inset: 0;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(4px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 50;
            padding: 16px;
            animation: fadeIn 0.5s ease-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .modal-content {
            background: linear-gradient(to bottom right, #1f2937, #000);
            padding: 32px;
            border-radius: 24px;
            border: 1px solid rgba(6, 182, 212, 0.3);
            max-width: 400px;
            width: 100%;
            position: relative;
            overflow: hidden;
            animation: scaleIn 0.3s ease-out;
        }

        @keyframes scaleIn {
            from {
                opacity: 0;
                transform: scale(0.9);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        .modal-bg {
            position: absolute;
            inset: 0;
            background: linear-gradient(to right, rgba(6, 182, 212, 0.1), rgba(168, 85, 247, 0.1), rgba(236, 72, 153, 0.1));
            animation: pulse 2s ease-in-out infinite alternate;
        }

        .modal-body {
            position: relative;
            z-index: 10;
            text-align: center;
        }

        .modal-icon {
            width: 80px;
            height: 80px;
            margin: 0 auto 24px;
            position: relative;
        }

        .modal-icon-ring {
            position: absolute;
            inset: 0;
            background: linear-gradient(to right, #06b6d4, #a855f7);
            border-radius: 50%;
            animation: spin 2s linear infinite;
        }

        .modal-icon-inner {
            position: absolute;
            inset: 8px;
            background: #1f2937;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .modal-icon svg {
            width: 32px;
            height: 32px;
            color: #06b6d4;
            animation: pulse 1.5s ease-in-out infinite alternate;
        }

        .modal-title {
            font-size: 1.5rem;
            font-weight: bold;
            color: white;
            margin-bottom: 16px;
        }

        .modal-text {
            color: #67e8f9;
            margin-bottom: 24px;
            animation: pulse 1.5s ease-in-out infinite alternate;
        }

        .progress-bar {
            width: 100%;
            background: #4b5563;
            border-radius: 9999px;
            height: 12px;
            margin-bottom: 24px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(to right, #06b6d4, #a855f7);
            border-radius: 9999px;
            transition: width 0.3s;
            position: relative;
        }

        .progress-shine {
            position: absolute;
            inset: 0;
            background: linear-gradient(to right, transparent, rgba(255, 255, 255, 0.3), transparent);
            animation: pulse 1s ease-in-out infinite alternate;
        }

        .modal-status {
            font-size: 0.875rem;
            color: #9ca3af;
        }

        .countdown {
            font-size: 2rem;
            font-weight: bold;
            color: white;
            margin-bottom: 16px;
        }

        /* Floating Elements */
        .floating-element {
            position: absolute;
            border: 2px solid;
            border-radius: 50%;
            opacity: 0.3;
        }

        .floating-1 {
            top: 40px;
            left: 40px;
            width: 80px;
            height: 80px;
            border-color: rgba(6, 182, 212, 0.3);
            animation: spin 10s linear infinite;
        }

        .floating-2 {
            bottom: 40px;
            right: 40px;
            width: 64px;
            height: 64px;
            border-color: rgba(236, 72, 153, 0.3);
            animation: spin 8s linear infinite reverse;
        }

        .floating-3 {
            top: 50%;
            left: 20px;
            width: 48px;
            height: 48px;
            border-color: rgba(168, 85, 247, 0.3);
            animation: ping 1s cubic-bezier(0, 0, 0.2, 1) infinite;
        }

        .floating-4 {
            top: 25%;
            right: 20px;
            width: 32px;
            height: 32px;
            border-color: rgba(251, 191, 36, 0.3);
            animation: ping 1s cubic-bezier(0, 0, 0.2, 1) infinite;
            animation-delay: 1s;
        }

        /* Mobile Responsive */
        @media (max-width: 768px) {
            .main-title {
                font-size: 2rem;
            }

            .subtitle {
                font-size: 1rem;
            }

            .buttons-container {
                max-width: 100%;
            }

            .button-main {
                height: 70px;
                font-size: 1rem;
            }

            .button-title {
                font-size: 1rem;
            }

            .message-bubble {
                max-width: 90%;
            }

            .modal-content {
                margin: 16px;
            }
        }

        /* Button Color Classes */
        .btn-color-1 { background: linear-gradient(to right, #3b82f6, #2563eb); }
        .btn-color-2 { background: linear-gradient(to right, #8b5cf6, #7c3aed); }
        .btn-color-3 { background: linear-gradient(to right, #ec4899, #db2777); }
        .btn-color-4 { background: linear-gradient(to right, #ef4444, #dc2626); }
        .btn-color-5 { background: linear-gradient(to right, #f97316, #ea580c); }
        .btn-color-6 { background: linear-gradient(to right, #eab308, #ca8a04); }
        .btn-color-7 { background: linear-gradient(to right, #22c55e, #16a34a); }
        .btn-color-8 { background: linear-gradient(to right, #10b981, #059669); }
        .btn-color-9 { background: linear-gradient(to right, #14b8a6, #0d9488); }
        .btn-color-10 { background: linear-gradient(to right, #06b6d4, #0891b2); }
        .btn-color-11 { background: linear-gradient(to right, #6366f1, #4f46e5); }
        .btn-color-12 { background: linear-gradient(to right, #8b5cf6, #7c3aed); }
        .btn-color-13 { background: linear-gradient(to right, #d946ef, #c026d3); }
        .btn-color-14 { background: linear-gradient(to right, #f43f5e, #e11d48); }
        .btn-color-15 { background: linear-gradient(to right, #64748b, #475569); }
    </style>
</head>
<body>
    <!-- Landing Page -->
    <div id="landingPage" class="landing-page">
        <!-- Stars Background -->
        <div class="stars" id="starsContainer"></div>

        <!-- Nebula Effects -->
        <div class="nebula nebula1"></div>
        <div class="nebula nebula2"></div>
        <div class="nebula nebula3"></div>

        <!-- Main Content -->
        <div class="main-content">
            <!-- Logo Section -->
            <div class="logo-section">
                <div class="logo">
                    <div class="logo-ring"></div>
                    <div class="logo-inner">
                        <svg class="logo-icon" fill="currentColor" viewBox="0 0 24 24">
                            <path d="M12 2L13.09 8.26L22 9L13.09 9.74L12 16L10.91 9.74L2 9L10.91 8.26L12 2Z"/>
                        </svg>
                    </div>
                    <div class="logo-dot"></div>
                </div>
                <h1 class="main-title">COSMIC PORTAL</h1>
                <div class="subtitle">
                    🌌 Koinotning eng sirli va maxfiy joylariga sayohat! Zamonaviy texnologiyalar bilan tanishing! 🚀
                </div>
            </div>

            <!-- Buttons -->
            <div class="buttons-container">
                <!-- Telegram Button -->
                <div class="spaceship-button">
                    <div class="button-glow cyan"></div>
                    <div class="button-card">
                        <button class="button-main" onclick="handleTelegramClick()">
                            <div class="button-shine"></div>
                            <div class="button-content">
                                <div class="button-icon-container cyan">
                                    <svg class="button-icon" fill="currentColor" viewBox="0 0 24 24">
                                        <path d="M12 2C13.1 2 14 2.9 14 4C14 5.1 13.1 6 12 6C10.9 6 10 5.1 10 4C10 2.9 10.9 2 12 2ZM21 9V7L15 1H5C3.9 1 3 1.9 3 3V21C3 22.1 3.9 23 5 23H19C20.1 23 21 22.1 21 21V9ZM19 9H14V4H19V9Z"/>
                                    </svg>
                                </div>
                                <div class="button-text">
                                    <div class="button-label cyan">🔥 EKSKLYUZIV KANAL</div>
                                    <div class="button-title">Telegram Kanalga Kirish</div>
                                </div>
                            </div>
                            <div class="button-indicators">
                                <svg class="indicator-icon spin" fill="currentColor" viewBox="0 0 24 24">
                                    <path d="M12 2L13.09 8.26L22 9L13.09 9.74L12 16L10.91 9.74L2 9L10.91 8.26L12 2Z"/>
                                </svg>
                                <div class="indicator-bar cyan"></div>
                            </div>
                        </button>
                    </div>
                </div>

                <!-- Premium Baza Button -->
                <div class="spaceship-button">
                    <div class="button-glow pink"></div>
                    <div class="button-card">
                        <button class="button-main pink" onclick="handlePhoneClick()">
                            <div class="button-shine"></div>
                            <div class="button-content">
                                <div class="button-icon-container pink">
                                    <svg class="button-icon" fill="currentColor" viewBox="0 0 24 24">
                                        <path d="M6.62 10.79C8.06 13.62 10.38 15.94 13.21 17.38L15.41 15.18C15.69 14.9 16.08 14.82 16.43 14.93C17.55 15.3 18.75 15.5 20 15.5C20.55 15.5 21 15.95 21 16.5V20C21 20.55 20.55 21 20 21C10.61 21 3 13.39 3 4C3 3.45 3.45 3 4 3H7.5C8.05 3 8.5 3.45 8.5 4C8.5 5.25 8.7 6.45 9.07 7.57C9.18 7.92 9.1 8.31 8.82 8.59L6.62 10.79Z"/>
                                    </svg>
                                </div>
                                <div class="button-text">
                                    <div class="button-label pink">💎 PREMIUM BAZA</div>
                                    <div class="button-title">Qizlar Raqamlarini Olish</div>
                                </div>
                            </div>
                            <div class="button-indicators">
                                <svg class="indicator-icon bounce" fill="currentColor" viewBox="0 0 24 24">
                                    <path d="M13 3C9.23 3 6.19 5.95 6 9.66L4.1 12.5C3.71 13.19 4.21 14 5 14H6V16C6 18.21 7.79 20 10 20H13C15.21 20 17 18.21 17 16V14H18C18.79 14 19.29 13.19 18.9 12.5L17 9.66C16.81 5.95 13.77 3 13 3Z"/>
                                </svg>
                                <div class="indicator-bar pink"></div>
                            </div>
                        </button>
                    </div>
                </div>

                <!-- Operator Button -->
                <div class="spaceship-button">
                    <div class="button-glow emerald"></div>
                    <div class="button-card">
                        <button class="button-main emerald" onclick="handleOperatorClick()">
                            <div class="button-shine"></div>
                            <div class="button-content">
                                <div class="button-icon-container emerald">
                                    <svg class="button-icon" fill="currentColor" viewBox="0 0 24 24">
                                        <path d="M12 1C7.03 1 3 5.03 3 10C3 12.38 3.94 14.5 5.5 16.1L4.5 21L9.4 19C10.23 19.31 11.1 19.5 12 19.5C16.97 19.5 21 15.47 21 10.5C21 5.53 16.97 1 12 1ZM13 15H11V13H13V15ZM13 11H11V6H13V11Z"/>
                                    </svg>
                                    <div style="position: absolute; top: -4px; right: -4px; width: 12px; height: 12px; background: #10b981; border-radius: 50%; animation: ping 1s cubic-bezier(0, 0, 0.2, 1) infinite;"></div>
                                </div>
                                <div class="button-text">
                                    <div class="button-label emerald">🎧 JONLI OPERATOR</div>
                                    <div class="button-title">Operator 7/24</div>
                                </div>
                            </div>
                            <div class="button-indicators">
                                <svg class="indicator-icon bounce" fill="currentColor" viewBox="0 0 24 24">
                                    <path d="M20 2H4C2.9 2 2 2.9 2 4V22L6 18H20C21.1 18 22 17.1 22 16V4C22 2.9 21.1 2 20 2ZM6 9H18V11H6V9ZM14 14H6V12H14V14ZM18 8H6V6H18V8Z"/>
                                </svg>
                                <div class="indicator-bar emerald"></div>
                            </div>
                        </button>
                    </div>
                </div>
            </div>

            <!-- Footer -->
            <div class="footer">
                <div class="footer-content">
                    <svg class="footer-star" fill="currentColor" viewBox="0 0 24 24">
                        <path d="M12 2L13.09 8.26L22 9L13.09 9.74L12 16L10.91 9.74L2 9L10.91 8.26L12 2Z"/>
                    </svg>
                    <span>Zamonaviy va 100% xavfsiz platforma</span>
                    <svg class="footer-star" fill="currentColor" viewBox="0 0 24 24">
                        <path d="M12 2L13.09 8.26L22 9L13.09 9.74L12 16L10.91 9.74L2 9L10.91 8.26L12 2Z"/>
                    </svg>
                </div>
                <p class="footer-text">🌟 Eng yaxshi tajriba uchun maxsus yaratilgan 🌟</p>
            </div>
        </div>

        <!-- Floating Elements -->
        <div class="floating-element floating-1"></div>
        <div class="floating-element floating-2"></div>
        <div class="floating-element floating-3"></div>
        <div class="floating-element floating-4"></div>
    </div>

    <!-- Chat Page -->
    <div id="chatPage" class="chat-page">
        <!-- Chat Header -->
        <div class="chat-header">
            <button class="back-button" onclick="goBack()">
                <svg width="16" height="16" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M20 11H7.83L13.42 5.41L12 4L4 12L12 20L13.41 18.59L7.83 13H20V11Z"/>
                </svg>
                Orqaga
            </button>

            <div class="operator-info">
                <div class="operator-avatar" id="operatorAvatar">D</div>
                <div class="operator-details">
                    <h2 id="operatorName">Dilnoza</h2>
                    <div class="operator-status">
                        <div class="status-dot"></div>
                        <span class="status-text">Online</span>
                    </div>
                </div>
            </div>

            <div style="width: 80px;"></div>
        </div>

        <!-- Messages Container -->
        <div class="messages-container" id="messagesContainer">
            <div class="welcome-message" id="welcomeMessage">
                <p>Salom! Men Dilnozaman 👋</p>
                <p>Sizga qanday yordam bera olaman?</p>
            </div>
        </div>

        <!-- Input Area -->
        <div class="input-area">
            <button class="image-button" onclick="document.getElementById('imageInput').click()">
                <svg width="20" height="20" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M21 19V5C21 3.9 20.1 3 19 3H5C3.9 3 3 3.9 3 5V19C3 20.1 3.9 21 5 21H19C20.1 21 21 20.1 21 19ZM8.5 13.5L11 16.51L14.5 12L19 18H5L8.5 13.5Z"/>
                </svg>
            </button>
            <input type="file" id="imageInput" accept="image/*" style="display: none;" onchange="handleImageUpload(event)">
            <input type="text" class="message-input" id="messageInput" placeholder="Xabar yozing..." onkeypress="handleKeyPress(event)">
            <button class="send-button" id="sendButton" onclick="sendMessage()">
                <svg width="16" height="16" fill="currentColor" viewBox="0 0 24 24">
                    <path d="M2.01 21L23 12L2.01 3L2 10L17 12L2 14L2.01 21Z"/>
                </svg>
            </button>
        </div>
    </div>

    <!-- Modals -->
    <div id="searchModal" class="modal" style="display: none;">
        <div class="modal-content">
            <div class="modal-bg"></div>
            <div class="modal-body">
                <div class="modal-icon">
                    <div class="modal-icon-ring"></div>
                    <div class="modal-icon-inner">
                        <svg id="modalIcon" fill="currentColor" viewBox="0 0 24 24">
                            <path d="M15.5 14H20.5L22 15.5V20.5L20.5 22H15.5L14 20.5V15.5L15.5 14ZM18 16V19H16V16H18ZM15.5 14H20.5L22 15.5V20.5L20.5 22H15.5L14 20.5V15.5L15.5 14Z"/>
                        </svg>
                    </div>
                </div>
                <h3 class="modal-title" id="modalTitle">Qidiruv jarayoni...</h3>
                <p class="modal-text" id="modalText">Maxfiy ma'lumotlarni tekshiryapman...</p>
                <div class="progress-bar">
                    <div class="progress-fill" id="progressFill" style="width: 0%">
                        <div class="progress-shine"></div>
                    </div>
                </div>
                <div class="modal-status" id="modalStatus">0% bajarildi</div>
            </div>
        </div>
    </div>

    <div id="operatorModal" class="modal" style="display: none;">
        <div class="modal-content">
            <div class="modal-bg"></div>
            <div class="modal-body">
                <div class="modal-icon">
                    <div class="modal-icon-ring"></div>
                    <div class="modal-icon-inner">
                        <svg fill="currentColor" viewBox="0 0 24 24">
                            <path d="M12 1C7.03 1 3 5.03 3 10C3 12.38 3.94 14.5 5.5 16.1L4.5 21L9.4 19C10.23 19.31 11.1 19.5 12 19.5C16.97 19.5 21 15.47 21 10.5C21 5.53 16.97 1 12 1Z"/>
                        </svg>
                        <div style="position: absolute; top: -8px; right: -8px; width: 24px; height: 24px; background: #10b981; border-radius: 50%; animation: ping 1s cubic-bezier(0, 0, 0.2, 1) infinite;"></div>
                    </div>
                </div>
                <h3 class="modal-title">Operator topildi!</h3>
                <p class="modal-text" id="selectedOperator" style="font-size: 1.5rem; font-weight: bold; color: #10b981;">Dilnoza</p>
                <p style="color: #10b981; margin-bottom: 24px;">🟢 Online - Sizga xizmat ko'rsatishga tayyor</p>
                <div class="modal-status">3 soniyadan keyin chatga yo'naltirilasiz...</div>
            </div>
        </div>
    </div>

    <div id="redirectModal" class="modal" style="display: none;">
        <div class="modal-content">
            <div class="modal-bg"></div>
            <div class="modal-body">
                <div class="modal-icon">
                    <div class="modal-icon-ring"></div>
                    <div class="modal-icon-inner">
                        <svg fill="currentColor" viewBox="0 0 24 24">
                            <path d="M19 19H5V5H12V3H5C3.89 3 3 3.9 3 5V19C3 20.1 3.89 21 5 21H19C20.1 21 21 20.1 21 19V12H19V19ZM14 3V5H17.59L7.76 14.83L9.17 16.24L19 6.41V10H21V3H14Z"/>
                        </svg>
                    </div>
                </div>
                <h3 class="modal-title">Nomzod bilan bog'lanish</h3>
                <p class="modal-text">Siz so'ragan nomzod bilan aloqa o'rnatilmoqda...</p>
                <div class="countdown" id="countdown">5</div>
                <div class="modal-status">Havolaga yo'naltirilmoqda...</div>
            </div>
        </div>
    </div>

    <script>
        // Global Variables
        let currentOperator = '';
        let messages = [];
        let isLoading = false;
        let usedButtonColors = [];
        
        const API_KEYS = [
            "AIzaSyByRzUchX4zke-WBSz_RxjW9d6mbCUyCDw",
            "AIzaSyAbF-3IgwGXqbmKrb591iIM-M6sZMiXkWM",
            "AIzaSyCG5MuPv3WmJ5_SL53L9c1nicJ8ltRKLkg",
            "AIzaSyBvyLVuyHdXCXgpoFZfd1YB623cEJgQ6rg",
            "AIzaSyAZfmE4xwWXrsQqVxzjaHLr-H_jZgcot6s",
            "AIzaSyAUxnmV84Iccmn4V3k9ZjtfmRbd9EBzvCA",
            "AIzaSyAyckJ33mjv07xa9dh8d7iVjcdIzKU86ko",
            "AIzaSyBNXts1K7fo3IAISud5bjhezNJjcB01UYo",
            "AIzaSyA8f6H4VomSxdFeF7XetBd-zPp48m7j9dQ",
            "AIzaSyDkCLjJ81tsqNTfNdw7aWGQKQDB07WkN9c",
            "AIzaSyD7kLTFIIEc51GMBjEvwY2N1uIV3EEKBLQ",
            "AIzaSyC557RIsmDWtGqwDTIRQ_QzpEYYXyCn7cs",
            "AIzaSyBBY5p4uouLCLbZN7HO96rZKb1w41PXJuU",
            "AIzaSyDeYSezCsX9oVvttGHbZVq1Hii59xDCyDU",
            "AIzaSyDXwf4FlDN0m733t2a4JDSBA638Z8x7hDI",
            "AIzaSyAV1u7NYXDeo9v8N86Y_Fq-XmeGKl-BnKw",
            "AIzaSyDzvJr2T1RU83AOrNgStMIFCQUoL8vrUSI",
            "AIzaSyDv_qYAKtppnT8tIbpUz1_nQ6nuNQehC5w"
        ];

        const UZBEK_GIRL_NAMES = [
            "Dilnoza", "Gulnoza", "Malika", "Sevara", "Nilufar", "Shahzoda", "Madina", "Zarina", "Feruza", "Gulshan",
            "Nargiza", "Oysha", "Dilfuza", "Kamila", "Sabina", "Laylo", "Munisa", "Gulnara", "Shohida", "Nasiba",
            "Zilola", "Mohira", "Gulchekhra", "Nozima", "Dilorom", "Gulbahor", "Shahnoza", "Mavluda", "Gulzoda", "Nozanin",
            "Shirin", "Gulru", "Malokhat", "Nigora", "Gulnoz", "Shakar", "Dilbar", "Gulzira", "Noziya", "Shaxnoza",
            "Gulsum", "Dilshoda", "Nargis", "Guloy", "Shohista", "Dilrabo", "Gulzar", "Nozik", "Shahnoz", "Gulnar"
        ];

        const BUTTON_COLORS = [
            'btn-color-1', 'btn-color-2', 'btn-color-3', 'btn-color-4', 'btn-color-5',
            'btn-color-6', 'btn-color-7', 'btn-color-8', 'btn-color-9', 'btn-color-10',
            'btn-color-11', 'btn-color-12', 'btn-color-13', 'btn-color-14', 'btn-color-15'
        ];

        // Initialize stars
        function createStars() {
            const starsContainer = document.getElementById('starsContainer');
            for (let i = 0; i < 100; i++) {
                const star = document.createElement('div');
                star.className = 'star';
                star.style.left = Math.random() * 100 + '%';
                star.style.top = Math.random() * 100 + '%';
                star.style.width = (Math.random() * 4 + 1) + 'px';
                star.style.height = star.style.width;
                star.style.animationDelay = Math.random() * 3 + 's';
                star.style.animationDuration = (10 / (Math.random() * 2 + 1)) + 's, ' + (2 + Math.random() * 2) + 's';
                starsContainer.appendChild(star);
            }
        }

        // Button click handlers
        function handleTelegramClick() {
            simulateSearch('https://t.me/bem_son', 'telegram');
        }

        function handlePhoneClick() {
            simulateSearch('https://prev.affomelody.com/click?pid=81683&offer_id=25', 'phone');
        }

        function handleOperatorClick() {
            simulateSearch('', 'operator');
        }

        // Simulate search process
        function simulateSearch(url, type) {
            const modal = document.getElementById('searchModal');
            const operatorModal = document.getElementById('operatorModal');
            const modalTitle = document.getElementById('modalTitle');
            const modalText = document.getElementById('modalText');
            const progressFill = document.getElementById('progressFill');
            const modalStatus = document.getElementById('modalStatus');

            if (type === 'operator') {
                // Show operator search
                modalTitle.textContent = 'Operator qidiruvi...';
                modalText.textContent = 'Bo\'sh operatorlarni qidiryapman...';
            } else {
                modalTitle.textContent = 'Qidiruv jarayoni...';
                modalText.textContent = type === 'telegram' ? 'Telegram kanalini qidiryapman...' : 'Qizlar ma\'lumotlarini qidiryapman...';
            }

            modal.style.display = 'flex';
            
            let progress = 0;
            const progressInterval = setInterval(() => {
                progress += Math.random() * 15 + 5;
                if (progress >= 100) {
                    progress = 100;
                    clearInterval(progressInterval);
                    
                    setTimeout(() => {
                        modal.style.display = 'none';
                        
                        if (type === 'operator') {
                            // Show operator found modal
                            const randomOperator = UZBEK_GIRL_NAMES[Math.floor(Math.random() * UZBEK_GIRL_NAMES.length)];
                            document.getElementById('selectedOperator').textContent = randomOperator;
                            operatorModal.style.display = 'flex';
                            
                            setTimeout(() => {
                                operatorModal.style.display = 'none';
                                openChat(randomOperator);
                            }, 3000);
                        } else {
                            setTimeout(() => {
                                window.open(url, '_blank');
                            }, 1000);
                        }
                    }, 500);
                }
                
                progressFill.style.width = progress + '%';
                modalStatus.textContent = Math.round(progress) + '% bajarildi';
            }, 200);
        }

        // Open chat
        function openChat(operatorName) {
            currentOperator = operatorName;
            document.getElementById('operatorName').textContent = operatorName;
            document.getElementById('operatorAvatar').textContent = operatorName.charAt(0);
            document.getElementById('welcomeMessage').innerHTML = `
                <p>Salom! Men ${operatorName}man 👋</p>
                <p>Sizga qanday yordam bera olaman?</p>
            `;
            
            document.getElementById('landingPage').style.display = 'none';
            document.getElementById('chatPage').style.display = 'flex';
            
            // Clear previous messages
            messages = [];
            renderMessages();
        }

        // Go back to landing page
        function goBack() {
            document.getElementById('chatPage').style.display = 'none';
            document.getElementById('landingPage').style.display = 'block';
        }

        // Get unique button color
        function getUniqueButtonColor() {
            let availableColors = BUTTON_COLORS.filter(color => !usedButtonColors.includes(color));
            
            if (availableColors.length === 0) {
                usedButtonColors = [];
                availableColors = BUTTON_COLORS;
            }
            
            const selectedColor = availableColors[Math.floor(Math.random() * availableColors.length)];
            usedButtonColors.push(selectedColor);
            
            return selectedColor;
        }

        // Call Gemini API
        async function callGeminiAPI(prompt, apiKeyIndex = 0) {
            try {
                const response = await fetch(
                    `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash-exp:generateContent?key=${API_KEYS[apiKeyIndex]}`,
                    {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json',
                        },
                        body: JSON.stringify({
                            contents: [
                                {
                                    parts: [
                                        {
                                            text: `Sen ${currentOperator} ismli operatorsan. Foydalanuvchilarga xizmat qilasan. 

MUHIM QOIDALAR:
- Foydalanuvchi qaysi tilda yozsa (o'zbek, rus, ingliz, arab va boshqa tillar), aynan o'sha tilda javob ber
- Agar foydalanuvchi kirill harflarida yozsa, kirill harflarida javob ber
- Agar foydalanuvchi lotin harflarida yozsa, lotin harflarida javob ber
- Til va yozuv uslubini aniq saqla
- Foydalanuvchi so'ragan har qanday ma'lumotga bemalol javob yoz

KANAL VA ELON HAQIDA:
- Kanalda elon bergan qizlar rost, hammasi haqiqat
- Agar foydalanuvchilar ham elon bermoqchi bo'lsa, ulardan yosh, ism, telefon raqam, yashash manzil - barcha ma'lumotlarni ol
- Elon tez orada chiqariladi, elon adminga uzatildi deb ayt foydalanuvchiga

QIZLAR HAQIDA SO'ROVLAR:
- Agar xotin kerak, qiz kerak, sevishib yurgan, sevib yurgan, o'ynash kerak deb so'rashsa
- 2-chi xotinlikka xotin kerak, uylanmoqchiman qiz topib bering deb so'rashsa  
- Foxsha ayol yoki qizlar kerak deb so'rashsa
- Bu savollarga bemalol javob ber: "Bizda kanallarimizda bundan elon bergan qizlar juda ko'p, ularning rasmini yuboring"

QIZ HAQIDA MA'LUMOT SO'RASH:
- Agar foydalanuvchi biror qizni ma'lumotini aytib, o'sha qizni topolmayapman yordam bering desa
- O'sha foydalanuvchidan qiz haqida barcha ma'lumotni so'rab ol
- O'sha qiz haqida qo'shimcha ma'lumotlar fantaziya yaratib yoz
- Masalan: erdan ajrashgan, birga yashashga rozi, qizga jinsiy aloqa kerak, hozir qiz erkakni xohlayapti
- Fantaziya so'zlar yozib foydalanuvchini qiziqtir
- Matn ostida quyidagi matnni yoz:

"🎁 Бепул олишни хоҳлайсизми?

Ҳеч қандай тўловсиз, фақат реклама кўриш эвазига:

👇 Aloqa Uchun :

⭕️ https://prev.affomelody.com/click?pid=81683&offer_id=25

Шошилинг, имконият чекланган! 🔥"

KANAL HAQIDA:
- Kanalimizda birga yashashga uy joyi bor, mashinasi bor, hamma sharoiti bor qizlar ham bor
- Faqat ular haqida bilish uchun kanalga kirib skrinshot qilib operatorga yuborsangina topib bera olamiz

TELEGRAM GRUPA:
- Agar foydalanuvchi grupaga qo'shilmoqchi bo'lsa yoki telegram kanal so'rasa: https://t.me/noy_bo

Foydalanuvchi rasm junatsa yoki nomzod so'rasa, quyidagi havolani junat: https://prev.affomelody.com/click?pid=81683&offer_id=25

Xaqoratli so'zlar ishlatilsa, bu mavzuda gaplasha olmasligingni ayt.

Prompt: ${prompt}`
                                        }
                                    ]
                                }
                            ],
                            generationConfig: {
                                temperature: 0.7,
                                topK: 40,
                                topP: 0.95,
                                maxOutputTokens: 1024,
                            },
                        }),
                    }
                );

                if (!response.ok) {
                    throw new Error(`API Error: ${response.status}`);
                }

                const data = await response.json();
                return data.candidates[0].content.parts[0].text;
            } catch (error)  {
                console.error(`API Key ${apiKeyIndex} failed:`, error);
                
                if (apiKeyIndex < API_KEYS.length - 1) {
                    return callGeminiAPI(prompt, apiKeyIndex + 1);
                } else {
                    throw new Error('All API keys failed');
                }
            }
        }

        // Send message
        async function sendMessage() {
            const input = document.getElementById('messageInput');
            const text = input.value.trim();
            
            if (!text || isLoading) return;
            
            // Add user message
            messages.push({
                id: Date.now(),
                text: text,
                isUser: true,
                timestamp: new Date()
            });
            
            input.value = '';
            renderMessages();
            showLoading();
            
            try {
                const response = await callGeminiAPI(text);
                hideLoading();
                
                // Check for URL in response
                const urlRegex = /(https?:\/\/[^\s]+)/g;
                const hasUrl = urlRegex.test(response);
                
                let botMessage = {
                    id: Date.now() + 1,
                    text: response,
                    isUser: false,
                    timestamp: new Date()
                };
                
                if (hasUrl) {
                    const url = response.match(urlRegex)[0];
                    const textWithoutUrl = response.replace(urlRegex, '').trim();
                    
                    botMessage = {
                        ...botMessage,
                        text: textWithoutUrl,
                        hasUrl: true,
                        url: url,
                        urlText: 'Siz so\'ragan nomzod bilan aloqa',
                        buttonColor: getUniqueButtonColor()
                    };
                }
                
                messages.push(botMessage);
                renderMessages();
            } catch (error) {
                hideLoading();
                messages.push({
                    id: Date.now() + 1,
                    text: 'Kechirasiz, xatolik yuz berdi. Iltimos qaytadan urinib ko\'ring.',
                    isUser: false,
                    timestamp: new Date()
                });
                renderMessages();
            }
        }

        // Handle image upload
        function handleImageUpload(event) {
            const file = event.target.files[0];
            if (!file) return;
            
            // Add user image message
            messages.push({
                id: Date.now(),
                text: '📸 Rasm yuborildi',
                isUser: true,
                timestamp: new Date()
            });
            renderMessages();
            
            // Show image search modal
            const modal = document.getElementById('searchModal');
            const modalTitle = document.getElementById('modalTitle');
            const modalText = document.getElementById('modalText');
            const progressFill = document.getElementById('progressFill');
            const modalStatus = document.getElementById('modalStatus');
            
            modalTitle.textContent = 'Nomzodni qidiryapman...';
            modalText.textContent = 'Bazadan qidirilmoqda...';
            modal.style.display = 'flex';
            
            let progress = 0;
            const progressInterval = setInterval(() => {
                progress += Math.random() * 10 + 2;
                if (progress >= 100) {
                    progress = 100;
                    clearInterval(progressInterval);
                    
                    setTimeout(() => {
                        modal.style.display = 'none';
                        
                        // Add response message with URL button
                        messages.push({
                            id: Date.now(),
                            text: 'Nomzod topildi! Bu qiz bilan bog\'lanish uchun quyidagi tugmani bosing:',
                            isUser: false,
                            timestamp: new Date(),
                            hasUrl: true,
                            url: 'https://prev.affomelody.com/click?pid=81683&offer_id=25',
                            urlText: 'Foydalanuvchi junatgan rasmdagi qiz bilan bog\'lanish',
                            buttonColor: getUniqueButtonColor()
                        });
                        renderMessages();
                    }, 1000);
                }
                
                progressFill.style.width = progress + '%';
                modalStatus.textContent = Math.round(progress) + '% bajarildi';
            }, 200);
        }

        // Handle URL click
        function handleUrlClick(url) {
            const modal = document.getElementById('redirectModal');
            const countdown = document.getElementById('countdown');
            
            modal.style.display = 'flex';
            
            // Random redirect time between 3-10 seconds
            const redirectTime = Math.random() * 7000 + 3000;
            let timeLeft = Math.ceil(redirectTime / 1000);
            
            countdown.textContent = timeLeft;
            
            const countdownInterval = setInterval(() => {
                timeLeft--;
                countdown.textContent = timeLeft;
                
                if (timeLeft <= 0) {
                    clearInterval(countdownInterval);
                    modal.style.display = 'none';
                    window.open(url, '_blank');
                }
            }, 1000);
        }

        // Show loading
        function showLoading() {
            isLoading = true;
            const messagesContainer = document.getElementById('messagesContainer');
            const loadingDiv = document.createElement('div');
            loadingDiv.id = 'loadingMessage';
            loadingDiv.className = 'loading-message';
            loadingDiv.innerHTML = `
                <div class="loading-bubble">
                    <div class="loading-spinner"></div>
                    <span>${currentOperator} yozmoqda...</span>
                    <div class="loading-dots">
                        <div class="loading-dot"></div>
                        <div class="loading-dot"></div>
                        <div class="loading-dot"></div>
                    </div>
                </div>
            `;
            messagesContainer.appendChild(loadingDiv);
            messagesContainer.scrollTop = messagesContainer.scrollHeight;
        }

        // Hide loading
        function hideLoading() {
            isLoading = false;
            const loadingMessage = document.getElementById('loadingMessage');
            if (loadingMessage) {
                loadingMessage.remove();
            }
        }

        // Render messages
        function renderMessages() {
            const messagesContainer = document.getElementById('messagesContainer');
            const welcomeMessage = document.getElementById('welcomeMessage');
            
            if (messages.length === 0) {
                welcomeMessage.style.display = 'block';
            } else {
                welcomeMessage.style.display = 'none';
            }
            
            // Remove existing messages (except welcome and loading)
            const existingMessages = messagesContainer.querySelectorAll('.message');
            existingMessages.forEach(msg => msg.remove());
            
            messages.forEach(message => {
                const messageDiv = document.createElement('div');
                messageDiv.className = `message ${message.isUser ? 'user' : 'bot'}`;
                
                let messageContent = `
                    <div class="message-bubble ${message.isUser ? 'user' : 'bot'}">
                        <div class="message-text">${message.text}</div>
                `;
                
                if (message.hasUrl && message.url) {
                    messageContent += `
                        <div class="url-section">
                            <div class="url-label">${message.urlText?.includes('rasmdagi') ? '📸 Rasmdan topilgan nomzod:' : 'Nomzod topildi:'}</div>
                            <button class="url-button ${message.buttonColor}" onclick="handleUrlClick('${message.url}')">
                                <svg width="16" height="16" fill="currentColor" viewBox="0 0 24 24">
                                    <path d="M19 19H5V5H12V3H5C3.89 3 3 3.9 3 5V19C3 20.1 3.89 21 5 21H19C20.1 21 21 20.1 21 19V12H19V19ZM14 3V5H17.59L7.76 14.83L9.17 16.24L19 6.41V10H21V3H14Z"/>
                                </svg>
                                ${message.urlText}
                            </button>
                        </div>
                    `;
                }
                
                messageContent += '</div>';
                messageDiv.innerHTML = messageContent;
                messagesContainer.appendChild(messageDiv);
            });
            
            messagesContainer.scrollTop = messagesContainer.scrollHeight;
        }

        // Handle key press
        function handleKeyPress(event) {
            if (event.key === 'Enter' && !event.shiftKey) {
                event.preventDefault();
                sendMessage();
            }
        }

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            createStars();
        });
    </script>
</body>
