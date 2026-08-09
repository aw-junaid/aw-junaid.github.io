<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>awjunaid - DNSdumpster Reconnaissance (Kali Linux)</title>
<link
  href="https://fonts.googleapis.com/css2?family=League+Spartan:wght@700;800&family=Poppins:wght@300;400;600&family=Inter:wght@300;400;500;600;700;800;900&display=swap"
  rel="stylesheet"
/>
<link
  rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"
/>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}

:root{
  --bg-primary:#ffffff;
  --bg-secondary:#f5f5f5;
  --text-primary:#000000;
  --text-secondary:#666666;
  --border-color:#000000;
  --border-light:#e0e0e0;
  --input-bg:#ffffff;
  --hover-bg:#000000;
  --hover-text:#ffffff;
  --code-bg:#f4f4f4;
  --term-bg:#f4f4f4;
  --term-text:#000000;

  --font-header:'League Spartan',sans-serif;
  --font-body:'Poppins',sans-serif;
  --mono:'Fira Code','JetBrains Mono',monospace;
  --r:10px;--rs:6px;

  /* the ONLY non-monochrome colors in the whole page: risk levels + tip/warn */
  --grn:#3fb950;--ylw:#e3b341;--org:#ffa657;--red:#f85149;--acc:#2e6fd9;
}
body.dark-mode{
  --bg-primary:#000000;
  --bg-secondary:#111111;
  --text-primary:#ffffff;
  --text-secondary:#999999;
  --border-color:#ffffff;
  --border-light:#2a2a2a;
  --input-bg:#0a0a0a;
  --hover-bg:#ffffff;
  --hover-text:#000000;
  --code-bg:#141414;
  --term-bg:#0a0a0a;
  --term-text:#e5e5e5;
}

html{scroll-behavior:smooth}
body{
  background-color:var(--bg-primary);
  color:var(--text-primary);
  font-family:var(--font-body);
  min-height:100vh;
  display:flex;flex-direction:column;
  line-height:1.6;
  transition:background-color .25s,color .25s;
}
::-webkit-scrollbar{width:5px;height:5px}
::-webkit-scrollbar-track{background:var(--bg-primary)}
::-webkit-scrollbar-thumb{background:var(--border-light);border-radius:3px}
a{color:inherit;text-decoration:none;transition:all .2s ease}
.container{max-width:1200px;margin:0 auto;width:100%;padding:0 20px}

/* ── HEADER ── */
header{
  border-bottom:1px solid var(--border-color);
  padding:12px 0;width:100%;z-index:1000;position:sticky;top:0;
  background-color:var(--bg-primary);
  transition:all .3s ease;
}
header .container{display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:15px}
.logo a{
  font-family:var(--font-header);
  font-size:clamp(18px,5vw,24px);
  font-weight:800;text-transform:lowercase;letter-spacing:-1px;
  color:var(--text-primary);
}
.logo a:hover{opacity:.7}
.header-right{display:flex;align-items:center;gap:clamp(8px,1.5vw,15px);flex-wrap:wrap}
nav.main-nav{display:flex;gap:clamp(10px,2vw,15px);font-weight:600;font-size:clamp(12px,2vw,14px);flex-wrap:wrap}
nav.main-nav a{position:relative;padding-bottom:2px;color:var(--text-primary)}
nav.main-nav a:hover{opacity:.7}
.dropdown{position:relative;display:inline-block}
.dropdown-content{
  display:none;position:absolute;background-color:var(--bg-primary);min-width:180px;
  border:1px solid var(--border-color);z-index:100;top:100%;left:0;
}
.dropdown-content a{padding:10px 14px;display:block;border-bottom:1px solid var(--border-color);font-size:13px}
.dropdown-content a:last-child{border-bottom:none}
.dropdown-content a:hover{background-color:var(--hover-bg);color:var(--hover-text);padding-left:16px}
.dropdown:hover .dropdown-content{display:block}
.social-icons{display:flex;gap:4px;font-size:16px;align-items:center}
.social-icons a{
  display:inline-flex;align-items:center;justify-content:center;width:24px;height:24px;
  padding:0;margin:0;line-height:1;color:var(--text-primary);
}
.social-icons a:hover{transform:translateY(-2px);opacity:.7}
.theme-switcher{
  background:var(--bg-primary);border:1px solid var(--border-color);color:var(--text-primary);
  padding:6px 10px;cursor:pointer;font-family:var(--font-header);font-weight:700;
  text-transform:uppercase;font-size:clamp(8px,1.5vw,10px);transition:all .2s;border-radius:2px;white-space:nowrap;
}
.theme-switcher:hover{background-color:var(--hover-bg);color:var(--hover-text)}

main{flex:1;width:100%}

/* ── HERO / TOOL PANEL ── */
.hero{position:relative;z-index:10;max-width:860px;margin:2.5rem auto 2rem;padding:0 1.2rem;text-align:center}
.chip{
  display:inline-flex;align-items:center;gap:.4rem;font-size:.68rem;letter-spacing:1.4px;text-transform:uppercase;
  color:var(--text-primary);background:var(--code-bg);border:1px solid var(--border-color);
  padding:.26rem .85rem;border-radius:2rem;margin-bottom:.9rem;font-weight:700;
}
.hero h2{font-size:2rem;font-weight:800;color:var(--text-primary);line-height:1.2;font-family:var(--font-header)}
.hero p{color:var(--text-secondary);margin-top:.55rem;font-size:.88rem;max-width:640px;margin-inline:auto;line-height:1.6}
.panel{
  margin-top:1.6rem;background:var(--bg-primary);border:1px solid var(--border-color);border-radius:14px;
  padding:1.2rem 1.3rem;
}
.irow{display:flex;gap:.45rem;flex-wrap:wrap}
.ipfx{
  display:flex;align-items:center;padding:.68rem .85rem;background:var(--code-bg);
  border:1px solid var(--border-color);border-radius:var(--rs);color:var(--text-secondary);
  font-family:var(--mono);font-size:.8rem;white-space:nowrap;
}
#targetInput{
  flex:1;min-width:160px;padding:.7rem .95rem;border:1px solid var(--border-color);border-radius:var(--rs);
  background:var(--input-bg);color:var(--text-primary);font-size:.93rem;outline:none;font-family:var(--mono);
  transition:box-shadow .18s;
}
#targetInput:focus{box-shadow:0 0 0 2px var(--text-primary)}
#targetInput::placeholder{color:var(--text-secondary)}
#generateBtn{
  padding:.7rem 1.5rem;border:1px solid var(--border-color);border-radius:var(--rs);
  background:var(--text-primary);color:var(--bg-primary);font-size:.88rem;font-weight:700;
  cursor:pointer;white-space:nowrap;transition:opacity .18s,transform .1s;font-family:var(--font-body);
}
#generateBtn:hover{opacity:.8}
#generateBtn:active{transform:scale(.97)}
.errbox{
  display:none;margin-top:.55rem;background:transparent;border:1px solid var(--red);
  border-radius:var(--rs);padding:.42rem .65rem;font-size:.78rem;color:var(--red);
}
.statsbar{display:none;gap:1rem;margin-top:.75rem;flex-wrap:wrap}
.sc{display:flex;align-items:center;gap:.3rem;font-size:.73rem;color:var(--text-secondary)}
.sc strong{color:var(--text-primary)}
.sdot{width:6px;height:6px;border-radius:50%;background:var(--text-primary)}

