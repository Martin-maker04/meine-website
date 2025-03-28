<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BEESCHRAM – Imkerverwaltung</title>
    <style>
        /* Allgemeine Stile */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #faf0e6; /* Warmer Beige-Ton */
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }
        header {
            background-color: #2c3e50;
            color: white;
            padding: 15px;
            text-align: center;
        }
        nav {
            background: #34495e;
            padding: 10px;
            text-align: center;
        }
        nav a {
            color: white;
            text-decoration: none;
            margin: 0 15px;
            font-size: 18px;
        }
        nav a:hover {
            text-decoration: underline;
        }

        /* Hauptcontainer */
        .container {
            width: 80%;
            margin: 20px auto;
            flex: 1;
        }

        /* Layout für die Kästchen */
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin-top: 30px;
        }

        /* Kästchen-Stil */
        .box {
            background: white;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            position: relative;
        }
        .box h3 {
            margin-top: 0;
            text-align: center;
            color: #2c3e50;
        }

        /* Stil für das Pluszeichen */
        .plus {
            position: absolute;
            top: 10px;
            right: 10px;
            font-size: 24px;
            cursor: pointer;
            color: #2c3e50;
            transition: transform 0.3s, color 0.3s;
        }

        .plus:hover {
            transform: scale(1.2);
            color: #e67e22;
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 15px;
            background: #2c3e50;
            color: white;
            margin-top: auto;
            position: fixed;
            width: 100%;
            bottom: 0;
        }
    </style>
</head>
<body>

    <!-- Header -->
    <header>
        <h1>BEESCHRAM – Imkerverwaltung</h1>
    </header>

    <!-- Navigation -->
    <nav>
        <a href="#">Home</a>
        <a href="staende.html">Stände</a>
        <a href="todo.html">To-Do</a>
        <a href="termine.html">Termine</a>
    </nav>

    <!-- Hauptinhalt -->
    <div class="container">
        <h2>Willkommen zur digitalen Imkerverwaltung</h2>
        <p>Hier kannst du deine Bienenstände, Völker und Aufgaben verwalten.</p>

        <!-- Info-Box -->
        <div class="box">
            <h3>Info</h3>
            <p>Aktuelle Erweiterung: <strong>Hobby</strong></p>
            <p>Punkte aus Empfehlung: <strong>0 Punkte</strong></p>
        </div>

        <!-- Grid für die Hauptbereiche -->
        <div class="grid">
            <!-- Stände -->
            <div class="box">
                <h3>Stände</h3>
                <div id="standorteListe"></div>
                <span class="plus" onclick="window.location.href='staende.html'">+</span>
            </div>

            <!-- TODO -->
            <div class="box">
                <h3>To-Do</h3>
                <p>✅ 01.04.2025 - Varroa behandeln.</p>
                <a href="todo.html"><span class="plus">+</span></a>
            </div>

            <!-- Termine -->
            <div class="box">
                <h3>Termine</h3>
                <p>📅 Trage hier deinen ersten Termin ein.</p>
                <a href="termine.html"><span class="plus">+</span></a>
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer>
        Impressum Martin Platter 26.03.2025
    </footer>

    <script>
        // Lade Standorte aus LocalStorage und zeige sie auf der Startseite an
        var standorte = JSON.parse(localStorage.getItem('standorte')) || [];
        var standorteListe = document.getElementById('standorteListe');

        if (standorte.length > 0) {
            standorte.forEach(function(standort, index) {
                var standortText = document.createElement('p');
                standortText.innerHTML = `📍 ${standort.name}: ${standort.lat.toFixed(4)}, ${standort.lng.toFixed(4)}`;
                standorteListe.appendChild(standortText);
            });
        } else {
            standorteListe.innerHTML = 'Es wurden noch keine Standorte hinzugefügt.';
        }
    </script>

</body>
</html>
