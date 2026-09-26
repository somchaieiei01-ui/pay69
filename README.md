[my-sql.html](https://github.com/user-attachments/files/32686233/my-sql.html)
<!DOCTYPE html>
<html lang="th">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบจัดการสมาชิกและบริการฝากถอน - บ.จ.ก. INTARTKAMHENG285BAT (ประเทศไทย) จำกัด</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: 'Prompt', sans-serif;
        }
    </style>
</head>

<body class="bg-slate-900 text-slate-100 min-h-screen flex flex-col">

    <header class="bg-slate-800 border-b border-slate-700 shadow-lg">
        <div class="max-w-7xl mx-auto px-4 py-4 flex flex-col md:flex-row justify-between items-center gap-4">
            <div class="flex items-center space-x-3">
                <div class="bg-amber-500 text-slate-900 p-2.5 rounded-xl font-bold text-xl shadow-md">
                    <i class="fa-solid fa-shield-halved"></i>
                </div>
                <div>
                    <h1 class="text-xl font-bold text-amber-400">บ.จ.ก. INTARTKAMHENG285BAT (ประเทศไทย) จำกัด</h1>
                    <p class="text-xs text-slate-400">ระบบจัดการสมาชิก ควบคุมเกม และบริการฝาก-ถอนอัตโนมัติ</p>
                </div>
            </div>
            <div class="flex items-center gap-3">
                <span
                    class="px-3 py-1 bg-emerald-500/20 text-emerald-400 border border-emerald-500/30 text-xs rounded-full font-medium">
                    <i class="fa-solid fa-circle text-[8px] mr-1 text-emerald-400 animate-pulse"></i> API Connected
                    (Port 3000)
                </span>
                <button onclick="openModal('notificationModal')"
                    class="bg-slate-700 hover:bg-slate-600 px-3 py-2 rounded-lg text-sm transition relative">
                    <i class="fa-solid fa-bell"></i>
                    <span id="pendingWithdrawalBadge"
                        class="absolute -top-1 -right-1 bg-rose-500 text-white text-[10px] w-5 h-5 rounded-full flex items-center justify-center font-bold">2</span>
                </button>
            </div>
        </div>
    </header>

    <nav class="bg-slate-800/60 border-b border-slate-700/60 backdrop-blur">
        <div class="max-w-7xl mx-auto px-4 overflow-x-auto flex space-x-2 py-2">
            <button onclick="switchTab('users')" id="tab-users"
                class="tab-btn px-4 py-2 rounded-lg text-sm font-medium transition bg-amber-500 text-slate-900 shadow">
                <i class="fa-solid fa-users mr-2"></i> ผู้ใช้งานระบบ (Users)
            </button>
            <button onclick="switchTab('controls')" id="tab-controls"
                class="tab-btn px-4 py-2 rounded-lg text-sm font-medium transition text-slate-300 hover:bg-slate-700">
                <i class="fa-solid fa-sliders mr-2"></i> ควบคุมเกมผู้เล่น (Game Controls)
            </button>
            <button onclick="switchTab('apis')" id="tab-apis"
                class="tab-btn px-4 py-2 rounded-lg text-sm font-medium transition text-slate-300 hover:bg-slate-700">
                <i class="fa-solid fa-network-wired mr-2"></i> ตั้งค่า API & Provider
            </button>
            <button onclick="switchTab('accounts')" id="tab-accounts"
                class="tab-btn px-4 py-2 rounded-lg text-sm font-medium transition text-slate-300 hover:bg-slate-700">
                <i class="fa-solid fa-building-columns mr-2"></i> บัญชีรับเงินบริษัท
            </button>
            <button onclick="switchTab('wallets')" id="tab-wallets"
                class="tab-btn px-4 py-2 rounded-lg text-sm font-medium transition text-slate-300 hover:bg-slate-700">
                <i class="fa-solid fa-wallet mr-2"></i> กระเป๋าเงินระบบ (Wallets)
            </button>
            <button onclick="switchTab('withdrawals')" id="tab-withdrawals"
                class="tab-btn px-4 py-2 rounded-lg text-sm font-medium transition text-slate-300 hover:bg-slate-700">
                <i class="fa-solid fa-money-bill-transfer mr-2"></i> รายการถอนเงิน (Withdrawals)
            </button>
        </div>
    </nav>

    <main class="max-w-7xl mx-auto px-4 py-6 flex-1 w-full">

        <!-- SECTION 1: USERS -->
        <section id="section-users" class="space-y-4">
            <div class="flex justify-between items-center">
                <h2 class="text-lg font-bold text-white"><i class="fa-solid fa-users text-amber-400 mr-2"></i>
                    ตารางข้อมูลสมาชิก (Users)</h2>
                <button onclick="openAddUserModal()"
                    class="bg-amber-500 hover:bg-amber-600 text-slate-900 font-semibold px-4 py-2 rounded-lg text-sm shadow transition flex items-center gap-2">
                    <i class="fa-solid fa-user-plus"></i> เพิ่มผู้ใช้งาน
                </button>
            </div>
            <div class="bg-slate-800 rounded-xl border border-slate-700 shadow overflow-x-auto">
                <table class="w-full text-left border-collapse text-sm">
                    <thead>
                        <tr class="bg-slate-700/50 text-slate-300 border-b border-slate-700">
                            <th class="p-3">ID</th>
                            <th class="p-3">ชื่อผู้ใช้ (Username)</th>
                            <th class="p-3">เบอร์โทรศัพท์</th>
                            <th class="p-3">บทบาท (Role)</th>
                            <th class="p-3">สถานะ (Status)</th>
                            <th class="p-3">สร้างเมื่อ</th>
                            <th class="p-3 text-right">จัดการ</th>
                        </tr>
                    </thead>
                    <tbody id="usersTableBody" class="divide-y divide-slate-700">
                        <!-- Populated by JS -->
                    </tbody>
                </table>
            </div>
        </section>

        <!-- SECTION 2: PLAYER GAME CONTROLS -->
        <section id="section-controls" class="space-y-4 hidden">
            <div class="flex justify-between items-center">
                <h2 class="text-lg font-bold text-white"><i class="fa-solid fa-sliders text-amber-400 mr-2"></i>
                    ควบคุมอัตราแพ้ชนะ & ยอดถอนต่อวัน (Player Game Controls)</h2>
                <p class="text-xs text-slate-400">กำหนดเรทเปอร์เซ็นต์ชนะ ล็อกผล และจำกัดยอดถอนต่อผู้เล่น</p>
            </div>
            <div class="bg-slate-800 rounded-xl border border-slate-700 shadow overflow-x-auto">
                <table class="w-full text-left border-collapse text-sm">
                    <thead>
                        <tr class="bg-slate-700/50 text-slate-300 border-b border-slate-700">
                            <th class="p-3">User ID & Username</th>
                            <th class="p-3">อัตราเปอร์เซ็นต์ชนะ (%)</th>
                            <th class="p-3">ล็อกผลแพ้ (Lock Loss)</th>
                            <th class="p-3">ล็อกผลชนะ (Lock Win)</th>
                            <th class="p-3">จำกัดยอดถอน/วัน (บาท)</th>
                            <th class="p-3 text-right">บันทึกการแก้ไข</th>
                        </tr>
                    </thead>
                    <tbody id="controlsTableBody" class="divide-y divide-slate-700">
                        <!-- Populated by JS -->
                    </tbody>
                </table>
            </div>
        </section>

        <!-- SECTION 3: API CONFIGURATIONS -->
        <section id="section-apis" class="space-y-4 hidden">
            <div class="flex justify-between items-center">
                <h2 class="text-lg font-bold text-white"><i class="fa-solid fa-network-wired text-amber-400 mr-2"></i>
                    ตั้งค่าเชื่อมต่อ API และ Game Provider</h2>
                <button onclick="openAddApiModal()"
                    class="bg-amber-500 hover:bg-amber-600 text-slate-900 font-semibold px-4 py-2 rounded-lg text-sm shadow transition flex items-center gap-2">
                    <i class="fa-solid fa-plus"></i> เพิ่ม Provider API
                </button>
            </div>
            <div class="bg-slate-800 rounded-xl border border-slate-700 shadow overflow-x-auto">
                <table class="w-full text-left border-collapse text-sm">
                    <thead>
                        <tr class="bg-slate-700/50 text-slate-300 border-b border-slate-700">
                            <th class="p-3">ID</th>
                            <th class="p-3">ชื่อ Provider</th>
                            <th class="p-3">API URL</th>
                            <th class="p-3">Merchant ID</th>
                            <th class="p-3">สถานะการใช้งาน</th>
                            <th class="p-3 text-right">จัดการ</th>
                        </tr>
                    </thead>
                    <tbody id="apisTableBody" class="divide-y divide-slate-700">
                        <!-- Populated by JS -->
                    </tbody>
                </table>
            </div>
        </section>

        <!-- SECTION 4: COMPANY PAYMENT ACCOUNTS -->
        <section id="section-accounts" class="space-y-4 hidden">
            <div class="flex justify-between items-center">
                <h2 class="text-lg font-bold text-white"><i
                        class="fa-solid fa-building-columns text-amber-400 mr-2"></i> บัญชีรับเงินบริษัท (Payment
                    Accounts)</h2>
                <button onclick="openAddAccountModal()"
                    class="bg-amber-500 hover:bg-amber-600 text-slate-900 font-semibold px-4 py-2 rounded-lg text-sm shadow transition flex items-center gap-2">
                    <i class="fa-solid fa-plus"></i> เพิ่มบัญชีรับเงิน
                </button>
            </div>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4" id="accountsCardGrid">
                <!-- Populated by JS -->
            </div>
        </section>

        <!-- SECTION 5: SYSTEM WALLETS -->
        <section id="section-wallets" class="space-y-4 hidden">
            <div class="flex justify-between items-center">
                <h2 class="text-lg font-bold text-white"><i class="fa-solid fa-wallet text-amber-400 mr-2"></i>
                    ยอดเงินคงเหลือในระบบ (System Wallets)</h2>
                <p class="text-xs text-slate-400">ตรวจสอบยอดเงินสด โบนัส และยอดเทิร์นโอเวอร์สะสม</p>
            </div>
            <div class="bg-slate-800 rounded-xl border border-slate-700 shadow overflow-x-auto">
                <table class="w-full text-left border-collapse text-sm">
                    <thead>
                        <tr class="bg-slate-700/50 text-slate-300 border-b border-slate-700">
                            <th class="p-3">User ID & Username</th>
                            <th class="p-3">ยอดเงินสด (Balance)</th>
                            <th class="p-3">โบนัส (Bonus Balance)</th>
                            <th class="p-3">เทิร์นโอเวอร์สะสม (Turnover)</th>
                            <th class="p-3">อัปเดตล่าสุด</th>
                            <th class="p-3 text-right">ปรับยอดเงิน</th>
                        </tr>
                    </thead>
                    <tbody id="walletsTableBody" class="divide-y divide-slate-700">
                        <!-- Populated by JS -->
                    </tbody>
                </table>
            </div>
        </section>

        <!-- SECTION 6: WITHDRAWALS -->
        <section id="section-withdrawals" class="space-y-4 hidden">
            <div class="flex justify-between items-center">
                <h2 class="text-lg font-bold text-white"><i
                        class="fa-solid fa-money-bill-transfer text-amber-400 mr-2"></i> รายการถอนเงิน (Withdrawal
                    Requests & Logs)</h2>
                <div class="flex gap-2">
                    <span class="text-xs bg-slate-700 px-3 py-1 rounded-lg flex items-center text-slate-300">
                        API Base: <code class="text-amber-400 ml-1">http://localhost:3000/api</code>
                    </span>
                </div>
            </div>
            <div class="bg-slate-800 rounded-xl border border-slate-700 shadow overflow-x-auto">
                <table class="w-full text-left border-collapse text-sm">
                    <thead>
                        <tr class="bg-slate-700/50 text-slate-300 border-b border-slate-700">
                            <th class="p-3">ID</th>
                            <th class="p-3">ผู้เล่น (User)</th>
                            <th class="p-3">จำนวนเงิน (THB)</th>
                            <th class="p-3">บัญชีปลายทาง</th>
                            <th class="p-3">สถานะ (Status)</th>
                            <th class="p-3">หมายเหตุแอดมิน</th>
                            <th class="p-3 text-right">การจัดการ</th>
                        </tr>
                    </thead>
                    <tbody id="withdrawalsTableBody" class="divide-y divide-slate-700">
                        <!-- Populated by JS -->
                    </tbody>
                </table>
            </div>
        </section>

    </main>

    <!-- MODAL: ADD USER -->
    <div id="addUserModal"
        class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-slate-800 border border-slate-700 rounded-2xl w-full max-w-md p-6 shadow-2xl space-y-4">
            <div class="flex justify-between items-center border-b border-slate-700 pb-3">
                <h3 class="font-bold text-lg text-amber-400"><i class="fa-solid fa-user-plus mr-2"></i> เพิ่มสมาชิกใหม่
                    (Users)</h3>
                <button onclick="closeModal('addUserModal')" class="text-slate-400 hover:text-white"><i
                        class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <form id="addUserForm" onsubmit="handleCreateUser(event)" class="space-y-3">
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">ชื่อผู้ใช้ (Username)</label>
                    <input type="text" id="newUsername" required
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400">
                </div>
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">รหัสผ่าน (Password Hash)</label>
                    <input type="password" id="newPassword" required
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400"
                        value="********">
                </div>
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">เบอร์โทรศัพท์ (Phone Number)</label>
                    <input type="text" id="newPhone" required
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400"
                        placeholder="0812345678">
                </div>
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">บทบาท (Role)</label>
                    <select id="newRole"
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400">
                        <option value="USER">USER (ผู้เล่นทั่วไป)</option>
                        <option value="AGENT">AGENT (ตัวแทน)</option>
                        <option value="ADMIN">ADMIN (ผู้ดูแลระบบ)</option>
                    </select>
                </div>
                <div class="pt-2 flex justify-end gap-2">
                    <button type="button" onclick="closeModal('addUserModal')"
                        class="px-4 py-2 bg-slate-700 hover:bg-slate-600 rounded-lg text-sm">ยกเลิก</button>
                    <button type="submit"
                        class="px-4 py-2 bg-amber-500 hover:bg-amber-600 text-slate-900 font-semibold rounded-lg text-sm">บันทึกข้อมูล</button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL: ADD API CONFIG -->
    <div id="addApiModal"
        class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-slate-800 border border-slate-700 rounded-2xl w-full max-w-md p-6 shadow-2xl space-y-4">
            <div class="flex justify-between items-center border-b border-slate-700 pb-3">
                <h3 class="font-bold text-lg text-amber-400"><i class="fa-solid fa-network-wired mr-2"></i> เพิ่ม API
                    Provider</h3>
                <button onclick="closeModal('addApiModal')" class="text-slate-400 hover:text-white"><i
                        class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <form id="addApiForm" onsubmit="handleCreateApi(event)" class="space-y-3">
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">ชื่อ Provider (เช่น SA_GAMING, PG_SOFT,
                        BANK_API)</label>
                    <input type="text" id="apiProviderName" required
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400"
                        placeholder="PG_SOFT">
                </div>
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">API URL</label>
                    <input type="text" id="apiUrlPath" required
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400"
                        placeholder="https://api.provider.com/v1">
                </div>
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">API Key / Secret Key</label>
                    <input type="text" id="apiKeyVal"
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400"
                        placeholder="sec_key_xxxx">
                </div>
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">Merchant ID</label>
                    <input type="text" id="apiMerchantId"
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400"
                        placeholder="INTART_285">
                </div>
                <div class="pt-2 flex justify-end gap-2">
                    <button type="button" onclick="closeModal('addApiModal')"
                        class="px-4 py-2 bg-slate-700 hover:bg-slate-600 rounded-lg text-sm">ยกเลิก</button>
                    <button type="submit"
                        class="px-4 py-2 bg-amber-500 hover:bg-amber-600 text-slate-900 font-semibold rounded-lg text-sm">บันทึก
                        API</button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL: ADD PAYMENT ACCOUNT -->
    <div id="addAccountModal"
        class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-slate-800 border border-slate-700 rounded-2xl w-full max-w-md p-6 shadow-2xl space-y-4">
            <div class="flex justify-between items-center border-b border-slate-700 pb-3">
                <h3 class="font-bold text-lg text-amber-400"><i class="fa-solid fa-building-columns mr-2"></i>
                    เพิ่มบัญชีรับเงินบริษัท</h3>
                <button onclick="closeModal('addAccountModal')" class="text-slate-400 hover:text-white"><i
                        class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <form id="addAccountForm" onsubmit="handleCreateAccount(event)" class="space-y-3">
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">ประเภทบัญชี</label>
                    <select id="accType" onchange="toggleBankCode()"
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400">
                        <option value="BANK">BANK (ธนาคารพาณิชย์)</option>
                        <option value="PROMPTPAY">PROMPTPAY (พร้อมเพย์)</option>
                        <option value="TRUEWALLET">TRUEWALLET (ทรูวอเลท)</option>
                    </select>
                </div>
                <div id="bankCodeGroup">
                    <label class="block text-xs font-medium text-slate-300 mb-1">รหัสธนาคาร (Bank Code)</label>
                    <select id="accBankCode"
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400">
                        <option value="KBANK">KBANK (กสิกรไทย)</option>
                        <option value="SCB">SCB (ไทยพาณิชย์)</option>
                        <option value="KTB">KTB (กรุงไทย)</option>
                        <option value="BBL">BBL (กรุงเทพ)</option>
                    </select>
                </div>
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">เลขบัญชี / เบอร์โทร</label>
                    <input type="text" id="accNumber" required
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400"
                        placeholder="1234567890">
                </div>
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">ชื่อบัญชี</label>
                    <input type="text" id="accName" required
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400"
                        placeholder="บ.จ.ก. อินทร์อาร์ตคําแหง 285">
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-xs font-medium text-slate-300 mb-1">ฝากขั้นต่ำ</label>
                        <input type="number" id="minDep" value="10"
                            class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400">
                    </div>
                    <div>
                        <label class="block text-xs font-medium text-slate-300 mb-1">ฝากสูงสุด</label>
                        <input type="number" id="maxDep" value="50000"
                            class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400">
                    </div>
                </div>
                <div class="pt-2 flex justify-end gap-2">
                    <button type="button" onclick="closeModal('addAccountModal')"
                        class="px-4 py-2 bg-slate-700 hover:bg-slate-600 rounded-lg text-sm">ยกเลิก</button>
                    <button type="submit"
                        class="px-4 py-2 bg-amber-500 hover:bg-amber-600 text-slate-900 font-semibold rounded-lg text-sm">เพิ่มบัญชี</button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL: ADJUST WALLET -->
    <div id="adjustWalletModal"
        class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-slate-800 border border-slate-700 rounded-2xl w-full max-w-md p-6 shadow-2xl space-y-4">
            <div class="flex justify-between items-center border-b border-slate-700 pb-3">
                <h3 class="font-bold text-lg text-amber-400"><i class="fa-solid fa-wallet mr-2"></i>
                    จัดการยอดเงินในกระเป๋า (Wallet)</h3>
                <button onclick="closeModal('adjustWalletModal')" class="text-slate-400 hover:text-white"><i
                        class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <form id="adjustWalletForm" onsubmit="handleSaveWallet(event)" class="space-y-3">
                <input type="hidden" id="walletUserId">
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">ผู้ใช้งาน</label>
                    <input type="text" id="walletUsernameDisplay" disabled
                        class="w-full bg-slate-900/50 border border-slate-700 rounded-lg p-2.5 text-sm text-slate-400">
                </div>
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">ยอดเงินสด (Balance)</label>
                    <input type="number" step="0.01" id="walletBalanceInput" required
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400">
                </div>
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">ยอดโบนัส (Bonus Balance)</label>
                    <input type="number" step="0.01" id="walletBonusInput" required
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400">
                </div>
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">ยอดเทิร์นโอเวอร์สะสม (Turnover)</label>
                    <input type="number" step="0.01" id="walletTurnoverInput" required
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400">
                </div>
                <div class="pt-2 flex justify-end gap-2">
                    <button type="button" onclick="closeModal('adjustWalletModal')"
                        class="px-4 py-2 bg-slate-700 hover:bg-slate-600 rounded-lg text-sm">ยกเลิก</button>
                    <button type="submit"
                        class="px-4 py-2 bg-amber-500 hover:bg-amber-600 text-slate-900 font-semibold rounded-lg text-sm">อัปเดตกระเป๋าเงิน</button>
                </div>
            </form>
        </div>
    </div>

    <!-- MODAL: WITHDRAWAL ACTION -->
    <div id="withdrawalModal"
        class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div class="bg-slate-800 border border-slate-700 rounded-2xl w-full max-w-md p-6 shadow-2xl space-y-4">
            <div class="flex justify-between items-center border-b border-slate-700 pb-3">
                <h3 class="font-bold text-lg text-amber-400"><i class="fa-solid fa-money-bill-transfer mr-2"></i>
                    ตรวจสอบคำขอถอนเงิน</h3>
                <button onclick="closeModal('withdrawalModal')" class="text-slate-400 hover:text-white"><i
                        class="fa-solid fa-xmark text-lg"></i></button>
            </div>
            <div id="withdrawalDetails"
                class="space-y-2 text-sm bg-slate-900 p-3 rounded-lg border border-slate-700 text-slate-300">
                <!-- Filled dynamically -->
            </div>
            <form id="withdrawalActionForm" onsubmit="handleProcessWithdrawal(event)" class="space-y-3">
                <input type="hidden" id="actionWithdrawalId">
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">เปลี่ยนสถานะ (Status)</label>
                    <select id="withdrawalNewStatus"
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400">
                        <option value="APPROVED">APPROVED (อนุมัติแล้ว)</option>
                        <option value="PROCESSING">PROCESSING (กำลังโอนเงิน)</option>
                        <option value="COMPLETED">COMPLETED (สำเร็จเรียบร้อย)</option>
                        <option value="REJECTED">REJECTED (ปฏิเสธรายการ)</option>
                    </select>
                </div>
                <div>
                    <label class="block text-xs font-medium text-slate-300 mb-1">หมายเหตุแอดมิน (Admin Remark)</label>
                    <textarea id="withdrawalRemark" rows="3"
                        class="w-full bg-slate-900 border border-slate-700 rounded-lg p-2.5 text-sm text-white focus:outline-none focus:border-amber-400"
                        placeholder="ระบุเหตุผลหรือเลขอ้างอิงการโอนเงิน..."></textarea>
                </div>
                <div class="pt-2 flex justify-end gap-2">
                    <button type="button" onclick="closeModal('withdrawalModal')"
                        class="px-4 py-2 bg-slate-700 hover:bg-slate-600 rounded-lg text-sm">ปิด</button>
                    <button type="submit"
                        class="px-4 py-2 bg-amber-500 hover:bg-amber-600 text-slate-900 font-semibold rounded-lg text-sm">ยืนยันการทำรายการ</button>
                </div>
            </form>
        </div>
    </div>

    <!-- NOTIFICATION MODAL FOR SYSTEM ALERTS -->
    <div id="notificationModal"
        class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 flex items-center justify-center hidden p-4">
        <div
            class="bg-slate-800 border border-slate-700 rounded-2xl w-full max-w-sm p-6 shadow-2xl text-center space-y-4">
            <div
                class="w-12 h-12 bg-amber-500/20 text-amber-400 rounded-full flex items-center justify-center mx-auto text-xl">
                <i class="fa-solid fa-circle-info"></i>
            </div>
            <h3 class="font-bold text-lg text-white">แจ้งเตือนระบบ</h3>
            <p id="notificationText" class="text-sm text-slate-300">ระบบทำงานปกติ เชื่อมต่อฐานข้อมูล PostgreSQL ผ่าน API
                Endpoint: http://localhost:3000/api พร้อมให้บริการ</p>
            <button onclick="closeModal('notificationModal')"
                class="w-full py-2 bg-amber-500 hover:bg-amber-600 text-slate-900 font-semibold rounded-lg text-sm">รับทราบ</button>
        </div>
    </div>

    <script>
        // Initial Simulated Database State matching SQL schema tables
        const dbState = {
            users: [
                { id: 1, username: 'admin_intart', phone_number: '0891112233', role: 'ADMIN', status: 'ACTIVE', created_at: '2026-01-10 10:00:00' },
                { id: 2, username: 'agent_285bat', phone_number: '0882223344', role: 'AGENT', status: 'ACTIVE', created_at: '2026-01-15 12:30:00' },
                { id: 3, username: 'player_somchai', phone_number: '0815556677', role: 'USER', status: 'ACTIVE', created_at: '2026-02-01 14:20:00' },
                { id: 4, username: 'player_jinda', phone_number: '0826667788', role: 'USER', status: 'ACTIVE', created_at: '2026-02-05 09:15:00' },
                { id: 5, username: 'player_hack_suspect', phone_number: '0899990000', role: 'USER', status: 'SUSPENDED', created_at: '2026-02-10 18:45:00' }
            ],
            player_game_controls: [
                { user_id: 3, win_rate_percent: 52.00, is_locked_loss: false, is_locked_win: false, max_payout_per_day: 100000.00 },
                { user_id: 4, win_rate_percent: 50.00, is_locked_loss: false, is_locked_win: false, max_payout_per_day: 50000.00 },
                { user_id: 5, win_rate_percent: 10.00, is_locked_loss: true, is_locked_win: false, max_payout_per_day: 0.00 }
            ],
            api_configurations: [
                { id: 1, provider_name: 'PG_SOFT', api_url: 'https://api.pgsoft-integration.com/v2', api_key: 'pg_live_key_998877', merchant_id: 'INTART_PG', is_active: true },
                { id: 2, provider_name: 'SA_GAMING', api_url: 'https://api.sagaming-api.net/live', api_key: 'sa_live_key_443322', merchant_id: 'INTART_SA', is_active: true },
                { id: 3, provider_name: 'BANK_API', api_url: 'https://api.bangkokbank-auto.co.th/v1', api_key: 'bank_sec_token_11', merchant_id: 'INTART_BANK', is_active: true }
            ],
            company_payment_accounts: [
                { id: 1, account_type: 'BANK', bank_code: 'KBANK', account_number: '045-8-99211-3', account_name: 'บ.จ.ก. อินทร์อาร์ตคำแหง 285', min_deposit: 10.00, max_deposit: 100000.00, is_active: true },
                { id: 2, account_type: 'PROMPTPAY', bank_code: null, account_number: '0891112233', account_name: 'บ.จ.ก. อินทร์อาร์ตคำแหง 285', min_deposit: 10.00, max_deposit: 50000.00, is_active: true },
                { id: 3, account_type: 'TRUEWALLET', bank_code: null, account_number: '0891112233', account_name: 'บ.จ.ก. อินทร์อาร์ตคำแหง 285', min_deposit: 20.00, max_deposit: 30000.00, is_active: true }
            ],
            wallets: [
                { user_id: 3, balance: 14520.50, bonus_balance: 500.00, turnover_accumulated: 12500.00, updated_at: '2026-03-30 08:30:00' },
                { user_id: 4, balance: 3200.00, bonus_balance: 0.00, turnover_accumulated: 3400.00, updated_at: '2026-03-30 09:12:00' },
                { user_id: 5, balance: 0.00, bonus_balance: 0.00, turnover_accumulated: 0.00, updated_at: '2026-03-25 11:00:00' }
            ],
            withdrawals: [
                { id: 101, user_id: 3, amount: 2500.00, target_account_type: 'BANK', target_bank_code: 'KBANK', target_account_number: '123-4-56789-0', target_account_name: 'สมชาย ใจดี', status: 'PENDING', admin_remark: 'รอตรวจสอบยอดเทิร์น', approved_by: null, created_at: '2026-03-30 09:10:00' },
                { id: 102, user_id: 4, amount: 1200.00, target_account_type: 'PROMPTPAY', target_bank_code: null, target_account_number: '0826667788', target_account_name: 'จินดา ศรีสว่าง', status: 'PENDING', admin_remark: '-', approved_by: null, created_at: '2026-03-30 09:25:00' },
                { id: 103, user_id: 3, amount: 5000.00, target_account_type: 'TRUEWALLET', target_bank_code: null, target_account_number: '0815556677', target_account_name: 'สมชาย ใจดี', status: 'COMPLETED', admin_remark: 'โอนสำเร็จอัตโนมัติ', approved_by: 1, created_at: '2026-03-29 15:00:00' }
            ]
        };

        // Tab Switching
        function switchTab(tabId) {
            document.querySelectorAll('section').forEach(sec => sec.classList.add('hidden'));
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('bg-amber-500', 'text-slate-900', 'shadow');
                btn.classList.add('text-slate-300', 'hover:bg-slate-700');
            });

            document.getElementById(`section-${tabId}`).classList.remove('hidden');
            const activeBtn = document.getElementById(`tab-${tabId}`);
            activeBtn.classList.add('bg-amber-500', 'text-slate-900', 'shadow');
            activeBtn.classList.remove('text-slate-300', 'hover:bg-slate-700');

            renderAllTables();
        }

        // Render All Tables
        function renderAllTables() {
            renderUsersTable();
            renderControlsTable();
            renderApisTable();
            renderAccountsGrid();
            renderWalletsTable();
            renderWithdrawalsTable();
            updatePendingBadge();
        }

        // 1. Users Table
        function renderUsersTable() {
            const tbody = document.getElementById('usersTableBody');
            tbody.innerHTML = '';
            dbState.users.forEach(u => {
                let badgeColor = u.role === 'ADMIN' ? 'bg-rose-500/20 text-rose-400 border-rose-500/30' : (u.role === 'AGENT' ? 'bg-amber-500/20 text-amber-400 border-amber-500/30' : 'bg-blue-500/20 text-blue-400 border-blue-500/30');
                let statusColor = u.status === 'ACTIVE' ? 'bg-emerald-500/20 text-emerald-400' : 'bg-rose-500/20 text-rose-400';

                tbody.innerHTML += `
                    <tr class="hover:bg-slate-700/30 transition">
                        <td class="p-3 font-mono text-xs text-slate-400">#${u.id}</td>
                        <td class="p-3 font-semibold text-white">${u.username}</td>
                        <td class="p-3 text-slate-300">${u.phone_number || '-'}</td>
                        <td class="p-3"><span class="px-2 py-0.5 rounded text-xs border ${badgeColor}">${u.role}</span></td>
                        <td class="p-3"><span class="px-2 py-0.5 rounded text-xs ${statusColor}">${u.status}</span></td>
                        <td class="p-3 text-xs text-slate-400">${u.created_at}</td>
                        <td class="p-3 text-right">
                            <button onclick="toggleUserStatus(${u.id})" class="text-xs bg-slate-700 hover:bg-slate-600 px-2 py-1 rounded text-slate-200 transition">
                                <i class="fa-solid fa-power-off"></i> สลับสถานะ
                            </button>
                        </td>
                    </tr>
                `;
            });
        }

        // 2. Player Controls Table
        function renderControlsTable() {
            const tbody = document.getElementById('controlsTableBody');
            tbody.innerHTML = '';

            // Map users with controls
            dbState.users.filter(u => u.role === 'USER').forEach(u => {
                let ctrl = dbState.player_game_controls.find(c => c.user_id === u.id) || { win_rate_percent: 50.00, is_locked_loss: false, is_locked_win: false, max_payout_per_day: 50000.00 };

                tbody.innerHTML += `
                    <tr class="hover:bg-slate-700/30 transition">
                        <td class="p-3 font-medium text-white">#${u.id} - ${u.username}</td>
                        <td class="p-3">
                            <div class="flex items-center gap-2">
                                <input type="range" min="0" max="100" step="1" value="${ctrl.win_rate_percent}" id="winRate_${u.id}" class="w-28 accent-amber-500" oninput="document.getElementById('val_${u.id}').innerText = this.value + '%'">
                                <span id="val_${u.id}" class="text-xs font-bold text-amber-400 w-10">${ctrl.win_rate_percent}%</span>
                            </div>
                        </td>
                        <td class="p-3">
                            <input type="checkbox" id="lockLoss_${u.id}" ${ctrl.is_locked_loss ? 'checked' : ''} class="w-4 h-4 accent-rose-500 rounded">
                        </td>
                        <td class="p-3">
                            <input type="checkbox" id="lockWin_${u.id}" ${ctrl.is_locked_win ? 'checked' : ''} class="w-4 h-4 accent-emerald-500 rounded">
                        </td>
                        <td class="p-3">
                            <input type="number" id="maxPayout_${u.id}" value="${ctrl.max_payout_per_day}" class="bg-slate-900 border border-slate-700 rounded p-1.5 text-xs text-white w-32 focus:outline-none focus:border-amber-400">
                        </td>
                        <td class="p-3 text-right">
                            <button onclick="savePlayerControl(${u.id})" class="bg-amber-500 hover:bg-amber-600 text-slate-900 font-semibold px-3 py-1.5 rounded text-xs shadow transition">
                                <i class="fa-solid fa-floppy-disk mr-1"></i> บันทึก
                            </button>
                        </td>
                    </tr>
                `;
            });
        }

        // 3. API Config Table
        function renderApisTable() {
            const tbody = document.getElementById('apisTableBody');
            tbody.innerHTML = '';
            dbState.api_configurations.forEach(api => {
                tbody.innerHTML += `
                    <tr class="hover:bg-slate-700/30 transition">
                        <td class="p-3 font-mono text-xs text-slate-400">#${api.id}</td>
                        <td class="p-3 font-bold text-white">${api.provider_name}</td>
                        <td class="p-3 font-mono text-xs text-amber-400">${api.api_url}</td>
                        <td class="p-3 font-mono text-xs text-slate-300">${api.merchant_id || '-'}</td>
                        <td class="p-3">
                            <span class="px-2 py-0.5 rounded text-xs ${api.is_active ? 'bg-emerald-500/20 text-emerald-400' : 'bg-rose-500/20 text-rose-400'}">
                                ${api.is_active ? 'ACTIVE' : 'INACTIVE'}
                            </span>
                        </td>
                        <td class="p-3 text-right">
                            <button onclick="toggleApiStatus(${api.id})" class="text-xs bg-slate-700 hover:bg-slate-600 px-2 py-1 rounded text-slate-200 transition">
                                เปิด/ปิด
                            </button>
                        </td>
                    </tr>
                `;
            });
        }

        // 4. Payment Accounts Grid
        function renderAccountsGrid() {
            const grid = document.getElementById('accountsCardGrid');
            grid.innerHTML = '';
            dbState.company_payment_accounts.forEach(acc => {
                let icon = acc.account_type === 'BANK' ? 'fa-building-columns text-blue-400' : (acc.account_type === 'PROMPTPAY' ? 'fa-qrcode text-emerald-400' : 'fa-wallet text-orange-400');
                grid.innerHTML += `
                    <div class="bg-slate-800 border border-slate-700 rounded-xl p-5 shadow space-y-3 relative">
                        <div class="flex justify-between items-start">
                            <div class="flex items-center gap-3">
                                <div class="w-10 h-10 rounded-lg bg-slate-700/50 flex items-center justify-center text-lg ${icon}">
                                    <i class="fa-solid ${icon}"></i>
                                </div>
                                <div>
                                    <h4 class="font-bold text-white">${acc.account_type} ${acc.bank_code ? '(' + acc.bank_code + ')' : ''}</h4>
                                    <p class="text-xs text-slate-400">${acc.account_name}</p>
                                </div>
                            </div>
                            <span class="px-2 py-0.5 rounded text-[10px] ${acc.is_active ? 'bg-emerald-500/20 text-emerald-400' : 'bg-rose-500/20 text-rose-400'}">
                                ${acc.is_active ? 'เปิดใช้งาน' : 'ปิดใช้งาน'}
                            </span>
                        </div>
                        <div class="bg-slate-900/80 p-3 rounded-lg border border-slate-700 font-mono text-amber-400 font-bold text-center tracking-wider text-base">
                            ${acc.account_number}
                        </div>
                        <div class="flex justify-between text-xs text-slate-400 pt-1">
                            <span>ฝากขั้นต่ำ: <strong class="text-white">${acc.min_deposit} ฿</strong></span>
                            <span>ฝากสูงสุด: <strong class="text-white">${acc.max_deposit} ฿</strong></span>
                        </div>
                        <div class="pt-2 border-t border-slate-700 flex justify-end">
                            <button onclick="toggleAccountStatus(${acc.id})" class="text-xs text-slate-300 hover:text-white bg-slate-700 hover:bg-slate-600 px-3 py-1 rounded transition">
                                สลับสถานะเปิด/ปิด
                            </button>
                        </div>
                    </div>
                `;
            });
        }

        // 5. System Wallets Table
        function renderWalletsTable() {
            const tbody = document.getElementById('walletsTableBody');
            tbody.innerHTML = '';
            dbState.users.filter(u => u.role === 'USER').forEach(u => {
                let wallet = dbState.wallets.find(w => w.user_id === u.id) || { balance: 0.00, bonus_balance: 0.00, turnover_accumulated: 0.00, updated_at: '-' };
                tbody.innerHTML += `
                    <tr class="hover:bg-slate-700/30 transition">
                        <td class="p-3 font-medium text-white">#${u.id} - ${u.username}</td>
                        <td class="p-3 font-bold text-emerald-400">${wallet.balance.toLocaleString('th-TH', { minimumFractionDigits: 2 })} ฿</td>
                        <td class="p-3 text-amber-400">${wallet.bonus_balance.toLocaleString('th-TH', { minimumFractionDigits: 2 })} ฿</td>
                        <td class="p-3 text-slate-300">${wallet.turnover_accumulated.toLocaleString('th-TH', { minimumFractionDigits: 2 })} ฿</td>
                        <td class="p-3 text-xs text-slate-400">${wallet.updated_at}</td>
                        <td class="p-3 text-right">
                            <button onclick="openAdjustWallet(${u.id})" class="bg-slate-700 hover:bg-slate-600 text-slate-200 text-xs px-3 py-1 rounded transition">
                                <i class="fa-solid fa-pen-to-square mr-1"></i> ปรับยอด
                            </button>
                        </td>
                    </tr>
                `;
            });
        }

        // 6. Withdrawals Table
        function renderWithdrawalsTable() {
            const tbody = document.getElementById('withdrawalsTableBody');
            tbody.innerHTML = '';
            dbState.withdrawals.forEach(w => {
                let user = dbState.users.find(u => u.id === w.user_id) || { username: 'Unknown' };
                let statusBadge = '';
                if (w.status === 'PENDING') statusBadge = 'bg-amber-500/20 text-amber-400 border border-amber-500/30';
                else if (w.status === 'APPROVED' || w.status === 'PROCESSING') statusBadge = 'bg-blue-500/20 text-blue-400 border border-blue-500/30';
                else if (w.status === 'COMPLETED') statusBadge = 'bg-emerald-500/20 text-emerald-400 border border-emerald-500/30';
                else statusBadge = 'bg-rose-500/20 text-rose-400 border border-rose-500/30';

                tbody.innerHTML += `
                    <tr class="hover:bg-slate-700/30 transition">
                        <td class="p-3 font-mono text-xs text-slate-400">#${w.id}</td>
                        <td class="p-3 font-medium text-white">${user.username}</td>
                        <td class="p-3 font-bold text-amber-400">${w.amount.toLocaleString('th-TH', { minimumFractionDigits: 2 })} ฿</td>
                        <td class="p-3 text-xs">
                            <div class="text-white font-medium">${w.target_account_type} ${w.target_bank_code ? '(' + w.target_bank_code + ')' : ''}</div>
                            <div class="font-mono text-slate-400">${w.target_account_number} (${w.target_account_name})</div>
                        </td>
                        <td class="p-3"><span class="px-2 py-0.5 rounded text-xs ${statusBadge}">${w.status}</span></td>
                        <td class="p-3 text-xs text-slate-300">${w.admin_remark || '-'}</td>
                        <td class="p-3 text-right">
                            <button onclick="openWithdrawalModal(${w.id})" class="bg-amber-500 hover:bg-amber-600 text-slate-900 font-semibold px-3 py-1 rounded text-xs transition">
                                <i class="fa-solid fa-gear mr-1"></i> จัดการ
                            </button>
                        </td>
                    </tr>
                `;
            });
        }

        function updatePendingBadge() {
            const count = dbState.withdrawals.filter(w => w.status === 'PENDING').length;
            const badge = document.getElementById('pendingWithdrawalBadge');
            badge.innerText = count;
            badge.style.display = count > 0 ? 'flex' : 'none';
        }

        // Actions & Modals handling
        function openModal(modalId) {
            document.getElementById(modalId).classList.remove('hidden');
        }
        function closeModal(modalId) {
            document.getElementById(modalId).classList.add('hidden');
        }

        function openAddUserModal() { openModal('addUserModal'); }
        function openAddApiModal() { openModal('addApiModal'); }
        function openAddAccountModal() { openModal('addAccountModal'); }

        function toggleBankCode() {
            const type = document.getElementById('accType').value;
            const group = document.getElementById('bankCodeGroup');
            group.style.display = type === 'BANK' ? 'block' : 'none';
        }

        function handleCreateUser(e) {
            e.preventDefault();
            const newUser = {
                id: dbState.users.length + 1,
                username: document.getElementById('newUsername').value,
                phone_number: document.getElementById('newPhone').value,
                role: document.getElementById('newRole').value,
                status: 'ACTIVE',
                created_at: new Date().toISOString().slice(0, 19).replace('T', ' ')
            };
            dbState.users.push(newUser);
            if (newUser.role === 'USER') {
                dbState.wallets.push({ user_id: newUser.id, balance: 0.00, bonus_balance: 0.00, turnover_accumulated: 0.00, updated_at: newUser.created_at });
            }
            closeModal('addUserModal');
            renderAllTables();
            alertPopup('เพิ่มผู้ใช้งานสำเร็จเรียบร้อย');
        }

        function handleCreateApi(e) {
            e.preventDefault();
            const newApi = {
                id: dbState.api_configurations.length + 1,
                provider_name: document.getElementById('apiProviderName').value,
                api_url: document.getElementById('apiUrlPath').value,
                api_key: document.getElementById('apiKeyVal').value,
                merchant_id: document.getElementById('apiMerchantId').value,
                is_active: true
            };
            dbState.api_configurations.push(newApi);
            closeModal('addApiModal');
            renderAllTables();
            alertPopup('เพิ่ม API Provider สำเร็จ');
        }

        function handleCreateAccount(e) {
            e.preventDefault();
            const newAcc = {
                id: dbState.company_payment_accounts.length + 1,
                account_type: document.getElementById('accType').value,
                bank_code: document.getElementById('accType').value === 'BANK' ? document.getElementById('accBankCode').value : null,
                account_number: document.getElementById('accNumber').value,
                account_name: document.getElementById('accName').value,
                min_deposit: parseFloat(document.getElementById('minDep').value),
                max_deposit: parseFloat(document.getElementById('maxDep').value),
                is_active: true
            };
            dbState.company_payment_accounts.push(newAcc);
            closeModal('addAccountModal');
            renderAllTables();
            alertPopup('เพิ่มบัญชีรับเงินบริษัทสำเร็จ');
        }

        function toggleUserStatus(id) {
            let u = dbState.users.find(x => x.id === id);
            if (u) {
                u.status = u.status === 'ACTIVE' ? 'SUSPENDED' : 'ACTIVE';
                renderUsersTable();
            }
        }

        function toggleApiStatus(id) {
            let a = dbState.api_configurations.find(x => x.id === id);
            if (a) {
                a.is_active = !a.is_active;
                renderApisTable();
            }
        }

        function toggleAccountStatus(id) {
            let acc = dbState.company_payment_accounts.find(x => x.id === id);
            if (acc) {
                acc.is_active = !acc.is_active;
                renderAccountsGrid();
            }
        }

        function savePlayerControl(userId) {
            let winRate = parseFloat(document.getElementById(`winRate_${userId}`).value);
            let lockLoss = document.getElementById(`lockLoss_${userId}`).checked;
            let lockWin = document.getElementById(`lockWin_${userId}`).checked;
            let maxPayout = parseFloat(document.getElementById(`maxPayout_${userId}`).value);

            let ctrl = dbState.player_game_controls.find(c => c.user_id === userId);
            if (ctrl) {
                ctrl.win_rate_percent = winRate;
                ctrl.is_locked_loss = lockLoss;
                ctrl.is_locked_win = lockWin;
                ctrl.max_payout_per_day = maxPayout;
            } else {
                dbState.player_game_controls.push({
                    user_id: userId,
                    win_rate_percent: winRate,
                    is_locked_loss: lockLoss,
                    is_locked_win: lockWin,
                    max_payout_per_day: maxPayout
                });
            }
            alertPopup(`บันทึกการควบคุมเกมสำหรับ User ID #${userId} สำเร็จ`);
        }

        function openAdjustWallet(userId) {
            let u = dbState.users.find(x => x.id === userId);
            let w = dbState.wallets.find(x => x.user_id === userId) || { balance: 0, bonus_balance: 0, turnover_accumulated: 0 };

            document.getElementById('walletUserId').value = userId;
            document.getElementById('walletUsernameDisplay').value = `#${u.id} - ${u.username}`;
            document.getElementById('walletBalanceInput').value = w.balance;
            document.getElementById('walletBonusInput').value = w.bonus_balance;
            document.getElementById('walletTurnoverInput').value = w.turnover_accumulated;

            openModal('adjustWalletModal');
        }

        function handleSaveWallet(e) {
            e.preventDefault();
            let userId = parseInt(document.getElementById('walletUserId').value);
            let balance = parseFloat(document.getElementById('walletBalanceInput').value);
            let bonus = parseFloat(document.getElementById('walletBonusInput').value);
            let turnover = parseFloat(document.getElementById('walletTurnoverInput').value);

            let w = dbState.wallets.find(x => x.user_id === userId);
            let nowStr = new Date().toISOString().slice(0, 19).replace('T', ' ');
            if (w) {
                w.balance = balance;
                w.bonus_balance = bonus;
                w.turnover_accumulated = turnover;
                w.updated_at = nowStr;
            } else {
                dbState.wallets.push({ user_id: userId, balance, bonus_balance: bonus, turnover_accumulated: turnover, updated_at: nowStr });
            }
            closeModal('adjustWalletModal');
            renderWalletsTable();
            alertPopup('อัปเดตยอดเงินในกระเป๋าเรียบร้อย');
        }

        function openWithdrawalModal(wId) {
            let w = dbState.withdrawals.find(x => x.id === wId);
            let u = dbState.users.find(x => x.id === w.user_id);

            document.getElementById('actionWithdrawalId').value = w.id;
            document.getElementById('withdrawalNewStatus').value = w.status;
            document.getElementById('withdrawalRemark').value = w.admin_remark === '-' ? '' : w.admin_remark;

            document.getElementById('withdrawalDetails').innerHTML = `
                <div><strong>รหัสรายการ:</strong> #${w.id}</div>
                <div><strong>ผู้เล่น:</strong> ${u.username}</div>
                <div><strong>จำนวนเงิน:</strong> <span class="text-amber-400 font-bold">${w.amount.toLocaleString()} บาท</span></div>
                <div><strong>บัญชีรับเงิน:</strong> ${w.target_account_type} ${w.target_bank_code ? '(' + w.target_bank_code + ')' : ''} - ${w.target_account_number} (${w.target_account_name})</div>
            `;

            openModal('withdrawalModal');
        }

        function handleProcessWithdrawal(e) {
            e.preventDefault();
            let wId = parseInt(document.getElementById('actionWithdrawalId').value);
            let newStatus = document.getElementById('withdrawalNewStatus').value;
            let remark = document.getElementById('withdrawalRemark').value;

            let w = dbState.withdrawals.find(x => x.id === wId);
            if (w) {
                w.status = newStatus;
                w.admin_remark = remark || '-';
                w.approved_by = 1; // Admin ID 1
            }
            closeModal('withdrawalModal');
            renderWithdrawalsTable();
            alertPopup('บันทึกสถานะการถอนเงินเรียบร้อย');
        }

        function alertPopup(msg) {
            document.getElementById('notificationText').innerText = msg;
            openModal('notificationModal');
        }

        // Initialize on window load
        window.onload = function () {
            renderAllTables();
        };
    </script>
</body>

</html>
