# badminton-invite-page
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>邀请你打羽毛球</title>

    <script>
        function init_viewport(){
            if(navigator.userAgent.indexOf('Android') != -1){
                var width = window.outerWidth == 0 ? window.screen.width : window.outerWidth;
                var phoneScale = parseInt(width)/500;
                document.write('<meta name="viewport" content="width=500, minimum-scale='+ phoneScale +', maximum-scale='+ phoneScale +'">');
            } else if(navigator.userAgent.indexOf('iPhone') != -1){
                var phoneScale = parseInt(window.screen.width)/500;
                document.write('<meta name="viewport" content="width=500, initial-scale=' + phoneScale +', maximum-scale='+phoneScale+'">');
            } else {
                document.write('<meta name="viewport" content="width=500, height=750, initial-scale=0.64">');
            }
        }
        init_viewport();
    </script>

    <style>
        * {
            padding: 0;
            margin: 0;
            box-sizing: border-box;
        }

        body {
            background-color: #f9f9f9;
            font-family: "Microsoft YaHei", sans-serif;
        }

        #div_container {
            width: 500px;
            margin: 0 auto;
            position: relative;
            text-align: center;
            padding-top: 30px;
        }

        h1 {
            color: #2ECC71;
            font-size: 2em;
            margin-bottom: 15px;
        }

        input[type="text"] {
            padding: 10px;
            font-size: 1em;
            width: 80%;
            max-width: 300px;
            border-radius: 5px;
            border: 1px solid #ccc;
            margin-top: 15px;
        }

        input[type="button"] {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 1em;
            background-color: #2ECC71;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        #invitation_result {
            display: none;
            margin-top: 30px;
            font-size: 1.1em;
        }

        /* 羽毛球图形 */
        .badminton-ball {
            width: 60px;
            height: 60px;
            background: radial-gradient(circle at 40% 40%, #fff, #ddd);
            border-radius: 50%;
            box-shadow: inset 0 0 10px rgba(0,0,0,0.2);
            margin: 40px auto 0;
            animation: bounce 2s infinite ease-in-out;
            position: relative;
        }

        .badminton-ball::before {
            content: '';
            position: absolute;
            top: 25px;
            left: 0;
            width: 60px;
            height: 8px;
            background: black;
        }

        /* 球拍图形 */
        .badminton-racket {
            width: 80px;
            height: 180px;
            border: 3px solid #3498db;
            border-radius: 50% 50% 0 0 / 70% 70% 0 0;
            position: relative;
            margin: 20px auto;
            animation: swing 3s infinite alternate;
        }

        .badminton-racket::after {
            content: '';
            position: absolute;
            bottom: -20px;
            left: 30px;
            width: 20px;
            height: 40px;
            background: #3498db;
            border-radius: 5px;
        }

        /* 动画效果 */
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }

        @keyframes swing {
            from { transform: rotate(-10deg); }
            to { transform: rotate(10deg); }
        }

        /* 隐藏音频控件 */
        audio {
            display: none;
        }
    </style>
</head>

<body>
    <div id="div_container">
        <div id="invitation_header">
            <h1>周末一起打羽毛球吗？</h1>
            <p style="font-size:1.1em;">欢迎加入我们的羽毛球小队，请输入你的名字：</p>
            <input type="text" id="input_name" placeholder="你的名字" maxlength="10" oninput="toggleButton()">
            <br>
            <input type="button" id="btn_send" value="点这里确认参加" onclick="showInvitation()" style="display:none;">
        </div>

        <!-- 羽毛球与球拍 -->
        <div class="badminton-racket"></div>
        <div class="badminton-ball"></div>

        <!-- 邀请信息展示区域 -->
        <div id="invitation_result">
            <p><strong id="name_placeholder"></strong>，周六下午三点我们在体育馆等你来打球！</p>
            <p>记得带上水杯和球拍哦~</p>
        </div>
    </div>

    <!-- 背景音乐 -->
    <audio id="bg-music" autoplay loop>
        <source src="https://www.bensound.com/bensound-music/bensound-happyrock.mp3" type="audio/mp3">
        您的浏览器不支持音频播放。
    </audio>

    <script>
        function toggleButton() {
            const btn = document.getElementById("btn_send");
            const input = document.getElementById("input_name").value.trim();
            btn.style.display = input.length > 0 ? 'inline-block' : 'none';
        }

        function showInvitation() {
            const name = document.getElementById("input_name").value.trim();
            const resultDiv = document.getElementById("invitation_result");
            const namePlaceholder = document.getElementById("name_placeholder");

            if (name === '') return;

            namePlaceholder.textContent = name;
            resultDiv.style.display = 'block';

            // 隐藏输入框
            document.getElementById("invitation_header").style.display = 'none';

            // 尝试播放音乐（移动端需用户操作后才能播放）
            const music = document.getElementById("bg-music");
            if (music.paused) {
                music.play().catch(() => {
                    alert("由于浏览器限制，请先点击页面任意位置以播放音乐");
                });
            }
        }

        // 移动端点击任意地方允许播放音乐
        document.addEventListener("click", () => {
            const music = document.getElementById("bg-music");
            if (music.paused) {
                music.play().catch(() => {});
            }
        }, { once: true });
    </script>
</body>
</html>
