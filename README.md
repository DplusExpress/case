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

        .login-container {
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 60vh;
            padding: 40px;
        }

        .login-form {
            background: white;
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 400px;
            text-align: center;
        }

        .login-form h2 {
            color: #333;
            margin-bottom: 30px;
            font-size: 2em;
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

        .filters select {
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
    <!-- หน้า Login -->
    <div id="loginPage" class="container">
        <div class="header">
            <div class="header-left">
                <h1>🏢 ระบบติดตามลูกค้า</h1>
                <p>เข้าสู่ระบบเพื่อจัดการข้อมูลลูกค้า</p>
            </div>
        </div>
        <div class="login-container">
            <form class="login-form" id="loginForm">
                <h2>🔐 เข้าสู่ระบบ</h2>
                <div class="form-group">
                    <label for="username">ชื่อผู้ใช้</label>
                    <input type="text" id="username" required placeholder="กรอกชื่อผู้ใช้">
                </div>
                <div class="form-group" style="margin-bottom: 30px;">
                    <label for="displayName">ชื่อที่แสดง</label>
                    <input type="text" id="displayName" required placeholder="ชื่อที่จะแสดงในระบบ">
                </div>
                <button type="submit" class="btn">เข้าสู่ระบบ</button>
                <p style="margin-top: 20px; color: #666; font-size: 0.9em;">
                    💡 ใส่ชื่อผู้ใช้และชื่อที่แสดงเพื่อเข้าใช้งาน
                </p>
            </form>
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
                    <div style="font-size: 0.9em; opacity: 0.8;">ผู้ใช้งาน</div>
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
                            <label for="customerEmail">User</label>
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
                <label>กรองตามสถานะ:</label>
                <select id="statusFilter">
                    <option value="all">ทั้งหมด</option>
                    <option value="waiting">รอติดตาม</option>
                    <option value="followup">ติดตามซ้ำ</option>
                    <option value="completed">เสร็จแล้ว</option>
                </select>
                <label>กรองตามผู้สร้าง:</label>
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
        let currentUser = null;
        let editingId = null;

        // เมื่อโหลดหน้า
        document.addEventListener('DOMContentLoaded', function() {
            // ตรวจสอบว่ามี user login อยู่หรือไม่
            checkLogin();
        });

        // ตรวจสอบการ login
        function checkLogin() {
            // ในการใช้งานจริง อาจจะเก็บใน localStorage หรือ session
            if (currentUser) {
                showMainPage();
            } else {
                showLoginPage();
            }
        }

        // แสดงหน้า login
        function showLoginPage() {
            document.getElementById('loginPage').classList.remove('hidden');
            document.getElementById('mainPage').classList.add('hidden');
        }

        // แสดงหน้าหลัก
        function showMainPage() {
            document.getElementById('loginPage').classList.add('hidden');
            document.getElementById('mainPage').classList.remove('hidden');
            
            // อัพเดทข้อมูล user
            updateUserDisplay();
            updateUserFilter();
            renderCustomers();
            updateStats();
        }

        // Login form
        document.getElementById('loginForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const username = document.getElementById('username').value.trim();
            const displayName = document.getElementById('displayName').value.trim();
            
            if (username && displayName) {
                currentUser = {
                    username: username,
                    displayName: displayName,
                    loginTime: new Date().toLocaleString('th-TH')
                };
                
                // ล้างฟอร์ม
                this.reset();
                
                // ไปหน้าหลัก
                showMainPage();
            }
        });

        // อัพเดทการแสดงผล user
        function updateUserDisplay() {
            if (currentUser) {
                document.getElementById('userAvatar').textContent = currentUser.displayName.charAt(0).toUpperCase();
                document.getElementById('userDisplayName').textContent = currentUser.displayName;
            }
        }

        // อัพเดทฟิลเตอร์ผู้ใช้
        function updateUserFilter() {
            const userFilter = document.getElementById('userFilter');
            const users = [...new Set(customers.map(c => c.createdBy))];
            
            userFilter.innerHTML = '<option value="all">ทุกคน</option>';
            users.forEach(user => {
                userFilter.innerHTML += `<option value="${user}">${user}</option>`;
            });
        }

        // ออกจากระบบ
        function logout() {
            if (confirm('คุณต้องการออกจากระบบหรือไม่?')) {
                currentUser = null;
                showLoginPage();
            }
        }

        // ส่งฟอร์มลูกค้า
        document.getElementById('customerForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            if (!currentUser) {
                alert('กรุณาเข้าสู่ระบบก่อน');
                return;
            }
            
            const customerData = {
                id: editingId || Date.now(),
                name: document.getElementById('customerName').value,
                phone: document.getElementById('customerPhone').value,
                email: document.getElementById('customerEmail').value,
                reason: document.getElementById('contactReason').value,
                details: document.getElementById('customerDetails').value,
                status: 'waiting',
                createdBy: currentUser.displayName,
                createdAt: new Date().toLocaleString('th-TH'),
                updatedBy: currentUser.displayName,
                updatedAt: new Date().toLocaleString('th-TH')
            };

            if (editingId) {
                // แก้ไข
                const index = customers.findIndex(c => c.id === editingId);
                customers[index] = {...customers[index], ...customerData, 
                    createdBy: customers[index].createdBy, 
                    createdAt: customers[index].createdAt
                };
                editingId = null;
                document.querySelector('.btn[type="submit"]').textContent = 'เพิ่มลูกค้า';
            } else {
                // เพิ่มใหม่
                customers.push(customerData);
            }

            // ล้างฟอร์ม
            this.reset();
            
            // อัพเดท
            updateUserFilter();
            renderCustomers();
            updateStats();
        });

        // กรองข้อมูล
        document.getElementById('statusFilter').addEventListener('change', renderCustomers);
        document.getElementById('userFilter').addEventListener('change', renderCustomers);

        // แสดงรายการลูกค้า
        function renderCustomers() {
            const statusFilter = document.getElementById('statusFilter').value;
            const userFilter = document.getElementById('userFilter').value;
            
            let filteredCustomers = customers;
            
            if (statusFilter !== 'all') {
                filteredCustomers = filteredCustomers.filter(c => c.status === statusFilter);
            }
            
            if (userFilter !== 'all') {
                filteredCustomers = filteredCustomers.filter(c => c.createdBy === userFilter);
            }

            const customerList = document.getElementById('customerList');
            
            if (filteredCustomers.length === 0) {
                customerList.innerHTML = `
                    <div class="empty-state">
                        <div style="font-size: 4em; margin-bottom: 20px; opacity: 0.3;">📋</div>
                        <h3>ไม่พบข้อมูลลูกค้า</h3>
                        <p>ลองเปลี่ยนเงื่อนไขการกรองหรือเพิ่มข้อมูลใหม่</p>
                    </div>
                `;
                return;
            }

            customerList.innerHTML = filteredCustomers.map(customer => `
                <div class="customer-item">
                    <div class="customer-header">
                        <div class="customer-name">${customer.name}</div>
                        <div class="customer-date">${customer.createdAt}</div>
                    </div>
                    <div class="customer-details">
                        <strong>เรื่องที่ติดต่อ:</strong> ${customer.reason}<br>
                        ${customer.phone ? `<strong>เบอร์โทร:</strong> ${customer.phone}<br>` : ''}
                        ${customer.email ? `<strong>User:</strong> ${customer.email}<br>` : ''}
                        ${customer.details ? `<strong>รายละเอียด:</strong> ${customer.details}` : ''}
                    </div>
                    <div class="customer-meta">
                        👤 <strong>สร้างโดย:</strong> ${customer.createdBy} | 
                        📅 <strong>สร้างเมื่อ:</strong> ${customer.createdAt}
                        ${customer.updatedBy !== customer.createdBy ? `<br>✏️ <strong>แก้ไขล่าสุดโดย:</strong> ${customer.updatedBy} (${customer.updatedAt})` : ''}
                    </div>
                    <div class="customer-actions">
                        <span class="status-badge status-${customer.status}">
                            ${getStatusText(customer.status)}
                        </span>
                        <select onchange="updateStatus(${customer.id}, this.value)" style="padding: 6px 10px; border-radius: 15px; border: 2px solid #ddd;">
                            <option value="waiting" ${customer.status === 'waiting' ? 'selected' : ''}>รอติดตาม</option>
                            <option value="followup" ${customer.status === 'followup' ? 'selected' : ''}>ติดตามซ้ำ</option>
                            <option value="completed" ${customer.status === 'completed' ? 'selected' : ''}>เสร็จแล้ว</option>
                        </select>
                        <button class="btn btn-small btn-edit" onclick="editCustomer(${customer.id})">แก้ไข</button>
                        <button class="btn btn-small btn-delete" onclick="deleteCustomer(${customer.id})">ลบ</button>
                    </div>
                </div>
            `).join('');
        }

        // แปลงสถานะเป็นข้อความ
        function getStatusText(status) {
            const statusMap = {
                'waiting': 'รอติดตาม',
                'followup': 'ติดตามซ้ำ',
                'completed': 'เสร็จแล้ว'
            };
            return statusMap[status] || status;
        }

        // อัพเดทสถานะ
        function updateStatus(id, newStatus) {
            if (!currentUser) {
                alert('กรุณาเข้าสู่ระบบก่อน');
                return;
            }
            
            const customer = customers.find(c => c.id === id);
            if (customer) {
                customer.status = newStatus;
                customer.updatedBy = currentUser.displayName;
                customer.updatedAt = new Date().toLocaleString('th-TH');
                renderCustomers();
                updateStats();
            }
        }

        // แก้ไขลูกค้า
        function editCustomer(id) {
            if (!currentUser) {
                alert('กรุณาเข้าสู่ระบบก่อน');
                return;
            }
            
            const customer = customers.find(c => c.id === id);
            if (customer) {
                document.getElementById('customerName').value = customer.name;
                document.getElementById('customerPhone').value = customer.phone || '';
                document.getElementById('customerEmail').value = customer.email || '';
                document.getElementById('contactReason').value = customer.reason;
                document.getElementById('customerDetails').value = customer.details || '';
                
                editingId = id;
                document.querySelector('.btn[type="submit"]').textContent = 'บันทึกการแก้ไข';
                
                // เลื่อนไปที่ฟอร์ม
                document.querySelector('.form-section').scrollIntoView({ behavior: 'smooth' });
            }
        }

        // ลบลูกค้า
        function deleteCustomer(id) {
            if (!currentUser) {
                alert('กรุณาเข้าสู่ระบบก่อน');
                return;
            }
            
            if (confirm('คุณแน่ใจหรือไม่ที่จะลบข้อมูลลูกค้านี้?')) {
                customers = customers.filter(c => c.id !== id);
                updateUserFilter();
                renderCustomers();
                updateStats();
            }
        }

        // อัพเดทสถิติ
        function updateStats() {
            const total = customers.length;
            const completed = customers.filter(c => c.status === 'completed').length;
            const waiting = customers.filter(c => c.status === 'waiting').length;
            const followup = customers.filter(c => c.status === 'followup').length;

            document.getElementById('totalCount').textContent = total;
            document.getElementById('completedCount').textContent = completed;
            document.getElementById('waitingCount').textContent = waiting;
            document.getElementById('followupCount').textContent = followup;
        }
    </script>
</body>
</html>
