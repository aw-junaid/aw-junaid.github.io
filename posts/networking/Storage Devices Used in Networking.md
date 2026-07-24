<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>
      Storage Devices Used in Networking - awjunaid
    </title>
    <link
      href="https://fonts.googleapis.com/css2?family=League+Spartan:wght@700;800&family=Poppins:wght@300;400;600&family=Inter:wght@300;400;500;600;700;800;900&display=swap"
      rel="stylesheet"
    />
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"
    />
    <link
      rel="stylesheet"
      href="https://sibforms.com/forms/end-form/build/sib-styles.css"
    />

    <!-- MathJax for mathematical expressions -->
    <script
      src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"
      id="MathJax-script"
      async
    ></script>

    <style>
      /* ============================================
           GLOBAL BLACK & WHITE THEME (DEFAULT)
           ============================================ */

      :root {
        --bg-primary: #ffffff;
        --bg-secondary: #f5f5f5;
        --bg-color: #ffffff;
        --text-primary: #000000;
        --text-secondary: #333333;
        --text-color: #000000;
        --border-color: #000000;
        --border-light: #e0e0e0;
        --input-bg: #ffffff;
        --hover-bg: #000000;
        --hover-text: #ffffff;
        --font-header: "League Spartan", sans-serif;
        --font-body: "Poppins", sans-serif;
        --font-inter: "Inter", sans-serif;
        --code-bg: #f4f4f4;
        --code-text: #000000;
        --content-width: 1280px;
        --warning-red: #8b0000;
        --note-blue: #1e3a8a;
        --caution-orange: #b45309;
        --quote-border: #333333;
        --success-green: #166534;
      }

      body.dark-mode {
        --bg-primary: #000000;
        --bg-secondary: #0a0a0a;
        --bg-color: #000000;
        --text-primary: #ffffff;
        --text-secondary: #cccccc;
        --text-color: #ffffff;
        --border-color: #ffffff;
        --border-light: #2a2a2a;
        --input-bg: #111111;
        --hover-bg: #ffffff;
        --hover-text: #000000;
        --code-bg: #111111;
        --code-text: #e0e0e0;
        --warning-red: #ff6b6b;
        --note-blue: #60a5fa;
        --caution-orange: #fb923c;
        --quote-border: #666666;
        --success-green: #4ade80;
      }

      * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
      }
      html {
        scroll-behavior: smooth;
      }
      body {
        background-color: var(--bg-color);
        color: var(--text-color);
        font-family: var(--font-body);
        display: flex;
        flex-direction: column;
        min-height: 100vh;
        transition:
          background-color 0.3s,
          color 0.3s;
        line-height: 1.6;
        overflow-x: hidden;
      }
      a {
        color: var(--text-color);
        text-decoration: none;
        transition: all 0.2s ease;
      }
      a:hover {
        text-decoration: underline;
        opacity: 0.8;
      }
      .container {
        max-width: var(--content-width);
        margin: 0 auto;
        width: 100%;
        padding: 0 24px;
      }

      /* ============================================
           HEADER & NAVIGATION (PRESERVED)
           ============================================ */
      header {
        border-bottom: 1px solid var(--border-color);
        padding: 16px 0;
        width: 100%;
        z-index: 1000;
        position: sticky;
        top: 0;
        background-color: var(--bg-color);
      }
      header .container {
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-wrap: wrap;
        gap: 15px;
      }
      .logo a {
        font-family: var(--font-header);
        font-size: clamp(18px, 5vw, 26px);
        font-weight: 800;
        text-transform: lowercase;
        letter-spacing: -1px;
      }
      .logo a:hover {
        opacity: 0.7;
        text-decoration: none;
      }
      .header-right {
        display: flex;
        align-items: center;
        gap: clamp(12px, 2vw, 24px);
        flex-wrap: wrap;
      }
      nav.main-nav {
        display: flex;
        gap: clamp(16px, 2.5vw, 24px);
        font-weight: 600;
        font-size: 14px;
        flex-wrap: wrap;
      }
      nav.main-nav a:hover {
        opacity: 0.65;
        text-decoration: none;
      }
      .dropdown {
        position: relative;
        display: inline-block;
      }
      .dropdown-content {
        display: none;
        position: absolute;
        background-color: var(--bg-color);
        min-width: 200px;
        border: 1px solid var(--border-color);
        z-index: 100;
        top: 100%;
        left: 0;
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.05);
      }
      .dropdown-content a {
        padding: 12px 16px;
        display: block;
        border-bottom: 1px solid var(--border-color);
        font-size: 13px;
        font-weight: 500;
      }
      .dropdown-content a:hover {
        background-color: var(--hover-bg);
        color: var(--hover-text);
        padding-left: 20px;
        text-decoration: none;
      }
      .dropdown:hover .dropdown-content {
        display: block;
      }
      .social-icons {
        display: flex;
        gap: 10px;
        font-size: 18px;
        align-items: center;
      }
      .social-icons a {
        opacity: 0.8;
        transition: all 0.2s;
      }
      .social-icons a:hover {
        transform: translateY(-2px);
        opacity: 1;
        text-decoration: none;
      }
      .theme-switcher {
        background: var(--bg-color);
        border: 1px solid var(--border-color);
        color: var(--text-color);
        padding: 6px 14px;
        cursor: pointer;
        font-family: var(--font-header);
        font-weight: 700;
        text-transform: uppercase;
        font-size: 11px;
        border-radius: 30px;
        transition: 0.2s;
      }
      .theme-switcher:hover {
        background-color: var(--hover-bg);
        color: var(--hover-text);
        text-decoration: none;
      }

      /* ============================================
           GLOBAL POST CONTENT STYLES (AUTO-FORMAT ANY HTML)
           ============================================ */
      .post-content {
        max-width: 900px;
        margin: 0 auto 64px;
      }

      /* Headings */
      .post-content h1 {
        font-family: var(--font-inter);
        font-size: 2.5rem;
        font-weight: 900;
        margin: 48px 0 24px 0;
        border-left: 5px solid var(--border-color);
        padding-left: 24px;
      }
      .post-content h2 {
        font-family: var(--font-inter);
        font-size: 2rem;
        font-weight: 800;
        margin: 48px 0 20px 0;
        border-left: 4px solid var(--border-color);
        padding-left: 20px;
      }
      .post-content h3 {
        font-family: var(--font-inter);
        font-size: 1.5rem;
        font-weight: 700;
        margin: 32px 0 16px 0;
        border-left: 3px solid var(--border-color);
        padding-left: 16px;
      }
      .post-content h4 {
        font-family: var(--font-inter);
        font-size: 1.25rem;
        font-weight: 600;
        margin: 24px 0 12px 0;
      }
      .post-content p {
        margin-bottom: 20px;
        line-height: 1.8;
      }

      /* GLOBAL CODE BLOCK SYSTEM with AUTO COPY BUTTON */
      .post-content pre {
        position: relative;
        margin: 28px 0;
        background: var(--code-bg);
        border: 1px solid var(--border-light);
        border-radius: 12px;
        padding: 20px;
        overflow-x: auto;
        font-family: "Courier New", "SF Mono", monospace;
        font-size: 0.85rem;
        line-height: 1.5;
        color: var(--code-text);
      }

      /* Auto-generated copy button wrapper */
      .code-wrapper {
        position: relative;
        margin: 28px 0;
      }
      .code-wrapper pre {
        margin: 0;
      }
      .copy-code-btn {
        position: absolute;
        top: 12px;
        right: 12px;
        background: var(--bg-color);
        border: 1px solid var(--border-color);
        color: var(--text-color);
        padding: 6px 12px;
        border-radius: 8px;
        cursor: pointer;
        font-size: 0.7rem;
        font-weight: 600;
        font-family: var(--font-body);
        transition: 0.2s;
        z-index: 10;
        backdrop-filter: blur(4px);
      }
      .copy-code-btn:hover {
        background: var(--hover-bg);
        color: var(--hover-text);
      }

      /* Inline code */
      .post-content code:not(pre code) {
        font-family: "Courier New", monospace;
        background: var(--code-bg);
        padding: 2px 6px;
        border-radius: 6px;
        font-size: 0.85rem;
        color: var(--code-text);
      }

      /* Lists */
      .post-content ul,
      .post-content ol {
        margin: 20px 0 20px 32px;
      }
      .post-content li {
        margin-bottom: 8px;
      }

      /* TABLES - Auto-styled */
      .post-content table {
        width: 100%;
        border-collapse: collapse;
        margin: 28px 0;
        border: 1px solid var(--border-light);
      }
      .post-content th,
      .post-content td {
        border: 1px solid var(--border-light);
        padding: 12px 16px;
        text-align: left;
      }
      .post-content th {
        background: var(--bg-secondary);
        font-weight: 700;
      }
      .post-content tr:nth-child(even) {
        background: var(--bg-secondary);
      }

      /* BLOCKQUOTES */
      .post-content blockquote {
        margin: 28px 0;
        padding: 20px 24px;
        background: var(--code-bg);
        border-left: 6px solid var(--border-color);
        font-style: italic;
        border-radius: 12px;
      }
      .post-content blockquote p {
        margin-bottom: 0;
      }

      /* NOTE, CAUTION, WARNING, TIP - Auto detect by class or data attributes */
      .post-content .note,
      .post-content .note-box,
      .post-content div[class*="note"] {
        margin: 28px 0;
        padding: 20px 24px;
        background: var(--code-bg);
        border-left: 6px solid var(--note-blue);
        border-radius: 12px;
      }

      .post-content .caution,
      .post-content .warning,
      .post-content .caution-box,
      .post-content div[class*="caution"],
      .post-content div[class*="warning"] {
        margin: 28px 0;
        padding: 20px 24px;
        background: var(--code-bg);
        border-left: 6px solid var(--caution-orange);
        border-radius: 12px;
      }

      .post-content .tip,
      .post-content .success,
      .post-content div[class*="tip"] {
        margin: 28px 0;
        padding: 20px 24px;
        background: var(--code-bg);
        border-left: 6px solid var(--success-green);
        border-radius: 12px;
      }

      /* HR */
      .post-content hr {
        border: none;
        border-top: 2px solid var(--border-light);
        margin: 40px 0;
      }

      /* IMAGES */
      .post-content img {
        max-width: 100%;
        height: auto;
        border-radius: 12px;
        border: 1px solid var(--border-light);
        margin: 20px 0;
        filter: grayscale(100%);
      }

      /* Back to top button */
      .back-to-top {
        display: inline-flex;
        align-items: center;
        gap: 8px;
        margin: 32px 0;
        padding: 10px 20px;
        border: 1px solid var(--border-color);
        border-radius: 40px;
        font-size: 13px;
        font-weight: 600;
        transition: 0.2s;
        cursor: pointer;
      }
      .back-to-top:hover {
        background: var(--hover-bg);
        color: var(--hover-text);
        text-decoration: none;
      }

      /* Hero section */
      .post-hero {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 48px;
        margin: 48px 0 48px;
        align-items: center;
        border-bottom: 2px solid var(--border-color);
        padding-bottom: 48px;
      }
      .hero-image {
        width: 100%;
        border-radius: 24px;
        overflow: hidden;
        border: 1px solid var(--border-color);
        background: var(--code-bg);
      }
      .hero-image img {
        width: 100%;
        height: auto;
        display: block;
        filter: grayscale(100%);
      }
      .hero-content h1 {
        font-family: var(--font-inter);
        font-size: clamp(32px, 5vw, 48px);
        font-weight: 900;
        line-height: 1.2;
        letter-spacing: -0.02em;
        margin-bottom: 20px;
        border-left: none;
        padding-left: 0;
      }
      .post-meta {
        display: flex;
        gap: 24px;
        flex-wrap: wrap;
        margin: 20px 0 16px;
        font-size: 0.85rem;
        opacity: 0.7;
        border-top: 1px solid var(--border-light);
        padding-top: 16px;
      }
      .post-meta span i {
        margin-right: 6px;
      }
      .hero-excerpt {
        font-size: 1.1rem;
        opacity: 0.85;
        margin-top: 16px;
        border-left: 3px solid var(--border-color);
        padding-left: 20px;
      }
      @media (max-width: 768px) {
        .post-hero {
          grid-template-columns: 1fr;
          gap: 28px;
        }
      }

      /* Footer & Signup (preserved) */
      .email-signup {
        background: var(--bg-secondary);
        padding: 2.8rem 2rem;
        border-radius: 32px;
        text-align: center;
        margin: 48px 0 40px;
        border: 1px solid var(--border-light);
      }
      .signup-form {
        display: flex;
        gap: 12px;
        max-width: 500px;
        margin: 0 auto;
        flex-wrap: wrap;
        justify-content: center;
      }
      .signup-form input {
        flex: 1;
        min-width: 200px;
        padding: 14px 20px;
        border-radius: 60px;
        border: 1px solid var(--border-light);
        background: var(--input-bg);
        color: var(--text-primary);
        font-family: var(--font-body);
      }
      .signup-form button {
        background: var(--text-primary);
        color: var(--bg-primary);
        border: none;
        padding: 14px 32px;
        border-radius: 60px;
        font-weight: 700;
        font-family: var(--font-header);
        cursor: pointer;
      }
      footer {
        border-top: 1px solid var(--border-color);
        width: 100%;
        margin-top: auto;
        padding: 40px 0 30px;
      }
      .footer-middle {
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-wrap: wrap;
        gap: 20px;
        padding: 20px 0;
        border-top: 1px solid var(--border-light);
      }
      .footer-links {
        display: flex;
        gap: 24px;
        font-weight: 600;
        font-size: 12px;
      }
      .footer-bottom {
        text-align: center;
        padding: 20px 0 0;
        border-top: 1px solid var(--border-light);
        font-size: 11px;
      }
      @media (max-width: 768px) {
        .footer-middle {
          flex-direction: column;
          text-align: center;
        }
        .signup-form {
          flex-direction: column;
        }
      }
    </style>
  </head>
  <body class="dark-mode">
    <header>
      <div class="container">
        <div class="logo">
          <a
            href="https://aw-junaid.github.io/"
            title="awjunaid - Cyber Security"
            >awjunaid</a
          >
        </div>
        <div class="header-right">
          <nav class="main-nav">
            <a href="https://aw-junaid.github.io/">Home</a>
            <a href="https://aw-junaid.github.io/page/blog.html">Blog</a>
            <a href="https://aw-junaid.github.io/page/membership.html"
              >Membership</a
            >
            <div class="dropdown">
              <a href="#">Categories <i class="fa-solid fa-caret-down"></i></a>
              <div class="dropdown-content">
                <a href="https://aw-junaid.github.io/posts/cyber-security.html"
                  >Cyber Security</a
                >
                <a href="https://aw-junaid.github.io/posts/linux.html">Linux</a>
                <a href="https://aw-junaid.github.io/posts/networking.html"
                  >Networking</a
                >
                <a href="https://aw-junaid.github.io/posts/kali-linux.html"
                  >Kali Linux</a
                >
                <a href="https://aw-junaid.github.io/posts/hardware.html"
                  >Hardware</a
                >
              </div>
            </div>
          </nav>
          <div class="social-icons">
            <a href="https://github.com/aw-junaid/" target="_blank"
              ><i class="fa-brands fa-github"></i
            ></a>
            <a href="https://x.com/awjunaid_" target="_blank"
              ><i class="fa-brands fa-twitter"></i
            ></a>
            <a href="https://www.linkedin.com/in/aw-junaid/" target="_blank"
              ><i class="fa-brands fa-linkedin"></i
            ></a>
            <a href="https://www.youtube.com/@awjunaid/featured" target="_blank"
              ><i class="fa-brands fa-youtube"></i
            ></a>
            <a href="https://www.facebook.com/awjuna1d" target="_blank"
              ><i class="fa-brands fa-facebook"></i
            ></a>
            <a href="https://instagram.com/awjunaid_" target="_blank"
              ><i class="fa-brands fa-instagram"></i
            ></a>
          </div>
          <button class="theme-switcher" onclick="toggleTheme()">Invert</button>
        </div>
      </div>
    </header>

    <main>
      <div class="container">
        <!-- HERO SECTION -->
        <div class="post-hero">
          <div class="hero-image">
            <img
              src="https://raw.githubusercontent.com/aw-junaid/aw-junaid.github.io/refs/heads/main/posts/Cyber%20Security/images/A%20Comprehensive%20Program%20for%20Preventing%20and%20Detecting%20Computer%20Viruses%20A%202026%20Forensic%20Retrospective%20on%20the%20IRS%20Security%20Crisis%20of%202000.jpg"
              alt="Storage Devices Used in Networking"
            />
          </div>
          <div class="hero-content">
            <h1>Storage Devices Used in Networking </h1>
            <div class="post-meta">
              <span><i class="fa-regular fa-calendar"></i> March 25, 2026</span>
              <span><i class="fa-regular fa-clock"></i> 12 min read</span>
              <span
                ><i class="fa-solid fa-tag"></i> Linux / Privilege
                Escalation</span
              >
              <span><i class="fa-regular fa-user"></i> awjunaid</span>
            </div>
            <div class="hero-excerpt">
              Networked storage exists so that data isn't trapped on a single server's local disks — it can be shared, protected, and scaled independently of any one machine. This article surveys the storage devices and systems commonly deployed in networked environments, how they fit together, and practical guidance on setting up and managing each.


            </div>
          </div>
        </div>

        <!-- POST CONTENT - Any raw HTML pasted here gets auto-styled with copy buttons -->
        <article class="post-content">
       
