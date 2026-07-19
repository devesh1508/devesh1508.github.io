---
layout: page
permalink: /videos/
title: videos
description: Demos and talks — autonomous robotic assembly, tactile manipulation, and more. Click any thumbnail to play.
nav: true
nav_order: 3
---

<div id="vidGrid" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:20px;"></div>

<script>
(function(){
  const IDS = [
    "iyMES2UFMdI","QqK2NnUV6Vw","2inxpdrq74U","akjGDgfwLbM",
    "YWk4PPY-IE8","cZ9M1DQ23OI","9vJmqVti8to","XNYkWSHkAaU",
    "YB7ust0gHYw","Ss2JrlXx93U","QLgThVoxceQ","ojlZDaGytSY",
    "jMVBg_e3gLw","VsClK04qDhk","xaxNCXBovpc","Rn4gCsByFc0"
  ];
  const grid = document.getElementById('vidGrid');
  IDS.forEach(id => {
    const card = document.createElement('div');
    const btn = document.createElement('button');
    btn.setAttribute('aria-label','Play video');
    btn.style.cssText = 'position:relative;aspect-ratio:16/9;width:100%;border:1px solid rgba(128,128,128,.3);border-radius:6px;overflow:hidden;cursor:pointer;padding:0;background:#000;display:block;';
    btn.innerHTML = '<img loading="lazy" src="https://i.ytimg.com/vi/'+id+'/hqdefault.jpg" alt="Video thumbnail" style="width:100%;height:100%;object-fit:cover;display:block;">' +
      '<span style="position:absolute;inset:0;margin:auto;width:50px;height:50px;border-radius:50%;background:rgba(0,0,0,.7);pointer-events:none;display:flex;align-items:center;justify-content:center;"><span style="width:0;height:0;border-left:14px solid #fff;border-top:9px solid transparent;border-bottom:9px solid transparent;margin-left:4px;"></span></span>';
    btn.addEventListener('click', () => {
      const ifr = document.createElement('iframe');
      ifr.src = 'https://www.youtube-nocookie.com/embed/'+id+'?autoplay=1&rel=0';
      ifr.allow = 'accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture';
      ifr.allowFullscreen = true;
      ifr.style.cssText = 'position:absolute;inset:0;width:100%;height:100%;border:0;';
      btn.replaceChildren(ifr);
    }, { once: true });
    const cap = document.createElement('a');
    cap.href = 'https://www.youtube.com/watch?v='+id;
    cap.target = '_blank'; cap.rel = 'noopener';
    cap.textContent = 'Watch on YouTube';
    cap.style.cssText = 'display:block;font-size:.8rem;margin-top:6px;text-decoration:none;opacity:.8;';
    card.append(btn, cap);
    grid.appendChild(card);
    fetch('https://noembed.com/embed?url=https://www.youtube.com/watch?v='+id)
      .then(r => r.json())
      .then(d => { if (d && d.title) { cap.textContent = d.title; btn.setAttribute('aria-label','Play: '+d.title); } })
      .catch(() => {});
  });
})();
</script>
