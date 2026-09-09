<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const visible = ref(false)
let observer

const plans = [
  { plan: 'Business Starter', storage: '25 GB', share: '38%', tone: 'green' },
  { plan: 'Business Pro', storage: '50 GB', share: '27%', tone: 'plain' },
  { plan: 'Team Workspace', storage: '100 GB', share: '18%', tone: 'yellow' },
  { plan: 'Enterprise Mail', storage: 'Custom', share: '11%', tone: 'plain' },
  { plan: 'Email Security+', storage: 'Add-on', share: '6%', tone: 'green' }
]

onMounted(() => {
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      visible.value = true
      observer.disconnect()
    }
  }, { threshold: 0.16 })
  if (root.value) observer.observe(root.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section ref="root" class="market" :class="{ 'is-visible': visible }" aria-labelledby="market-title">
    <div class="shape shape--top" aria-hidden="true"><i/><i/><i/></div>
    <div class="shape shape--bottom" aria-hidden="true"><i/><i/><i/></div>

    <div class="market__inner">
      <div class="eyebrow"><strong>Email Hosting</strong><span /></div>

      <header class="market__header">
        <h2 id="market-title">Professional Email That Helps<br><mark>Your Business Grow</mark></h2>
        <p>Flexible plans for every stage of your business, with reliable delivery, generous storage, and advanced protection included.</p>
      </header>

      <div class="market__grid">
        <article class="share-card">
          <a class="corner-link" href="https://smardove.com/features/" aria-label="Explore email features">↗</a>
          <div class="card-heading">
            <span>POPULAR PLAN MIX</span>
            <h3>Business email plans chosen by growing teams</h3>
          </div>

          <div class="donut-wrap">
            <div class="donut" role="img" aria-label="68 percent business plans and 32 percent enterprise solutions">
              <div class="donut__center">
                <svg viewBox="0 0 40 40"><rect x="7" y="11" width="26" height="20" rx="4"/><path d="m8 14 12 9 12-9M15 8h10"/></svg>
              </div>
            </div>
            <span class="donut-value donut-value--large"><strong>68%</strong><small>Business plans</small></span>
            <span class="donut-value donut-value--small"><strong>32%</strong><small>Advanced plans</small></span>
          </div>

          <div class="legend">
            <span><i class="legend__green"/>Business email</span>
            <span><i class="legend__yellow"/>Enterprise &amp; add-ons</span>
          </div>
        </article>

        <article class="plans-card">
          <div class="plans-title">
            <span>TOP SOLUTIONS</span>
            <h3>Most selected Smardove email products</h3>
          </div>

          <div class="plans-table" role="table" aria-label="Most selected Smardove plans">
            <div class="table-row table-head" role="row">
              <span role="columnheader">Product</span><span role="columnheader">Mailbox</span><span role="columnheader">Share</span>
            </div>
            <div v-for="(item, index) in plans" :key="item.plan" class="table-row" :class="`table-row--${item.tone}`" role="row" :style="{ '--delay': `${.58 + index * .11}s` }">
              <span role="cell"><b>{{ String(index + 1).padStart(2, '0') }}</b>{{ item.plan }}</span>
              <span role="cell">{{ item.storage }}</span>
              <strong role="cell">{{ item.share }}</strong>
            </div>
          </div>

          <div class="table-footer">
            <span><i/>99.9% delivery uptime</span>
            <a href="https://smardove.com/features/">Compare all plans <b>↗</b></a>
          </div>
        </article>
      </div>

      <footer class="source"><span>Smardove product overview</span><i/><strong>Secure email built for modern business</strong></footer>
    </div>
  </section>
</template>

<style scoped>
.market,.market *{box-sizing:border-box}.market{--ink:#0d0d0d;--muted:#747a72;--line:#e5e9e2;--green:#c9e6a8;--green-deep:#98c46e;--yellow:#f3ee9a;position:relative;isolation:isolate;overflow:hidden;width:100%;padding:clamp(60px,7vw,108px) clamp(18px,6vw,90px) 35px;background:radial-gradient(circle at 92% 5%,rgba(201,230,168,.3),transparent 25%),radial-gradient(circle at 0 100%,rgba(243,238,154,.36),transparent 28%),#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.market::before{position:absolute;z-index:-2;inset:0;background-image:linear-gradient(rgba(13,13,13,.018) 1px,transparent 1px),linear-gradient(90deg,rgba(13,13,13,.018) 1px,transparent 1px);background-size:48px 48px;mask-image:linear-gradient(#000,transparent 43%);content:""}.market__inner{width:min(1400px,100%);margin:auto}.eyebrow{display:flex;align-items:center;gap:15px;margin-bottom:clamp(35px,4vw,58px);font-size:11px}.eyebrow strong{font-weight:700}.eyebrow span{display:block;height:1px;flex:1;background:linear-gradient(90deg,#bcc4b8,transparent)}.market__header{max-width:1050px;margin-bottom:clamp(35px,4.5vw,66px);opacity:0;transform:translateY(22px)}.is-visible .market__header{animation:rise .75s .08s forwards}.market h2{margin:0;font-family:var(--font-display,var(--font-sans));font-size:clamp(38px,4.6vw,68px);font-weight:380;line-height:1.08;letter-spacing:-.042em}.market h2 mark{padding:0 3px;background:linear-gradient(transparent 64%,var(--yellow) 64%);color:inherit}.market__header p{max-width:720px;margin:19px 0 0;color:var(--muted);font-size:clamp(11px,.95vw,14px);line-height:1.7}.market__grid{display:grid;grid-template-columns:.92fr 1.08fr;gap:clamp(24px,3vw,46px)}.share-card,.plans-card{position:relative;min-width:0;min-height:510px;border:1px solid rgba(220,226,216,.9);border-radius:28px;background:rgba(249,250,247,.9);box-shadow:0 27px 75px -50px rgba(29,42,23,.38);opacity:0;transform:translateY(28px);backdrop-filter:blur(16px)}.is-visible .share-card{animation:rise .8s .22s forwards}.is-visible .plans-card{animation:rise .8s .34s forwards}.share-card{padding:clamp(28px,3vw,45px)}.corner-link{position:absolute;top:25px;right:25px;display:grid;width:43px;height:43px;place-items:center;border:1px solid #ccd4c8;border-radius:50%;color:var(--ink);font-size:20px;text-decoration:none;transition:transform .25s ease,background .25s ease}.corner-link:hover{background:var(--green);transform:rotate(45deg)}.card-heading>span,.plans-title>span{color:#92998f;font-size:8px;font-weight:800;letter-spacing:.13em}.card-heading h3,.plans-title h3{max-width:470px;margin:7px 0 0;font-size:clamp(17px,1.45vw,22px);font-weight:600;line-height:1.35;letter-spacing:-.025em}.donut-wrap{position:relative;display:grid;min-height:330px;place-items:center;margin-top:6px}.donut{position:relative;width:clamp(190px,19vw,275px);aspect-ratio:1;border-radius:50%;background:conic-gradient(var(--green-deep) 0 68%,var(--yellow) 68% 100%);box-shadow:0 24px 50px rgba(50,68,40,.1);transform:rotate(-90deg) scale(.75);opacity:0}.is-visible .donut{animation:donutIn 1s .55s cubic-bezier(.17,.82,.28,1.15) forwards}.donut::before{position:absolute;inset:27%;border-radius:50%;background:#fafbf8;box-shadow:inset 0 0 0 1px #e7ebe4;content:""}.donut__center{position:absolute;z-index:2;inset:34%;display:grid;place-items:center;border-radius:50%;background:#fff;transform:rotate(90deg)}.donut__center svg{width:38px;fill:none;stroke:#252a24;stroke-width:1.6;stroke-linecap:round;stroke-linejoin:round}.donut-value{position:absolute;display:flex;flex-direction:column;opacity:0}.is-visible .donut-value{animation:fade .55s .95s forwards}.donut-value strong{font-size:clamp(22px,2.2vw,32px);font-weight:520}.donut-value small{color:var(--muted);font-size:8px}.donut-value--large{bottom:44px;left:1%}.donut-value--small{top:95px;right:3%}.legend{position:absolute;right:38px;bottom:33px;display:flex;flex-direction:column;gap:10px;color:#666d64;font-size:9px}.legend span{display:flex;align-items:center;gap:9px}.legend i{width:15px;height:15px;border-radius:50%}.legend__green{background:var(--green-deep)}.legend__yellow{background:var(--yellow)}.plans-card{padding:clamp(28px,3vw,45px);background:rgba(255,255,255,.94)}.plans-title{margin-bottom:25px}.plans-table{overflow:hidden;border-radius:15px}.table-row{display:grid;min-height:61px;grid-template-columns:1.7fr .8fr .45fr;align-items:center;padding:0 clamp(15px,2vw,28px);border-bottom:1px solid #e8ece6;color:#555c53;font-size:clamp(10px,.85vw,13px);opacity:0;transform:translateX(20px)}.is-visible .table-row:not(.table-head){animation:rowIn .6s var(--delay) forwards}.table-row span:first-child{display:flex;align-items:center;gap:12px}.table-row span:first-child b{color:#abb1a9;font-size:9px}.table-row strong{text-align:right;color:#1b211a;font-size:13px}.table-head{min-height:58px;border:0;background:#111;color:#fff;font-size:9px;font-weight:750;letter-spacing:.05em;opacity:1;transform:none}.table-head span:last-child{text-align:right}.table-row--green{background:linear-gradient(90deg,rgba(201,230,168,.55),rgba(201,230,168,.22))}.table-row--yellow{background:linear-gradient(90deg,rgba(243,238,154,.5),rgba(243,238,154,.18))}.table-footer{display:flex;align-items:center;justify-content:space-between;margin-top:24px;color:#7d847a;font-size:9px}.table-footer>span{display:flex;align-items:center;gap:7px}.table-footer>span i{width:7px;height:7px;border-radius:50%;background:var(--green-deep);box-shadow:0 0 0 5px rgba(201,230,168,.24)}.table-footer a{display:flex;align-items:center;gap:8px;color:var(--ink);font-weight:700;text-decoration:none}.table-footer a b{display:grid;width:25px;height:25px;place-items:center;border-radius:50%;background:var(--yellow)}.source{display:flex;align-items:center;justify-content:flex-end;gap:12px;margin-top:25px;color:#949a92;font-size:8px}.source i{width:35px;height:1px;background:#d9ded6}.source strong{color:#5c635a;font-weight:650}.shape{position:absolute;z-index:-1;width:260px;height:210px;pointer-events:none;opacity:.72}.shape i{position:absolute;border:1px solid rgba(255,255,255,.75);border-radius:42% 58% 55% 45%;background:linear-gradient(145deg,rgba(201,230,168,.9),rgba(243,238,154,.7));box-shadow:inset 0 0 22px rgba(255,255,255,.75),0 20px 50px rgba(52,72,42,.12)}.shape i:nth-child(1){inset:5% 5% 30% 18%;transform:rotate(18deg)}.shape i:nth-child(2){inset:32% 18% 5% 0;transform:rotate(-22deg)}.shape i:nth-child(3){inset:14% 0 18% 42%;transform:rotate(38deg)}.shape--top{top:-60px;right:-35px;transform:rotate(20deg)}.shape--bottom{bottom:-75px;left:-60px;transform:rotate(-25deg)}.is-visible .shape{animation:shapeFloat 6s ease-in-out infinite}
@keyframes rise{to{opacity:1;transform:translateY(0)}}@keyframes rowIn{to{opacity:1;transform:translateX(0)}}@keyframes fade{to{opacity:1}}@keyframes donutIn{to{opacity:1;transform:rotate(-90deg) scale(1)}}@keyframes shapeFloat{50%{translate:0 -12px;rotate:4deg}}
@media(max-width:900px){.market__grid{grid-template-columns:1fr}.share-card,.plans-card{min-height:500px}.shape{opacity:.45}}
@media(max-width:600px){.market{padding:52px 14px 28px}.market h2{font-size:clamp(35px,10.5vw,48px)}.market__grid{gap:18px}.share-card,.plans-card{min-height:auto;border-radius:22px;padding:25px 20px}.donut-wrap{min-height:315px}.donut-value--large{bottom:42px}.donut-value--small{top:78px}.legend{position:static;align-items:center;flex-direction:row;justify-content:center;margin-top:-12px}.table-row{min-height:58px;grid-template-columns:1.55fr .65fr .42fr;padding:0 12px}.table-row span:first-child{gap:7px}.table-footer{align-items:flex-start;flex-direction:column;gap:18px}.source{justify-content:flex-start}.shape{width:180px;height:150px}}
@media(prefers-reduced-motion:reduce){.market__header,.share-card,.plans-card,.table-row,.donut,.donut-value{opacity:1!important;transform:none!important;animation:none!important}.shape{animation:none!important}}
</style>
