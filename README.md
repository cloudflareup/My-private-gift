<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy 21st Birthday!</title>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Great+Vibes&family=Playfair+Display:italic,wght@0,400;1,700&family=Montserrat:wght@300;400&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        :root {
            --primary: #d4a5a5;            --secondary: #c9a89a;
            --accent: #8b5a5a;
            --bg: #fdf5f2;
            --text: #5a4a4a;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            background-color: var(--bg);
            color: var(--text);
            font-family: 'Montserrat', sans-serif;
            overflow: hidden; /* Prevents scrolling between pages */
        }

        /* Page Management */
        .page {
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100vh;            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 40px 20px;
            text-align: center;
            background: url('https://www.transparenttextures.com/patterns/paper-fibers.png');
            animation: fadeIn 0.8s ease-in-out;
        }

        .page.active { display: flex; }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }        /* Typography */
        h1 { font-family: 'Great Vibes', cursive; font-size: clamp(3rem, 8vw, 6rem); color: var(--accent); }
        h2 { font-family: 'Dancing Script', cursive; font-size: 2.5rem; color: var(--accent); margin-bottom: 20px; }
        .handwritten { font-family: 'Dancing Script', cursive; font-size: 1.5rem; }
        p { line-height: 1.6; max-width: 600px; }

        /* Buttons */
        .btn {            background: var(--accent);
            color: white;
            border: none;
            padding: 15px 35px;
            font-size: 1.1rem;
            border-radius: 50px;
            cursor: pointer;
            margin-top: 30px;
            transition: 0.3s;
            font-family: 'Montserrat', sans-serif;            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn:hover { background: var(--primary); transform: scale(1.05); }

        /* Timer */
        .timer-container {
            display: flex;
            gap: 20px;
            margin: 30px 0;
            background: white;
            padding: 20px 40px;
            border-radius: 50px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.05);
        }
        .timer-unit span { display: block; font-size: 2rem; font-weight: bold; color: var(--accent); }

        /* Polaroid Grid */
        .polaroid-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 20px;
            width: 100%;
            max-width: 1000px;
            overflow-y: auto;
            padding: 20px;
        }

        .polaroid {
            background: white;
            padding: 10px 10px 30px 10px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            transform: rotate(var(--r));
            transition: 0.3s;
            cursor: pointer;
        }
        .polaroid:hover { transform: scale(1.05) rotate(0deg); z-index: 10; }        .polaroid img { width: 100%; height: 180px; object-fit: cover; }

        /* Stickers */
        .sticker {
            position: absolute;
            width: 100px;
            pointer-events: none;
            z-index: 5;
            animation: float 4s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(var(--r)); }
            50% { transform: translateY(-15px) rotate(calc(var(--r) + 5deg)); }
        }

        /* Letter Styling */
        .letter-box {
            background: white;
            padding: 50px;            border-radius: 5px;
            box-shadow: 0 5px 25px rgba(0,0,0,0.05);
            max-width: 700px;
            text-align: left;
            position: relative;
            font-family: 'Playfair Display', serif;
        }

        /* Modal */
        .modal {
            position: fixed;
            top:0; left:0; width:100%; height:100%;
            background: rgba(0,0,0,0.8);
            display: none;
            justify-content: center;            align-items: center;
            z-index: 1000;
        }
 
 /*Compliment*/
  .compliment-note {
  position: absolute;
  font-family: 'Dancing Script', cursive;
  font-size: 1.5rem;
  background: rgba(255,255,255,0.8);
  padding: 10px 15px;
  border-radius: 10px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.1);
  pointer-events: none; /* clicks pass through */
}
.compliment-note {
  opacity: 0;
  transition: opacity 0.5s ease, transform 0.5s ease;
}

.compliment-note.show {
  opacity: 1;
}

.compliment-note.fade {
  animation: fadeOut 1.5s forwards;
}

@keyframes fadeOut {
  from { opacity: 1; transform: translateY(0); }
  to { opacity: 0; transform: translateY(-20px); }
}

    /*Typing block*/
      .typing-block {
  font-family: 'Montserrat', sans-serif; /* clean */
  font-weight: 600;
  font-size: 1.4rem;
  line-height: 2;
  margin-top: 30px;
}

#idol-img {
  transition: opacity 0.4s ease;
}
     