<h1 id="storage-devices-used-in-networking">Storage Devices Used in Networking</h1>
<h2 id="introduction">Introduction</h2>
<p>Networked storage exists so that data isn&#39;t trapped on a single server&#39;s local disks — it can be shared, protected, and scaled independently of any one machine. This article surveys the storage devices and systems commonly deployed in networked environments, how they fit together, and practical guidance on setting up and managing each.</p>
<h2 id="the-networked-storage-landscape">The Networked Storage Landscape</h2>
<pre><code class="lang-mermaid">graph TD
    Client[Clients/Servers] --&gt; NAS[NAS: <span class="hljs-keyword">File</span>-<span class="hljs-keyword">Level</span> Storage]
    Client --&gt; SAN[SAN: <span class="hljs-keyword">Block</span>-<span class="hljs-keyword">Level</span> Storage]
    Client --&gt; Object[Object Storage: API-based]
    SAN --&gt; <span class="hljs-keyword">Array</span>[Storage <span class="hljs-keyword">Array</span> Controllers]
    NAS --&gt; Array2[NAS <span class="hljs-keyword">Head</span> + <span class="hljs-keyword">Disk</span> Shelves]
    Object --&gt; Cluster[Object Storage Cluster Nodes]
</code></pre>
<h2 id="nas-network-attached-storage-">NAS (Network Attached Storage)</h2>
<p>A NAS device is a self-contained system connected to the LAN that serves files over <strong>NFS</strong> (Linux/Unix) or <strong>SMB/CIFS</strong> (Windows), appearing to clients as ordinary shared folders.</p>
<h3 id="typical-nas-hardware-range">Typical NAS Hardware Range</h3>
<table>
<thead>
<tr>
<th>Tier</th>
<th>Example Use</th>
<th>Drive Count</th>
<th>Typical Features</th>
</tr>
</thead>
<tbody>
<tr>
<td>Consumer/SOHO</td>
<td>Home backups, media serving</td>
<td>2–4 bays</td>
<td>Basic RAID, DLNA, cloud sync</td>
</tr>
<tr>
<td>Prosumer</td>
<td>Small business file sharing</td>
<td>4–8 bays</td>
<td>Snapshots, replication, VM hosting</td>
</tr>
<tr>
<td>Enterprise</td>
<td>Department/company-wide file services</td>
<td>Dozens–hundreds</td>
<td>Clustering, tiering, deduplication, high availability</td>
</tr>
</tbody>
</table>
<h3 id="setting-up-nfs-sharing-on-a-linux-nas">Setting Up NFS Sharing on a Linux NAS</h3>
<pre><code class="lang-bash">sudo apt <span class="hljs-keyword">install</span> nfs-kernel-<span class="hljs-keyword">server</span>
sudo mkdir -p /<span class="hljs-keyword">export</span>/<span class="hljs-keyword">data</span>
sudo chown nobody:nogroup /<span class="hljs-keyword">export</span>/<span class="hljs-keyword">data</span>

