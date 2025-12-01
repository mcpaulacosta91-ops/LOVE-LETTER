# LOVE-LETTER
LOVE LETTER <!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Secret Confession 💌</title>
<style>
  :root{
    --bg:#0f1724;
    --card:#0b1220;
    --accent:#ff6b81;
    --muted:#9aa4b2;
    --glass: rgba(255,255,255,0.04);
  }
  *{box-sizing:border-box}
  body{
    margin:0;
    font-family:Inter,ui-sans-serif,system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",Arial;
    background: radial-gradient(1200px 600px at 10% 10%, rgba(255,107,129,0.08), transparent),
                radial-gradient(1000px 500px at 90% 90%, rgba(59,130,246,0.03), transparent),
                var(--bg);
    color:#e6eef6;
    min-height:100vh;
    display:flex;
    align-items:center;
    justify-content:center;
    padding:24px;
  }

  .container{
    width:100%;
    max-width:920px;
    display:grid;
    grid-template-columns: 1fr 420px;
    gap:28px;
    align-items:center;
  }

  .hero{
    background: linear-gradient(180deg, rgba(255,255,255,0.02), transparent);
    padding:28px;
    border-radius:14px;
    box-shadow: 0 6px 30px rgba(2,6,23,0.6);
    border:1px solid rgba(255,255,255,0.03);
    min-height:320px;
  }

  h1{margin:0 0 8px 0;font-size:24px}
  p.lead{color:var(--muted);margin:0 0 16px 0}

  .card{
    background:linear-gradient(180deg, rgba(255,255,255,0.02), transparent);
    border-radius:12px;
    padding:18px;
    border:1px solid rgba(255,255,255,0.035);
  }

  .preview{
    background: linear-gradient(135deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
    padding:18px;
    border-radius:10px;
    min-height:140px;
  }

  .from{
    font-weight:600;
    color:var(--accent);
    margin-bottom:8px;
  }

  .message{
    font-size:18px;
    line-height:1.45;
    color:#e8f0ff;
    white-space:pre-wrap;
  }

  .controls{margin-top:14px; display:flex; gap:10px; flex-wrap:wrap}
  .btn{
    background:var(--accent);
    border: none;
    color:white;
    padding:10px 14px;
    border-radius:10px;
    cursor:pointer;
    font-weight:600;
    box-shadow: 0 6px 18px rgba(255,107,129,0.14);
  }
  .btn.ghost{
    background:transparent;
    border:1px solid rgba(255,255,255,0.06);
    color:var(--muted);
    box-shadow:none;
    font-weight:600;
  }
  .sidebar{
    display:flex;
    flex-direction:column;
    gap:18px;
  }
  .open-btn{
    padding:18px;
    border-radius:12px;
    text-align:center;
    cursor:pointer;
    user-select:none;
    background:linear-gradient(90deg, rgba(255,255,255,0.02), transparent);
    border:1px solid rgba(255,255,255,0.03);
  }
  .small{font-size:13px;color:var(--muted)}
  .note{font-size:13px;color:var(--muted);}

  /* modal */
  .modal-bg{
    position:fixed;
    inset:0;
    background:rgba(2,6,23,0.6);
    display:none;
    align-items:center;
    justify-content:center;
    z-index:50;
  }
  .modal{
    width:92%;
    max-width:560px;
    background:linear-gradient(180deg, rgba(255,255,255,0.02), transparent);
    padding:22px;
    border-radius:12px;
    border:1px solid rgba(255,255,255,0.04);
    box-shadow: 0 18px 80px rgba(2,6,23,0.7);
  }
  textarea{
    width:100%;height:160px;border-radius:10px;padding:12px;border:1px solid rgba(255,255,255,0.03);
    background:var(--glass); color: #e6eef6; resize:vertical;
  }

  /* responsivity */
  @media (max-width:940px){
    .container{grid-template-columns: 1fr; max-width:760px}
    .sidebar{order:-1}
  }

  /* success */
  .result{
    text-align:center;
    padding:18px;
    border-radius:12px;
    background:linear-gradient(180deg, rgba(255,255,255,0.015), transparent);
    border:1px solid rgba(255,255,255,0.03);
  }

  /* hidden */
  .hidden{display:none}
  /* confetti container */
  #confetti{
    pointer-events:none;
    position:fixed;
    left:0; top:0; width:100%; height:100%; z-index:40;
  }
