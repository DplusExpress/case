<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบติดตามลูกค้า</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(45deg, #4CAF50, #45a049);
            color: white;
            padding: 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 15px;
        }

        .header-left h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 15px;
            background: rgba(255,255,255,0.1);
            padding: 10px 20px;
            border-radius: 25px;
        }

        .user-avatar {
            width: 40px;
            height: 40px;
            background: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            color: #4CAF50;
            font-size: 1.2em;
        }

        .auth-container {
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 60vh;
            padding: 40px;
        }

        .auth-form {
            background: white;
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 400px;
            text-align: center;
        }

        .auth-form h2 {
            color: #333;
            margin-bottom: 30px;
            font-size: 2em;
        }

        .auth-tabs {
            display: flex;
            margin-bottom: 30px;
            border-radius: 25px;
            overflow: hidden;
            background: #f0f0f0;
        }

        .auth-tab {
            flex: 1;
            padding: 12px;
            background: transparent;
            border: none;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s;
            color: #666;
        }

        .auth-tab.active {
            background: #4CAF50;
            color: white;
        }

        .main-content {
            padding: 30px;
        }

        .form-section {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 10px;
            margin-bottom: 30px;
            border-left: 5px solid #4CAF50;
        }

        .form-section h2 {
            color: #333;
            margin-bottom: 20px;
            font-size: 1.5em;
        }

        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }

        .form-group {
            display: flex;
            flex-direction: column;
        }

        .form-group label {
            font-weight: 600;
            margin-bottom: 8px;
            color: #555;
        }

        .form-group input,
        .form-group select,
        .form-group textarea {
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s ease;
        }

        .form-group input:focus,
        .form-group select:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: #4CAF50;
            box-shadow: 0 0 0 3px rgba(76, 175, 80, 0.1);
        }

        .form-group textarea {
            resize: vertical;
            min-height: 80px;
        }

        .error-message {
            color: #dc3545;
            font-size: 14px;
            margin-top: 5px;
        }

        .success-message {
            color: #28a745;
            font-size: 14px;
            margin-top: 5px;
        }

        .btn {
            background: linear-gradient(45deg, #4CAF50, #45a049);
            color: white;
            padding: 12px 30px;
            border: none;
            border-radius: 25px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
            width: 100%;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(76, 175, 80, 0.4);
        }

        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .btn-logout {
            background: #dc3545;
            padding: 8px 20px;
            font-size: 14px;
            width: auto;
        }

        .btn-logout:hover {
            background: #c82333;
            box-shadow: 0 5px 15px rgba(220, 53, 69, 0.4);
        }

        .filters {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
            align-items: center;
            flex-wrap: wrap;
        }

        .filters label {
            font-weight: 600;
            color: #555;
        }

        .filters select,
        .filters input {
            padding: 8px 15px;
            border: 2px solid #ddd;
            border-radius: 20px;
            background: white;
        }

        .customer-list {
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .customer-item {
            border-bottom: 1px solid #eee;
            padding: 20px;
            transition: background-color 0.3s ease;
        }

        .customer-item:hover {
            background: #f8f9fa;
        }

        .customer-item:last-child {
            border-bottom: none;
        }

        .customer-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
            flex-wrap: wrap;
            gap: 10px;
        }

        .customer-name {
            font-size: 1.2em;
            font-weight: 600;
            color: #333;
        }

        .customer-date {
            color: #666;
            font-size: 0.9em;
        }

        .customer-details {
            margin: 10px 0;
            color: #555;
        }

        .customer-meta {
            background: #f0f0f0;
            padding: 10px;
            border-radius: 8px;
            margin: 10px 0;
            font-size: 0.9em;
            color: #666;
            border-left: 3px solid #4CAF50;
        }

        .customer-actions {
            display: flex;
            gap: 10px;
            margin-top: 15px;
            flex-wrap: wrap;
        }

        .status-badge {
            padding: 6px 15px;
            border-radius: 20px;
            font-size: 0.9em;
            font-weight: 600;
            text-align: center;
            min-width: 100px;
        }

        .status-completed {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .status-waiting {
            background: #fff3cd;
            color: #856404;
            border: 1px solid #ffeaa7;
        }

        .status-followup {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .btn-small {
            padding: 6px 15px;
            font-size: 14px;
            border-radius: 15px;
            width: auto;
        }

        .btn-edit {
            background: #17a2b8;
        }

        .btn-edit:hover {
            background: #138496;
        }

        .btn-delete {
            background: #dc3545;
        }

        .btn-delete:hover {
            background: #c82333;
        }

        .empty-state {
            text-align: center;
            padding: 40px;
            color: #666;
        }

        .empty-state i {
            font-size: 4em;
            margin-bottom: 20px;
            opacity: 0.3;
        }

        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            border-top: 4px solid #4CAF50;
        }

        .stat-number {
            font-size: 2em;
            font-weight: bold;
            color: #4CAF50;
        }

        .stat-label {
            color: #666;
            margin-top: 5px;
        }

        .hidden {
            display: none;
        }

        .password-strength {
            margin-top: 5px;
            font-size: 12px;
        }

        .strength-weak { color: #dc3545; }
        .strength-medium { color: #ffc107; }
        .strength-strong { color: #28a745; }

        @media (max-width: 768px) {
            .container {
                margin: 10px;
                border-radius: 10px;
            }

            .main-content {
                padding: 20px;
            }

            .header {
                padding: 20px;
                flex-direction: column;
                text-align: center;
            }

            .header-left h1 {
                font-size: 2em;
            }

            .form-grid {
                grid-template-columns: 1fr;
            }

            .filters {
                flex-direction: column;
                align-items: stretch;
            }

            .customer-header {
                flex-direction: column;
                align-items: flex-start;
            }

            .customer-actions {
                justify-content: center;
            }
        }
    </style>
</head>
<body>
    <!-- หน้า Authentication -->
    <div id="authPage" class="container">
        <div class="header">
            <div class="header-left">
                <h1>🏢 ระบบติดตามลูกค้า</h1>
                <p>ระบบจัดการข้อมูลลูกค้าและติดตามสถานะงาน</p>
            </div>
        </div>
        <div class="auth-container">
            <div class="auth-form">
                <div class="auth-tabs">
                    <button class="auth-tab active" onclick="showLoginTab()">เข้าสู่ระบบ</button>
                    <button class="auth-tab" onclick="showRegisterTab()">สมัครสมาชิก</button>
                </div>

                <!-- Login Form -->
                <div id="loginTab">
                    <h2>🔐 เข้าสู่ระบบ</h2>
                    <form id="loginForm">
                        <div class="form-group">
                            <label for="loginUsername">ชื่อผู้ใช้</label>
                            <input type="text" id="loginUsername" required placeholder="กรอกชื่อผู้ใช้">
                        </div>
                        <div class="form-group" style="margin-bottom: 30px;">
                            <label for="loginPassword">รหัสผ่าน</label>
                            <input type="password" id="loginPassword" required placeholder="กรอกรหัสผ่าน">
                            <div id="loginError" class="error-message"></div>
                        </div>
                        <button type="submit" class="btn">เข้าสู่ระบบ</button>
                    </form>
                </div>

                <!-- Register Form -->
                <div id="registerTab" class="hidden">
                    <h2>👤 สมัครสมาชิก</h2>
                    <form id="registerForm">
                        <div class="form-group">
                            <label for="regUsername">ชื่อผู้ใช้ *</label>
                            <input type="text" id="regUsername" required placeholder="ชื่อผู้ใช้ (ภาษาอังกฤษ)">
                            <div id="usernameError" class="error-message"></div>
                        </div>
                        <div class="form-group">
                            <label for="regDisplayName">ชื่อที่แสดง *</label>
                            <input type="text" id="regDisplayName" required placeholder="ชื่อที่จะแสดงในระบบ">
                        </div>
                        <div class="form-group">
                            <label for="regEmail">อีเมล *</label>
                            <input type="email" id="regEmail" required placeholder="example@email.com">
                            <div id="emailError" class="error-message"></div>
                        </div>
                        <div class="form-group">
                            <label for="regPassword">รหัสผ่าน *</label>
                            <input type="password" id="regPassword" required placeholder="รหัสผ่าน (อย่างน้อย 6 ตัวอักษร)">
                            <div id="passwordStrength" class="password-strength"></div>
                        </div>
                        <div class="form-group" style="margin-bottom: 30px;">
                            <label for="regConfirmPassword">ยืนยันรหัสผ่าน *</label>
                            <input type="password" id="regConfirmPassword" required placeholder="ยืนยันรหัสผ่าน">
                            <div id="confirmPasswordError" class="error-message"></div>
                        </div>
                        <button type="submit" class="btn" id="registerBtn">สมัครสมาชิก</button>
                        <div id="registerSuccess" class="success-message" style="margin-top: 15px;"></div>
                    </form>
                </div>
            </div>
        </div>
    </div>

    <!-- หน้าหลัก -->
    <div id="mainPage" class="container hidden">
        <div class="header">
            <div class="header-left">
                <h1>🏢 ระบบติดตามลูกค้า</h1>
                <p>จัดการข้อมูลลูกค้าและติดตามสถานะงาน</p>
            </div>
            <div class="user-info">
                <div class="user-avatar" id="userAvatar"></div>
                <div>
                    <div style="font-weight: 600;" id="userDisplayName"></div>
                    <div style="font-size: 0.9em; opacity: 0.8;" id="userEmail"></div>
                </div>
                <button class="btn btn-logout" onclick="logout()">ออกจากระบบ</button>
            </div>
        </div>

        <div class="main-content">
            <!-- สถิติ -->
            <div class="stats">
                <div class="stat-card">
                    <div class="stat-number" id="totalCount">0</div>
                    <div class="stat-label">ลูกค้าทั้งหมด</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="completedCount">0</div>
                    <div class="stat-label">เสร็จแล้ว</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="waitingCount">0</div>
                    <div class="stat-label">รอติดตาม</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number" id="followupCount">0</div>
                    <div class="stat-label">ติดตามซ้ำ</div>
                </div>
            </div>

            <!-- ฟอร์มเพิ่มลูกค้า -->
            <div class="form-section">
                <h2>➕ เพิ่มข้อมูลลูกค้าใหม่</h2>
                <form id="customerForm">
                    <div class="form-grid">
                        <div class="form-group">
                            <label for="customerName">ชื่อลูกค้า *</label>
                            <input type="text" id="customerName" required>
                        </div>
                        <div class="form-group">
                            <label for="customerPhone">เบอร์โทร</label>
                            <input type="tel" id="customerPhone">
                        </div>
                        <div class="form-group">
                            <label for="customerEmail">อีเมล</label>
                            <input type="email" id="customerEmail">
                        </div>
                        <div class="form-group">
                            <label for="contactReason">เรื่องที่ติดต่อ *</label>
                            <input type="text" id="contactReason" required>
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="customerDetails">รายละเอียดเพิ่มเติม</label>
                        <textarea id="customerDetails" placeholder="บันทึกรายละเอียดหรือข้อมูลเพิ่มเติม..."></textarea>
                    </div>
                    <button type="submit" class="btn">เพิ่มลูกค้า</button>
                </form>
            </div>

            <!-- ฟิลเตอร์ -->
            <div class="filters">
                <label>ค้นหา:</label>
                <input type="text" id="searchInput" placeholder="ค้นหาชื่อ, เบอร์โทร, หรือเรื่องที่ติดต่อ">
                <label>สถานะ:</label>
                <select id="statusFilter">
                    <option value="all">ทั้งหมด</option>
                    <option value="waiting">รอติดตาม</option>
                    <option value="followup">ติดตามซ้ำ</option>
                    <option value="completed">เสร็จแล้ว</option>
                </select>
                <label>ผู้สร้าง:</label>
                <select id="userFilter">
                    <option value="all">ทุกคน</option>
                </select>
            </div>

            <!-- รายการลูกค้า -->
            <div class="customer-list" id="customerList">
                <div class="empty-state">
                    <div style="font-size: 4em; margin-bottom: 20px; opacity: 0.3;">📋</div>
                    <h3>ยังไม่มีข้อมูลลูกค้า</h3>
                    <p>เริ่มต้นโดยเพิ่มข้อมูลลูกค้าแรกของคุณ</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        // ตัวแปรระบบ
        let customers = [];
        let users = [];
        let currentUser = null;
        let editingId = null;

        // เมื่อโหลดหน้า
        document.addEventListener('DOMContentLoaded', function() {
            loadData();
            checkLogin();
            initializeEventListeners();
        });

        // โหลดข้อมูลจาก LocalStorage
        function loadData() {
            const savedCustomers = localStorage.getItem('customers');
            const savedUsers = localStorage.getItem('users');
            const savedCurrentUser = localStorage.getItem('currentUser');
            
            if (savedCustomers) customers = JSON.parse(savedCustomers);
            if (savedUsers) users = JSON.parse(savedUsers);
            if (savedCurrentUser) currentUser = JSON.parse(savedCurrentUser);
        }

        // บันทึกข้อมูลใน LocalStorage
        function saveData() {
            localStorage.setItem('customers', JSON.stringify(customers));
            localStorage.setItem('users', JSON.stringify(users));
            localStorage.setItem('currentUser', JSON.stringify(currentUser));
        }

        // ตรวจสอบการ login
        function checkLogin() {
            if (currentUser) {
                showMainPage();
            } else {
                showAuthPage();
            }
        }

        // แสดงหน้า Authentication
        function showAuthPage() {
            document.getElementById('authPage').classList.remove('hidden');
            document.getElementById('mainPage').classList.add('hidden');
        }

        // แสดงหน้าหลัก
        function showMainPage() {
            document.getElementById('authPage').classList.add('hidden');
            document.getElementById('mainPage').classList.remove('hidden');
            
            updateUserDisplay();
            updateUserFilter();
            renderCustomers();
            updateStats();
        }

        // Tab switching
        function showLoginTab() {
            document.getElementById('loginTab').classList.remove('hidden');
            document.getElementById('registerTab').classList.add('hidden');
            document.querySelectorAll('.auth-tab')[0].classList.add('active');
            document.querySelectorAll('.auth-tab')[1].classList.remove('active');
        }

        function showRegisterTab() {
            document.getElementById('loginTab').classList.add('hidden');
            document.getElementById('registerTab').classList.remove('hidden');
            document.querySelectorAll('.auth-tab')[0].classList.remove('active');
            document.querySelectorAll('.auth-tab')[1].classList.add('active');
        }

        // Initialize Event Listeners
        function initializeEventListeners() {
            // Login form
            document.getElementById('loginForm').addEventListener('submit', handleLogin);
            
            // Register form
            document.getElementById('registerForm').addEventListener('submit', handleRegister);
            
            // Customer form
            document.getElementById('customerForm').addEventListener('submit', handleCustomerSubmit);
            
            // Filters
            document.getElementById('statusFilter').addEventListener('change', renderCustomers);
            document.getElementById('userFilter').addEventListener('change', renderCustomers);
            document.getElementById('searchInput').addEventListener('input', renderCustomers);
            
            // Real-time validation
            document.getElementById('regUsername').addEventListener('input', validateUsername);
            document.getElementById('regEmail').addEventListener('input', validateEmail);
            document.getElementById('regPassword').addEventListener('input', checkPasswordStrength);
            document.getElementById('regConfirmPassword').addEventListener('input', validateConfirmPassword);
        }

        // Handle Login
        function handleLogin(e) {
            e.preventDefault();
            
            const username = document.getElementById('loginUsername').value.trim();
            const password = document.getElementById('loginPassword').value;
            const errorDiv = document.getElementById('loginError');
            
            // Clear previous errors
            errorDiv.textContent = '';
            
            // Find user
            const user = users.find(u => u.username === username);
            
            if (!user) {
                errorDiv.textContent = 'ไม่พบชื่อผู้ใช้นี้';
                return;
            }
            
            if (user.password !== password) {
                errorDiv.textContent = 'รหัสผ่านไม่ถูกต้อง';
                return;
            }
            
            // Login successful
            currentUser = {
                username: user.username,
                displayName: user.displayName,
                email: user.email,
                loginTime: new Date().toLocaleString('th-TH')
            };
            
            saveData();
            document.getElementById('loginForm').reset();
            showMainPage();
        }

        // Handle Register
        function handleRegister(e) {
            e.preventDefault();
            
            const username = document.getElementById('regUsername').value.trim();
            const displayName = document.getElementById('regDisplayName').value.trim();
            const email = document.getElementById('regEmail').value.trim();
            const password = document.getElementById('regPassword').value;
            const confirmPassword = document.getElementById('regConfirmPassword').value;
            
            // Validate all fields
            if (!validateUsername() || !validateEmail() || !validateConfirmPassword()) {
                return;
            }
            
            if (password.length < 6) {
                alert('รหัสผ่านต้องมีความยาวอย่างน้อย 6 ตัวอักษร');
                return;
            }
            
            // Check if user already exists
            if (users.find(u => u.username === username)) {
                document.getElementById('usernameError').textContent = 'ชื่อผู้ใช้นี้มีอยู่แล้ว';
                return;
            }
            
            if (users.find(u => u.email === email)) {
                document.getElementById('emailError').textContent = 'อีเมลนี้มีอยู่แล้ว';
                return;
            }
            
            // Create new user
            const newUser = {
                id: Date.now(),
                username: username,
                displayName: displayName,
                email: email,
                password: password,
                createdAt: new Date().toLocaleString('th-TH')
            };
            
            users.push(newUser);
            saveData();
            
            // Show success message
            document.getElementById('registerSuccess').textContent = 'สมัครสมาชิกสำเร็จ! กรุณาเข้าสู่ระบบ';
            document.getElementById('registerForm').reset();
            
            // Switch to login tab after 2 seconds
            setTimeout(() => {
                showLoginTab();
                document.getElementById('registerSuccess').textContent = '';
            }, 2000);
        }

        // Validation functions
        function validateUsername() {
            const username = document.getElementById('regUsername').value.trim();
            const errorDiv = document.getElementById('usernameError');
            
            if (username.length < 3) {
                errorDiv.textContent = 'ชื่อผู้ใช้ต้องมีอย่างน้อย 3 ตัวอักษร';
                return false;
            }
            
            if (!/^[a-zA-Z0-9_]+$/.test(username)) {
                errorDiv.textContent = 'ชื่อผู้ใช้ใช้ได้เฉพาะ a-z, A-Z, 0-9 และ _';
                return false;
            }
            
            errorDiv.textContent = '';
            return true;
        }

        function validateEmail() {
            const email = document.getElementById('regEmail').value.trim();
            const errorDiv = document.getElementById('emailError');
            
            if (!isValidEmail(email)) {
                errorDiv.textContent = 'รูปแบบอีเมลไม่ถูกต้อง';
                return false;
            }
            
            errorDiv.textContent = '';
            return true;
        }

        function checkPasswordStrength() {
            const password = document.getElementById('regPassword').value;
            const strengthDiv = document.getElementById('passwordStrength');
            
            if (password.length === 0) {
                strengthDiv.textContent = '';
                return;
            }
            
            let strength = 0;
            if (password.length >= 6) strength++;
            if (password.length >= 8) strength++;
            if (/[a-z]/.test(password)) strength++;
            if (/[A-Z]/.test(password)) strength++;
            if (/[0-9]/.test(password)) strength++;
            if (/[^A-Za-z0-9]/.test(password)) strength++;
            
            if (strength < 3) {
                strengthDiv.textContent = 'รหัสผ่านอ่อน