echo <span class="hljs-string">"/export/data 10.0.0.0/24(rw,sync,no_subtree_check)"</span> | sudo tee -a /etc/exports
sudo exportfs -ra
sudo systemctl restart nfs-kernel-<span class="hljs-keyword">server</span>
</code></pre>
<p>Client-side mount:</p>
<pre><code class="lang-bash">sudo mount -t nfs <span class="hljs-number">10.0</span>.<span class="hljs-number">0</span>.<span class="hljs-number">60</span><span class="hljs-symbol">:/export/data</span> /mnt/data
</code></pre>
<h3 id="setting-up-samba-smb-sharing-on-linux">Setting Up Samba (SMB) Sharing on Linux</h3>
<pre><code class="lang-bash">sudo apt <span class="hljs-keyword">install</span> samba

sudo tee -a /etc/samba/smb.conf &lt;&lt; <span class="hljs-string">'EOF'</span>
[<span class="hljs-keyword">shared</span>]
<span class="hljs-keyword">path</span> = /srv/samba/<span class="hljs-keyword">shared</span>
browsable = yes
writable = yes
guest ok = <span class="hljs-keyword">no</span>
valid <span class="hljs-keyword">users</span> = @sambashare
EOF

sudo systemctl restart smbd
sudo smbpasswd -a myuser
</code></pre>
<h2 id="san-storage-area-network-devices">SAN (Storage Area Network) Devices</h2>
<p>A SAN presents block-level storage over a dedicated network (Fibre Channel or iSCSI), with each connected server treating the storage as if it were a locally attached disk. Covered in depth in the companion Storage Array and Storage Interfaces/Protocols articles — the key SAN-specific devices are:</p>
<ul>
<li><strong>Storage array controllers</strong>: Manage RAID, caching, and host connectivity.</li>
<li><strong>FC/iSCSI switches</strong>: Build the fabric or network connecting hosts to the array.</li>
<li><strong>HBAs/iSCSI initiators</strong>: The host-side connection point into the SAN.</li>
</ul>
<h2 id="tape-storage-still-relevant-for-networked-backup-">Tape Storage (Still Relevant for Networked Backup)</h2>
<p>Despite being decades old, <strong>LTO (Linear Tape-Open)</strong> tape remains widely used for long-term archival and offsite backup, due to its low cost per terabyte and strong resilience for cold, rarely-accessed data.</p>
<table>
<thead>
<tr>
<th>LTO Generation</th>
<th>Native Capacity</th>
<th>Native Speed</th>
</tr>
</thead>
<tbody>
<tr>
<td>LTO-7</td>
<td>6 TB</td>
<td>300 MB/s</td>
</tr>
<tr>
<td>LTO-8</td>
<td>12 TB</td>
<td>360 MB/s</td>
</tr>
<tr>
<td>LTO-9</td>
<td>18 TB</td>
<td>400 MB/s</td>
</tr>
</tbody>
</table>
<p>Tape libraries are typically connected via SAS or Fibre Channel and integrated with backup software that manages tape rotation, cataloging, and offsite handling.</p>
<h2 id="object-storage-nodes">Object Storage Nodes</h2>
<p>Object storage systems (covered in the Storage Array article) run across clusters of standard servers, each contributing disks to a shared, distributed pool. Data is spread and protected using <strong>erasure coding</strong> rather than traditional RAID, allowing the system to tolerate multiple node or drive failures across a large cluster.</p>
<h3 id="example-interacting-with-s3-compatible-object-storage-python-">Example: Interacting with S3-Compatible Object Storage (Python)</h3>
<pre><code class="lang-python">import <span class="hljs-keyword">boto3
</span>
<span class="hljs-built_in">s3</span> = <span class="hljs-keyword">boto3.client(
</span>    <span class="hljs-string">"s3"</span>,
    endpoint_url=<span class="hljs-string">"http://10.0.0.70:9000"</span>,
    aws_access_key_id=<span class="hljs-string">"myaccesskey"</span>,
    aws_secret_access_key=<span class="hljs-string">"mysecretkey"</span>
)

