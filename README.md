<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>Calculatrice Poker</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
  body {
    font-family: Arial, sans-serif;
    background: #121212;
    color: #fff;
    max-width: 400px;
    margin: auto;
    padding: 20px;
  }
  h2 {
    text-align: center;
    margin-bottom: 20px;
    color: #00ffae;
  }
  label {
    display: block;
    margin-top: 15px;
    font-size: 16px;
  }
  input {
    width: 100%;
    padding: 10px;
    margin-top: 8px;
    font-size: 16px;
    border-radius: 8px;
    border: none;
  }
  button {
    width: 100%;
    padding: 12px;
    margin-top: 20px;
    font-size: 18px;
    font-weight: bold;
    background: #00ffae;
    color: #000;
    border: none;
    border-radius: 8px;
    cursor: pointer;
  }
  button:hover {
    background: #00e69a;
  }
  .result {
    margin-top: 20px;
    padding: 15px;
    background: #1f1f1f;
    border-radius: 8px;
    font-size: 16px;
  }
</style>
</head>
<body>
<h2>Calculatrice Poker</h2>

<label>Pot actuel (en BB) :</label>
<input type="number" id="pot" placeholder="Ex: 10">

<label>Mise à payer (en BB) :</label>
<input type="number" id="mise" placeholder="Ex: 5">

<label>Nombre d'outs :</label>
<input type="number" id="outs" placeholder="Ex: 9">

<button onclick="calculer()">Calculer</button>

<div class="result" id="result"></div>

<script>
function calculer() {
  let pot = parseFloat(document.getElementById('pot').value);
  let mise = parseFloat(document.getElementById('mise').value);
  let outs = parseFloat(document.getElementById('outs').value);

  if (isNaN(pot) || isNaN(mise) || isNaN(outs)) {
    document.getElementById('result').innerHTML = "⚠️ Remplis tous les champs.";
    return;
  }

  let potFinal = pot + mise + mise; // pot actuel + mise adverse + ton call
  let cote = (mise / potFinal) * 100;

  let probaFlop = outs * 4; // règle du 4 (flop -> river)
  let probaTurn = outs * 2; // règle du 2 (turn -> river)

  let verdictFlop = probaFlop >= cote ? "✅ CALL OK" : "❌ FOLD";
  let verdictTurn = probaTurn >= cote ? "✅ CALL OK" : "❌ FOLD";

  document.getElementById('result').innerHTML = `
    💰 Cote du pot : ${cote.toFixed(1)}%<br>
    📊 Probabilité (Flop→River): ${probaFlop}% → ${verdictFlop}<br>
    📊 Probabilité (Turn→River): ${probaTurn}% → ${verdictTurn}
  `;
}
</script>
</body>
</html>
