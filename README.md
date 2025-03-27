<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page 2</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f5f5f5;
    }
    .container {
      padding: 20px;
      text-align: center;
      position: relative;
      min-height: 100vh;
    }
    .button-back {
      position: fixed;
      top: 20px;
      left: 20px;
      padding: 10px 20px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .post-it {
      background-color: #fef6a1;
      padding: 20px;
      width: 1000px;
      margin-bottom: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      font-size: 18px;
      position: relative;
    }
    .column {
      display: flex;
      justify-content: center;
      gap: 20px;
    }
    .box {
      background-color: #fef6a1;
      padding: 20px;
      width: 30%;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      font-size: 16px;
      text-align: center;
      position: relative;
    }
    .item {
      padding: 10px;
      margin: 10px 0;
      background-color: #fff;
      border: 1px solid #000;
      border-radius: 5px;
      cursor: pointer;
    }
    .context-menu {
      position: absolute;
      background-color: white;
      border: 1px solid #ccc;
      border-radius: 5px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      z-index: 1000;
    }
    .context-menu div {
      padding: 10px;
      cursor: pointer;
      border-bottom: 1px solid #ccc;
    }
    .context-menu div:last-child {
      border-bottom: none;
    }
    .footer {
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100%;
      text-align: center;
      font-size: 14px;
      color: #666;
      background-color: #fef6a1;
      padding: 5px 0;
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- Zurück Button -->
    <div class="button-back" onclick="window.location.href='index.html'">Zurück zur Seite 1</div>

    <!-- Info Post-It -->
    <div class="post-it">
      <h2>Info</h2>
      <p>Dies ist ein längliches Post-It, das fast den ganzen Bildschirm ausfüllt!</p>
    </div>

    <!-- Stände, TODOs, Termine -->
    <div class="column">
      <!-- Stände -->
      <div class="box">
        <h3>Stände</h3>
        <div id="stands-list"></div>
        <div>
          <input type="text" id="new-stand" placeholder="Neuen Stand hinzufügen" />
          <button onclick="addStand()">Hinzufügen</button>
        </div>
      </div>

      <!-- TODO -->
      <div class="box">
        <h3>TODO</h3>
        <div id="todos-list"></div>
        <div>
          <input type="text" id="new-todo" placeholder="Neues TODO hinzufügen" />
          <button onclick="addTodo()">Hinzufügen</button>
        </div>
      </div>

      <!-- Termine -->
      <div class="box">
        <h3>Termine</h3>
        <div id="termine-list"></div>
        <div>
          <input type="text" id="new-termine" placeholder="Neuen Termin hinzufügen" />
          <button onclick="addTermine()">Hinzufügen</button>
        </div>
      </div>
    </div>
    
    <!-- Kontextmenü -->
    <div id="context-menu" class="context-menu" style="display: none;"></div>

    <!-- Footer -->
    <div class="footer">
      <strong>Impressum:</strong> <br />
      Martin Platter <br />
      26.03.2025
    </div>
  </div>

  <script>
    // Zustände
    let stands = [];
    let todos = [];
    let termine = [];
    let contextMenu = null;

    // Funktionen zum Hinzufügen
    function addStand() {
      const standInput = document.getElementById("new-stand");
      const newStand = standInput.value.trim();
      if (newStand) {
        stands.push(newStand);
        standInput.value = '';
        renderLists();
      }
    }

    function addTodo() {
      const todoInput = document.getElementById("new-todo");
      const newTodo = todoInput.value.trim();
      if (newTodo) {
        todos.push(newTodo);
        todoInput.value = '';
        renderLists();
      }
    }

    function addTermine() {
      const termineInput = document.getElementById("new-termine");
      const newTermine = termineInput.value.trim();
      if (newTermine) {
        termine.push(newTermine);
        termineInput.value = '';
        renderLists();
      }
    }

    // Funktion zum Rendern der Listen
    function renderLists() {
      document.getElementById("stands-list").innerHTML = stands.map((stand, index) => `
        <div class="item" oncontextmenu="showContextMenu(event, 'stand', ${index})">${stand}</div>
      `).join('');
      
      document.getElementById("todos-list").innerHTML = todos.map((todo, index) => `
        <div class="item" oncontextmenu="showContextMenu(event, 'todo', ${index})">${todo}</div>
      `).join('');
      
      document.getElementById("termine-list").innerHTML = termine.map((termin, index) => `
        <div class="item" oncontextmenu="showContextMenu(event, 'termine', ${index})">${termin}</div>
      `).join('');
    }

    // Kontextmenü anzeigen
    function showContextMenu(event, type, index) {
      event.preventDefault();
      contextMenu = { x: event.clientX, y: event.clientY, type, index };
      const menu = document.getElementById("context-menu");
      menu.style.top = `${contextMenu.y}px`;
      menu.style.left = `${contextMenu.x}px`;
      menu.style.display = "block";
      menu.innerHTML = `
        <div onclick="editItem('${type}', ${index})">Bearbeiten</div>
        <div onclick="deleteItem('${type}', ${index})">Löschen</div>
      `;
    }

    // Kontextmenü schließen
    document.addEventListener("click", () => {
      document.getElementById("context-menu").style.display = "none";
    });

    // Bearbeiten
    function editItem(type, index) {
      const newValue = prompt(`Bearbeite das ${type === 'stand' ? 'Stand' : type === 'todo' ? 'Todo' : 'Termin'}`, type === 'stand' ? stands[index] : type === 'todo' ? todos[index] : termine[index]);
      if (newValue !== null) {
        if (type === 'stand') {
          stands[index] = newValue;
        } else if (type === 'todo') {
          todos[index] = newValue;
        } else if (type === 'termine') {
          termine[index] = newValue;
        }
        renderLists();
      }
    }

    // Löschen
    function deleteItem(type, index) {
      if (type === 'stand') {
        stands.splice(index, 1);
      } else if (type === 'todo') {
        todos.splice(index, 1);
      } else if (type === 'termine') {
        termine.splice(index, 1);
      }
      renderLists();
    }

    // Initialer Render
    renderLists();
  </script>
</body>
</html>