<span class="hljs-comment"># Upload a file</span>
<span class="hljs-built_in">s3</span>.upload_file(<span class="hljs-string">"backup.tar.gz"</span>, <span class="hljs-string">"my-bucket"</span>, <span class="hljs-string">"backups/backup.tar.gz"</span>)

<span class="hljs-comment"># List objects in a bucket</span>
response = <span class="hljs-built_in">s3</span>.list_objects_v2(<span class="hljs-keyword">Bucket="my-bucket")
</span>for obj in response.get(<span class="hljs-string">"Contents"</span>, []):
    print(obj[<span class="hljs-string">"Key"</span>], obj[<span class="hljs-string">"Size"</span>])
</code></pre>
<p>This example works against any S3-compatible object store (AWS S3, MinIO, Ceph RGW, etc.), illustrating the API-driven nature of object storage compared to file/block access.</p>
<h2 id="storage-devices-in-a-data-center-network-context">Storage Devices in a Data Center Network Context</h2>
<pre><code class="lang-mermaid">graph TD
    subgraph Data Center
    Compute[Server Cluster] <span class="hljs-comment">--- SANSwitch[SAN Switch Fabric]</span>
    SANSwitch <span class="hljs-comment">--- Array[Block Storage Array]</span>
    Compute <span class="hljs-comment">--- LAN[Ethernet LAN]</span>
    LAN <span class="hljs-comment">--- NASHead[NAS Head]</span>
    NASHead <span class="hljs-comment">--- Shelf[Disk Shelves]</span>
    LAN <span class="hljs-comment">--- ObjCluster[Object Storage Cluster]</span>
    <span class="hljs-keyword">Array</span> <span class="hljs-comment">--- Backup[Backup Target / Tape Library]</span>
    <span class="hljs-keyword">end</span>