/* Meme page text */
.meme-text {
  font-family: Calibri, Arial, Helvetica, sans-serif;
  font-size: 1.3rem;
  max-width: 600px;
  margin-bottom: 30px;
  line-height: 1.6;
}

/* Meme image */
.meme-img {
  max-width: 70%;
  max-height: 60vh;
  border-radius: 15px;
  opacity: 0;
}

/* Fade-in animation */
.fade-in {
  animation: fadeInImage 1.8s ease forwards;
}

@keyframes fadeInImage {
  from {
    opacity: 0;
    transform: scale(0.96);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

/* Glow YES button */
@keyframes glowPulse {
  0% {
    box-shadow: 0 0 5px #d4a5a5, 0 0 10px #d4a5a5;
  }
  50% {
    box-shadow: 0 0 20px #ffb3b3, 0 0 40px #ffb3b3;
  }
  100% {
    box-shadow: 0 0 5px #d4a5a5, 0 0 10px #d4a5a5;
  }
}

.glow {
  animation: glowPulse 1.5s infinite;
  transform: scale(1.05);
}

#page13b p {
  font-family: Calibri, Arial, sans-serif;
  font-size: 2.5rem;
  text-align: center;
  margin: auto;
}

#page13b {
  transform: scale(0.95);
  transition: transform 0.8s ease;
}

#page13b.active {
  transform: scale(1);
}

.heart {
  position: absolute;
  width: 25px;
  height: 25px;
  background: red;
  transform: rotate(-45deg);
  pointer-events: none;
  opacity: 0.9;
  animation: floatHeart 1.5s ease-out forwards;
  z-index: 999;
}

/* Create the two circular bumps of the heart using pseudo-elements */
.heart::before,
.heart::after {
  content: "";
  position: absolute;
  width: 25px;
  height: 25px;
  background: red;
  border-radius: 50%;
}

.heart::before {
  top: -12px;
  left: 0;
}

.heart::after {
  left: 12px;
  top: 0;
}

@keyframes floatHeart {
  0% { transform: translateY(0) scale(1) rotate(-45deg); opacity: 0.9; }
  100% { transform: translateY(-120px) scale(1.3) rotate(-45deg); opacity: 0; }
}

#page4b div:hover {
  transform: scale(1.05) rotate(-2deg);
  transition: transform 0.2s;
}


.scroll-video {
  width: 80%;
  max-height: 60vh;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.2);
  opacity: 0.5;       /* slightly faded when not in view */
  transform: scale(0.98);
  transition: opacity 0.6s ease, transform 0.6s ease;
  margin: 0 auto;
  display: block;
}
.scroll-video.in-view {
  opacity: 1;
  transform: scale(1);
}

    </style>
</head>
<body>

  <script>
