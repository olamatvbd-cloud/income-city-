
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Earning App</title>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <!-- Telegram Web App SDK -->
    <script src="https://telegram.org/js/telegram-web-app.js"></script>

    <!-- Ad Network SDK (Updated Zone ID) -->
    <script src='//libtl.com/sdk.js' data-zone='10479160' data-sdk='show_10479160'></script>

    <style>
        :root {
            --primary-color: #007bff;
            --secondary-color: #28a745;
            --background-color: #f0f2f5;
            --card-background: #ffffff;
            --text-color: #333333;
            --light-text-color: #888888;
            --border-color: #e0e0e0;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--background-color);
            margin: 0;
            padding-bottom: 60px;
            color: var(--text-color);
        }

        .container {
            max-width: 450px;
            margin: 0 auto;
            background-color: var(--card-background);
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        .header {
            display: flex;
            align-items: center;
            padding: 10px 15px;
            background-color: var(--card-background);
            border-bottom: 1px solid var(--border-color);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        .header-profile-pic {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            margin-right: 12px;
            border: 2px solid var(--primary-color);
            background-color: #eee;
            object-fit: cover;
        }

        .header-user-info h3 {
            margin: 0;
            font-size: 16px;
            font-weight: 600;
        }
        
        .header-user-info p {
            margin: 0;
            font-size: 12px;
            color: var(--light-text-color);
        }

        .content {
            flex-grow: 1;
            padding: 20px;
            overflow-y: auto;
        }

        .card {
            background-color: var(--background-color);
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
            text-align: center;
            border: 1px solid var(--border-color);
        }

        .card-header {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 15px;
            color: var(--text-color);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .card-header .material-icons, .card-header .fa-solid {
            margin-right: 8px;
            color: var(--primary-color);
        }

        .balance-card .balance {
            font-size: 36px;
            font-weight: 700;
            color: var(--secondary-color);
            margin: 10px 0;
        }

        .card-label {
            font-size: 14px;
            color: var(--light-text-color);
        }

        .dashboard-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-top: 20px;
        }

        .dashboard-item {
            background-color: var(--card-background);
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
            text-align: center;
        }

        .dashboard-item .material-icons {
            font-size: 32px;
            margin-bottom: 10px;
            color: var(--primary-color);
        }

        .dashboard-item-value {
            font-size: 24px;
            font-weight: 700;
            color: var(--text-color);
        }

        .dashboard-item-label {
            font-size: 12px;
            color: var(--light-text-color);
        }

        .primary-btn, .secondary-btn {
            border: none;
            padding: 15px;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
            transition: background-color 0.3s, transform 0.2s;
            margin-top: 20px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        .primary-btn:hover {
            background-color: #0056b3;
            transform: translateY(-2px);
        }
        
        .primary-btn:disabled {
            background-color: #ccc;
            cursor: not-allowed;
            transform: none;
        }

        .primary-btn {
            background-color: var(--primary-color);
            color: #fff;
        }

        .secondary-btn {
            background-color: #f0f0f0;
            color: var(--text-color);
            border: 1px solid var(--border-color);
        }

        .progress-bar-container {
            height: 10px;
            background-color: #eee;
            border-radius: 5px;
            overflow: hidden;
            margin-top: 10px;
        }

        .progress-bar {
            height: 100%;
            background-color: var(--primary-color);
            width: 0;
            transition: width 0.5s ease-in-out;
        }

        .footer-nav {
            display: flex;
            justify-content: space-around;
            align-items: center;
            position: fixed;
            bottom: 0;
            width: 100%;
            max-width: 450px;
            background-color: var(--card-background);
            border-top: 1px solid var(--border-color);
            box-shadow: 0 -2px 8px rgba(0, 0, 0, 0.05);
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 10px;
            cursor: pointer;
            color: var(--light-text-color);
            flex: 1;
        }

        .nav-item.active {
            color: var(--primary-color);
        }

        .page {
            display: none;
            animation: fadeIn 0.5s;
        }

        .page.active {
            display: block;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .withdraw-form-container, .profile-info {
            background-color: var(--card-background);
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
            margin-top: 20px;
            border: 1px solid var(--border-color);
        }
        
        .profile-pic-container {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            background-color: #eee;
            margin: 0 auto 15px;
            overflow: hidden;
            border: 3px solid var(--primary-color);
        }

        .form-group {
            margin-bottom: 15px;
            text-align: left;
        }
        .form-group label { display: block; margin-bottom: 5px; font-weight: 600; }
        .form-group input, .form-group select {
            width: 100%; padding: 12px; border-radius: 8px; border: 1px solid var(--border-color); box-sizing: border-box;
        }
    </style>
</head>
<body>
    <div class="container">
        <header class="header">
            <img id="header-profile-pic" src="https://via.placeholder.com/40" alt="Profile" class="header-profile-pic">
            <div class="header-user-info">
                <h3 id="header-user-name">User</h3>
                <p>Welcome to the Earning App!</p>
            </div>
        </header>

        <main class="content">
            <!-- Home Page -->
            <section id="home-page" class="page active">
                <div class="card balance-card">
                    <h2 class="card-header"><span class="material-icons">account_balance_wallet</span> Balance</h2>
                    <div class="balance" id="current-balance">BDT 0.00</div>
                    <button class="primary-btn" id="start-earning-btn">Start Earning Now</button>
                    <button class="secondary-btn" id="withdraw-btn">Withdraw</button>
                </div>
                <div class="dashboard-grid">
                    <div class="dashboard-item">
                        <div class="dashboard-item-value" id="total-earnings">BDT 0.00</div>
                        <div class="dashboard-item-label">Total Earnings</div>
                    </div>
                    <div class="dashboard-item">
                        <div class="dashboard-item-value" id="ads-watched">0</div>
                        <div class="dashboard-item-label">Ads Watched</div>
                    </div>
                </div>
            </section>

            <!-- Earn Page -->
            <section id="earn-page" class="page">
                <div class="card">
                    <h2 class="card-header">Earn Rewards</h2>
                    <div id="ad-progress-text">Completed: 0 / 50</div>
                    <div class="progress-bar-container">
                        <div class="progress-bar" id="ad-progress-bar"></div>
                    </div>
                    <button class="primary-btn" id="watch-ad-btn">
                        বিজ্ঞাপন দেখুন ও আয় করুন
                        <span class="material-icons">play_circle_filled</span>
                    </button>
                </div>
            </section>
            
            <!-- Withdraw Page -->
            <section id="withdraw-page" class="page">
                <div class="card">
                    <h2>Withdraw</h2>
                    <div class="balance" id="withdraw-balance-display">BDT 0.00</div>
                    <p>Minimum: BDT 100.00</p>
                </div>
                <div class="withdraw-form-container">
                    <form id="withdraw-form">
                        <div class="form-group">
                            <label>Method</label>
                            <select id="withdraw-method" required>
                                <option value="bkash">bKash</option>
                                <option value="binance">Binance</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>Account Number</label>
                            <input type="text" id="account-number" required>
                        </div>
                        <div class="form-group">
                            <label>Amount</label>
                            <input type="number" id="withdraw-amount" min="100" required>
                        </div>
                        <button type="submit" class="primary-btn" id="submit-withdraw-btn">Submit Request</button>
                    </form>
                </div>
            </section>

            <!-- Profile Page -->
            <section id="profile-page" class="page">
                <div class="card">
                    <div class="profile-pic-container">
                        <img id="profile-page-pic" src="https://via.placeholder.com/80" style="width:100%">
                    </div>
                    <h3 id="profile-user-name">User</h3>
                </div>
            </section>
        </main>

        <nav class="footer-nav">
            <div class="nav-item active" data-page="home-page"><span class="material-icons">home</span></div>
            <div class="nav-item" data-page="earn-page"><span class="material-icons">play_circle</span></div>
            <div class="nav-item" data-page="withdraw-page"><span class="material-icons">payments</span></div>
            <div class="nav-item" data-page="profile-page"><span class="material-icons">person</span></div>
        </nav>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const tg = window.Telegram.WebApp;
            tg.ready();
            tg.expand();

            const DAILY_ADS_LIMIT = 50;
            const AD_REWARD = 0.02; 
            const MIN_WITHDRAW = 100;

            // Load Data
            let earnings = parseFloat(localStorage.getItem('earnings')) || 0;
            let adsWatched = parseInt(localStorage.getItem('adsWatched')) || 0;

            function updateUI() {
                document.getElementById('current-balance').textContent = `BDT ${earnings.toFixed(2)}`;
                document.getElementById('total-earnings').textContent = `BDT ${earnings.toFixed(2)}`;
                document.getElementById('ads-watched').textContent = adsWatched;
                document.getElementById('ad-progress-text').textContent = `Completed: ${adsWatched} / ${DAILY_ADS_LIMIT}`;
                document.getElementById('withdraw-balance-display').textContent = `BDT ${earnings.toFixed(2)}`;
                
                const progress = (adsWatched / DAILY_ADS_LIMIT) * 100;
                document.getElementById('ad-progress-bar').style.width = `${progress}%`;

                const watchBtn = document.getElementById('watch-ad-btn');
                if (adsWatched >= DAILY_ADS_LIMIT) {
                    watchBtn.disabled = true;
                    watchBtn.innerText = "Daily Limit Reached";
                }

                if(tg.initDataUnsafe.user) {
                    document.getElementById('header-user-name').textContent = tg.initDataUnsafe.user.first_name;
                    if(tg.initDataUnsafe.user.photo_url) {
                        document.getElementById('header-profile-pic').src = tg.initDataUnsafe.user.photo_url;
                        document.getElementById('profile-page-pic').src = tg.initDataUnsafe.user.photo_url;
                    }
                }
            }

            // Navigation
            document.querySelectorAll('.nav-item').forEach(item => {
                item.addEventListener('click', () => {
                    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
                    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
                    document.getElementById(item.dataset.page).classList.add('active');
                    item.classList.add('active');
                });
            });

            // Watch Ad Logic (Updated with new Zone ID)
            document.getElementById('watch-ad-btn').addEventListener('click', () => {
                if (adsWatched >= DAILY_ADS_LIMIT) {
                    tg.showAlert('আজকের লিমিট শেষ!');
                    return;
                }

                // Call the Ad SDK function
                if (typeof show_10479160 === 'function') {
                    show_10479160('pop').then(() => {
                        // User watched the ad
                        earnings += AD_REWARD;
                        adsWatched += 1;
                        localStorage.setItem('earnings', earnings);
                        localStorage.setItem('adsWatched', adsWatched);
                        updateUI();
                        tg.showAlert(`অভিনন্দন! আপনি BDT ${AD_REWARD} পেয়েছেন।`);
                    }).catch(e => {
                        tg.showAlert('অ্যাড লোড হতে সমস্যা হয়েছে, আবার চেষ্টা করুন।');
                    });
                } else {
                    tg.showAlert('Ad SDK found, but function not ready.');
                }
            });

            // Withdraw Logic
            document.getElementById('withdraw-form').addEventListener('submit', (e) => {
                e.preventDefault();
                const amount = parseFloat(document.getElementById('withdraw-amount').value);
                if (amount > earnings) {
                    tg.showAlert('পর্যাপ্ত ব্যালেন্স নেই!');
                    return;
                }
                if (amount < MIN_WITHDRAW) {
                    tg.showAlert(`নূন্যতম উইথড্র BDT ${MIN_WITHDRAW}`);
                    return;
                }

                tg.showConfirm("আপনি কি উইথড্র করতে চান?", (confirmed) => {
                    if (confirmed) {
                        earnings -= amount;
                        localStorage.setItem('earnings', earnings);
                        updateUI();
                        tg.showAlert('অনুরোধ সফল হয়েছে!');
                    }
                });
            });

            updateUI();
        });
    </script>
</body>
</html>
