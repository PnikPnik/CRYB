<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>nu8n – The Contradictory Manifesto</title>
  <style>
    body {
      background: #f2f2f2;
      font-family: sans-serif;
      color: #111;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      cursor: pointer;
      text-align: center;
      padding: 2rem;
    }
    .text {
      font-size: 2rem;
      max-width: 700px;
      transition: opacity 0.4s ease;
    }
    .glitch {
      animation: glitch 0.2s infinite;
    }
    @keyframes glitch {
      0% { transform: translate(0); }
      20% { transform: translate(-1px, 1px); }
      40% { transform: translate(2px, -1px); }
      60% { transform: translate(-1px, 2px); }
      80% { transform: translate(1px, -1px); }
      100% { transform: translate(0); }
    }
    #langToggle {
      position: absolute;
      top: 1rem;
      right: 1rem;
      padding: 0.5rem 1rem;
      font-size: 1rem;
      background: #111;
      color: #fff;
      border: none;
      cursor: pointer;
      border-radius: 5px;
    }
  </style>
</head>
<body>
  <button id="langToggle">Deutsch</button>
  <div class="text" id="manifest"></div>
  <audio id="clickSound" src="https://actions.google.com/sounds/v1/alarms/beep_short.ogg"></audio>

  <script>
    const manifest = {
      en: [
        ["We do because we must.", "We must do nothing."],
        ["Doing is origin.", "Doing always comes too late."],
        ["There is no intention.", "Except the one to claim that."],
        ["Every act is pure.", "Every act is tainted with meaning."],
        ["To ask is to lose the act.", "To not ask is to remain empty."],
        ["We believe in making.", "We doubt all that arises."],
        ["Form is an accident.", "Form is the only comfort."],
        ["All doing is now.", "All doing is a memory of soon."],
        ["The work is not important.", "The work is the reason we still exist."],
        ["We act in the name of nothing.", "We shout a name into that nothing."],
        ["Only doing counts.", "Only not-doing remains."],
        ["nu8n is the law.", "nu8n is a stutter. A mistake. A path."]
      ],
      de: [
        ["Wir tun, weil wir müssen.", "Wir müssen gar nichts tun."],
        ["Tun ist Ursprung.", "Tun kommt immer zu spät."],
        ["Es gibt keine Absicht.", "Außer der, das zu behaupten."],
        ["Jede Handlung ist rein.", "Jede Handlung ist bedeutungskrank."],
        ["Fragen heißt verlieren.", "Nicht fragen heißt leer bleiben."],
        ["Wir glauben ans Machen.", "Wir zweifeln an allem, was entsteht."],
        ["Form ist Zufall.", "Form ist Trost."],
        ["Alles Tun ist jetzt.", "Alles Tun ist Erinnerung an gleich."],
        ["Das Werk ist nicht wichtig.", "Das Werk hält uns am Leben."],
        ["Wir handeln aus Nichts.", "Wir rufen einen Namen ins Nichts."],
        ["Nur das Tun zählt.", "Nur das Nichttun bleibt."],
        ["nu8n ist Gesetz.", "nu8n ist Stottern. Fehler. Weg."]
      ]
    };

    let current = null;
    let lang = "en";

    function showRandomPair() {
      const sound = document.getElementById("clickSound");
      sound.currentTime = 0;
      sound.play();

      const data = manifest[lang];
      let index;
      do {
        index = Math.floor(Math.random() * data.length);
      } while (index === current);
      current = index;

      const pair = data[index];
      const textElement = document.getElementById("manifest");
      textElement.classList.remove("glitch");
      textElement.style.opacity = 0;

      setTimeout(() => {
        textElement.innerHTML = `<div>${pair[0]}</div><div style='margin-top:1rem;'>${pair[1]}</div>`;
        textElement.style.opacity = 1;
        textElement.classList.add("glitch");
      }, 400);
    }

    document.body.addEventListener("click", showRandomPair);
    window.onload = showRandomPair;

    document.getElementById("langToggle").addEventListener("click", (e) => {
      lang = lang === "en" ? "de" : "en";
      e.target.textContent = lang === "en" ? "Deutsch" : "English";
      current = null;
      showRandomPair();
    });
  </script>
</body>
</html>
