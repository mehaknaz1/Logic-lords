<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CryptoAlert Pro</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <meta name="theme-color" content="#1e1b4b">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <style>
        @keyframes pulse-alert {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }
        .alert-pulse {
            animation: pulse-alert 1s ease-in-out infinite;
        }
        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
        .slide-in {
            animation: slideIn 0.3s ease-out;
        }
        @keyframes priceUpdate {
            0% { background-color: rgba(34, 197, 94, 0.2); }
            100% { background-color: transparent; }
        }
        .price-flash {
            animation: priceUpdate 0.5s ease-out;
        }
        @keyframes fadeInUp {
            from { 
                opacity: 0; 
                transform: translateY(30px); 
            }
            to { 
                opacity: 1; 
                transform: translateY(0); 
            }
        }
        .fade-in-up {
            animation: fadeInUp 0.6s ease-out;
        }
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }
        .float {
            animation: float 3s ease-in-out infinite;
        }
        @keyframes glow {
            0%, 100% { box-shadow: 0 0 20px rgba(59, 130, 246, 0.3); }
            50% { box-shadow: 0 0 30px rgba(59, 130, 246, 0.6); }
        }
        .glow {
            animation: glow 2s ease-in-out infinite;
        }
        @keyframes shimmer {
            0% { background-position: -200% 0; }
            100% { background-position: 200% 0; }
        }
        .shimmer {
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            background-size: 200% 100%;
            animation: shimmer 2s infinite;
        }
        @keyframes bounce {
            0%, 20%, 53%, 80%, 100% { transform: translate3d(0,0,0); }
            40%, 43% { transform: translate3d(0,-15px,0); }
            70% { transform: translate3d(0,-7px,0); }
            90% { transform: translate3d(0,-2px,0); }
        }
        .bounce {
            animation: bounce 1s ease-in-out;
        }
        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        .gradient-animate {
            background-size: 200% 200%;
            animation: gradientShift 4s ease infinite;
        }
        @keyframes scaleIn {
            from { 
                transform: scale(0.8); 
                opacity: 0; 
            }
            to { 
                transform: scale(1); 
                opacity: 1; 
            }
        }
        .scale-in {
            animation: scaleIn 0.4s ease-out;
        }
        .hover-lift {
            transition: all 0.3s ease;
        }
        .hover-lift:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.3);
        }
        .glass-effect {
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255,255,255,0.1);
        }
        @keyframes ripple {
            0% {
                transform: scale(0);
                opacity: 1;
            }
            100% {
                transform: scale(4);
                opacity: 0;
            }
        }
        .ripple-effect {
            position: relative;
            overflow: hidden;
        }
        .ripple-effect::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            border-radius: 50%;
            background: rgba(255,255,255,0.3);
            transform: translate(-50%, -50%);
            transition: width 0.6s, height 0.6s;
        }
        .ripple-effect:active::before {
            width: 300px;
            height: 300px;
        }
        
        /* Mobile App Styles */
        .mobile-app {
            max-width: 428px;
            margin: 0 auto;
            min-height: 100vh;
            position: relative;
            overflow-x: hidden;
        }
        
        .app-header {
            position: sticky;
            top: 0;
            z-index: 50;
            backdrop-filter: blur(20px);
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }
        
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            max-width: 428px;
            width: 100%;
            z-index: 50;
            backdrop-filter: blur(20px);
            border-top: 1px solid rgba(255,255,255,0.1);
        }
        
        .tab-content {
            display: none;
            padding-bottom: 100px;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .nav-item {
            transition: all 0.3s ease;
        }
        
        .nav-item.active {
            color: #60A5FA;
            transform: translateY(-2px);
        }
        
        @media (max-width: 428px) {
            .mobile-app {
                max-width: 100%;
            }
            .bottom-nav {
                max-width: 100%;
            }
        }
        
        .status-bar {
            height: env(safe-area-inset-top, 20px);
            background: rgba(0,0,0,0.3);
        }
        
        .safe-bottom {
            padding-bottom: env(safe-area-inset-bottom, 0px);
        }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-900 via-purple-900 to-indigo-900 min-h-screen text-white mobile-app">
    <!-- Status Bar -->
    <div class="status-bar"></div>
    
    <!-- App Header -->
    <div class="app-header bg-gradient-to-r from-blue-900/80 to-purple-900/80 px-4 py-3">
        <div class="flex items-center justify-between">
            <div class="flex items-center">
                <svg width="32" height="32" viewBox="0 0 48 48" class="mr-3">
                    <circle cx="24" cy="24" r="24" fill="url(#gradient1)"/>
                    <path d="M12 32l6-8 4 4 8-12 6 8" stroke="white" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
                    <circle cx="18" cy="24" r="2" fill="white"/>
                    <circle cx="22" cy="28" r="2" fill="white"/>
                    <circle cx="30" cy="16" r="2" fill="white"/>
                    <circle cx="36" cy="24" r="2" fill="white"/>
                    <defs>
                        <linearGradient id="gradient1" x1="0%" y1="0%" x2="100%" y2="100%">
                            <stop offset="0%" style="stop-color:#60A5FA"/>
                            <stop offset="50%" style="stop-color:#A855F7"/>
                            <stop offset="100%" style="stop-color:#EC4899"/>
                        </linearGradient>
                    </defs>
                </svg>
                <div>
                    <h1 class="text-lg font-bold text-white">CryptoAlert Pro</h1>
                    <p class="text-xs text-blue-200">Live Market Monitoring</p>
                </div>
            </div>
            <div class="flex items-center space-x-2">
                <div class="w-2 h-2 bg-green-400 rounded-full animate-pulse"></div>
                <span class="text-xs text-green-400">Live</span>
            </div>
        </div>
    </div>

    <!-- Tab Content Container -->
    <div class="px-4 pt-4">

        <!-- Home Tab -->
        <div id="homeTab" class="tab-content active">
            <!-- Quick Stats -->
            <div class="grid grid-cols-2 gap-3 mb-4">
                <div class="bg-gradient-to-br from-green-500/10 to-emerald-500/10 glass-effect rounded-lg p-4 border border-green-400/20">
                    <div class="text-2xl font-bold text-green-400 bounce" id="homeAlertCount">0</div>
                    <div class="text-xs text-white/60">Active Alerts</div>
                </div>
                <div class="bg-gradient-to-br from-blue-500/10 to-cyan-500/10 glass-effect rounded-lg p-4 border border-blue-400/20">
                    <div class="text-2xl font-bold text-blue-400 bounce" id="homeTriggeredToday">0</div>
                    <div class="text-xs text-white/60">Triggered Today</div>
                </div>
            </div>

            <!-- Top Cryptos -->
            <div class="bg-gradient-to-r from-purple-500/10 to-pink-500/10 glass-effect rounded-xl p-4 mb-4 border border-purple-400/30">
                <h2 class="text-lg font-semibold mb-3 flex items-center">
                    <span class="mr-2">🚀</span>
                    Top Cryptocurrencies
                </h2>
                <div id="homeTopCryptos" class="space-y-3"></div>
            </div>
        </div>

        <!-- Markets Tab -->
        <div id="marketsTab" class="tab-content">
            <div id="cryptoPrices" class="bg-gradient-to-r from-green-500/10 to-blue-500/10 glass-effect rounded-xl p-4 mb-4 border border-green-400/30">
                <div class="mb-4">
                    <h2 class="text-lg font-semibold mb-3">📈 Live Prices</h2>
                    <div class="flex space-x-2">
                        <input type="text" id="cryptoSearch" placeholder="Search crypto..." class="flex-1 px-3 py-2 bg-white/20 border border-white/30 rounded-lg text-white placeholder-white/60 focus:outline-none focus:ring-2 focus:ring-green-400 text-sm">
                        <button id="cryptoSearchBtn" class="px-4 py-2 bg-gradient-to-r from-green-500 to-blue-600 hover:from-green-600 hover:to-blue-700 rounded-lg font-medium transition-all duration-200 ripple-effect text-sm">
                            Search
                        </button>
                    </div>
                </div>
            
                <!-- Top 5 Cryptocurrencies -->
                <div id="topCryptos" class="space-y-3 mb-4">
                    <div class="flex items-center justify-between p-3 bg-gradient-to-r from-orange-500/10 to-yellow-500/10 glass-effect rounded-lg border border-orange-400/20">
                        <div class="flex items-center">
                            <svg width="24" height="24" viewBox="0 0 32 32" class="mr-3">
                                <circle cx="16" cy="16" r="16" fill="#F7931A"/>
                                <path d="M23.189 14.02c.314-2.096-1.283-3.223-3.465-3.975l.708-2.84-1.728-.43-.69 2.765c-.454-.114-.92-.22-1.385-.326l.695-2.783L15.596 6l-.708 2.839c-.376-.086-.746-.17-1.104-.26l.002-.009-2.384-.595-.46 1.846s1.283.294 1.256.312c.7.175.826.638.805 1.006l-.806 3.235c.048.012.11.03.18.057l-.183-.045-1.13 4.532c-.086.212-.303.531-.793.41.018.025-1.256-.313-1.256-.313l-.858 1.978 2.25.561c.418.105.828.215 1.231.318l-.715 2.872 1.727.43.708-2.84c.472.127.93.245 1.378.357l-.706 2.828 1.728.43.715-2.866c2.948.558 5.164.333 6.097-2.333.752-2.146-.037-3.385-1.588-4.192 1.13-.26 1.98-1.003 2.207-2.538zm-3.95 5.538c-.533 2.147-4.148.986-5.32.695l.95-3.805c1.172.293 4.929.872 4.37 3.11zm.535-5.569c-.487 1.953-3.495.96-4.47.717l.86-3.45c.975.243 4.118.696 3.61 2.733z" fill="white"/>
                            </svg>
                            <div>
                                <div class="font-medium text-white">Bitcoin</div>
                                <div class="text-xs text-white/60">BTC</div>
                            </div>
                        </div>
                        <div class="text-right">
                            <div class="font-bold text-white" id="price-bitcoin">Loading...</div>
                            <div class="text-xs" id="change-bitcoin">-</div>
                        </div>
                    </div>
                    <div class="flex items-center justify-between p-3 bg-gradient-to-r from-blue-500/10 to-purple-500/10 glass-effect rounded-lg border border-blue-400/20">
                        <div class="flex items-center">
                            <svg width="24" height="24" viewBox="0 0 32 32" class="mr-3">
                                <circle cx="16" cy="16" r="16" fill="#627EEA"/>
                                <path d="M16.498 4v8.87l7.497 3.35-7.497-12.22z" fill="#FFFFFF" opacity="0.602"/>
                                <path d="M16.498 4L9 16.22l7.498-3.35V4z" fill="#FFFFFF"/>
                                <path d="M16.498 21.968v6.027L24 17.616l-7.502 4.352z" fill="#FFFFFF" opacity="0.602"/>
                                <path d="M16.498 27.995v-6.028L9 17.616l7.498 10.38z" fill="#FFFFFF"/>
                                <path d="M16.498 20.573l7.497-4.353-7.497-3.348v7.701z" fill="#FFFFFF" opacity="0.2"/>
                                <path d="M9 16.22l7.498 4.353v-7.701L9 16.22z" fill="#FFFFFF" opacity="0.602"/>
                            </svg>
                            <div>
                                <div class="font-medium text-white">Ethereum</div>
                                <div class="text-xs text-white/60">ETH</div>
                            </div>
                        </div>
                        <div class="text-right">
                            <div class="font-bold text-white" id="price-ethereum">Loading...</div>
                            <div class="text-xs" id="change-ethereum">-</div>
                        </div>
                    </div>
                    <div class="flex items-center justify-between p-3 bg-gradient-to-r from-green-500/10 to-teal-500/10 glass-effect rounded-lg border border-green-400/20">
                        <div class="flex items-center">
                            <svg width="24" height="24" viewBox="0 0 32 32" class="mr-3">
                                <circle cx="16" cy="16" r="16" fill="#26A17B"/>
                                <path d="M17.922 17.383v-.002c-.11.008-.677.042-1.942.042-1.01 0-1.721-.03-1.971-.042v.003c-3.888-.171-6.79-.848-6.79-1.658 0-.809 2.902-1.486 6.79-1.66v2.644c.254.018.982.061 1.988.061 1.207 0 1.812-.05 1.925-.06v-2.643c3.88.173 6.775.85 6.775 1.658 0 .81-2.895 1.485-6.775 1.657m0-3.59v-2.366h5.414V7.819H8.595v3.608h5.414v2.365c-4.4.202-7.709 1.074-7.709 2.118 0 1.044 3.309 1.915 7.709 2.118v7.582h3.913v-7.584c4.393-.202 7.694-1.073 7.694-2.116 0-1.043-3.301-1.914-7.694-2.117" fill="white"/>
                            </svg>
                            <div>
                                <div class="font-medium text-white">Tether</div>
                                <div class="text-xs text-white/60">USDT</div>
                            </div>
                        </div>
                        <div class="text-right">
                            <div class="font-bold text-white" id="price-tether">Loading...</div>
                            <div class="text-xs" id="change-tether">-</div>
                        </div>
                    </div>
                    <div class="flex items-center justify-between p-3 bg-gradient-to-r from-yellow-500/10 to-orange-500/10 glass-effect rounded-lg border border-yellow-400/20">
                        <div class="flex items-center">
                            <svg width="24" height="24" viewBox="0 0 32 32" class="mr-3">
                                <circle cx="16" cy="16" r="16" fill="#F3BA2F"/>
                                <path d="M12.116 14.404L16 10.52l3.886 3.886 2.26-2.26L16 6l-6.144 6.144 2.26 2.26zM6 16l2.26-2.26L10.52 16l-2.26 2.26L6 16zm6.116 1.596L16 21.48l3.886-3.886 2.26 2.26L16 26l-6.144-6.144-2.26-2.26zm9.764-5.596L26 16l-2.26 2.26L21.48 16l2.26-2.26zm-3.764 0h4.52L16 19.48 9.364 12l4.52-.001L16 14.115 18.116 12z" fill="white"/>
                            </svg>
                            <div>
                                <div class="font-medium text-white">BNB</div>
                                <div class="text-xs text-white/60">BNB</div>
                            </div>
                        </div>
                        <div class="text-right">
                            <div class="font-bold text-white" id="price-binancecoin">Loading...</div>
                            <div class="text-xs" id="change-binancecoin">-</div>
                        </div>
                    </div>
                    <div class="flex items-center justify-between p-3 bg-gradient-to-r from-purple-500/10 to-pink-500/10 glass-effect rounded-lg border border-purple-400/20">
                        <div class="flex items-center">
                            <svg width="24" height="24" viewBox="0 0 32 32" class="mr-3">
                                <circle cx="16" cy="16" r="16" fill="#9945FF"/>
                                <path d="M6.5 21.5c0-.3.1-.5.3-.7l2.8-2.8c.2-.2.4-.3.7-.3h14.2c.6 0 .9.7.5 1.1l-2.8 2.8c-.2.2-.4.3-.7.3H7.3c-.4 0-.8-.2-.8-.4zm0-11c0-.3.1-.5.3-.7l2.8-2.8c.2-.2.4-.3.7-.3h14.2c.6 0 .9.7.5 1.1l-2.8 2.8c-.2.2-.4.3-.7.3H7.3c-.4 0-.8-.2-.8-.4zm17.2 5.5H9.5c-.6 0-.9-.7-.5-1.1l2.8-2.8c.2-.2.4-.3.7-.3h14.2c.4 0 .8.4.8.8 0 .3-.1.5-.3.7l-2.8 2.8c-.2.2-.4.3-.7.3z" fill="white"/>
                            </svg>
                            <div>
                                <div class="font-medium text-white">Solana</div>
                                <div class="text-xs text-white/60">SOL</div>
                            </div>
                        </div>
                        <div class="text-right">
                            <div class="font-bold text-white" id="price-solana">Loading...</div>
                            <div class="text-xs" id="change-solana">-</div>
                        </div>
                    </div>
                </div>

                <!-- Search Results -->
                <div id="searchResults" class="hidden">
                    <h3 class="text-lg font-semibold mb-3">Search Results</h3>
                    <div id="searchResultsGrid" class="space-y-3"></div>
                </div>
            </div>
        </div>

        <!-- Alerts Tab -->
        <div id="alertsTab" class="tab-content">
            <!-- Add Alert Form -->
            <div class="bg-gradient-to-r from-purple-500/10 to-pink-500/10 glass-effect rounded-xl p-4 mb-4 border border-purple-400/30">
                <h2 class="text-lg font-semibold mb-3 flex items-center">
                    <svg width="20" height="20" viewBox="0 0 24 24" class="mr-2">
                        <path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9" fill="#A855F7"/>
                        <path d="M13.73 21a2 2 0 0 1-3.46 0" fill="#A855F7"/>
                        <circle cx="18" cy="6" r="3" fill="#EF4444"/>
                    </svg>
                    Create Alert
                </h2>
                <form id="alertForm" class="space-y-3">
                    <select id="alertCrypto" class="w-full px-3 py-2 bg-white/20 border border-white/30 rounded-lg text-white focus:outline-none focus:ring-2 focus:ring-purple-400 text-sm" required>
                        <option value="" class="bg-gray-800">Select Cryptocurrency</option>
                        <option value="bitcoin" class="bg-gray-800">Bitcoin (BTC)</option>
                        <option value="ethereum" class="bg-gray-800">Ethereum (ETH)</option>
                        <option value="tether" class="bg-gray-800">Tether (USDT)</option>
                        <option value="binancecoin" class="bg-gray-800">BNB (BNB)</option>
                        <option value="solana" class="bg-gray-800">Solana (SOL)</option>
                        <option value="cardano" class="bg-gray-800">Cardano (ADA)</option>
                        <option value="ripple" class="bg-gray-800">XRP (XRP)</option>
                        <option value="dogecoin" class="bg-gray-800">Dogecoin (DOGE)</option>
                    </select>
                    <div class="grid grid-cols-2 gap-3">
                        <select id="alertType" class="px-3 py-2 bg-white/20 border border-white/30 rounded-lg text-white focus:outline-none focus:ring-2 focus:ring-purple-400 text-sm">
                            <option value="above" class="bg-gray-800">Price Above</option>
                            <option value="below" class="bg-gray-800">Price Below</option>
                        </select>
                        <input type="number" id="alertPrice" placeholder="Target Price ($)" step="0.01" class="px-3 py-2 bg-white/20 border border-white/30 rounded-lg text-white placeholder-white/60 focus:outline-none focus:ring-2 focus:ring-purple-400 text-sm" required>
                    </div>
                    <button type="submit" class="w-full py-3 bg-gradient-to-r from-purple-500 to-pink-600 hover:from-purple-600 hover:to-pink-700 rounded-lg font-medium transition-all duration-200 ripple-effect text-sm">
                        Create Alert
                    </button>
                </form>
            </div>

            <!-- Active Alerts -->
            <div id="activeAlerts" class="bg-gradient-to-br from-white/5 to-white/10 glass-effect rounded-xl p-4 mb-4 border border-white/20">
                <div class="flex justify-between items-center mb-3">
                    <h3 class="text-lg font-medium">🔔 Active Alerts</h3>
                    <button id="clearAllAlerts" class="px-3 py-1 bg-red-500/20 hover:bg-red-500/30 text-red-400 rounded-lg text-xs transition-all duration-200">
                        Clear All
                    </button>
                </div>
                <div id="alertsList" class="space-y-3">
                    <div class="text-center text-white/60 py-8 text-sm">
                        No active alerts. Create one above to get started!
                    </div>
                </div>
            </div>
        </div>

        <!-- Monitoring Tab -->
        <div id="monitoringTab" class="tab-content">
            <!-- Monitoring Stats -->
            <div class="grid grid-cols-2 gap-3 mb-4">
                <div class="text-center p-4 bg-gradient-to-br from-cyan-500/10 to-blue-500/10 glass-effect rounded-lg border border-cyan-400/20">
                    <div class="text-2xl font-bold text-cyan-400 bounce" id="monitoredCount">5</div>
                    <div class="text-xs text-white/60">Cryptos Monitored</div>
                </div>
                <div class="text-center p-4 bg-gradient-to-br from-green-500/10 to-emerald-500/10 glass-effect rounded-lg border border-green-400/20">
                    <div class="text-2xl font-bold text-green-400 bounce" id="alertCount">0</div>
                    <div class="text-xs text-white/60">Active Alerts</div>
                </div>
                <div class="text-center p-4 bg-gradient-to-br from-blue-500/10 to-indigo-500/10 glass-effect rounded-lg border border-blue-400/20">
                    <div class="text-2xl font-bold text-blue-400 bounce" id="lastUpdate">--:--</div>
                    <div class="text-xs text-white/60">Last Update</div>
                </div>
                <div class="text-center p-4 bg-gradient-to-br from-purple-500/10 to-pink-500/10 glass-effect rounded-lg border border-purple-400/20">
                    <div class="text-2xl font-bold text-purple-400 bounce" id="triggeredToday">0</div>
                    <div class="text-xs text-white/60">Triggered Today</div>
                </div>
            </div>

            <!-- Monitoring Status -->
            <div class="bg-gradient-to-r from-cyan-500/10 to-teal-500/10 glass-effect rounded-xl p-4 mb-4 border border-cyan-400/30">
                <div class="flex items-center mb-3">
                    <svg width="20" height="20" viewBox="0 0 24 24" class="mr-2">
                        <circle cx="12" cy="12" r="3" fill="#22D3EE"/>
                        <path d="M12 1v6m0 6v6m11-7h-6m-6 0H1" stroke="#22D3EE" stroke-width="2"/>
                        <circle cx="12" cy="12" r="11" stroke="#22D3EE" stroke-width="1" fill="none" opacity="0.3"/>
                    </svg>
                    <h3 class="text-lg font-medium">System Status</h3>
                </div>
                <div class="space-y-2">
                    <div class="flex justify-between items-center p-3 bg-white/5 rounded-lg">
                        <span class="text-white/80 text-sm">Data Source</span>
                        <span class="text-green-400 font-medium text-sm">CoinGecko ✓</span>
                    </div>
                    <div class="flex justify-between items-center p-3 bg-white/5 rounded-lg">
                        <span class="text-white/80 text-sm">Update Rate</span>
                        <span class="text-blue-400 font-medium text-sm">30 seconds</span>
                    </div>
                    <div class="flex justify-between items-center p-3 bg-white/5 rounded-lg">
                        <span class="text-white/80 text-sm">Alert System</span>
                        <div class="flex items-center">
                            <div class="w-2 h-2 bg-green-400 rounded-full animate-pulse mr-2"></div>
                            <span class="text-green-400 font-medium text-sm">Active</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Recent Alerts History -->
            <div class="bg-gradient-to-r from-amber-500/10 to-orange-500/10 glass-effect rounded-xl p-4 border border-amber-400/30">
                <div class="flex items-center mb-3">
                    <svg width="20" height="20" viewBox="0 0 24 24" class="mr-2">
                        <circle cx="12" cy="12" r="10" stroke="#F59E0B" stroke-width="2" fill="none"/>
                        <polyline points="12,6 12,12 16,14" stroke="#F59E0B" stroke-width="2" fill="none"/>
                    </svg>
                    <h3 class="text-lg font-medium">Recent History</h3>
                </div>
                <div id="recentAlerts" class="space-y-3">
                    <div class="text-center text-white/60 py-8 text-sm">
                        No recent alerts triggered. Your alerts will appear here when they activate.
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Bottom Navigation -->
    <div class="bottom-nav bg-gradient-to-r from-blue-900/90 to-purple-900/90 safe-bottom">
        <div class="flex justify-around items-center py-2">
            <button class="nav-item active flex flex-col items-center p-2" onclick="switchTab('home')">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z"/>
                </svg>
                <span class="text-xs mt-1">Home</span>
            </button>
            <button class="nav-item flex flex-col items-center p-2" onclick="switchTab('markets')">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M16 6l2.29 2.29-4.88 4.88-4-4L2 16.59 3.41 18l6-6 4 4 6.3-6.29L22 12V6z"/>
                </svg>
                <span class="text-xs mt-1">Markets</span>
            </button>
            <button class="nav-item flex flex-col items-center p-2" onclick="switchTab('alerts')">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                    <path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/>
                    <path d="M13.73 21a2 2 0 0 1-3.46 0"/>
                </svg>
                <span class="text-xs mt-1">Alerts</span>
            </button>
            <button class="nav-item flex flex-col items-center p-2" onclick="switchTab('monitoring')">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
                    <circle cx="12" cy="12" r="3"/>
                    <path d="M12 1v6m0 6v6m11-7h-6m-6 0H1"/>
                </svg>
                <span class="text-xs mt-1">Monitor</span>
            </button>
        </div>
    </div>

    <!-- Alert Notifications -->
    <div id="notifications" class="fixed top-20 right-4 space-y-2 z-40 max-w-80"></div>


    <script>
        // Global variables
        let alerts = JSON.parse(localStorage.getItem('cryptoAlerts')) || [];
        let recentAlerts = JSON.parse(localStorage.getItem('recentAlerts')) || [];
        let currentPrices = {};
        let updateInterval;
        let triggeredToday = parseInt(localStorage.getItem('triggeredToday')) || 0;
        let lastResetDate = localStorage.getItem('lastResetDate') || new Date().toDateString();

        // Tab switching functionality
        function switchTab(tabName) {
            // Hide all tab contents
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // Remove active class from all nav items
            document.querySelectorAll('.nav-item').forEach(item => {
                item.classList.remove('active');
            });
            
            // Show selected tab
            document.getElementById(tabName + 'Tab').classList.add('active');
            
            // Add active class to clicked nav item
            event.target.closest('.nav-item').classList.add('active');
        }

        // Update home tab stats
        function updateHomeStats() {
            document.getElementById('homeAlertCount').textContent = alerts.length;
            document.getElementById('homeTriggeredToday').textContent = triggeredToday;
            
            // Update home crypto list
            const homeTopCryptos = document.getElementById('homeTopCryptos');
            const cryptos = ['bitcoin', 'ethereum', 'tether'];
            
            homeTopCryptos.innerHTML = cryptos.map(crypto => {
                const price = currentPrices[crypto] || 0;
                const priceElement = document.getElementById(price-${crypto});
                const changeElement = document.getElementById(change-${crypto});
                
                const priceText = priceElement ? priceElement.textContent : 'Loading...';
                const changeText = changeElement ? changeElement.textContent : '-';
                const changeClass = changeElement ? changeElement.className : '';
                
                const cryptoNames = {
                    bitcoin: 'Bitcoin',
                    ethereum: 'Ethereum', 
                    tether: 'Tether'
                };
                
                const cryptoSymbols = {
                    bitcoin: 'BTC',
                    ethereum: 'ETH',
                    tether: 'USDT'
                };
                
                return `
                    <div class="flex items-center justify-between p-3 bg-white/5 rounded-lg">
                        <div>
                            <div class="font-medium text-white text-sm">${cryptoNames[crypto]}</div>
                            <div class="text-xs text-white/60">${cryptoSymbols[crypto]}</div>
                        </div>
                        <div class="text-right">
                            <div class="font-bold text-white text-sm">${priceText}</div>
                            <div class="text-xs ${changeClass.includes('green') ? 'text-green-400' : 'text-red-400'}">${changeText}</div>
                        </div>
                    </div>
                `;
            }).join('');
        }

        // Initialize the app
        document.addEventListener('DOMContentLoaded', function() {
            // Reset daily counter if it's a new day
            if (lastResetDate !== new Date().toDateString()) {
                triggeredToday = 0;
                localStorage.setItem('triggeredToday', '0');
                localStorage.setItem('lastResetDate', new Date().toDateString());
            }
            
            loadPrices();
            loadMarketStats();
            renderAlerts();
            renderRecentAlerts();
            updateMonitoringStats();
            updateHomeStats();
            
            // Start auto-refresh every 30 seconds
            updateInterval = setInterval(() => {
                loadPrices();
                loadMarketStats();
                updateMonitoringStats();
                updateHomeStats();
            }, 30000);

            // Event listeners
            document.getElementById('alertForm').addEventListener('submit', addAlert);
            document.getElementById('cryptoSearchBtn').addEventListener('click', searchCrypto);
            document.getElementById('clearAllAlerts').addEventListener('click', clearAllAlerts);
            document.getElementById('cryptoSearch').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    searchCrypto();
                }
            });
        });

        // Load cryptocurrency prices
        async function loadPrices() {
            try {
                const cryptos = ['bitcoin', 'ethereum', 'tether', 'binancecoin', 'solana'];
                const response = await fetch(https://api.coingecko.com/api/v3/simple/price?ids=${cryptos.join(',')}&vs_currencies=usd&include_24hr_change=true);
                const data = await response.json();
                
                cryptos.forEach(crypto => {
                    if (data[crypto]) {
                        const price = data[crypto].usd;
                        const change = data[crypto].usd_24h_change;
                        
                        // Update price display
                        const priceElement = document.getElementById(price-${crypto});
                        const changeElement = document.getElementById(change-${crypto});
                        
                        if (priceElement) {
                            priceElement.textContent = $${price.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2})};
                            priceElement.classList.add('price-flash');
                            setTimeout(() => priceElement.classList.remove('price-flash'), 500);
                        }
                        
                        if (changeElement) {
                            const changeText = ${change >= 0 ? '+' : ''}${change.toFixed(2)}%;
                            changeElement.textContent = changeText;
                            changeElement.className = text-xs mt-1 ${change >= 0 ? 'text-green-400' : 'text-red-400'};
                        }
                        
                        // Store current price and check alerts
                        currentPrices[crypto] = price;
                        checkAlerts(crypto, price);
                    }
                });
            } catch (error) {
                console.error('Error loading prices:', error);
                showNotification('Failed to load prices. Please check your connection.', 'error');
            }
        }

        // Load market statistics
        async function loadMarketStats() {
            try {
                const response = await fetch('https://api.coingecko.com/api/v3/global');
                const data = await response.json();
                
                if (data.data) {
                    const marketCap = data.data.total_market_cap.usd;
                    const volume = data.data.total_volume.usd;
                    const btcDominance = data.data.market_cap_percentage.btc;
                    
                    document.getElementById('marketCap').textContent = $${(marketCap / 1e12).toFixed(2)}T;
                    document.getElementById('volume24h').textContent = $${(volume / 1e9).toFixed(1)}B;
                    document.getElementById('btcDominance').textContent = ${btcDominance.toFixed(1)}%;
                }
            } catch (error) {
                console.error('Error loading market stats:', error);
            }
        }

        // Search for cryptocurrencies
        async function searchCrypto() {
            const query = document.getElementById('cryptoSearch').value.trim().toLowerCase();
            if (!query) return;

            try {
                const response = await fetch(https://api.coingecko.com/api/v3/simple/price?ids=${query}&vs_currencies=usd&include_24hr_change=true);
                const data = await response.json();
                
                const resultsContainer = document.getElementById('searchResults');
                const resultsGrid = document.getElementById('searchResultsGrid');
                
                if (Object.keys(data).length > 0) {
                    resultsGrid.innerHTML = '';
                    
                    Object.entries(data).forEach(([id, priceData]) => {
                        const price = priceData.usd;
                        const change = priceData.usd_24h_change || 0;
                        
                        const resultCard = document.createElement('div');
                        resultCard.className = 'flex items-center justify-between p-3 bg-white/5 rounded-lg border border-white/10 slide-in';
                        resultCard.innerHTML = `
                            <div>
                                <div class="font-medium capitalize text-white">${id.replace('-', ' ')}</div>
                                <div class="text-xs text-white/60">${id.toUpperCase()}</div>
                            </div>
                            <div class="text-right">
                                <div class="font-bold text-white">$${price.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2})}</div>
                                <div class="text-xs ${change >= 0 ? 'text-green-400' : 'text-red-400'}">
                                    ${change >= 0 ? '+' : ''}${change.toFixed(2)}%
                                </div>
                            </div>
                        `;
                        resultsGrid.appendChild(resultCard);
                    });
                    
                    resultsContainer.classList.remove('hidden');
                } else {
                    showNotification('Cryptocurrency not found. Try searching for "bitcoin", "ethereum", etc.', 'error');
                }
            } catch (error) {
                console.error('Error searching crypto:', error);
                showNotification('Search failed. Please try again.', 'error');
            }
        }

        // Add new price alert
        function addAlert(e) {
            e.preventDefault();
            
            const crypto = document.getElementById('alertCrypto').value;
            const type = document.getElementById('alertType').value;
            const price = parseFloat(document.getElementById('alertPrice').value);
            
            if (!crypto || !price) {
                showNotification('Please select a cryptocurrency and enter a price', 'error');
                return;
            }
            
            // Check for duplicate alerts
            const duplicate = alerts.find(alert => 
                alert.crypto === crypto && 
                alert.type === type && 
                alert.price === price
            );
            
            if (duplicate) {
                showNotification('This alert already exists', 'error');
                return;
            }
            
            const alert = {
                id: Date.now(),
                crypto: crypto,
                type: type,
                price: price,
                created: new Date().toLocaleString()
            };
            
            alerts.push(alert);
            localStorage.setItem('cryptoAlerts', JSON.stringify(alerts));
            
            renderAlerts();
            updateMonitoringStats();
            document.getElementById('alertForm').reset();
            
            const cryptoName = crypto.replace('-', ' ').replace(/\b\w/g, l => l.toUpperCase());
            showNotification(Alert created for ${cryptoName} ${type} $${price.toLocaleString()}, 'success');
        }

        // Update monitoring statistics
        function updateMonitoringStats() {
            document.getElementById('alertCount').textContent = alerts.length;
            document.getElementById('triggeredToday').textContent = triggeredToday;
            document.getElementById('lastUpdate').textContent = new Date().toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
        }

        // Clear all alerts
        function clearAllAlerts() {
            if (alerts.length === 0) return;
            
            if (confirm('Are you sure you want to remove all alerts?')) {
                alerts = [];
                localStorage.setItem('cryptoAlerts', JSON.stringify(alerts));
                renderAlerts();
                updateMonitoringStats();
                showNotification('All alerts cleared', 'success');
            }
        }

        // Render recent alerts
        function renderRecentAlerts() {
            const recentAlertsList = document.getElementById('recentAlerts');
            
            if (recentAlerts.length === 0) {
                recentAlertsList.innerHTML = `
                    <div class="text-center text-white/60 py-8">
                        No recent alerts triggered. Your alerts will appear here when they activate.
                    </div>
                `;
                return;
            }
            
            // Show only the last 5 recent alerts
            const displayAlerts = recentAlerts.slice(-5).reverse();
            
            recentAlertsList.innerHTML = displayAlerts.map(alert => {
                const statusColor = alert.status === 'failed' ? 'text-red-400' : 'text-green-400';
                const statusIcon = alert.status === 'failed' ? '❌' : '✅';
                const statusText = alert.status === 'failed' ? 'FAILED' : 'SUCCESS';
                
                return `
                    <div class="p-3 bg-white/5 rounded-lg border border-white/10 slide-in">
                        <div class="flex items-center justify-between mb-2">
                            <div class="font-medium capitalize ${statusColor} text-sm">${statusIcon} ${alert.crypto.replace('-', ' ')}</div>
                            <div class="text-xs text-white/40">${alert.triggeredAt}</div>
                        </div>
                        <div class="text-xs text-white/80 mb-1">
                            Target: ${alert.type} $${alert.targetPrice.toLocaleString()}
                        </div>
                        <div class="text-xs text-white/60 mb-1">
                            Actual: $${alert.currentPrice.toLocaleString()}
                        </div>
                        <div class="text-xs ${statusColor}">
                            ${statusText}
                        </div>
                    </div>
                `;
            }).join('');
        }

        // Render active alerts
        function renderAlerts() {
            const alertsList = document.getElementById('alertsList');
            
            if (alerts.length === 0) {
                alertsList.innerHTML = `
                    <div class="text-center text-white/60 py-8">
                        No active alerts. Create one above to get started!
                    </div>
                `;
                return;
            }
            
            alertsList.innerHTML = alerts.map(alert => `
                <div class="p-3 bg-white/5 rounded-lg border border-white/10">
                    <div class="flex items-center justify-between mb-2">
                        <div class="font-medium capitalize text-white">${alert.crypto.replace('-', ' ')}</div>
                        <div class="text-xs px-2 py-1 bg-green-500/20 text-green-400 rounded">Active</div>
                    </div>
                    <div class="text-sm text-white/60 mb-2">
                        Alert when price goes ${alert.type} $${alert.price.toLocaleString()}
                    </div>
                    <div class="flex items-center justify-between">
                        <div class="text-xs text-white/40">Created: ${alert.created}</div>
                        <button onclick="removeAlert(${alert.id})" class="px-3 py-1 bg-red-500/20 hover:bg-red-500/30 text-red-400 rounded-lg text-xs transition-all duration-200">
                            Remove
                        </button>
                    </div>
                </div>
            `).join('');
        }

        // Remove alert
        function removeAlert(alertId) {
            alerts = alerts.filter(alert => alert.id !== alertId);
            localStorage.setItem('cryptoAlerts', JSON.stringify(alerts));
            renderAlerts();
            updateMonitoringStats();
            showNotification('Alert removed', 'success');
        }

        // Check if any alerts should be triggered
        function checkAlerts(crypto, currentPrice) {
            alerts.forEach(alert => {
                if (alert.crypto === crypto) {
                    let triggered = false;
                    
                    if (alert.type === 'above' && currentPrice >= alert.price) {
                        triggered = true;
                    } else if (alert.type === 'below' && currentPrice <= alert.price) {
                        triggered = true;
                    }
                    
                    if (triggered) {
                        // Simulate random success/failure for demonstration
                        const isSuccess = Math.random() > 0.2; // 80% success rate
                        
                        // Add to recent alerts
                        const recentAlert = {
                            id: Date.now(),
                            crypto: crypto,
                            type: alert.type,
                            targetPrice: alert.price,
                            currentPrice: currentPrice,
                            triggeredAt: new Date().toLocaleString(),
                            status: isSuccess ? 'success' : 'failed'
                        };
                        
                        recentAlerts.push(recentAlert);
                        
                        // Keep only last 10 recent alerts
                        if (recentAlerts.length > 10) {
                            recentAlerts = recentAlerts.slice(-10);
                        }
                        
                        localStorage.setItem('recentAlerts', JSON.stringify(recentAlerts));
                        renderRecentAlerts();
                        
                        // Update triggered count
                        triggeredToday++;
                        localStorage.setItem('triggeredToday', triggeredToday.toString());
                        
                        // Remove triggered alert
                        removeAlert(alert.id);
                    }
                }
            });
        }

        // Show notification
        function showNotification(message, type = 'info') {
            const notification = document.createElement('div');
            const bgColor = type === 'error' ? 'bg-red-500' : type === 'alert' ? 'bg-orange-500 alert-pulse' : 'bg-green-500';
            
            notification.className = ${bgColor} text-white px-6 py-3 rounded-lg shadow-lg slide-in max-w-sm;
            notification.textContent = message;
            
            document.getElementById('notifications').appendChild(notification);
            
            // Auto-remove after 5 seconds
            setTimeout(() => {
                notification.remove();
            }, 5000);
        }

        // Format large numbers
        function formatNumber(num) {
            if (num >= 1e12) return (num / 1e12).toFixed(2) + 'T';
            if (num >= 1e9) return (num / 1e9).toFixed(2) + 'B';
            if (num >= 1e6) return (num / 1e6).toFixed(2) + 'M';
            return num.toLocaleString();
        }
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'981f80a813927679',t:'MTc1ODM1MjIyMi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
