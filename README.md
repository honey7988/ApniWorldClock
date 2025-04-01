<!doctype html>
<html lang="en">

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>World Clock</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    <style>
        .bg-image {
            background-image: url('https://example.com/your-background.jpg');
            background-size: cover;
            background-position: center;
            height: 100vh;
            color: white;
            text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.7);
        }

        .jumbotron.my-4 {
            background-color: rgba(0, 0, 0, 0.5);
            padding: 2rem;
            border-radius: 10px;
        }
    </style>
</head>

<body class="bg-image">
    <script>
        let selectedTimeZone = "UTC"; // Default timezone

        const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };

        function updateTime() {
            let now = new Date();
            let date = now.toLocaleDateString(undefined, { ...options, timeZone: selectedTimeZone });
            let time = now.toLocaleTimeString(undefined, { timeZone: selectedTimeZone });

            // Extract hour from selected timezone for greeting
            let formatter = new Intl.DateTimeFormat('en-US', { hour: 'numeric', hour12: false, timeZone: selectedTimeZone });
            let hour = parseInt(formatter.format(now));

            let greeting = getGreeting(hour);

            document.getElementById('time').innerHTML = time + "<br>on " + date;
            document.getElementById('greeting').innerHTML = greeting;
        }

        function getGreeting(hour) {
            if (hour < 12) {
                return "Good Morning!";
            } else if (hour < 18) {
                return "Good Afternoon!";
            } else {
                return "Good Evening!";
            }
        }

        function updateTimeZone() {
            selectedTimeZone = document.getElementById('timezoneSelector').value;
            updateTime();
        }

        // Ensure script runs after the page loads
        window.onload = function() {
            updateTime();
            setInterval(updateTime, 1000);
        };
    </script>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz"
        crossorigin="anonymous"></script>

    <nav class="navbar navbar-expand-lg bg-body-tertiary">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">World Clock</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
                aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav">
                    <li class="nav-item">
                        <a class="nav-link active" aria-current="page" href="#">Home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#">Features</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#">Pricing</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link disabled" aria-disabled="true">Disabled</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <center>
        <div class="jumbotron my-4">
            <h1 class="display-4" id="greeting"></h1>
            <h2 class="display-5">Current time is: <span id="time"></span></h2>
            <p class="lead">Check the time across different locations!</p>
            <hr class="my-4">
            <p>Select a time zone to see the current time:</p>
            <select class="form-select" id="timezoneSelector" onchange="updateTimeZone()">
                <option value="UTC" selected>UTC</option>
                <option value="America/New_York">New York</option>
                <option value="Europe/London">London</option>
                <option value="Asia/Tokyo">Tokyo</option>
                <option value="Asia/Kolkata">India</option>
                <option value="Australia/Sydney">Sydney</option>
            </select>
            <p class="lead">
                <a class="btn btn-primary btn-lg" href="#" role="button">Browse Times</a>
            </p>
        </div>
    </center>
</body>

</html>
