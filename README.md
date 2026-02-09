<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>THE AI HUB - Digital Khata</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        :root { --primary: #2563eb; --success: #16a34a; --danger: #dc2626; --dark: #1e293b; }
        body { font-family: 'Poppins', sans-serif; margin: 0; background-color: #f1f5f9; color: var(--dark); }
        
        header { 
            background: var(--primary); color: white; padding: 25px 15px; 
            text-align: center; border-bottom-left-radius: 25px; border-bottom-right-radius: 25px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        .container { padding: 15px; max-width: 500px; margin: auto; }
        
        .card { 
            background: white; padding: 20px; border-radius: 15px; 
            box-shadow: 0 4px 6px rgba(0,0,0,0.05); margin-bottom: 20px; 
        }

        h3 { margin-top: 0; color: var(--primary); font-size: 18px; }
        
        input { 
            width: 100%; padding: 12px; margin: 8px 0; border: 1px solid #cbd5e1; 
            border-radius: 10px; box-sizing: border-box; font-size: 16px;
        }

        button { 
            width: 100%; padding: 14px; border: none; border-radius: 10px; 
            font-size: 16px; font-weight: 600; cursor: pointer; transition: 0.2s;
        }

        .btn-add { background: var(--success); color: white; margin-top: 10px; }
        .btn-add:active { transform: scale(0.96); }

        .khata-item { 
            background: white; padding: 15px; border-radius: 12px; 
            margin-bottom: 12px; display: flex; justify-content: space-between; 
            align-items: center; border-left: 6px solid var(--danger);
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }

        .khata-info h4 { margin: 0; font-size: 17px; text-transform: capitalize; }
        .khata-info p { margin: 0; color: #64748b; font-size: 12px; }
        .amount { color: var(--danger); font-weight: bold; font-size: 18px; }

        .btn-clear { 
            background: #fee2e2; color: var(--danger); padding: 6px 12px; 
            font-size: 12px; width: auto; margin-left: 10px;
        }

        footer { text-align: center; padding: 30px 15px; color: #94a3b8; font-size: 13px; }
        .badge { background: #dbeafe; color: #1e40af; padding: 4px 10px; border-radius: 20px; font-size: 11px; font-weight: 600; }
    </style>
</head>
<body>

<header>
    <h1 style="margin:0; letter-spacing: 1px;">THE AI HUB</h1>
    <span class="badge">IIT Patna Student Startup</span>
</header>

<div class="container">
    <div class="card">
        <h3>Naya Udhari Entry 📝</h3>
        <input type="text" id="custName" placeholder="Customer ka Naam">
        <input type="number" id="custAmount" placeholder="Amount (₹) kitna baaki hai?">
        <button class="btn-add" onclick="saveData()">Khata mein Jodein</button>
    </div>

    <h3 style="color: #64748b; font-size: 16px; padding-left: 5px;">Active Udhari Register</h3>
    <div id="khataList">
        </div>
</div>

<footer>
    <p>Developed with ❤️ by <b>Harshwardhan Singh Lodhi</b></p>
    <p>Founder @ THE AI HUB | Bhilai, CG</p>
</footer>

<script>
    function loadData() {
        const list = document.getElementById('khataList');
        const data = JSON.parse(localStorage.getItem('aiHubKhata')) || [];
        list.innerHTML = '';

        if(data.length === 0) {
            list.innerHTML = '<div style="text-align:center; padding:40px; color:#94a3b8;">Koi pending udhari nahi hai. Chill maaro! 😎</div>';
            return;
        }

        data.forEach((item, index) => {
            list.innerHTML += `
                <div class="khata-item">
                    <div class="khata-info">
                        <h4>${item.name}</h4>
                        <p>📅 ${item.date}</p>
                    </div>
                    <div style="display:flex; align-items:center;">
                        <div class="amount">₹${item.amount}</div>
                        <button class="btn-clear" onclick="deleteEntry(${index})">Hatao</button>
                    </div>
                </div>
            `;
        });
    }

    function saveData() {
        const name = document.getElementById('custName').value;
        const amount = document.getElementById('custAmount').value;
        const date = new Date().toLocaleDateString('en-IN', { day:'numeric', month:'short', year:'numeric' });

        if(!name || !amount) {
            alert('Bhai, naam aur amount dono likho!');
            return;
        }

        const data = JSON.parse(localStorage.getItem('aiHubKhata')) || [];
        data.push({ name, amount, date });
        localStorage.setItem('aiHubKhata', JSON.stringify(data));

        document.getElementById('custName').value = '';
        document.getElementById('custAmount').value = '';
        loadData();
    }

    function deleteEntry(index) {
        if(confirm('Kya ye udhari chukta ho gayi?')) {
            let data = JSON.parse(localStorage.getItem('aiHubKhata'));
            data.splice(index, 1);
            localStorage.setItem('aiHubKhata', JSON.stringify(data));
            loadData();
        }
    }

    loadData();
</script>

</body>
</html>
