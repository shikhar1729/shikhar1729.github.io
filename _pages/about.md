---
layout: about
title: about
permalink: /

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false

selected_papers: true
social: false

announcements:
  enabled: true
  scrollable: true
  limit: 6

latest_posts:
  enabled: false
  scrollable: true
  limit: 3
---

Hi! I am an ML Engineer at [Apple](https://www.apple.com), where I work on improving power and
performance across Apple's operating systems using intelligent algorithms. Before Apple I
was at NVIDIA, where I worked on predicting node failures to keep large GPU fleets up, and
earlier on low-level, low-latency software for autonomous driving.

Outside that, I work on AI safety and mechanistic interpretability. The question I keep
returning to is whether a model's stated reasoning bears any load. The interesting question is
not whether an explanation sounds plausible, but whether it is causally connected to the
mechanism that produced the answer, and what our monitoring tools are actually measuring when
it is not.

I am a **Pivotal Research Fellow**, working with Noah Y. Siegel at Google DeepMind on
chain-of-thought faithfulness, and a **MARS V Research Fellow** at Meridian, working with
Julian Schulz on <span id="stego" class="stego" role="button" tabindex="0" aria-expanded="false">steganographic reasoning</span>. Earlier in 2026 I was a **SPAR Research Fellow** at
Kairos, where I worked on attention consistency training.

If you work on faithfulness, monitorability, or evaluation, I would be glad to hear from you.

<p class="contact-row">
  <a href="mailto:rbk.shikhar@gmail.com" title="Email" aria-label="Email"><i class="fa-solid fa-envelope"></i></a>
  <a href="https://scholar.google.com/citations?user=RvNitH0AAAAJ" title="Google Scholar" aria-label="Google Scholar"><i class="ai ai-google-scholar"></i></a>
  <a href="https://github.com/shikhar1729" title="GitHub" aria-label="GitHub"><i class="fa-brands fa-github"></i></a>
  <a href="https://www.linkedin.com/in/shikhar-shiromani" title="LinkedIn" aria-label="LinkedIn"><i class="fa-brands fa-linkedin"></i></a>
  <a href="/assets/pdf/Shikhar_Shiromani_CV.pdf" title="CV" aria-label="CV"><i class="ai ai-cv"></i></a>
</p>

<span id="trace" aria-hidden="true" style="font-size: 0; line-height: 0">​‌​‌‌​​‌​‌‌​‌‌‌‌​‌‌‌​‌​‌​​‌​​​​​​‌‌‌​​‌​​‌‌​​‌​‌​‌‌​​​​‌​‌‌​​‌​​​​‌​​​​​​‌‌‌​‌​​​‌‌​‌​​​​‌‌​​‌​‌​​‌​​​​​​‌‌​​​​‌​‌‌​​​‌‌​‌‌‌​‌​​​‌‌​‌​​‌​‌‌‌​‌‌​​‌‌​​​​‌​‌‌‌​‌​​​‌‌​‌​​‌​‌‌​‌‌‌‌​‌‌​‌‌‌​​‌‌‌​​‌‌​​‌​​​​​​‌‌​‌​​‌​‌‌​‌‌‌​​‌‌‌​​‌‌​‌‌‌​‌​​​‌‌​​‌​‌​‌‌​​​​‌​‌‌​​‌​​​​‌​​​​​​‌‌​‌‌‌‌​‌‌​​‌‌​​​‌​​​​​​‌‌‌​‌​​​‌‌​‌​​​​‌‌​​‌​‌​​‌​​​​​​‌‌​‌‌‌‌​‌‌‌​‌​‌​‌‌‌​‌​​​‌‌‌​​​​​‌‌‌​‌​‌​‌‌‌​‌​​​​‌​‌‌‌​​​‌​​​​​​‌​‌​‌​​​‌‌​‌​​​​‌‌​​​​‌​‌‌‌​‌​​​​‌​​​​​​‌‌​‌​​‌​‌‌‌​​‌‌​​‌​​​​​​‌‌‌​‌​​​‌‌​‌​​​​‌‌​​‌​‌​​‌​​​​​​‌‌‌​‌‌‌​‌‌​‌​​​​‌‌​‌‌‌‌​‌‌​‌‌​​​‌‌​​‌​‌​​‌​​​​​​‌‌​‌​‌​​‌‌​‌‌‌‌​‌‌​​​‌​​​‌​‌‌‌​</span>

<div id="stego-panel" class="stego-panel" hidden>
  <div class="stego-label">carrier &mdash; 560 zero-width characters, one bit each</div>
  <div class="stego-bits" id="stego-bits"></div>
  <div class="stego-out" id="stego-out"></div>
</div>

<script>
  (function () {
    var ZERO = "\u200b";
    var trigger = document.getElementById("stego");
    var panel = document.getElementById("stego-panel");
    var bitsEl = document.getElementById("stego-bits");
    var outEl = document.getElementById("stego-out");
    var carrier = document.getElementById("trace").textContent;
    var running = false;

    function decode(str) {
      var bits = "";
      for (var i = 0; i < str.length; i++) bits += str[i] === ZERO ? "0" : "1";
      var bytes = [];
      for (var j = 0; j + 8 <= bits.length; j += 8) bytes.push(parseInt(bits.slice(j, j + 8), 2));
      return new TextDecoder().decode(new Uint8Array(bytes));
    }

    function type(msg) {
      var n = 0;
      var t = setInterval(function () {
        outEl.textContent = msg.slice(0, ++n);
        if (n >= msg.length) { clearInterval(t); running = false; }
      }, 22);
    }

    function run() {
      if (running) return;
      running = true;
      panel.hidden = false;
      trigger.setAttribute("aria-expanded", "true");
      bitsEl.textContent = "";
      outEl.textContent = "";

      var glyphs = "";
      for (var i = 0; i < carrier.length; i++) glyphs += carrier[i] === ZERO ? "\u00b7" : "\u25aa";

      var shown = 0;
      var reveal = setInterval(function () {
        shown = Math.min(shown + 14, glyphs.length);
        bitsEl.textContent = glyphs.slice(0, shown);
        if (shown >= glyphs.length) { clearInterval(reveal); type(decode(carrier)); }
      }, 16);
    }

    function toggle() {
      if (!panel.hidden && !running) {
        panel.hidden = true;
        trigger.setAttribute("aria-expanded", "false");
        return;
      }
      run();
    }

    trigger.addEventListener("click", toggle);
    trigger.addEventListener("keydown", function (e) {
      if (e.key === "Enter" || e.key === " ") { e.preventDefault(); toggle(); }
    });
  })();
</script>
