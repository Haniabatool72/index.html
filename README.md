<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Hania Batool — Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400;1,700&family=Inter:wght@300;400;500;600&family=Space+Mono:ital@0;1&display=swap" rel="stylesheet"/>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css"/>
<style>
/* ============================================================
   DESIGN TOKENS
   ============================================================ */
:root{
  --bg:           #0a0a0f;
  --bg2:          #111118;
  --surface:      rgba(255,255,255,.04);
  --surface-h:    rgba(255,255,255,.08);
  --border:       rgba(255,255,255,.08);
  --border-h:     rgba(79,140,255,.4);
  --blue:         #4f8cff;
  --blue2:        #7ab3ff;
  --blue-glow:    rgba(79,140,255,.18);
  --white:        #f0f4ff;
  --muted:        #8892a4;
  --text:         #d4daf0;
  --display:      'Playfair Display', serif;
  --body:         'Inter', sans-serif;
  --mono:         'Space Mono', monospace;
  --r:            14px;
  --r2:           22px;
  --ease:         cubic-bezier(.4,0,.2,1);
  --shadow:       0 8px 40px rgba(0,0,0,.5);
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth;font-size:16px}
body{
  background:var(--bg);
  color:var(--text);
  font-family:var(--body);
  line-height:1.7;
  overflow-x:hidden;
}
::selection{background:var(--blue);color:#fff}
a{color:inherit;text-decoration:none}
img{max-width:100%}
button{cursor:pointer;border:none;background:none;font-family:inherit}

/* ============================================================
   SCROLLBAR
   ============================================================ */
::-webkit-scrollbar{width:5px}
::-webkit-scrollbar-track{background:var(--bg)}
::-webkit-scrollbar-thumb{background:var(--blue);border-radius:99px}

/* ============================================================
   LOADING SCREEN
   ============================================================ */
#loader{
  position:fixed;inset:0;z-index:9999;
  background:var(--bg);
  display:flex;flex-direction:column;align-items:center;justify-content:center;gap:24px;
  transition:opacity .6s var(--ease),visibility .6s;
}
#loader.hidden{opacity:0;visibility:hidden}
.loader-logo{
  font-family:var(--display);
  font-style:italic;
  font-size:2rem;
  color:var(--white);
  letter-spacing:.04em;
}
.loader-logo span{color:var(--blue)}
.loader-bar{
  width:160px;height:2px;
  background:var(--surface-h);
  border-radius:99px;overflow:hidden;
}
.loader-fill{
  height:100%;width:0;
  background:linear-gradient(90deg,var(--blue),var(--blue2));
  border-radius:99px;
  animation:loadFill 1.6s var(--ease) forwards;
}
@keyframes loadFill{to{width:100%}}

/* ============================================================
   WELCOME POPUP
   ============================================================ */
#welcome-popup{
  position:fixed;inset:0;z-index:9000;
  display:flex;align-items:center;justify-content:center;
  background:rgba(0,0,0,.7);
  backdrop-filter:blur(10px);
  opacity:0;visibility:hidden;
  transition:all .5s var(--ease);
}
#welcome-popup.show{opacity:1;visibility:visible}
.popup-card{
  background:linear-gradient(135deg,rgba(255,255,255,.07),rgba(255,255,255,.02));
  border:1px solid var(--border-h);
  border-radius:var(--r2);
  padding:48px 56px;
  text-align:center;
  max-width:500px;
  width:90%;
  position:relative;
  backdrop-filter:blur(20px);
  box-shadow:0 0 80px var(--blue-glow);
  animation:popIn .5s var(--ease);
}
@keyframes popIn{from{transform:scale(.85);opacity:0}to{transform:scale(1);opacity:1}}
.popup-emoji{font-size:3rem;margin-bottom:16px;display:block}
.popup-card h2{
  font-family:var(--display);font-style:italic;
  font-size:1.75rem;color:var(--white);margin-bottom:8px;
}
.popup-card p{color:var(--muted);font-size:.95rem;margin-bottom:28px}
.popup-close{
  background:var(--blue);
  color:#fff;border-radius:99px;
  padding:12px 36px;font-size:.9rem;font-weight:600;letter-spacing:.06em;
  transition:transform .2s,box-shadow .2s;
}
.popup-close:hover{transform:translateY(-2px);box-shadow:0 8px 24px rgba(79,140,255,.4)}
.popup-x{
  position:absolute;top:16px;right:20px;
  font-size:1.25rem;color:var(--muted);cursor:pointer;
  transition:color .2s;
}
.popup-x:hover{color:var(--white)}

/* ============================================================
   CANVAS BACKGROUND
   ============================================================ */
#bg-canvas{
  position:fixed;inset:0;z-index:-1;
  pointer-events:none;
}

/* ============================================================
   NAVBAR
   ============================================================ */