const pass = prompt("Enter the password");
if (pass !== "purplealien") {
  document.body.innerHTML = "";
}
</script>

  <!-- PAGE 1: THE COUNTDOWN -->
    <section id="page1" class="page active">
        <img src="https://i.ibb.co/1tQWWz3W/IMG-0157.jpg" class="sticker" style="top:10%; left:10%; --r: -15deg">
        <h2 class="handwritten">ITS YOUR BIRTHDAYYY</h2>
        <h1>Happy 21st, my purple alien!</h1>
        <div class="timer-container">
            <div class="timer-unit"><span id="days">00</span><small>Days</small></div>
            <div class="timer-unit"><span id="hours">00</span><small>Hrs</small></div>
            <div class="timer-unit"><span id="mins">00</span><small>Mins</small></div>
            <div class="timer-unit"><span id="secs">00</span><small>Secs</small></div>
        </div>
        
        <div id="ready-gate" style="margin-top: 40px;">
            <p>Are you ready for your surprises?</p>
            <div style="display: flex; gap: 20px; justify-content: center;">                <button class="btn" onclick="nextPage(2)">YES!</button>
                <button class="btn" id="no-btn" onmouseover="moveNo()" onclick="clickNo()">NO</button>
            </div>
        </div>
    </section>
    
    <!-- PAGE 2: THE INTRO -->
    <section id="page2" class="page">
        <img src="https://i.ibb.co/xtzBSrYQ/IMG-0151.jpg" class="sticker" style="top:5%; right:10%; --r: 10deg">
        <div class="letter-box">
            <h2>To my love, my Izekial,</h2>
            <p>Today is not just any birthday. It's the big 21! I've been waiting to celebrate this with you forever (even from afar). You've grown into such a beautiful, kind, and slightly crazy human, and I wouldn't have it any other way (meaning I just love whatever is wrong with you).</p>
            <p style="margin-top: 10px;">I've gathered a few of our best (and most embarrassing) bits here just for you.</p>
            <button class="btn" onclick="nextPage(3)">Open the Vault</button>
        </div>
    </section>

    <!-- PAGE 3: CORE MEMORIES -->
    <section id="page3" class="page">
    <img src="https://i.ibb.co/MkCBjGJv/IMG-0149.jpg" class="sticker" style="top:5%; left:5%; --r:-10deg">
    <img src="https://i.ibb.co/gMtc4qKj/IMG-0155.jpg" class="sticker" style="top:5%; right:5%; --r:10deg">
    <img src="https://i.ibb.co/xtzBSrYQ/IMG-0151.jpg" class="sticker" style="bottom:20%; left:5%; --r:5deg">
        <h2 style="font-size: 3.5rem;">Our Memories</h2>
        <p>A collection of moments that define us and remind us how cringe we were...🙂</p>
        <div class="polaroid-grid">
            <div class="polaroid" style="--r: -2deg"><img src="https://i.ibb.co/jP66Gpxm/IMG-8431.jpg"></div>
            <div class="polaroid" style="--r: 3deg"><img src="https://i.ibb.co/2Yyry7bk/IMG-8104.jpg"></div>
            <div class="polaroid" style="--r: -1deg"><img src="https://i.ibb.co/nMkKKgM2/IMG-8087.jpg"></div>
            <div class="polaroid" style="--r: 2deg"><img src="https://i.ibb.co/cK9YStCc/IMG-8123.jpg"></div>
            <div class="polaroid" style="--r: -3deg"><img src="https://i.ibb.co/fGFF0QRS/IMG-8128.jpg"></div>
            <div class="polaroid" style="--r: 4deg"><img src="https://i.ibb.co/MxW6kFMy/IMG-9274.jpg"></div>
            <div class="polaroid" style="--r: 4deg"><img src="https://i.ibb.co/TMJtM0DN/IMG-1599.jpg"></div>
                       </div>        <button class="btn" onclick="nextPage(8)">Keep Going👾✨</button>
    </section>

    <!-- PAGE 4: INTERACTIVE SURPRISES -->
    <section id="page4" class="page">
        <img src="https://i.ibb.co/bRBQR23d/IMG-0150.jpg" class="sticker" style="bottom:10%; left:5%; --r: -5deg">
        <img src="https://i.ibb.co/1tQWWz3W/IMG-0157.jpg" class="sticker" style="top:20%; left:15%; --r: -10deg">
        <img src="https://i.ibb.co/xtzBSrYQ/IMG-0151.jpg" class="sticker" style="top:50%; right:5%; --r: 20deg; width: 80px;">
        <h2>Tap for Hidden Messages</h2>
        <div class="polaroid-grid">            <div class="polaroid" onclick="alert('You are the smartest person I know (mostly)! 🧠')">                <img src="https://i.ibb.co/5xFnhS4t/IMG-1762495682145.jpg">
                <p class="handwritten">Tap Me</p>
            </div>
            <div class="polaroid" onclick="alert('Remember when we decided not to post anything for each other\'s birthday but couldn\'t resist?')">
                <img src="https://i.ibb.co/MbLcpsV/IMG-1985.jpg">
                <p class="handwritten">Tap Me</p>
            </div>
            <div class="polaroid" onclick="alert('oo, my shayllaaa😭')">
                <img src="https://i.ibb.co/yFYfybNh/26ce5691-02a7-4318-b950-9561d9b74b4d.jpg">
                <p class="handwritten">Tap Me</p>
                </div>
        </div>
        <button class="btn" onclick="nextPage('4b')">I have a secret...</button>
    </section>

    <!-- PAGE 4B: SECRET REVEAL -->
