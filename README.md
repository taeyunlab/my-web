<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Voice Studio — AI 번역 & TTS</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css">
<style>
:root {
  --bg: #09090f;
  --bg2: #111118;
  --bg3: #16161f;
  --bg4: #1c1c28;
  --border: rgba(255,255,255,0.07);
  --border2: rgba(255,255,255,0.12);
  --accent: #7c6cfa;
  --accent2: #a89cff;
  --accent3: #c4baff;
  --text: #f0eeff;
  --text2: #9b97b8;
  --text3: #5c5878;
  --green: #4ade80;
  --pink: #f472b6;
  --font-head: 'Syne', sans-serif;
  --font-body: 'DM Sans', sans-serif;
  --r: 12px;
  --r-sm: 8px;
}
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--font-body);
  min-height: 100vh;
  overflow-x: hidden;
}
 
/* NAV */
nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 100;
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 2rem; height: 60px;
  background: rgba(9,9,15,0.85);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border);
}
.nav-logo {
  display: flex; align-items: center; gap: 10px;
  font-family: var(--font-head); font-size: 18px; font-weight: 700; color: var(--text);
  text-decoration: none;
}
.nav-logo-icon {
  width: 32px; height: 32px; background: var(--accent);
  border-radius: 8px; display: flex; align-items: center; justify-content: center;
}
.nav-logo-icon i { font-size: 18px; color: #fff; }
.nav-badge {
  font-size: 10px; padding: 3px 8px; border-radius: 20px;
  background: rgba(124,108,250,0.15); color: var(--accent2);
  border: 1px solid rgba(124,108,250,0.25); font-family: var(--font-body);
}
.nav-links { display: flex; gap: 2rem; }
.nav-links a { color: var(--text2); text-decoration: none; font-size: 14px; transition: color .2s; }
.nav-links a:hover { color: var(--text); }
 
/* HERO */
.hero {
  padding: 140px 2rem 80px;
  text-align: center;
  position: relative;
  overflow: hidden;
}
.hero::before {
  content: '';
  position: absolute; top: 0; left: 50%; transform: translateX(-50%);
  width: 600px; height: 400px;
  background: radial-gradient(ellipse, rgba(124,108,250,0.18) 0%, transparent 70%);
  pointer-events: none;
}
.hero-eyebrow {
  display: inline-flex; align-items: center; gap: 8px;
  font-size: 12px; letter-spacing: .12em; text-transform: uppercase;
  color: var(--accent2); padding: 6px 14px;
  border: 1px solid rgba(124,108,250,0.3); border-radius: 20px;
  margin-bottom: 2rem;
  animation: fadeUp .6s ease both;
}
.hero h1 {
  font-family: var(--font-head); font-size: clamp(42px, 6vw, 80px);
  font-weight: 800; line-height: 1.05; letter-spacing: -.02em;
  color: var(--text); margin-bottom: 1.25rem;
  animation: fadeUp .6s .1s ease both;
}
.hero h1 span { color: var(--accent); }
.hero-sub {
  font-size: 18px; color: var(--text2); max-width: 520px; margin: 0 auto 2.5rem;
  line-height: 1.7; animation: fadeUp .6s .2s ease both;
}
.hero-cta {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 13px 28px; background: var(--accent); color: #fff;
  border: none; border-radius: var(--r); font-size: 15px; font-weight: 500;
  cursor: pointer; text-decoration: none; font-family: var(--font-body);
  transition: opacity .2s, transform .2s;
  animation: fadeUp .6s .3s ease both;
}
.hero-cta:hover { opacity: .88; transform: translateY(-1px); }
.hero-cta i { font-size: 18px; }
 
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(16px); }
  to   { opacity: 1; transform: translateY(0); }
}
 
/* WAVE VISUAL */
.wave-wrap {
  display: flex; justify-content: center; align-items: center; gap: 3px;
  margin: 3rem auto 0; height: 48px; animation: fadeUp .6s .4s ease both;
}
.wave-bar {
  width: 3px; border-radius: 3px; background: var(--accent);
  opacity: .5; animation: wave 1.4s ease-in-out infinite;
}
.wave-bar:nth-child(1){height:12px;animation-delay:0s}
.wave-bar:nth-child(2){height:22px;animation-delay:.1s}
.wave-bar:nth-child(3){height:36px;animation-delay:.2s}
.wave-bar:nth-child(4){height:48px;animation-delay:.3s;opacity:.9}
.wave-bar:nth-child(5){height:36px;animation-delay:.4s}
.wave-bar:nth-child(6){height:22px;animation-delay:.5s}
.wave-bar:nth-child(7){height:12px;animation-delay:.6s}
@keyframes wave {
  0%,100%{transform:scaleY(1)} 50%{transform:scaleY(1.5)}
}
 