nav{
  position:fixed;top:0;left:0;right:0;z-index:800;
  padding:0 5%;
  height:70px;
  display:flex;align-items:center;justify-content:space-between;
  transition:background .4s,backdrop-filter .4s,border-bottom .4s;
}
nav.scrolled{
  background:rgba(10,10,15,.85);
  backdrop-filter:blur(24px);
  border-bottom:1px solid var(--border);
}
.nav-logo{
  font-family:var(--display);font-style:italic;
  font-size:1.4rem;font-weight:700;color:var(--white);
  letter-spacing:.02em;
}
.nav-logo span{color:var(--blue)}
.nav-links{display:flex;align-items:center;gap:36px;list-style:none}
.nav-links a{
  font-size:.85rem;font-weight:500;letter-spacing:.08em;
  text-transform:uppercase;color:var(--muted);
  position:relative;transition:color .25s;
}
.nav-links a::after{
  content:'';position:absolute;bottom:-4px;left:0;right:100%;
  height:1px;background:var(--blue);
  transition:right .3s var(--ease);
}
.nav-links a:hover{color:var(--white)}
.nav-links a:hover::after{right:0}
.nav-toggle{display:none;flex-direction:column;gap:5px;padding:6px;cursor:pointer}
.nav-toggle span{display:block;width:24px;height:2px;background:var(--white);border-radius:2px;transition:all .3s}
.nav-toggle.open span:nth-child(1){transform:rotate(45deg) translate(5px,5px)}
.nav-toggle.open span:nth-child(2){opacity:0}
.nav-toggle.open span:nth-child(3){transform:rotate(-45deg) translate(5px,-5px)}
.mobile-menu{
  display:none;
  position:fixed;top:70px;left:0;right:0;
  background:rgba(10,10,15,.97);backdrop-filter:blur(24px);
  border-bottom:1px solid var(--border);
  flex-direction:column;padding:24px 5%;gap:0;
  transform:translateY(-16px);opacity:0;
  transition:all .35s var(--ease);
}
.mobile-menu.open{display:flex;transform:translateY(0);opacity:1}
.mobile-menu a{
  padding:14px 0;font-size:.95rem;letter-spacing:.06em;
  text-transform:uppercase;color:var(--muted);font-weight:500;
  border-bottom:1px solid var(--border);transition:color .2s;
}
.mobile-menu a:last-child{border-bottom:none}
.mobile-menu a:hover{color:var(--white)}

/* ============================================================
   SECTIONS SHARED
   ============================================================ */
section{padding:110px 5%}
.section-label{
  display:inline-block;
  font-family:var(--mono);font-style:italic;
  font-size:.75rem;letter-spacing:.18em;text-transform:uppercase;
  color:var(--blue);margin-bottom:14px;
}
.section-title{
  font-family:var(--display);font-style:italic;
  font-size:clamp(2rem,4vw,3rem);
  color:var(--white);line-height:1.15;margin-bottom:16px;
}
.section-line{
  width:48px;height:2px;
  background:linear-gradient(90deg,var(--blue),var(--blue2));
  border-radius:2px;margin-bottom:48px;
}

/* ============================================================
   HERO
   ============================================================ */
#hero{
  min-height:100vh;
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  text-align:center;padding-top:70px;
  position:relative;overflow:hidden;
}
.hero-badge{
  display:inline-flex;align-items:center;gap:8px;
  border:1px solid var(--border-h);border-radius:99px;
  padding:6px 18px;font-size:.8rem;color:var(--blue2);
  font-family:var(--mono);letter-spacing:.1em;
  margin-bottom:32px;
  background:rgba(79,140,255,.06);
  animation:fadeUp .8s .2s var(--ease) both;
}
.hero-badge .dot{width:6px;height:6px;border-radius:50%;background:var(--blue);animation:pulse 2s infinite}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.3}}
.hero-h1{
  font-family:var(--display);font-style:italic;
  font-size:clamp(2.6rem,6.5vw,5.5rem);
  font-weight:700;color:var(--white);
  line-height:1.08;letter-spacing:-.01em;
  animation:fadeUp .8s .35s var(--ease) both;
}
.hero-h1 .name-blue{
  background:linear-gradient(135deg,var(--blue),var(--blue2));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
}
.hero-sub{
  font-size:1rem;color:var(--muted);margin-top:16px;
  font-weight:400;letter-spacing:.02em;
  animation:fadeUp .8s .5s var(--ease) both;
}
.hero-type-wrap{
  margin-top:28px;height:48px;display:flex;align-items:center;justify-content:center;
  animation:fadeUp .8s .65s var(--ease) both;
}
.hero-type-prefix{color:var(--muted);font-size:1.1rem;margin-right:10px;font-style:italic;font-family:var(--display)}
#typed-text{
  font-family:var(--display);font-style:italic;
  font-size:1.35rem;color:var(--blue2);font-weight:700;
}
.cursor{display:inline-block;width:2px;height:1.2em;background:var(--blue);margin-left:3px;vertical-align:middle;animation:blink .7s infinite}
@keyframes blink{0%,100%{opacity:1}50%{opacity:0}}
.hero-desc{
  max-width:560px;margin:28px auto 0;
  font-size:.95rem;color:var(--muted);line-height:1.8;
  animation:fadeUp .8s .8s var(--ease) both;
}
.hero-ctas{
  margin-top:44px;display:flex;gap:16px;justify-content:center;flex-wrap:wrap;
  animation:fadeUp .8s .95s var(--ease) both;
}
.btn-primary{
  background:var(--blue);color:#fff;
  padding:14px 34px;border-radius:99px;font-size:.88rem;font-weight:600;
  letter-spacing:.06em;transition:all .25s;
  box-shadow:0 0 0 0 rgba(79,140,255,.4);
}
.btn-primary:hover{transform:translateY(-3px);box-shadow:0 8px 30px rgba(79,140,255,.45)}
.btn-ghost{
  border:1px solid var(--border-h);color:var(--blue2);
  padding:14px 34px;border-radius:99px;font-size:.88rem;font-weight:600;
  letter-spacing:.06em;transition:all .25s;
}
.btn-ghost:hover{background:var(--blue-glow);transform:translateY(-3px)}
.hero-scroll{
  position:absolute;bottom:40px;left:50%;transform:translateX(-50%);
  display:flex;flex-direction:column;align-items:center;gap:8px;
  color:var(--muted);font-size:.7rem;letter-spacing:.14em;text-transform:uppercase;
  animation:fadeUp .8s 1.2s var(--ease) both;
}
.hero-scroll-line{
  width:1px;height:50px;
  background:linear-gradient(to bottom,var(--blue),transparent);
  animation:scrollPulse 2s infinite;
}
@keyframes scrollPulse{0%,100%{transform:scaleY(1);opacity:.6}50%{transform:scaleY(.6);opacity:1}}

