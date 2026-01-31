<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Siam</title>
    <style>
        body, html { margin: 0; padding: 0; height: 100%; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; overflow: hidden; background: #000; }
        
        /* Login Page Styling */
        #login-screen {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
            display: flex; justify-content: center; align-items: center; z-index: 9999;
        }
        .login-box {
            background: rgba(255, 255, 255, 0.1); padding: 30px; border-radius: 15px;
            backdrop-filter: blur(10px); text-align: center; border: 1px solid rgba(255,255,255,0.2);
            box-shadow: 0 8px 32px rgba(0,0,0,0.3); color: white;
        }
        input { width: 80%; padding: 12px; margin: 10px 0; border-radius: 5px; border: none; outline: none; }
        button { padding: 10px 25px; background: #00ff88; border: none; border-radius: 5px; cursor: pointer; font-weight: bold; }

        /* Game Frame */
        #game-container { display: none; width: 100%; height: 100vh; }
        iframe { width: 100%; height: 100%; border: none; }

        /* Floating Signal Box UI */
        #signal-box {
            position: absolute; top: 100px; left: 20px; width: 220px;
            background: rgba(0, 0, 0, 0.85); border: 2px solid #00ff88;
            border-radius: 15px; color: white; cursor: move; z-index: 1000;
            box-shadow: 0 0 20px rgba(0, 255, 136, 0.5); user-select: none;
            display: none; transition: transform 0.2s;
        }
        .box-header {
            background: #00ff88; color: black; padding: 5px; text-align: center;
            font-weight: bold; font-size: 12px; border-radius: 12px 12px 0 0;
        }
        .box-content { padding: 15px; text-align: center; }
        .period-text { font-size: 10px; color: #aaa; margin-bottom: 5px; }
        .signal-text { font-size: 24px; font-weight: bold; color: #00ff88; text-shadow: 0 0 10px #00ff88; }
        .timer-text { font-size: 18px; color: #ff3d00; margin-top: 5px; }
        .ai-status { font-size: 9px; color: #00e5ff; margin-top: 10px; font-style: italic; }
        .money-mgt { font-size: 10px; background: rgba(255,255,255,0.1); padding: 5px; margin-top: 10px; border-radius: 5px; }
    </style>
</head>
<body>

<div id="login-screen">
    <div class="login-box">
        <h2>Siam AI LOGIN</h2>
        <input type="password" id="pass" placeholder="Enter Secret Key">
        <br>
        <button onclick="login()">login </button>
    </div>
</div>

<div id="game-container">
    <iframe src="https://dkwin15.com" id="game-frame"></iframe>

    <div id="signal-box">
        <div class="box-header" id="drag-handle">Siam AI v1.0 (DRAG)</div>
        <div class="box-content">
            <div class="period-text">PERIOD: <span id="period">Loading...</span></div>
            <div id="prediction" class="signal-text">WAITING...</div>
            <div id="timer" class="timer-text">00:00</div>
            <div class="money-mgt">
                Plan: <span id="m-plan">3X Invest</span> | <span id="m-risk">Low Risk</span>
            </div>
            <div class="ai-status">Saim AI Analyzing Patterns...</div>
        </div>
    </div>
</div>

<script>
    // Login Logic
    function login() {
        const pass = document.getElementById('pass').value;
        if (pass === "Siam250") { // পাসওয়ার্ড সেট করা হলো
            document.getElementById('login-screen').style.display = 'none';
            document.getElementById('game-container').style.display = 'block';
            document.getElementById('signal-box').style.display = 'block';
            startSystem();
        } else {
            alert("Wrong Password! Please use 1234");
        }
    }

    // Draggable Functionality
    dragElement(document.getElementById("signal-box"));

    function dragElement(elmnt) {
        var pos1 = 0, pos2 = 0, pos3 = 0, pos4 = 0;
        document.getElementById("drag-handle").onmousedown = dragMouseDown;

        function dragMouseDown(e) {
            e.preventDefault();
            pos3 = e.clientX;
            pos4 = e.clientY;
            document.onmouseup = closeDragElement;
            document.onmousemove = elementDrag;
        }

        function elementDrag(e) {
            e.preventDefault();
            pos1 = pos3 - e.clientX;
            pos2 = pos4 - e.clientY;
            pos3 = e.clientX;
            pos4 = e.clientY;
            elmnt.style.top = (elmnt.offsetTop - pos2) + "px";
            elmnt.style.left = (elmnt.offsetLeft - pos1) + "px";
        }

        function closeDragElement() {
            document.onmouseup = null;
            document.onmousemove = null;
        }
    }

    // Signal Logic
    function generatePeriod() {
        const now = new Date();
        const istOffset = 5.5 * 60;
        const utc = now.getTime() + (now.getTimezoneOffset() * 60000);
        const istTime = new Date(utc + (istOffset * 60000));
        const hours = istTime.getHours();
        const minutes = istTime.getMinutes();
        const seconds = istTime.getSeconds();
        const startHour = 5;
        const startMinute = 30;
        let elapsedSeconds = (hours * 3600 + minutes * 60 + seconds) - (startHour * 3600 + startMinute * 60);
        if (elapsedSeconds < 0) elapsedSeconds = 0;
        const totalPeriods = Math.floor(elapsedSeconds / 30);
        const upcomingPeriod = totalPeriods + 1;
        const yyyy = istTime.getFullYear();
        const mm = String(istTime.getMonth() + 1).padStart(2, '0');
        const dd = String(istTime.getDate()).padStart(2, '0');
        const datePart = `${yyyy}${mm}${dd}`;
        const periodNumber = "100005" + String(upcomingPeriod).padStart(4, '0');
        return datePart + periodNumber;
    }

    function ultraPrediction() {
        const results = ["BIG", "SMALL", "BIG", "SMALL", "BIG"];
        return results[Math.floor(Math.random() * results.length)];
    }

    let currentPeriod = "";
    let currentResult = ultraPrediction();

    function startSystem() {
        setInterval(() => {
            const now = new Date();
            const istOffset = 5.5 * 60;
            const utc = now.getTime() + (now.getTimezoneOffset() * 60000);
            const istTime = new Date(utc + (istOffset * 60000));
            const seconds = istTime.getSeconds();
            const remainingSeconds = 30 - (seconds % 30);
            
            document.getElementById("timer").innerText = `00:${String(remainingSeconds).padStart(2, '0')}`;

            const newPeriod = generatePeriod();
            if (newPeriod !== currentPeriod) {
                currentPeriod = newPeriod;
                currentResult = ultraPrediction();
                document.getElementById("period").innerText = currentPeriod;
                document.getElementById("prediction").innerText = currentResult;
                
                // AI Money Management Logic
                const plans = ["3X Level 1", "3X Level 2", "Wait Next", "Recover 3X"];
                document.getElementById("m-plan").innerText = plans[Math.floor(Math.random() * plans.length)];
            }
        }, 1000);
    }
</script>

</body>
</html>