<section id="page4b" class="page">
  <h2>The not so secret secret!</h2>
  <p id="secret-text" style="font-size:1.5rem; margin-top:20px;">Tap the box to reveal it 💌</p>
  
  <div onclick="revealSecret()" 
       style="width:250px; height:150px; background:#c9a89a; border-radius:15px; display:flex; align-items:center; justify-content:center; cursor:pointer; margin:30px auto; font-size:2rem;">
    🎁
  </div>

  <button class="btn" style="display:none;" id="secret-next" onclick="nextPage(5)">Continue to letters</button>
</section>

    <!-- PAGE 5: HEARTFELT LETTER 1 -->
    <section id="page5" class="page">
        <div class="letter-box">
            <h2>The "Thank You" Letter</h2>
            <p>I don't say it enough, but thank you for being the person you are. Thank you for giving me a place that I can always return to. Thank you for the 2 hour phone calls, the shared snacks, and the way you just *know* what I'm thinking without me saying a word.</p>
            <p style="margin-top: 15px;">21 years of you has made the world a much better place. I'm so lucky to have a front-row seat to your life.(It is definitely better than an oscar winning movie)</p>
            <button class="btn" onclick="nextPage('5b')">One More Thing...</button>
        </div>
    </section>
    
<!-- PAGE 5B: SCROLLING VIDEOS WITH FADE-IN AND SOUND -->
<section id="page5b" class="page">
  <h2>You are my muse 🎬</h2>
  <p style="margin-bottom:20px;">
    Proof that you are indeed my muse.
  </p>

  <!-- Vertical scroll container -->
  <div id="videoScroll"
     style="display:flex; flex-direction:column; gap:40px; overflow-y:auto; max-height:70vh; padding:10px 0;">
     
  <video class="scroll-video" playsinline loop preload="metadata"
src="https://www.dropbox.com/scl/fi/mi2jknrzweds2vvr4ur9v/9d98b03811a54665a14cacf1fe1aae75_mov.mp4?raw=1"></video>

<video class="scroll-video" playsinline loop preload="metadata"
src="https://www.dropbox.com/scl/fi/wmb7kk4zg768y8mlbxq30/copy_1F99F3E6_F666_4FAD_89E4_DEB886A915DC_mov.mp4?raw=1"></video>

<video class="scroll-video" playsinline loop preload="metadata"
src="https://www.dropbox.com/scl/fi/alxfjesuxqcj7fd7ugl3k/copy_57EEE68E_8F1A_4308_ACCC_DA049C3E8AB8_mov.mp4?raw=1"></video>

<video class="scroll-video" playsinline loop preload="metadata"
src="https://www.dropbox.com/scl/fi/sqpx6yhehd9n9auu84bwv/copy_285BBAD6_EAB6_4859_8115_81631C5A3AC1_mov.mp4?raw=1"></video>

<video class="scroll-video" playsinline loop preload="metadata"
src="https://www.dropbox.com/scl/fi/o6sxafcsmr5x7sgagtoyz/copy_345ACCDE_3861_4C85_83EF_603E9355E0A9_mov.mp4?raw=1"></video>

<video class="scroll-video" playsinline loop preload="metadata"
src="https://www.dropbox.com/scl/fi/g00wx3dzu1cdnhg4luehk/copy_13845499_2E4F_4D48_99F5_FEB6B4386822_mov.mp4?raw=1"></video>

<video class="scroll-video" playsinline loop preload="metadata"
src="https://www.dropbox.com/scl/fi/mbsp2odqk4ag9qoybr5dg/copy_A8EB858E_4B3F_4AED_A1CC_B775965A532A_mov.mp4?raw=1"></video>

<video class="scroll-video" playsinline loop preload="metadata"
src="https://www.dropbox.com/scl/fi/7pr2qffg899jd84tiigkb/copy_ADA38E56_E475_40E5_9703_41E3C2127337_mov.mp4?raw=1"></video>

<video class="scroll-video" playsinline loop preload="metadata"
src="https://www.dropbox.com/scl/fi/j40jkdpualtfd2wprdilr/copy_CE80C9A3_5B4F_4BE2_8093_98A3B0759F7C_mov.mp4?raw=1"></video>

</div>

  <button class="btn" onclick="nextPage(6)">Be wowed before you click me</button>
  