/* ============================================================
   ABOUT
   ============================================================ */
#about{background:var(--bg2)}
.about-grid{display:grid;grid-template-columns:1fr 1fr;gap:64px;align-items:center}
.about-avatar{
  position:relative;
  width:100%;max-width:360px;margin:0 auto;
}
.avatar-ring{
  width:100%;aspect-ratio:1;border-radius:50%;
  border:2px solid var(--border-h);
  display:flex;align-items:center;justify-content:center;
  background:linear-gradient(135deg,rgba(79,140,255,.1),rgba(122,179,255,.05));
  position:relative;overflow:hidden;
}
.avatar-ring::before{
  content:'';position:absolute;inset:0;
  background:conic-gradient(var(--blue),transparent,var(--blue2),transparent,var(--blue));
  opacity:.2;animation:rotateSlow 8s linear infinite;
}
@keyframes rotateSlow{to{transform:rotate(360deg)}}
.avatar-inner{
  width:85%;height:85%;border-radius:50%;
  background:linear-gradient(135deg,rgba(79,140,255,.15),rgba(10,10,15,.8));
  display:flex;align-items:center;justify-content:center;
  font-size:5rem;color:var(--blue2);position:relative;z-index:1;
}
.about-floating{
  position:absolute;
  background:rgba(255,255,255,.06);border:1px solid var(--border-h);
  border-radius:var(--r);padding:10px 16px;backdrop-filter:blur(12px);
  font-size:.78rem;font-weight:600;color:var(--white);white-space:nowrap;
  box-shadow:var(--shadow);
}
.about-floating.f1{top:-10px;right:-20px;animation:floatY 3.5s ease-in-out infinite}
.about-floating.f2{bottom:-10px;left:-20px;animation:floatY 4s 1s ease-in-out infinite}
@keyframes floatY{0%,100%{transform:translateY(0)}50%{transform:translateY(-10px)}}
.about-content p{font-size:1.05rem;color:var(--muted);line-height:1.9;margin-bottom:18px}
.about-content p strong{color:var(--white);font-weight:600}
.about-stats{display:flex;gap:32px;margin-top:32px}
.stat-card{
  background:var(--surface);border:1px solid var(--border);
  border-radius:var(--r);padding:20px 24px;text-align:center;
  backdrop-filter:blur(10px);transition:border-color .25s;
  flex:1;
}
.stat-card:hover{border-color:var(--blue)}
.stat-num{font-family:var(--display);font-size:1.8rem;font-weight:700;color:var(--blue);font-style:italic}
.stat-label{font-size:.75rem;color:var(--muted);letter-spacing:.1em;text-transform:uppercase;margin-top:4px}

/* ============================================================
   SKILLS
   ============================================================ */
#skills{background:var(--bg)}
.skills-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:24px}
.skill-card{
  background:linear-gradient(135deg,rgba(255,255,255,.05),rgba(255,255,255,.02));
  border:1px solid var(--border);border-radius:var(--r2);
  padding:28px 32px;backdrop-filter:blur(16px);
  transition:border-color .3s,transform .3s,box-shadow .3s;
  position:relative;overflow:hidden;
}
.skill-card::before{
  content:'';position:absolute;top:0;left:0;right:0;height:1px;
  background:linear-gradient(90deg,transparent,var(--blue),transparent);
  opacity:0;transition:opacity .3s;
}
.skill-card:hover{border-color:var(--border-h);transform:translateY(-4px);box-shadow:0 16px 48px var(--blue-glow)}
.skill-card:hover::before{opacity:1}
.skill-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:16px}
.skill-icon{font-size:1.5rem;margin-right:12px}
.skill-name{font-size:.95rem;font-weight:600;color:var(--white);flex:1}
.skill-pct{font-family:var(--mono);font-size:.85rem;color:var(--blue);font-weight:600}
.skill-track{
  height:4px;background:rgba(255,255,255,.06);
  border-radius:99px;overflow:hidden;
}
.skill-fill{
  height:100%;border-radius:99px;width:0;
  background:linear-gradient(90deg,var(--blue),var(--blue2));
  transition:width 1.4s var(--ease);
  position:relative;
}
.skill-fill::after{
  content:'';position:absolute;right:0;top:50%;transform:translateY(-50%);
  width:8px;height:8px;border-radius:50%;background:var(--blue2);
  box-shadow:0 0 10px var(--blue2);
}

/* ============================================================
   TOOLS
   ============================================================ */
#tools{background:var(--bg2)}
.tools-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:24px}
.tool-card{
  background:linear-gradient(135deg,rgba(255,255,255,.06),rgba(255,255,255,.02));
  border:1px solid var(--border);border-radius:var(--r2);
  padding:40px 24px;text-align:center;
  backdrop-filter:blur(16px);
  transition:all .3s var(--ease);
  position:relative;overflow:hidden;cursor:default;
}
.tool-card::after{
  content:'';position:absolute;inset:0;
  background:radial-gradient(circle at 50% 0%,rgba(79,140,255,.12),transparent 70%);
  opacity:0;transition:opacity .4s;
}
.tool-card:hover{border-color:var(--border-h);transform:translateY(-8px);box-shadow:0 20px 60px var(--blue-glow)}
.tool-card:hover::after{opacity:1}
.tool-icon{
  font-size:2.8rem;margin-bottom:18px;
  display:block;transition:transform .3s;
  position:relative;z-index:1;
}
.tool-card:hover .tool-icon{transform:scale(1.15)}
.tool-name{font-size:1rem;font-weight:600;color:var(--white);margin-bottom:6px;position:relative;z-index:1}
.tool-desc{font-size:.82rem;color:var(--muted);position:relative;z-index:1}

/* ============================================================
   PROJECTS
   ============================================================ */
