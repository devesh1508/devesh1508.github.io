---
layout: about
title: about
permalink: /
subtitle: Lead Research Scientist, <a href="https://sra.samsung.com/">Samsung Research America</a>, Mountain View, CA

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false
  more_info: >
    <p>Samsung Research America</p>
    <p>Mountain View, California</p>

selected_papers: true
social: true

announcements:
  enabled: true
  scrollable: true
  limit: 5

latest_posts:
  enabled: false
---

I build robots that understand contact. I am a Lead Research Scientist in the Robot Intelligence Lab at **Samsung Research America**, where I am working on several fundamental topics for scalable dexterous manipulation. I am interested in creating multi-modal foundation models for robotics which can understand interaction semantics using vision, touch, force and more.

Previously, I was a Senior Principal Research Scientist at <a href="https://www.merl.com/">Mitsubishi Electric Research Labs (MERL)</a> in Cambridge, MA, where I led the robotic manipulation effort - setting fundamental research directions and finding avenues for commercializing matured technologies. I also had a brief stint as AI co-founder of a robotics startup, building its manipulation-focused AI strategy.

**From Contact to Cognition**: I believe robots exist in a physical world where they have to do more than seeing and reacting. I believe true autonomy would come by reasoning about making and breaking contacts with their environment. My research develops **physical intelligence for contact-rich robotic manipulation**: dexterous manipulation, tactile sensing, contact-implicit trajectory optimization, learning from demonstration, and foundation models for robotics. I have published 80+ papers at venues like ICRA, IROS, RSS, CoRL, T-RO, NeurIPS and ICML, and hold 20 granted or allowed patents.

I received my Ph.D. in Mechanical Engineering from Penn State, along with M.A. degrees in Mathematics and Mechanical Engineering, and my B.E. from Jadavpur University. I serve as Area Chair for NeurIPS, AAAI and ICML, and Associate Editor for IEEE T-ASE, ICRA, and CASE. I have mentored 25+ Ph.D. students and postdocs through research internships, most resulting in publications at top robotics and ML venues.

<!-- tactile marker-field background -->

<canvas id="tactile-bg" aria-hidden="true" style="position:fixed;inset:0;width:100vw;height:100vh;z-index:-1;pointer-events:none;"></canvas>
<script>
  (function () {
    const canvas = document.getElementById("tactile-bg");
    const reduced = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
    const ctx = canvas.getContext("2d");
    const SPACING = 44, R = 1.4, INFLUENCE = 120, PUSH = 18;
    let dots = [], W = 0, H = 0;
    let mouse = { x: -9999, y: -9999 };

    function build() {
      const dpr = window.devicePixelRatio || 1;
      W = window.innerWidth; H = window.innerHeight;
      canvas.width = W * dpr; canvas.height = H * dpr;
      ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
      dots = [];
      for (let y = SPACING / 2; y < H; y += SPACING)
        for (let x = SPACING / 2; x < W; x += SPACING)
          dots.push({ ox: x, oy: y, x: x, y: y, vx: 0, vy: 0 });
      if (reduced) drawStatic();
    }

    function dotColor(alpha) {
      const dark = document.documentElement.getAttribute("data-theme") === "dark";
      return dark ? "rgba(170,180,190," + alpha + ")" : "rgba(90,105,120," + alpha + ")";
    }

    function drawStatic() {
      ctx.clearRect(0, 0, W, H);
      ctx.fillStyle = dotColor(0.16);
      for (const d of dots) { ctx.beginPath(); ctx.arc(d.ox, d.oy, R, 0, 7); ctx.fill(); }
    }

    function step() {
      ctx.clearRect(0, 0, W, H);
      for (const d of dots) {
        const dx = d.x - mouse.x, dy = d.y - mouse.y;
        const dist = Math.hypot(dx, dy);
        if (dist < INFLUENCE && dist > 0.01) {
          const f = (1 - dist / INFLUENCE) * PUSH;
          d.vx += (dx / dist) * f * 0.12;
          d.vy += (dy / dist) * f * 0.12;
        }
        d.vx += (d.ox - d.x) * 0.06; d.vy += (d.oy - d.y) * 0.06;
        d.vx *= 0.86; d.vy *= 0.86;
        d.x += d.vx; d.y += d.vy;
        const t = Math.min(Math.hypot(d.x - d.ox, d.y - d.oy) / PUSH, 1);
        ctx.fillStyle = dotColor((0.14 + t * 0.35).toFixed(3));
        ctx.beginPath(); ctx.arc(d.x, d.y, R + t * 1.2, 0, 7); ctx.fill();
      }
      requestAnimationFrame(step);
    }

    window.addEventListener("pointermove", function (e) { mouse.x = e.clientX; mouse.y = e.clientY; });
    window.addEventListener("pointerleave", function () { mouse.x = -9999; mouse.y = -9999; });
    window.addEventListener("resize", build);
    build();
    if (!reduced) requestAnimationFrame(step);
  })();
</script>
