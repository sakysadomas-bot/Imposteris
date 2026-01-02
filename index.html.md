  
<!DOCTYPE html>  
<html lang="lt">  
<head>  
<meta charset="UTF-8">  
<meta name="viewport" content="width=device-width, initial-scale=1.0">  
<title>Imposter</title>  
  
<style>  
body {  
    margin: 0;  
    background: #0b132b;  
    color: white;  
    font-family: -apple-system, BlinkMacSystemFont, Arial;  
}  
  
.app {  
    max-width: 400px;  
    margin: auto;  
    padding: 20px;  
    text-align: center;  
    animation: fadeIn 0.6s ease;  
}  
  
@keyframes fadeIn {  
    from { opacity: 0; transform: translateY(10px); }  
    to { opacity: 1; transform: translateY(0); }  
}  
  
.hidden {  
    display: none;  
}  
  
h1 {  
    font-size: 28px;  
}  
  
input, button {  
    width: 100%;  
    padding: 16px;  
    font-size: 18px;  
    margin-top: 12px;  
    border-radius: 14px;  
    border: none;  
}  
  
button {  
    background: #5bc0be;  
    font-weight: bold;  
}  
  
.word {  
    font-size: 38px;  
    margin-top: 30px;  
    color: #6fffe9;  
    animation: fadeIn 0.4s ease;  
}  
  
.overlay {  
    position: fixed;  
    inset: 0;  
    background: black;  
    display: none;  
    justify-content: center;  
    align-items: center;  
    color: white;  
    font-size: 22px;  
    text-align: center;  
    z-index: 10;  
    animation: fadeIn 0.4s ease;  
}  
</style>  
</head>  
  
<body>  
  
<div class="overlay" id="overlay">  
    <div>  
        📵 Perduok telefoną<br><br>  
        <button onclick="nextPlayer()">Tęsti</button>  
    </div>  
</div>  
  
<div class="app">  
  
<h1 id="title">🕵️ Imposter</h1>  
  
<div id="setup">  
    <input type="number" id="players" min="3" max="10" value="3">  
    <input type="number" id="time" min="1" max="10" value="3">  
    <small>⏱ Žodžio rodymo laikas (sek.)</small>  
    <button onclick="startGame()">Pradėti</button>  
</div>  
  
<div id="game" class="hidden">  
    <h2 id="playerText"></h2>  
    <button onclick="showWord()">Rodyti žodį</button>  
    <div class="word" id="word"></div>  
</div>  
  
</div>  
  
<script>  
const wordPairs = [  
  
const wordPairs = [  
    ["katė", "šuo"],  
    ["liūtas", "tigras"],  
    ["arklys", "karvė"],  
    ["pica", "mėsainis"],  
    ["makaronai", "ryžiai"],  
    ["sriuba", "troškinys"],  
    ["jūra", "ežeras"],  
    ["upė", "kanalas"],  
    ["paplūdimys", "krantas"],  
    ["mokykla", "universitetas"],  
    ["pamoka", "paskaita"],  
    ["mokytojas", "dėstytojas"],  
    ["telefonas", "planšetė"],  
    ["kompiuteris", "nešiojamas"],  
    ["ausinės", "kolonėlė"],  
    ["dviratis", "paspirtukas"],  
    ["automobilis", "motociklas"],  
    ["traukinys", "metro"],  
    ["futbolas", "krepšinis"],  
    ["tenisas", "badmintonas"],  
    ["plaukimas", "nardymas"],  
    ["filmas", "serialas"],  
    ["kino teatras", "televizorius"],  
    ["aktorius", "režisierius"],  
    ["vasara", "pavasaris"],  
    ["žiema", "ruduo"],  
    ["lietus", "sniegas"],  
    ["miestas", "kaimas"],  
    ["butas", "namas"],  
    ["gatvė", "prospektas"],  
    ["detektyvas", "policininkas"],  
    ["vagis", "nusikaltėlis"],  
    ["paslaptis", "mįslė"],  
    ["žaidimas", "varžybos"],  
    ["laimėjimas", "pergalė"],  
    ["pralaimėjimas", "nesėkmė"]  
];  
  
let words = [];  
let current = 0;  
let showing = false;  
let showTime = 3000;  
  
// 🔊 Detektyvinis / būgno garsas (be failų)  
const drumSound = new Audio("https://actions.google.com/sounds/v1/drums/tribal_drum_roll.ogg");  
  
function vibrateStrong() {  
    if (navigator.vibrate) {  
        navigator.vibrate([200, 100, 200, 100, 300]);  
    }  
}  
  
function startGame() {  
    const count = Number(players.value);  
    showTime = Number(time.value) * 1000;  
  
    const pair = wordPairs[Math.floor(Math.random() * wordPairs.length)];  
  
    words = Array(count).fill(pair[0]);  
    words[Math.floor(Math.random() * count)] = pair[1];  
  
    current = 0;  
  
    setup.classList.add("hidden");  
    game.classList.remove("hidden");  
  
    playerText.innerText = "Žaidėjas 1";  
    word.innerText = "";  
}  
  
function showWord() {  
    if (showing) return;  
  
    vibrateStrong();  
    showing = true;  
    word.innerText = words[current];  
  
    setTimeout(() => {  
        word.innerText = "";  
        overlay.style.display = "flex";  
        showing = false;  
    }, showTime);  
}  
  
function nextPlayer() {  
    overlay.style.display = "none";  
    current++;  
  
    if (current < words.length) {  
        playerText.innerText = `Žaidėjas ${current + 1}`;  
    } else {  
        game.classList.add("hidden");  
        title.innerText = "🎧 Žaidimas prasideda!";  
        drumSound.play();  
    }  
}  
</script>  
  
</body>  
</html>  