</style>
</head>
<body>

<div id="confetti"></div>

<div class="container" role="main">
  <div class="hero card">
    <h1>Secret Confession</h1>
    <p class="lead">Make it personal, make it kind. When you're ready, have your crush open this page — they’ll get a private message from <strong id="senderPreview">Mc Paul</strong> 💌</p>

    <div class="preview" id="preview">
      <div class="from">From: <span id="fromName">Mc Paul</span></div>
      <div class="message" id="messagePreview">Hi — I've been wanting to tell you something for a while. I really enjoy spending time with you and I think you're amazing. Would you like to hang out sometime?</div>
    </div>

    <div class="controls">
      <button class="btn" id="openModal">Customize & Open</button>
      <button class="btn ghost" id="copyText">Copy Confession</button>
      <button class="btn ghost" id="downloadPNG">Download as Image</button>
      <button class="btn ghost" id="resetBtn">Reset</button>
    </div>

    <div style="margin-top:14px" class="note">
      Tip: change the message to be honest and respectful. Keep it short if you're nervous — sincerity wins.
    </div>
  </div>

  <div class="sidebar">
    <div class="card open-btn" id="openForCrush">
      <div style="font-weight:700;font-size:18px">Open Confession</div>
      <div class="small">Give this link to your crush. When they open it, they see your message and can respond.</div>
    </div>

    <div class="card result hidden" id="responseBox">
      <div id="responseTitle" style="font-weight:700">Waiting for a response...</div>
      <div id="responseText" class="small">Once they respond, the result will be shown here.</div>
    </div>

    <div class="card" style="padding:14px">
      <div style="font-weight:700">How to use</div>
      <ol style="padding-left:18px;margin:8px 0 0 0;color:var(--muted);font-size:14px">
        <li>Customize the message using "Customize & Open".</li>
        <li>Send the file or link to your crush.</li>
        <li>They can respond with Accept or Not ready — you'll see the result locally in their browser.</li>
      </ol>
    </div>
  </div>
</div>

<!-- modal for editing / "open for crush" view -->
<div class="modal-bg" id="modalBg" aria-hidden="true">
  <div class="modal" role="dialog" aria-modal="true" aria-labelledby="modalTitle">
    <h2 id="modalTitle" style="margin-top:0">Customize your confession</h2>
    <label class="small">Your name</label>
    <input id="fromInput" style="width:100%;padding:10px;border-radius:8px;margin:6px 0 12px 0;border:1px solid rgba(255,255,255,0.03);background:var(--glass);color:#e6eef6" value="Mc Paul" />
    <label class="small">Message</label>
    <textarea id="messageInput">Hi — I've been wanting to tell you something for a while. I really enjoy spending time with you and I think you're amazing. Would you like to hang out sometime?</textarea>

    <div style="display:flex;gap:8px; margin-top:12px; justify-content:flex-end">
      <button class="btn ghost" id="closeModal">Cancel</button>
      <button class="btn" id="saveOpen">Save & Open for crush</button>
    </div>
  </div>
</div>

<!-- hidden content for the crush view -->
<div class="modal-bg" id="openBg" aria-hidden="true">
  <div class="modal" role="dialog" aria-modal="true" style="max-width:520px">
    <h2 style="margin:0 0 6px 0">A message for you 💌</h2>
    <div class="small" style="margin-bottom:10px">From <strong id="openFrom">Mc Paul</strong></div>
    <div style="background:var(--glass);padding:14px;border-radius:10px;border:1px solid rgba(255,255,255,0.03);min-height:120px">
      <div id="openMessage" style="white-space:pre-wrap;color:#eaf1ff"></div>
    </div>

    <div style="display:flex;gap:8px;margin-top:14px">
      <button class="btn" id="acceptBtn">Accept 💖</button>
      <button class="btn ghost" id="notReadyBtn">Not ready</button>
    </div>

    <div style="margin-top:12px" class="small">Their choice will only show on this device — it doesn't send notifications. Be kind in your response.</div>
  </div>
</div>

