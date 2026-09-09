<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const isVisible = ref(false)
let observer

const benefits = [
  {
    title: 'Customized Email Solutions',
    text: 'Tailor professional mailboxes and storage to suit your business goals and team size.',
    icon: 'signal'
  },
  {
    title: 'Professional Communication',
    text: 'Build customer trust with reliable, branded email addresses for every member of your team.',
    icon: 'person'
  },
  {
    title: 'Advanced Risk Protection',
    text: 'Protect every inbox with intelligent spam filtering, malware scanning, and secure delivery.',
    icon: 'shield'
  }
]

onMounted(() => {
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      isVisible.value = true
      observer.disconnect()
    }
  }, { threshold: 0.15 })
  if (root.value) observer.observe(root.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section
    ref="root"
    class="smardove-returns"
    :class="{ 'is-visible': isVisible }"
    aria-labelledby="returns-title"
  >
    <div class="returns-wrap">
      <header class="returns-header">
        <div class="returns-heading">
          <span class="section-pill">Business Email</span>
          <h2 id="returns-title">
            Cultivate Better Connections<br>
            <span>with <mark>Smarter Email</mark></span>
          </h2>
        </div>

        <div class="diamond-motif" aria-hidden="true">
          <span class="diamond diamond--outline" />
          <span class="diamond diamond--soft" />
          <span class="diamond diamond--dark">
            <svg viewBox="0 0 34 34"><path d="M17 4c1.4 8.1 5.9 12.6 14 14-8.1 1.4-12.6 5.9-14 14-1.4-8.1-5.9-12.6-14-14C11.1 16.6 15.6 12.1 17 4Z" /></svg>
          </span>
        </div>
      </header>

      <div class="feature-grid">
        <article class="feature-card feature-card--large">
          <div class="card-copy">
            <h3>Continuous Monitoring and Control</h3>
            <p>Keep every mailbox performing at its best with real-time visibility into activity, storage, and delivery.</p>
          </div>

          <div class="admin-visual" aria-hidden="true">
            <div class="admin-window">
              <div class="admin-window__bar">
                <div class="window-dots"><i/><i/><i/></div>
                <span>mail.smardove.com</span>
                <b>•••</b>
              </div>
              <div class="admin-window__body">
                <aside class="admin-sidebar">
                  <div class="admin-logo"><span>S</span></div>
                  <i class="is-active"/><i/><i/><i/><i/>
                </aside>
                <div class="admin-content">
                  <div class="admin-content__top">
                    <div><small>DELIVERY HEALTH</small><strong>98.7%</strong></div>
                    <span class="health-badge"><i/> Excellent</span>
                  </div>
                  <div class="admin-chart">
                    <div class="admin-bars"><i/><i/><i/><i/><i/><i/><i/><i/></div>
                    <svg viewBox="0 0 460 115" preserveAspectRatio="none">
                      <path pathLength="1" d="M0 91C45 87 60 60 103 68s61 7 92-17 69-33 104-8 60 42 89 17 41-44 72-42"/>
                    </svg>
                  </div>
                  <div class="admin-stats">
                    <div><span>Delivered</span><strong>23.8K</strong><small>+12.4%</small></div>
                    <div><span>Protected</span><strong>4.2K</strong><small>+8.1%</small></div>
                    <div><span>Mailboxes</span><strong>128</strong><small>Active</small></div>
                  </div>
                </div>
              </div>
            </div>
            <div class="floating-mail-card">
              <span class="mail-card-icon">
                <svg viewBox="0 0 24 24"><path d="M4 7.5 12 13l8-5.5M5.5 5h13A1.5 1.5 0 0 1 20 6.5v11a1.5 1.5 0 0 1-1.5 1.5h-13A1.5 1.5 0 0 1 4 17.5v-11A1.5 1.5 0 0 1 5.5 5Z"/></svg>
              </span>
              <span><small>SECURE DELIVERY</small><strong>All systems healthy</strong></span>
              <b>✓</b>
            </div>
          </div>
        </article>

        <article class="feature-card feature-card--chart">
          <div class="card-copy">
            <h3>Scale Your Team Effortlessly</h3>
            <p>Add new professional mailboxes as your business grows, without sacrificing speed, security, or control.</p>
          </div>

          <div class="chart-area" aria-hidden="true">
            <svg viewBox="0 0 520 220" preserveAspectRatio="none">
              <defs>
                <linearGradient id="smardoveArea" x1="0" y1="0" x2="0" y2="1">
                  <stop offset="0" stop-color="#c9e6a8" stop-opacity=".48" />
                  <stop offset="1" stop-color="#c9e6a8" stop-opacity="0" />
                </linearGradient>
              </defs>
              <g class="chart-lines"><path d="M0 200H520M0 146H520M0 92H520M0 38H520" /></g>
              <path class="chart-fill" d="M0 173C54 172 59 117 116 119s61-8 96-38 85-35 119 12 62 89 103 73 47-82 86-88V220H0Z" />
              <path class="chart-path" pathLength="1" d="M0 173C54 172 59 117 116 119s61-8 96-38 85-35 119 12 62 89 103 73 47-82 86-88" />
              <circle class="chart-node" cx="435" cy="166" r="7" />
            </svg>

            <div class="chart-summary">
              <span>MONTHLY DELIVERY</span>
              <strong>23,827</strong>
              <small><b>↑ 25%</b> from last month</small>
            </div>
            <div class="chart-tooltip"><span>Today</span><strong>1,284</strong><small>Delivered <b>99.9%</b></small></div>
            <div class="chart-label">Smardove Growth</div>
          </div>
        </article>
      </div>

      <div class="benefits-grid">
        <article v-for="(benefit, index) in benefits" :key="benefit.title" class="benefit" :style="{ '--delay': `${.55 + index * .12}s` }">
          <div class="benefit-icon" aria-hidden="true">
            <svg v-if="benefit.icon === 'signal'" viewBox="0 0 24 24">
              <path d="M8.5 15.5a5 5 0 0 1 0-7M5.5 18.5a9 9 0 0 1 0-13M15.5 8.5a5 5 0 0 1 0 7M18.5 5.5a9 9 0 0 1 0 13"/><circle cx="12" cy="12" r="2"/>
            </svg>
            <svg v-else-if="benefit.icon === 'person'" viewBox="0 0 24 24">
              <circle cx="15" cy="7" r="3"/><path d="M10 20v-2a5 5 0 0 1 5-5h2a4 4 0 0 1 4 4v3M3 11h8M7 7l4 4-4 4"/>
            </svg>
            <svg v-else viewBox="0 0 24 24">
              <path d="M12 3 20 6v5c0 5.2-3.1 8.4-8 10-4.9-1.6-8-4.8-8-10V6Z"/><path d="m8.5 12 2.2 2.2 4.8-5"/>
            </svg>
          </div>
          <div>
            <h3>{{ benefit.title }}</h3>
            <p>{{ benefit.text }}</p>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.smardove-returns,.smardove-returns *{box-sizing:border-box}.smardove-returns{--ink:#0d0d0d;--muted:#747874;--line:#e9ede7;--card:#f8faf7;--green:#c9e6a8;--green-strong:#b7d990;--yellow:#f3ee9a;position:relative;overflow:hidden;width:100%;padding:clamp(72px,8vw,124px) clamp(16px,5vw,70px);background:#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.smardove-returns::before{position:absolute;right:-180px;bottom:-240px;width:520px;height:520px;border-radius:50%;background:var(--green);filter:blur(130px);opacity:.19;content:"";pointer-events:none}.returns-wrap{position:relative;width:min(1420px,100%);margin:0 auto}.returns-header{display:flex;align-items:flex-start;justify-content:space-between;gap:40px;margin-bottom:clamp(48px,5vw,74px)}.returns-heading{opacity:0;transform:translateY(22px)}.is-visible .returns-heading{animation:rise .8s cubic-bezier(.2,.8,.2,1) forwards}.section-pill{display:inline-flex;min-height:38px;align-items:center;margin-bottom:28px;padding:8px 18px;border:1px solid #e2e7df;border-radius:999px;background:#fff;box-shadow:0 7px 20px rgba(25,33,24,.04);font-size:12px;font-weight:600}.returns-heading h2{margin:0;font-family:var(--font-display,var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif));font-size:clamp(40px,5vw,76px);font-weight:400;line-height:1.05;letter-spacing:-.045em}.returns-heading h2 span{color:#9a9e99}.returns-heading h2 mark{padding:0 2px;background:linear-gradient(transparent 64%,var(--yellow) 64%);color:var(--ink)}.diamond-motif{display:flex;align-items:center;gap:17px;padding:13px 8px 0 0;opacity:0;transform:translateX(20px)}.is-visible .diamond-motif{animation:motifIn .75s .2s forwards}.diamond{display:grid;width:65px;height:65px;place-items:center;border-radius:16px;transform:rotate(45deg)}.diamond--outline{border:1px solid #e2e7df;background:#fff}.diamond--soft{background:var(--green)}.diamond--dark{background:var(--ink)}.diamond svg{width:33px;transform:rotate(-45deg);fill:var(--yellow)}
.feature-grid{display:grid;grid-template-columns:1.43fr 1fr;gap:clamp(20px,2vw,32px)}.feature-card{position:relative;min-width:0;height:clamp(355px,31vw,475px);overflow:hidden;border:1px solid #eef0ec;border-radius:clamp(22px,2vw,30px);background:linear-gradient(145deg,#fafbf9,#f2f4f1);opacity:0;transform:translateY(34px);box-shadow:0 24px 60px -48px rgba(22,31,20,.32)}.is-visible .feature-card--large{animation:rise .8s .2s forwards}.is-visible .feature-card--chart{animation:rise .8s .34s forwards}.card-copy{position:relative;z-index:3;padding:clamp(28px,3vw,46px)}.card-copy h3{margin:0 0 14px;font-size:clamp(18px,1.55vw,25px);font-weight:650;letter-spacing:-.035em}.card-copy p{max-width:610px;margin:0;color:var(--muted);font-size:clamp(12px,.95vw,15px);line-height:1.65}.feature-card--chart .card-copy p{max-width:460px}
.analytics-stack{position:absolute;right:-3%;bottom:-34px;left:-4%;height:64%;transform:translateY(45px)}.is-visible .analytics-stack{animation:stackIn .9s .62s cubic-bezier(.17,.84,.31,1.15) forwards}.mini-panel{position:absolute;border:2px solid #151815;border-radius:17px;background:rgba(255,255,255,.96);box-shadow:0 24px 45px rgba(25,32,24,.14);overflow:hidden}.mini-panel--back{bottom:-8px;left:0;width:39%;height:75%;padding:24px;transform:rotate(13deg)}.mini-panel--middle{bottom:-23px;left:31%;width:33%;height:72%;padding:25px 30px;transform:rotate(-1deg)}.mini-panel--front{right:7%;bottom:-22px;width:48%;height:112%;padding:27px 31px;transform:rotate(8deg)}.mini-panel small{display:block;color:#697069;font-size:12px}.mini-panel strong{display:block;margin-top:5px;font-size:clamp(30px,3vw,47px);font-weight:500}.mini-panel span{color:#8b918a;font-size:10px}.panel-row{display:flex;align-items:center;justify-content:space-between}.panel-row b{font-size:22px}.bars{position:absolute;right:24px;bottom:0;left:24px;display:flex;height:64px;align-items:flex-end;gap:14px}.bars i{display:block;width:18%;height:35%;border-radius:8px 8px 0 0;background:#d5d9d4}.bars i:nth-child(2){height:68%;background:var(--green)}.bars i:nth-child(3){height:46%;background:var(--ink)}.bars i:nth-child(4){height:81%;background:#cfd4ce}.bars i:nth-child(5){height:60%;background:var(--yellow)}.bars i:nth-child(6){height:90%;background:#8c918c}.bars--main{height:80px}.bars--small i:nth-child(2){background:var(--yellow)}
.chart-area{position:absolute;right:0;bottom:0;left:0;height:63%}.chart-area svg{position:absolute;inset:0;width:100%;height:100%;overflow:visible}.chart-lines{fill:none;stroke:#e1e5df;stroke-width:1}.chart-fill{fill:url(#smardoveArea);opacity:0}.chart-path{fill:none;stroke:var(--ink);stroke-width:2.2;stroke-linecap:round;stroke-dasharray:1;stroke-dashoffset:1}.chart-node{fill:var(--yellow);stroke:#fff;stroke-width:5;opacity:0;filter:drop-shadow(0 3px 5px rgba(70,80,60,.2))}.is-visible .chart-fill{animation:fade .8s .9s forwards}.is-visible .chart-path{animation:draw 1.5s .58s cubic-bezier(.35,0,.2,1) forwards}.is-visible .chart-node{animation:pop .45s 1.8s forwards}.chart-tooltip{position:absolute;right:8%;top:-4%;display:flex;min-width:138px;flex-direction:column;padding:14px 17px;border:2px solid var(--ink);border-radius:13px;background:#fff;box-shadow:7px 8px 0 rgba(201,230,168,.8);opacity:0;transform:translateY(12px)}.is-visible .chart-tooltip{animation:rise .55s 1.55s forwards}.chart-tooltip span{color:#7f857e;font-size:9px}.chart-tooltip strong{margin:3px 0;font-size:19px}.chart-tooltip small{color:#989d97;font-size:9px}.chart-tooltip b{color:#8aae62}.chart-label{position:absolute;right:0;bottom:30px;left:0;text-align:center;font-size:12px;font-weight:600}
.benefits-grid{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:clamp(28px,5vw,82px);padding-top:clamp(52px,6vw,88px)}.benefit{display:grid;grid-template-columns:56px 1fr;gap:18px;opacity:0;transform:translateY(20px)}.is-visible .benefit{animation:rise .65s var(--delay) forwards}.benefit-icon{display:grid;width:54px;height:54px;place-items:center;border-radius:50%;background:var(--yellow);box-shadow:0 11px 28px rgba(191,184,90,.16);transition:transform .25s ease}.benefit:nth-child(2) .benefit-icon{background:var(--green)}.benefit:hover .benefit-icon{transform:translateY(-5px) rotate(-5deg)}.benefit-icon svg{width:23px;fill:none;stroke:var(--ink);stroke-width:1.7;stroke-linecap:round;stroke-linejoin:round}.benefit h3{margin:4px 0 10px;font-size:clamp(15px,1.2vw,19px);font-weight:650;letter-spacing:-.02em}.benefit p{max-width:350px;margin:0;color:var(--muted);font-size:clamp(11px,.9vw,14px);line-height:1.65}
@keyframes rise{to{opacity:1;transform:translateY(0)}}@keyframes motifIn{to{opacity:1;transform:translateX(0)}}@keyframes stackIn{to{transform:translateY(0)}}@keyframes draw{to{stroke-dashoffset:0}}@keyframes fade{to{opacity:1}}@keyframes pop{0%{opacity:0;transform:scale(0)}70%{opacity:1;transform:scale(1.4)}100%{opacity:1;transform:scale(1)}}
@media(max-width:900px){.diamond-motif{display:none}.feature-grid{grid-template-columns:1fr}.feature-card{height:420px}.benefits-grid{grid-template-columns:1fr 1fr}.benefit:last-child{grid-column:1/-1;max-width:480px}.returns-heading h2 br{display:none}}
@media(max-width:600px){.smardove-returns{padding-inline:14px}.returns-header{margin-bottom:38px}.section-pill{margin-bottom:22px}.returns-heading h2{font-size:clamp(37px,11vw,52px)}.feature-card{height:390px}.card-copy{padding:27px 24px}.analytics-stack{height:57%;right:-20%;left:-18%}.mini-panel--front{right:8%;width:53%;padding:23px 22px}.mini-panel--middle{left:29%;width:39%}.chart-area{height:59%}.chart-tooltip{right:5%;top:1%;min-width:120px}.benefits-grid{grid-template-columns:1fr;gap:32px;padding-top:52px}.benefit:last-child{grid-column:auto}.benefit{grid-template-columns:50px 1fr;gap:15px}.benefit-icon{width:48px;height:48px}.benefit h3{margin-top:2px}}
/* Premium surface refinement */
.smardove-returns{background:radial-gradient(circle at 93% 5%,rgba(201,230,168,.19),transparent 24%),radial-gradient(circle at 5% 78%,rgba(243,238,154,.15),transparent 22%),#fff}.returns-wrap::before{position:absolute;top:8px;right:0;width:180px;height:1px;background:linear-gradient(90deg,transparent,#dfe6da);content:""}.section-pill{border-color:#e1e7df;background:rgba(255,255,255,.82);box-shadow:0 8px 30px rgba(24,35,21,.06);backdrop-filter:blur(12px)}.section-pill::before{width:7px;height:7px;margin-right:9px;border-radius:50%;background:var(--green);box-shadow:0 0 0 5px rgba(201,230,168,.22);content:""}.diamond{box-shadow:0 14px 36px rgba(25,32,23,.08)}.diamond--soft{background:linear-gradient(145deg,#d9edc1,var(--green))}.diamond--dark{background:linear-gradient(145deg,#242824,var(--ink));box-shadow:0 18px 38px rgba(13,17,12,.2)}
.feature-card{border-color:rgba(218,225,215,.82);background:linear-gradient(145deg,rgba(255,255,255,.98),rgba(246,249,244,.96));box-shadow:0 28px 75px -50px rgba(28,46,22,.48),inset 0 1px 0 #fff;transition:border-color .35s ease,box-shadow .35s ease}.feature-card::before{position:absolute;z-index:0;inset:0;border-radius:inherit;background:radial-gradient(circle at 82% 90%,rgba(201,230,168,.22),transparent 32%);content:"";pointer-events:none}.feature-card--chart::before{background:radial-gradient(circle at 12% 95%,rgba(243,238,154,.2),transparent 36%),radial-gradient(circle at 90% 75%,rgba(201,230,168,.19),transparent 32%)}.feature-card:hover{border-color:#d2dfca;box-shadow:0 36px 85px -48px rgba(28,46,22,.56),inset 0 1px 0 #fff}.card-copy::after{display:block;width:42px;height:3px;margin-top:20px;border-radius:99px;background:linear-gradient(90deg,var(--green-strong),var(--yellow));content:""}.card-copy h3{font-weight:620}.card-copy p{color:#747b73}
.mini-panel{border-color:#20251f;background:rgba(255,255,255,.94);box-shadow:0 28px 58px rgba(29,40,25,.15);backdrop-filter:blur(12px)}.mini-panel--front{box-shadow:10px 16px 0 rgba(201,230,168,.55),0 28px 60px rgba(29,40,25,.18)}.bars i{background:linear-gradient(180deg,#e3e6e1,#cbd0ca)}.bars i:nth-child(2){background:linear-gradient(180deg,#e9f5db,var(--green))}.bars i:nth-child(3){background:linear-gradient(180deg,#333a32,var(--ink))}.bars i:nth-child(5){background:linear-gradient(180deg,#fffcc7,var(--yellow))}
.chart-area::after{position:absolute;right:11%;bottom:32px;width:9px;height:9px;border-radius:50%;background:var(--green-strong);box-shadow:0 0 0 7px rgba(172,213,125,.15);content:"";animation:softPulse 2.2s infinite}.chart-tooltip{border-color:#242924;box-shadow:8px 9px 0 rgba(201,230,168,.72),0 22px 44px rgba(27,36,24,.13)}.chart-label{color:#3f453f;letter-spacing:.02em}
.benefits-grid{position:relative}.benefits-grid::before{position:absolute;top:clamp(24px,3vw,42px);right:0;left:0;height:1px;background:linear-gradient(90deg,transparent,#e9eee6 12%,#e9eee6 88%,transparent);content:""}.benefit{padding:14px;border-radius:18px;transition:background .25s ease,transform .25s ease}.benefit:hover{background:rgba(248,250,246,.88);transform:translateY(-4px)}.benefit-icon{border:1px solid rgba(211,205,119,.38);background:linear-gradient(145deg,#fffcc7,var(--yellow));box-shadow:0 14px 32px rgba(191,184,90,.16),inset 0 1px 0 rgba(255,255,255,.72)}.benefit:nth-child(2) .benefit-icon{border-color:rgba(169,199,135,.38);background:linear-gradient(145deg,#e9f5db,var(--green));box-shadow:0 14px 32px rgba(151,183,116,.16),inset 0 1px 0 rgba(255,255,255,.72)}.benefit h3{font-weight:650}.benefit p{color:#777e76}
@keyframes softPulse{50%{box-shadow:0 0 0 12px rgba(172,213,125,0)}}
/* Professional product visuals */
.returns-heading h2{font-size:clamp(34px,4.1vw,56px);line-height:1.08;letter-spacing:-.035em}.returns-header{align-items:center}.diamond{width:56px;height:56px;border-radius:15px}.diamond svg{width:28px}
.admin-visual{position:absolute;right:clamp(22px,3vw,46px);bottom:-48px;left:clamp(22px,3vw,46px);height:66%;perspective:1000px}.admin-window{height:100%;overflow:hidden;border:1px solid #dce4d8;border-radius:18px 18px 0 0;background:rgba(255,255,255,.97);box-shadow:0 28px 65px rgba(27,42,22,.16);transform:rotateX(2deg) rotateZ(-1.2deg);transform-origin:center bottom}.admin-window__bar{display:flex;height:38px;align-items:center;gap:18px;padding:0 14px;border-bottom:1px solid #ebefea;background:#fafbf9;color:#9ba19a;font-size:8px}.window-dots{display:flex;gap:5px}.window-dots i{width:6px;height:6px;border-radius:50%;background:#d6dbd4}.window-dots i:nth-child(2){background:var(--yellow)}.window-dots i:nth-child(3){background:var(--green)}.admin-window__bar>span{flex:1;text-align:center}.admin-window__bar>b{color:#7e857d;font-size:10px;letter-spacing:2px}.admin-window__body{display:grid;height:calc(100% - 38px);grid-template-columns:54px 1fr}.admin-sidebar{display:flex;align-items:center;flex-direction:column;gap:16px;padding:13px 0;border-right:1px solid #edf0eb;background:#fafbf9}.admin-logo{display:grid;width:25px;height:25px;place-items:center;margin-bottom:3px;border-radius:8px;background:var(--ink);color:var(--yellow);font-size:9px;font-weight:800}.admin-sidebar>i{width:17px;height:5px;border-radius:99px;background:#dfe4dd}.admin-sidebar>i.is-active{height:17px;background:var(--green);box-shadow:0 0 0 4px rgba(201,230,168,.22)}.admin-content{min-width:0;padding:18px 20px}.admin-content__top{display:flex;align-items:flex-start;justify-content:space-between}.admin-content__top>div{display:flex;flex-direction:column}.admin-content__top small{color:#929991;font-size:7px;font-weight:700;letter-spacing:.11em}.admin-content__top strong{margin-top:4px;font-size:clamp(22px,2.5vw,36px);font-weight:500;letter-spacing:-.05em}.health-badge{display:inline-flex;align-items:center;gap:6px;padding:6px 9px;border:1px solid #e2eadc;border-radius:999px;background:#f7fbf3;color:#66745e;font-size:7px;font-weight:700}.health-badge i{width:6px;height:6px;border-radius:50%;background:#9ecb71}.admin-chart{position:relative;height:72px;margin:3px 0 10px}.admin-chart svg{position:absolute;inset:0;width:100%;height:100%;overflow:visible;fill:none;stroke:var(--ink);stroke-width:2;stroke-linecap:round}.admin-chart svg path{stroke-dasharray:1;stroke-dashoffset:1}.is-visible .admin-chart svg path{animation:draw 1.3s .9s forwards}.admin-bars{position:absolute;inset:10px 0 0;display:flex;align-items:flex-end;gap:7%}.admin-bars i{width:6.5%;height:25%;border-radius:4px 4px 0 0;background:#e8ece6}.admin-bars i:nth-child(2){height:48%}.admin-bars i:nth-child(3){height:38%;background:var(--yellow)}.admin-bars i:nth-child(4){height:67%}.admin-bars i:nth-child(5){height:54%;background:var(--green)}.admin-bars i:nth-child(6){height:78%}.admin-bars i:nth-child(7){height:64%;background:#dfe9d7}.admin-bars i:nth-child(8){height:88%;background:var(--ink)}.admin-stats{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}.admin-stats>div{display:flex;min-width:0;flex-direction:column;padding:8px 9px;border:1px solid #edf0eb;border-radius:9px;background:#fbfcfa}.admin-stats span{color:#8b928a;font-size:6px}.admin-stats strong{margin:2px 0;font-size:11px}.admin-stats small{color:#8ab35f;font-size:6px}.floating-mail-card{position:absolute;right:-10px;bottom:29px;display:flex;align-items:center;gap:9px;min-width:215px;padding:11px 12px;border:1px solid #dce5d7;border-radius:13px;background:rgba(255,255,255,.94);box-shadow:0 18px 42px rgba(24,39,19,.16);backdrop-filter:blur(12px);opacity:0;transform:translateY(16px)}.is-visible .floating-mail-card{animation:rise .65s 1.15s forwards}.mail-card-icon{display:grid;width:32px;height:32px;place-items:center;border-radius:9px;background:var(--green)}.mail-card-icon svg{width:17px;fill:none;stroke:var(--ink);stroke-width:1.7}.floating-mail-card>span:nth-child(2){display:flex;flex:1;flex-direction:column;gap:2px}.floating-mail-card small{color:#90968f;font-size:6px;letter-spacing:.08em}.floating-mail-card strong{font-size:8px}.floating-mail-card>b{display:grid;width:19px;height:19px;place-items:center;border-radius:50%;background:var(--yellow);font-size:8px}
.chart-summary{position:absolute;z-index:2;left:clamp(24px,3vw,42px);top:-5%;display:flex;flex-direction:column}.chart-summary>span{color:#8c938b;font-size:8px;font-weight:750;letter-spacing:.11em}.chart-summary>strong{margin:4px 0;font-size:clamp(27px,3vw,40px);font-weight:500;letter-spacing:-.05em}.chart-summary>small{color:#929891;font-size:8px}.chart-summary b{color:#82ab5d}.chart-tooltip{top:13%;right:7%;min-width:124px;padding:12px 14px;border-width:1.5px;box-shadow:6px 7px 0 rgba(243,238,154,.85),0 18px 38px rgba(27,36,24,.11)}.chart-tooltip strong{font-size:17px}.chart-label{bottom:22px;color:#737a72;font-size:9px;font-weight:650;letter-spacing:.08em;text-transform:uppercase}
@media(max-width:900px){.returns-wrap::before{display:none}.feature-card:hover{box-shadow:0 28px 75px -50px rgba(28,46,22,.48)}.benefits-grid::before{display:none}}
@media(max-width:600px){.feature-card{border-radius:22px}.mini-panel--front{box-shadow:7px 10px 0 rgba(201,230,168,.5),0 22px 46px rgba(29,40,25,.16)}.benefit{padding:8px 4px}.benefit:hover{background:transparent;transform:none}.returns-heading h2{font-size:clamp(32px,9.5vw,42px)}.admin-visual{right:14px;bottom:-34px;left:14px;height:61%}.admin-window__body{grid-template-columns:42px 1fr}.admin-sidebar{gap:12px}.admin-content{padding:13px 12px}.admin-stats>div{padding:7px 5px}.floating-mail-card{right:-4px;bottom:20px;min-width:186px}.chart-summary{top:1%;left:24px}.chart-tooltip{top:18%;right:5%}}
@media(prefers-reduced-motion:reduce){.returns-heading,.diamond-motif,.feature-card,.benefit,.chart-tooltip,.chart-fill,.chart-node,.floating-mail-card{opacity:1!important;transform:none!important;animation:none!important}.analytics-stack{transform:none;animation:none!important}.chart-path,.admin-chart svg path{stroke-dashoffset:0;animation:none!important}.chart-area::after{animation:none!important}}
</style>