#toolbar{
  display:none;position:relative;z-index:500;max-width:1360px;margin:.7rem auto .3rem;
  padding:0 1.2rem;gap:.4rem;flex-wrap:wrap;align-items:center;
}
.vbtn{
  padding:.3rem .75rem;font-size:.73rem;border:1px solid var(--border-color);border-radius:var(--rs);
  background:var(--bg-primary);color:var(--text-secondary);cursor:pointer;transition:all .14s;font-family:var(--font-body);
}
.vbtn.on{background:var(--text-primary);color:var(--bg-primary);font-weight:700}
.vbtn:hover{opacity:.8}
.srch{position:relative;margin-left:auto}
#searchInput{
  display:block;width:260px;padding:.4rem .9rem .4rem 2.1rem;background:var(--input-bg);
  border:1px solid var(--border-color);border-radius:var(--rs);color:var(--text-primary);font-size:.8rem;
  font-family:inherit;outline:none;
}
#searchInput::placeholder{color:var(--text-secondary)}
.sico{position:absolute;left:.65rem;top:50%;transform:translateY(-50%);color:var(--text-secondary);font-size:.75rem;pointer-events:none}

#pills{display:none;max-width:1360px;margin:0 auto .55rem;padding:0 1.2rem;gap:.35rem;flex-wrap:wrap}
.pill{
  padding:.26rem .72rem;border-radius:2rem;border:1px solid var(--border-color);background:var(--bg-primary);
  color:var(--text-primary);font-size:.72rem;cursor:pointer;transition:all .14s;user-select:none;
}
.pill:hover{opacity:.7}
.pill.on{background:var(--text-primary);color:var(--bg-primary);font-weight:700}