</section>

    <!-- PAGE 6: HEARTFELT LETTER 2 -->
    <section id="page6" class="page">
        <img src="https://i.ibb.co/MkCBjGJv/IMG-0149.jpg" class="sticker" style="top:15%; right:10%; --r: 20deg">
        <img src="https://i.ibb.co/bRBQR23d/IMG-0150.jpg" class="sticker" style="top:5%; right:5%; --r: 20deg">
        <img src="https://i.ibb.co/0ppdK2vB/IMG-0154.jpg" class="sticker" style="bottom: 8%; left: 10%; --r: -5deg;">
        <img src="https://i.ibb.co/gMtc4qKj/IMG-0155.jpg" class="sticker" style="top: 50%; left: 2%; --r: -25deg; width: 80px;">
        <div class="letter-box">
            <h2>Our Future Adventures</h2>
            <p>Now that you're 21, the world is officially our playground! (as long as our moms agree) I can't wait for the trips we'll take (again moms agreement necessary), the bad decisions we'll make together (that we can do without them knowing), and the thousands of photos we'll take until our phones run out of storage.</p>
            <p style="margin-top: 15px;">Whatever happens, I promise to always be the one cheering the loudest for you even if I am thousand miles away from you. And I stole this line from my colleague- May health be a shadow and follow you, like an obsessed stalker (the last part is mine).</p>
            <button class="btn" onclick="nextPage(7)">The Final Surprise</button>
        </div>
    </section>

    <!-- PAGE 7: FINAL CELEBRATION -->
    <section id="page7" class="page">
    <img src="https://i.ibb.co/FqYmqFF9/IMG-0152.jpg" class="sticker" style="bottom: 10%; right: 10%; --r: 20deg;">
    <img src="https://i.ibb.co/N2tTk467/IMG-0156.jpg" class="sticker" style="top: 50%; left: 2%; --r: -25deg; width: 80px;">
    <img src="https://i.ibb.co/CLrvtDG/IMG-0153.jpg" class="sticker" style="bottom: 8%; left: 10%; --r: -5deg;">
    <img src="https://i.ibb.co/gMtc4qKj/IMG-0155.jpg" class="sticker" style="top: 5%; right: 5%; --r: 15deg;">
    <img src="https://i.ibb.co/MkCBjGJv/IMG-0149.jpg" class="sticker" style="top: 5%; left: 5%; --r: -10deg;">
        <h1>Happy Birthday!</h1>
        <h2 class="handwritten">Go out there and shine like the star you are!</h2>
        <img src="https://i.ibb.co/MbLcpsV/IMG-1985.jpg" style="width: 200px; border-radius: 50%; margin: 20px;">
        <p>I love you to the moon and back!</p>
        <button class="btn" onclick="celebrate()">CELEBRATE! 🎉</button>
    </section>
    
    <!-- PAGE 8: K-POP TREND TITLE -->
    <section id="page8" class="page">
    <h1>K-pop boys I would sell you for, by me</h1>
    <button class="btn" onclick="nextPage(10)">Next</button>
</section>

    
    <!--PAGE 9: COMPLIMENTS -->
    <section id="page9" class="page">
    <h2>You didn’t ask, but here it is</h2>
    <div id="compliment-area" style="position:relative; width:100%; height:60vh;"></div>
    <div style="margin-top:20px; display:flex; gap:20px;">
  <button class="btn" onclick="newCompliment()">Another one, cause you DESERVE it GURL.</button>
  <button class="btn" onclick="nextPage(14)">Next page, only when you are fully mesmerised by my flirting skills😌</button>
  </div>
</section>

    <!-- PAGE 10: NUMBER 1 -->
<section id="page10" class="page">
  <h1>Number 1</h1>
  
  <div id="typing-text"
     class="typing-block">
  </div>
    
</section>

    <!-- PAGE 11: NUMBER 2 RM -->
    <section id="page11" class="page">
  <h1>Number 2— Kim Namjoon</h1>
  <img src="https://i.ibb.co/chCzHfP1/IMG-0171.jpg"
       style="width:280px; border-radius:20px; margin-top:25px;">
</section>


  <!--PAGE 12: NUMBER 3 YOOONGI -->
  <section id="page12" class="page">
  <h1>Number 3- Min Yoongi</h1>
  <img src="https://i.ibb.co/gF4rwZj5/IMG-0172.jpg" 
        style="width:280px; border-radius:20px; margin-top:25px;">
 </section>
 
 <!--PAGE 13: NUMBER 4 ALL MEMBERS -->
  <section id="page13" class="page">
  <h1>Number 4- All of them (I know you would too😒)</h1>
  <img src="https://i.ibb.co/0pR01MHm/IMG-0173.jpg"
       style="width:280px; border-radius:20px; margin-top:25px;">
