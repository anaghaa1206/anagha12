---
toc: true
comments: true
layout: post
title: parent page
type: hacks
courses: { compsci: {week: 20} }
---



<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cookie Check and Webpage Loader</title>
    <script>
        function checkCookiesEnabled() {
    
            return navigator.cookieEnabled;
        }

        function loadContent() {
            if (checkCookiesEnabled()) {
                // Cookies are enabled, load the iframe
                document.getElementById("main-content").innerHTML = '<iframe src="https://drishyamody.github.io/Frontend/weather" width="100%" height="600px" style="border:none;"></iframe>';
            } else {
                // Cookies are not enabled, display error message
                document.getElementById("main-content").textContent = "403 Forbidden: Cookies are not enabled in your browser.";
            }
        }
    </script>
</head>
<body onload="loadContent()">
    <div id="main-content">
        <!-- Content will be loaded here based on cookie check -->
    </div>
</body>
</html>