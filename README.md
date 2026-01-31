# TZCHILA
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>דשבורד תזרים - צחילה</title>
    <link href="https://fonts.googleapis.com/css2?family=Heebo:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --bg-primary: #0a0f1c;
            --bg-secondary: #111827;
            --bg-card: #1a2234;
            --border-color: #2a3548;
            --text-primary: #f1f5f9;
            --text-secondary: #94a3b8;
            --text-muted: #64748b;
            --accent-green: #10b981;
            --accent-green-soft: rgba(16, 185, 129, 0.15);
            --accent-red: #ef4444;
            --accent-red-soft: rgba(239, 68, 68, 0.15);
            --accent-blue: #3b82f6;
            --accent-blue-soft: rgba(59, 130, 246, 0.15);
            --accent-yellow: #f59e0b;
            --accent-yellow-soft: rgba(245, 158, 11, 0.15);
            --accent-purple: #8b5cf6;
            --accent-purple-soft: rgba(139, 92, 246, 0.15);
            --radius-sm: 8px;
            --radius-md: 12px;
            --radius-lg: 16px;
        }
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Heebo', sans-serif; background: var(--bg-primary); color: var(--text-primary); min-height: 100vh; }
        .header { background: linear-gradient(135deg, var(--bg-secondary) 0%, var(--bg-card) 100%); border-bottom: 1px solid var(--border-color); padding: 20px 32px; position: sticky; top: 0; z-index: 100; }
        .header-content { max-width: 1600px; margin: 0 auto; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 16px; }
        .logo { display: flex; align-items: center; gap: 16px; }
        .logo-icon { width: 48px; height: 48px; background: linear-gradient(135deg, var(--accent-green) 0%, #059669 100%); border-radius: var(--radius-md); display: flex; align-items: center; justify-content: center; font-size: 24px; }
        .logo-text h1 { font-size: 24px; font-weight: 700; }
        .logo-text span { font-size: 13px; color: var(--text-muted); }
        .btn { padding: 10px 20px; border-radius: var(--radius-sm); font-family: inherit; font-size: 14px; font-weight: 500; cursor: pointer; border: none; display: flex; align-items: center; gap: 8px; }
        .btn-primary { background: linear-gradient(135deg, var(--accent-green) 0%, #059669 100%); color: white; }
        .main-container { max-width: 1600px; margin: 0 auto; padding: 24px 32px; }
        .config-section { background: var(--bg-card); border: 1px solid var(--border-color); border-radius: var(--radius-lg); padding: 24px; margin-bottom: 24px; }
        .config-section h3 { font-size: 16px; font-weight: 600; margin-bottom: 16px; }
        .config-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 16px; }
        .config-item { display: flex; flex-direction: column; gap: 6px; }
        .config-item label { font-size: 13px; color: var(--text-secondary); }
        .config-item input, .config-item select { padding: 12px 16px; background: var(--bg-secondary); border: 1px solid var(--border-color); border-radius: var(--radius-sm); color: var(--text-primary); font-family: inherit; font-size: 14px; }
        .stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 16px; margin-bottom: 24px; }
        .stat-card { background: var(--bg-card); border: 1px solid var(--border-color); border-radius: var(--radius-lg); padding: 20px 24px; }
        .stat-icon { width: 40px; height: 40px; border-radius: var(--radius-sm); display: flex; align-items: center; justify-content: center; font-size: 18px; margin-bottom: 12px; }
        .stat-card.green .stat-icon { background: var(--accent-green-soft); }
        .stat-card.red .stat-icon { background: var(--accent-red-soft); }
        .stat-card.blue .stat-icon { background: var(--accent-blue-soft); }
        .stat-card.purple .stat-icon { background: var(--accent-purple-soft); }
        .stat-value { font-size: 28px; font-weight: 700; margin-bottom: 4px; }
        .stat-label { font-size: 13px; color: var(--text-secondary); }
        .charts-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(400px, 1fr)); gap: 24px; margin-bottom: 24px; }
        .chart-card { background: var(--bg-card); border: 1px solid var(--border-color); border-radius: var(--radius-lg); padding: 24px; }
        .chart-title { font-size: 16px; font-weight: 600; margin-bottom: 20px; }
        .chart-container { height: 280px; }
        .category-section { background: var(--bg-card); border: 1px solid var(--border-color); border-radius: var(--radius-lg); padding: 24px; margin-bottom: 24px; }
        .category-title { font-size: 16px; font-weight: 600; margin-bottom: 20px; }
        .category-item { background: var(--bg-secondary); border-radius: var(--radius-sm); padding: 14px 16px; margin-bottom: 8px; display: flex; justify-content: space-between; align-items: center; }
        .category-name { font-size: 14px; font-weight: 500; }
        .category-amount { font-size: 16px; font-weight: 600; }
        .table-section { background: var(--bg-card); border: 1px solid var(--border-color); border-radius: var(--radius-lg); overflow: hidden; }
        .table-header { padding: 20px 24px; border-bottom: 1px solid var(--border-color); font-size: 16px; font-weight: 600; }
        table { width: 100%; border-collapse: collapse; }
        th { padding: 14px 16px; text-align: right; font-size: 12px; font-weight: 600; color: var(--text-secondary); background: var(--bg-secondary); }
        td { padding: 14px 16px; font-size: 14px; border-bottom: 1px solid var(--border-color); }
        .status-badge { padding: 4px 10px; border-radius: 20px; font-size: 12px; font-weight: 500; }
        .status-badge.completed { background: var(--accent-green-soft); color: var(--accent-green); }
        .status-badge.pending { background: var(--accent-yellow-soft); color: var(--accent-yellow); }
        .type-badge { padding: 4px 8px; border-radius: var(--radius-sm); font-size: 11px; font-weight: 500; }
        .type-badge.income { background: var(--accent-green-soft); color: var(--accent-green); }
        .type-badge.expense { background: var(--accent-red-soft); color: var(--accent-red); }
        .amount-cell.income { color: var(--accent-green); }
        .amount-cell.expense { color: var(--accent-red); }
        .loading { text-align: center; padding: 40px; color: var(--text-muted); }
        .error-msg { background: var(--accent-red-soft); color: var(--accent-red); padding: 16px; border-radius: var(--radius-sm); margin-bottom: 24px; text-align: center; }
        .success-msg { background: var(--accent-green-soft); color: var(--accent-green); padding: 16px; border-radius: var(--radius-sm); margin-bottom: 24px; text-align: center; }
        @media (max-width: 768px) { .main-container { padding: 16px; } .stats-grid { grid-template-columns: repeat(2, 1fr); } .charts-grid { grid-template-columns: 1fr; } }
    </style>
