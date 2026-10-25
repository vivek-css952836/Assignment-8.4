<!DOCTYPE html>
<html lang="en" class="h-full bg-slate-900 text-slate-100">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Assignment 8.4 - Grid & Flexbox Dashboard</title>
  <!-- Tailwind CSS CDN for visual utilities and icon integration -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Lucide Icons -->
  <script src="https://unpkg.com/lucide@latest"></script>
  <style>
    /* ==========================================================================
       ASSIGNMENT 8.4 CORE CSS: GRID & FLEXBOX LAYOUT DEMONSTRATION
       ========================================================================== */

    /* 1. OUTER PAGE LAYOUT WITH CSS GRID */
    .dashboard-grid {
      display: grid;
      grid-template-areas:
        "header header"
        "sidebar main";
      grid-template-columns: 260px 1fr;
      grid-template-rows: 70px 1fr;
      min-height: 100vh;
      transition: all 0.3s ease-in-out;
    }

    .grid-header {
      grid-area: header;
      z-index: 30;
    }

    .grid-sidebar {
      grid-area: sidebar;
      z-index: 20;
    }

    .grid-main {
      grid-area: main;
      overflow-y: auto;
    }

    /* Responsive Grid Adjustments for Mobile Viewports */
    @media (max-width: 1024px) {
      .dashboard-grid {
        grid-template-areas:
          "header"
          "main";
        grid-template-columns: 1fr;
        grid-template-rows: 70px 1fr;
      }

      .grid-sidebar {
        position: fixed;
        top: 70px;
        left: -260px;
        bottom: 0;
        width: 260px;
        transition: left 0.3s ease;
      }

      .grid-sidebar.active {
        left: 0;
      }
    }

    /* 2. STATISTIC CARDS AND FLEXBOX ALIGNMENTS */
    .stats-grid-container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
      gap: 1.25rem;
    }

    /* Inner Flexbox Card Layout */
    .flex-stat-card {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      border-radius: 0.75rem;
      padding: 1.25rem;
      background-color: #1e293b; /* bg-slate-800 */
      border: 1px solid #334155; /* border-slate-700 */
      transition: transform 0.2s ease, box-shadow 0.2s ease;
    }

    .flex-stat-card:hover {
      transform: translateY(-3px);
      box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.4);
    }

    /* Card Top Row Flexbox Alignment */
    .flex-card-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    /* Icon Box Flexbox Alignment */
    .flex-icon-box {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 2.75rem;
      height: 2.75rem;
      border-radius: 0.5rem;
    }

    /* Metric & Badge Flexbox Alignment */
    .flex-card-body {
      display: flex;
      align-items: baseline;
      justify-content: space-between;
      margin-top: 1rem;
    }

    /* Badge Alignment */
    .flex-badge {
      display: flex;
      align-items: center;
      gap: 0.25rem;
      padding: 0.25rem 0.5rem;
      border-radius: 9999px;
      font-size: 0.75rem;
      font-weight: 600;
    }

    /* 3. FLEXBOX NAVIGATION LIST */
    .flex-nav-list {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }

    .flex-nav-item {
      display: flex;
      align-items: center;
      gap: 0.75rem;
      padding: 0.75rem 1rem;
      border-radius: 0.5rem;
      color: #94a3b8;
      transition: all 0.2s ease;
      text-decoration: none;
    }

    .flex-nav-item:hover, .flex-nav-item.active {
      color: #ffffff;
      background-color: #334155;
    }

    /* Custom Scrollbar for smooth aesthetics */
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: #0f172a;
    }
    ::-webkit-scrollbar-thumb {
      background: #334155;
      border-radius: 3px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #475569;
    }
  </style>