/* MAIN APP */
.container { max-width: 900px; margin: 0 auto; padding: 0 1.5rem; }
.app-section { padding: 2rem 0 5rem; }
 
.section-chip {
  display: inline-block; font-size: 11px; font-weight: 500;
  letter-spacing: .1em; text-transform: uppercase; color: var(--accent2);
  padding: 4px 12px; border-radius: 20px;
  background: rgba(124,108,250,0.1); border: 1px solid rgba(124,108,250,0.2);
  margin-bottom: 1.25rem;
}
 
/* VOICE CARDS */
.voice-section-head {
  display: flex; align-items: center; justify-content: space-between;
  margin-bottom: 1rem;
}
.voice-section-head h3 { font-family: var(--font-head); font-size: 15px; font-weight: 600; color: var(--text); }
.voice-count { font-size: 12px; color: var(--text3); }
 
.voice-grid {
  display: grid; grid-template-columns: repeat(auto-fill, minmax(155px,1fr));
  gap: 10px; margin-bottom: 1.5rem;
}
.voice-card {
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: var(--r); padding: 14px; cursor: pointer;
  transition: border-color .2s, background .2s, transform .15s;
}
.voice-card:hover { border-color: var(--border2); background: var(--bg3); transform: translateY(-1px); }
.voice-card.active {
  border-color: var(--accent); background: rgba(124,108,250,0.1);
}
.vc-top { display: flex; align-items: center; gap: 8px; margin-bottom: 6px; }
.vc-av {
  width: 28px; height: 28px; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 15px; flex-shrink: 0;
}
.vc-name { font-family: var(--font-head); font-size: 13px; font-weight: 600; color: var(--text); }
.vc-desc { font-size: 11px; color: var(--text3); margin-bottom: 8px; line-height: 1.4; }
.vc-tag {
  font-size: 10px; padding: 2px 8px; border-radius: 20px;
  background: var(--bg4); color: var(--text2); border: 1px solid var(--border);
  display: inline-block;
}
.voice-card.active .vc-tag { background: rgba(124,108,250,0.2); color: var(--accent2); border-color: rgba(124,108,250,0.3); }
 
/* EMOTIONS */
.emotion-row { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 1.75rem; }
.emotion-btn {
  padding: 6px 14px; border: 1px solid var(--border2);
  border-radius: 20px; background: transparent; font-size: 13px;
  color: var(--text2); cursor: pointer; font-family: var(--font-body);
  transition: all .15s;
}
.emotion-btn:hover { border-color: var(--accent); color: var(--accent2); }
.emotion-btn.active { background: var(--accent); border-color: var(--accent); color: #fff; }
 
/* KNOBS */
.knobs-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 1.75rem; }
.knob-card { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r-sm); padding: 12px 14px; }
.knob-top { display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px; }
.knob-label { font-size: 12px; color: var(--text3); display: flex; align-items: center; gap: 5px; }
.knob-label i { font-size: 13px; }
.knob-val { font-size: 12px; font-weight: 500; color: var(--accent2); }
input[type=range] {
  width: 100%; -webkit-appearance: none; height: 4px;
  background: var(--bg4); border-radius: 2px; outline: none; cursor: pointer;
}
input[type=range]::-webkit-slider-thumb {
  -webkit-appearance: none; width: 16px; height: 16px; border-radius: 50%;
  background: var(--accent); cursor: pointer; transition: transform .15s;
}
input[type=range]::-webkit-slider-thumb:hover { transform: scale(1.2); }
 
/* LANG ROW */
.lang-row { display: flex; gap: 8px; align-items: center; margin-bottom: 1rem; }
select {
  flex: 1; padding: 10px 12px; font-size: 13px;
  border: 1px solid var(--border2); border-radius: var(--r-sm);
  background: var(--bg2); color: var(--text); cursor: pointer;
  font-family: var(--font-body); outline: none; appearance: none;
  transition: border-color .15s;
}
select:hover { border-color: var(--accent); }
.swap-btn {
  width: 38px; height: 38px; border: 1px solid var(--border2);
  border-radius: var(--r-sm); background: var(--bg2); color: var(--text2);
  display: flex; align-items: center; justify-content: center;
  cursor: pointer; transition: all .15s; flex-shrink: 0;
}
.swap-btn:hover { border-color: var(--accent); color: var(--accent2); }
.swap-btn i { font-size: 16px; }
 
