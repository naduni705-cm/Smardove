<script setup>
const people = [
  { name: 'Maya', city: 'New York', x: 185, y: 252, tone: '#c9e6a8' },
  { name: 'Noah', city: 'London', x: 495, y: 190, tone: '#f3ee9a' },
  { name: 'Amina', city: 'Lagos', x: 550, y: 355, tone: '#c9e6a8' },
  { name: 'Mei', city: 'Singapore', x: 890, y: 338, tone: '#f3ee9a' },
  { name: 'Leo', city: 'Sydney', x: 1040, y: 418, tone: '#c9e6a8' }
]
</script>

<template>
  <section class="mail-network" aria-labelledby="mail-network-title">
    <div class="orb orb--green" /><div class="orb orb--yellow" />
    <div class="mail-network__inner">
      <header class="section-heading">
        <span class="eyebrow"><i /> Global email network</span>
        <h2 id="mail-network-title">One inbox. Every person.<br><mark>Connected worldwide.</mark></h2>
        <p>Keep every conversation moving with fast, secure business email—wherever your people work.</p>
      </header>

      <div class="network-stage">
        <div class="stage-status"><span><i /> All systems operational</span><span>Protected by Smardove</span></div>

        <svg class="world-map" viewBox="0 0 1200 560" role="img" aria-label="People exchanging email across a connected world map">
          <defs>
            <pattern id="map-dots" width="8" height="8" patternUnits="userSpaceOnUse">
              <circle cx="2.5" cy="2.5" r="1.7" fill="#758079" />
            </pattern>
            <linearGradient id="route-color"><stop stop-color="#9bd069"/><stop offset=".5" stop-color="#e5df72"/><stop offset="1" stop-color="#92c967"/></linearGradient>
            <filter id="soft-shadow" x="-60%" y="-60%" width="220%" height="220%">
              <feDropShadow dx="0" dy="8" stdDeviation="8" flood-color="#27331f" flood-opacity=".2"/>
            </filter>
          </defs>

          <g class="continents" fill="url(#map-dots)">
            <path d="M62 201 86 144l47-43 72-27 85 13 49 48-21 42-44 16-15 51-46 28-22 79-42-23-15-62-56-23Z"/>
            <path d="m238 334 47 20 30 54-12 74-39 65-31-55-13-84Z"/>
            <path d="m462 143 45-48 86-19 67 22 51-9 67 28 78 4 58 30 92 10 90 57-39 35-80-12-55 25-54-1-39 40-69-23-42-50-72 2-41-43-63 10-48-25Z"/>
            <path d="m522 279 80-8 65 53-13 107-60 80-45-53-30-98Z"/>
            <path d="m932 380 68-38 81 29 45 59-30 50-89 4-67-45Z"/>
            <path d="m1040 267 31-28 31 18-18 33Z"/>
          </g>

          <g class="routes" fill="none" stroke="url(#route-color)" stroke-width="3" stroke-linecap="round">
            <path d="M185 252Q335 52 495 190"/><path d="M495 190Q705 45 890 338"/>
            <path d="M185 252Q350 210 550 355"/><path d="M550 355Q730 190 890 338"/>
            <path d="M890 338Q1015 280 1040 418"/>
          </g>

          <g class="packets" aria-hidden="true">
            <g class="packet packet--1"><rect x="-14" y="-10" width="28" height="20" rx="5"/><path d="m-10-6 10 8 10-8"/></g>
            <g class="packet packet--2"><rect x="-14" y="-10" width="28" height="20" rx="5"/><path d="m-10-6 10 8 10-8"/></g>
            <g class="packet packet--3"><rect x="-14" y="-10" width="28" height="20" rx="5"/><path d="m-10-6 10 8 10-8"/></g>
          </g>

          <g v-for="(person, i) in people" :key="person.name" class="person" :transform="`translate(${person.x} ${person.y})`" filter="url(#soft-shadow)">
            <circle class="person__pulse" r="39" :fill="person.tone" opacity=".25"/>
            <circle r="27" fill="#fff"/><circle cy="-6" r="8" fill="#202420"/>
            <path d="M-15 16c1-12 8-18 15-18s14 6 15 18" :fill="person.tone"/>
            <circle r="27" fill="none" :stroke="person.tone" stroke-width="3"/>
            <g v-if="i === 0 || i === 3" transform="translate(21 -23)">
              <circle r="10" fill="#111"/><path d="M-4-2h8v6h-8Zm0 0 4 3 4-3" fill="none" stroke="#fff" stroke-width="1.2"/>
            </g>
          </g>
        </svg>

        <div v-for="(person, i) in people" :key="person.city" class="person-label" :class="`person-label--${i + 1}`">
          <i :style="{ background: person.tone }"/><span><strong>{{ person.name }}</strong><small>{{ person.city }}</small></span>
        </div>

        <div class="delivery-card">
          <span class="delivery-icon"><svg viewBox="0 0 24 24"><path d="M4 7h16v11H4zM5 8l7 6 7-6"/></svg></span>
          <span><small>Message delivered</small><strong>London → Singapore</strong></span><b>✓</b>
        </div>

        <footer class="stage-footer">
          <span><strong>99.99%</strong> uptime</span><span><strong>&lt; 1 sec</strong> smart routing</span><span><strong>24/7</strong> protection</span>
        </footer>
      </div>
    </div>
  </section>
