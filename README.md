<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BEEINTOUCH Klon</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #e0dac4;
        }
        header {
            background-color: #2c3e50;
            color: white;
            padding: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .logo {
            font-size: 20px;
            font-weight: bold;
        }
        nav ul {
            list-style: none;
            padding: 0;
            margin: 0;
            display: flex;
        }
        nav ul li {
            margin-left: 20px;
        }
        nav ul li a {
            color: white;
            text-decoration: none;
        }
        .info {
            display: flex;
            justify-content: space-between;
            padding: 20px;
            background: white;
            margin: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .expandable {
            padding: 20px;
        }
        .section {
            background: white;
            padding: 10px;
            margin: 10px 0;
            border-radius: 8px;
            box-shadow: 0 0 5px rgba(0,0,0,0.1);
            cursor: pointer;
        }
        .content {
            display: none;
            padding: 10px;
            background: #f9f9f9;
            border-radius: 5px;
            margin-top: 5px;
        }
    </style>
    <script>
        function toggleSection(id) {
            var section = document.getElementById(id);
            if (section.style.display === "block") {
                section.style.display = "none";
            } else {
                section.style.display = "block";
            }
        }
    </script>
</head>
<body>
    <header>
        <div class="logo">BEEINTOUCH</div>
        <nav>
            <ul>
                <li><a href="#">STÄNDE</a></li>
                <li><a href="#">LAGER</a></li>
                <li><a href="#">ZUCHT</a></li>
                <li><a href="#">BÜRO</a></li>
            </ul>
        </nav>
    </header>
    
    <main>
        <section class="info">
            <div class="logo-box">Hier das Logo Ihrer Imkerei</div>
            <div class="details">
                <p>Guten Tag</p>
                <p>Aktuelle Erweiterung: Hobby (kostenlos)</p>
                <p>Punkte aus Empfehlung: <span id="punkte">0</span></p>
            </div>
        </section>
        
        <section class="expandable">
            <div class="section" onclick="toggleSection('staende')">
                <h3>STÄNDE</h3>
                <div id="staende" class="content">
                    <p>Vinschgau - (0 Völker)</p>
                    <p>Zuhause - (5 Völker)</p>
                </div>
            </div>
            <div class="section" onclick="toggleSection('todo')">
                <h3>TODO</h3>
                <div id="todo" class="content">
                    <p>01.04.2025 - Varia behandeln.</p>
                </div>
            </div>
            <div class="section" onclick="toggleSection('termine')">
                <h3>TERMINE</h3>
                <div id="termine" class="content">
                    <p>Tragen Sie hier den ersten Termin ein.</p>
                </div>
            </div>
        </section>
    </main>
</body>
</html>
