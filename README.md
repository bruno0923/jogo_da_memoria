# jogo_da_memoria
Meu jogo de memória
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jogo Da Memória</title>
</head>
<link rel="stylesheet" href="./src/styles/reset.css">
<link rel="stylesheet" href="./src/styles/main.css">
<body>
    <div class="container">
        <h2>Jogo da Memória</h2>
        <div class="game"></div>
        <button class="reset"  onclick="window.location.reload()">RESET GAME</button>
    </div>
    
    <script src="./src/scripts/engine.js" defer></script>
</body>
</html>

<!--main.CSS -->

body{
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background: #fc1e8a;
    user-select: none;

}

.container {
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 30px;
    background: linear-gradient(325deg,
    #03001e 0%, #7303c0 30%, #ec38bc 70%, #fdeff9 100%);
    padding: 40px 60px;

}

h2 {
    font-size: 3em;
    color: #fff;
    text-transform: uppercase;
    letter-spacing: 0.1em;
}

.reset {
    padding: 15px 20px;
    width: 100%;
    color: #000;
    background-color: #fff;
    border: none;
    font-size: 1.5em;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    cursor: pointer;
    font-weight: 600;
}

.reset:focus{
    color: #ec38bc;
    background-color: #262809;
}

.game{
    width: 430px;
    height: 430px;
    display: flex;
    flex-wrap: wrap;
    gap:10px;
    transform-style: preserve-3d;
    perspective: 500px;
}

.item{
    position: relative;
    width: 100px;
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #fff;
    
    font-size: 3em;
    transform: rotateY('180deg');
    transition: 0.25s;
}

.item :: after{
    content: "";
    position: absolute;
    inset: 0;
    background: #404040;
    /*opacity: 0.85;*/
    transition: 0.25s;
    transform: rotateY('0deg');
    backface-visibility: hidden;
}

.item.boxOpen {
    transform: rotateY('0deg');
}

.item.boxOpen::after,
.boxMacht{
    transform: rotateY('180deg');
}

<!-- reset.css -->
* {
    margin: 0;
    padding: 0;
    outline: none;
    box-sizing: border-box;
    font-family: monospace;
}

<!-- engine.js -->

const emojis = [
   "📺",
   "📺",
   "🤑",
   "🤑",
   "😤",
   "😤", 
   "🤡",
   "🤡",
   "👹",
   "👹",
   "👻",
   "👻",
   "😺",
   "😺",
   "👽",
   "👽",
   "🍕",
   "🍕",
];
let openCard = [];

let shuffleEmojis = emojis.sort( (Math.random() > 0.5 ? 2 : -1));

for(let i=0; i <emojis.length; i++)
{
    let box = document.createElement
    ("div");
    box.className = "item";
    box.innerHTML = shuffleEmojis[i];
    box.onclick = handleclick;
    document.querySelector(".game").appendChild(box);
}

function handleclick() {
    if(openCard.length < 2) {
        this.classList.add("boxOpen");
        openCards.push(this);
    }

    if (openCards.length == 2) {
        setTimeout(checkMatch, 500);
    }

    console.log(openCards);
}

function checkMatch() {
    if(openCards[1].innerHTML === openCards[1].innerHTML) {
        openCards[0].classList.add("boxMatch")
        openCards[1].classList.add("boxMatch")
    }else{
        openCards[0]classList.remove("boxOpen");
        openCards[1]classList.remove("boxOpen");
    }

    openCards = [];

    if(document.querySelectorAll("boxMatch").length === emojis.length){
        alert("Você venceu !");
    }
};