#projects{background:var(--bg)}
.projects-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(320px,1fr));gap:28px}
.project-card{
  background:linear-gradient(160deg,rgba(255,255,255,.06),rgba(255,255,255,.02));
  border:1px solid var(--border);border-radius:var(--r2);overflow:hidden;
  backdrop-filter:blur(16px);transition:all .35s var(--ease);
  position:relative;
}
.project-card:hover{border-color:var(--border-h);transform:translateY(-6px);box-shadow:0 24px 64px var(--blue-glow)}
.project-img{
  height:200px;
  background:linear-gradient(135deg,rgba(79,140,255,.15) 0%,rgba(10,10,15,.9) 100%);
  display:flex;align-items:center;justify-content:center;
  font-size:4rem;color:var(--blue2);
  position:relative;overflow:hidden;
}
.project-img::before{
  content:'';position:absolute;inset:0;
  background:repeating-linear-gradient(45deg,rgba(79,140,255,.04) 0px,rgba(79,140,255,.04) 1px,transparent 1px,transparent 12px);
}
.project-img-label{
  position:absolute;bottom:14px;right:16px;
  font-family:var(--mono);font-size:.65rem;letter-spacing:.12em;
  color:var(--muted);text-transform:uppercase;
}
.project-body{padding:28px 28px 32px}
.project-tag{
  display:inline-block;
  font-family:var(--mono);font-size:.65rem;letter-spacing:.14em;
  color:var(--blue);text-transform:uppercase;margin-bottom:10px;
}
.project-title{font-size:1.15rem;font-weight:700;color:var(--white);margin-bottom:10px;font-family:var(--display);font-style:italic}
.project-desc{font-size:.88rem;color:var(--muted);line-height:1.8;margin-bottom:22px}
.project-link{
  display:inline-flex;align-items:center;gap:8px;
  font-size:.82rem;font-weight:600;color:var(--blue2);
  transition:gap .25s;letter-spacing:.04em;
}
.project-link:hover{gap:14px}
.project-link i{font-size:.7rem}

/* ============================================================
   EDUCATION
   ============================================================ */
#education{background:var(--bg2)}
.timeline{
  position:relative;max-width:720px;margin:0 auto;
  padding-left:48px;
}
.timeline::before{
  content:'';position:absolute;left:18px;top:8px;bottom:8px;
  width:1px;background:linear-gradient(to bottom,var(--blue),transparent);
}
.timeline-item{
  position:relative;margin-bottom:48px;
}
.timeline-item:last-child{margin-bottom:0}
.tl-dot{
  position:absolute;left:-38px;top:4px;
  width:14px;height:14px;border-radius:50%;
  background:var(--bg);border:2px solid var(--blue);
  box-shadow:0 0 16px var(--blue);
  transition:box-shadow .3s;
}
.timeline-item:hover .tl-dot{box-shadow:0 0 28px var(--blue2)}
.tl-card{
  background:linear-gradient(135deg,rgba(255,255,255,.05),rgba(255,255,255,.02));
  border:1px solid var(--border);border-radius:var(--r2);
  padding:28px 32px;backdrop-filter:blur(16px);
  transition:border-color .3s,box-shadow .3s;
}
.timeline-item:hover .tl-card{border-color:var(--border-h);box-shadow:0 8px 40px var(--blue-glow)}
.tl-date{
  font-family:var(--mono);font-size:.72rem;color:var(--blue);
  letter-spacing:.14em;text-transform:uppercase;margin-bottom:10px;
}
.tl-title{font-family:var(--display);font-style:italic;font-size:1.25rem;font-weight:700;color:var(--white);margin-bottom:6px}
.tl-sub{font-size:.88rem;color:var(--muted);margin-bottom:18px}
.tl-list{list-style:none;display:flex;flex-direction:column;gap:10px}
.tl-list li{
  font-size:.88rem;color:var(--muted);
  display:flex;align-items:flex-start;gap:10px;
}
.tl-list li::before{
  content:'→';color:var(--blue);font-size:.8rem;flex-shrink:0;margin-top:2px;
}

/* ============================================================
   CONTACT
   ============================================================ */
#contact{background:var(--bg)}
.contact-grid{display:grid;grid-template-columns:1fr 1.4fr;gap:64px;align-items:start}
.contact-info-text{
  font-size:1rem;color:var(--muted);line-height:1.9;margin-bottom:32px;
}
.social-links{display:flex;gap:14px;flex-wrap:wrap}
.social-btn{
  display:inline-flex;align-items:center;gap:10px;
  border:1px solid var(--border);border-radius:99px;
  padding:11px 22px;font-size:.83rem;color:var(--text);font-weight:500;
  transition:all .25s;backdrop-filter:blur(10px);
}
.social-btn:hover{border-color:var(--blue);color:var(--blue2);transform:translateY(-2px);background:var(--blue-glow)}
.contact-form{
  background:linear-gradient(135deg,rgba(255,255,255,.05),rgba(255,255,255,.02));
  border:1px solid var(--border);border-radius:var(--r2);
  padding:40px 40px;backdrop-filter:blur(20px);
}
.form-group{margin-bottom:22px}
.form-label{
  display:block;font-size:.78rem;letter-spacing:.1em;text-transform:uppercase;
  color:var(--muted);margin-bottom:8px;font-weight:600;
}
.form-input, .form-textarea{
  width:100%;background:rgba(255,255,255,.04);
  border:1px solid var(--border);border-radius:var(--r);
  padding:14px 18px;color:var(--white);font-family:var(--body);font-size:.92rem;
  outline:none;transition:border-color .25s,box-shadow .25s;
  resize:none;
}
.form-input:focus,.form-textarea:focus{
  border-color:var(--blue);
  box-shadow:0 0 0 3px rgba(79,140,255,.12);
}
.form-input::placeholder,.form-textarea::placeholder{color:rgba(136,146,164,.5)}
.form-textarea{min-height:130px}
.form-submit{
  width:100%;background:var(--blue);color:#fff;
  border-radius:99px;padding:15px;font-size:.9rem;font-weight:700;
  letter-spacing:.06em;transition:all .25s;
}
.form-submit:hover{background:var(--blue2);transform:translateY(-2px);box-shadow:0 10px 30px rgba(79,140,255,.4)}
.form-success{
  display:none;text-align:center;padding:20px;
  color:var(--blue2);font-size:.95rem;font-weight:600;
}

