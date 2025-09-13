<html lang="vi">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>AIM PANEL</title>
<style>
  :root{
    --card-bg: rgba(0,0,0,0.55);
    --accent: #6ee7b7;
    --muted: rgba(255,255,255,0.85);
    --glass: rgba(255,255,255,0.06);
    --shadow: 0 6px 18px rgba(0,0,0,0.45);
  }

  html,body{
    height:100%;
    margin:0;
    font-family: Inter, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    color:var(--muted);
    background: #0b1020;
  }

  /* background "đường nối" svg */
  .bg-wrap{
    position:fixed;
    inset:0;
    z-index:-1;
    overflow:hidden;
  }
  .bg-svg{
    width:100%;
    height:100%;
    display:block;
    object-fit:cover;
    opacity:0.95;
    filter:drop-shadow(0 10px 20px rgba(0,0,0,0.6));
  }

  /* container */
  .container{
    min-height:100vh;
    display:flex;
    align-items:center;
    justify-content:center;
    padding:40px;
    box-sizing:border-box;
  }

  .panel{
    width:100%;
    max-width:760px;
    background: linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.02));
    border-radius:14px;
    padding:22px;
    box-shadow:var(--shadow);
    border:1px solid rgba(255,255,255,0.04);
    backdrop-filter: blur(6px) saturate(120%);
  }

  .panel-header{
    display:flex;
    align-items:center;
    justify-content:space-between;
    gap:12px;
    margin-bottom:18px;
  }

  .title{
    font-weight:700;
    font-size:18px;
    letter-spacing:0.6px;
  }
  .sub{
    font-size:13px;
    opacity:0.8;
  }

  .list{
    display:grid;
    grid-template-columns:1fr;
    gap:10px;
  }

  .item{
    display:flex;
    align-items:center;
    justify-content:space-between;
    background:var(--card-bg);
    padding:12px 14px;
    border-radius:10px;
    border:1px solid rgba(255,255,255,0.03);
  }

  .item-left{
    display:flex;
    align-items:center;
    gap:12px;
  }

  .dot{
    width:10px;
    height:10px;
    border-radius:50%;
    background: rgba(255,255,255,0.08);
    box-shadow: 0 0 8px rgba(0,0,0,0.6) inset;
  }

  .label{
    font-size:15px;
    font-weight:600;
    letter-spacing:0.2px;
  }
  .desc{
    font-size:12px;
    opacity:0.7;
    margin-top:2px;
  }

  /* switch style (checkbox-like) */
  .switch{
    --w:48px;
    --h:26px;
    width:var(--w);
    height:var(--h);
    background: rgba(255,255,255,0.06);
    border-radius:100px;
    position:relative;
    box-sizing:border-box;
    padding:3px;
    transition: background .18s ease;
    cursor:pointer;
    display:inline-block;
  }
  .switch .knob{
    width:calc(var(--h) - 6px);
    height:calc(var(--h) - 6px);
    border-radius:50%;
    background:white;
    transform:translateX(0);
    transition: transform .18s cubic-bezier(.2,.9,.2,1), box-shadow .15s;
    box-shadow:0 3px 8px rgba(0,0,0,0.35);
  }
  .switch.on{
    background: linear-gradient(90deg, rgba(110,231,183,0.18), rgba(86,190,238,0.12));
  }
  .switch.on .knob{
    transform:translateX(calc(var(--w) - var(--h)));
    background:linear-gradient(180deg,var(--accent), #4fd0ff);
    box-shadow: 0 6px 18px rgba(54,199,173,0.22), 0 2px 6px rgba(0,0,0,0.35);
  }

  /* small active badge */
  .active-badge{
    display:inline-block;
    font-size:11px;
    padding:4px 8px;
    border-radius:999px;
    background: rgba(110,231,183,0.08);
    color:var(--accent);
    font-weight:700;
    border:1px solid rgba(110,231,183,0.08);
    margin-left:10px;
  }

  /* mobile tweaks */
  @media (max-width:520px){
    .panel{ padding:14px; }
    .label{ font-size:14px; }
    .switch{ --w:42px; --h:22px; }
  }

  /* small helper text bottom */
  .hint{
    margin-top:12px;
    font-size:13px;
    opacity:0.7;
  }

  /* focus styles */
  .switch:focus, .switch:focus-visible{
    outline:2px solid rgba(255,255,255,0.06);
    outline-offset:3px;
  }
</style>
</head>
<body>
  <div class="bg-wrap" aria-hidden="true">
    <!-- Inline SVG background: nodes with connecting lines (nền dạng đường nối) -->
    <svg class="bg-svg" viewBox="0 0 1200 800" preserveAspectRatio="xMidYMid slice" xmlns="http://www.w3.org/2000/svg">
      <defs>
        <linearGradient id="g1" x1="0" x2="1"><stop offset="0" stop-color="#05263b"/><stop offset="1" stop-color="#08172a"/></linearGradient>
        <filter id="blurMe"><feGaussianBlur stdDeviation="20" /></filter>
      </defs>
      <rect width="100%" height="100%" fill="url(#g1)" />
      <!-- soft glows -->
      <g opacity="0.08" filter="url(#blurMe)">
        <circle cx="180" cy="120" r="120" fill="#0e4b6b"/>
        <circle cx="1000" cy="560" r="140" fill="#113b2f"/>
        <circle cx="840" cy="140" r="100" fill="#1b2b5a"/>
      </g>

      <!-- connections -->
      <g stroke="rgba(255,255,255,0.06)" stroke-width="1.4" fill="none" stroke-linecap="round">
        <path d="M120 150 C 200 120, 260 90, 360 110 S 600 200, 800 140" />
        <path d="M220 420 C 300 380, 420 360, 540 410 S 800 520, 1020 480" />
        <path d="M420 70 C 520 30, 660 20, 760 80" />
        <path d="M980 280 C 920 220, 840 190, 760 200" />
        <path d="M300 620 C 420 560, 560 540, 720 600" />
      </g>

      <!-- nodes -->
      <g>
        <!-- each node: outer ring + inner glow -->
        <g transform="translate(120,150)">
          <circle r="6" fill="#9be7d3"/>
          <circle r="14" fill="none" stroke="rgba(155,231,211,0.08)"/>
        </g>
        <g transform="translate(360,110)">
          <circle r="5" fill="#7fd1f5"/>
          <circle r="11" fill="none" stroke="rgba(127,209,245,0.07)"/>
        </g>
        <g transform="translate(800,140)">
          <circle r="6" fill="#82c7ff"/>
          <circle r="14" fill="none" stroke="rgba(130,199,255,0.06)"/>
        </g>
        <g transform="translate(220,420)">
          <circle r="6" fill="#ffd48a"/>
          <circle r="14" fill="none" stroke="rgba(255,212,138,0.06)"/>
        </g>
        <g transform="translate(540,410)">
          <circle r="7" fill="#6ee7b7"/>
          <circle r="16" fill="none" stroke="rgba(110,231,183,0.06)"/>
        </g>
        <g transform="translate(1020,480)">
          <circle r="6" fill="#a7b8ff"/>
          <circle r="14" fill="none" stroke="rgba(167,184,255,0.06)"/>
        </g>
        <g transform="translate(420,70)">
          <circle r="5" fill="#ff9ab9"/>
          <circle r="11" fill="none" stroke="rgba(255,154,185,0.05)"/>
        </g>
        <g transform="translate(980,280)">
          <circle r="6" fill="#9be7d3"/>
          <circle r="14" fill="none" stroke="rgba(155,231,211,0.05)"/>
        </g>
        <g transform="translate(300,620)">
          <circle r="6" fill="#7fd1f5"/>
          <circle r="14" fill="none" stroke="rgba(127,209,245,0.04)"/>
        </g>
        <g transform="translate(720,600)">
          <circle r="6" fill="#82c7ff"/>
          <circle r="14" fill="none" stroke="rgba(130,199,255,0.04)"/>
        </g>
      </g>

      <!-- subtle moving lines (animated) -->
      <g stroke="rgba(255,255,255,0.03)" stroke-width="1" fill="none">
        <path id="p1" d="M50 700 C 250 650, 450 680, 650 620" stroke-linecap="round"/>
        <path id="p2" d="M1000 50 C 820 120, 640 80, 480 130" stroke-linecap="round"/>
      </g>
    </svg>
  </div>

  <div class="container">
    <div class="panel" role="region" aria-label="AIM toggle panel">
      <div class="panel-header">
        <div>
          <div class="title">AIM TOGGLES</div>
          <div class="sub">Nền: đường nối — Chỉ 1 mục bật cùng lúc. Bấm lần nữa để tắt.</div>
        </div>
        <div class="active-summary" aria-live="polite"></div>
      </div>

      <div class="list" id="toggleList">
        <!-- We'll generate items here via HTML for clarity -->
        <div class="item">
          <div class="item-left">
            <div class="dot" aria-hidden="true"></div>
            <div>
              <div class="label">AIMLOCK</div>
            </div>
          </div>
          <div>
            <button class="switch" role="switch" aria-checked="false" data-id="1" tabindex="0">
              <span class="knob" aria-hidden="true"></span>
            </button>
          </div>
        </div>

        <div class="item">
          <div class="item-left">
            <div class="dot"></div>
            <div>
              <div class="label">AIM</div>
            </div>
          </div>
          <div>
            <button class="switch" role="switch" aria-checked="false" data-id="2" tabindex="0">
              <span class="knob" aria-hidden="true"></span>
            </button>
          </div>
        </div>

        <div class="item">
          <div class="item-left">
            <div class="dot"></div>
            <div>
              <div class="label">AIM NECK 60%</div>
            </div>
          </div>
          <div>
            <button class="switch" role="switch" aria-checked="false" data-id="3" tabindex="0">
              <span class="knob" aria-hidden="true"></span>
            </button>
          </div>
        </div>

        <div class="item">
          <div class="item-left">
            <div class="dot"></div>
            <div>
              <div class="label">AIM CHEST VIP</div>
            </div>
          </div>
          <div>
            <button class="switch" role="switch" aria-checked="false" data-id="4" tabindex="0">
              <span class="knob" aria-hidden="true"></span>
            </button>
          </div>
        </div>

        <div class="item">
          <div class="item-left">
            <div class="dot"></div>
            <div>
              <div class="label">AIMBODY</div>
            </div>
          </div>
          <div>
            <button class="switch" role="switch" aria-checked="false" data-id="5" tabindex="0">
              <span class="knob" aria-hidden="true"></span>
            </button>
          </div>
        </div>

        <div class="item">
          <div class="item-left">
            <div class="dot"></div>
            <div>
              <div class="label">AIM BỤNG</div>
            </div>
          </div>
          <div>
            <button class="switch" role="switch" aria-checked="false" data-id="6" tabindex="0">
              <span class="knob" aria-hidden="true"></span>
            </button>
          </div>
        </div>

        <div class="item">
          <div class="item-left">
            <div class="dot"></div>
            <div>
              <div class="label">GIẢM LỰC CẢN</div>
            </div>
          </div>
          <div>
            <button class="switch" role="switch" aria-checked="false" data-id="7" tabindex="0">
              <span class="knob" aria-hidden="true"></span>
            </button>
          </div>
        </div>

        <div class="item">
          <div class="item-left">
            <div class="dot"></div>
            <div>
              <div class="label">AIMBODY + ĐỊNH VỊ GUNS</div>
            </div>
          </div>
          <div>
            <button class="switch" role="switch" aria-checked="false" data-id="8" tabindex="0">
              <span class="knob" aria-hidden="true"></span>
            </button>
          </div>
        </div>

        <div class="item">
          <div class="item-left">
            <div class="dot"></div>
            <div>
              <div class="label">AIMBỤNG + ĐỊNH VỊ GUNS</div>
            </div>
          </div>
          <div>
            <button class="switch" role="switch" aria-checked="false" data-id="9" tabindex="0">
              <span class="knob" aria-hidden="true"></span>
            </button>
          </div>
        </div>

        <div class="item">
          <div class="item-left">
            <div class="dot"></div>
            <div>
              <div class="label">ĐỊNH VỊ</div>
            </div>
          </div>
          <div>
            <button class="switch" role="switch" aria-checked="false" data-id="10" tabindex="0">
              <span class="knob" aria-hidden="true"></span>
            </button>
          </div>
        </div>

      </div>

      <div class="hint">Lưu ý: chỉ 1 mục được bật cùng lúc. Bấm mục đang bật để tắt.</div>
    </div>
  </div>

<script>
  // JS: chỉ cho phép 1 switch ON cùng lúc; người dùng có thể tắt switch hiện tại bằng bấm lại.
  (function(){
    const switches = Array.from(document.querySelectorAll('.switch'));
    const summary = document.querySelector('.active-summary');

    function updateSummary(activeId, labelText){
      if (!summary) return;
      summary.innerHTML = activeId ? ('<span class="active-badge">ON: ' + labelText + '</span>') : '';
    }

    // helper: turn off all except optionally one
    function setActive(exceptId){
      switches.forEach(btn=>{
        const id = btn.getAttribute('data-id');
        if (id === exceptId) return;
        btn.classList.remove('on');
        btn.setAttribute('aria-checked', 'false');
      });
    }

    switches.forEach(btn=>{
      btn.addEventListener('click', (e)=>{
        const isOn = btn.classList.contains('on');
        const id = btn.getAttribute('data-id');
        const label = btn.closest('.item').querySelector('.label').textContent.trim();

        if (isOn){
          // bấm vào cái đang bật => tắt nó
          btn.classList.remove('on');
          btn.setAttribute('aria-checked', 'false');
          updateSummary(null, null);
        } else {
          // bật cái này và tắt tất cả cái khác
          setActive(id);
          btn.classList.add('on');
          btn.setAttribute('aria-checked', 'true');
          updateSummary(id, label);
        }
      });

      // keyboard accessibility: Space / Enter toggles
      btn.addEventListener('keydown', (e)=>{
        if (e.key === ' ' || e.key === 'Enter'){
          e.preventDefault();
          btn.click();
        }
      });
    });

    // initialize none active
    updateSummary(null,null);
  })();
</script>
</body>
</html>
