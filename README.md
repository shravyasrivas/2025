# meme genrator
how has my year been ig? im just making shit up atp
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Meme Generator — Single File</title>
  <!-- Tailwind via CDN for quick styling -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts for fun headline styles -->
  <link href="https://fonts.googleapis.com/css2?family=Anton&family=Bangers&family=Bebas+Neue&family=Oswald:wght@400;600&display=swap" rel="stylesheet">
  <style>
    :root { --card: #0b1220; --muted: #0f172a; --ink: #e5e7eb; }
    body { background: radial-gradient(1200px 600px at 80% -20%, #1f2937, #0b1220 55%); color: var(--ink); }
    .glass { background: rgba(255,255,255,0.06); backdrop-filter: blur(10px); }
    .dropzone { border: 2px dashed rgba(255,255,255,0.25); }
    label { color: #cbd5e1; }
    .font-Impact { font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif; }
    .font-Anton { font-family: 'Anton', sans-serif; }
    .font-Bangers { font-family: 'Bangers', system-ui, sans-serif; }
    .font-Bebas { font-family: 'Bebas Neue', sans-serif; }
    .font-Oswald { font-family: 'Oswald', sans-serif; }
  </style>
</head>
<body class="min-h-screen p-4 md:p-8">
  <div class="max-w-6xl mx-auto grid md:grid-cols-2 gap-6 items-start">
    <!-- Controls -->
    <section class="glass rounded-2xl shadow-xl p-5 md:p-7">
      <div class="flex items-center gap-3 mb-4">
        <svg xmlns="http://www.w3.org/2000/svg" class="w-8 h-8" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M4 5a2 2 0 0 1 2-2h9.5a2 2 0 0 1 1.6.8l2.5 3.3a2 2 0 0 1 .4 1.2V19a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V5Z"/><path d="M14 3v4a1 1 0 0 0 1 1h4"/></svg>
        <h1 class="text-2xl md:text-3xl font-semibold">Meme Generator</h1>
      </div>

      <!-- Upload / Drop -->
      <div id="drop" class="dropzone rounded-xl p-6 text-center cursor-pointer transition hover:bg-white/5">
        <input id="file" type="file" accept="image/*" class="hidden" />
        <p class="text-slate-300">Drop an image here or <span class="underline">browse</span></p>
        <p class="text-xs text-slate-400 mt-1">PNG, JPG, or GIF</p>
      </div>

      <!-- Text Controls -->
      <div class="grid grid-cols-1 gap-4 mt-6">
        <div>
          <label class="text-sm">Top Text</label>
          <input id="topText" class="mt-1 w-full px-3 py-2 rounded-lg bg-slate-800/60 focus:outline-none focus:ring ring-slate-500" placeholder="TOP TEXT" />
        </div>
        <div>
          <label class="text-sm">Bottom Text</label>
          <input id="bottomText" class="mt-1 w-full px-3 py-2 rounded-lg bg-slate-800/60 focus:outline-none focus:ring ring-slate-500" placeholder="BOTTOM TEXT" />
        </div>
        
        <div class="grid grid-cols-2 gap-4">
          <div>
            <label class="text-sm">Font</label>
            <select id="fontFamily" class="mt-1 w-full px-3 py-2 rounded-lg bg-slate-800/60">
              <option value="Impact" class="font-Impact">Impact (classic)</option>
              <option value="Anton" class="font-Anton">Anton</option>
              <option value="Bangers" class="font-Bangers">Bangers (comic)</option>
              <option value="Bebas" class="font-Bebas">Bebas Neue</option>
              <option value="Oswald" class="font-Oswald">Oswald</option>
            </select>
          </div>
          <div>
            <label class="text-sm">All Caps</label>
            <div class="mt-2">
              <input id="allCaps" type="checkbox" class="w-4 h-4 align-middle" checked>
              <span class="ml-2 text-sm text-slate-300">SHOUTING MODE</span>
            </div>
          </div>
        </div>

        <div class="grid grid-cols-2 gap-4">
          <div>
            <label class="text-sm">Font Size</label>
            <input id="fontSize" type="range" min="16" max="128" value="48" class="w-full" />
          </div>
          <div>
            <label class="text-sm">Line Width (stroke)</label>
            <input id="strokeWidth" type="range" min="0" max="10" value="4" class="w-full" />
          </div>
        </div>

        <div class="grid grid-cols-2 gap-4">
          <div>
            <label class="text-sm">Text Color</label>
            <input id="fillColor" type="color" value="#ffffff" class="mt-1 w-full h-10 rounded" />
          </div>
          <div>
            <label class="text-sm">Stroke Color</label>
            <input id="strokeColor" type="color" value="#000000" class="mt-1 w-full h-10 rounded" />
          </div>
        </div>

        <div class="grid grid-cols-2 gap-4">
          <div>
            <label class="text-sm">Top Offset</label>
            <input id="topOffset" type="range" min="0" max="200" value="30" class="w-full" />
          </div>
          <div>
            <label class="text-sm">Bottom Offset</label>
            <input id="bottomOffset" type="range" min="0" max="200" value="30" class="w-full" />
          </div>
        </div>

        <div class="grid grid-cols-2 gap-4 items-end">
          <div>
            <label class="text-sm">Canvas Width (px)</label>
            <input id="canvasWidth" type="number" min="256" max="2048" value="900" class="mt-1 w-full px-3 py-2 rounded-lg bg-slate-800/60" />
          </div>
          <button id="downloadBtn" class="w-full px-4 py-3 rounded-xl bg-indigo-500 hover:bg-indigo-600 transition disabled:opacity-50">Download PNG</button>
        </div>
      </div>

      <p class="text-xs text-slate-400 mt-4">Tip: You can drag & drop an image onto the canvas too.</p>
    </section>

    <!-- Canvas / Preview -->
    <section class="glass rounded-2xl shadow-xl p-4 md:p-6">
      <div class="relative">
        <canvas id="canvas" class="w-full rounded-xl shadow-lg bg-black/40"></canvas>
        <input id="hiddenFile" type="file" accept="image/*" class="hidden" />
      </div>
    </section>
  </div>

  <script>
    const state = {
      img: null,
      imgNatural: { w: 0, h: 0 },
    };

    const el = (id) => document.getElementById(id);
    const canvas = el('canvas');
    const ctx = canvas.getContext('2d');

    const controls = {
      file: el('file'),
      drop: el('drop'),
      topText: el('topText'),
      bottomText: el('bottomText'),
      fontFamily: el('fontFamily'),
      allCaps: el('allCaps'),
      fontSize: el('fontSize'),
      strokeWidth: el('strokeWidth'),
      fillColor: el('fillColor'),
      strokeColor: el('strokeColor'),
      topOffset: el('topOffset'),
      bottomOffset: el('bottomOffset'),
      canvasWidth: el('canvasWidth'),
      downloadBtn: el('downloadBtn'),
      hiddenFile: el('hiddenFile'),
    };

    function setCanvasSizeByWidth(width) {
      if (!state.img) return;
      const ratio = state.imgNatural.h / state.imgNatural.w;
      canvas.width = Math.max(256, Math.min(2048, width));
      canvas.height = Math.round(canvas.width * ratio);
    }

    function draw() {
      if (!state.img) {
        // Draw placeholder
        canvas.width = parseInt(controls.canvasWidth.value) || 900;
        canvas.height = Math.round(canvas.width * 9/16);
        const g = ctx.createLinearGradient(0,0,canvas.width,canvas.height);
        g.addColorStop(0,'#0f172a');
        g.addColorStop(1,'#020617');
        ctx.fillStyle = g;
        ctx.fillRect(0,0,canvas.width,canvas.height);
        ctx.fillStyle = 'rgba(255,255,255,0.6)';
        ctx.font = '24px Oswald, sans-serif';
        ctx.textAlign = 'center';
        ctx.fillText('Drop an image to start', canvas.width/2, canvas.height/2);
        return;
      }

      // Background image
      ctx.clearRect(0,0,canvas.width,canvas.height);
      ctx.drawImage(state.img, 0, 0, canvas.width, canvas.height);

      const fontName = controls.fontFamily.value;
      const fontSize = parseInt(controls.fontSize.value);
      const strokeW = parseInt(controls.strokeWidth.value);
      const fill = controls.fillColor.value;
      const stroke = controls.strokeColor.value;
      const cap = controls.allCaps.checked;

      ctx.lineJoin = 'round';
      ctx.textAlign = 'center';

      function drawCaption(text, y) {
        if (!text) return;
        const t = cap ? text.toUpperCase() : text;
        ctx.font = `${fontSize}px ${fontName}, Impact, sans-serif`;
        ctx.lineWidth = strokeW;
        ctx.strokeStyle = stroke;
        ctx.fillStyle = fill;

        // Wrap text to fit width
        const maxWidth = canvas.width * 0.92;
        const words = t.split(' ');
        const lines = [];
        let line = '';
        for (let i = 0; i < words.length; i++) {
          const test = line ? line + ' ' + words[i] : words[i];
          const metrics = ctx.measureText(test);
          if (metrics.width > maxWidth && i > 0) {
            lines.push(line);
            line = words[i];
          } else {
            line = test;
          }
        }
        lines.push(line);

        const lineHeight = fontSize * 1.15;
        const totalHeight = lines.length * lineHeight;
        let cy = y;
        if (y > canvas.height / 2) { // bottom block draws upward
          cy = y - totalHeight + lineHeight;
        }
        lines.forEach((ln, idx) => {
          const ly = y > canvas.height / 2 ? cy + idx * lineHeight : cy + idx * lineHeight;
          if (strokeW > 0) ctx.strokeText(ln, canvas.width/2, ly);
          ctx.fillText(ln, canvas.width/2, ly);
        });
      }

      const topY = (parseInt(controls.topOffset.value) || 30) + parseInt(controls.fontSize.value);
      const bottomY = canvas.height - (parseInt(controls.bottomOffset.value) || 30);

      drawCaption(controls.topText.value, topY);
      drawCaption(controls.bottomText.value, bottomY);
    }

    function handleFile(file) {
      if (!file) return;
      const reader = new FileReader();
      reader.onload = () => {
        const img = new Image();
        img.onload = () => {
          state.img = img;
          state.imgNatural = { w: img.naturalWidth, h: img.naturalHeight };
          setCanvasSizeByWidth(parseInt(controls.canvasWidth.value) || 900);
          draw();
        };
        img.src = reader.result;
      };
      reader.readAsDataURL(file);
    }

    // Initialize
    draw();

    // Event listeners
    controls.drop.addEventListener('click', () => controls.file.click());
    controls.drop.addEventListener('dragover', (e) => { e.preventDefault(); controls.drop.classList.add('bg-white/10'); });
    controls.drop.addEventListener('dragleave', () => controls.drop.classList.remove('bg-white/10'));
    controls.drop.addEventListener('drop', (e) => {
      e.preventDefault();
      controls.drop.classList.remove('bg-white/10');
      const file = e.dataTransfer.files?.[0];
      handleFile(file);
    });
    controls.file.addEventListener('change', (e) => handleFile(e.target.files?.[0]));

    // Also allow dropping directly on canvas
    canvas.addEventListener('dragover', (e) => { e.preventDefault(); });
    canvas.addEventListener('drop', (e) => {
      e.preventDefault();
      const file = e.dataTransfer.files?.[0];
      handleFile(file);
    });

    // Redraw on control changes
    ['topText','bottomText','fontFamily','allCaps','fontSize','strokeWidth','fillColor','strokeColor','topOffset','bottomOffset']
      .forEach(id => controls[id].addEventListener('input', draw));

    controls.canvasWidth.addEventListener('input', () => {
      setCanvasSizeByWidth(parseInt(controls.canvasWidth.value) || 900);
      draw();
    });

    controls.downloadBtn.addEventListener('click', () => {
      if (!canvas.width || !canvas.height) return;
      const a = document.create
