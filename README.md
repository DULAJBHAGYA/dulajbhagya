<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Dulaj Bhagya — README</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=DM+Mono:wght@300;400;500&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #0a0a0b;
    --surface: #111113;
    --border: #1e1e22;
    --accent: #c8a96e;
    --accent2: #7b9ea6;
    --text: #e8e6e0;
    --muted: #6b6860;
    --dim: #3a3830;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-weight: 300;
    line-height: 1.7;
    overflow-x: hidden;
    min-height: 100vh;
  }

  /* Grain overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 999;
    opacity: 0.4;
  }

  .container {
    max-width: 860px;
    margin: 0 auto;
    padding: 0 2rem;
  }

  /* ── HEADER ── */
  header {
    padding: 7rem 0 5rem;
    position: relative;
    overflow: hidden;
  }

  .header-line {
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
    animation: shimmer 3s ease-in-out infinite;
  }

  @keyframes shimmer {
    0%, 100% { opacity: 0.3; }
    50% { opacity: 1; }
  }

  .label {
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    font-weight: 400;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 1.5rem;
    opacity: 0;
    animation: fadeUp 0.8s ease forwards 0.2s;
  }

  .name {
    font-family: 'Playfair Display', serif;
    font-size: clamp(3rem, 8vw, 5.5rem);
    font-weight: 900;
    line-height: 1.0;
    letter-spacing: -0.03em;
    color: var(--text);
    opacity: 0;
    animation: fadeUp 0.9s ease forwards 0.4s;
  }

  .name span {
    color: var(--accent);
    position: relative;
    display: inline-block;
  }

  .name span::after {
    content: '';
    position: absolute;
    bottom: 4px;
    left: 0; right: 0;
    height: 2px;
    background: var(--accent);
    transform: scaleX(0);
    transform-origin: left;
    animation: lineIn 0.8s ease forwards 1.4s;
  }

  @keyframes lineIn {
    to { transform: scaleX(1); }
  }

  .tagline {
    margin-top: 1.5rem;
    font-size: 1rem;
    color: var(--muted);
    max-width: 480px;
    font-weight: 300;
    opacity: 0;
    animation: fadeUp 0.9s ease forwards 0.7s;
  }

  .links {
    margin-top: 2.5rem;
    display: flex;
    gap: 1.2rem;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeUp 0.9s ease forwards 0.9s;
  }

  .link-btn {
    font-family: 'DM Mono', monospace;
    font-size: 0.7rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--muted);
    text-decoration: none;
    border: 1px solid var(--border);
    padding: 0.5rem 1.1rem;
    border-radius: 2px;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }

  .link-btn::before {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--accent);
    transform: translateX(-100%);
    transition: transform 0.3s ease;
    z-index: -1;
  }

  .link-btn:hover {
    color: var(--bg);
    border-color: var(--accent);
  }

  .link-btn:hover::before {
    transform: translateX(0);
  }

  /* ── DIVIDER ── */
  .divider {
    border: none;
    border-top: 1px solid var(--border);
    margin: 3.5rem 0;
    opacity: 0;
    animation: fadeIn 1s ease forwards 1.1s;
  }

  /* ── SECTIONS ── */
  .section {
    margin-bottom: 4.5rem;
    opacity: 0;
    transform: translateY(24px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }

  .section.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .section-label {
    font-family: 'DM Mono', monospace;
    font-size: 0.6rem;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 1.8rem;
    display: flex;
    align-items: center;
    gap: 1rem;
  }

  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  /* ── ABOUT ── */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
  }

  .about-cell {
    background: var(--surface);
    padding: 1.6rem;
    transition: background 0.3s ease;
  }

  .about-cell:hover {
    background: #15151a;
  }

  .cell-key {
    font-family: 'DM Mono', monospace;
    font-size: 0.6rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 0.5rem;
  }

  .cell-val {
    font-size: 0.92rem;
    color: var(--text);
    font-weight: 400;
  }

  /* ── STACK ── */
  .stack-group {
    margin-bottom: 2rem;
  }

  .stack-group-title {
    font-family: 'DM Mono', monospace;
    font-size: 0.6rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 0.9rem;
  }

  .tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
  }

  .tag {
    font-family: 'DM Mono', monospace;
    font-size: 0.72rem;
    color: var(--text);
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 0.35rem 0.85rem;
    border-radius: 2px;
    letter-spacing: 0.05em;
    transition: all 0.25s ease;
    cursor: default;
    position: relative;
    overflow: hidden;
  }

  .tag::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0;
    width: 100%; height: 1px;
    background: var(--accent);
    transform: scaleX(0);
    transition: transform 0.25s ease;
  }

  .tag:hover {
    border-color: var(--accent);
    color: var(--accent);
  }

  .tag:hover::after {
    transform: scaleX(1);
  }

  /* ── WRITING ── */
  .writing-list {
    display: flex;
    flex-direction: column;
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
  }

  .writing-item {
    background: var(--surface);
    display: grid;
    grid-template-columns: 120px 1fr 24px;
    align-items: center;
    gap: 1.5rem;
    padding: 1.2rem 1.6rem;
    text-decoration: none;
    color: inherit;
    transition: background 0.3s ease;
    group: true;
  }

  .writing-item:hover {
    background: #13131a;
  }

  .writing-item:hover .writing-title {
    color: var(--accent);
  }

  .writing-area {
    font-family: 'DM Mono', monospace;
    font-size: 0.62rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--accent2);
  }

  .writing-title {
    font-size: 0.88rem;
    color: var(--text);
    font-weight: 400;
    transition: color 0.3s ease;
  }

  .writing-arrow {
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    color: var(--dim);
    transition: color 0.3s ease, transform 0.3s ease;
    display: flex;
    align-items: center;
  }

  .writing-item:hover .writing-arrow {
    color: var(--accent);
    transform: translateX(4px);
  }

  /* ── FOOTER ── */
  footer {
    padding: 3rem 0 5rem;
    border-top: 1px solid var(--border);
  }

  .footer-inner {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
  }

  .footer-name {
    font-family: 'Playfair Display', serif;
    font-size: 1.1rem;
    color: var(--muted);
    font-weight: 400;
  }

  .footer-mono {
    font-family: 'DM Mono', monospace;
    font-size: 0.65rem;
    color: var(--dim);
    letter-spacing: 0.1em;
  }

  /* ── CURSOR DOT ── */
  .cursor {
    display: inline-block;
    width: 2px;
    height: 1em;
    background: var(--accent);
    margin-left: 2px;
    vertical-align: text-bottom;
    animation: blink 1s step-end infinite;
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  /* ── KEYFRAMES ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeIn {
    to { opacity: 1; }
  }

  /* ── SCROLL PROGRESS ── */
  .progress-bar {
    position: fixed;
    top: 0; left: 0;
    height: 2px;
    background: var(--accent);
    width: 0%;
    z-index: 1000;
    transition: width 0.1s linear;
  }

  /* ── STAT NUMBERS ── */
  .stats-row {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
    margin-bottom: 3rem;
  }

  .stat-cell {
    background: var(--surface);
    padding: 1.8rem 1.5rem;
    text-align: center;
    transition: background 0.3s ease;
  }

  .stat-cell:hover {
    background: #13131a;
  }

  .stat-num {
    font-family: 'Playfair Display', serif;
    font-size: 2.2rem;
    font-weight: 700;
    color: var(--accent);
    display: block;
    line-height: 1;
  }

  .stat-desc {
    font-family: 'DM Mono', monospace;
    font-size: 0.6rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--muted);
    margin-top: 0.5rem;
    display: block;
  }

  @media (max-width: 600px) {
    .about-grid { grid-template-columns: 1fr; }
    .stats-row { grid-template-columns: 1fr 1fr; }
    .writing-item { grid-template-columns: 90px 1fr 20px; gap: 0.8rem; }
    .footer-inner { flex-direction: column; align-items: flex-start; }
  }