</code></pre>
<h2 id="redundancy-and-high-availability-in-networked-storage">Redundancy and High Availability in Networked Storage</h2>
<table>
<thead>
<tr>
<th>Technique</th>
<th>Purpose</th>
</tr>
</thead>
<tbody>
<tr>
<td>Dual controllers</td>
<td>Survive a single controller failure</td>
</tr>
<tr>
<td>Multipathing</td>
<td>Survive a single network/fabric path failure</td>
</tr>
<tr>
<td>RAID/erasure coding</td>
<td>Survive one or more drive failures</td>
</tr>
<tr>
<td>Snapshots</td>
<td>Point-in-time recovery from logical errors (accidental deletion, corruption)</td>
</tr>
<tr>
<td>Replication</td>
<td>Survive an entire site/array failure via a secondary copy</td>
</tr>
<tr>
<td>Backup to a separate medium/location</td>
<td>Survive a catastrophic primary system loss</td>
</tr>
</tbody>
</table>
<p>Snapshots and replication protect against different failure modes than RAID — RAID protects against a drive failure, but not against someone accidentally deleting a file, which is where snapshots come in.</p>
<h2 id="practical-example-verifying-storage-connectivity-from-a-server">Practical Example: Verifying Storage Connectivity from a Server</h2>
<pre><code class="lang-bash"><span class="hljs-meta"># For iSCSI-attached storage</span>
sudo iscsiadm -m session -P <span class="hljs-number">3</span>

