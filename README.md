<!DOCTYPE html>
<html lang="vi">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <title>Tìm Duyên Số Chiến Dê</title>
    <style>
      :root {
        --bg: #0f1724;
        --card: #0b1220;
        --accent: #ff6584;
        --muted: rgba(255, 255, 255, 0.75);
        --glass: rgba(255, 255, 255, 0.04);
        --glass-2: rgba(255, 255, 255, 0.02);
        --neon: drop-shadow(0 6px 30px rgba(255, 101, 132, 0.14));
        font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI",
          Roboto, "Helvetica Neue", Arial;
      }
      * {
        box-sizing: border-box;
        scroll-behavior: smooth;
      }
      html,
      body {
        height: 100%;
        margin: 0;
        background: radial-gradient(
            1200px 700px at 10% 10%,
            rgba(255, 101, 132, 0.06),
            transparent 8%
          ),
          radial-gradient(
            900px 500px at 90% 90%,
            rgba(78, 144, 255, 0.04),
            transparent 8%
          ),
          linear-gradient(120deg, #0f1724 0%, #071025 60%);
        color: var(--muted);
        overflow-x: hidden;
      }

      /* subtle animated gradient background */
      @keyframes bgShift {
        0% {
          background-position: 0% 50%;
        }
        50% {
          background-position: 100% 50%;
        }
        100% {
          background-position: 0% 50%;
        }
      }
      body {
        background-size: 400% 400%;
        animation: bgShift 12s ease infinite;
      }

      body {
        display: flex;
        justify-content: center;
        align-items: flex-start;
        padding: 40px 20px 80px;
        min-height: 100vh;
      }

      .card {
        width: min(980px, 96%);
        background: linear-gradient(
          180deg,
          rgba(11, 18, 32, 0.9),
          rgba(255, 255, 255, 0.02)
        );
        border-radius: 18px;
        padding: 28px;
        box-shadow: 0 10px 60px rgba(2, 6, 23, 0.6);
        position: relative;
        overflow: visible;
      }

      header {
        display: flex;
        align-items: center;
        gap: 16px;
        margin-bottom: 18px;
      }
      .logo {
        width: 56px;
        height: 56px;
        border-radius: 12px;
        background: linear-gradient(135deg, var(--accent), #5fb6ff);
        display: grid;
        place-items: center;
        font-weight: 700;
        color: white;
        font-size: 20px;
        letter-spacing: 0.6px;
        box-shadow: 0 6px 30px rgba(0, 0, 0, 0.5);
      }
      h1 {
        font-size: 20px;
        margin: 0;
        color: #fff;
      }
      p.desc {
        margin: 0;
        color: rgba(255, 255, 255, 0.6);
        font-size: 13px;
      }

      .stage {
        display: grid;
        grid-template-columns: 1fr 360px 1fr;
        gap: 20px;
        align-items: center;
      }

      .panel {
        background: linear-gradient(180deg, var(--glass), var(--glass-2));
        border-radius: 14px;
        padding: 18px;
        min-height: 200px;
        display: flex;
        flex-direction: column;
        gap: 12px;
        align-items: center;
        justify-content: center;
        backdrop-filter: blur(6px);
        transition: transform 0.25s ease, box-shadow 0.25s ease;
      }
      .panel:hover {
        transform: translateY(-6px);
        box-shadow: 0 20px 50px rgba(2, 6, 23, 0.5);
      }

      label {
        font-size: 12px;
        color: rgba(255, 255, 255, 0.65);
        align-self: flex-start;
      }
      input.name {
        width: 100%;
        padding: 12px 14px;
        border-radius: 10px;
        border: 1px solid rgba(255, 255, 255, 0.05);
        background: transparent;
        color: white;
        font-size: 16px;
        outline: none;
        transition: box-shadow 0.18s, transform 0.12s;
      }
      input.name:focus {
        box-shadow: 0 6px 18px rgba(95, 182, 255, 0.06);
        transform: translateY(-2px);
      }

      .center {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 12px;
      }
      .resultBubble {
        width: 220px;
        height: 220px;
        border-radius: 50%;
        display: grid;
        place-items: center;
        background: linear-gradient(
          180deg,
          rgba(255, 255, 255, 0.02),
          rgba(255, 255, 255, 0.01)
        );
        border: 1px solid rgba(255, 255, 255, 0.04);
        font-size: 18px;
        color: var(--muted);
        text-align: center;
        padding: 18px;
        position: relative;
        transition: transform 0.18s ease, box-shadow 0.25s ease;
        will-change: transform, box-shadow;
      }
      .resultBubble.pop {
        transform: scale(1.08);
        box-shadow: 0 20px 60px rgba(255, 101, 132, 0.12);
      }
      .resultBubble.compress {
        transform: scale(0.65);
        transition: transform 0.22s cubic-bezier(0.2, 0.9, 0.2, 1);
      }
      .resultBubble.explode {
        transform: scale(1.18);
        box-shadow: 0 30px 90px rgba(255, 101, 132, 0.18);
      }
      .choice {
        font-size: 22px;
        font-weight: 700;
        color: #fff;
        margin-top: 8px;
      }
      .sub {
        font-size: 13px;
        color: rgba(255, 255, 255, 0.6);
      }

      .btn {
        padding: 12px 18px;
        border-radius: 12px;
        border: none;
        cursor: pointer;
        font-weight: 600;
        background: linear-gradient(90deg, var(--accent), #5fb6ff);
        color: white;
        box-shadow: var(--neon);
        transition: transform 0.12s ease, filter 0.12s;
      }
      .btn:hover {
        transform: translateY(-4px) scale(1.02);
        filter: brightness(1.03);
      }

      .actions {
        display: flex;
        gap: 10px;
      }

      .hint {
        font-size: 12px;
        color: rgba(255, 255, 255, 0.45);
      }

      .effects {
        position: fixed;
        inset: 0;
        pointer-events: none;
        overflow: visible;
      }
      .particle {
        position: absolute;
        transform: translate(-50%, -50%) scale(0.95);
        animation-timing-function: cubic-bezier(0.2, 0.8, 0.2, 1);
        pointer-events: none;
        will-change: transform, opacity;
      }

      .heartIcon {
        font-size: 18px;
        color: var(--accent);
        text-shadow: 0 2px 6px rgba(255, 101, 132, 0.25);
      }
      .sadIcon {
        font-size: 18px;
        color: #9fb0c6;
        text-shadow: 0 1px 4px rgba(0, 0, 0, 0.2);
      }
      .bubbleIcon {
        font-size: 18px;
        color: #8fe1ff;
        text-shadow: 0 1px 6px rgba(143, 225, 255, 0.12);
      }

      @keyframes flyUpSmall {
        0% {
          opacity: 1;
          transform: translate(-50%, -50%) scale(0.9) translateY(0) rotate(0);
        }
        100% {
          opacity: 0;
          transform: translate(-50%, -50%) translateY(-260px) scale(1.15)
            rotate(200deg);
        }
      }

      /* big burst visual in center */
      .bigBurst {
        position: fixed;
        inset: 0;
        display: grid;
        place-items: center;
        pointer-events: none;
        mix-blend-mode: screen;
      }
      .bigBurst .core {
        width: 140px;
        height: 140px;
        border-radius: 50%;
        background: radial-gradient(
          circle at 30% 30%,
          rgba(255, 101, 132, 0.95),
          rgba(255, 101, 132, 0.65) 40%,
          rgba(255, 101, 132, 0.18) 55%
        );
        filter: blur(8px);
        opacity: 0;
        transform: scale(0.4);
        animation: burstBig 900ms ease-out forwards;
      }
      @keyframes burstBig {
        0% {
          opacity: 0;
          transform: scale(0.3);
        }
        45% {
          opacity: 0.95;
          transform: scale(1.15);
        }
        100% {
          opacity: 0;
          transform: scale(2.4);
        }
      }

      /* bounce animation for final label */
      @keyframes finalBounce {
        0% {
          transform: translateY(0);
        }
        30% {
          transform: translateY(-18px);
        }
        55% {
          transform: translateY(6px);
        }
        80% {
          transform: translateY(-6px);
        }
        100% {
          transform: translateY(0);
        }
      }

      /* responsive */
      @media (max-width: 900px) {
        .stage {
          grid-template-columns: 1fr;
        }
        .card {
          padding: 18px;
        }
        .resultBubble {
          width: 180px;
          height: 180px;
        }
      }

      .namePreview {
        font-size: 14px;
        color: rgba(255, 255, 255, 0.85);
        font-weight: 600;
      }
    </style>
  </head>
  <body>
    <div class="card" aria-live="polite">
      <header>
        <div class="logo">♡</div>
        <div>
          <h1>Duyên Số</h1>
          <p class="desc">Nhập tên 2 người ở hai bên.</p>
        </div>
      </header>

      <main class="stage">
        <section class="panel left">
          <label for="leftName">Tên A</label>
          <input
            id="leftName"
            class="name"
            placeholder="Ví dụ: Chiến"
            value=""
          />
          <div class="hint">Bạn có thể để tên thật hoặc nickname</div>
          <div style="height: 6px"></div>
          <div class="namePreview" id="previewA">—</div>
        </section>

        <section class="center">
          <div
            class="resultBubble"
            id="bubble"
            role="status"
            aria-atomic="true"
          >
            <div style="text-align: center">
              <div class="sub">Kết quả</div>
              <div class="choice" id="choiceLabel">Chưa có</div>
              <div class="sub" id="namesCombined">— &mdash;</div>
            </div>
          </div>

          <div class="actions" style="margin-top: 12px">
            <button class="btn" id="revealBtn">Xem duyên</button>
            <button
              class="btn"
              id="shuffleBtn"
              style="
                background: transparent;
                border: 1px solid rgba(255, 255, 255, 0.06);
                box-shadow: none;
                color: var(--muted);
              "
            >
              Làm mới
            </button>
          </div>
          <div style="height: 8px"></div>
          <div class="hint">
            Các lựa chọn: <strong>người yêu</strong>, <strong>bạn thân</strong>,
            <strong>bạn thường</strong>
          </div>
        </section>

        <section class="panel right">
          <label for="rightName">Tên B</label>
          <input id="rightName" class="name" placeholder="Ví dụ: Hà" value="" />
          <div class="hint">Nhập 2 tên khác nhau</div>
          <div style="height: 6px"></div>
          <div class="namePreview" id="previewB">—</div>
        </section>
      </main>

      <div class="effects" id="effects" aria-hidden="true"></div>
      <div id="bigBurstArea" aria-hidden="true"></div>
    </div>

    <script>
      // --- DOM references (keep your original variable names) ---
      const leftInput = document.getElementById("leftName");
      const rightInput = document.getElementById("rightName");
      const previewA = document.getElementById("previewA");
      const previewB = document.getElementById("previewB");
      const revealBtn = document.getElementById("revealBtn");
      const shuffleBtn = document.getElementById("shuffleBtn");
      const choiceLabel = document.getElementById("choiceLabel");
      const namesCombined = document.getElementById("namesCombined");
      const bubble = document.getElementById("bubble");
      const effects = document.getElementById("effects");
      const bigBurstArea = document.getElementById("bigBurstArea");

      const choices = ["người yêu", "bạn thân", "bạn thường"];

      function updatePreviews() {
        previewA.textContent = leftInput.value.trim() || "—";
        previewB.textContent = rightInput.value.trim() || "—";
        namesCombined.textContent = `${previewA.textContent} ❤ ${previewB.textContent}`;
      }

      leftInput.addEventListener("input", updatePreviews);
      rightInput.addEventListener("input", updatePreviews);

      // --- WebAudio simple synthesizer for pop / boom / romantic ---
      const AudioCtx = window.AudioContext || window.webkitAudioContext;
      const audioCtx = AudioCtx ? new AudioCtx() : null;

      function playPopSound() {
        if (!audioCtx) return;
        const t = audioCtx.currentTime;
        const o = audioCtx.createOscillator();
        const g = audioCtx.createGain();
        o.type = "triangle";
        o.frequency.setValueAtTime(900 + Math.random() * 200, t);
        g.gain.setValueAtTime(0.0001, t);
        g.gain.exponentialRampToValueAtTime(0.18, t + 0.01);
        g.gain.exponentialRampToValueAtTime(0.0001, t + 0.22);
        o.connect(g);
        g.connect(audioCtx.destination);
        o.start(t);
        o.stop(t + 0.25);
      }

      function playBoomSound() {
        if (!audioCtx) return;
        const t = audioCtx.currentTime;
        const o = audioCtx.createOscillator();
        const g = audioCtx.createGain();
        const biquad = audioCtx.createBiquadFilter();
        biquad.type = "lowpass";
        biquad.frequency.setValueAtTime(500, t);
        o.type = "sine";
        o.frequency.setValueAtTime(80, t);
        g.gain.setValueAtTime(0.0001, t);
        g.gain.exponentialRampToValueAtTime(0.5, t + 0.02);
        g.gain.exponentialRampToValueAtTime(0.0001, t + 0.9);
        o.connect(biquad);
        biquad.connect(g);
        g.connect(audioCtx.destination);
        o.start(t);
        o.stop(t + 1.0);
      }

      // short romantic arpeggio for 'người yêu'
      function playRomanticShort() {
        if (!audioCtx) return;
        const t = audioCtx.currentTime;
        const notes = [440, 660, 550, 880]; // simple arpeggio (A4, E5, C#5-ish --- pleasant)
        const master = audioCtx.createGain();
        master.gain.setValueAtTime(0.0001, t);
        master.gain.linearRampToValueAtTime(0.18, t + 0.02);
        master.gain.exponentialRampToValueAtTime(0.0001, t + 2.0);
        master.connect(audioCtx.destination);

        notes.forEach((freq, i) => {
          const o = audioCtx.createOscillator();
          const g = audioCtx.createGain();
          o.type = "sine";
          o.frequency.setValueAtTime(freq, t + i * 0.12);
          g.gain.setValueAtTime(0.0001, t + i * 0.12);
          g.gain.linearRampToValueAtTime(0.14, t + i * 0.12 + 0.06);
          g.gain.exponentialRampToValueAtTime(0.0001, t + i * 0.12 + 0.7);
          o.connect(g);
          g.connect(master);
          o.start(t + i * 0.12);
          o.stop(t + i * 0.12 + 0.9);
        });
      }

      function playSadTone() {
        if (!audioCtx) return;
        const t = audioCtx.currentTime;
        const o = audioCtx.createOscillator();
        const g = audioCtx.createGain();
        o.type = "sine";
        o.frequency.setValueAtTime(260, t);
        g.gain.setValueAtTime(0.0001, t);
        g.gain.exponentialRampToValueAtTime(0.12, t + 0.02);
        g.gain.exponentialRampToValueAtTime(0.0001, t + 0.7);
        o.connect(g);
        g.connect(audioCtx.destination);
        o.start(t);
        o.stop(t + 0.9);
      }

      // helper create particle element (heart / sad / bubble)
      function createParticle(iconClass, iconText, x, y, delay = 0, size = 18) {
        const el = document.createElement("div");
        el.className = "particle";
        el.style.left = x + "px";
        el.style.top = y + "px";
        el.style.fontSize = size + "px";
        el.innerHTML = `<span class="${iconClass}">${iconText}</span>`;
        // CSS animation via JS
        el.style.animation = `flyUpSmall ${
          900 + Math.random() * 500
        }ms forwards ${delay}ms`;
        effects.appendChild(el);
        // cleanup
        setTimeout(() => {
          el.remove();
        }, 2200 + delay);
      }

      // explosion of particles around center (cx,cy are viewport coords)
      function explodeParticles(type, cx, cy, count) {
        for (let i = 0; i < count; i++) {
          const angle = Math.PI * 2 * (i / count) + (Math.random() * 0.6 - 0.3);
          const radius = 30 + Math.random() * 130;
          const x = cx + Math.cos(angle) * radius + (Math.random() * 30 - 15);
          const y = cy + Math.sin(angle) * radius + (Math.random() * 30 - 15);
          if (type === "heart")
            createParticle(
              "heartIcon",
              "💖",
              x,
              y,
              i * 12,
              16 + Math.random() * 12
            );
          else if (type === "smallheart")
            createParticle(
              "heartIcon",
              "💗",
              x,
              y,
              i * 10,
              14 + Math.random() * 8
            );
          else if (type === "sad")
            createParticle(
              "sadIcon",
              "😢",
              x,
              y,
              i * 14,
              16 + Math.random() * 6
            );
          else if (type === "bubble")
            createParticle(
              "bubbleIcon",
              "🫧",
              x,
              y,
              i * 12,
              14 + Math.random() * 6
            );
        }
      }

      // show a big central burst visual
      function showBigBurst() {
        const wrap = document.createElement("div");
        wrap.className = "bigBurst";
        wrap.innerHTML = '<div class="core"></div>';
        bigBurstArea.appendChild(wrap);
        setTimeout(() => wrap.remove(), 1200);
      }

      // main sequence: 10 pops, 9 compress->10 explode
      async function runPopSequence(finalResult, cx, cy) {
        // ensure audio context resumed on user gesture (some browsers require this)
        if (audioCtx && audioCtx.state === "suspended") audioCtx.resume();

        // pop cadence (ms)
        const cadence = 220;
        // show intermediate random choices to create suspense
        for (let i = 0; i < 10; i++) {
          if (i < 8) {
            // regular pop
            playPopSound();
            bubble.classList.remove("compress", "explode");
            bubble.classList.add("pop");
            // random intermediate label for visual suspense
            const interim = choices[Math.floor(Math.random() * choices.length)];
            choiceLabel.textContent = interim.toUpperCase();
            // small particle burst per pop for fun
            explodeParticles("smallheart", cx, cy, 6);
            await wait(cadence);
            bubble.classList.remove("pop");
          } else if (i === 8) {
            // 9th: compress (co lại rõ rệt)
            playPopSound();
            bubble.classList.remove("pop");
            bubble.classList.add("compress");
            choiceLabel.textContent = "...";
            // tiny inward particles
            await wait(cadence + 60);
          } else {
            // 10th: final explode
            // remove compress then explode
            bubble.classList.remove("compress");
            bubble.classList.add("explode");
            // sound depends on result — boom for người yêu, milder for others
            if (finalResult === "người yêu") {
              // strong boom + romantic melody
              playBoomSound();
              playRomanticShort();
              // big visual boom
              showBigBurst();
              explodeParticles("heart", cx, cy, 28);
            } else if (finalResult === "bạn thân") {
              // mild pop chorus
              for (let s = 0; s < 3; s++) {
                setTimeout(playPopSound, s * 80);
              }
              explodeParticles("bubble", cx, cy, 14);
            } else {
              // bạn thường -> sad icons + sad tone
              playSadTone();
              explodeParticles("sad", cx, cy, 18);
            }
            // set final label
            choiceLabel.textContent = finalResult.toUpperCase();
            await wait(240);
            // apply bounce to the whole result label
            choiceLabel.style.animation = "finalBounce 900ms ease";
            // cleanup bounce after a few cycles
            setTimeout(() => {
              choiceLabel.style.animation = "";
              bubble.classList.remove("explode");
            }, 2200);
          }
        } // end for
      }

      function wait(ms) {
        return new Promise((res) => setTimeout(res, ms));
      }

      function pickRandom() {
        return choices[Math.floor(Math.random() * choices.length)];
      }

      revealBtn.addEventListener("click", async () => {
        const nameA = leftInput.value.trim() || "A";
        const nameB = rightInput.value.trim() || "B";
        updatePreviews();
        namesCombined.textContent = `Đang suy...`;
        choiceLabel.textContent = "";
        // compute center of bubble relative to viewport for explosion coords
        const rect = bubble.getBoundingClientRect();
        const cx = rect.left + rect.width / 2 + window.scrollX;
        const cy = rect.top + rect.height / 2 + window.scrollY;
        // determine final result ahead of time to orchestrate sounds
        const result = pickRandom();
        // run sequence: 10 pops with special 9->10 behavior
        await runPopSequence(result, cx, cy);
        // final small name display and ensure combined names correct
        namesCombined.textContent = `${nameA} ❤ ${nameB}`;
      });

      shuffleBtn.addEventListener("click", () => {
        leftInput.value = "";
        rightInput.value = "";
        updatePreviews();
        choiceLabel.textContent = "Chưa có";
        namesCombined.textContent = "— —";
      });

      // Enter to trigger
      [leftInput, rightInput].forEach((inp) =>
        inp.addEventListener("keydown", (e) => {
          if (e.key === "Enter") revealBtn.click();
        })
      );

      // initialize
      updatePreviews();
    </script>

    <footer
      style="
        text-align: center;
        margin-top: 40px;
        font-size: 13px;
        color: rgba(255, 255, 255, 0.45);
      "
    >
      Web Dành Cho <strong>Chien De</strong>
    </footer>
  </body>
</html>
