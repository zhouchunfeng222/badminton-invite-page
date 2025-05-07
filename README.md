<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>邀请你打羽毛球</title>
    <style>
        body {
            background: url('https://broadscope-dialogue-new.oss-cn-beijing.aliyuncs.com/output/20250507/d00fa899079ecf9f563443f1ed2ac1f1.webp?Expires=1778116779&OSSAccessKeyId=LTAI5tL97mBYzVcjkG1cUyin&Signature=wlNWetPc%2BRpOLk9gfr%2FPGGWd8cA%3D') no-repeat center center fixed;
            -webkit-background-size: cover;
            -moz-background-size: cover;
            -o-background-size: cover;
            background-size: cover;
            animation: fadeInOut 30s infinite;
        }

        @keyframes fadeInOut {
            0% { opacity: 1; }
            50% { opacity: 0.7; }
            100% { opacity: 1; }
        }

        #div_container {
            width: 500px;
            margin: 0 auto;
            position: relative;
            text-align: center;
            padding-top: 30px;
            background-color: rgba(255,255,255,0.8);
        }

        /* 羽毛球动画示例 */
        .shuttlecock {
            width: 50px;
            height: 50px;
            background: url('URL_TO_SHUTTLECOCK_IMAGE') no-repeat;
            background-size: contain;
            animation: flyUp 3s ease-in-out infinite;
        }

        @keyframes flyUp {
            0% { transform: translateY(0); }
            100% { transform: translateY(-300px); }
        }
    </style>
</head>
<body>
    <div id="div_container">
        <h1>让我们一起打羽毛球吧！</h1>
        <p>期待在球场上见到你！</p>
        <!-- 添加羽毛球动画 -->
        <div class="shuttlecock"></div>
    </div>
</body>
</html>