<span class="hljs-meta"># For NFS mounts</span>
mount | grep nfs
showmount -e <span class="hljs-number">10.0</span><span class="hljs-number">.0</span><span class="hljs-number">.60</span>

<span class="hljs-meta"># For general block device visibility</span>
lsblk
multipath -ll
</code></pre>
<h2 id="cisco-example-verifying-san-port-connectivity-for-storage">Cisco Example: Verifying SAN Port Connectivity for Storage</h2>
<pre><code><span class="hljs-keyword">Switch</span><span class="hljs-meta"># show interface fc1/1</span>
<span class="hljs-keyword">Switch</span><span class="hljs-meta"># show flogi database</span>
<span class="hljs-keyword">Switch</span><span class="hljs-meta"># show fcns database</span>
</code></pre><h2 id="best-practices">Best Practices</h2>
<ul>
<li>Match storage device type to workload: NAS for shared files, SAN for databases/VMs, object storage for backup/archive/unstructured scale.</li>
<li>Always plan redundancy at every layer — controller, network path, and drive — not just one.</li>
<li>Separate storage traffic (iSCSI, NFS) onto dedicated VLANs or physical networks where performance matters.</li>
<li>Use snapshots in addition to, not instead of, real backups — a snapshot on the same array doesn&#39;t protect against array-level failure.</li>
<li>Regularly test backup/restore procedures, not just backup completion — an untested backup is not a reliable backup.</li>
<li>Monitor capacity, performance, and error counters proactively across all networked storage devices, not just when something breaks.</li>
</ul>
<h2 id="troubleshooting">Troubleshooting</h2>
<table>
<thead>
<tr>
<th>Symptom</th>
<th>Likely Cause</th>
<th>Fix</th>
</tr>
</thead>
<tbody>
<tr>
<td>NAS share inaccessible</td>
<td>Network issue, service down, permissions</td>
<td>Check <code>showmount -e</code>, service status, share permissions</td>
</tr>
<tr>
<td>SAN LUN missing on host</td>
<td>Zoning/masking misconfiguration</td>
<td>Verify LUN masking and fabric zoning</td>
</tr>
<tr>
<td>Slow object storage uploads</td>
<td>Network bandwidth, cluster load</td>
<td>Check network path, cluster health/load metrics</td>
</tr>
<tr>
<td>Backup job fails intermittently</td>
<td>Tape/media issue, network timeout</td>
<td>Check backup software logs, verify media/network health</td>
</tr>
<tr>
<td>Snapshot consuming excessive space</td>
<td>High data churn rate</td>
<td>Review snapshot retention policy and schedule</td>
</tr>
</tbody>
</table>
<h2 id="further-reading">Further Reading</h2>
<ul>
<li><a href="https://www.snia.org/education/storage_networking_primer">SNIA Storage Networking Industry Association Education</a></li>
<li><a href="https://www.rfc-editor.org/rfc/rfc7530">RFC 7530 — NFS Version 4 Protocol</a></li>
<li><a href="https://www.samba.org/samba/docs/">Samba Project Documentation</a></li>
<li><a href="https://www.lto.org/technology/">LTO Ultrium Technology Overview</a></li>
<li><a href="https://min.io/docs/minio/linux/index.html">MinIO S3-Compatible Object Storage Documentation</a></li>
</ul>
<h2 id="conclusion">Conclusion</h2>
<p>Networked storage spans a wide spectrum — from simple file-sharing NAS boxes to high-performance SAN fabrics, tape archives, and massively scalable object storage clusters. Understanding which device type fits which workload, and building redundancy in at every layer, is what separates a resilient storage environment from one that&#39;s one failure away from a serious outage.</p>

          <div style="text-align: center; margin-top: 40px">
            <div
              class="back-to-top"
              onclick="window.scrollTo({ top: 0, behavior: 'smooth' })"
            >
              <i class="fa-solid fa-arrow-up"></i> Back to Top
            </div>
          </div>
        </article>
      </div>
    </main>

    <footer>
      <div class="container">
        <div class="email-signup">
          <h3 style="font-weight: 800">✉️ Subscribe to The Byteforge</h3>
          <p>
            Get the latest research, offensive tooling updates, and quantum
            security insights — straight to your inbox.
          </p>
          <form class="signup-form" id="emailSignupForm">
            <input
              type="email"
              placeholder="your@email.com"
              required
              id="footerEmailInput"
            /><button type="submit">Subscribe →</button>
          </form>
          <small>No spam, only quality content. Unsubscribe anytime.</small>
        </div>
        <div id="brevoFormWrapper" style="display: none">
          <div class="sib-form">
            <div id="sib-form-container">
              <div id="success-message" style="display: none"></div>
              <div id="sib-container">
                <form
                  id="sib-form"
                  method="POST"
                  action="https://a216f6cc.sibforms.com/serve/MUIFADLmiU8YhMWe2xVzsa_U0J4excsFiFMzblyZ3WldLJuuGNKShI--ZwfClHTJ5I9XUi_4mNj_CWkABuw9g7bqtdD8WP3SBNtgpg7Y8Jh90tr7vF6QXMfhiVYsQ4xgpsJLXp7-3KxedFpb-fL3Adt3kwxloiIisUHeA-4p5SaghUVMe61_3pMGLXqnuNRsIrbZ-4h5dcCN7p9O"
                >
                  <input
                    type="email"
                    id="EMAIL"
                    name="EMAIL"
                    style="display: none"
                  />
                </form>
              </div>
            </div>
          </div>
        </div>
        <div class="footer-middle">
          <div class="footer-links">
            <a href="https://aw-junaid.github.io/page/privacy.html">Privacy</a
            ><a href="https://aw-junaid.github.io/page/terms.html">T&C'S</a
            ><a href="https://aw-junaid.github.io/page/contact.html">Contact</a
            ><a href="https://aw-junaid.github.io/page/about.html">About</a
            ><a href="https://aw-junaid.github.io/page/sitemap.html"
              >Site Map</a
            >
          </div>
          <div class="social-icons">
            <a href="https://github.com/aw-junaid/" target="_blank"
              ><i class="fa-brands fa-github"></i
            ></a>
            <a href="https://x.com/awjunaid_" target="_blank"
              ><i class="fa-brands fa-twitter"></i
            ></a>
            <a href="https://www.linkedin.com/in/aw-junaid/" target="_blank"
              ><i class="fa-brands fa-linkedin"></i
            ></a>
            <a href="https://www.youtube.com/@awjunaid/featured" target="_blank"
              ><i class="fa-brands fa-youtube"></i
            ></a>
            <a href="https://www.facebook.com/awjuna1d" target="_blank"
              ><i class="fa-brands fa-facebook"></i
            ></a>
            <a href="https://instagram.com/awjunaid_" target="_blank"
              ><i class="fa-brands fa-instagram"></i
            ></a>
          </div>
        </div>
        <div class="footer-bottom">
          &copy; 2026 AWJUNAID.COM | All Rights Reserved
        </div>
      </div>
    </footer>

    <script>
      // Theme toggle
      function toggleTheme() {
        document.body.classList.toggle("dark-mode");
        localStorage.setItem(
          "theme",
          document.body.classList.contains("dark-mode") ? "dark" : "light",
        );
      }
      window.addEventListener("load", () => {
        if (localStorage.getItem("theme") === "light")
          document.body.classList.remove("dark-mode");
        // Auto-wrap all pre elements with copy buttons
        addCopyButtonsToCodeBlocks();
      });

      // GLOBAL FUNCTION: Automatically adds copy buttons to every pre element inside .post-content
      function addCopyButtonsToCodeBlocks() {
        const postContent = document.querySelector(".post-content");
        if (!postContent) return;

        const preElements = postContent.querySelectorAll("pre");
        preElements.forEach((pre) => {
          // Skip if already wrapped
          if (
            pre.parentElement.classList &&
            pre.parentElement.classList.contains("code-wrapper")
          )
            return;

          // Create wrapper
          const wrapper = document.createElement("div");
          wrapper.className = "code-wrapper";

          // Create copy button
          const copyBtn = document.createElement("button");
          copyBtn.className = "copy-code-btn";
          copyBtn.innerHTML = '<i class="fa-regular fa-copy"></i> Copy';
          copyBtn.onclick = function () {
            const code = pre.innerText;
            navigator.clipboard
              .writeText(code)
              .then(() => {
                copyBtn.innerHTML =
                  '<i class="fa-regular fa-check"></i> Copied!';
                setTimeout(() => {
                  copyBtn.innerHTML = '<i class="fa-regular fa-copy"></i> Copy';
                }, 2000);
              })
              .catch(() => {
                copyBtn.innerHTML = '<i class="fa-solid fa-xmark"></i> Error';
                setTimeout(() => {
                  copyBtn.innerHTML = '<i class="fa-regular fa-copy"></i> Copy';
                }, 1500);
              });
          };

          // Wrap the pre element
          pre.parentNode.insertBefore(wrapper, pre);
          wrapper.appendChild(pre);
          wrapper.appendChild(copyBtn);
        });
      }

      // Email subscription preserved
      document
        .getElementById("emailSignupForm")
        .addEventListener("submit", function (e) {
          e.preventDefault();
          const email = document.getElementById("footerEmailInput").value;
          const brevoEmail = document.getElementById("EMAIL");
          if (email && brevoEmail) {
            brevoEmail.value = email;
            const sibForm = document.getElementById("sib-form");
            if (sibForm) sibForm.submit();
            setTimeout(() => this.reset(), 500);
          } else {
            alert("Please enter a valid email for subscription.");
          }
        });

      window.REQUIRED_CODE_ERROR_MESSAGE = "Please choose a country code";
      window.LOCALE = "en";
      var AUTOHIDE = Boolean(0);

      // Re-run copy button addition after dynamic content loads (MathJax may affect)
      if (window.MathJax) {
        MathJax.startup.promise.then(() => {
          setTimeout(addCopyButtonsToCodeBlocks, 100);
        });
      }
    </script>
    <script
      defer
      src="https://sibforms.com/forms/end-form/build/main.js"
    ></script>
  </body>
</html>
