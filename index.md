---
layout: default
title: Home
permalink: /
---
<section class="hero">
  <h1>AI and Robotics</h1>
  <p>I build robotics and AI systems from first principles, with a focus on perception, estimation, control, and learning. My work combines mathematical modelling, implementation detail, and empirical validation.</p>
  <div class="button-row">
    <a class="button button-primary" href="{{ '/projects/' | relative_url }}">Projects</a>
    <a class="button" href="{{ '/technical-notes/' | relative_url }}">Technical Notes</a>
    <a class="button" href="https://github.com/samiosborn" target="_blank" rel="noopener noreferrer">GitHub</a>
    <a class="button" href="{{ '/about/' | relative_url }}">About</a>
  </div>
</section>

<section>
  <h2 class="section-title">Background</h2>
  <div class="proof-strip">
    <div class="proof-item">Mathematics training</div>
    <div class="proof-item">Imperial College London</div>
    <div class="proof-item">Robotics and AI builder</div>
    <div class="proof-item">Deeptech and startup exposure</div>
  </div>
</section>

<section>
  <h2 class="section-title">Featured Work</h2>
  <div class="card-grid">
    <article class="card">
      <h3><a href="{{ '/projects/vision-slam/monoslam/' | relative_url }}">MonoSLAM</a></h3>
      <p>Monocular SLAM pipeline with two-view bootstrap, keyframe tracking, and map refinement.</p>
      <p class="card-meta">Vision &amp; SLAM</p>
    </article>

    <article class="card">
      <h3><a href="{{ '/projects/robotics/self-balancing-robot/' | relative_url }}">Self-balancing Robot</a></h3>
      <p>Inverted pendulum platform for estimation, linearisation, and closed-loop controller design.</p>
      <p class="card-meta">Robotics</p>
    </article>

    <article class="card">
      <h3><a href="{{ '/projects/robotics/so100-arm/' | relative_url }}">SO100 Arm</a></h3>
      <p>Manipulation and control experiments on a low-cost robotic arm stack.</p>
      <p class="card-meta">Robotics</p>
    </article>

    <article class="card">
      <h3><a href="{{ '/projects/learning-control/double-dqn/' | relative_url }}">Double DQN</a></h3>
      <p>Value-based reinforcement learning with overestimation analysis and stability diagnostics.</p>
      <p class="card-meta">Learning &amp; Control</p>
    </article>
  </div>
</section>

<section>
  <h2 class="section-title">Writing and Thinking</h2>
  <div class="card-grid">
    <article class="card">
      <h3><a href="{{ '/technical-notes/' | relative_url }}">Technical Notes</a></h3>
      <p>Focused derivations, implementation notes, and system-level reasoning.</p>
    </article>
    <article class="card">
      <h3><a href="{{ '/build-logs/' | relative_url }}">Build Logs</a></h3>
      <p>Dated engineering updates: what changed, what broke, and what comes next.</p>
    </article>
    <article class="card">
      <h3><a href="{{ '/research-reflections/' | relative_url }}">Research Reflections</a></h3>
      <p>Longer-form thinking on robotics, learning systems, and technical strategy.</p>
    </article>
  </div>
</section>

<section>
  <h2 class="section-title">About</h2>
  <p>I am a mathematician building technical systems at the intersection of robotics, perception, control, and machine learning. I care about end-to-end stack design: modelling assumptions, algorithmic choices, software structure, and measurable performance.</p>
  <p>My current focus is on project-driven work where each build becomes a canonical technical record, from architecture decisions through to demos and post-mortems.</p>
  <p><a href="{{ '/about/' | relative_url }}">Read more about my background and research interests.</a></p>
</section>
