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
Julian Schulz on steganographic reasoning. Earlier in 2026 I was a **SPAR Research Fellow** at
Kairos, where I worked on attention consistency training.

If you work on faithfulness, monitorability, or evaluation, I would be glad to hear from you.

<p class="contact-row">
  <a href="mailto:rbk.shikhar@gmail.com" title="Email" aria-label="Email"><i class="fa-solid fa-envelope"></i></a>
  <a href="https://scholar.google.com/citations?user=RvNitH0AAAAJ" title="Google Scholar" aria-label="Google Scholar"><i class="ai ai-google-scholar"></i></a>
  <a href="https://github.com/shikhar1729" title="GitHub" aria-label="GitHub"><i class="fa-brands fa-github"></i></a>
  <a href="https://www.linkedin.com/in/shikhar-shiromani" title="LinkedIn" aria-label="LinkedIn"><i class="fa-brands fa-linkedin"></i></a>
  <a href="/assets/pdf/Shikhar_Shiromani_CV.pdf" title="CV" aria-label="CV"><i class="ai ai-cv"></i></a>
</p>

<!--
  There is reasoning in this page that the rendered text does not show.
  It is encoded the way a model would hide it: in the token stream, not the prose.
  Open the console and run reveal().
-->
<span id="trace" aria-hidden="true" style="font-size: 0; line-height: 0">​‌​‌‌​​‌​‌‌​‌‌‌‌​‌‌‌​‌​‌​​‌​​​​​​‌‌‌​​‌​​‌‌​​‌​‌​‌‌​​​​‌​‌‌​​‌​​​​‌​​​​​​‌‌‌​‌​​​‌‌​‌​​​​‌‌​​‌​‌​​‌​​​​​​‌‌​​​​‌​‌‌​​​‌‌​‌‌‌​‌​​​‌‌​‌​​‌​‌‌‌​‌‌​​‌‌​​​​‌​‌‌‌​‌​​​‌‌​‌​​‌​‌‌​‌‌‌‌​‌‌​‌‌‌​​‌‌‌​​‌‌​​‌​​​​​​‌‌​‌​​‌​‌‌​‌‌‌​​‌‌‌​​‌‌​‌‌‌​‌​​​‌‌​​‌​‌​‌‌​​​​‌​‌‌​​‌​​​​‌​​​​​​‌‌​‌‌‌‌​‌‌​​‌‌​​​‌​​​​​​‌‌‌​‌​​​‌‌​‌​​​​‌‌​​‌​‌​​‌​​​​​​‌‌​‌‌‌‌​‌‌‌​‌​‌​‌‌‌​‌​​​‌‌‌​​​​​‌‌‌​‌​‌​‌‌‌​‌​​​​‌​‌‌‌​​​‌​​​​​​‌​‌​‌​​​‌‌​‌​​​​‌‌​​​​‌​‌‌‌​‌​​​​‌​​​​​​‌‌​‌​​‌​‌‌‌​​‌‌​​‌​​​​​​‌‌‌​‌​​​‌‌​‌​​​​‌‌​​‌​‌​​‌​​​​​​‌‌‌​‌‌‌​‌‌​‌​​​​‌‌​‌‌‌‌​‌‌​‌‌​​​‌‌​​‌​‌​​‌​​​​​​‌‌​‌​‌​​‌‌​‌‌‌‌​‌‌​​​‌​​​‌​‌‌‌​</span>

<script>
  (function () {
    var ZERO = "\u200b";
    var carrier = document.getElementById("trace");
    var log = window["con" + "sole"].log;

    function decode(s) {
      var bits = "";
      for (var i = 0; i < s.length; i++) bits += s[i] === ZERO ? "0" : "1";
      var bytes = [];
      for (var j = 0; j + 8 <= bits.length; j += 8) bytes.push(parseInt(bits.slice(j, j + 8), 2));
      return new TextDecoder().decode(new Uint8Array(bytes));
    }

    window.reveal = function () {
      var out = decode(carrier.textContent);
      log("%c" + out, "font-size:13px;line-height:1.7;font-style:italic");
      return out;
    };

    log(
      "%cThis page carries reasoning its visible text does not.%c\nRun %creveal()%c to decode it.",
      "font-weight:600", "", "font-family:monospace", ""
    );
  })();
</script>
