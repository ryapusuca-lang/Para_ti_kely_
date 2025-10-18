<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Para ti, mi mejor amiga Kely 💖</title>
  <style>
    :root{--bg:#0f1724;--accent:#ff6b9a;--muted:#9aa6b2}
    *{box-sizing:border-box;font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial}
    body{
      margin:0;
      min-height:100vh;
      display:flex;
      align-items:center;
      justify-content:center;
      background:linear-gradient(180deg,#071028 0%, #081226 60%);
      color:#e6eef6;
      overflow:hidden;
    }
    .wrap{
      width:min(800px,94vw);
      background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent);
      border-radius:16px;
      padding:24px;
      box-shadow:0 8px 30px rgba(2,6,23,0.7);
      position:relative;
      overflow:hidden;
      text-align:center;
    }
    h1{
      font-size:26px;
      margin-bottom:8px;
      color:#ff8fb5;
      text-shadow:0 0 8px rgba(255,107,154,0.4);
    }
    p.lead{color:var(--muted);margin-bottom:20px}
    .heart-btn{
      width:140px;
      height:140px;
      margin:0 auto;
      cursor:pointer;
      display:flex;
      align-items:center;
      justify-content:center;
      transition:transform .2s ease;
    }
    .heart-btn:hover{transform:scale(1.1)}
    svg{filter:drop-shadow(0 8px 18px rgba(255,107,154,0.3))}
    
    /* 💖 Ajuste para que las frases salgan en dos líneas y se vean completas */
    .phrase{
      font-size:20px;
      position:absolute;
      left:50%;
      transform:translateX(-50%);
      max-width:85vw;       /* límite para que no se salga del celular */
      white-space:normal;   /* permite que el texto se parta en varias líneas */
      text-align:center;    /* centra las líneas */
      line-height:1.4;
      opacity:0;
      transition:opacity 1s ease, transform 1s ease;
    }

    footer{margin-top:28px;font-size:13px;color:var(--muted)}
    canvas#confetti{
      position:absolute;
      left:0;
      top:0;
      width:100%;
      height:100%;
      pointer-events:none;
    }
  </style>
</head>
<body>
  <div class="wrap">
    <h1>💖 Para ti, mi mejor amiga Kely 💖</h1>
    <p class="lead">Toca el corazón para ver lo mucho que te quiero ✨</p>

    <div class="heart-btn" id="heartBtn">
      <svg viewBox="0 0 32 29" width="120" height="120">
        <defs>
          <linearGradient id="g" x1="0" x2="1">
            <stop offset="0%" stop-color="#ff95b0" />
            <stop offset="100%" stop-color="#ff4b87" />
          </linearGradient>
        </defs>
        <path d="M23.6 2.6c-2.6 0-4.8 1.5-5.6 3.6-.8-2.1-3-3.6-5.6-3.6C6.2 2.6 3 6.2 3 10.3 3 18.2 15.7 25 16 25c.3 0 13-6.8 13-14.7 0-4.1-3.2-7.7-5.4-7.7z" fill="url(#g)"/>
      </svg>
    </div>

    <footer>Hecho con cariño departe de Andree (especial) xd </footer>
    <canvas id="confetti"></canvas>
  </div>

  <script>
    const phrases = [
      'Eres una amiga increíble pero pendeja jaja no no es broma',
      'Tu sonrisa alegra mis días, siempre cuando estoy contigo me alegro mucho',
      'Eres la mejor nadadora para mi y para muchos, sé que darás todo de ti el 30,31,1,2',
      'Me inspiras a ser mejor cada día, me alegro que estés a mi lado',
      'Tu amistad vale más que mil tesoros, nunca te dejaría, vales más que la antimateria jaja xd',
      'Siempre estás cuando más te necesito, aunque me pongo medio raro la verdad xd',
      'Gracias por soportarme, eres única',
      'Eres mi persona favorita, ojalá nunca te vayas de mi lado :(',
      'No hay día que no me alegres 🌷',
      'Eres una persona llena de luz y de sombra más jaja no xd',
      'Tu forma de ser es muy linda para mí xd',
      'Eres la mejor amiga que alguien pudo tener jsjjs',
      'Brillas más que todas las estrellas, ya te dije que en tus ojos se refleja un universo :3',
      'Nunca cambies, Kely 💗',
      'Eres tan dedicada, incluso nadando, por eso eres la mejor',
      'Tengo hambre xd',
      'Eres la definición de única, aunque no seas perfecta para mí lo eres con tus defectos jajsjs',
      'Me hace feliz compartir momentos contigo, siempre disponible para ti wazaaa xd',
      'Oe cuidado cuando sales ojito',
      'Tu talento para nadar es tan hermoso como tu corazón, eso no lo niego'
    ];

    const heartBtn = document.getElementById('heartBtn');
    const confettiCanvas = document.getElementById('confetti');
    const ctx = confettiCanvas.getContext('2d');
    let cw, ch;

    function resize(){
      cw = confettiCanvas.width = confettiCanvas.clientWidth;
      ch = confettiCanvas.height = confettiCanvas.clientHeight;
    }
    window.addEventListener('resize', resize);
    resize();

    function rand(min,max){return Math.random()*(max-min)+min;}
    let parts = [];

    function spawnConfetti(x,y,count=40){
      for(let i=0;i<count;i++){
        parts.push({
          x:x, y:y,
          vx:rand(-5,5),
          vy:rand(-10,-3),
          r:rand(5,10),
          t:rand(0,Math.PI*2),
          c:`hsl(${Math.floor(rand(330,360))},90%,${Math.floor(rand(55,65))}%)`
        });
      }
    }

    function draw(){
      ctx.clearRect(0,0,cw,ch);
      for(let i=parts.length-1;i>=0;i--){
        const p=parts[i];
        p.vy+=0.3; p.x+=p.vx; p.y+=p.vy; p.t+=0.1;
        ctx.save();
        ctx.translate(p.x,p.y);
        ctx.rotate(Math.sin(p.t));
        ctx.fillStyle=p.c;
        ctx.fillRect(-p.r/2,-p.r/2,p.r,p.r*0.6);
        ctx.restore();
        if(p.y>ch+50) parts.splice(i,1);
      }
      requestAnimationFrame(draw);
    }
    draw();

    let index = 0;
    function showPhrase(){
      const phrase = document.createElement('div');
      phrase.className = 'phrase';
      phrase.textContent = phrases[index];
      document.body.appendChild(phrase);

      const y = window.innerHeight/2 + rand(-100,100);
      phrase.style.top = y + 'px';
      phrase.style.opacity = 0;
      phrase.style.transform = 'translate(-50%,20px)';

      setTimeout(()=>{
        phrase.style.opacity = 1;
        phrase.style.transform = 'translate(-50%,0)';
      },50);

      setTimeout(()=>{
        phrase.style.opacity = 0;
        phrase.style.transform = 'translate(-50%,-20px)';
        setTimeout(()=>phrase.remove(),2000);
      },3500);

      index = (index + 1) % phrases.length;
    }

    heartBtn.addEventListener('click', ()=>{
      heartBtn.animate([{transform:'scale(1)'},{transform:'scale(1.4)'},{transform:'scale(1)'}],{duration:500});
      const rect = heartBtn.getBoundingClientRect();
      const x = rect.left + rect.width/2 - confettiCanvas.getBoundingClientRect().left;
      const y = rect.top + rect.height/2 - confettiCanvas.getBoundingClientRect().top;
      spawnConfetti(x,y,70);
      showPhrase();
    });
  </script>
</body>
</html>