#mainLayout{display:none;max-width:1360px;margin:0 auto 4rem;padding:0 1.2rem;gap:1.1rem;grid-template-columns:215px 1fr}
@media(max-width:820px){#mainLayout{grid-template-columns:1fr}}
#sidebar{position:sticky;top:72px;height:fit-content;display:flex;flex-direction:column;gap:.2rem}
@media(max-width:820px){#sidebar{display:none}}
.sbt{font-size:.61rem;letter-spacing:1.2px;text-transform:uppercase;color:var(--text-secondary);padding:.3rem .48rem;margin-top:.3rem}
.sbtn{
  display:flex;align-items:center;gap:.45rem;padding:.38rem .55rem;border-radius:var(--rs);
  border:none;background:none;color:var(--text-secondary);font-size:.77rem;cursor:pointer;width:100%;text-align:left;
  transition:all .14s;border-left:2px solid transparent;font-family:var(--font-body);
}
.sbtn:hover{color:var(--text-primary)}
.sbtn.on{background:var(--code-bg);color:var(--text-primary);border-left-color:var(--text-primary);font-weight:600}
.sblbl{flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.sbcnt{
  font-size:.61rem;padding:.06rem .35rem;border-radius:2rem;background:var(--bg-primary);
  border:1px solid var(--border-light);color:var(--text-secondary);flex-shrink:0;
}
.sbtn.on .sbcnt{border-color:var(--border-color);color:var(--text-primary)}
.sbsep{height:1px;background:var(--border-light);margin:.28rem 0}

#content{position:relative;z-index:1}
.sec{margin-bottom:1.8rem}
.sechdr{display:flex;align-items:center;gap:.6rem;margin-bottom:.75rem;padding-bottom:.65rem;border-bottom:1px solid var(--border-color)}
.sectitle{font-size:.92rem;font-weight:700;color:var(--text-primary);font-family:var(--font-header)}
.secsub{font-size:.72rem;color:var(--text-secondary);margin-top:1px;line-height:1.5}
.seccnt{
  margin-left:auto;font-size:.65rem;padding:.15rem .48rem;border-radius:2rem;
  background:var(--code-bg);border:1px solid var(--border-light);color:var(--text-secondary);white-space:nowrap;flex-shrink:0;
}

.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(430px,1fr));gap:.85rem}
@media(max-width:900px){.grid{grid-template-columns:1fr}}
.card{
  background:var(--bg-primary);border:1px solid var(--border-color);border-radius:var(--r);overflow:hidden;
  display:flex;flex-direction:column;transition:transform .18s;
}
.card:hover{transform:translateY(-3px)}
.ch{padding:.85rem 1rem .65rem;border-bottom:1px solid var(--border-color);background:var(--code-bg)}
.ctrow{display:flex;align-items:flex-start;gap:.5rem;margin-bottom:.45rem}
.cname{font-weight:700;font-size:.9rem;color:var(--text-primary);flex:1;line-height:1.3}
.cbadges{display:flex;gap:.28rem;flex-wrap:wrap;flex-shrink:0}
.bdg{
  font-size:.59rem;padding:.1rem .44rem;border-radius:2rem;border:1px solid var(--border-color);
  color:var(--text-secondary);background:var(--bg-primary);
}
.rb{font-size:.59rem;padding:.1rem .44rem;border-radius:2rem;border:1px solid;font-weight:700}
.r-info{color:var(--acc);border-color:var(--acc)}
.r-low{color:var(--grn);border-color:var(--grn)}
.r-medium{color:var(--ylw);border-color:var(--ylw)}
.r-high{color:var(--org);border-color:var(--org)}
.r-critical{color:var(--red);border-color:var(--red)}

.what{
  background:var(--bg-primary);border:1px solid var(--border-light);border-radius:var(--rs);
  padding:.45rem .65rem;font-size:.73rem;color:var(--text-primary);line-height:1.58;
}
.wlbl{font-size:.6rem;letter-spacing:.8px;text-transform:uppercase;color:var(--text-secondary);font-weight:700;margin-bottom:.18rem}

.cb{padding:.8rem 1rem;display:flex;flex-direction:column;gap:.6rem}
.dblk{background:var(--term-bg);border:1px solid var(--border-color);border-radius:var(--rs);overflow:hidden}
.dbar{
  display:flex;align-items:center;justify-content:space-between;padding:.28rem .65rem;
  border-bottom:1px solid var(--border-color);background:var(--code-bg);
}
.dbar-l{display:flex;align-items:center;gap:.45rem}
.dots{display:flex;gap:3px}
.dots span{width:8px;height:8px;border-radius:50%;background:var(--text-secondary);opacity:.5}
.dbar-r{display:flex;align-items:center;gap:.35rem}
.cbtn{
  background:none;border:1px solid var(--border-color);color:var(--text-secondary);font-size:.65rem;
  padding:.13rem .5rem;border-radius:3px;cursor:pointer;transition:all .14s;font-family:var(--mono);
}
.cbtn:hover{background:var(--text-primary);color:var(--bg-primary)}
.cbtn.ok{border-color:var(--grn)!important;color:var(--grn)!important;background:none!important}
.dpre{
  padding:.65rem .9rem;font-family:var(--mono);font-size:.78rem;color:var(--term-text);
  line-height:1.75;white-space:pre-wrap;word-break:break-all;margin:0;
}
.dpre .fl{font-weight:600;text-decoration:underline;text-decoration-style:dotted}
.dpre .tgt{font-weight:700;text-decoration:underline}

.outblk{background:var(--term-bg);border:1px solid var(--border-light);border-radius:var(--rs);overflow:hidden}
.outbar{
  display:flex;align-items:center;justify-content:space-between;padding:.26rem .65rem;
  border-bottom:1px solid var(--border-light);background:var(--code-bg);
}
.outlbl{font-family:var(--mono);font-size:.63rem;letter-spacing:.5px;text-transform:uppercase;color:var(--text-secondary)}
.outpre{
  padding:.6rem .9rem;font-family:var(--mono);font-size:.72rem;color:var(--text-secondary);
  line-height:1.7;white-space:pre-wrap;word-break:break-all;margin:0;
}
.outpre .oline{color:var(--text-primary)}

.ptog{
  display:flex;align-items:center;justify-content:space-between;background:var(--code-bg);
  border:1px solid var(--border-light);border-radius:var(--rs);padding:.34rem .65rem;
  font-size:.7rem;color:var(--text-secondary);cursor:pointer;transition:all .14s;width:100%;text-align:left;font-family:var(--font-body);
}
.ptog:hover{color:var(--text-primary)}
.ptog .arr{transition:transform .18s;font-size:.58rem;margin-left:auto;padding-left:.5rem}
.ptog.open .arr{transform:rotate(180deg)}
.pwrap{display:none;border:1px solid var(--border-light);border-top:none;border-radius:0 0 var(--rs) var(--rs);overflow:hidden}
.pwrap.open{display:block}
.ptbl{width:100%;border-collapse:collapse;font-size:.7rem}
.ptbl th{
  text-align:left;padding:.32rem .58rem;background:var(--bg-secondary);color:var(--text-secondary);
  font-size:.61rem;letter-spacing:.5px;text-transform:uppercase;border-bottom:1px solid var(--border-light);
}
.ptbl td{padding:.32rem .58rem;border-bottom:1px solid var(--border-light);vertical-align:top}
.ptbl tr:last-child td{border-bottom:none}
.pf{font-family:var(--mono);color:var(--text-primary);font-size:.68rem}
.pd{color:var(--text-secondary);font-size:.68rem}

.tip{
  background:transparent;border:1px solid var(--acc);border-radius:var(--rs);
  padding:.44rem .65rem;font-size:.71rem;color:var(--acc);display:flex;gap:.42rem;line-height:1.5;align-items:flex-start;
}
.wrn{
  background:transparent;border:1px solid var(--red);border-radius:var(--rs);
  padding:.44rem .65rem;font-size:.71rem;color:var(--red);display:flex;gap:.42rem;line-height:1.5;align-items:flex-start;
}
.tip .lbl,.wrn .lbl{font-weight:700;flex-shrink:0}

.ctable{background:var(--bg-primary);border:1px solid var(--border-color);border-radius:var(--r);overflow:hidden}
.chdr{
  display:grid;grid-template-columns:200px 1fr 82px 80px;gap:.4rem;padding:.36rem .75rem;
  background:var(--code-bg);border-bottom:1px solid var(--border-color);font-size:.62rem;color:var(--text-secondary);
  letter-spacing:.5px;text-transform:uppercase;
}
.crow{
  display:grid;grid-template-columns:200px 1fr 82px 80px;gap:.4rem;padding:.44rem .75rem;
  border-bottom:1px solid var(--border-light);align-items:center;transition:background .14s;
}
.crow:last-child{border-bottom:none}
.crow:hover{background:var(--code-bg)}
.cr-name{font-size:.75rem;font-weight:600;color:var(--text-primary);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.cr-cmd{font-family:var(--mono);font-size:.68rem;color:var(--text-secondary);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.cr-act{display:flex;gap:.28rem;align-items:center}
.crc{
  background:none;border:1px solid var(--border-color);color:var(--text-secondary);font-size:.62rem;
  padding:.1rem .38rem;border-radius:3px;cursor:pointer;transition:all .14s;
}
.crc:hover{background:var(--text-primary);color:var(--bg-primary)}
.crc.ok{border-color:var(--grn)!important;color:var(--grn)!important;background:none!important}
@media(max-width:640px){.chdr,.crow{grid-template-columns:130px 1fr 70px}}

.nores{text-align:center;padding:3.5rem;color:var(--text-secondary)}
.nores h3{font-size:.95rem;color:var(--text-primary);margin-bottom:.4rem;font-family:var(--font-header)}

/* ── FOOTER ── */
footer{border-top:1px solid var(--border-color);width:100%;margin-top:auto;padding:clamp(30px,5vw,50px) 0}
.footer-legal{
  border:1px solid var(--red);border-radius:8px;padding:1rem 1.4rem;margin-bottom:2rem;
  color:var(--red);font-size:.78rem;line-height:1.6;
}
.footer-legal strong{color:var(--red)}
.footer-middle{
  display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:20px;
  padding:20px 0;border-top:1px solid var(--border-light);
}
.footer-links{display:flex;gap:20px;font-weight:600;font-size:12px;flex-wrap:wrap}
.footer-links a{color:var(--text-secondary)}
.footer-links a:hover{color:var(--text-primary)}
.footer-brand{font-family:var(--font-header);font-weight:800;font-size:1rem;color:var(--text-primary)}
.footer-bottom{
  text-align:center;padding:15px 0;border-top:1px solid var(--border-light);
  font-size:11px;color:var(--text-secondary);margin-top:10px;
}
@media(max-width:768px){.footer-middle{flex-direction:column;text-align:center}}
</style>
</head>
<body class="dark-mode">

<header>
  <div class="container">
    <div class="logo">
      <a href="https://aw-junaid.github.io/" title="awjunaid - Cyber Security & Tech">awjunaid</a>
    </div>
    <div class="header-right">
      <nav class="main-nav">
        <a href="https://aw-junaid.github.io/">Home</a>
        <a href="https://aw-junaid.github.io/page/blog.html">Blog</a>
        <a href="https://buymeacoffee.com/awjunaid/membership">Membership</a>
        <div class="dropdown">
          <a href="#categories">Categories <i class="fa-solid fa-caret-down"></i></a>
          <div class="dropdown-content">
            <a href="https://aw-junaid.github.io/posts/cyber-security.html">Cyber Security</a>
            <a href="https://aw-junaid.github.io/posts/linux.html">Linux</a>
            <a href="https://aw-junaid.github.io/posts/networking.html">Networking</a>
            <a href="https://aw-junaid.github.io/posts/kali-linux.html">Kali Linux</a>
            <a href="https://aw-junaid.github.io/posts/hardware.html">Hardware</a>
          </div>
        </div>
      </nav>
      <div class="social-icons">
        <a href="https://github.com/aw-junaid/" target="_blank"><i class="fa-brands fa-github"></i></a>
        <a href="https://x.com/awjunaid_" target="_blank"><i class="fa-brands fa-twitter"></i></a>
        <a href="https://www.linkedin.com/in/aw-junaid/" target="_blank"><i class="fa-brands fa-linkedin"></i></a>
        <a href="https://www.youtube.com/@awjunaid/featured" target="_blank"><i class="fa-brands fa-youtube"></i></a>
        <a href="https://www.facebook.com/awjuna1d" target="_blank"><i class="fa-brands fa-facebook"></i></a>
        <a href="https://instagram.com/awjunaid_" target="_blank"><i class="fa-brands fa-instagram"></i></a>
      </div>
      <button class="theme-switcher" onclick="toggleTheme()">Invert</button>
    </div>
  </div>
</header>

<main>
<section class="hero">
  <div class="chip">DNSdumpster Reconnaissance &mdash; Kali Linux</div>
  <h2>Enter Domain &rarr; Get DNSdumpster Commands</h2>
  <p>Type any domain and instantly get copy-paste ready DNSdumpster commands and companion DNS-recon commands for passive subdomain discovery, DNS record mapping, and network host visualization &ndash; all optimized for Kali Linux.</p>
  <div class="panel">
    <div class="irow">
      <div class="ipfx">domain:</div>
      <input id="targetInput" type="text" placeholder="example.com" autocomplete="off" spellcheck="false"/>
      <button id="generateBtn">Generate</button>
    </div>
    <div class="errbox" id="errbox">Please enter a valid domain e.g. <strong>example.com</strong></div>
    <div class="statsbar" id="statsbar">
      <div class="sc"><div class="sdot"></div>Categories: <strong id="sc1">0</strong></div>
      <div class="sc"><div class="sdot"></div>Commands: <strong id="sc2">0</strong></div>
      <div class="sc"><div class="sdot"></div>Domain: <strong id="sc3">-</strong></div>
    </div>
  </div>
</section>

<div id="toolbar">
  <button class="vbtn on" id="vcard">Cards</button>
  <button class="vbtn" id="vcomp">Compact</button>
  <div class="srch">
    <span class="sico">&#9906;</span>
    <input type="text" id="searchInput" placeholder="Search commands, records, flags..." autocomplete="off" spellcheck="false"/>
  </div>
</div>

<div id="pills"></div>

<div id="mainLayout">
  <aside id="sidebar"></aside>
  <main id="content"></main>
</div>
</main>

<footer>
  <div class="container">
    <div class="footer-legal">
      <strong>Legal Disclaimer:</strong> These DNSdumpster commands are for <strong>authorized security research and penetration testing only</strong>.
      Only use on domains you own or have explicit written permission to test.
      Unauthorized DNS reconnaissance may be prohibited by your local laws.
    </div>
    <div class="footer-middle">
      <div class="footer-links">
        <a href="https://aw-junaid.github.io/page/privacy.html">Privacy</a>
        <a href="https://aw-junaid.github.io/page/terms.html">T&C'S</a>
        <a href="https://aw-junaid.github.io/page/contact.html">Contact</a>
        <a href="https://aw-junaid.github.io/page/about.html">About</a>
        <a href="https://aw-junaid.github.io/page/sitemap.html">Site Map</a>
      </div>
      <div class="social-icons">
        <a href="https://github.com/aw-junaid/" target="_blank"><i class="fa-brands fa-github"></i></a>
        <a href="https://x.com/awjunaid_" target="_blank"><i class="fa-brands fa-twitter"></i></a>
        <a href="https://www.linkedin.com/in/aw-junaid/" target="_blank"><i class="fa-brands fa-linkedin"></i></a>
        <a href="https://www.youtube.com/@awjunaid/featured" target="_blank"><i class="fa-brands fa-youtube"></i></a>
        <a href="https://www.facebook.com/awjuna1d" target="_blank"><i class="fa-brands fa-facebook"></i></a>
        <a href="https://instagram.com/awjunaid_" target="_blank"><i class="fa-brands fa-instagram"></i></a>
      </div>
    </div>
    <div class="footer-bottom">
      <span class="footer-brand">awjunaid</span> &mdash; Copyright &copy; 2026
      <a href="https://awjunaid.com" target="_blank" rel="noopener">awjunaid.com</a>. All rights reserved.
    </div>
  </div>
</footer>

<script>
/* ── DATA (DNSdumpster + companion DNS-recon commands) ── */
var CATS = [
{id:"webui",
 title:"DNSdumpster Web Reconnaissance",
 desc:"Core DNSdumpster.com usage for passive DNS reconnaissance &ndash; no direct interaction with the target, all data comes from existing DNS records and third-party sources.",
 tip:"DNSdumpster is entirely passive &ndash; it queries existing DNS records rather than probing the target directly, making it safe for early-stage recon.",
 warn:"Free DNSdumpster scans are rate-limited per IP. Space out requests or use an account/API key for heavier usage.",
 flags:[
   {f:"domain",d:"Target domain to look up"},
   {f:"export",d:"Download results as CSV/XLSX from the UI"},
   {f:"map",d:"Visual host/network relationship graph"}
 ],
 cmds:[
   {l:"Open DNSdumpster in browser",r:"low",c:"xdg-open https://dnsdumpster.com/?q={T}",e:"Opens DNSdumpster directly in the default browser pre-filled with the target domain, ready to run a scan from the web UI.",
    o:"Opening 'https://dnsdumpster.com/?q={T}' in existing browser session.\n[-] DNSdumpster loaded &ndash; domain field pre-filled with {T}\n[-] Click 'Search' to begin passive DNS lookup"},
   {l:"Curl the DNSdumpster page",r:"low",c:"curl -s https://dnsdumpster.com/ -c cookies.txt -o dnsdumpster_home.html",e:"Fetches the DNSdumpster homepage and stores session cookies, needed before submitting a search via curl (site requires a CSRF token).",
    o:"[-] Saved cookies to cookies.txt\n[-] Saved response to dnsdumpster_home.html\n$ grep csrfmiddlewaretoken dnsdumpster_home.html\n<input type=\"hidden\" name=\"csrfmiddlewaretoken\" value=\"aBcD123...\">"},
   {l:"Extract CSRF token",r:"low",c:"grep -oP \"csrfmiddlewaretoken['\\\"] value=['\\\"]\\K[^'\\\"]+\" dnsdumpster_home.html",e:"Pulls the CSRF token out of the saved homepage HTML, required as a form field for the next POST request to the search endpoint.",
    o:"aBcD123eFgH456iJkL789mNoP012qRsT"},
   {l:"Submit search via curl",r:"medium",c:"curl -s https://dnsdumpster.com/ -b cookies.txt -e https://dnsdumpster.com/ -d \"csrfmiddlewaretoken=$(cat token.txt)\" -d \"targetip={T}\" -o results_{T}.html",e:"Submits the domain search using the saved cookies and CSRF token, saving the full results page (host table, DNS records, network map) to a local HTML file.",
    o:"[-] POST request sent to dnsdumpster.com\n[-] HTTP/1.1 200 OK\n[-] Saved results to results_{T}.html\n[-] Results contain: DNS Servers, MX Records, TXT Records, Host Records"}
 ]
},
{id:"dnsrecords",
 title:"DNS Record Enumeration",
 desc:"Companion command-line DNS lookups that mirror what DNSdumpster surfaces &ndash; A, MX, TXT, NS, and SOA records &ndash; useful for cross-verifying web UI results from the terminal.",
 tip:"Cross-check DNSdumpster's web results against dig/host output to confirm records haven't changed since the passive data was last indexed.",
 warn:"Active DNS queries (dig/host) are minimal-footprint but are technically direct interaction with the target's nameservers, unlike DNSdumpster's passive lookups.",
 flags:[
   {f:"+short",d:"Print only the answer, no verbose header"},
   {f:"ANY",d:"Query for all available record types"},
   {f:"@server",d:"Query a specific nameserver directly"}
 ],
 cmds:[
   {l:"A record lookup",r:"low",c:"dig {T} A +short",e:"Resolves the domain's IPv4 address(es) &ndash; the same base data DNSdumpster's host table is built from.",
    o:"203.0.113.10"},
   {l:"MX record lookup",r:"low",c:"dig {T} MX +short",e:"Lists the mail exchange servers responsible for the domain, matching DNSdumpster's 'MX Records' section.",
    o:"10 mail.{T}.\n20 mail2.{T}."},
   {l:"TXT record lookup",r:"low",c:"dig {T} TXT +short",e:"Retrieves TXT records (SPF, DKIM, verification strings) &ndash; often reveals third-party services in use, same as DNSdumpster's TXT section.",
    o:"\"v=spf1 include:_spf.google.com ~all\"\n\"google-site-verification=abc123XYZ\""},
   {l:"NS record lookup",r:"low",c:"dig {T} NS +short",e:"Shows the authoritative nameservers for the domain, matching DNSdumpster's 'DNS Servers' table.",
    o:"ns1.{T}.\nns2.{T}."},
   {l:"All records at once",r:"medium",c:"dig {T} ANY +noall +answer",e:"Attempts to pull every available record type in a single query. Many modern resolvers restrict ANY queries, so results may be partial.",
    o:"{T}.  3600  IN  A      203.0.113.10\n{T}.  3600  IN  MX     10 mail.{T}.\n{T}.  3600  IN  NS     ns1.{T}.\n{T}.  3600  IN  TXT    \"v=spf1 ...\""},
   {l:"Zone transfer attempt",r:"high",c:"dig {T} AXFR @ns1.{T}",e:"Attempts a full zone transfer from the domain's own nameserver. Almost always refused on properly configured servers, but worth checking &ndash; a successful transfer dumps the entire zone.",
    o:"; Transfer failed.\n;; communications error to ns1.{T}#53: end of file\n[-] Zone transfer refused (expected on hardened servers)"}
 ]
},
{id:"hostmap",
 title:"Subdomain & Host Mapping",
 desc:"Cross-referencing DNSdumpster's host table with certificate transparency logs to build a fuller subdomain picture.",
 tip:"DNSdumpster's host table is sourced from passive DNS + search engines; combine it with crt.sh for subdomains that only ever had a certificate issued and no other public footprint.",
 warn:"Not every subdomain returned by crt.sh is still live &ndash; always verify with a resolution check before including it in a report.",
 flags:[
   {f:"output=json",d:"crt.sh JSON output format"},
   {f:"-o file",d:"Save results to a file"}
 ],
 cmds:[
   {l:"Cross-check with crt.sh",r:"low",c:"curl -s \"https://crt.sh/?q=%25.{T}&output=json\" | jq -r '.[].name_value' | sort -u",e:"Pulls every subdomain that has ever had a publicly logged SSL certificate, then deduplicates the list &ndash; a strong complement to DNSdumpster's host table.",
    o:"api.{T}\nblog.{T}\nmail.{T}\nsecure.{T}\nwww.{T}"},
   {l:"Merge DNSdumpster + crt.sh hosts",r:"medium",c:"grep -oP '(?<=<td class=\"col-md-4\">)[a-zA-Z0-9.\\-]+' results_{T}.html | sort -u > dumpster_hosts.txt && cat dumpster_hosts.txt crt_hosts.txt | sort -u > merged_hosts_{T}.txt",e:"Extracts hostnames from the saved DNSdumpster results page, combines them with a separate crt.sh export, and deduplicates for one master subdomain list.",
    o:"[-] dumpster_hosts.txt: 11 entries\n[-] crt_hosts.txt: 19 entries\n[-] merged_hosts_{T}.txt: 24 unique entries after dedup"},
   {l:"Resolve merged host list",r:"medium",c:"cat merged_hosts_{T}.txt | while read h; do ip=$(dig +short $h A | head -1); [ -n \"$ip\" ] && echo \"$h -> $ip\"; done",e:"Resolves every hostname in the merged list to confirm which ones are actually live before further testing.",
    o:"www.{T} -> 203.0.113.10\napi.{T} -> 203.0.113.22\nblog.{T} -> 203.0.113.5\nsecure.{T} -> NXDOMAIN (skipped)"}
 ]
},
{id:"netblock",
 title:"IP & Netblock / ASN Lookup",
 desc:"DNSdumpster's map view groups hosts by netblock and ASN &ndash; these commands reproduce that grouping from the command line for offline analysis.",
 tip:"Grouping hosts by ASN quickly reveals whether an organization is self-hosting, using a cloud provider, or spread across multiple providers.",
 warn:"WHOIS and ASN lookup services are also rate-limited &ndash; batch queries with short delays to avoid temporary blocks.",
 flags:[
   {f:"-h whois.server",d:"Query a specific WHOIS server"},
   {f:"origin",d:"Team Cymru IP-to-ASN lookup type"}
 ],
 cmds:[
   {l:"WHOIS lookup on resolved IP",r:"low",c:"whois $(dig +short {T} | head -1)",e:"Looks up ownership and netblock information for the domain's primary IP, matching the netblock data shown on DNSdumpster's map.",
    o:"NetRange:       203.0.113.0 - 203.0.113.255\nCIDR:           203.0.113.0/24\nOrgName:        Example Hosting Ltd\nCountry:        US"},
   {l:"ASN lookup via Team Cymru",r:"low",c:"whois -h whois.cymru.com \" -v $(dig +short {T} | head -1)\"",e:"Queries Team Cymru's WHOIS service for the Autonomous System Number tied to the resolved IP &ndash; useful for spotting shared hosting or CDN usage.",
    o:"AS      | IP             | AS Name\n64512   | 203.0.113.10   | EXAMPLE-AS, US"},
   {l:"Reverse DNS on netblock",r:"medium",c:"for i in $(seq 1 254); do host 203.0.113.$i 2>/dev/null | grep -v 'not found'; done",e:"Performs reverse DNS lookups across an entire /24 netblock to discover other hostnames sharing the same infrastructure as the target.",
    o:"Host 203.0.113.10 -> www.{T}\nHost 203.0.113.22 -> api.{T}\nHost 203.0.113.5 -> internal-host.otherdomain.com"}
 ]
},
{id:"export",
 title:"Output & Export Formats",
 desc:"Turning DNSdumpster's saved HTML results into structured data (CSV, JSON) for reporting or feeding into other tools.",
 tip:"Keep the raw saved HTML from each scan &ndash; DNSdumpster's free tier doesn't retain scan history, so your local copy is the only record.",
 warn:"Always double-check parsed data against the original DNSdumpster page &ndash; HTML table structure can change and break simple grep/sed extraction.",
 flags:[
   {f:"-o file",d:"Write output to file"},
   {f:"jq",d:"JSON processor for structured output"}
 ],
 cmds:[
   {l:"Extract host table to CSV",r:"medium",c:"grep -oP '(?<=<td class=\"col-md-4\">)[^<]+' results_{T}.html | paste -sd, - > hosts_{T}.csv",e:"Pulls the hostname column out of the saved results page and writes it as a single-line CSV, ready to open in a spreadsheet.",
    o:"$ cat hosts_{T}.csv\nwww.{T},api.{T},mail.{T},ftp.{T}"},
   {l:"Convert host list to JSON",r:"low",c:"cat merged_hosts_{T}.txt | jq -R -s 'split(\"\\n\") | map(select(length>0)) | {domain:\"{T}\", hosts: .}' > hosts_{T}.json",e:"Wraps the merged hostname list into a simple JSON object with the target domain as a key, suitable for feeding into other automation.",
    o:"$ cat hosts_{T}.json\n{\n  \"domain\": \"{T}\",\n  \"hosts\": [\"www.{T}\", \"api.{T}\", \"mail.{T}\"]\n}"},
   {l:"Generate Markdown report table",r:"medium",c:"echo \"| Host | IP |\\n|------|----|\" > report_{T}.md && cat merged_hosts_{T}.txt | while read h; do ip=$(dig +short $h A|head -1); echo \"| $h | $ip |\" >> report_{T}.md; done",e:"Builds a simple Markdown table of hosts and their resolved IPs, ready to paste directly into a recon report.",
    o:"$ cat report_{T}.md\n| Host | IP |\n|------|----|\n| www.{T} | 203.0.113.10 |\n| api.{T} | 203.0.113.22 |"}
 ]
},
{id:"automation",
 title:"Automation & Scripting",
 desc:"Wrapping the DNSdumpster workflow (fetch token, submit search, parse results) into a repeatable script for use across multiple targets.",
 tip:"Add a short sleep between requests in any loop to stay well under DNSdumpster's rate limit when scanning several domains.",
 warn:"Automating requests against DNSdumpster's web form is against convenience, not guaranteed uptime &ndash; expect occasional CAPTCHA challenges on heavy use.",
 flags:[
   {f:"-b cookies.txt",d:"Use/store cookies for the session"},
   {f:"-d",d:"Send POST data"},
   {f:"sleep N",d:"Delay between requests"}
 ],
 cmds:[
   {l:"Full scan-and-save one-liner",r:"high",c:"curl -sc c.txt https://dnsdumpster.com/ -o h.html && TOKEN=$(grep -oP \"csrfmiddlewaretoken['\\\"] value=['\\\"]\\K[^'\\\"]+\" h.html) && curl -s -b c.txt -e https://dnsdumpster.com/ -d \"csrfmiddlewaretoken=$TOKEN\" -d \"targetip={T}\" https://dnsdumpster.com/ -o results_{T}.html",e:"Chains the cookie fetch, token extraction, and search submission into a single command &ndash; a full DNSdumpster scan in one line.",
    o:"[-] Session cookie stored\n[-] CSRF token extracted: aBcD123...\n[-] Search submitted for {T}\n[-] Results saved to results_{T}.html"},
   {l:"Batch scan multiple domains",r:"high",c:"for d in $(cat domains.txt); do curl -sc c.txt https://dnsdumpster.com/ -o h.html; TOKEN=$(grep -oP \"csrfmiddlewaretoken['\\\"] value=['\\\"]\\K[^'\\\"]+\" h.html); curl -s -b c.txt -e https://dnsdumpster.com/ -d \"csrfmiddlewaretoken=$TOKEN\" -d \"targetip=$d\" https://dnsdumpster.com/ -o results_$d.html; sleep 5; done",e:"Loops the full scan process across a list of domains from domains.txt, with a 5-second delay between each to respect rate limits.",
    o:"[-] Scanning {T} .. done (results_{T}.html)\n[-] Sleeping 5s\n[-] Scanning otherdomain.com .. done (results_otherdomain.com.html)\n[-] Batch scan complete: 2/2 domains processed"},
   {l:"Schedule recurring scans (cron)",r:"medium",c:"echo \"0 3 * * 1 /usr/local/bin/dnsdumpster_scan.sh {T} >> /var/log/dnsdumpster_{T}.log 2>&1\" | crontab -",e:"Schedules a wrapper script to re-scan the target every Monday at 3 AM, appending output to a log file &ndash; useful for tracking DNS changes over time.",
    o:"[-] Crontab updated\n$ crontab -l\n0 3 * * 1 /usr/local/bin/dnsdumpster_scan.sh {T} >> /var/log/dnsdumpster_{T}.log 2>&1"}
 ]
},
{id:"integration",
 title:"Integration With Other Tools",
 desc:"Feeding DNSdumpster's output into other recon and scanning tools to build a complete reconnaissance pipeline.",
 tip:"Use DNSdumpster early in recon &ndash; it's passive and free, so it's a good first pass before spending time on active brute-force tools.",
 warn:"Only pass DNSdumpster-derived hosts into active scanning tools (nmap, httprobe) once you've confirmed they're in scope for the engagement.",
 flags:[
   {f:"-iL file",d:"Nmap input list of targets"},
   {f:"httprobe",d:"Probes hosts for live HTTP/HTTPS"}
 ],
 cmds:[
   {l:"Feed hosts into Nmap",r:"high",c:"nmap -iL merged_hosts_{T}.txt -oA nmap_{T} -p 80,443,8080,8443",e:"Uses the merged DNSdumpster + crt.sh host list as Nmap's target list, scanning common web ports across every discovered host in one pass.",
    o:"Starting Nmap 7.94 ( https://nmap.org )\nNmap scan report for www.{T} (203.0.113.10)\nPORT     STATE SERVICE\n80/tcp   open  http\n443/tcp  open  https\nNmap done: 24 IP addresses scanned"},
   {l:"Pipe hosts into httprobe",r:"high",c:"cat merged_hosts_{T}.txt | httprobe -c 50 > live_{T}.txt",e:"Checks every discovered host for a live HTTP/HTTPS response using 50 concurrent workers, filtering the list down to only reachable services.",
    o:"https://www.{T}\nhttps://api.{T}\nhttp://mail.{T}\n[-] 3/24 hosts responded"},
   {l:"Import into Amass for correlation",r:"medium",c:"amass enum -passive -d {T} -src -o amass_{T}.txt && diff <(sort merged_hosts_{T}.txt) <(sort amass_{T}.txt)",e:"Runs Amass in passive mode alongside the DNSdumpster results and diffs the two host lists to spot anything one tool found that the other missed.",
    o:"[-] Amass found 31 hosts, DNSdumpster+crt.sh found 24\n< dev.{T}\n< internal.{T}\n> secure.{T}\n[-] 6 hosts unique to Amass, 1 unique to DNSdumpster set"}
 ]
}
];

/* ── STATE ── */
var TARGET = "";
var FILTER = "all";
var QUERY  = "";
var VIEW   = "cards";

/* ── THEME ── */
function toggleTheme() {
  document.body.classList.toggle("dark-mode");
  localStorage.setItem("theme", document.body.classList.contains("dark-mode") ? "dark" : "light");
}
window.addEventListener("load", function(){
  if (localStorage.getItem("theme") === "light") { document.body.classList.remove("dark-mode"); }
});

/* ── HELPERS ── */
function esc(s) {
  return String(s)
    .replace(/&/g,"&amp;")
    .replace(/</g,"&lt;")
    .replace(/>/g,"&gt;")
    .replace(/"/g,"&quot;");
}
function validDomain(t) {
  var d = t.trim().replace(/^https?:\/\//i,"").replace(/\/.*/,"");
  return /^([a-zA-Z0-9]([a-zA-Z0-9\-]{0,61}[a-zA-Z0-9])?\.)+[a-zA-Z]{2,}$/.test(d)
      || /^[a-zA-Z0-9][a-zA-Z0-9\-]{0,61}$/.test(d)
      || /^(\d{1,3}\.){3}\d{1,3}$/.test(d);
}
function cleanDomain(t) {
  return t.trim().replace(/^https?:\/\//i,"").replace(/\/.*/,"").replace(/\/$/,"");
}
function fillCmd(c) { return c.replace(/\{T\}/g, TARGET || "example.com"); }
function totalCmds() {
  var n = 0;
  for (var i = 0; i < CATS.length; i++) { n += CATS[i].cmds.length; }
  return n;
}
function colorize(raw) {
  var s = esc(fillCmd(raw));
  s = s.replace(/(\s)(--?[a-zA-Z][a-zA-Z0-9\-_\.]*)/g,'$1<span class="fl">$2</span>');
  if (TARGET) {
    var et = esc(TARGET);
    var re = new RegExp(et.replace(/[.*+?^${}()|[\]\\]/g,"\\$&"),"g");
    s = s.replace(re,'<span class="tgt">'+et+"</span>");
  }
  return s;
}
function colorizeOut(raw) {
  return esc(fillCmd(raw));
}

/* ── FILTER / SEARCH ── */
function getVisibleCats() {
  return CATS.filter(function(cat) {
    if (FILTER !== "all" && cat.id !== FILTER) { return false; }
    if (!QUERY) { return true; }
    var q = QUERY.toLowerCase();
    if (cat.title.toLowerCase().indexOf(q) >= 0) { return true; }
    if (cat.desc.toLowerCase().indexOf(q) >= 0) { return true; }
    for (var i = 0; i < cat.cmds.length; i++) {
      var cm = cat.cmds[i];
      if (cm.l.toLowerCase().indexOf(q) >= 0 ||
          cm.c.toLowerCase().indexOf(q) >= 0 ||
          cm.e.toLowerCase().indexOf(q) >= 0) { return true; }
    }
    return false;
  });
}
function getFilteredCmds(cat) {
  if (!QUERY) { return cat.cmds; }
  var q = QUERY.toLowerCase();
  return cat.cmds.filter(function(cm) {
    return cm.l.toLowerCase().indexOf(q) >= 0 ||
           cm.c.toLowerCase().indexOf(q) >= 0 ||
           cm.e.toLowerCase().indexOf(q) >= 0;
  });
}

/* ── COPY ── */
function doCopy(text, btn) {
  var orig = btn.textContent;
  function ok() {
    btn.textContent = "Copied!";
    btn.classList.add("ok");
    setTimeout(function(){ btn.textContent = orig; btn.classList.remove("ok"); }, 2000);
  }
  function fb() {
    var ta = document.createElement("textarea");
    ta.value = text;
    ta.style.cssText = "position:fixed;top:-9999px;left:-9999px;opacity:0;";
    document.body.appendChild(ta);
    ta.focus(); ta.select();
    try { document.execCommand("copy"); ok(); } catch(e) {}
    document.body.removeChild(ta);
  }
  if (navigator.clipboard && window.isSecureContext) {
    navigator.clipboard.writeText(text).then(ok, fb);
  } else { fb(); }
}
function copyFromBlock(bid, btn) {
  var el = document.getElementById(bid);
  if (!el) { return; }
  var pre = el.querySelector(".dpre");
  if (!pre) { return; }
  doCopy(pre.innerText.trim(), btn);
}
function copyInline(btn) { doCopy(btn.getAttribute("data-v"), btn); }

/* ── GENERATE ── */
function doGenerate() {
  var raw = document.getElementById("targetInput").value;
  var errBox = document.getElementById("errbox");
  if (!raw || !raw.trim() || !validDomain(raw)) {
    errBox.style.display = "block";
    return;
  }
  errBox.style.display = "none";
  TARGET = cleanDomain(raw);
  FILTER = "all";
  QUERY  = "";
  var si = document.getElementById("searchInput");
  if (si) { si.value = ""; }
  document.getElementById("sc1").textContent = CATS.length;
  document.getElementById("sc2").textContent = totalCmds();
  document.getElementById("sc3").textContent = TARGET;
  document.getElementById("statsbar").style.display = "flex";
  document.getElementById("toolbar").style.display  = "flex";
  document.getElementById("pills").style.display    = "flex";
  document.getElementById("mainLayout").style.display = "grid";
  buildSidebar(); buildPills(); render();
  setTimeout(function(){
    document.getElementById("mainLayout").scrollIntoView({behavior:"smooth",block:"start"});
  }, 100);
}

/* ── SIDEBAR ── */
function buildSidebar() {
  var h = '<div class="sbt">Navigation</div>';
  h += '<button class="sbtn on" data-cat="all">';
  h += '<span class="sblbl">All Categories</span>';
  h += '<span class="sbcnt">'+CATS.length+"</span></button>";
  h += '<div class="sbsep"></div>';
  h += '<div class="sbt">DNSdumpster Techniques</div>';
  for (var i = 0; i < CATS.length; i++) {
    var c = CATS[i];
    h += '<button class="sbtn" data-cat="'+c.id+'">';
    h += '<span class="sblbl">'+esc(c.title)+"</span>";
    h += '<span class="sbcnt">'+c.cmds.length+"</span></button>";
  }
  var sb = document.getElementById("sidebar");
  sb.innerHTML = h;
  var btns = sb.querySelectorAll(".sbtn[data-cat]");
  for (var j = 0; j < btns.length; j++) {
    btns[j].addEventListener("click", function(){
      setFilter(this.getAttribute("data-cat"));
    });
  }
}

/* ── PILLS ── */
function buildPills() {
  var h = '<span class="pill on" data-cat="all">All</span>';
  for (var i = 0; i < CATS.length; i++) {
    var c = CATS[i];
    h += '<span class="pill" data-cat="'+c.id+'">'+esc(c.title)+"</span>";
  }
  var container = document.getElementById("pills");
  container.innerHTML = h;
  var pills = container.querySelectorAll(".pill");
  for (var j = 0; j < pills.length; j++) {
    pills[j].addEventListener("click", function(){
      setFilter(this.getAttribute("data-cat"));
    });
  }
}

/* ── SET FILTER / VIEW ── */
function setFilter(id) {
  FILTER = id;
  var pills = document.querySelectorAll(".pill");
  for (var i = 0; i < pills.length; i++) {
    pills[i].classList.toggle("on", pills[i].getAttribute("data-cat") === id);
  }
  var btns = document.querySelectorAll(".sbtn[data-cat]");
  for (var j = 0; j < btns.length; j++) {
    btns[j].classList.toggle("on", btns[j].getAttribute("data-cat") === id);
  }
  render();
}
function setView(v) {
  VIEW = v;
  document.getElementById("vcard").classList.toggle("on", v === "cards");
  document.getElementById("vcomp").classList.toggle("on", v === "compact");
  render();
}
function togParams(wid, tid) {
  var w = document.getElementById(wid);
  var t = document.getElementById(tid);
  if (!w || !t) { return; }
  var o = w.classList.contains("open");
  w.classList.toggle("open", !o);
  t.classList.toggle("open", !o);
}

/* ── RENDER ── */
function render() {
  var content = document.getElementById("content");
  var cats = getVisibleCats();
  if (!cats.length) {
    content.innerHTML = '<div class="nores"><h3>No commands found</h3><p>Try a different search term or select a different category.</p></div>';
    return;
  }
  if (VIEW === "compact") { renderCompact(content, cats); }
  else { renderCards(content, cats); }
}

function renderCards(content, cats) {
  var html = "";
  for (var i = 0; i < cats.length; i++) {
    var cat = cats[i];
    var cmds = getFilteredCmds(cat);
    if (!cmds.length) { continue; }
    html += '<div class="sec" id="sec-'+cat.id+'">';
    html += '<div class="sechdr">';
    html += "<div>";
    html += '<div class="sectitle">'+esc(cat.title)+"</div>";
    html += '<div class="secsub">'+esc(cat.desc)+"</div>";
    html += "</div>";
    html += '<span class="seccnt">'+cmds.length+' cmd'+(cmds.length!==1?"s":"")+"</span>";
    html += "</div>";
    html += '<div class="grid">';
    for (var j = 0; j < cmds.length; j++) {
      html += buildCard(cat, cmds[j], cat.id+"_"+j);
    }
    html += "</div></div>";
  }
  content.innerHTML = html;
}

function buildCard(cat, cm, uid) {
  var bid   = "blk_"+uid;
  var ptid  = "pt_"+uid;
  var togid = "ptog_"+uid;
  var risk  = cm.r || "info";
  var h = "";
  h += '<div class="card">';
  h += '<div class="ch">';
  h += '<div class="ctrow">';
  h += '<span class="cname">'+esc(cm.l)+"</span>";
  h += '<div class="cbadges">';
  h += '<span class="bdg">'+esc(cat.id)+"</span>";
  h += '<span class="rb r-'+risk+'">'+risk+"</span>";
  h += "</div></div>";
  h += '<div class="what">';
  h += '<div class="wlbl">What This Command Does</div>';
  h += esc(cm.e);
  h += "</div>";
  h += "</div>";
  h += '<div class="cb">';
  h += '<div class="dblk" id="'+bid+'">';
  h += '<div class="dbar">';
  h += '<div class="dbar-l">';
  h += '<div class="dots"><span></span><span></span><span></span></div>';
  h += '<span style="font-family:var(--mono);font-size:.66rem;color:var(--text-secondary)">terminal</span>';
  h += "</div>";
  h += '<div class="dbar-r">';
  h += '<span class="rb r-'+risk+'">'+risk+"</span>";
  h += '<button class="cbtn" onclick="copyFromBlock(\''+bid+'\',this)">Copy</button>';
  h += "</div></div>";
  h += '<pre class="dpre">'+colorize(cm.c)+"</pre>";
  h += "</div>";
  if (cm.o) {
    h += '<div class="outblk">';
    h += '<div class="outbar"><span class="outlbl">Expected Output</span></div>';
    h += '<pre class="outpre">'+colorizeOut(cm.o)+"</pre>";
    h += "</div>";
  }
  if (cat.flags && cat.flags.length) {
    h += '<button class="ptog" id="'+togid+'" onclick="togParams(\''+ptid+'\',\''+togid+'\')">';
    h += "<span>Flags Reference ("+cat.flags.length+")</span>";
    h += '<span class="arr">&#9660;</span>';
    h += "</button>";
    h += '<div class="pwrap" id="'+ptid+'">';
    h += '<table class="ptbl"><thead><tr><th>Flag</th><th>Description</th></tr></thead><tbody>';
    for (var k = 0; k < cat.flags.length; k++) {
      h += "<tr>";
      h += '<td class="pf">'+esc(cat.flags[k].f)+"</td>";
      h += '<td class="pd">'+esc(cat.flags[k].d)+"</td>";
      h += "</tr>";
    }
    h += "</tbody></table></div>";
  }
  if (cat.tip) {
    h += '<div class="tip"><span class="lbl">Tip:</span><span>'+esc(cat.tip)+"</span></div>";
  }
  if (cat.warn) {
    h += '<div class="wrn"><span class="lbl">Warning:</span><span>'+esc(cat.warn)+"</span></div>";
  }
  h += "</div>";
  h += "</div>";
  return h;
}

function renderCompact(content, cats) {
  var html = '<div class="ctable">';
  html += '<div class="chdr"><div>Command Name</div><div>Command</div><div>Risk</div><div>Copy</div></div>';
  for (var i = 0; i < cats.length; i++) {
    var cmds = getFilteredCmds(cats[i]);
    for (var j = 0; j < cmds.length; j++) {
      var cm   = cmds[j];
      var risk = cm.r || "info";
      var filled = fillCmd(cm.c);
      html += '<div class="crow">';
      html += '<span class="cr-name" title="'+esc(cm.e)+'">'+esc(cm.l)+"</span>";
      html += '<span class="cr-cmd" title="'+esc(filled)+'">'+esc(filled)+"</span>";
      html += '<span><span class="rb r-'+risk+'">'+risk+"</span></span>";
      html += '<span class="cr-act"><button class="crc" data-v="'+esc(filled)+'" onclick="copyInline(this)">Copy</button></span>';
      html += "</div>";
    }
  }
  html += "</div>";
  content.innerHTML = html;
}

/* ── BOOT ── */
(function() {
  var btn = document.getElementById("generateBtn");
  if (btn) {
    btn.addEventListener("click", function(e){ e.preventDefault(); doGenerate(); });
  }
  var inp = document.getElementById("targetInput");
  if (inp) {
    inp.addEventListener("keydown", function(e){ if (e.key==="Enter"){ e.preventDefault(); doGenerate(); } });
  }
  var si = document.getElementById("searchInput");
  if (si) {
    function doSearch(){ QUERY = si.value.trim(); render(); }
    si.addEventListener("input",  doSearch);
    si.addEventListener("keyup",  doSearch);
    si.addEventListener("change", doSearch);
  }
  var vc = document.getElementById("vcard");
  var vp = document.getElementById("vcomp");
  if (vc) { vc.addEventListener("click", function(){ setView("cards"); }); }
  if (vp) { vp.addEventListener("click", function(){ setView("compact"); }); }
})();
</script>
</body>
</html>