/* ============================================================
   FOOTER
   ============================================================ */
footer{
  background:var(--bg2);
  border-top:1px solid var(--border);
  padding:32px 5%;
  display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:16px;
}
.footer-logo{font-family:var(--display);font-style:italic;color:var(--white);font-size:1.1rem}
.footer-logo span{color:var(--blue)}
.footer-copy{font-size:.8rem;color:var(--muted);text-align:center}
.footer-heart{color:#e05580}

/* ============================================================
   BACK TO TOP
   ============================================================ */
#back-top{
  position:fixed;bottom:32px;right:32px;z-index:500;
  width:46px;height:46px;border-radius:50%;
  background:var(--blue);color:#fff;
  display:flex;align-items:center;justify-content:center;
  font-size:.9rem;box-shadow:0 8px 24px rgba(79,140,255,.4);
  transition:all .3s;
  opacity:0;pointer-events:none;transform:translateY(16px);
}
#back-top.show{opacity:1;pointer-events:all;transform:translateY(0)}
#back-top:hover{background:var(--blue2);transform:translateY(-4px)}

/* ============================================================
   SCROLL REVEAL
   ============================================================ */
.reveal{opacity:0;transform:translateY(32px);transition:opacity .7s var(--ease),transform .7s var(--ease)}
.reveal.visible{opacity:1;transform:none}
.reveal-left{opacity:0;transform:translateX(-40px);transition:opacity .8s var(--ease),transform .8s var(--ease)}
.reveal-left.visible{opacity:1;transform:none}
.reveal-right{opacity:0;transform:translateX(40px);transition:opacity .8s var(--ease),transform .8s var(--ease)}
.reveal-right.visible{opacity:1;transform:none}
@keyframes fadeUp{from{opacity:0;transform:translateY(24px)}to{opacity:1;transform:none}}

/* ============================================================
   SCROLL POPUP TOAST
   ============================================================ */
.scroll-toast{
  position:fixed;bottom:80px;left:50%;transform:translateX(-50%) translateY(20px);
  background:rgba(10,10,15,.9);border:1px solid var(--border-h);
  border-radius:99px;padding:10px 24px;
  font-size:.82rem;color:var(--blue2);font-weight:600;letter-spacing:.06em;
  backdrop-filter:blur(16px);z-index:700;
  opacity:0;pointer-events:none;
  transition:all .4s var(--ease);white-space:nowrap;
}
.scroll-toast.show{opacity:1;transform:translateX(-50%) translateY(0)}

/* ============================================================
   RESPONSIVE
   ============================================================ */
@media(max-width:900px){
  .about-grid{grid-template-columns:1fr}
  .about-avatar{max-width:260px}
  .contact-grid{grid-template-columns:1fr}
}
@media(max-width:768px){
  .nav-links{display:none}
  .nav-toggle{display:flex}
  section{padding:80px 5%}
  .about-stats{gap:16px}
  .contact-form{padding:28px 22px}
  footer{flex-direction:column;text-align:center}
  .about-floating.f1{right:-10px}
  .about-floating.f2{left:-10px}
}
@media(max-width:480px){
  .hero-ctas{flex-direction:column;align-items:center}
  .btn-primary,.btn-ghost{width:80%;text-align:center}
  .about-stats{flex-direction:column}
  .tools-grid{grid-template-columns:1fr 1fr}
}
@media(prefers-reduced-motion:reduce){
  *{animation-duration:.01ms!important;transition-duration:.01ms!important}
}
</style>
</head>
<body>

<!-- LOADER -->
<div id="loader">
  <div class="loader-logo">Hania <span>Batool</span></div>
  <div class="loader-bar"><div class="loader-fill"></div></div>
</div>

<!-- WELCOME POPUP -->
<div id="welcome-popup">
  <div class="popup-card">
    <span class="popup-emoji">✨</span>
    <span class="popup-x" onclick="closePopup()"><i class="fas fa-times"></i></span>
    <h2>Welcome to My Portfolio</h2>
    <p>Hi there! I'm Hania Batool — a B.Ed (Hons) student & aspiring Front-End Developer. Thanks for stopping by!</p>
    <button class="popup-close" onclick="closePopup()">Explore Portfolio</button>
  </div>
</div>

<!-- SCROLL TOAST -->
<div class="scroll-toast" id="scroll-toast"></div>

<!-- CANVAS BACKGROUND -->
<canvas id="bg-canvas"></canvas>

<!-- NAVBAR -->
<nav id="navbar">
  <a href="#hero" class="nav-logo">Hania <span>Batool</span></a>
  <ul class="nav-links">
    <li><a href="#hero">Home</a></li>
    <li><a href="#about">About</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#tools">Tools</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#education">Education</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <button class="nav-toggle" id="nav-toggle" aria-label="Menu">
    <span></span><span></span><span></span>
  </button>
</nav>
<nav class="mobile-menu" id="mobile-menu">
  <a href="#hero" onclick="closeMenu()">Home</a>
  <a href="#about" onclick="closeMenu()">About</a>
  <a href="#skills" onclick="closeMenu()">Skills</a>
  <a href="#tools" onclick="closeMenu()">Tools</a>
  <a href="#projects" onclick="closeMenu()">Projects</a>
  <a href="#education" onclick="closeMenu()">Education</a>
  <a href="#contact" onclick="closeMenu()">Contact</a>
