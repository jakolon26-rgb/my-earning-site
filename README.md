<!-- ======= CSS ======= -->
<style>
body {
    font-family: Arial, sans-serif;
    background: #f5f7fa;
    color: #333;
    margin: 0;
    padding: 0;
}

.hero {
    padding: 60px 20px;
    text-align: center;
    background: linear-gradient(to right, #0084ff, #00c6ff);
    color: white;
}

.hero h1 {
    font-size: 36px;
    margin-bottom: 10px;
}

.hero p {
    font-size: 16px;
    opacity: 0.9;
}

.dashboard {
    padding: 40px 20px;
    max-width: 900px;
    margin: auto;
}

.card {
    background: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0 3px 10px rgba(0,0,0,0.1);
    margin-bottom: 20px;
}

.card button {
    padding: 10px 20px;
    background: #00a2ff;
    color: white;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    margin-top: 10px;
    font-size: 15px;
}

.ref-box {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #eef6ff;
    padding: 15px;
    border-radius: 8px;
}

.ref-box input {
    width: 80%;
    border: none;
    background: transparent;
    font-size: 16px;
}

.ref-box button {
    padding: 10px 15px;
    border: none;
    background: #0084ff;
    color: white;
    border-radius: 5px;
    cursor: pointer;
}
</style>

<!-- ======= HTML ======= -->
<div class="hero">
    <h1>Earn Money by Referring Friends</h1>
    <p>Complete tasks, watch ads, invite friends, and earn rewards!</p>
</div>

<div class="dashboard">
    <div class="card">
        <h3>Your Earnings: $<span id="earnings">0</span></h3>
    </div>

    <div class="card">
        <h3>Your Referral Link</h3>
        <div class="ref-box">
            <input id="refLink" value="https://yourdomain.com/">
            <button onclick="copyLink()">Copy</button>
        </div>
    </div>

    <h2>Daily Tasks</h2>

    <div class="card">
        <h3>Watch a video</h3>
        <p>Earn $0.20 for completing this task.</p>
        <button onclick="completeTask(0.20)">Complete Task</button>
    </div>

    <div class="card">
        <h3>Click an ad</h3>
        <p>Earn $0.10 for clicking.</p>
        <button onclick="completeTask(0.10)">Complete Task</button>
    </div>

    <div class="card">
        <h3>Invite a friend</h3>
        <p>Earn $1.00 when the friend joins (simulated).</p>
        <button onclick="completeTask(1.00)">Complete Task</button>
    </div>

    <h2>Video Ad Tasks</h2>

    <div class="card">
        <h3>Watch Video Ad #1</h3>
        <p>Earn $0.30 for watching this ad.</p>
        <button onclick="startVideoAd(1, 0.30)">Watch Ad</button>
        <p id="adTimer1" style="color:#0084ff; font-weight:bold;"></p>
    </div>

    <div class="card">
        <h3>Watch Video Ad #2</h3>
        <p>Earn $0.50 for watching this ad.</p>
        <button onclick="startVideoAd(2, 0.50)">Watch Ad</button>
        <p id="adTimer2" style="color:#0084ff; font-weight:bold;"></p>
    </div>

    <div class="card">
        <h3>Watch Video Ad #3</h3>
        <p>Earn $1.00 for watching this ad.</p>
        <button onclick="startVideoAd(3, 1.00)">Watch Ad</button>
        <p id="adTimer3" style="color:#0084ff; font-weight:bold;"></p>
    </div>
</div>

<!-- ======= JavaScript ======= -->
<script>
function copyLink() {
    let copyText = document.getElementById("refLink");
    copyText.select();
    navigator.clipboard.writeText(copyText.value);
    alert("Referral link copied!");
}

function completeTask(amount) {
    let earn = document.getElementById("earnings");
    earn.innerText = (parseFloat(earn.innerText) + amount).toFixed(2);
    alert("Task completed! You earned $" + amount.toFixed(2));
}

function startVideoAd(adNumber, reward) {
    let timerId = "adTimer" + adNumber;
    let label = document.getElementById(timerId);

    let timeLeft = 10; // 10 seconds fake ad

    label.innerText = "Ad Playing... " + timeLeft + "s";

    let countdown = setInterval(() => {
        timeLeft--;
        label.innerText = "Ad Playing... " + timeLeft + "s";

        if (timeLeft <= 0) {
            clearInterval(countdown);
            label.innerText = "Ad Completed! You earned $" + reward.toFixed(2);

            let earn = document.getElementById("earnings");
            earn.innerText = (parseFloat(earn.innerText) + reward).toFixed(2);

            alert("You earned $" + reward.toFixed(2) + " from the video ad!");
        }
    }, 1000);
}
</script>