</head>
<body>
    <header class="header">
        <div class="header-content">
            <div class="logo">
                <div class="logo-icon">💰</div>
                <div class="logo-text">
                    <h1>דשבורד תזרים</h1>
                    <span>צחילה • תמיד מקומי • תמיד טרי</span>
                </div>
            </div>
            <div class="header-actions">
                <button class="btn btn-primary" onclick="loadData()">🔄 רענן נתונים</button>
            </div>
        </div>
    </header>
    <div class="main-container">
        <div class="config-section">
            <h3>⚙️ הגדרות</h3>
            <div class="config-grid">
                <div class="config-item">
                    <label>יתרת פתיחה</label>
                    <input type="number" id="openingBalance" value="0" onchange="updateStats()" />
                </div>
                <div class="config-item">
                    <label>חודש נבחר</label>
                    <select id="selectedMonth" onchange="loadData()">
                        <option value="01-2026">ינואר 2026</option>
                        <option value="02-2026">פברואר 2026</option>
                        <option value="03-2026">מרץ 2026</option>
                        <option value="04-2026">אפריל 2026</option>
                        <option value="05-2026">מאי 2026</option>
                        <option value="06-2026">יוני 2026</option>
                        <option value="07-2026">יולי 2026</option>
                        <option value="08-2026">אוגוסט 2026</option>
                        <option value="09-2026">ספטמבר 2026</option>
                        <option value="10-2026">אוקטובר 2026</option>
                        <option value="11-2026">נובמבר 2026</option>
                        <option value="12-2026">דצמבר 2026</option>
                    </select>
                </div>
            </div>
        </div>
        <div id="statusMsg" style="display:none;"></div>
        <div class="stats-grid">
            <div class="stat-card blue"><div class="stat-icon">💵</div><div class="stat-value" id="currentBalance">₪0</div><div class="stat-label">יתרה נוכחית</div></div>
            <div class="stat-card green"><div class="stat-icon">📈</div><div class="stat-value" id="totalIncome">₪0</div><div class="stat-label">סה"כ הכנסות</div></div>
            <div class="stat-card red"><div class="stat-icon">📉</div><div class="stat-value" id="totalExpenses">₪0</div><div class="stat-label">סה"כ הוצאות</div></div>
            <div class="stat-card purple"><div class="stat-icon">📊</div><div class="stat-value" id="netFlow">₪0</div><div class="stat-label">רווח/הפסד תזרימי</div></div>
        </div>
        <div class="charts-grid">
            <div class="chart-card"><div class="chart-title">התפלגות הוצאות לפי קטגוריה</div><div class="chart-container"><canvas id="categoryChart"></canvas></div></div>
            <div class="chart-card"><div class="chart-title">הכנסות מול הוצאות</div><div class="chart-container"><canvas id="incomeExpenseChart"></canvas></div></div>
        </div>
        <div class="category-section"><div class="category-title">התפלגות הוצאות לפי קטגוריה</div><div id="categoryList"></div></div>
        <div class="table-section">
            <div class="table-header">כל התנועות</div>
            <table>
                <thead><tr><th>תאריך</th><th>סוג</th><th>קטגוריה</th><th>תת-קטגוריה</th><th>ספק</th><th>סכום</th><th>מס' צ'ק</th><th>סטטוס</th><th>הערות</th></tr></thead>
                <tbody id="transactionsBody"><tr><td colspan="9" class="loading">טוען נתונים...</td></tr></tbody>
            </table>
        </div>
    </div>
    <script>
        const SHEET_ID = '1JTTGR7W_VG1q25jbZNXQ3X3DW97rUJJAPduyeuu7DLw';
        let allTransactions = [];
        let charts = {};

        async function loadData() {
            const month = document.getElementById('selectedMonth').value;
            const url = `https://docs.google.com/spreadsheets/d/${SHEET_ID}/gviz/tq?tqx=out:csv&sheet=${encodeURIComponent(month)}`;
            document.getElementById('transactionsBody').innerHTML = '<tr><td colspan="9" class="loading">טוען נתונים...</td></tr>';
            hideStatus();
            try {
                const response = await fetch(url);
                if (!response.ok) throw new Error('Failed to fetch');
                const csvText = await response.text();
                const transactions = parseCSV(csvText);
                if (transactions.length === 0) { showStatus('לא נמצאו נתונים בגיליון ' + month, 'error'); allTransactions = []; updateStats(); updateCharts(); updateCategoryList(); updateTable(); return; }
                allTransactions = transactions;
                updateStats(); updateCharts(); updateCategoryList(); updateTable();
                showStatus('נטענו ' + transactions.length + ' תנועות בהצלחה!', 'success');
            } catch (error) { console.error('Error:', error); showStatus('שגיאה בטעינת הנתונים. וודא שהגיליון משותף לכולם.', 'error'); }
        }

        function showStatus(msg, type) { const el = document.getElementById('statusMsg'); el.textContent = msg; el.className = type === 'error' ? 'error-msg' : 'success-msg'; el.style.display = 'block'; if (type === 'success') setTimeout(() => { el.style.display = 'none'; }, 3000); }
        function hideStatus() { document.getElementById('statusMsg').style.display = 'none'; }

        function parseCSV(csvText) {
            const lines = csvText.split('\n').filter(line => line.trim());
            const transactions = [];
            let headerIndex = -1;
            for (let i = 0; i < Math.min(5, lines.length); i++) { if (lines[i].includes('תאריך') && lines[i].includes('סכום')) { headerIndex = i; break; } }
            if (headerIndex === -1) return [];
            const headers = parseCSVLine(lines[headerIndex]);
            const headerMap = {};
            headers.forEach((h, i) => { headerMap[h.trim().replace(/"/g, '')] = i; });
            for (let i = headerIndex + 1; i < lines.length; i++) {
                const values = parseCSVLine(lines[i]);
                if (values.length < 3) continue;
                const getValue = (key) => { const idx = headerMap[key]; return idx !== undefined ? (values[idx] || '').trim().replace(/"/g, '') : ''; };
                const dateStr = getValue('תאריך');
                if (!dateStr) continue;
                let date = dateStr;
                if (dateStr.includes('/')) { const parts = dateStr.split('/'); if (parts.length === 3) date = `${parts[2]}-${parts[1].padStart(2, '0')}-${parts[0].padStart(2, '0')}`; }
                const typeVal = getValue('סוג');
                const type = typeVal.includes('הכנסה') ? 'income' : 'expense';
                const statusVal = getValue('סטטוס');
                const status = statusVal.includes('בוצע') ? 'completed' : 'pending';
                const amountStr = getValue('סכום').replace(/[₪,\s]/g, '');
                const amount = parseFloat(amountStr) || 0;
                transactions.push({ date, type, category: getValue('קטגוריה') || 'אחר', subcategory: getValue('תת_קטגוריה') || 'אחר', supplier: getValue('ספק') || '', amount, checkNum: getValue('מס_צק') || '', status, notes: getValue('הערות') || '' });
            }
            return transactions;
        }

        function parseCSVLine(line) { const result = []; let current = ''; let inQuotes = false; for (let i = 0; i < line.length; i++) { const char = line[i]; if (char === '"') inQuotes = !inQuotes; else if (char === ',' && !inQuotes) { result.push(current); current = ''; } else current += char; } result.push(current); return result; }

        function updateStats() {
            const openingBalance = parseFloat(document.getElementById('openingBalance').value) || 0;
            const completed = allTransactions.filter(t => t.status === 'completed');
            const totalIncome = completed.filter(t => t.type === 'income').reduce((sum, t) => sum + t.amount, 0);
            const totalExpenses = completed.filter(t => t.type === 'expense').reduce((sum, t) => sum + t.amount, 0);
            const currentBalance = openingBalance + totalIncome - totalExpenses;
            const netFlow = totalIncome - totalExpenses;
            document.getElementById('currentBalance').textContent = formatCurrency(currentBalance);
            document.getElementById('totalIncome').textContent = formatCurrency(totalIncome);
            document.getElementById('totalExpenses').textContent = formatCurrency(totalExpenses);
            document.getElementById('netFlow').textContent = formatCurrency(netFlow);
            document.getElementById('netFlow').style.color = netFlow >= 0 ? 'var(--accent-green)' : 'var(--accent-red)';
        }

        function updateCharts() {
            const expensesByCategory = {};
            allTransactions.filter(t => t.type === 'expense').forEach(t => { expensesByCategory[t.category] = (expensesByCategory[t.category] || 0) + t.amount; });
            const labels = Object.keys(expensesByCategory);
            const data = Object.values(expensesByCategory);
            const colors = ['#ef4444', '#f97316', '#8b5cf6', '#3b82f6', '#ec4899', '#10b981', '#f59e0b'];
            if (charts.category) charts.category.destroy();
            charts.category = new Chart(document.getElementById('categoryChart'), { type: 'doughnut', data: { labels, datasets: [{ data, backgroundColor: colors, borderWidth: 0 }] }, options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { position: 'right', labels: { color: '#94a3b8' } } } } });
            const totalIncome = allTransactions.filter(t => t.type === 'income').reduce((sum, t) => sum + t.amount, 0);
            const totalExpenses = allTransactions.filter(t => t.type === 'expense').reduce((sum, t) => sum + t.amount, 0);
            if (charts.incomeExpense) charts.incomeExpense.destroy();
            charts.incomeExpense = new Chart(document.getElementById('incomeExpenseChart'), { type: 'bar', data: { labels: ['הכנסות', 'הוצאות'], datasets: [{ data: [totalIncome, totalExpenses], backgroundColor: ['rgba(16, 185, 129, 0.8)', 'rgba(239, 68, 68, 0.8)'], borderRadius: 6 }] }, options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } }, scales: { y: { grid: { color: 'rgba(255,255,255,0.05)' }, ticks: { color: '#64748b' } }, x: { grid: { display: false }, ticks: { color: '#64748b' } } } } });
        }

        function updateCategoryList() {
            const expensesByCategory = {};
            allTransactions.filter(t => t.type === 'expense').forEach(t => { expensesByCategory[t.category] = (expensesByCategory[t.category] || 0) + t.amount; });
            const sorted = Object.entries(expensesByCategory).sort((a, b) => b[1] - a[1]);
            document.getElementById('categoryList').innerHTML = sorted.length > 0 ? sorted.map(([cat, amount]) => `<div class="category-item"><span class="category-name">${cat}</span><span class="category-amount" style="color: var(--accent-red)">${formatCurrency(amount)}</span></div>`).join('') : '<div class="loading">אין נתונים</div>';
        }

        function updateTable() {
            const tbody = document.getElementById('transactionsBody');
            if (allTransactions.length === 0) { tbody.innerHTML = '<tr><td colspan="9" class="loading">אין נתונים להצגה</td></tr>'; return; }
            tbody.innerHTML = allTransactions.map(t => `<tr><td>${formatDate(t.date)}</td><td><span class="type-badge ${t.type}">${t.type === 'income' ? '📈 הכנסה' : '📉 הוצאה'}</span></td><td>${t.category}</td><td>${t.subcategory}</td><td>${t.supplier}</td><td class="amount-cell ${t.type}">${formatCurrency(t.amount)}</td><td>${t.checkNum || '-'}</td><td><span class="status-badge ${t.status}">${t.status === 'completed' ? '✅ בוצע' : '⏳ ממתין'}</span></td><td>${t.notes || '-'}</td></tr>`).join('');
        }

        function formatCurrency(amount) { return '₪' + Math.abs(amount).toLocaleString('he-IL'); }
        function formatDate(dateStr) { if (!dateStr) return '-'; const date = new Date(dateStr); return date.toLocaleDateString('he-IL'); }

        loadData();
    </script>
</body>
</html>
