<html lang="en">
   <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Varun Sharma — Technical Architect & GenAI Engineer</title>
      <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@300;400;500;600;700&display=swap" rel="stylesheet">
      <style>
         *{margin:0;padding:0;box-sizing:border-box}
         :root{
         --bg:#0a0a0f;
         --surface:#12121a;
         --card:#16161f;
         --border:#1e1e2e;
         --accent:#6c63ff;
         --accent2:#00d4aa;
         --accent3:#ff6b6b;
         --accent4:#ffd93d;
         --text:#e4e4ed;
         --muted:#6b6b80;
         --glow:rgba(108,99,255,0.15);
         }
         body{background:var(--bg);color:var(--text);font-family:'Inter',sans-serif;min-height:100vh;overflow-x:hidden}
         body::before{content:'';position:fixed;inset:0;background:
         radial-gradient(ellipse 600px 600px at 20% 10%,rgba(108,99,255,0.06),transparent),
         radial-gradient(ellipse 500px 500px at 80% 80%,rgba(0,212,170,0.04),transparent);
         pointer-events:none;z-index:0}
         .wrapper{position:relative;z-index:1;max-width:960px;margin:0 auto;padding:60px 24px 100px}
         /* ── HERO ── */
         .hero{text-align:center;margin-bottom:64px;position:relative}
         .hero::after{content:'';position:absolute;bottom:-32px;left:50%;transform:translateX(-50%);width:120px;height:1px;background:linear-gradient(90deg,transparent,var(--accent),transparent)}
         .avatar-ring{width:140px;height:140px;border-radius:50%;padding:3px;background:conic-gradient(var(--accent),var(--accent2),var(--accent4),var(--accent3),var(--accent));margin:0 auto 28px;animation:spin 8s linear infinite}
         @keyframes spin{to{background:conic-gradient(var(--accent3),var(--accent),var(--accent2),var(--accent4),var(--accent3))}}
         .avatar-ring img{width:100%;height:100%;border-radius:50%;object-fit:cover;border:4px solid var(--bg)}
         .hero h1{font-size:2.6rem;font-weight:800;letter-spacing:-0.03em;margin-bottom:8px;background:linear-gradient(135deg,#fff,#a5a0ff);-webkit-background-clip:text;-webkit-text-fill-color:transparent}
         .hero .tagline{font-size:1.05rem;color:var(--muted);font-weight:400;line-height:1.6;max-width:620px;margin:0 auto 20px}
         .hero .location{font-size:0.85rem;color:var(--muted);margin-bottom:20px}
         .social-links{display:flex;gap:12px;justify-content:center;flex-wrap:wrap}
         .social-links a{display:inline-flex;align-items:center;gap:6px;padding:8px 18px;border-radius:8px;font-size:0.82rem;font-weight:500;text-decoration:none;color:var(--text);background:var(--card);border:1px solid var(--border);transition:all 0.25s ease}
         .social-links a:hover{border-color:var(--accent);background:var(--glow);transform:translateY(-2px)}
         .social-links a svg{width:16px;height:16px}
         /* ── SECTIONS ── */
         .section{margin-bottom:52px}
         .section-title{font-size:0.72rem;font-weight:700;text-transform:uppercase;letter-spacing:0.18em;color:var(--accent);margin-bottom:20px;display:flex;align-items:center;gap:10px}
         .section-title::after{content:'';flex:1;height:1px;background:var(--border)}
         /* ── ABOUT ── */
         .about-text{font-size:0.95rem;line-height:1.75;color:var(--text);opacity:0.9}
         /* ── STATS BAR ── */
         .stats-bar{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:12px;margin-bottom:52px}
         .stat-item{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:20px 16px;text-align:center}
         .stat-num{font-family:'JetBrains Mono',monospace;font-size:1.6rem;font-weight:700;color:var(--accent2);display:block}
         .stat-label{font-size:0.72rem;color:var(--muted);text-transform:uppercase;letter-spacing:0.1em;margin-top:4px}
         /* ── EXPERIENCE ── */
         .timeline{position:relative;padding-left:28px}
         .timeline::before{content:'';position:absolute;left:6px;top:8px;bottom:8px;width:2px;background:linear-gradient(var(--accent),var(--accent2))}
         .tl-item{position:relative;margin-bottom:28px}
         .tl-item::before{content:'';position:absolute;left:-24px;top:8px;width:10px;height:10px;border-radius:50%;background:var(--accent);border:2px solid var(--bg)}
         .tl-title{font-size:1rem;font-weight:700;color:#fff}
         .tl-company{font-size:0.85rem;color:var(--accent2);font-weight:500}
         .tl-period{font-size:0.75rem;color:var(--muted);margin:2px 0 8px;font-family:'JetBrains Mono',monospace}
         .tl-desc{font-size:0.85rem;color:var(--text);opacity:0.8;line-height:1.6}
         /* ── CERTIFICATIONS ── */
         .cert-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:14px}
         .cert-card{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:20px;display:flex;align-items:flex-start;gap:14px;transition:all 0.25s ease}
         .cert-card:hover{border-color:var(--accent);transform:translateY(-2px)}
         .cert-icon{font-size:1.8rem;flex-shrink:0}
         .cert-name{font-size:0.88rem;font-weight:600;color:#fff}
         .cert-issuer{font-size:0.75rem;color:var(--muted)}
         /* ── SKILLS ── */
         .skill-category{margin-bottom:18px}
         .skill-category-title{font-size:0.78rem;font-weight:600;color:var(--accent2);margin-bottom:10px;font-family:'JetBrains Mono',monospace}
         .skill-tags{display:flex;flex-wrap:wrap;gap:8px}
         .skill-tag{font-size:0.75rem;font-weight:500;padding:6px 14px;border-radius:6px;background:rgba(108,99,255,0.08);border:1px solid rgba(108,99,255,0.2);color:var(--text);font-family:'JetBrains Mono',monospace;transition:all 0.2s}
         .skill-tag:hover{background:rgba(108,99,255,0.15);border-color:var(--accent)}
         /* ── PROJECTS ── */
         .project-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:14px}
         .project-card{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:22px;transition:all 0.25s ease;text-decoration:none;color:var(--text);display:block}
         .project-card:hover{border-color:var(--accent);transform:translateY(-3px);box-shadow:0 8px 30px rgba(108,99,255,0.1)}
         .project-emoji{font-size:1.4rem;margin-bottom:10px;display:block}
         .project-name{font-size:0.95rem;font-weight:700;color:#fff;margin-bottom:6px}
         .project-desc{font-size:0.8rem;color:var(--muted);line-height:1.55;margin-bottom:12px}
         .project-stack{display:flex;flex-wrap:wrap;gap:6px}
         .project-stack span{font-size:0.65rem;padding:3px 8px;border-radius:4px;background:rgba(0,212,170,0.1);color:var(--accent2);font-family:'JetBrains Mono',monospace}
         /* ── EDUCATION ── */
         .edu-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:14px}
         .edu-card{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:20px}
         .edu-degree{font-size:0.92rem;font-weight:700;color:#fff}
         .edu-school{font-size:0.82rem;color:var(--accent2)}
         .edu-year{font-size:0.75rem;color:var(--muted);font-family:'JetBrains Mono',monospace}
         /* ── FOCUS ── */
         .focus-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:12px}
         .focus-card{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:18px;text-align:center}
         .focus-icon{font-size:1.6rem;margin-bottom:8px;display:block}
         .focus-label{font-size:0.82rem;font-weight:600;color:#fff}
         .focus-status{font-size:0.68rem;color:var(--accent2);text-transform:uppercase;letter-spacing:0.08em;margin-top:4px;font-family:'JetBrains Mono',monospace}
         /* ── GITHUB STATS ── */
         .gh-stats{text-align:center}
         .gh-stats img{max-width:100%;border-radius:10px;margin:6px}
         /* ── FOOTER ── */
         .footer{text-align:center;margin-top:60px;padding-top:32px;border-top:1px solid var(--border)}
         .footer p{font-size:0.78rem;color:var(--muted);line-height:1.8}
         .footer .heart{color:var(--accent3)}
         /* ── RESPONSIVE ── */
         @media(max-width:600px){
         .hero h1{font-size:1.8rem}
         .wrapper{padding:32px 16px 60px}
         .stats-bar{grid-template-columns:repeat(2,1fr)}
         }
      </style>
   </head>
   <body>
      <div class="wrapper">
         <!-- ═══ HERO ═══ -->
         <section class="hero">
            <div class="avatar-ring">
               <img src="https://avatars.githubusercontent.com/u/2123341?v=4" alt="Varun Sharma">
            </div>
            <h1>Varun Sharma</h1>
            <p class="tagline">Technical Architect &amp; GenAI Engineer with 14+ years designing enterprise-scale systems and building real-world AI solutions that scale.</p>
            <p class="location">📍 Greater Tampa Bay Area, FL &nbsp;·&nbsp; 🏢 Tata Consultancy Services</p>
            <div class="social-links">
               <a href="https://github.com/ivarunsharma" target="_blank">
                  <svg viewBox="0 0 24 24" fill="currentColor">
                     <path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/>
                  </svg>
                  GitHub
               </a>
               <a href="https://www.linkedin.com/in/ivarunsharma/" target="_blank">
                  <svg viewBox="0 0 24 24" fill="currentColor">
                     <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
                  </svg>
                  LinkedIn
               </a>
               <a href="mailto:ivarunsharma@gmail.com" target="_blank">
                  <svg viewBox="0 0 24 24" fill="currentColor">
                     <path d="M20 4H4c-1.1 0-2 .9-2 2v12c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
                  </svg>
                  Email
               </a>
            </div>
         </section>
         <!-- ═══ STATS ═══ -->
         <div class="stats-bar">
            <div class="stat-item"><span class="stat-num">14+</span><span class="stat-label">Years Experience</span></div>
            <div class="stat-item"><span class="stat-num">3x</span><span class="stat-label">AWS Certified</span></div>
            <div class="stat-item"><span class="stat-num">99.99%</span><span class="stat-label">System Uptime</span></div>
            <div class="stat-item"><span class="stat-num">25%</span><span class="stat-label">Perf. Improvement</span></div>
         </div>
         <!-- ═══ ABOUT ═══ -->
         <section class="section">
            <div class="section-title">About Me</div>
            <p class="about-text">
               Technical Architect with 14+ years of experience designing, optimizing, and delivering enterprise-scale technology solutions across banking and financial services. Currently at Tata Consultancy Services, supporting Citibank USA on large-scale transformation and modernization initiatives. I specialize in enterprise cloud architecture (AWS), full-stack development (Java, Python), and robust system design including microservices and distributed systems. Passionate about Generative AI, LLM applications, RAG pipelines, and AI Agents — actively building real-world AI systems that scale. Recognized as SPOC for complex technical escalations, consistently delivering under stringent SLAs while mentoring engineers and fostering continuous improvement.
            </p>
         </section>
         <!-- ═══ CURRENT FOCUS ═══ -->
         <section class="section">
            <div class="section-title">Current Focus</div>
            <div class="focus-grid">
               <div class="focus-card"><span class="focus-icon">🧠</span><span class="focus-label">Generative AI & LLMs</span><span class="focus-status">Primary Focus</span></div>
               <div class="focus-card"><span class="focus-icon">🔗</span><span class="focus-label">RAG Pipelines</span><span class="focus-status">Active</span></div>
               <div class="focus-card"><span class="focus-icon">🤖</span><span class="focus-label">AI Agents & Automation</span><span class="focus-status">Building</span></div>
               <div class="focus-card"><span class="focus-icon">☁️</span><span class="focus-label">Cloud (AWS / Azure)</span><span class="focus-status">Deepening</span></div>
            </div>
         </section>
         <!-- ═══ EXPERIENCE ═══ -->
         <section class="section">
            <div class="section-title">Experience</div>
            <div class="timeline">
               <div class="tl-item">
                  <div class="tl-title">Assistant Consultant</div>
                  <div class="tl-company">Tata Consultancy Services · Citibank USA</div>
                  <div class="tl-period">Oct 2019 — Present · Tampa, FL</div>
                  <div class="tl-desc">Orchestrating annual SWIFT upgrades ensuring 99.99% availability. Architected failover & clustering solutions. Automated performance analysis achieving 25% improvement in response times. SPOC for critical technical escalations under stringent SLAs.</div>
               </div>
               <div class="tl-item">
                  <div class="tl-title">IT Analyst</div>
                  <div class="tl-company">Tata Consultancy Services · Northern Trust</div>
                  <div class="tl-period">Apr 2016 — Oct 2019 · Gurgaon, India</div>
                  <div class="tl-desc">Developed web services and REST APIs. Managed delivery and deployment using uDeploy, Oracle, and shell scripts. Led knowledge-sharing sessions and source code management with GIT.</div>
               </div>
               <div class="tl-item">
                  <div class="tl-title">Systems Engineer</div>
                  <div class="tl-company">Tata Consultancy Services · Société Générale</div>
                  <div class="tl-period">Mar 2015 — Mar 2016 · Gurgaon, India</div>
                  <div class="tl-desc">Developed interfaces using Java & XML for TCS BaNCS Corporate Actions. Source code refactoring using FORTIFY and SONAR. Offshore support for onsite teams.</div>
               </div>
               <div class="tl-item">
                  <div class="tl-title">Software Developer</div>
                  <div class="tl-company">Oodles Technologies Pvt Ltd</div>
                  <div class="tl-period">Feb 2012 — Mar 2015 · Gurgaon, India</div>
                  <div class="tl-desc">Full-stack development for web/mobile apps. Backend development with Grails, Jenkins CI/CD, AWS/Azure environments. Client scrum meetings and daily standup management.</div>
               </div>
            </div>
         </section>
         <!-- ═══ CERTIFICATIONS ═══ -->
         <section class="section">
            <div class="section-title">Certifications</div>
            <div class="cert-grid">
               <div class="cert-card">
                  <span class="cert-icon">🏅</span>
                  <div>
                     <div class="cert-name">AWS Certified GenAI Developer — Professional</div>
                     <div class="cert-issuer">Amazon Web Services · Feb 2026</div>
                  </div>
               </div>
               <div class="cert-card">
                  <span class="cert-icon">🏅</span>
                  <div>
                     <div class="cert-name">AWS Certified Solutions Architect — Associate</div>
                     <div class="cert-issuer">Amazon Web Services</div>
                  </div>
               </div>
               <div class="cert-card">
                  <span class="cert-icon">🏅</span>
                  <div>
                     <div class="cert-name">AWS Certified Cloud Practitioner</div>
                     <div class="cert-issuer">Amazon Web Services</div>
                  </div>
               </div>
            </div>
         </section>
         <!-- ═══ SKILLS ═══ -->
         <section class="section">
            <div class="section-title">Tech Stack</div>
            <div class="skill-category">
               <div class="skill-category-title">// Languages</div>
               <div class="skill-tags">
                  <span class="skill-tag">Java</span><span class="skill-tag">Python</span><span class="skill-tag">J2EE</span><span class="skill-tag">Groovy</span><span class="skill-tag">Shell/UNIX</span><span class="skill-tag">SQL</span><span class="skill-tag">JavaScript</span><span class="skill-tag">HTML/CSS</span>
               </div>
            </div>
            <div class="skill-category">
               <div class="skill-category-title">// AI & ML</div>
               <div class="skill-tags">
                  <span class="skill-tag">LLMs</span><span class="skill-tag">RAG</span><span class="skill-tag">AI Agents</span><span class="skill-tag">Prompt Engineering</span><span class="skill-tag">Claude API</span><span class="skill-tag">OpenAI</span><span class="skill-tag">Streamlit</span><span class="skill-tag">LangChain</span>
               </div>
            </div>
            <div class="skill-category">
               <div class="skill-category-title">// Cloud & DevOps</div>
               <div class="skill-tags">
                  <span class="skill-tag">AWS</span><span class="skill-tag">Azure</span><span class="skill-tag">Jenkins</span><span class="skill-tag">Git</span><span class="skill-tag">uDeploy</span><span class="skill-tag">Docker</span><span class="skill-tag">Grafana</span><span class="skill-tag">IBM WebSphere</span>
               </div>
            </div>
            <div class="skill-category">
               <div class="skill-category-title">// Databases & Messaging</div>
               <div class="skill-tags">
                  <span class="skill-tag">Oracle</span><span class="skill-tag">MySQL</span><span class="skill-tag">SQLite</span><span class="skill-tag">Kafka</span><span class="skill-tag">REST APIs</span>
               </div>
            </div>
            <div class="skill-category">
               <div class="skill-category-title">// Architecture & Design</div>
               <div class="skill-tags">
                  <span class="skill-tag">Microservices</span><span class="skill-tag">System Design (HLD/LLD)</span><span class="skill-tag">Distributed Systems</span><span class="skill-tag">Failover & Clustering</span><span class="skill-tag">Design Patterns</span><span class="skill-tag">SDLC</span>
               </div>
            </div>
         </section>
         <!-- ═══ PROJECTS ═══ -->
         <section class="section">
            <div class="section-title">Featured Projects</div>
            <div class="project-grid">
               <a class="project-card" href="https://github.com/ivarunsharma/ai-news-digest" target="_blank">
                  <span class="project-emoji">🤖</span>
                  <div class="project-name">ai-news-digest</div>
                  <div class="project-desc">AI-powered news dashboard — fetches live headlines, summarizes with Claude Haiku, stores to SQLite.</div>
                  <div class="project-stack"><span>Python</span><span>Streamlit</span><span>Claude Haiku</span><span>NewsAPI</span></div>
               </a>
               <a class="project-card" href="https://github.com/ivarunsharma/ai-summarizer" target="_blank">
                  <span class="project-emoji">✍️</span>
                  <div class="project-name">ai-summarizer</div>
                  <div class="project-desc">Summarize any text or URL in seconds — 4 styles including ELI5 & Key Takeaways.</div>
                  <div class="project-stack"><span>Python</span><span>Streamlit</span><span>Claude API</span><span>newspaper3k</span></div>
               </a>
               <a class="project-card" href="https://github.com/ivarunsharma/GenaipythonExamples" target="_blank">
                  <span class="project-emoji">🐍</span>
                  <div class="project-name">GenaipythonExamples</div>
                  <div class="project-desc">Hands-on Generative AI code examples with Python covering LLMs, agents, and more.</div>
                  <div class="project-stack"><span>Python</span><span>LLMs</span><span>GenAI</span></div>
               </a>
            </div>
         </section>
         <!-- ═══ EDUCATION ═══ -->
         <section class="section">
            <div class="section-title">Education</div>
            <div class="edu-grid">
               <div class="edu-card">
                  <div class="edu-degree">M.Tech — Computer Science</div>
                  <div class="edu-school">Maharishi Markandeshwar University</div>
               </div>
               <div class="edu-card">
                  <div class="edu-degree">B.Tech — Information Technology</div>
                  <div class="edu-school">Kurukshetra University</div>
               </div>
            </div>
         </section>
         <!-- ═══ GITHUB STATS ═══ -->
         <section class="section">
            <div class="section-title">GitHub Activity</div>
            <div class="gh-stats">
               <img src="https://github-readme-stats.vercel.app/api?username=ivarunsharma&show_icons=true&theme=midnight-purple&hide_border=true&bg_color=0a0a0f&title_color=6c63ff&icon_color=00d4aa&text_color=e4e4ed" alt="GitHub Stats">
               <br>
               <img src="https://streak-stats.demolab.com/?user=ivarunsharma&theme=midnight-purple&hide_border=true&background=0a0a0f&ring=6c63ff&fire=ff6b6b&currStreakLabel=00d4aa" alt="GitHub Streak">
               <br>
               <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=ivarunsharma&layout=compact&theme=midnight-purple&hide_border=true&bg_color=0a0a0f&title_color=6c63ff&text_color=e4e4ed" alt="Top Languages">
            </div>
         </section>
         <!-- ═══ COLLABORATION ═══ -->
         <section class="section">
            <div class="section-title">Open to Collaborate</div>
            <div class="focus-grid">
               <div class="focus-card"><span class="focus-icon">🚀</span><span class="focus-label">GenAI & LLM Products</span></div>
               <div class="focus-card"><span class="focus-icon">🔗</span><span class="focus-label">RAG Systems & AI Agents</span></div>
               <div class="focus-card"><span class="focus-icon">📦</span><span class="focus-label">Productionizing AI Apps</span></div>
               <div class="focus-card"><span class="focus-icon">⚡</span><span class="focus-label">Intelligent Automation</span></div>
            </div>
         </section>
         <!-- ═══ FOOTER ═══ -->
         <div class="footer">
            <p>Building the future, one model at a time.<br><span class="heart">♥</span> Crafted by Varun Sharma · 2026</p>
         </div>
      </div>
   </body>
</html>