</head>
<body class="h-full bg-slate-900 font-sans text-slate-100 antialiased selection:bg-indigo-500 selection:text-white">

  <!-- ==========================================
       MAIN DASHBOARD GRID LAYOUT
       ========================================== -->
  <div class="dashboard-grid">

    <!-- 1. HEADER (CSS Grid Area: header) -->
    <header class="grid-header bg-slate-800/90 border-b border-slate-700/80 backdrop-blur px-4 lg:px-6 flex items-center justify-between">
      <!-- Left side: Mobile Toggle & Title -->
      <div class="flex items-center gap-3">
        <button id="sidebarToggle" class="lg:hidden p-2 text-slate-400 hover:text-white rounded-lg hover:bg-slate-700 focus:outline-none">
          <i data-lucide="menu" class="w-6 h-6"></i>
        </button>
        <div class="flex items-center gap-2">
          <div class="w-9 h-9 rounded-lg bg-indigo-600 flex items-center justify-center font-bold text-white shadow-lg shadow-indigo-500/30">
            <i data-lucide="layout-grid" class="w-5 h-5"></i>
          </div>
          <div>
            <h1 class="text-base font-bold text-white leading-tight">DevGrid Pro</h1>
            <p class="text-xs text-slate-400 hidden sm:block">Assignment 8.4 • Dashboard</p>
          </div>
        </div>
      </div>

      <!-- Center / Right Controls -->
      <div class="flex items-center gap-3 sm:gap-4">
        <!-- Submission Modal Trigger Button -->
        <button onclick="openCodeModal()" class="flex items-center gap-2 bg-indigo-600 hover:bg-indigo-500 text-white text-xs sm:text-sm font-semibold px-3.5 py-2 rounded-lg shadow-md transition-all border border-indigo-400/30 hover:shadow-indigo-500/20">
          <i data-lucide="code" class="w-4 h-4"></i>
          <span>View Submission Code</span>
        </button>

        <!-- User Profile Pill (Flexbox) -->
        <div class="flex items-center gap-3 border-l border-slate-700 pl-4">
          <div class="relative">
            <img src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&w=120&q=80" alt="Avatar" class="w-9 h-9 rounded-full object-cover ring-2 ring-slate-700">
            <span class="absolute bottom-0 right-0 w-2.5 h-2.5 bg-emerald-500 rounded-full ring-2 ring-slate-800"></span>
          </div>
          <div class="hidden md:block text-left">
            <div class="text-sm font-semibold text-slate-200">Alex Morgan</div>
            <div class="text-xs text-slate-400">Web Developer</div>
          </div>
        </div>
      </div>
    </header>

    <!-- 2. SIDEBAR NAVIGATION (CSS Grid Area: sidebar) -->
    <aside id="sidebar" class="grid-sidebar bg-slate-800 border-r border-slate-700/80 p-4 flex flex-col justify-between">
      <div>
        <!-- Sidebar Navigation (Flexbox vertical container) -->
        <div class="text-xs font-semibold text-slate-400 uppercase tracking-wider mb-3 px-3">Main Navigation</div>
        <nav class="flex-nav-list">
          <a href="#" class="flex-nav-item active">
            <i data-lucide="layout-dashboard" class="w-5 h-5 text-indigo-400"></i>
            <span class="font-medium text-sm">Dashboard</span>
          </a>
          <a href="#" class="flex-nav-item">
            <i data-lucide="bar-chart-3" class="w-5 h-5"></i>
            <span class="font-medium text-sm">Analytics</span>
          </a>
          <a href="#" class="flex-nav-item">
            <i data-lucide="activity" class="w-5 h-5"></i>
            <span class="font-medium text-sm">Activity Feed</span>
          </a>
          <a href="#" class="flex-nav-item">
            <i data-lucide="settings" class="w-5 h-5"></i>
            <span class="font-medium text-sm">Settings</span>
          </a>
        </nav>

        <div class="text-xs font-semibold text-slate-400 uppercase tracking-wider mt-8 mb-3 px-3">Grid & Flexbox Info</div>
        <div class="bg-slate-900/60 border border-slate-700/50 rounded-lg p-3 text-xs text-slate-300 space-y-2">
          <div class="flex items-center gap-2 text-indigo-400 font-semibold">
            <i data-lucide="grid" class="w-4 h-4"></i> CSS Grid Active
          </div>
          <p class="text-slate-400 leading-relaxed">Outer page uses 2-column, 2-row grid layout template areas.</p>
          <div class="flex items-center gap-2 text-emerald-400 font-semibold pt-1">
            <i data-lucide="move" class="w-4 h-4"></i> Flexbox Active
          </div>
          <p class="text-slate-400 leading-relaxed">Card elements, icons, headers & badges aligned with flex.</p>
        </div>
      </div>

      <!-- Sidebar Footer Badge -->
      <div class="pt-4 border-t border-slate-700/60 flex items-center justify-between text-xs text-slate-400">
        <span>Assignment Status</span>
        <span class="px-2 py-0.5 rounded bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 font-medium">Completed</span>
      </div>
    </aside>

    <!-- 3. MAIN CONTENT AREA (CSS Grid Area: main) -->
    <main class="grid-main p-4 sm:p-6 lg:p-8 space-y-6">

      <!-- Welcome Banner Section (Flexbox) -->
      <section class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 bg-gradient-to-r from-indigo-900/40 via-slate-800 to-slate-800 border border-indigo-500/20 rounded-xl p-5 sm:p-6 shadow-sm">
        <div>
          <h2 class="text-xl sm:text-2xl font-bold text-white flex items-center gap-2">
            Welcome back, Student! <span class="inline-block animate-bounce">👋</span>
          </h2>
          <p class="text-sm text-slate-300 mt-1">Here is an overview of your CSS Grid & Flexbox dashboard architecture.</p>
        </div>
        <div class="flex items-center gap-2">
          <button class="flex items-center gap-1.5 px-3.5 py-2 bg-slate-700/80 hover:bg-slate-700 text-slate-200 text-xs font-semibold rounded-lg border border-slate-600 transition">
            <i data-lucide="calendar" class="w-4 h-4"></i>
            <span>Today: Oct 25</span>
          </button>
          <button class="flex items-center gap-1.5 px-3.5 py-2 bg-slate-700/80 hover:bg-slate-700 text-slate-200 text-xs font-semibold rounded-lg border border-slate-600 transition">
            <i data-lucide="download" class="w-4 h-4"></i>
            <span>Export Data</span>
          </button>
        </div>
      </section>

      <!-- SECTION 1: 4 STATISTIC CARDS (Aligned internally using FLEXBOX) -->
      <section class="space-y-3">
        <div class="flex items-center justify-between">
          <h3 class="text-base font-semibold text-slate-200 flex items-center gap-2">
            <i data-lucide="layers" class="w-4 h-4 text-indigo-400"></i>
            Key Statistics Cards (Flexbox Internal Alignment)
          </h3>
          <span class="text-xs text-slate-400">Auto-responsive grid container</span>
        </div>

        <div class="stats-grid-container">

          <!-- Card 1: Total Revenue -->
          <div class="flex-stat-card">
            <div class="flex-card-header">
              <span class="text-xs font-medium text-slate-400 uppercase tracking-wide">Total Revenue</span>
              <div class="flex-icon-box bg-indigo-500/10 text-indigo-400 border border-indigo-500/20">
                <i data-lucide="dollar-sign" class="w-5 h-5"></i>
              </div>
            </div>
            <div class="flex-card-body">
              <span class="text-2xl font-bold text-white">$45,231.89</span>
              <div class="flex-badge bg-emerald-500/10 text-emerald-400 border border-emerald-500/20">
                <i data-lucide="trending-up" class="w-3.5 h-3.5"></i>
                <span>+12.5%</span>
              </div>
            </div>
          </div>

          <!-- Card 2: Active Users -->
          <div class="flex-stat-card">
            <div class="flex-card-header">
              <span class="text-xs font-medium text-slate-400 uppercase tracking-wide">Active Users</span>
              <div class="flex-icon-box bg-blue-500/10 text-blue-400 border border-blue-500/20">
                <i data-lucide="users" class="w-5 h-5"></i>
              </div>
            </div>
            <div class="flex-card-body">
              <span class="text-2xl font-bold text-white">2,350</span>
              <div class="flex-badge bg-emerald-500/10 text-emerald-400 border border-emerald-500/20">
                <i data-lucide="trending-up" class="w-3.5 h-3.5"></i>
                <span>+8.2%</span>
              </div>
            </div>
          </div>

          <!-- Card 3: New Orders -->
          <div class="flex-stat-card">
            <div class="flex-card-header">
              <span class="text-xs font-medium text-slate-400 uppercase tracking-wide">New Orders</span>
              <div class="flex-icon-box bg-amber-500/10 text-amber-400 border border-amber-500/20">
                <i data-lucide="shopping-cart" class="w-5 h-5"></i>
              </div>
            </div>
            <div class="flex-card-body">
              <span class="text-2xl font-bold text-white">+12,234</span>
              <div class="flex-badge bg-rose-500/10 text-rose-400 border border-rose-500/20">
                <i data-lucide="trending-down" class="w-3.5 h-3.5"></i>
                <span>-2.4%</span>
              </div>
            </div>
          </div>

          <!-- Card 4: Conversion Rate -->
          <div class="flex-stat-card">
            <div class="flex-card-header">
              <span class="text-xs font-medium text-slate-400 uppercase tracking-wide">Conversion Rate</span>
              <div class="flex-icon-box bg-emerald-500/10 text-emerald-400 border border-emerald-500/20">
                <i data-lucide="percent" class="w-5 h-5"></i>
              </div>
            </div>
            <div class="flex-card-body">
              <span class="text-2xl font-bold text-white">3.18%</span>
              <div class="flex-badge bg-emerald-500/10 text-emerald-400 border border-emerald-500/20">
                <i data-lucide="trending-up" class="w-3.5 h-3.5"></i>
                <span>+4.6%</span>
              </div>
            </div>
          </div>

        </div>
      </section>

      <!-- SECTION 2 & 3: DATA TABLE & RECENT ACTIVITY FEED -->
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">

        <!-- Recent Transactions Table (Spans 2 columns on large screens) -->
        <div class="lg:col-span-2 bg-slate-800 border border-slate-700/80 rounded-xl p-5 flex flex-col justify-between space-y-4">
          <div>
            <div class="flex items-center justify-between pb-3 border-b border-slate-700/60">
              <div>
                <h3 class="text-base font-semibold text-white flex items-center gap-2">
                  <i data-lucide="shopping-bag" class="w-4 h-4 text-indigo-400"></i>
                  Recent Orders & Transactions
                </h3>
                <p class="text-xs text-slate-400">Latest activity registered in your store</p>
              </div>
              <button class="text-xs text-indigo-400 hover:text-indigo-300 font-medium">View All</button>
            </div>

            <!-- Table Responsive Wrapper -->
            <div class="overflow-x-auto mt-4">
              <table class="w-full text-left text-sm text-slate-300">
                <thead class="text-xs text-slate-400 uppercase bg-slate-900/50 rounded-lg">
                  <tr>
                    <th class="px-4 py-3 rounded-l-lg">Order ID</th>
                    <th class="px-4 py-3">Customer</th>
                    <th class="px-4 py-3">Status</th>
                    <th class="px-4 py-3">Amount</th>
                    <th class="px-4 py-3 rounded-r-lg text-right">Date</th>
                  </tr>
                </thead>
                <tbody class="divide-y divide-slate-700/50">
                  <tr class="hover:bg-slate-700/30 transition-colors">
                    <td class="px-4 py-3.5 font-mono text-xs text-indigo-300 font-semibold">#ORD-9482</td>
                    <td class="px-4 py-3.5">
                      <div class="flex items-center gap-2.5">
                        <div class="w-7 h-7 rounded-full bg-slate-700 flex items-center justify-center font-bold text-xs text-slate-200">JD</div>
                        <span class="font-medium text-white">Jane Doe</span>
                      </div>
                    </td>
                    <td class="px-4 py-3.5">
                      <span class="inline-flex items-center gap-1.5 px-2.5 py-1 rounded-full text-xs font-medium bg-emerald-500/10 text-emerald-400 border border-emerald-500/20">
                        <span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span> Completed
                      </span>
                    </td>
                    <td class="px-4 py-3.5 font-medium text-white">$240.00</td>
                    <td class="px-4 py-3.5 text-right text-xs text-slate-400">Oct 25, 2026</td>
                  </tr>
                  <tr class="hover:bg-slate-700/30 transition-colors">
                    <td class="px-4 py-3.5 font-mono text-xs text-indigo-300 font-semibold">#ORD-9481</td>
                    <td class="px-4 py-3.5">
                      <div class="flex items-center gap-2.5">
                        <div class="w-7 h-7 rounded-full bg-slate-700 flex items-center justify-center font-bold text-xs text-slate-200">MS</div>
                        <span class="font-medium text-white">Michael Scott</span>
                      </div>
                    </td>
                    <td class="px-4 py-3.5">
                      <span class="inline-flex items-center gap-1.5 px-2.5 py-1 rounded-full text-xs font-medium bg-amber-500/10 text-amber-400 border border-amber-500/20">
                        <span class="w-1.5 h-1.5 rounded-full bg-amber-400"></span> Pending
                      </span>
                    </td>
                    <td class="px-4 py-3.5 font-medium text-white">$1,120.50</td>
                    <td class="px-4 py-3.5 text-right text-xs text-slate-400">Oct 25, 2026</td>
                  </tr>
                  <tr class="hover:bg-slate-700/30 transition-colors">
                    <td class="px-4 py-3.5 font-mono text-xs text-indigo-300 font-semibold">#ORD-9480</td>
                    <td class="px-4 py-3.5">
                      <div class="flex items-center gap-2.5">
                        <div class="w-7 h-7 rounded-full bg-slate-700 flex items-center justify-center font-bold text-xs text-slate-200">EC</div>
                        <span class="font-medium text-white">Emily Clarke</span>
                      </div>
                    </td>
                    <td class="px-4 py-3.5">
                      <span class="inline-flex items-center gap-1.5 px-2.5 py-1 rounded-full text-xs font-medium bg-emerald-500/10 text-emerald-400 border border-emerald-500/20">
                        <span class="w-1.5 h-1.5 rounded-full bg-emerald-400"></span> Completed
                      </span>
                    </td>
                    <td class="px-4 py-3.5 font-medium text-white">$85.20</td>
                    <td class="px-4 py-3.5 text-right text-xs text-slate-400">Oct 24, 2026</td>
                  </tr>
                  <tr class="hover:bg-slate-700/30 transition-colors">
                    <td class="px-4 py-3.5 font-mono text-xs text-indigo-300 font-semibold">#ORD-9479</td>
                    <td class="px-4 py-3.5">
                      <div class="flex items-center gap-2.5">
                        <div class="w-7 h-7 rounded-full bg-slate-700 flex items-center justify-center font-bold text-xs text-slate-200">BH</div>
                        <span class="font-medium text-white">Bruce Wayne</span>
                      </div>
                    </td>
                    <td class="px-4 py-3.5">
                      <span class="inline-flex items-center gap-1.5 px-2.5 py-1 rounded-full text-xs font-medium bg-rose-500/10 text-rose-400 border border-rose-500/20">
                        <span class="w-1.5 h-1.5 rounded-full bg-rose-400"></span> Cancelled
                      </span>
                    </td>
                    <td class="px-4 py-3.5 font-medium text-white">$4,500.00</td>
                    <td class="px-4 py-3.5 text-right text-xs text-slate-400">Oct 24, 2026</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <!-- Recent Activity Feed Sidebar (Flexbox list layout) -->
        <div class="bg-slate-800 border border-slate-700/80 rounded-xl p-5 flex flex-col justify-between">
          <div>
            <div class="flex items-center justify-between pb-3 border-b border-slate-700/60">
              <h3 class="text-base font-semibold text-white flex items-center gap-2">
                <i data-lucide="activity" class="w-4 h-4 text-emerald-400"></i>
                Recent Activity
              </h3>
              <span class="text-xs text-slate-400">Real-time updates</span>
            </div>

            <!-- Activity List (Flexbox) -->
            <div class="mt-4 space-y-4">
              <!-- Item 1 -->
              <div class="flex items-start gap-3">
                <div class="w-8 h-8 rounded-full bg-indigo-500/10 text-indigo-400 border border-indigo-500/20 flex items-center justify-center shrink-0">
                  <i data-lucide="user-plus" class="w-4 h-4"></i>
                </div>
                <div class="text-xs">
                  <p class="text-slate-200"><span class="font-semibold text-white">Sarah Connor</span> created a new account.</p>
                  <span class="text-slate-400 text-[10px]">10 minutes ago</span>
                </div>
              </div>

              <!-- Item 2 -->
              <div class="flex items-start gap-3">
                <div class="w-8 h-8 rounded-full bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 flex items-center justify-center shrink-0">
                  <i data-lucide="check-circle" class="w-4 h-4"></i>
                </div>
                <div class="text-xs">
                  <p class="text-slate-200">Server backup completed successfully.</p>
                  <span class="text-slate-400 text-[10px]">42 minutes ago</span>
                </div>
              </div>

              <!-- Item 3 -->
              <div class="flex items-start gap-3">
                <div class="w-8 h-8 rounded-full bg-amber-500/10 text-amber-400 border border-amber-500/20 flex items-center justify-center shrink-0">
                  <i data-lucide="alert-triangle" class="w-4 h-4"></i>
                </div>
                <div class="text-xs">
                  <p class="text-slate-200">High API traffic threshold reached.</p>
                  <span class="text-slate-400 text-[10px]">2 hours ago</span>
                </div>
              </div>

              <!-- Item 4 -->
              <div class="flex items-start gap-3">
                <div class="w-8 h-8 rounded-full bg-blue-500/10 text-blue-400 border border-blue-500/20 flex items-center justify-center shrink-0">
                  <i data-lucide="credit-card" class="w-4 h-4"></i>
                </div>
                <div class="text-xs">
                  <p class="text-slate-200">Payout of <span class="font-semibold text-white">$1,240.00</span> processed.</p>
                  <span class="text-slate-400 text-[10px]">5 hours ago</span>
                </div>
              </div>
            </div>
          </div>

          <div class="mt-6 pt-3 border-t border-slate-700/60">
            <button class="w-full py-2 bg-slate-700/50 hover:bg-slate-700 text-slate-300 hover:text-white rounded-lg text-xs font-semibold transition flex items-center justify-center gap-1">
              <span>View Activity Log</span>
              <i data-lucide="chevron-right" class="w-3.5 h-3.5"></i>
            </button>
          </div>
        </div>

      </div>

    </main>
  </div>

  <!-- ==========================================
       SUBMISSION CODE MODAL (HTML & CSS)
       ========================================== -->
  <div id="codeModal" class="fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
    <div class="bg-slate-900 border border-slate-700 rounded-xl max-w-4xl w-full max-h-[85vh] flex flex-col shadow-2xl overflow-hidden">
      <!-- Modal Header -->
      <div class="p-4 bg-slate-800 border-b border-slate-700 flex items-center justify-between">
        <div>
          <h3 class="font-bold text-white text-base flex items-center gap-2">
            <i data-lucide="file-code" class="w-5 h-5 text-indigo-400"></i>
            Assignment 8.4 Submission Code
          </h3>
          <p class="text-xs text-slate-400">Copy the standalone HTML & CSS for your assignment submission</p>
        </div>
        <button onclick="closeCodeModal()" class="text-slate-400 hover:text-white p-1 rounded-lg hover:bg-slate-700">
          <i data-lucide="x" class="w-5 h-5"></i>
        </button>
      </div>

      <!-- Modal Tabs & Copy Button -->
      <div class="bg-slate-900 px-4 py-2 border-b border-slate-800 flex items-center justify-between">
        <div class="flex gap-2">
          <button id="tabCssBtn" onclick="switchTab('css')" class="px-3 py-1.5 rounded-md text-xs font-semibold bg-indigo-600 text-white">CSS (Grid & Flexbox Focus)</button>
          <button id="tabHtmlBtn" onclick="switchTab('html')" class="px-3 py-1.5 rounded-md text-xs font-semibold bg-slate-800 text-slate-400 hover:text-slate-200">Full Combined HTML</button>
        </div>
        <button onclick="copySubmissionCode()" class="flex items-center gap-1.5 text-xs bg-emerald-600 hover:bg-emerald-500 text-white px-3 py-1.5 rounded-md transition font-medium">
          <i data-lucide="copy" class="w-3.5 h-3.5"></i>
          <span id="copyBtnText">Copy Code</span>
        </button>
      </div>

      <!-- Code Box -->
      <div class="p-4 flex-1 overflow-y-auto font-mono text-xs bg-slate-950 text-slate-300">
        <pre id="codeDisplay" class="whitespace-pre-wrap leading-relaxed"></pre>
      </div>

      <!-- Modal Footer -->
      <div class="p-3 bg-slate-800 border-t border-slate-700 flex justify-end">
        <button onclick="closeCodeModal()" class="px-4 py-1.5 bg-slate-700 hover:bg-slate-600 text-slate-200 text-xs rounded-lg font-semibold">
          Close
        </button>
      </div>
    </div>
  </div>

  <!-- JavaScript Interactions -->
  <script>
    // Initialize Lucide Icons
    lucide.createIcons();

    // Responsive Mobile Sidebar Toggle
    const sidebarToggle = document.getElementById('sidebarToggle');
    const sidebar = document.getElementById('sidebar');

    sidebarToggle.addEventListener('click', () => {
      sidebar.classList.toggle('active');
    });

    // Close sidebar when clicking outside on mobile
    document.addEventListener('click', (e) => {
      if (window.innerWidth < 1024) {
        if (!sidebar.contains(e.target) && !sidebarToggle.contains(e.target)) {
          sidebar.classList.remove('active');
        }
      }
    });

    // Code Snippets for Student Assignment Submission
    const cssCodeSnippet = `/* ==========================================================================
   ASSIGNMENT 8.4: GRID & FLEXBOX LAYOUT CSS
   ========================================================================== */

/* 1. OUTER PAGE LAYOUT WITH CSS GRID */
.dashboard-grid {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar main";
  grid-template-columns: 260px 1fr;
  grid-template-rows: 70px 1fr;
  min-height: 100vh;
}

.grid-header  { grid-area: header; }
.grid-sidebar { grid-area: sidebar; }
.grid-main    { grid-area: main; }

/* Responsive Grid for Mobile Screens */
@media (max-width: 1024px) {
  .dashboard-grid {
    grid-template-areas:
      "header"
      "main";
    grid-template-columns: 1fr;
    grid-template-rows: 70px 1fr;
  }
  
  .grid-sidebar {
    position: fixed;
    top: 70px;
    left: -260px;
    bottom: 0;
    width: 260px;
    transition: left 0.3s ease;
  }

  .grid-sidebar.active {
    left: 0;
  }
}

/* 2. STATISTIC CARDS AND FLEXBOX ALIGNMENTS */
.stats-grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1.25rem;
}

/* Inner Card Flexbox Alignment */
.flex-stat-card {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 1.25rem;
  border-radius: 0.75rem;
  background-color: #1e293b;
  border: 1px solid #334155;
}

/* Card Header Flexbox Alignment (Icon & Title) */
.flex-card-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

/* Flexbox Icon Box */
.flex-icon-box {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 2.75rem;
  height: 2.75rem;
  border-radius: 0.5rem;
}

/* Card Metric & Badge Flexbox Alignment */
.flex-card-body {
  display: flex;
  align-items: baseline;
  justify-content: space-between;
  margin-top: 1rem;
}

/* Badge Flexbox Alignment */
.flex-badge {
  display: flex;
  align-items: center;
  gap: 0.25rem;
  padding: 0.25rem 0.5rem;
  border-radius: 9999px;
  font-size: 0.75rem;
  font-weight: 600;
}

/* 3. FLEXBOX NAVIGATION LIST */
.flex-nav-list {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.flex-nav-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem 1rem;
  border-radius: 0.5rem;
  text-decoration: none;
}`;

    let activeTab = 'css';

    function openCodeModal() {
      document.getElementById('codeModal').classList.remove('hidden');
      switchTab('css');
    }

    function closeCodeModal() {
      document.getElementById('codeModal').classList.add('hidden');
    }

    function switchTab(tab) {
      activeTab = tab;
      const cssBtn = document.getElementById('tabCssBtn');
      const htmlBtn = document.getElementById('tabHtmlBtn');
      const display = document.getElementById('codeDisplay');

      if (tab === 'css') {
        cssBtn.className = "px-3 py-1.5 rounded-md text-xs font-semibold bg-indigo-600 text-white";
        htmlBtn.className = "px-3 py-1.5 rounded-md text-xs font-semibold bg-slate-800 text-slate-400 hover:text-slate-200";
        display.textContent = cssCodeSnippet;
      } else {
        htmlBtn.className = "px-3 py-1.5 rounded-md text-xs font-semibold bg-indigo-600 text-white";
        cssBtn.className = "px-3 py-1.5 rounded-md text-xs font-semibold bg-slate-800 text-slate-400 hover:text-slate-200";
        display.textContent = "<!DOCTYPE html>\n" + document.documentElement.outerHTML;
      }
    }

    function copySubmissionCode() {
      const codeText = document.getElementById('codeDisplay').textContent;
      
      // Fallback copy mechanism for iframe environment compatibility
      const textarea = document.createElement('textarea');
      textarea.value = codeText;
      document.body.appendChild(textarea);
      textarea.select();
      document.execCommand('copy');
      document.body.removeChild(textarea);

      const btnText = document.getElementById('copyBtnText');
      btnText.textContent = "Copied!";
      setTimeout(() => {
        btnText.textContent = "Copy Code";
      }, 2000);
    }
  </script>
</body>
</html>