</nav>

<!-- ===================== HERO ===================== -->
<section id="hero">
  <div class="hero-badge"><span class="dot"></span>Available for Projects</div>
  <h1 class="hero-h1">Hi, I'm <span class="name-blue">Hania Batool</span></h1>
  <p class="hero-sub">B.Ed (Hons) Student &nbsp;·&nbsp; Front-End Developer &nbsp;·&nbsp; Web Designer</p>
  <div class="hero-type-wrap">
    <span class="hero-type-prefix">I am a</span>
    <span id="typed-text"></span><span class="cursor"></span>
  </div>
  <p class="hero-desc">Passionate about crafting beautiful, responsive, and user-friendly web experiences from scratch — one pixel at a time.</p>
  <div class="hero-ctas">
    <a href="#projects" class="btn-primary">View My Work</a>
    <a href="#contact" class="btn-ghost">Get in Touch</a>
  </div>
  <div class="hero-scroll">
    <div class="hero-scroll-line"></div>
    <span>Scroll</span>
  </div>
</section>

<!-- ===================== ABOUT ===================== -->
<section id="about">
  <div class="about-grid">
    <div class="about-avatar reveal-left">
      <div class="avatar-ring">
        <div class="avatar-inner"><i class="fas fa-user"></i></div>
      </div>
      <div class="about-floating f1">🎓 B.Ed (Hons) Student</div>
      <div class="about-floating f2">💻 Front-End Developer</div>
    </div>
    <div class="about-content reveal-right">
      <span class="section-label">// Who I Am</span>
      <h2 class="section-title">About Me</h2>
      <div class="section-line"></div>
      <p>I am <strong>Hania Batool</strong>, a <strong>B.Ed (Hons) student</strong> and aspiring Front-End Developer. I enjoy creating modern, responsive, and user-friendly websites using <strong>HTML, CSS, and JavaScript</strong>.</p>
      <p>I am passionate about web design and continuously improving my development skills — turning ideas into clean, functional, and visually compelling digital experiences.</p>
      <div class="about-stats">
        <div class="stat-card">
          <div class="stat-num">2+</div>
          <div class="stat-label">Projects Done</div>
        </div>
        <div class="stat-card">
          <div class="stat-num">3+</div>
          <div class="stat-label">Tools Mastered</div>
        </div>
        <div class="stat-card">
          <div class="stat-num">100%</div>
          <div class="stat-label">Dedication</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ===================== SKILLS ===================== -->
<section id="skills">
  <div style="text-align:center;margin-bottom:56px" class="reveal">
    <span class="section-label">// What I Know</span>
    <h2 class="section-title">My Skills</h2>
    <div class="section-line" style="margin:16px auto 0"></div>
  </div>
  <div class="skills-grid">
    <div class="skill-card reveal" data-delay="0">
      <div class="skill-header">
        <span class="skill-icon">🌐</span>
        <span class="skill-name">HTML5</span>
        <span class="skill-pct">90%</span>
      </div>
      <div class="skill-track"><div class="skill-fill" data-pct="90"></div></div>
    </div>
    <div class="skill-card reveal" data-delay="80">
      <div class="skill-header">
        <span class="skill-icon">🎨</span>
        <span class="skill-name">CSS3</span>
        <span class="skill-pct">85%</span>
      </div>
      <div class="skill-track"><div class="skill-fill" data-pct="85"></div></div>
    </div>
    <div class="skill-card reveal" data-delay="160">
      <div class="skill-header">
        <span class="skill-icon">⚡</span>
        <span class="skill-name">JavaScript</span>
        <span class="skill-pct">70%</span>
      </div>
      <div class="skill-track"><div class="skill-fill" data-pct="70"></div></div>
    </div>
    <div class="skill-card reveal" data-delay="240">
      <div class="skill-header">
        <span class="skill-icon">📱</span>
        <span class="skill-name">Responsive Web Design</span>
        <span class="skill-pct">88%</span>
      </div>
      <div class="skill-track"><div class="skill-fill" data-pct="88"></div></div>
    </div>
    <div class="skill-card reveal" data-delay="320">
      <div class="skill-header">
        <span class="skill-icon">💻</span>
        <span class="skill-name">Front-End Development</span>
        <span class="skill-pct">80%</span>
      </div>
      <div class="skill-track"><div class="skill-fill" data-pct="80"></div></div>
    </div>
    <div class="skill-card reveal" data-delay="400">
      <div class="skill-header">
        <span class="skill-icon">📊</span>
        <span class="skill-name">Microsoft Excel</span>
        <span class="skill-pct">75%</span>
      </div>
      <div class="skill-track"><div class="skill-fill" data-pct="75"></div></div>
    </div>
  </div>
</section>

<!-- ===================== TOOLS ===================== -->
<section id="tools">
  <div style="text-align:center;margin-bottom:56px" class="reveal">
    <span class="section-label">// My Arsenal</span>
    <h2 class="section-title">Tools I Use</h2>
    <div class="section-line" style="margin:16px auto 0"></div>
  </div>
  <div class="tools-grid">
    <div class="tool-card reveal" data-delay="0">
      <span class="tool-icon" style="color:#4ec9b0"><i class="fas fa-code"></i></span>
      <div class="tool-name">VS Code</div>
      <div class="tool-desc">My primary code editor for building beautiful web interfaces with speed and precision.</div>
    </div>
    <div class="tool-card reveal" data-delay="100">
      <span class="tool-icon" style="color:#f1f1f1"><i class="fab fa-github"></i></span>
      <div class="tool-name">GitHub</div>
      <div class="tool-desc">Version control and collaboration platform to manage and showcase my projects.</div>
    </div>
    <div class="tool-card reveal" data-delay="200">
      <span class="tool-icon" style="color:#7b68ee"><i class="fas fa-palette"></i></span>
      <div class="tool-name">Canva</div>
      <div class="tool-desc">Design tool for creating stunning graphics, presentations, and visual assets.</div>
    </div>
    <div class="tool-card reveal" data-delay="300">
      <span class="tool-icon" style="color:#1d6f42"><i class="fas fa-table"></i></span>
      <div class="tool-name">Microsoft Excel</div>
      <div class="tool-desc">Powerful spreadsheet tool for data management, analysis, and organization.</div>
    </div>
  </div>
