
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Will You Be My Valentine? 💗</title>

<style>
* {
    box-sizing: border-box;
}

    :root {
        --pink: #ffb6cf;
        --hot-pink: #ff4f91;
        --dark-red: #650015;
        --green: #20a65a;
    }

body {
    margin: 0;
    min-height: 100vh;
    font-family: Georgia, serif;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow-x: hidden;
    background: linear-gradient(135deg, #ffc3d8, #ffe8f0, #ffb1cf);
    color: #a71950;
    transition: background 0.6s ease, color 0.6s ease;
}

/* DARK RED MODE: hovering over NO */
body.no-mode {
    background: linear-gradient(135deg, #650015, #a00028, #36000d);
    color: #ffd7e2;
}

body.no-mode .card {
    background: #4b0018eF;
    border-color: #ff647f;
    box-shadow: 0 0 45px #ff173c66;
}

/* VIBRANT MODE: hovering over YES */
body.yes-mode {
    background: linear-gradient(135deg, #ff69a6, #ffb5d4, #ff4f91);
}

body.yes-mode .card {
    box-shadow: 0 0 55px #ffffffcc;
    border-color: white;
}

.flowers {
    position: fixed;
    inset: 0;
    overflow: hidden;
    pointer-events: none;
    z-index: 0;
}

.flower {
    position: absolute;
    font-size: clamp(22px, 4vw, 44px);
    opacity: 0.9;
    animation: float 4s ease-in-out infinite alternate;
    transition: transform 0.6s, filter 0.6s, opacity 0.6s;
}

@keyframes float {
    from { translate: 0 0; }
    to { translate: 0 -12px; }
}

/* Flowers wilt when NO is hovered */
.flower.wilted {
    transform: rotate(90deg) scale(0.65);
    filter: grayscale(1) brightness(0.55);
    opacity: 0.5;
    animation: none;
}

/* Flowers bloom when YES is hovered */
.flower.bloomed {
    transform: scale(1.45);
    filter: saturate(1.8) brightness(1.2);
}

.card {
    position: relative;
    z-index: 1;
    width: min(92%, 520px);
    margin: 25px 0;
    padding: 30px 24px;
    text-align: center;
    border: 2px solid #ffffffc9;
    border-radius: 28px;
    background: #fff4f8e8;
    box-shadow: 0 12px 40px #a72d5925;
    backdrop-filter: blur(8px);
    transition: background 0.6s, box-shadow 0.6s;
}

.subtitle {
    font-size: 17px;
    line-height: 1.5;
    margin: 18px 0 8px;
}

h1 {
    font-size: clamp(30px, 7vw, 43px);
    line-height: 1.2;
    margin: 10px 0 24px;
}

.photo {
    display: block;
    width: min(100%, 330px);
    height: 230px;
    object-fit: cover;
    margin: 0 auto 28px;
    border: 5px solid white;
    border-radius: 20px;
    box-shadow: 0 6px 20px #8b16432b;
}

.buttons {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    gap: 20px;
}

button {
    padding: 14px 28px;
    border: none;
    border-radius: 16px;
    color: white;
    font-family: Georgia, serif;
    font-size: 19px;
    font-weight: bold;
    cursor: pointer;
    transition: transform 0.3s, box-shadow 0.3s;
}

#noButton {
    background: #e5233e;
    box-shadow: 0 5px 0 #941023;
}

#yesButton {
    background: #20a65a;
    box-shadow: 0 5px 0 #126d38;
}

/* The YES button glows while hovered */
body.yes-mode #yesButton {
    transform: scale(1.15);
    box-shadow:
        0 0 12px #80ffad,
        0 0 28px #20e879,
        0 0 50px #00ff77;
}

#noButton:hover {
    transform: scale(1.08);
}

#message {
    display: none;
    margin-top: 26px;
    font-size: 22px;
    line-height: 1.7;
    color: #d51d69;
    font-weight: bold;
    animation: appear 0.5s ease;
}

@keyframes appear {
    from { opacity: 0; transform: scale(0.8); }
    to { opacity: 1; transform: scale(1); }
}

@media (max-width: 400px) {
    .card {
        padding: 24px 16px;
    }

    .photo {
        height: 190px;
    }

    button {
        padding: 13px 22px;
    }
}

@media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
        animation-duration: 0.01ms !important;
        transition-duration: 0.01ms !important;
    }
}
</style>
</head>

<body>

<div class="flowers" id="flowers"></div>