</section>

<!-- PAGE 13B: MICRO TRANSITION -->
<section id="page13b" class="page">
  <p class="meme-text">
    Anyways… back to reality
  </p>
</section>


<!--PAGE 14: MEME PAGE -->
<section id="page14" class="page">

<p class="meme-text"> Our shared brain cell, in one image: </p>
<img 
src="https://i.ibb.co/d0996RZh/IMG-0174.jpg" 
alt="meme"
class="meme-img"
>

</section>


<script>

document.addEventListener('click', function(e) {
  const heart = document.createElement('div');
  heart.className = 'heart';

  // get exact click position relative to viewport
  heart.style.left = e.clientX - 12 + 'px';
  heart.style.top = e.clientY - 12 + 'px';

  document.body.appendChild(heart);

  setTimeout(() => heart.remove(), 1500);
});

function revealSecret() {
  const text = document.getElementById("secret-text");
  text.innerText = "I have videographic evidence of your most embarrassing dance moves safe in my vault. (Yes that lets kill this love video too) 💃🕺";

  // mini confetti
  confetti({ particleCount: 50, spread: 70, origin: { y: 0.6 } });

  // show continue button
  document.getElementById("secret-next").style.display = "inline-block";
}


let autoTimer;

const worshipText = [
    "ABSOLUTELY NO ONE.",
    "You are my soulmate.",
    "You are my platonic life partner.",
    "You are my safe place.",
    "You are the love of my life in every universe.",
    "You are my ride or die, my diva, my person.",
    "",
    "I would never sell you for anyone."
];
function typeWorshipText() {
  const container = document.getElementById("typing-text");
  if (!container) return;
  
  container.innerHTML = "";
  
  let lineIndex = 0;
  let charIndex = 0;
  let currentLine = document.createElement('div');
  container.appendChild(currentLine);
  
  function type() {
    const line = worshipText[lineIndex];
    
    if (!line) {
      // Finished all lines
      setTimeout(() => nextPage(11), 2500);
      return;
    }
    
    if (charIndex < line.length) {
      currentLine.textContent += line[charIndex];
      charIndex++;
      setTimeout(type, 40);
    } else {
      // Move to next line
      lineIndex++;
      charIndex = 0;
      if (worshipText[lineIndex]) {
        currentLine = document.createElement('div');
        container.appendChild(currentLine);
        setTimeout(type, 500);
      } else {
        // No more lines
        setTimeout(() => nextPage(11), 2500);
      }
    }
  }
  
  type();
}


const compliments = [
  "You could commit a crime and I’d still defend you.",
  "Main character energy. No debate.",
  "If I ever go to war, I would put your picture in my wallet.",
  "If confidence were currency, you’d be illegal.",
  "The universe definitely favors you.",
  "Your smile could start a revolution.",
  "Brains, beauty, and chaos — you have it all.",
  "You make life feel like a movie.",
  "Even Mondays are scared of you.",
  "You’re basically a limited edition masterpiece.",
  "The world isn’t ready for your energy.",
  "You turn ordinary days into adventures.",
  "You radiate vibes that are straight up illegal.",
  "I’d follow you anywhere, no questions asked.",
  "You have the perfect mix of mischief and charm."
];
let unusedCompliments = [...compliments];

function newCompliment() {
  const area = document.getElementById("compliment-area");

  if (unusedCompliments.length === 0) {
    unusedCompliments = [...compliments];
  }

  const index = Math.floor(Math.random() * unusedCompliments.length);
  const text = unusedCompliments.splice(index, 1)[0];

  area.innerHTML = "";

  const note = document.createElement("div");
  note.className = "compliment-note";
  note.innerText = text;

  note.style.top = Math.random() * 50 + 5 + "%";
  note.style.left = Math.random() * 60 + 20 + "%";
  note.style.transform += ` rotate(${Math.random() * 10 - 5}deg)`;

  area.appendChild(note);

  // fade in
  requestAnimationFrame(() => {
    note.classList.add("show");
  });

  // fade out
  setTimeout(() => {
    note.classList.add("fade");
  }, 2200);

  note.addEventListener("animationend", () => note.remove());

  confetti({
    particleCount: 40,
    spread: 70,
    origin: { y: 0.6 }
  });
}