</section>

<!-- ===================== PROJECTS ===================== -->
<section id="projects">
  <div style="text-align:center;margin-bottom:56px" class="reveal">
    <span class="section-label">// My Work</span>
    <h2 class="section-title">Projects</h2>
    <div class="section-line" style="margin:16px auto 0"></div>
  </div>
  <div class="projects-grid">
    <div class="project-card reveal" data-delay="0">
      <div class="project-img">
        <i class="fas fa-sign-in-alt"></i>
        <span class="project-img-label">HTML · CSS</span>
      </div>
      <div class="project-body">
        <span class="project-tag">Web Design</span>
        <h3 class="project-title">Responsive Login Page</h3>
        <p class="project-desc">A modern login page built using HTML and CSS with responsive design and professional styling. Includes smooth transitions and clean form layout.</p>
        <a href="#" class="project-link">View Project <i class="fas fa-arrow-right"></i></a>
      </div>
    </div>
    <div class="project-card reveal" data-delay="120">
      <div class="project-img">
        <i class="fas fa-briefcase"></i>
        <span class="project-img-label">HTML · CSS · JS</span>
      </div>
      <div class="project-body">
        <span class="project-tag">Portfolio</span>
        <h3 class="project-title">Personal Portfolio Website</h3>
        <p class="project-desc">A professional portfolio website showcasing my skills, education, tools, and projects with modern animations, glassmorphism effects, and a fully responsive layout.</p>
        <a href="#" class="project-link">View Project <i class="fas fa-arrow-right"></i></a>
      </div>
    </div>
  </div>
</section>

<!-- ===================== EDUCATION ===================== -->
<section id="education">
  <div style="text-align:center;margin-bottom:64px" class="reveal">
    <span class="section-label">// My Journey</span>
    <h2 class="section-title">Education</h2>
    <div class="section-line" style="margin:16px auto 0"></div>
  </div>
  <div class="timeline">
    <div class="timeline-item reveal">
      <div class="tl-dot"></div>
      <div class="tl-card">
        <div class="tl-date">Currently Pursuing</div>
        <div class="tl-title">B.Ed (Hons) Program</div>
        <div class="tl-sub">Bachelor of Education (Honours) &nbsp;·&nbsp; In Progress</div>
        <ul class="tl-list">
          <li>Pursuing formal education while simultaneously developing technical web development skills.</li>
          <li>Focused on Front-End Development using HTML5, CSS3, and JavaScript from the ground up.</li>
          <li>Practising Web Design principles: layout, typography, color theory, and UX fundamentals.</li>
          <li>Building real-world Responsive Websites that adapt seamlessly across all screen sizes.</li>
          <li>Continuously learning through self-study, projects, and hands-on coding practice.</li>
        </ul>
      </div>
    </div>
  </div>
</section>

<!-- ===================== CONTACT ===================== -->
<section id="contact">
  <div style="margin-bottom:56px" class="reveal">
    <span class="section-label">// Let's Talk</span>
    <h2 class="section-title">Get In Touch</h2>
    <div class="section-line"></div>
  </div>
  <div class="contact-grid">
    <div class="reveal-left">
      <p class="contact-info-text">Have a project in mind, a question, or just want to say hi? I'd love to hear from you. Fill out the form or reach out through my social channels!</p>
      <div class="social-links">
        <a href="mailto:hania@example.com" class="social-btn"><i class="fas fa-envelope"></i> Email Me</a>
        <a href="https://github.com" target="_blank" class="social-btn"><i class="fab fa-github"></i> GitHub</a>
      </div>
    </div>
    <div class="contact-form reveal-right">
      <div class="form-group">
        <label class="form-label">Your Name</label>
        <input type="text" class="form-input" placeholder="e.g. Sara Ahmed" id="cf-name"/>
      </div>
      <div class="form-group">
        <label class="form-label">Email Address</label>
        <input type="email" class="form-input" placeholder="e.g. sara@example.com" id="cf-email"/>
      </div>
      <div class="form-group">
        <label class="form-label">Message</label>
        <textarea class="form-textarea" placeholder="Write your message here…" id="cf-msg"></textarea>
      </div>
      <button class="form-submit" onclick="submitForm()">Send Message &nbsp;<i class="fas fa-paper-plane"></i></button>
      <div class="form-success" id="form-success">✅ Message sent! I'll get back to you soon.</div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">Hania <span>Batool</span></div>
  <p class="footer-copy">© 2025 Hania Batool. Crafted with <span class="footer-heart">♥</span> & lots of CSS.</p>
  <div class="social-links" style="flex-shrink:0">
    <a href="mailto:hania@example.com" class="social-btn" style="padding:8px 18px;font-size:.78rem"><i class="fas fa-envelope"></i></a>
    <a href="https://github.com" target="_blank" class="social-btn" style="padding:8px 18px;font-size:.78rem"><i class="fab fa-github"></i></a>
  </div>
</footer>

<!-- BACK TO TOP -->
<button id="back-top" onclick="window.scrollTo({top:0,behavior:'smooth'})" aria-label="Back to top">
  <i class="fas fa-chevron-up"></i>
</button>

<!-- ===================== SCRIPTS ===================== -->
<script>
/* ---------- LOADER ---------- */
window.addEventListener('load',()=>{
  setTimeout(()=>{
    document.getElementById('loader').classList.add('hidden');
    setTimeout(()=>document.getElementById('welcome-popup').classList.add('show'),400);
  },1800);
});
function closePopup(){document.getElementById('welcome-popup').classList.remove('show')}

