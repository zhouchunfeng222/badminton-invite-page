# Time to play badminton!
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>打羽毛球啦</title>

    <!-- 前面的部分保持不变 -->

    <style>
        /* 前面的样式保持不变 */

        #map {
            width: 100%;
            height: 300px;
            margin-top: 20px;
        }

        #countdown {
            font-size: 1.5em;
            color: red;
            margin-top: 20px;
        }
    </style>
</head>

<body>
    <div id="div_container">
        <!-- 前面的内容保持不变 -->

        <!-- 邀请信息展示区域 -->
        <div id="invitation_result">
            <p><strong id="name_placeholder"></strong>，19：00-21:00我们在超越体育馆等你来打球！</p>
            <p>记得带上水杯和球拍哦~</p>
            
            <!-- 地图位置 -->
            <div id="map">
                <iframe src="YOUR_GOOGLE_MAPS_EMBED_URL" width="100%" height="100%" style="border:0;" allowfullscreen="" loading="lazy"></iframe>
            </div>

            <!-- 倒计时 -->
            <div id="countdown">活动倒计时：Loading...</div>
        </div>
    </div>

    <!-- 背景音乐部分保持不变 -->

    <script>
        // 前面的脚本保持不变

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

            // 设置倒计时
            setCountdown();
        }

        function setCountdown() {
            const countdownElement = document.getElementById('countdown');
            const eventDate = new Date("May 11, 2025 15:00:00").getTime(); // 修改为你想要的日期和时间

            const timer = setInterval(function() {
                const now = new Date().getTime();
                const distance = eventDate - now;

                const days = Math.floor(distance / (1000 * 60 * 60 * 24));
                const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
                const seconds = Math.floor((distance % (1000 * 60)) / 1000);

                countdownElement.innerHTML = "活动倒计时：" + days + "天 " + hours + "小时 "
                    + minutes + "分钟 " + seconds + "秒";

                if (distance < 0) {
                    clearInterval(timer);
                    countdownElement.innerHTML = "活动已经开始！";
                }
            }, 1000);
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