</script>
  
    <script>
    
        // NAVIGATION LOGIC
        function nextPage(num) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('page' + num).classList.add('active');

  if (num === 7) celebrate();
  if (num === 9) newCompliment();
  if (num === 10) typeWorshipText();

  if (num === 14) {
    const img = document.querySelector('.meme-img');
    if (img) {
      img.style.opacity = 0;
      setTimeout(() => {
        img.classList.add('fade-in');
      }, 1000);
    }
  }

  handleAutoPages(num);
}


    // AUTO-SKIP LOGIC
function handleAutoPages(num) {
  clearTimeout(autoTimer);

  if (num === 11) autoTimer = setTimeout(() => nextPage(12), 3500);
  if (num === 12) autoTimer = setTimeout(() => nextPage(13), 3500);
  if (num === 13) autoTimer = setTimeout(() => nextPage("13b"), 3500);
  if (num === "13b") autoTimer = setTimeout(() => nextPage(14), 1500);
  if (num === 14) {
    // Auto-advance page 14 after image fade-in completes + approx same time as previous pages
    autoTimer = setTimeout(() => nextPage(4), 7000); // change 3500ms if you want it longer/shorter
  }
}

        // NO BUTTON LOGIC
        function moveNo() {
            const btn = document.getElementById('no-btn');
            btn.style.position = 'absolute';
            btn.style.top = Math.random() * 80 + '%';
            btn.style.left = Math.random() * 80 + '%';
        }

        function clickNo() {
            alert("Jinja, are you suure?");
            document.getElementById('no-btn').style.display = 'none';
        }

        // TIMER LOGIC (India Time: Jan 30, 2026 00:00:00)
        // India is UTC + 5:30. So we target Jan 29, 18:30:00 UTC.
        const targetDate = new Date("2026-01-29T18:30:00Z").getTime();

        function updateTimer() {
            const now = new Date().getTime();
            const diff = targetDate - now;

            if (diff > 0) {
                const d = Math.floor(diff / (1000 * 60 * 60 * 24));
                const h = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
                const m = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
                const s = Math.floor((diff % (1000 * 60)) / 1000);

                document.getElementById('days').innerText = d;
                document.getElementById('hours').innerText = h;
                document.getElementById('mins').innerText = m;
                document.getElementById('secs').innerText = s;
            } else {
     document.querySelector('.timer-container').innerHTML = "<h2>IT'S YOUR DAY!</h2>";

     const yesBtn = document.querySelector('#ready-gate .btn');
     if (yesBtn) {
     yesBtn.classList.add('glow');
      }
        }

        }
        updateTimer();
        setInterval(updateTimer, 1000);
      
  
function playVideoInView() {
  const container = document.getElementById('videoScroll');
  const videos = container.querySelectorAll('.scroll-video');

  videos.forEach(video => {
    const rect = video.getBoundingClientRect();
    const mid = window.innerHeight / 2;
    const inView = rect.top < mid && rect.bottom > mid;

    if (inView) {
      video.play().catch(() => {});
      video.muted = false;
      video.classList.add('in-view');
    } else {
      video.pause();
      video.muted = true;
      video.classList.remove('in-view');
    }
  });
}

const container = document.getElementById('videoScroll');
container.addEventListener('scroll', playVideoInView);
window.addEventListener('load', playVideoInView);


        // CONFETTI
        function celebrate() {
            const count = 200;
            const defaults = { origin: { y: 0.7 } };

            function fire(particleRatio, opts) {
                confetti(Object.assign({}, defaults, opts, {
                    particleCount: Math.floor(count * particleRatio)
                }));
            }

            fire(0.25, { spread: 26, startVelocity: 55 });
            fire(0.2, { spread: 60 });
            fire(0.35, { spread: 100, decay: 0.91, scalar: 0.8 });
            fire(0.1, { spread: 120, startVelocity: 25, decay: 0.92, scalar: 1.2 });
            fire(0.1, { spread: 120, startVelocity: 45 });
        }

</script>

</body>
</html>