/* ---------- PARTICLE CANVAS ---------- */
(function(){
  const canvas=document.getElementById('bg-canvas');
  const ctx=canvas.getContext('2d');
  let W,H,pts=[];
  const N=80;
  function resize(){W=canvas.width=window.innerWidth;H=canvas.height=window.innerHeight}
  window.addEventListener('resize',()=>{resize();init()});
  resize();
  function init(){
    pts=[];
    for(let i=0;i<N;i++){
      pts.push({
        x:Math.random()*W,y:Math.random()*H,
        vx:(Math.random()-.5)*.3,vy:(Math.random()-.5)*.3,
        r:Math.random()*1.4+.4,o:Math.random()*.5+.2
      });
    }
  }
  init();
  function draw(){
    ctx.clearRect(0,0,W,H);
    for(let i=0;i<pts.length;i++){
      let p=pts[i];
      p.x+=p.vx;p.y+=p.vy;
      if(p.x<0)p.x=W;if(p.x>W)p.x=0;
      if(p.y<0)p.y=H;if(p.y>H)p.y=0;
      ctx.beginPath();
      ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
      ctx.fillStyle=`rgba(79,140,255,${p.o})`;
      ctx.fill();
      for(let j=i+1;j<pts.length;j++){
        let q=pts[j];
        let d=Math.hypot(p.x-q.x,p.y-q.y);
        if(d<130){
          ctx.beginPath();
          ctx.moveTo(p.x,p.y);ctx.lineTo(q.x,q.y);
          ctx.strokeStyle=`rgba(79,140,255,${.08*(1-d/130)})`;
          ctx.lineWidth=.6;ctx.stroke();
        }
      }
    }
    requestAnimationFrame(draw);
  }
  draw();
})();

/* ---------- NAVBAR ---------- */
const navbar=document.getElementById('navbar');
window.addEventListener('scroll',()=>{
  navbar.classList.toggle('scrolled',window.scrollY>40);
  document.getElementById('back-top').classList.toggle('show',window.scrollY>400);
});
const toggle=document.getElementById('nav-toggle');
const mobileMenu=document.getElementById('mobile-menu');
toggle.addEventListener('click',()=>{
  toggle.classList.toggle('open');
  mobileMenu.classList.toggle('open');
});
function closeMenu(){toggle.classList.remove('open');mobileMenu.classList.remove('open')}

/* ---------- TYPING EFFECT ---------- */
const words=['Front-End Developer','Web Designer','Responsive Website Creator'];
let wi=0,ci=0,del=false;
function type(){
  const w=words[wi];
  const el=document.getElementById('typed-text');
  if(!del){
    el.textContent=w.slice(0,++ci);
    if(ci===w.length){del=true;setTimeout(type,1600);return;}
  }else{
    el.textContent=w.slice(0,--ci);
    if(ci===0){del=false;wi=(wi+1)%words.length;}
  }
  setTimeout(type,del?45:80);
}
setTimeout(type,1000);

/* ---------- SCROLL REVEAL ---------- */
const reveals=document.querySelectorAll('.reveal,.reveal-left,.reveal-right');
const skillFills=document.querySelectorAll('.skill-fill');
let skillsAnimated=false;
const io=new IntersectionObserver((entries)=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      const delay=parseInt(e.target.dataset.delay||0);
      setTimeout(()=>e.target.classList.add('visible'),delay);
      io.unobserve(e.target);
    }
  });
},{threshold:.12});
reveals.forEach(r=>io.observe(r));

const skillsIo=new IntersectionObserver((entries)=>{
  if(entries[0].isIntersecting&&!skillsAnimated){
    skillsAnimated=true;
    skillFills.forEach(f=>{
      setTimeout(()=>{f.style.width=f.dataset.pct+'%'},200);
    });
  }
},{threshold:.2});
const skillsSection=document.getElementById('skills');
if(skillsSection)skillsIo.observe(skillsSection);

/* ---------- SCROLL TOASTS ---------- */
const toasts=[
  {id:'about',msg:'👩‍💻 Learn about Hania Batool'},
  {id:'skills',msg:'⚡ Explore her skills'},
  {id:'projects',msg:'🚀 Check out the projects'},
  {id:'contact',msg:'📬 Let\'s connect!'},
];
const shownToasts=new Set();
const toastEl=document.getElementById('scroll-toast');
let toastTimer;
const toastIo=new IntersectionObserver((entries)=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      const t=toasts.find(x=>x.id===e.target.id);
      if(t&&!shownToasts.has(t.id)){
        shownToasts.add(t.id);
        clearTimeout(toastTimer);
        toastEl.textContent=t.msg;
        toastEl.classList.add('show');
        toastTimer=setTimeout(()=>toastEl.classList.remove('show'),2800);
      }
    }
  });
},{threshold:.3});
['about','skills','projects','contact'].forEach(id=>{
  const s=document.getElementById(id);
  if(s)toastIo.observe(s);
});

/* ---------- CONTACT FORM ---------- */
function submitForm(){
  const name=document.getElementById('cf-name').value.trim();
  const email=document.getElementById('cf-email').value.trim();
  const msg=document.getElementById('cf-msg').value.trim();
  if(!name||!email||!msg){alert('Please fill in all fields.');return;}
  const btn=document.querySelector('.form-submit');
  btn.textContent='Sending…';btn.disabled=true;
  setTimeout(()=>{
    btn.style.display='none';
    document.getElementById('form-success').style.display='block';
    document.getElementById('cf-name').value='';
    document.getElementById('cf-email').value='';
    document.getElementById('cf-msg').value='';
  },1200);
}
</script>
</body>
</html>
