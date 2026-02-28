<!DOCTYPE html>
<html lang="ca">
<head>
  <meta charset="UTF-8" />
  <title>App de Fitness Personalitzada</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    * {
      box-sizing: border-box;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }

    body {
      margin: 0;
      background: #0f172a;
      color: #e5e7eb;
      display: flex;
      justify-content: center;
      padding: 20px;
    }

    .app {
      width: 100%;
      max-width: 800px;
      background: #020617;
      border-radius: 16px;
      padding: 24px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.6);
      border: 1px solid #1f2937;
    }

    h1 {
      margin-top: 0;
      font-size: 1.8rem;
      text-align: center;
      color: #f97316;
    }

    p.subtitle {
      text-align: center;
      color: #9ca3af;
      margin-top: 4px;
      margin-bottom: 24px;
      font-size: 0.95rem;
    }

    form {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
      margin-bottom: 24px;
    }

    .field {
      display: flex;
      flex-direction: column;
      gap: 4px;
    }

    label {
      font-size: 0.85rem;
      color: #9ca3af;
    }

    input, select {
      padding: 8px 10px;
      border-radius: 8px;
      border: 1px solid #374151;
      background: #020617;
      color: #e5e7eb;
      font-size: 0.95rem;
    }

    input:focus, select:focus {
      outline: 2px solid #f97316;
      border-color: transparent;
    }

    .full-width {
      grid-column: 1 / -1;
    }

    button {
      width: 100%;
      padding: 10px 14px;
      border-radius: 999px;
      border: none;
      background: linear-gradient(135deg, #f97316, #fb923c);
      color: #111827;
      font-weight: 600;
      font-size: 1rem;
      cursor: pointer;
      transition: transform 0.1s ease, box-shadow 0.1s ease, opacity 0.1s ease;
    }

    button:hover {
      transform: translateY(-1px);
      box-shadow: 0 10px 20px rgba(248, 113, 22, 0.35);
      opacity: 0.95;
    }

    button:active {
      transform: translateY(0);
      box-shadow: none;
      opacity: 0.9;
    }

    .result {
      background: #020617;
      border-radius: 12px;
      border: 1px solid #1f2937;
      padding: 16px 18px;
    }

    .result h2 {
      margin-top: 0;
      font-size: 1.2rem;
      color: #f97316;
    }

    .result p {
      margin: 6px 0;
      font-size: 0.95rem;
      color: #e5e7eb;
    }

    .tag {
      display: inline-block;
      padding: 2px 8px;
      border-radius: 999px;
      font-size: 0.75rem;
      background: #111827;
      color: #9ca3af;
      margin-left: 6px;
    }

    ul {
      padding-left: 18px;
      margin: 8px 0;
    }

    li {
      margin-bottom: 4px;
      font-size: 0.95rem;
    }

    .small {
      font-size: 0.8rem;
      color: #6b7280;
      margin-top: 10px;
    }

    @media (max-width: 640px) {
      form {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <div class="app">
    <h1>Programa d'entrenament personalitzat</h1>
    <p class="subtitle">
      Introdueix les teves dades i genera un pla bàsic adaptat al teu objectiu.
    </p>

    <form id="fitnessForm">
      <div class="field">
        <label for="name">Nom</label>
        <input type="text" id="name" placeholder="Ex: Marta" />
      </div>

      <div class="field">
        <label for="age">Edat (anys)</label>
        <input type="number" id="age" min="10" max="100" placeholder="Ex: 30" required />
      </div>

      <div class="field">
        <label for="height">Alçada (cm)</label>
        <input type="number" id="height" min="120" max="230" placeholder="Ex: 170" required />
      </div>

      <div class="field">
        <label for="weight">Pes (kg)</label>
        <input type="number" id="weight" min="30" max="250" placeholder="Ex: 70" required />
      </div>

      <div class="field full-width">
        <label for="goal">Objectiu principal</label>
        <select id="goal" required>
          <option value="">Selecciona un objectiu…</option>
          <option value="perdre_pes">Perdre pes</option>
          <option value="guanyar_muscul">Guanyar múscul</option>
          <option value="mantenir">Mantenir-se en forma</option>
        </select>
      </div>

      <div class="field full-width">
        <button type="submit">Generar programa</button>
      </div>
    </form>

    <div class="result" id="resultBox" style="display:none;">
      <h2 id="resultTitle"></h2>
      <p id="resultSummary"></p>
      <p id="resultStats"></p>

      <p><strong>Programa setmanal recomanat</strong><span class="tag" id="intensityTag"></span></p>
      <ul id="workoutList"></ul>

      <p class="small">
        Aquest programa és orientatiu i molt bàsic. Per a un seguiment professional, consulta un entrenador o metge.
      </p>
    </div>
  </div>

  <script>
    const form = document.getElementById("fitnessForm");
    const resultBox = document.getElementById("resultBox");
    const resultTitle = document.getElementById("resultTitle");
    const resultSummary = document.getElementById("resultSummary");
    const resultStats = document.getElementById("resultStats");
    const workoutList = document.getElementById("workoutList");
    const intensityTag = document.getElementById("intensityTag");

    form.addEventListener("submit", function (e) {
      e.preventDefault();

      const name = document.getElementById("name").value.trim() || "Usuari";
      const age = parseInt(document.getElementById("age").value, 10);
      const height = parseInt(document.getElementById("height").value, 10);
      const weight = parseFloat(document.getElementById("weight").value);
      const goal = document.getElementById("goal").value;

      if (!age || !height || !weight || !goal) {
        alert("Si us plau, omple totes les dades obligatòries.");
        return;
      }

      // Càlcul molt bàsic de l'IMC
      const heightMeters = height / 100;
      const bmi = weight / (heightMeters * heightMeters);
      let bmiCategory = "";

      if (bmi < 18.5) bmiCategory = "baix pes";
      else if (bmi < 25) bmiCategory = "pes saludable";
      else if (bmi < 30) bmiCategory = "sobrepès";
      else bmiCategory = "obesitat";

      // Text segons objectiu
      let goalText = "";
      let intensity = "";
      let workouts = [];

      if (goal === "perdre_pes") {
        goalText = "perdre greix corporal de manera progressiva i saludable.";
        intensity = "Intensitat moderada";
        workouts = [
          "3 dies de cardio suau a moderat (30–40 minuts: caminar ràpid, bici, el·líptica).",
          "2 dies de força total (cos complet) amb pes lleuger a moderat.",
          "1 dia d'activitat lleugera (passeig llarg, mobilitat, estiraments)."
        ];
      } else if (goal === "guanyar_muscul") {
        goalText = "guanyar massa muscular i força de forma gradual.";
        intensity = "Intensitat mitjana-alta";
        workouts = [
          "3 dies d'entrenament de força (dividint tren superior / tren inferior).",
          "1–2 dies de cardio suau (20–30 minuts) per mantenir la salut cardiovascular.",
          "1 dia de mobilitat i estiraments actius."
        ];
      } else if (goal === "mantenir") {
        goalText = "mantenir-te actiu, saludable i amb bona condició física general.";
        intensity = "Intensitat moderada";
        workouts = [
          "2–3 dies de força (cos complet o circuits).",
          "2 dies de cardio moderat (30 minuts).",
          "1 dia d'activitat lleugera i estiraments."
        ];
      }

      // Ajust molt simple segons edat (només text)
      let ageNote = "";
      if (age < 18) {
        ageNote = "Recorda que, si ets menor, és important entrenar sota supervisió adequada.";
      } else if (age > 50) {
        ageNote = "Posa especial atenció a l'escalfament i a la tècnica per protegir les articulacions.";
      }

      // Omplim la interfície
      resultTitle.textContent = `Hola, ${name}!`;
      resultSummary.textContent = `Hem creat un programa bàsic pensat per ${goalText}`;
      resultStats.textContent = `IMC aproximat: ${bmi.toFixed(1)} (${bmiCategory}). Edat: ${age} anys, Pes: ${weight} kg, Alçada: ${height} cm. ${ageNote}`;
      intensityTag.textContent = intensity;

      workoutList.innerHTML = "";
      workouts.forEach(item => {
        const li = document.createElement("li");
        li.textContent = item;
        workoutList.appendChild(li);
      });

      resultBox.style.display = "block";
      resultBox.scrollIntoView({ behavior: "smooth" });
    });
  </script>
</body>
</html>