/* TEXT PANELS */
.text-panels { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 1rem; }
.t-panel {
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: var(--r); overflow: hidden; transition: border-color .2s;
}
.t-panel:focus-within { border-color: var(--border2); }
.t-panel-head {
  display: flex; align-items: center; justify-content: space-between;
  padding: 10px 14px 0;
}
.t-panel-label { font-size: 11px; font-weight: 500; color: var(--text3); letter-spacing: .08em; text-transform: uppercase; }
.char-count { font-size: 11px; color: var(--text3); }
textarea {
  width: 100%; height: 130px; padding: 10px 14px;
  font-size: 14px; color: var(--text); background: transparent;
  border: none; outline: none; resize: none;
  font-family: var(--font-body); line-height: 1.65;
}
textarea::placeholder { color: var(--text3); }
.t-result { min-height: 130px; padding: 10px 14px; font-size: 14px; color: var(--text); line-height: 1.65; }
.t-placeholder { color: var(--text3); }
.panel-foot {
  display: flex; justify-content: flex-end; gap: 6px;
  padding: 8px 10px; border-top: 1px solid var(--border);
}
.icon-btn {
  display: flex; align-items: center; gap: 5px; padding: 5px 11px;
  border: 1px solid var(--border2); border-radius: var(--r-sm);
  background: transparent; font-size: 12px; color: var(--text2);
  cursor: pointer; font-family: var(--font-body); transition: all .15s;
}
.icon-btn:hover { border-color: var(--accent); color: var(--accent2); }
.icon-btn i { font-size: 14px; }
.icon-btn.playing { background: var(--accent); border-color: var(--accent); color: #fff; }
 
/* ACTION ROW */
.action-row { display: flex; gap: 10px; margin-bottom: 1.25rem; }
.main-btn {
  flex: 1; padding: 12px; background: var(--accent); color: #fff;
  border: none; border-radius: var(--r); font-size: 14px; font-weight: 500;
  cursor: pointer; display: flex; align-items: center; justify-content: center;
  gap: 8px; font-family: var(--font-body); transition: opacity .15s, transform .15s;
}
.main-btn:hover { opacity: .88; transform: translateY(-1px); }
.main-btn:disabled { opacity: .4; cursor: not-allowed; transform: none; }
.sec-btn {
  padding: 12px 16px; border: 1px solid var(--border2);
  border-radius: var(--r); background: transparent; color: var(--text2);
  font-size: 13px; cursor: pointer; display: flex; align-items: center;
  gap: 6px; font-family: var(--font-body); transition: all .15s;
}
.sec-btn:hover { border-color: var(--border2); background: var(--bg3); }
.sec-btn i { font-size: 15px; }
 
/* BIG PLAY */
.play-strip {
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: var(--r); padding: 14px 18px;
  display: flex; align-items: center; gap: 14px; margin-bottom: 1rem;
  cursor: pointer; transition: border-color .2s;
}
.play-strip:hover { border-color: var(--border2); }
.play-strip.playing { border-color: var(--accent); background: rgba(124,108,250,0.06); }
.play-circle {
  width: 42px; height: 42px; border-radius: 50%;
  background: var(--bg4); border: 1px solid var(--border2);
  display: flex; align-items: center; justify-content: center;
  flex-shrink: 0; transition: all .2s;
}
.play-strip.playing .play-circle { background: var(--accent); border-color: var(--accent); }
.play-circle i { font-size: 18px; color: var(--text2); }
.play-strip.playing .play-circle i { color: #fff; }
.play-info { flex: 1; }
.play-title { font-size: 14px; font-weight: 500; color: var(--text); margin-bottom: 2px; }
.play-sub { font-size: 12px; color: var(--text3); }
.play-speed { font-size: 12px; color: var(--accent2); font-weight: 500; }
 
/* SUBTITLE */
.sub-box {
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: var(--r); padding: 16px 20px; margin-bottom: 1rem;
  display: none;
}
.sub-box.show { display: block; }
.sub-head { display: flex; align-items: center; gap: 7px; font-size: 11px; color: var(--text3); letter-spacing: .08em; text-transform: uppercase; margin-bottom: 10px; }
.sub-dot { width: 6px; height: 6px; border-radius: 50%; background: var(--accent); animation: pulse 1.2s infinite; }
@keyframes pulse { 0%,100%{opacity:1} 50%{opacity:.2} }
.sub-content { font-size: 16px; color: var(--text); line-height: 1.8; min-height: 28px; }
.w-hi { background: rgba(124,108,250,0.25); color: var(--accent3); border-radius: 4px; padding: 0 4px; }
 
/* SPINNER */
.spin {
  display: inline-block; width: 14px; height: 14px;
  border: 2px solid rgba(255,255,255,.2); border-top-color: #fff;
  border-radius: 50%; animation: sp .7s linear infinite;
}
@keyframes sp { to { transform: rotate(360deg); } }
 
/* FEATURES */
.features { padding: 4rem 0; border-top: 1px solid var(--border); }
.features-title { font-family: var(--font-head); font-size: 28px; font-weight: 700; color: var(--text); margin-bottom: 2.5rem; text-align: center; }
.features-grid { display: grid; grid-template-columns: repeat(3,1fr); gap: 16px; }
.feature-card {
  background: var(--bg2); border: 1px solid var(--border);
  border-radius: var(--r); padding: 20px;
  transition: border-color .2s, transform .2s;
}
.feature-card:hover { border-color: var(--border2); transform: translateY(-2px); }
.feat-icon {
  width: 36px; height: 36px; border-radius: var(--r-sm);
  background: rgba(124,108,250,0.12); border: 1px solid rgba(124,108,250,0.2);
  display: flex; align-items: center; justify-content: center;
  margin-bottom: 12px;
}
.feat-icon i { font-size: 18px; color: var(--accent2); }
.feat-title { font-family: var(--font-head); font-size: 14px; font-weight: 600; color: var(--text); margin-bottom: 6px; }
.feat-desc { font-size: 13px; color: var(--text3); line-height: 1.6; }
 
/* FOOTER */
footer {
  border-top: 1px solid var(--border); padding: 2rem;
  text-align: center; font-size: 12px; color: var(--text3);
}
footer span { color: var(--accent2); }
 
/* DIVIDER */
.divider { height: 1px; background: var(--border); margin: 2rem 0; }
 
/* SECTION TITLE */
.s-title { font-family: var(--font-head); font-size: 15px; font-weight: 600; color: var(--text); margin-bottom: 1rem; }
 
/* NOTICE */
.voice-notice { font-size: 11px; color: var(--text3); margin-top: .5rem; }
 
@media (max-width: 600px) {
  .text-panels { grid-template-columns: 1fr; }
  .knobs-grid { grid-template-columns: 1fr; }
  .features-grid { grid-template-columns: 1fr; }
  .nav-links { display: none; }
  .hero h1 { font-size: 38px; }
}
</style>
</head>
<body>
 
<nav>
  <a class="nav-logo" href="#">
    <div class="nav-logo-icon"><i class="ti ti-waveform"></i></div>
    Voice Studio
  </a>
  <div class="nav-links">
    <a href="#app">번역기</a>
    <a href="#features">기능</a>
  </div>
  <span class="nav-badge">브라우저 TTS</span>
</nav>
 
<section class="hero">
  <div class="hero-eyebrow"><i class="ti ti-sparkles"></i> AI 번역 + TTS 통합 도구</div>
  <h1>목소리로 듣는<br><span>언어 번역기</span></h1>
  <p class="hero-sub">8가지 목소리 프리셋과 감정 조절로 더 자연스럽게. 번역과 동시에 영어 자막으로 확인하세요.</p>
  <a href="#app" class="hero-cta"><i class="ti ti-player-play"></i> 지금 시작하기</a>
  <div class="wave-wrap">
    <div class="wave-bar"></div><div class="wave-bar"></div><div class="wave-bar"></div>
    <div class="wave-bar"></div><div class="wave-bar"></div><div class="wave-bar"></div>
    <div class="wave-bar"></div>
  </div>
</section>
 
<section class="app-section" id="app">
<div class="container">
 
  <div class="section-chip">목소리 선택</div>
  <div class="voice-section-head">
    <h3 class="s-title" style="margin:0">프리셋</h3>
    <span class="voice-count" id="voiceNotice">목소리 불러오는 중...</span>
  </div>
  <div class="voice-grid" id="voiceGrid"></div>
 
  <div class="section-chip">감정 / 톤</div>
  <div class="emotion-row" id="emotionRow">
    <button class="emotion-btn active" data-e="neutral">보통</button>
    <button class="emotion-btn" data-e="warm">따뜻하게</button>
    <button class="emotion-btn" data-e="excited">신나게</button>
    <button class="emotion-btn" data-e="calm">차분하게</button>
    <button class="emotion-btn" data-e="serious">진지하게</button>
    <button class="emotion-btn" data-e="friendly">친근하게</button>
  </div>
 
  <div class="section-chip">세부 조절</div>
  <div class="knobs-grid">
    <div class="knob-card">
      <div class="knob-top"><span class="knob-label"><i class="ti ti-player-play"></i> 속도</span><span class="knob-val" id="rateVal">1.0x</span></div>
      <input type="range" min="0.5" max="2" step="0.1" value="1" id="rateSlider">
    </div>
    <div class="knob-card">
      <div class="knob-top"><span class="knob-label"><i class="ti ti-arrows-vertical"></i> 음높이</span><span class="knob-val" id="pitchVal">1.0</span></div>
      <input type="range" min="0.5" max="2" step="0.1" value="1" id="pitchSlider">
    </div>
    <div class="knob-card">
      <div class="knob-top"><span class="knob-label"><i class="ti ti-volume"></i> 볼륨</span><span class="knob-val" id="volVal">100%</span></div>
      <input type="range" min="0" max="1" step="0.05" value="1" id="volSlider">
    </div>
    <div class="knob-card">
      <div class="knob-top"><span class="knob-label"><i class="ti ti-clock"></i> 문장 간격</span><span class="knob-val" id="pauseVal">보통</span></div>
      <input type="range" min="0" max="2" step="1" value="1" id="pauseSlider">
    </div>
  </div>
 
  <div class="section-chip">언어 설정</div>
  <div class="lang-row">
    <select id="srcLang">
      <option value="ko">🇰🇷 한국어</option>
      <option value="ja">🇯🇵 일본어</option>
      <option value="zh">🇨🇳 중국어</option>
      <option value="fr">🇫🇷 프랑스어</option>
      <option value="de">🇩🇪 독일어</option>
      <option value="es">🇪🇸 스페인어</option>
      <option value="en">🇺🇸 영어</option>
      <option value="it">🇮🇹 이탈리아어</option>
      <option value="pt">🇧🇷 포르투갈어</option>
      <option value="ru">🇷🇺 러시아어</option>
    </select>
    <button class="swap-btn" id="swapBtn" title="언어 교체"><i class="ti ti-switch-horizontal"></i></button>
    <select id="tgtLang">
      <option value="en">🇺🇸 영어</option>
      <option value="ko">🇰🇷 한국어</option>
      <option value="ja">🇯🇵 일본어</option>
      <option value="zh">🇨🇳 중국어</option>
      <option value="fr">🇫🇷 프랑스어</option>
      <option value="de">🇩🇪 독일어</option>
      <option value="es">🇪🇸 스페인어</option>
      <option value="it">🇮🇹 이탈리아어</option>
      <option value="pt">🇧🇷 포르투갈어</option>
      <option value="ru">🇷🇺 러시아어</option>
    </select>
  </div>
 
  <div class="text-panels">
    <div class="t-panel">
      <div class="t-panel-head">
        <span class="t-panel-label">원문</span>
        <span class="char-count" id="charCount">0 / 1000</span>
      </div>
      <textarea id="srcText" placeholder="번역할 텍스트를 입력하세요..." maxlength="1000"></textarea>
      <div class="panel-foot">
        <button class="icon-btn" id="srcPlayBtn"><i class="ti ti-volume"></i> 원문 듣기</button>
      </div>
    </div>
    <div class="t-panel">
      <div class="t-panel-head">
        <span class="t-panel-label">번역 결과</span>
      </div>
      <div class="t-result" id="resultBox"><span class="t-placeholder">번역 결과가 여기에 표시됩니다</span></div>
      <div class="panel-foot">
        <button class="icon-btn" id="copyBtn"><i class="ti ti-copy"></i> 복사</button>
        <button class="icon-btn" id="tgtPlayBtn"><i class="ti ti-volume"></i> 번역 듣기</button>
      </div>
    </div>
  </div>
 
  <div class="action-row">
    <button class="sec-btn" id="clearBtn"><i class="ti ti-trash"></i> 초기화</button>
    <button class="main-btn" id="translateBtn"><i class="ti ti-language"></i> 번역하기</button>
  </div>
 
  <div class="play-strip" id="bigPlayBtn">
    <div class="play-circle"><i class="ti ti-player-play" id="bigPlayIco"></i></div>
    <div class="play-info">
      <div class="play-title" id="bigPlayTitle">재생 준비됨</div>
      <div class="play-sub">번역 후 재생 버튼을 누르세요 · 자막과 함께 표시됩니다</div>
    </div>
    <span class="play-speed" id="playSpeedBadge">1.0x</span>
  </div>
 
  <div class="sub-box" id="subBox">
    <div class="sub-head"><span class="sub-dot"></span> 자막 재생 중</div>
    <div class="sub-content" id="subContent"></div>
  </div>
 
</div>
</section>
 
<section class="features" id="features">
<div class="container">
  <div class="features-title">주요 기능</div>
  <div class="features-grid">
    <div class="feature-card">
      <div class="feat-icon"><i class="ti ti-user-voice"></i></div>
      <div class="feat-title">8가지 목소리 프리셋</div>
      <div class="feat-desc">Aria, James, Nova 등 각기 다른 음색과 억양을 가진 목소리 캐릭터를 선택하세요.</div>
    </div>
    <div class="feature-card">
      <div class="feat-icon"><i class="ti ti-mood-smile"></i></div>
      <div class="feat-title">감정 톤 조절</div>
      <div class="feat-desc">따뜻하게, 신나게, 차분하게 등 6가지 감정으로 같은 목소리도 다르게 표현합니다.</div>
    </div>
    <div class="feature-card">
      <div class="feat-icon"><i class="ti ti-language"></i></div>
      <div class="feat-title">AI 번역 통합</div>
      <div class="feat-desc">Claude AI 기반 번역으로 10개 언어를 자연스럽게 번역하고 바로 들을 수 있습니다.</div>
    </div>
    <div class="feature-card">
      <div class="feat-icon"><i class="ti ti-subtask"></i></div>
      <div class="feat-title">실시간 자막</div>
      <div class="feat-desc">TTS 재생 중 현재 읽고 있는 단어가 하이라이트된 자막이 실시간으로 표시됩니다.</div>
    </div>
    <div class="feature-card">
      <div class="feat-icon"><i class="ti ti-adjustments-horizontal"></i></div>
      <div class="feat-title">세부 파라미터 조절</div>
      <div class="feat-desc">속도, 음높이, 볼륨, 문장 간격을 슬라이더로 미세하게 조절할 수 있습니다.</div>
    </div>
    <div class="feature-card">
      <div class="feat-icon"><i class="ti ti-shield-check"></i></div>
      <div class="feat-title">완전 무료 · 설치 불필요</div>
      <div class="feat-desc">브라우저 내장 TTS 엔진을 사용하여 별도 설치나 API 키 없이 바로 사용 가능합니다.</div>
    </div>
  </div>
</div>
</section>
 
<footer>
  <p>Voice Studio &mdash; 브라우저 TTS 최적화 번역기 &middot; Made with <span>♥</span></p>
</footer>
 
<script>
const PRESETS = [
  {id:'aria',  name:'Aria',  desc:'밝고 명랑한 여성',   tag:'여성·밝음',  av:'👩', bg:'rgba(244,114,182,0.15)', lang:'en-US', rate:1.05, pitch:1.15, vol:1},
  {id:'james', name:'James', desc:'차분한 남성 내레이터', tag:'남성·차분',  av:'👨', bg:'rgba(56,189,248,0.15)',  lang:'en-US', rate:0.95, pitch:0.88, vol:1},
  {id:'nova',  name:'Nova',  desc:'젊고 에너제틱한 느낌', tag:'중성·활발', av:'🧑', bg:'rgba(74,222,128,0.15)', lang:'en-US', rate:1.1,  pitch:1.05, vol:1},
  {id:'sage',  name:'Sage',  desc:'신뢰감 있는 여성',   tag:'여성·신뢰',  av:'👩', bg:'rgba(251,191,36,0.15)', lang:'en-GB', rate:0.98, pitch:1.0,  vol:1},
  {id:'echo',  name:'Echo',  desc:'깊고 낮은 남성',     tag:'남성·중후',  av:'👨', bg:'rgba(167,139,250,0.15)',lang:'en-US', rate:0.92, pitch:0.78, vol:1},
  {id:'luna',  name:'Luna',  desc:'부드럽고 감성적',    tag:'여성·감성',  av:'👩', bg:'rgba(244,114,182,0.15)',lang:'en-AU', rate:0.96, pitch:1.08, vol:0.95},
  {id:'rex',   name:'Rex',   desc:'힘차고 자신감 넘침',  tag:'남성·강함',  av:'👨', bg:'rgba(251,146,60,0.15)', lang:'en-US', rate:1.0,  pitch:0.82, vol:1},
  {id:'mia',   name:'Mia',   desc:'아이 같은 귀여운 톤', tag:'여성·귀여움',av:'🧒', bg:'rgba(74,222,128,0.15)', lang:'en-US', rate:1.12, pitch:1.25, vol:0.95},
];
const EMOTIONS = {
  neutral:  {rOff:0,     pOff:0},
  warm:     {rOff:-.05,  pOff:.05},
  excited:  {rOff:.15,   pOff:.15},
  calm:     {rOff:-.1,   pOff:-.1},
  serious:  {rOff:-.08,  pOff:-.15},
  friendly: {rOff:.05,   pOff:.1},
};
const PAUSE_LABELS = ['짧게','보통','길게'];
const LANG_MAP = {ko:'ko-KR',ja:'ja-JP',zh:'zh-CN',fr:'fr-FR',de:'de-DE',es:'es-ES',en:'en-US',it:'it-IT',pt:'pt-BR',ru:'ru-RU'};
const LANG_NAMES = {ko:'Korean',ja:'Japanese',zh:'Chinese',fr:'French',de:'German',es:'Spanish',en:'English',it:'Italian',pt:'Portuguese',ru:'Russian'};
 
let sel = PRESETS[0];
let emotion = 'neutral';
let translated = '';
let voices = [];
let playing = false;
 
const $ = id => document.getElementById(id);
 
function buildGrid() {
  const g = $('voiceGrid');
  PRESETS.forEach(p => {
    const c = document.createElement('div');
    c.className = 'voice-card' + (p.id === sel.id ? ' active' : '');
    c.innerHTML = `<div class="vc-top"><div class="vc-av" style="background:${p.bg}">${p.av}</div><span class="vc-name">${p.name}</span></div><div class="vc-desc">${p.desc}</div><span class="vc-tag">${p.tag}</span>`;
    c.onclick = () => { sel = p; document.querySelectorAll('.voice-card').forEach((x,i)=>x.classList.toggle('active',PRESETS[i].id===p.id)); applyPreset(); stopSpeech(); };
    g.appendChild(c);
  });
}
 
function applyPreset() {
  const em = EMOTIONS[emotion];
  $('rateSlider').value = Math.min(2, Math.max(0.5, sel.rate + em.rOff)).toFixed(1);
  $('pitchSlider').value = Math.min(2, Math.max(0.5, sel.pitch + em.pOff)).toFixed(1);
  $('volSlider').value = sel.vol;
  updateLabels();
}
 
function updateLabels() {
  $('rateVal').textContent = parseFloat($('rateSlider').value).toFixed(1) + 'x';
  $('pitchVal').textContent = parseFloat($('pitchSlider').value).toFixed(1);
  $('volVal').textContent = Math.round($('volSlider').value * 100) + '%';
  $('pauseVal').textContent = PAUSE_LABELS[parseInt($('pauseSlider').value)];
  $('playSpeedBadge').textContent = parseFloat($('rateSlider').value).toFixed(1) + 'x';
}
 
['rateSlider','pitchSlider','volSlider','pauseSlider'].forEach(id => $(id).addEventListener('input', updateLabels));
 
document.querySelectorAll('.emotion-btn').forEach(btn => {
  btn.onclick = () => {
    emotion = btn.dataset.e;
    document.querySelectorAll('.emotion-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    applyPreset();
  };
});
 
function loadVoices() {
  voices = window.speechSynthesis.getVoices();
  $('voiceNotice').textContent = voices.length ? `${voices.length}개 목소리 감지됨` : '목소리 로딩 중...';
}
if(window.speechSynthesis) { loadVoices(); window.speechSynthesis.onvoiceschanged = loadVoices; }
 
function findVoice(lc) {
  if(!voices.length) return null;
  return voices.find(v=>v.lang===lc) || voices.find(v=>v.lang.startsWith(lc.split('-')[0])) || null;
}
 
function stopSpeech() {
  if(window.speechSynthesis) window.speechSynthesis.cancel();
  playing = false;
  $('bigPlayBtn').classList.remove('playing');
  $('bigPlayIco').className = 'ti ti-player-play';
  $('bigPlayTitle').textContent = translated ? '재생 준비됨' : '텍스트를 입력하세요';
  [$('srcPlayBtn'), $('tgtPlayBtn')].forEach(b => {
    b.classList.remove('playing');
  });
  $('srcPlayBtn').innerHTML = '<i class="ti ti-volume"></i> 원문 듣기';
  $('tgtPlayBtn').innerHTML = '<i class="ti ti-volume"></i> 번역 듣기';
  $('subBox').classList.remove('show');
}
 
function speak(text, langCode, isMain) {
  if(!window.speechSynthesis) { alert('이 브라우저는 TTS를 지원하지 않습니다.'); return; }
  stopSpeech();
  const pauseMap = [.75, 1.0, 1.25];
  const pauseRate = pauseMap[parseInt($('pauseSlider').value)];
  const u = new SpeechSynthesisUtterance(text);
  u.rate = Math.min(2, parseFloat($('rateSlider').value) * pauseRate);
  u.pitch = parseFloat($('pitchSlider').value);
  u.volume = parseFloat($('volSlider').value);
  u.lang = langCode;
  const v = findVoice(langCode);
  if(v) u.voice = v;
  playing = true;
  if(isMain) {
    $('bigPlayBtn').classList.add('playing');
    $('bigPlayIco').className = 'ti ti-player-stop';
    $('bigPlayTitle').textContent = '재생 중 — 클릭하여 정지';
    runSubtitle(text);
  }
  u.onend = u.onerror = () => { playing = false; stopSpeech(); };
  window.speechSynthesis.speak(u);
}
 
function runSubtitle(text) {
  $('subBox').classList.add('show');
  const words = text.split(/\s+/);
  let wi = 0;
  const rate = parseFloat($('rateSlider').value) || 1;
  const ms = Math.max(80, (60000 / Math.max(words.length, 1)) / rate * 0.82);
  function tick() {
    if(!playing || wi >= words.length) return;
    const s = Math.max(0, wi-3), e = Math.min(words.length, wi+6);
    $('subContent').innerHTML = words.slice(s,e).map((w,i)=> s+i===wi ? `<span class="w-hi">${w}</span>` : w).join(' ');
    wi++; setTimeout(tick, ms);
  }
  tick();
}
 
$('bigPlayBtn').onclick = () => {
  if(playing) { stopSpeech(); return; }
  const t = translated || $('srcText').value.trim();
  if(!t) { alert('텍스트를 입력하거나 번역을 먼저 실행하세요.'); return; }
  const lc = translated ? LANG_MAP[$('tgtLang').value] || 'en-US' : LANG_MAP[$('srcLang').value] || 'ko-KR';
  speak(t, lc, true);
};
$('srcPlayBtn').onclick = () => {
  const t = $('srcText').value.trim(); if(!t) return;
  $('srcPlayBtn').innerHTML = '<i class="ti ti-player-stop"></i> 정지';
  $('srcPlayBtn').classList.add('playing');
  speak(t, LANG_MAP[$('srcLang').value] || 'ko-KR', false);
};
$('tgtPlayBtn').onclick = () => {
  if(!translated) { alert('번역을 먼저 실행하세요.'); return; }
  $('tgtPlayBtn').innerHTML = '<i class="ti ti-player-stop"></i> 정지';
  $('tgtPlayBtn').classList.add('playing');
  speak(translated, LANG_MAP[$('tgtLang').value] || 'en-US', true);
};
 
$('srcText').addEventListener('input', () => {
  $('charCount').textContent = $('srcText').value.length + ' / 1000';
});
$('copyBtn').onclick = () => {
  if(!translated) return;
  navigator.clipboard.writeText(translated).then(() => {
    $('copyBtn').innerHTML = '<i class="ti ti-check"></i> 복사됨';
    setTimeout(() => { $('copyBtn').innerHTML = '<i class="ti ti-copy"></i> 복사'; }, 1500);
  });
};
$('clearBtn').onclick = () => {
  $('srcText').value = ''; $('charCount').textContent = '0 / 1000';
  $('resultBox').innerHTML = '<span class="t-placeholder">번역 결과가 여기에 표시됩니다</span>';
  translated = ''; stopSpeech();
};
$('swapBtn').onclick = () => {
  const sv = $('srcLang').value, tv = $('tgtLang').value;
  const setV = (sel, v) => { for(let o of sel.options) if(o.value===v){o.selected=true;break;} };
  setV($('srcLang'), tv); setV($('tgtLang'), sv);
  if(translated) {
    $('srcText').value = translated;
    $('charCount').textContent = translated.length + ' / 1000';
    $('resultBox').innerHTML = '<span class="t-placeholder">번역 결과가 여기에 표시됩니다</span>';
    translated = '';
  }
};
 
$('translateBtn').onclick = async () => {
  const text = $('srcText').value.trim();
  if(!text) { alert('번역할 텍스트를 입력하세요.'); return; }
  stopSpeech();
  $('translateBtn').disabled = true;
  $('translateBtn').innerHTML = '<span class="spin"></span> 번역 중...';
  $('resultBox').innerHTML = '<span class="t-placeholder">번역 중...</span>';
  const srcCode = $('srcLang').value;
  const tgtCode = $('tgtLang').value;
  const langPair = `${srcCode}|${tgtCode}`;
  try {
    const url = `https://api.mymemory.translated.net/get?q=${encodeURIComponent(text)}&langpair=${langPair}`;
    const r = await fetch(url);
    const d = await r.json();
    if(d.responseStatus === 200 && d.responseData?.translatedText) {
      translated = d.responseData.translatedText.trim();
      $('resultBox').textContent = translated;
      $('bigPlayTitle').textContent = '재생 준비됨 — 클릭하여 듣기';
    } else {
      $('resultBox').innerHTML = '<span class="t-placeholder">번역 실패. 다시 시도하세요.</span>';
    }
  } catch(e) {
    $('resultBox').innerHTML = '<span class="t-placeholder">네트워크 오류. 인터넷 연결을 확인하세요.</span>';
  }
  $('translateBtn').disabled = false;
  $('translateBtn').innerHTML = '<i class="ti ti-language"></i> 번역하기';
};
 
buildGrid();
applyPreset();
</script>
</body>
</html>