</template>

<style scoped>
.mail-network,.mail-network *{box-sizing:border-box}
.mail-network{--ink:#0d0d0d;--sub:#6b6f76;--line:rgba(13,13,13,.085);--green:#c9e6a8;--yellow:#f3ee9a;position:relative;isolation:isolate;overflow:hidden;width:100%;padding:clamp(76px,8vw,126px) clamp(14px,4vw,64px);background:#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}
.orb{position:absolute;z-index:-1;width:38vw;height:38vw;border-radius:50%;filter:blur(110px);opacity:.23;pointer-events:none}.orb--green{right:-12%;top:25%;background:var(--green)}.orb--yellow{left:-15%;bottom:-20%;background:var(--yellow)}
.mail-network__inner{width:min(94vw,1480px);margin:auto}.section-heading{position:relative;z-index:3;max-width:920px;margin:0 auto clamp(36px,4vw,60px);text-align:center}
.eyebrow{display:inline-flex;align-items:center;gap:9px;margin-bottom:20px;padding:8px 13px;border:1px solid var(--line);border-radius:999px;background:rgba(255,255,255,.82);color:#535953;font-size:12px;font-weight:650;letter-spacing:.04em;text-transform:uppercase}.eyebrow i,.stage-status i{width:7px;height:7px;border-radius:50%;background:#79b649;box-shadow:0 0 0 5px rgba(121,182,73,.12)}
.mail-network h2{margin:0;font-family:var(--font-display,var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif));font-size:clamp(30px,4.6vw,68px);font-weight:380;line-height:1.08;letter-spacing:-.01em}.mail-network h2 mark{padding:0 2px;background:linear-gradient(transparent 62%,var(--yellow) 62%);color:inherit}.section-heading p{max-width:680px;margin:23px auto 0;color:var(--sub);font-size:clamp(14px,1.25vw,18px);line-height:1.65}
.network-stage{position:relative;min-height:650px;overflow:hidden;border:1px solid var(--line);border-radius:clamp(24px,3vw,42px);background:linear-gradient(145deg,rgba(255,255,255,.97),rgba(247,249,245,.92));box-shadow:0 40px 90px -58px rgba(32,47,23,.42)}
.network-stage:before{position:absolute;inset:0;background-image:linear-gradient(rgba(13,13,13,.025) 1px,transparent 1px),linear-gradient(90deg,rgba(13,13,13,.025) 1px,transparent 1px);background-size:44px 44px;mask-image:linear-gradient(to bottom,#000,transparent 86%);content:""}
.stage-status{position:absolute;z-index:4;top:22px;right:26px;left:26px;display:flex;justify-content:space-between;color:#80857f;font-size:11px;letter-spacing:.06em;text-transform:uppercase}.stage-status span:first-child{display:flex;align-items:center;gap:10px;color:#556052;font-weight:650}
.world-map{position:absolute;top:44px;left:50%;width:min(100%,1260px);height:auto;overflow:visible;transform:translateX(-50%)}.continents{opacity:.68}.routes path{stroke-dasharray:8 10}.packets{fill:#111;stroke:#fff;stroke-width:1.2}.packet--1{offset-path:path("M185 252Q335 52 495 190")}.packet--2{offset-path:path("M495 190Q705 45 890 338")}.packet--3{offset-path:path("M550 355Q730 190 890 338")}.person__pulse{transform-box:fill-box;transform-origin:center}
.person-label{position:absolute;z-index:3;display:flex;align-items:center;gap:9px;min-width:112px;padding:8px 12px;border:1px solid var(--line);border-radius:13px;background:rgba(255,255,255,.9);box-shadow:0 14px 30px -24px rgba(0,0,0,.35);backdrop-filter:blur(10px)}.person-label>i{width:7px;height:7px;flex:none;border-radius:50%;box-shadow:0 0 0 4px rgba(201,230,168,.2)}.person-label span{display:grid}.person-label strong{font-size:11px;line-height:1.2}.person-label small{color:#8a8e8a;font-size:8px}.person-label--1{top:43%;left:10%}.person-label--2{top:31%;left:38%}.person-label--3{top:58%;left:42%}.person-label--4{top:55%;right:20%}.person-label--5{top:68%;right:5%}
.delivery-card{position:absolute;z-index:5;top:63%;left:50%;display:flex;width:min(390px,42vw);min-height:78px;align-items:center;gap:14px;padding:10px 14px 10px 10px;border:1px solid rgba(13,13,13,.07);border-radius:20px;background:rgba(255,255,255,.96);box-shadow:0 28px 55px -30px rgba(23,38,14,.42);transform:translateX(-50%);backdrop-filter:blur(14px)}.delivery-icon{display:grid;width:56px;height:56px;flex:none;place-items:center;border-radius:16px;background:linear-gradient(135deg,var(--green),var(--yellow))}.delivery-icon svg{width:27px;fill:none;stroke:#111;stroke-width:1.7;stroke-linecap:round;stroke-linejoin:round}.delivery-card>span:nth-child(2){display:grid;gap:3px;flex:1}.delivery-card small{color:var(--sub);font-size:10px}.delivery-card strong{font-size:clamp(12px,1vw,15px)}.delivery-card b{display:grid;width:27px;height:27px;place-items:center;border-radius:50%;background:#eaf6df;color:#54942c;font-size:13px}
.stage-footer{position:absolute;right:5%;bottom:24px;left:5%;display:grid;grid-template-columns:repeat(3,1fr);padding:20px;border-top:1px solid var(--line);color:var(--sub);font-size:11px;text-align:center}.stage-footer strong{display:block;margin-bottom:4px;color:var(--ink);font-size:clamp(16px,1.6vw,23px);font-weight:620}
@media(prefers-reduced-motion:no-preference){.routes path{animation:route-flow 2.2s linear infinite}.routes path:nth-child(2n){animation-duration:2.8s;animation-direction:reverse}.packet{animation:packet-travel 5s ease-in-out infinite;offset-rotate:0deg}.packet--2{animation-delay:-1.6s;animation-duration:6.2s}.packet--3{animation-delay:-3.2s;animation-duration:5.6s}.person__pulse{animation:person-pulse 2.8s ease-in-out infinite}.delivery-card{animation:card-float 4.4s ease-in-out infinite}}
@keyframes route-flow{to{stroke-dashoffset:-36}}@keyframes packet-travel{0%,8%{offset-distance:0;opacity:0}16%,84%{opacity:1}92%,100%{offset-distance:100%;opacity:0}}@keyframes person-pulse{50%{opacity:.08;transform:scale(1.35)}}@keyframes card-float{50%{transform:translate(-50%,-7px)}}
@media(max-width:900px){.network-stage{min-height:720px}.world-map{top:90px;width:1060px;max-width:none}.person-label{display:none}.delivery-card{top:60%;width:min(82%,390px)}}
@media(max-width:600px){.mail-network{padding-inline:12px}.mail-network__inner{width:100%}.mail-network h2{font-size:clamp(34px,10vw,48px)}.mail-network h2 br{display:none}.network-stage{min-height:680px;border-radius:24px}.stage-status{right:16px;left:16px}.stage-status span:last-child{display:none}.world-map{top:110px;width:920px}.delivery-card{top:58%;width:calc(100% - 28px)}.stage-footer{right:14px;bottom:14px;left:14px;gap:5px;padding:16px 4px}.stage-footer strong{font-size:16px}}
</style>