<main class="card">

    <div style="font-size: 32px;">💌 🌹 🌼</div>

    <p class="subtitle">
        There's something I've been meaning to ask you...
    </p>

    <h1>Will you be my Valentine? 💗</h1>

    <!-- CHANGE photo.jpg TO YOUR IMAGE'S FILE NAME -->
    <img
        class="photo"
        src="photo.jpg"
        alt="A special picture"
    >

    <div class="buttons">
        <button id="noButton" type="button">No 💔</button>
        <button id="yesButton" type="button">Yes! 💚</button>
    </div>

    <div id="message">
        YAYYYY!! 💖🌹<br>
        You just made my heart bloom!<br>
        Happy Valentine's Day! 💋
    </div>

    <p style="font-size: 13px; margin-top: 25px;">
        Made with love, roses, and daisies. 🌷
    </p>

</main>

<script>
const body = document.body;
const flowerContainer = document.getElementById("flowers");
const noButton = document.getElementById("noButton");
const yesButton = document.getElementById("yesButton");
const message = document.getElementById("message");

let answered = false;

const flowerTypes = ["🌹", "🌼", "🌸", "🌷", "🌼", "🌹"];
const flowerElements = [];

/* Scatter flowers all over the background */
for (let i = 0; i < 38; i++) {
    const flower = document.createElement("span");

    flower.className = "flower";
    flower.textContent =
        flowerTypes[Math.floor(Math.random() * flowerTypes.length)];

    flower.style.left = Math.random() * 96 + "%";
    flower.style.top = Math.random() * 96 + "%";
    flower.style.animationDelay = Math.random() * -4 + "s";

    flowerContainer.appendChild(flower);
    flowerElements.push(flower);
}

function resetFlowers() {
    flowerElements.forEach(flower => {
        flower.classList.remove("wilted", "bloomed");
    });
}

function restoreDefault() {
    if (answered) return;

    body.classList.remove("no-mode", "yes-mode");
    resetFlowers();
}

/* HOVER OVER NO: dark red screen and wilted flowers */
noButton.addEventListener("mouseenter", () => {
    if (answered) return;

    body.classList.add("no-mode");
    body.classList.remove("yes-mode");

    flowerElements.forEach(flower => {
        flower.classList.remove("bloomed");
        flower.classList.add("wilted");
    });
});

/* LEAVE NO: restore original pink */
noButton.addEventListener("mouseleave", restoreDefault);

/* HOVER OVER YES: vibrant screen and blooming flowers */
yesButton.addEventListener("mouseenter", () => {
    if (answered) return;

    body.classList.remove("no-mode");
    body.classList.add("yes-mode");

    resetFlowers();

    flowerElements.forEach(flower => {
        flower.classList.add("bloomed");
    });
});

/* LEAVE YES: restore original pink */
yesButton.addEventListener("mouseleave", restoreDefault);

/* YES CLICK: show the happy ending */
yesButton.addEventListener("click", () => {
    answered = true;

    body.classList.remove("no-mode");
    body.classList.add("yes-mode");

    resetFlowers();

    flowerElements.forEach(flower => {
        flower.classList.add("bloomed");
    });

    message.style.display = "block";
    yesButton.textContent = "YESSS!! 💖";
    noButton.style.display = "none";

    /* Falling hearts and flowers */
    for (let i = 0; i < 30; i++) {
        const heart = document.createElement("span");

        heart.textContent = ["💖", "💕", "💗", "🌹", "🌼"][
            Math.floor(Math.random() * 5)
        ];

        heart.style.position = "fixed";
        heart.style.left = Math.random() * 100 + "vw";
        heart.style.top = "-50px";
        heart.style.fontSize = "28px";
        heart.style.zIndex = "10";
        heart.style.pointerEvents = "none";
        heart.style.transition =
            `top ${2 + Math.random() * 2}s linear`;

        document.body.appendChild(heart);

        requestAnimationFrame(() => {
            heart.style.top = "105vh";
        });

        setTimeout(() => heart.remove(), 4500);
    }
});

/* Touchscreen support */
noButton.addEventListener("click", () => {
    if (answered) return;

    body.classList.add("no-mode");
    body.classList.remove("yes-mode");

    flowerElements.forEach(flower => {
        flower.classList.remove("bloomed");
        flower.classList.add("wilted");
    });
});

yesButton.addEventListener("touchstart", () => {
    if (answered) return;

    body.classList.remove("no-mode");
    body.classList.add("yes-mode");

    resetFlowers();

    flowerElements.forEach(flower => {
        flower.classList.add("bloomed");
    });
}, { passive: true });
</script>

</body>
</html>