</style>
</head>
<body>

<div class="progress-bar" id="progress"></div>

<div class="container">

  <!-- HEADER -->
  <header>
    <div class="header-line"></div>
    <div class="label">IT Undergraduate — Sri Lanka</div>
    <h1 class="name">Dulaj<br /><span>Bhagya</span></h1>
    <p class="tagline">Building full-stack and mobile applications. Writing about software engineering, architecture, and emerging technology.<span class="cursor"></span></p>
    <div class="links">
      <a class="link-btn" href="https://www.linkedin.com/in/dulaj-bhagya-7029aa213/" target="_blank">LinkedIn</a>
      <a class="link-btn" href="https://medium.com/@dulajupananda" target="_blank">Medium</a>
      <a class="link-btn" href="https://dulajupananda.netlify.app" target="_blank">Portfolio</a>
      <a class="link-btn" href="mailto:dulajupananda@icloud.com">Email</a>
    </div>
  </header>

  <hr class="divider" />

  <!-- ABOUT -->
  <section class="section">
    <div class="section-label">About</div>
    <div class="about-grid">
      <div class="about-cell">
        <div class="cell-key">Currently</div>
        <div class="cell-val">Pursuing a degree in Information Technology</div>
      </div>
      <div class="about-cell">
        <div class="cell-key">Focus</div>
        <div class="cell-val">Full-stack and mobile development</div>
      </div>
      <div class="about-cell">
        <div class="cell-key">Interests</div>
        <div class="cell-val">React, React Native, Flutter, Node.js, clean system architecture</div>
      </div>
      <div class="about-cell">
        <div class="cell-key">Writing</div>
        <div class="cell-val">Technical articles on Flutter, MongoDB, DevOps and more</div>
      </div>
    </div>
  </section>

  <!-- STATS -->
  <section class="section">
    <div class="section-label">At a Glance</div>
    <div class="stats-row">
      <div class="stat-cell">
        <span class="stat-num" data-target="7">0</span>
        <span class="stat-desc">Articles Published</span>
      </div>
      <div class="stat-cell">
        <span class="stat-num" data-target="6">0</span>
        <span class="stat-desc">Languages</span>
      </div>
      <div class="stat-cell">
        <span class="stat-num" data-target="4">0</span>
        <span class="stat-desc">Frameworks</span>
      </div>
    </div>
  </section>

  <!-- TECH STACK -->
  <section class="section">
    <div class="section-label">Tech Stack</div>

    <div class="stack-group">
      <div class="stack-group-title">Frontend & Mobile</div>
      <div class="tags">
        <span class="tag">React</span>
        <span class="tag">React Native</span>
        <span class="tag">Flutter</span>
        <span class="tag">Next.js</span>
        <span class="tag">Angular</span>
      </div>
    </div>

    <div class="stack-group">
      <div class="stack-group-title">Languages</div>
      <div class="tags">
        <span class="tag">JavaScript</span>
        <span class="tag">TypeScript</span>
        <span class="tag">Dart</span>
        <span class="tag">Java</span>
        <span class="tag">Go</span>
        <span class="tag">C++</span>
      </div>
    </div>

    <div class="stack-group">
      <div class="stack-group-title">Backend</div>
      <div class="tags">
        <span class="tag">Node.js</span>
        <span class="tag">Spring Boot</span>
        <span class="tag">.NET</span>
      </div>
    </div>

    <div class="stack-group">
      <div class="stack-group-title">Databases</div>
      <div class="tags">
        <span class="tag">PostgreSQL</span>
        <span class="tag">MongoDB</span>
        <span class="tag">MySQL</span>
        <span class="tag">MS SQL Server</span>
      </div>
    </div>

    <div class="stack-group">
      <div class="stack-group-title">Cloud & DevOps</div>
      <div class="tags">
        <span class="tag">Firebase</span>
        <span class="tag">Supabase</span>
        <span class="tag">Docker</span>
        <span class="tag">Kubernetes</span>
      </div>
    </div>

    <div class="stack-group">
      <div class="stack-group-title">Tools</div>
      <div class="tags">
        <span class="tag">Git</span>
        <span class="tag">Figma</span>
        <span class="tag">Postman</span>
        <span class="tag">Blender</span>
      </div>
    </div>
  </section>

  <!-- WRITING -->
  <section class="section">
    <div class="section-label">Writing</div>
    <div class="writing-list">
      <a class="writing-item" href="https://medium.com/@dulajupananda/building-a-robust-data-pipeline-in-python-from-apis-to-dashboard-6e28dd277441" target="_blank">
        <span class="writing-area">Data Engineering</span>
        <span class="writing-title">Building a Robust Data Pipeline in Python: From APIs to Dashboard</span>
        <span class="writing-arrow">&#8599;</span>
      </a>
      <a class="writing-item" href="https://medium.com/@dulajupananda/mastering-mongodb-unleashing-the-power-of-a-document-database-a422836802c9" target="_blank">
        <span class="writing-area">Database</span>
        <span class="writing-title">Mastering MongoDB: Unleashing the Power of a Document Database</span>
        <span class="writing-arrow">&#8599;</span>
      </a>
      <a class="writing-item" href="https://medium.com/@dulajupananda/kubernetes-vs-docker-swarm-for-full-stack-apps-practical-differences-178dc0abd3db" target="_blank">
        <span class="writing-area">DevOps</span>
        <span class="writing-title">Kubernetes vs Docker Swarm for Full-Stack Apps — Practical Differences</span>
        <span class="writing-arrow">&#8599;</span>
      </a>
      <a class="writing-item" href="https://medium.com/@dulajupananda/flutter-bloc-state-management-a-step-by-step-guide-1f1ab1c358f7" target="_blank">
        <span class="writing-area">Flutter</span>
        <span class="writing-title">Flutter BLoC State Management: A Step-by-step Guide</span>
        <span class="writing-arrow">&#8599;</span>
      </a>
      <a class="writing-item" href="https://medium.com/@dulajupananda/making-http-requests-in-flutter-using-the-dio-package-09d2af361f36" target="_blank">
        <span class="writing-area">Flutter</span>
        <span class="writing-title">Making HTTP Requests in Flutter: Using the Dio Package</span>
        <span class="writing-arrow">&#8599;</span>
      </a>
      <a class="writing-item" href="https://medium.com/@dulajupananda/simplifying-data-management-with-crud-operations-in-node-js-eb7da8ed61d9" target="_blank">
        <span class="writing-area">Node.js</span>
        <span class="writing-title">Simplifying Data Management with CRUD Operations in Node.js</span>
        <span class="writing-arrow">&#8599;</span>
      </a>
      <a class="writing-item" href="https://medium.com/@dulajupananda/emerging-trends-in-artificial-inteligence-ai-784479b5e72a" target="_blank">
        <span class="writing-area">AI</span>
        <span class="writing-title">Emerging Trends in Artificial Intelligence</span>
        <span class="writing-arrow">&#8599;</span>
      </a>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <div class="footer-inner">
      <span class="footer-name">Dulaj Bhagya Upananda</span>
      <span class="footer-mono">dulajupananda@icloud.com</span>
    </div>
  </footer>

</div>

<script>
  // Scroll progress
  window.addEventListener('scroll', () => {
    const el = document.getElementById('progress');
    const pct = window.scrollY / (document.body.scrollHeight - window.innerHeight) * 100;
    el.style.width = pct + '%';
  });

  // Intersection observer for section reveals
  const sections = document.querySelectorAll('.section');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.08 });
  sections.forEach(s => observer.observe(s));

  // Counter animation
  const counters = document.querySelectorAll('[data-target]');
  const counterObserver = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        const el = e.target;
        const target = parseInt(el.dataset.target);
        let current = 0;
        const step = target / 30;
        const timer = setInterval(() => {
          current += step;
          if (current >= target) { el.textContent = target; clearInterval(timer); }
          else el.textContent = Math.floor(current);
        }, 40);
        counterObserver.unobserve(el);
      }
    });
  }, { threshold: 0.5 });
  counters.forEach(c => counterObserver.observe(c));
</script>
</body>
</html>