<script>
  // Elements
  const modalBg = document.getElementById('modalBg');
  const openBg = document.getElementById('openBg');
  const openModal = document.getElementById('openModal');
  const closeModal = document.getElementById('closeModal');
  const saveOpen = document.getElementById('saveOpen');
  const fromInput = document.getElementById('fromInput');
  const messageInput = document.getElementById('messageInput');
  const fromName = document.getElementById('fromName');
  const messagePreview = document.getElementById('messagePreview');
  const senderPreview = document.getElementById('senderPreview');
  const openForCrush = document.getElementById('openForCrush');
  const openFrom = document.getElementById('openFrom');
  const openMessage = document.getElementById('openMessage');
  const acceptBtn = document.getElementById('acceptBtn');
  const notReadyBtn = document.getElementById('notReadyBtn');
  const responseBox = document.getElementById('responseBox');
  const responseTitle = document.getElementById('responseTitle');
  const responseText = document.getElementById('responseText');
  const copyText = document.getElementById('copyText');
  const downloadPNG = document.getElementById('downloadPNG');
  const resetBtn = document.getElementById('resetBtn');
  const confettiRoot = document.getElementById('confetti');

  // initial values (can be saved in localStorage if you want)
  function updatePreview(){
    fromName.textContent = fromInput.value || 'Me';
    senderPreview.textContent = fromInput.value || 'Me';
    messagePreview.textContent = messageInput.value || '';
  }

  // show/hide helpers
  function showModal(){
    modalBg.style.display='flex';
    modalBg.setAttribute('aria-hidden','false');
  }
  function hideModal(){
    modalBg.style.display='none';
    modalBg.setAttribute('aria-hidden','true');
  }
  function showOpen(){
    openBg.style.display='flex';
    openBg.setAttribute('aria-hidden','false');
  }
  function hideOpen(){
    openBg.style.display='none';
    openBg.setAttribute('aria-hidden','true');
  }

  openModal.addEventListener('click', ()=> showModal());
  closeModal.addEventListener('click', ()=> hideModal());
  saveOpen.addEventListener('click', ()=>{
    updatePreview();
    hideModal();
    // Also prepare the "open for crush" view using the saved text
    openFrom.textContent = fromInput.value || 'Me';
    openMessage.textContent = messageInput.value || '';
  });

  // open for crush (simulates "they opened your link")
  openForCrush.addEventListener('click', ()=> {
    // ensure preview saved
    openFrom.textContent = fromInput.value || 'Me';
    openMessage.textContent = messageInput.value || '';
    showOpen();
  });

  // accept / not ready logic (local only)
  acceptBtn.addEventListener('click', ()=> {
    hideOpen();
    runConfetti();
    responseBox.classList.remove('hidden');
    responseTitle.textContent = 'They said yes! 🎉';
    responseText.textContent = fromInput.value + ' — your crush accepted. Congratulations!';
  });

  notReadyBtn.addEventListener('click', ()=> {
    hideOpen();
    responseBox.classList.remove('hidden');
    responseTitle.textContent = 'They said not ready.';
    responseText.textContent = 'It’s okay — be respectful and give them space. You can try again later.';
  });

  // copy confession text
  copyText.addEventListener('click', async ()=>{
    const txt = `${fromInput.value || 'Me'}: ${messageInput.value || ''}`;
    try {
      await navigator.clipboard.writeText(txt);
      copyText.textContent = 'Copied ✓';
      setTimeout(()=> copyText.textContent = 'Copy Confession', 1500);
    } catch(e){
      alert('Copy failed. You can select the text and press Ctrl/Cmd+C.');
    }
  });

  // download PNG of confession (simple canvas renderer)
  downloadPNG.addEventListener('click', ()=>{
    const w = 900, h = 520;
    const canvas = document.createElement('canvas');
    canvas.width = w; canvas.height = h;
    const ctx = canvas.getContext('2d');

    // background
    const g = ctx.createLinearGradient(0,0,w,h);
    g.addColorStop(0,'#0f1724'); g.addColorStop(1,'#081026');
    ctx.fillStyle=g; ctx.fillRect(0,0,w,h);

    // sender
    ctx.fillStyle='#ff6b81';
    ctx.font = 'bold 36px Inter, Arial';
    ctx.fillText(fromInput.value || 'Me', 40, 80);

    // box
    ctx.fillStyle='rgba(255,255,255,0.03)';
    roundRect(ctx, 30, 110, w-60, 320, 14, true, false);

    // message
    ctx.fillStyle='#eaf1ff';
    ctx.font = '20px Inter, Arial';
    wrapText(ctx, messageInput.value || '', 56, 150, w-120, 28);

    // footer
    ctx.fillStyle='#9aa4b2'; ctx.font='14px Inter, Arial';
    ctx.fillText('- sent with a little courage', 40, h-28);

    const link = document.createElement('a');
    link.download = 'confession.png';
    link.href = canvas.toDataURL('image/png');
    link.click();
  });

  // helpers for canvas
  function roundRect(ctx, x, y, width, height, radius, fill, stroke) {
    if (typeof radius === 'number') {
      radius = {tl: radius, tr: radius, br: radius, bl: radius};
    }
    ctx.beginPath();
    ctx.moveTo(x + radius.tl, y);
    ctx.lineTo(x + width - radius.tr, y);
    ctx.quadraticCurveTo(x + width, y, x + width, y + radius.tr);
    ctx.lineTo(x + width, y + height - radius.br);
    ctx.quadraticCurveTo(x + width, y + height, x + width - radius.br, y + height);
    ctx.lineTo(x + radius.bl, y + height);
    ctx.quadraticCurveTo(x, y + height, x, y + height - radius.bl);
    ctx.lineTo(x, y + radius.tl);
    ctx.quadraticCurveTo(x, y, x + radius.tl, y);
    ctx.closePath();
    if (fill) ctx.fill();
    if (stroke) ctx.stroke();
  }
  function wrapText(ctx, text, x, y, maxWidth, lineHeight) {
    const words = text.split(' ');
    let line = '';
    for (let n = 0; n < words.length; n++) {
      const testLine = line + words[n] + ' ';
      const metrics = ctx.measureText(testLine);
      const testWidth = metrics.width;
      if (testWidth > maxWidth && n > 0) {
        ctx.fillText(line, x, y);
        line = words[n] + ' ';
        y += lineHeight;
      } else {
        line = testLine;
      }
    }
    ctx.fillText(line, x, y);
  }

  // reset to default
  resetBtn.addEventListener('click', ()=>{
    fromInput.value = 'Mc Paul';
    messageInput.value = "Hi — I've been wanting to tell you something for a while. I really enjoy spending time with you and I think you're amazing. Would you like to hang out sometime?";
    updatePreview();
    responseBox.classList.add('hidden');
  });

  // simple confetti (no library)
  function runConfetti(){
    const colours = ['#ff6b81','#ffd166','#4ade80','#60a5fa','#c084fc'];
    const count = 60;
    for(let i=0;i<count;i++){
      const el = document.createElement('div');
      el.className = 'confetti-piece';
      const size = 8 + Math.random()*12;
      el.style.position = 'absolute';
      el.style.left = (Math.random()*100) + '%';
      el.style.top = '-10%';
      el.style.width = `${size}px`;
      el.style.height = `${size*0.6}px`;
      el.style.background = colours[Math.floor(Math.random()*colours.length)];
      el.style.opacity = Math.random()*0.9 + 0.3;
      el.style.transform = `rotate(${Math.random()*360}deg)`;
      el.style.borderRadius = '2px';
      el.style.zIndex = 50;
      confettiRoot.appendChild(el);
      // animate
      const duration = 1800 + Math.random()*1600;
      el.animate([
        { transform: `translateY(0) rotate(0deg)`, opacity:1 },
        { transform: `translateY(${window.innerHeight + 200}px) rotate(${Math.random()*720}deg)`, opacity:0.8 }
      ], { duration, easing: 'cubic-bezier(.2,.9,.3,1)'});
      // remove after
      setTimeout(()=> el.remove(), duration+200);
    }
  }

  // initial update
  updatePreview();

  // accessibility: close modal on background click
  modalBg.addEventListener('click', (e)=>{
    if(e.target===modalBg) hideModal();
  });
  openBg.addEventListener('click', (e)=>{
    if(e.target===openBg) hideOpen();
  });

  // close with Escape
  document.addEventListener('keydown', (e)=>{
    if(e.key==='Escape'){
      hideModal(); hideOpen();
    }
  });

</script>
</body>
</html>
