<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>بوابة الدعم الفني الذكي</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;600;700&display=swap');
        
        * {
            -webkit-tap-highlight-color: transparent;
            font-family: 'Cairo', sans-serif;
        }

        body { 
            background-color: #f8fafc; 
            margin: 0;
            padding: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
        }

        .terminal-box {
            background-color: #0f172a;
            color: #4ade80;
            font-family: monospace;
            border: 1px solid #1e293b;
        }

        .action-card {
            transition: all 0.2s ease;
            border: 1px solid #f1f5f9;
        }

        .action-card:active {
            transform: scale(0.95);
            background-color: #eff6ff;
        }

        @keyframes blink {
            50% { opacity: 0; }
        }
        .cursor {
            display: inline-block;
            width: 8px;
            height: 15px;
            background: #4ade80;
            animation: blink 1s infinite;
            vertical-align: middle;
        }
    </style>
</head>
<body>

    <div id="app" class="w-full max-w-md bg-white min-h-screen sm:min-h-[700px] sm:rounded-3xl shadow-2xl overflow-hidden flex flex-col">
        
        <!-- شاشة تسجيل الدخول -->
        <div id="login-screen" class="p-8 flex-grow flex flex-col justify-center">
            <div class="text-center mb-10">
                <div class="bg-blue-600 w-24 h-24 rounded-[2rem] flex items-center justify-center mx-auto mb-6 shadow-xl shadow-blue-200">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-12 w-12 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z" />
                    </svg>
                </div>
                <h1 class="text-3xl font-bold text-gray-800 tracking-tight">بوابة الدعم الفني</h1>
                <p class="text-gray-500 mt-2">نظام التحقق والإصلاح الذكي</p>
            </div>
            
            <form id="login-form" class="space-y-6">
                <div class="space-y-1 text-right">
                    <label class="text-sm font-bold text-gray-600 mr-1">اسم المستخدم</label>
                    <input type="text" id="username" required placeholder="ادخل اسمك" 
                           class="w-full px-5 py-4 bg-gray-50 border border-gray-200 rounded-2xl focus:ring-4 focus:ring-blue-100 focus:border-blue-500 outline-none transition-all text-right">
                </div>
                <div class="space-y-1 text-right">
                    <label class="text-sm font-bold text-gray-600 mr-1">المسمى الوظيفي</label>
                    <input type="text" id="job-title" required placeholder="مثلاً: فني شبكات" 
                           class="w-full px-5 py-4 bg-gray-50 border border-gray-200 rounded-2xl focus:ring-4 focus:ring-blue-100 focus:border-blue-500 outline-none transition-all text-right">
                </div>
                <button type="submit" class="w-full bg-blue-600 text-white py-5 rounded-2xl font-bold text-lg shadow-lg shadow-blue-200 active:bg-blue-700 transition-colors">
                    دخول النظام
                </button>
            </form>
        </div>

        <!-- لوحة التحكم الرئيسية -->
        <div id="dashboard" class="hidden flex-grow flex flex-col animate-in fade-in duration-500">
            <!-- الهيدر -->
            <div class="bg-blue-600 p-6 text-white text-right flex justify-between items-center">
                <div>
                    <h2 id="display-name" class="text-xl font-bold"></h2>
                    <div id="display-title" class="text-xs opacity-80 mt-1"></div>
                </div>
                <button onclick="location.reload()" class="bg-white/20 p-2 rounded-xl">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7" />
                    </svg>
                </button>
            </div>

            <!-- محتوى العمليات -->
            <div class="p-6 flex-grow space-y-6 overflow-y-auto">
                <div class="grid grid-cols-2 gap-4">
                    <button onclick="startAction('إصلاح الشبكة', '🌐')" class="action-card flex flex-col items-center p-5 bg-white rounded-2xl shadow-sm">
                        <div class="text-3xl mb-2">🌐</div>
                        <span class="text-sm font-bold text-gray-700">الشبكة</span>
                    </button>
                    
                    <button onclick="startAction('فحص الأمان', '🛡️')" class="action-card flex flex-col items-center p-5 bg-white rounded-2xl shadow-sm">
                        <div class="text-3xl mb-2">🛡️</div>
                        <span class="text-sm font-bold text-gray-700">الأمان</span>
                    </button>

                    <button onclick="startAction('تحديث النظام', '⚙️')" class="action-card flex flex-col items-center p-5 bg-white rounded-2xl shadow-sm">
                        <div class="text-3xl mb-2">⚙️</div>
                        <span class="text-sm font-bold text-gray-700">تحديث</span>
                    </button>

                    <button onclick="startAction('نسخ احتياطي', '💾')" class="action-card flex flex-col items-center p-5 bg-white rounded-2xl shadow-sm">
                        <div class="text-3xl mb-2">💾</div>
                        <span class="text-sm font-bold text-gray-700">نسخ</span>
                    </button>
                </div>

                <!-- تيرمينال الأوامر -->
                <div class="space-y-3">
                    <div class="flex justify-between items-center text-right">
                        <h3 class="text-sm font-bold text-gray-500 mr-1 italic underline">سجل الأوامر التقني:</h3>
                    </div>
                    <div id="log-box" class="terminal-box h-48 p-4 rounded-2xl text-[11px] overflow-y-auto leading-relaxed text-right dir-ltr">
                        <div class="text-white opacity-40">> النظام متصل وجاهز...<span class="cursor"></span></div>
                    </div>
                </div>
            </div>

            <div class="p-4 text-center text-[10px] text-gray-400 border-t bg-gray-50 uppercase tracking-widest">
                Safe Support System v2.0
            </div>
        </div>
    </div>

    <script>
        const loginForm = document.getElementById('login-form');
        const loginScreen = document.getElementById('login-screen');
        const dashboard = document.getElementById('dashboard');
        const logBox = document.getElementById('log-box');

        loginForm.onsubmit = (e) => {
            e.preventDefault();
            const name = document.getElementById('username').value;
            const title = document.getElementById('job-title').value;
            
            document.getElementById('display-name').innerText = name;
            document.getElementById('display-title').innerText = title;
            
            loginScreen.classList.add('hidden');
            dashboard.classList.remove('hidden');
            addLog(`تم التحقق من هوية الفني: ${name}`, '#fff');
        };

        function addLog(msg, color = '#4ade80') {
            const time = new Date().toLocaleTimeString('ar-SA');
            const line = document.createElement('div');
            line.className = "mb-1";
            line.style.color = color;
            line.innerHTML = `<span class="opacity-30 text-gray-400">[${time}]</span> ${msg}`;
            logBox.appendChild(line);
            logBox.scrollTop = logBox.scrollHeight;
        }

        function startAction(action, icon) {
            addLog(`بدء تنفيذ ${action} ${icon}...`, '#60a5fa');
            
            setTimeout(() => {
                addLog(`جاري تحليل البروتوكولات...`);
            }, 700);

            setTimeout(() => {
                addLog(`اكتملت العملية بنجاح ✅`, '#4ade80');
            }, 2000);
        }
    </script>
</body>
</html>

```
