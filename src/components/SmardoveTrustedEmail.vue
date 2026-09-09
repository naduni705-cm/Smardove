<script setup>
const features = [
  { theme: 'green', title: 'Expert Email Support', text: 'Get fast guidance from our migration and email specialists.', mock: 'assistant' },
  { theme: 'yellow', title: 'Reliable Delivery', text: 'Keep every important message moving securely and on time.', mock: 'chart' },
  { theme: 'dark', title: 'Built to Scale', text: 'Add professional mailboxes effortlessly as your business grows.', mock: 'dashboard' },
  { theme: 'soft', title: 'Simple Management', text: 'Manage domains, users and security from one clean dashboard.', mock: 'search' }
]

const stats = [
  { value: '99.9%', label: 'Delivery Uptime', color: '#98c46e' },
  { value: '25 GB', label: 'Mailbox Storage', color: '#e2d85c' },
  { value: '24/7', label: 'Mail Protection', color: '#0d0d0d' },
  { value: '700+', label: 'Businesses', color: '#c9e6a8' }
]
</script>

<template>
  <section class="saas-section">
    <div class="soft-orb orb-one"></div>
    <div class="soft-orb orb-two"></div>

    <div class="section-inner">
      <header class="intro reveal">
        <span class="eyebrow"><b>✦</b> Business Email, Simplified</span>
        <h2>Communicate, Protect, and<br />Grow with Confidence</h2>
        <p>Professional email hosting with reliable delivery, secure mailboxes,<br class="desktop-break" /> simple migration and support when you need it.</p>
      </header>

      <div class="feature-grid">
        <article
          v-for="(feature, index) in features"
          :key="feature.title"
          class="feature-card reveal"
          :class="feature.theme"
          :style="{ '--delay': `${index * 110}ms` }"
        >
          <div class="card-copy">
            <h3>{{ feature.title }}</h3>
            <p>{{ feature.text }}</p>
          </div>

          <div class="browser">
            <div class="browser-bar"><i></i><i></i><i></i></div>

            <div v-if="feature.mock === 'assistant'" class="mock assistant-mock">
              <div class="question"><span>RD</span><b>What should I do next?</b></div>
              <div class="answer"><strong>✦</strong><p><b>AI</b><br />To prevent further issues, isolate the impacted system and verify dependencies.</p></div>
              <div class="ask">✦ <span>Ask me anything</span></div>
            </div>

            <div v-else-if="feature.mock === 'chart'" class="mock chart-mock">
              <small>Average daily sales</small>
              <div class="bars"><i></i><i></i><i></i><i></i><i></i></div>
              <div class="line"></div>
              <span class="tooltip">Join Recent</span>
              <div class="metric"><small>Total balance</small><b>$44,923.18</b></div>
            </div>

            <div v-else-if="feature.mock === 'dashboard'" class="mock dashboard-mock">
              <b>Dashboard</b>
              <div class="balances"><span>Bank account<br /><strong>$44,923.18</strong></span><span>Cash<br /><strong>$44,923.18</strong></span></div>
              <div class="graph"><i></i><i></i><i></i><i></i><i></i></div>
              <div class="notes"><span>＋ Add a note</span><small>Type your note</small><small>Type your note</small></div>
            </div>

            <div v-else class="mock search-mock">
              <div class="search">⌕ &nbsp; Search for</div>
              <span class="chip c1">John Robert</span><span class="chip c2">Food chef</span>
              <span class="chip c3">House maid</span><span class="chip c4">Category</span>
              <div class="search-field">Search bar</div>
            </div>
          </div>
        </article>
      </div>

      <div class="stats-shell reveal">
        <div class="stats-heading">
          <h3>Business email you can depend on</h3>
          <p>Everything your team needs to communicate professionally and grow securely.</p>
        </div>
        <div class="stats-grid">
          <div v-for="stat in stats" :key="stat.label" class="stat">
            <div class="stat-value"><i :style="{ background: stat.color }"></i>{{ stat.value }}</div>
            <span>{{ stat.label }}</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');

