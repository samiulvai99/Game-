<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ad Watch Income</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #4A235A;
            color: white;
        }
        h1 {
            margin-top: 20px;
        }
        .balance-box {
            background: white;
            color: black;
            padding: 10px;
            border-radius: 10px;
            font-size: 18px;
            display: inline-block;
        }
        .watch-ad-btn {
            display: block;
            width: 80%;
            margin: 10px auto;
            padding: 10px;
            font-size: 18px;
            background-color: green;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .watch-ad-btn:disabled {
            background-color: gray;
        }
        .withdraw-btn {
            background-color: blue;
            color: white;
            padding: 10px;
            font-size: 18px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <h1>🎥 Ads দেখে ইনকাম করুন</h1>
    
    <div class="balance-box">💰 ব্যালেন্স: <span id="balance">0</span>৳</div>
    <br><br>
    <button class="withdraw-btn" onclick="withdraw()">Withdraw</button>

    <h2>Watch Ads (10/10)</h2>

    <div id="ads-container">
        <!-- Ads Buttons will be generated dynamically -->
    </div>

    <script>
        let balance = parseInt(localStorage.getItem("balance")) || 0;
        document.getElementById("balance").innerText = balance;

        let adWatched = JSON.parse(localStorage.getItem("adWatched")) || Array(10).fill(false);
        let lastResetDate = localStorage.getItem("lastResetDate") || "";

        function resetAdsIfNeeded() {
            let currentDate = new Date().toLocaleDateString();
            if (currentDate !== lastResetDate) {
                adWatched = Array(10).fill(false);
                localStorage.setItem("adWatched", JSON.stringify(adWatched));
                localStorage.setItem("lastResetDate", currentDate);
                console.log("Ads reset for the new day.");
            }
            generateAdButtons();
        }

        function generateAdButtons() {
            let adContainer = document.getElementById("ads-container");
            adContainer.innerHTML = "";
            let adLinks = [
                "https://heroicfuneral.com/eaymwdnx?key=435b62e2df410d952ccc67722837d832",
                "https://www.effectiveratecpm.com/iwfyj11w3k?key=45632d45fd930f3c5a5b0e1245a6cb8b",
                "https://heroicfuneral.com/juymxf59n1?key=8fab6c9100b0d4b31335f0397c6393b5",
                "https://www.effectiveratecpm.com/sygeei1v6u?key=9da7eaf74b3592de9f5d896fddda81aa",
                "https://heroicfuneral.com/naqbzisa?key=9b146737188b228745bd11d7e322b119",
                "https://www.effectiveratecpm.com/a78sptc3y?key=81e1bb5bacdc98774d9ec6c9c539ae6a",
                "https://heroicfuneral.com/eaymwdnx?key=435b62e2df410d952ccc67722837d832",
                "https://heroicfuneral.com/tv1ppjb73t?key=3c711144117c7cc127ca67a4f8c129da",
                "https://www.effectiveratecpm.com/nkg4b6kk4?key=13bf437f30f91775d13d024303d38df1",
                "https://www.effectiveratecpm.com/h1ibqt6q?key=a5a076e06db18f20d0cdd8e9777dfeca"
            ];
            
            for (let i = 0; i < 10; i++) {
                let btn = document.createElement("button");
                btn.innerText = "Watch Ads " + (i + 1);
                btn.className = "watch-ad-btn";
                btn.disabled = adWatched[i];
                btn.onclick = function() {
                    watchAd(i, adLinks[i]);
                };
                adContainer.appendChild(btn);
            }
        }

        function watchAd(index, url) {
            if (adWatched[index]) return;
window.open(url, "_blank");

            balance += 5;
            localStorage.setItem("balance", balance);
            document.getElementById("balance").innerText = balance;

            adWatched[index] = true;
            localStorage.setItem("adWatched", JSON.stringify(adWatched));

            generateAdButtons();
        }

        function withdraw() {
            if (balance < 500) {
                alert("আপনার ব্যালেন্স 500৳ না হলে উইথড্র করতে পারবেন না!");
                return;
            }
            
            let method = prompt("Bkash/Nagad/Rocket থেকে সিলেক্ট করুন:");
            if (!method || !["Bkash", "Nagad", "Rocket"].includes(method)) {
                alert("ভুল অপশন! দয়া করে Bkash/Nagad/Rocket থেকে সঠিক অপশন সিলেক্ট করুন।");
                return;
            }

            let phone = prompt(method + " নম্বর দিন:");
            if (!phone || phone.length < 11) {
                alert("ভুল নম্বর! দয়া করে সঠিক " + method + " নম্বর দিন।");
                return;
            }

            let accountType = prompt("একাউন্ট টাইপ দিন (Personal/Agent):");
            if (!accountType || !["Personal", "Agent"].includes(accountType)) {
                alert("ভুল টাইপ! দয়া করে Personal/Agent টাইপ দিন।");
                return;
            }

            alert("✅ উইথড্র রিকোয়েস্ট সফল হয়েছে!\n\nমেথড: " + method + "\nনম্বর: " + phone + "\nএকাউন্ট টাইপ: " + accountType + "\nAmount: " + balance + "৳");
            
            balance = 0;
            localStorage.setItem("balance", balance);
            document.getElementById("balance").innerText = balance;
        }

        resetAdsIfNeeded();
    </script>

</body>
</html>
