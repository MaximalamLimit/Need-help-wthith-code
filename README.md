# Need-help-wthith-code
The part with fortune upgrades isn't working, I need help
(function() {
    // Initialize variables for the intervals
    var newsTickerInterval;
    var goldenCookiesInterval;
    var cookieClickerInterval;

    // Function to start the automated process
    function startAutomation() {
        newsTickerInterval = setInterval(checkNewsTicker, 1000); // every 1 second
        goldenCookiesInterval = setInterval(clickGoldenCookies, 500); // every 500 milliseconds
        cookieClickerInterval = setInterval(clickRandomPositionOnCookie, 100); // every 100 milliseconds
        console.log("Automated process started");
    }

    // Function to stop the automated process
    function stopAutomation() {
        clearInterval(newsTickerInterval);
        clearInterval(goldenCookiesInterval);
        clearInterval(cookieClickerInterval);
        console.log("Automated process stopped");
    }

    // Function that checks the News Ticker and clicks on Fortune upgrades
    function checkNewsTicker() {
        var ticker = document.getElementById('commentsText');
        
        if (ticker && ticker.childNodes.length > 0) {
            var newsContent = ticker.childNodes[0].textContent;
            
            // Check if a Fortune upgrade is mentioned in the News Ticker
            if (newsContent.includes('Fortune!')) {
                // Click on the Fortune upgrade
                ticker.childNodes[0].click();
                console.log("Fortune upgrade clicked: " + newsContent);
            }
        }
    }

    // Function that clicks on golden cookies
    function clickGoldenCookies() {
        var goldenCookies = Game.shimmers;
        for (var i in goldenCookies) {
            if (goldenCookies[i].type == 'golden') {
                goldenCookies[i].pop();
                console.log("Golden cookie clicked");
            }
        }
    }

    // Function that clicks the big cookie at a random position
    function clickRandomPositionOnCookie() {
        var bigCookie = document.getElementById('bigCookie');
        if (!bigCookie) return;

        var cookieRect = bigCookie.getBoundingClientRect();
        var cookieCenterX = cookieRect.left + cookieRect.width / 2;
        var cookieCenterY = cookieRect.top + cookieRect.height / 2;
        var cookieRadius = cookieRect.width / 2; // Assuming cookie is round and width = height

        if (!Game.OnAscend) {
            // Generate random angle and radius for the click position
            var angle = Math.random() * Math.PI * 2;
            var radius = Math.random() * cookieRadius;

            // Calculate and set the random click position
            Game.mouseX = cookieCenterX + radius * Math.cos(angle) - document.documentElement.scrollLeft;
            Game.mouseY = cookieCenterY + radius * Math.sin(angle) - document.documentElement.scrollTop;

            // Click the cookie
            Game.ClickCookie();
        }
        else {
            clearInterval(cookieClickerInterval);
        }
    }

    // Global functions to start and stop the automated process
    window.startAutomation = startAutomation;
    window.stopAutomation = stopAutomation;

    // Start the automated process when the script is loaded
    startAutomation();
})();