* { box-sizing: border-box; }
.saas-section { position: relative; overflow: hidden; padding: 72px 22px 40px; color: #181817; background: #f8f8f6; font-family: Inter, sans-serif; }
.section-inner { position: relative; z-index: 2; width: min(1180px, 100%); margin: auto; }
.intro { text-align: center; }
.eyebrow { display: inline-flex; align-items: center; gap: 7px; padding: 5px 13px 5px 6px; border: 1px solid #ddd7c8; border-radius: 999px; background: rgba(255,255,255,.76); box-shadow: 0 2px 8px rgba(0,0,0,.05); font-size: 12px; font-weight: 600; }
.eyebrow b { display: grid; place-items: center; width: 22px; height: 22px; border-radius: 50%; color: white; background: #1f1f22; }
.intro h2 { margin: 22px 0 12px; font-size: clamp(37px, 5vw, 58px); line-height: .99; letter-spacing: -.06em; }
.intro p, .stats-heading p { color: #77746e; font-size: 14px; line-height: 1.55; }
.feature-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; margin-top: 52px; }
.feature-card { --card: #188681; position: relative; min-width: 0; height: 330px; overflow: hidden; border: 3px solid white; border-radius: 16px; color: white; background: var(--card); box-shadow: 0 14px 25px rgba(28,35,34,.18), inset 0 1px rgba(255,255,255,.28); transition: transform .35s ease, box-shadow .35s ease; animation-delay: var(--delay); }
.feature-card:hover { transform: translateY(-8px); box-shadow: 0 22px 34px rgba(28,35,34,.23); }
.feature-card.pink { --card: #df0759; }.feature-card.gold { --card: #ffad0a; }.feature-card.blue { --card: #087eae; }
.card-copy { height: 116px; padding: 19px 18px; }
.card-copy h3 { margin: 0 0 10px; font-size: 18px; letter-spacing: -.03em; }
.card-copy p { margin: 0; max-width: 235px; color: rgba(255,255,255,.92); font-size: 11px; line-height: 1.55; }
.browser { position: absolute; left: 48px; right: -14px; bottom: -13px; height: 215px; overflow: hidden; border-radius: 14px 0 0; background: rgba(255,255,255,.94); box-shadow: -8px 0 24px rgba(0,0,0,.12); color: #273038; }
.browser-bar { display: flex; gap: 5px; height: 30px; padding: 11px 13px; background: color-mix(in srgb, var(--card), black 18%); }
.browser-bar i { width: 7px; height: 7px; border-radius: 50%; background: rgba(255,255,255,.48); }
.mock { position: relative; height: calc(100% - 30px); padding: 14px; background: linear-gradient(145deg,#fff,#eef2f3); font-size: 7px; }
.question { display: flex; gap: 8px; align-items: center; }.question span { padding: 8px; border-radius: 50%; background: #edf1f2; }
.answer { display: flex; gap: 9px; margin-top: 14px; }.answer strong { display:grid; place-items:center; width:23px;height:23px;border-radius:50%; background:var(--card);color:white }.answer p { margin:0;line-height:1.5;color:#617078 }.answer b { color:#223038; }
.ask { position:absolute; left:0;right:0;bottom:20px;padding:10px 13px;border:1px solid #d7dede;background:white;font-size:9px;box-shadow:0 4px 12px #cdd8d8 }.ask span { margin-left:8px;font-weight:600 }
.chart-mock small { font-weight:700 }.bars { display:flex;align-items:flex-end;gap:12px;height:90px;padding:15px 10px;border-bottom:1px solid #ddd }.bars i { width:18px;background:#f8d4dd }.bars i:nth-child(1){height:30px}.bars i:nth-child(2){height:50px}.bars i:nth-child(3){height:38px}.bars i:nth-child(4){height:68px}.bars i:nth-child(5){height:48px}.line {position:absolute;left:30px;top:69px;width:145px;height:2px;background:#ef4d78;transform:rotate(-8deg)}
.tooltip { position:absolute;right:14px;top:65px;padding:5px 8px;border-radius:9px;background:#ed2d68;color:white }.metric { position:absolute;left:-25px;bottom:20px;padding:10px;width:118px;border-radius:8px;background:white;box-shadow:0 6px 20px #c5c5c5 }.metric b{display:block;margin-top:4px;font-size:13px}
.dashboard-mock>b{font-size:10px}.balances{display:flex;gap:8px;margin:14px -8px 0}.balances span{padding:8px;width:50%;background:white;box-shadow:0 2px 8px #ddd}.balances strong{font-size:9px}.graph{position:absolute;left:8px;bottom:25px;width:115px;height:75px;border-bottom:1px solid #ddd}.graph i{position:absolute;width:7px;height:7px;border-radius:50%;background:#f6b72f}.graph i:nth-child(1){left:4px;bottom:12px}.graph i:nth-child(2){left:29px;bottom:22px}.graph i:nth-child(3){left:53px;bottom:31px}.graph i:nth-child(4){left:77px;bottom:46px}.graph i:nth-child(5){left:101px;bottom:58px}.notes{position:absolute;right:5px;top:13px;display:grid;gap:9px;width:76px}.notes span{padding:7px;border-radius:10px;background:#ffc64c}.notes small{padding:6px;background:white;border-bottom:1px solid #eee}
.search-mock{background:linear-gradient(#f6fbfd,#65c8ef)}.search{padding:8px;border-radius:7px;background:white;color:#a1a9ae}.chip{position:absolute;padding:5px 10px;border-radius:12px;background:#20b4f3;color:white}.c1{top:56px;right:18px}.c2{top:82px;right:5px}.c3{top:101px;left:8px;background:white;color:#556}.c4{top:112px;right:12px}.search-field{position:absolute;left:10px;bottom:32px;padding:6px 9px;border-radius:10px;background:white;font-weight:600}
.stats-shell { position:relative;margin-top:49px;padding:32px 7% 30px;border-top:1px solid rgba(116,116,116,.18);background:rgba(255,255,255,.34) }
.stats-shell::before,.stats-shell::after{content:'';position:absolute;top:-1px;width:160px;height:70px;border-top:1px solid rgba(116,116,116,.18)}.stats-shell::before{left:-80px;transform:skewX(-45deg)}.stats-shell::after{right:-80px;transform:skewX(45deg)}
.stats-heading{text-align:center}.stats-heading h3{margin:0 0 8px;font-size:27px;letter-spacing:-.04em}.stats-grid{display:grid;grid-template-columns:repeat(4,1fr);margin-top:30px}.stat{text-align:center;border-right:1px solid rgba(0,0,0,.07)}.stat:last-child{border:0}.stat-value{display:flex;justify-content:center;align-items:center;gap:11px;font-size:30px;font-weight:700;letter-spacing:-.06em}.stat-value i{width:18px;height:18px;border-radius:3px;box-shadow:0 3px 6px rgba(0,0,0,.15)}.stat>span{display:block;margin-top:8px;color:#74716c;font-size:12px}
.soft-orb{position:absolute;border-radius:50%;filter:blur(50px);opacity:.16}.orb-one{width:420px;height:190px;left:4%;bottom:0;background:#28aeb4}.orb-two{width:420px;height:190px;right:5%;bottom:0;background:#ffb31a}
.reveal{animation:rise .8s cubic-bezier(.22,.75,.2,1) both}@keyframes rise{from{opacity:0;transform:translateY(24px)}to{opacity:1;transform:none}}
@media (max-width: 960px){.feature-grid{grid-template-columns:repeat(2,1fr)}.feature-card{height:340px}.browser{left:75px}.stats-shell{margin-top:35px}}
@media (max-width: 600px){.saas-section{padding:50px 15px 25px}.desktop-break{display:none}.intro h2{font-size:39px}.intro p{font-size:13px}.feature-grid{grid-template-columns:1fr;margin-top:36px}.feature-card{height:350px}.browser{left:58px}.stats-grid{grid-template-columns:repeat(2,1fr);gap:26px 0}.stat:nth-child(2){border:0}.stats-heading h3{font-size:23px}}
@media (prefers-reduced-motion: reduce){.reveal{animation:none}.feature-card{transition:none}}
/* Smardove website theme */
.saas-section{background:radial-gradient(circle at 8% 8%,rgba(243,238,154,.34),transparent 27%),radial-gradient(circle at 93% 90%,rgba(201,230,168,.38),transparent 29%),linear-gradient(180deg,#fff,#f8faf5);color:#0d0d0d}.eyebrow{border-color:#dfe5dc;background:rgba(255,255,255,.84);box-shadow:0 8px 24px rgba(30,43,23,.06)}.eyebrow b{background:#0d0d0d;color:#f3ee9a}.intro h2{font-weight:500}.intro h2::after{display:block;width:100px;height:7px;margin:12px auto 0;border-radius:99px;background:linear-gradient(90deg,#c9e6a8,#f3ee9a);content:""}.intro p,.stats-heading p{color:#747a72}.feature-card{--card:#a9cf7e;border-color:rgba(255,255,255,.92);color:#0d0d0d;box-shadow:0 18px 45px rgba(32,46,24,.14),inset 0 1px rgba(255,255,255,.48)}.feature-card.green{--card:#c9e6a8}.feature-card.yellow{--card:#f3ee9a}.feature-card.dark{--card:#171917;color:#fff}.feature-card.soft{--card:#e9efdf}.feature-card:not(.dark) .card-copy p{color:rgba(13,13,13,.62)}.feature-card.dark .card-copy p{color:rgba(255,255,255,.72)}.feature-card:hover{box-shadow:0 27px 54px rgba(32,46,24,.2)}.browser-bar{background:color-mix(in srgb,var(--card),#0d0d0d 15%)}.mock{background:linear-gradient(145deg,#fff,#f1f5ed);color:#273026}.answer strong{background:#0d0d0d;color:#f3ee9a}.ask{border-color:#dce5d7;box-shadow:0 5px 15px rgba(40,55,31,.12)}.bars i{background:#e8eddf}.bars i:nth-child(2),.bars i:nth-child(4){background:#c9e6a8}.bars i:nth-child(3),.bars i:nth-child(5){background:#f3ee9a}.line{background:#7fa858}.tooltip{background:#0d0d0d;color:#fff}.metric{box-shadow:0 8px 24px rgba(35,48,27,.16)}.graph i{background:#98c46e}.graph i:nth-child(even){background:#ded45c}.notes span{background:#f3ee9a}.search-mock{background:linear-gradient(#f8fbf4,#c9e6a8)}.chip{background:#0d0d0d;color:#fff}.c2{background:#91bd67}.c3{background:#fff;color:#55604f}.c4{background:#e1d759;color:#373513}.stats-shell{border-color:#e1e7df;background:rgba(255,255,255,.62);box-shadow:0 20px 60px rgba(30,43,23,.05)}.stats-shell::before,.stats-shell::after{border-color:#e1e7df}.stat{border-color:#e3e8e0}.stat>span{color:#747a72}.orb-one{background:#c9e6a8}.orb-two{background:#f3ee9a}
</style>
