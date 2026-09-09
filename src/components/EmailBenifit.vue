<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const visible = ref(false)
let observer

const benefits = [
  { title: 'Build Customer Trust', text: 'Use professional addresses on your own domain and make every message feel credible.' },
  { title: 'Protect Every Inbox', text: 'Block spam, malware, phishing attempts, and dangerous attachments before delivery.' },
  { title: 'Deliver Messages Reliably', text: 'Keep important conversations moving with dependable infrastructure and 99.9% uptime.' },
  { title: 'Scale Without Complexity', text: 'Add new mailboxes, aliases, storage, and controls as your team continues to grow.' }
]

onMounted(() => {
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) { visible.value = true; observer.disconnect() }
  }, { threshold: 0.16 })
  if (root.value) observer.observe(root.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section ref="root" class="email-benefits" :class="{ 'is-visible': visible }" aria-labelledby="benefits-title">
    <div class="email-benefits__inner">
      <div class="visual" aria-label="Smardove secure email delivery dashboard">
        <div class="visual__grid" />
        <div class="visual__glow" />

        <svg class="performance-line" viewBox="0 0 560 230" preserveAspectRatio="none" aria-hidden="true">
          <path class="performance-line__shadow" d="M15 35H112l42 56 43-38 43 54 52-22 47 65 43-25 48 53 72-22" />
          <path class="performance-line__path" pathLength="1" d="M15 35H112l42 56 43-38 43 54 52-22 47 65 43-25 48 53 72-22" />
        </svg>

        <div class="timer"><svg viewBox="0 0 40 40"><circle cx="20" cy="22" r="13"/><path d="M20 8V3M15 3h10M20 22l7-5"/></svg></div>

        <div class="mail-window">
          <div class="window-bar"><span><i/><i/><i/></span><small>mail.smardove.com</small><b>•••</b></div>
          <div class="window-body">
            <aside><strong>S</strong><i class="active"/><i/><i/><i/><i/></aside>
            <main>
              <header><span><small>DELIVERY OVERVIEW</small><b>Good morning, Naduni</b></span><em>NA</em></header>
              <div class="dashboard">
                <div class="summary"><span><small>MESSAGES DELIVERED</small><strong>24,827</strong><em>↑ 18.4%</em></span><div class="summary-ring">99<small>%</small></div></div>
                <div class="bar-chart"><i/><i/><i/><i/><i/><i/><i/><i/></div>
                <div class="mail-row"><i>AM</i><span><b>Client proposal</b><small>Delivered securely</small></span><em>Now</em></div>
                <div class="mail-row"><i>SK</i><span><b>Team update</b><small>Protected message</small></span><em>2m</em></div>
              </div>
            </main>
          </div>
        </div>

        <div v-for="(item, index) in ['AM','SK','JD','NA','TR','LP']" :key="item" class="person" :class="`person--${index + 1}`"><span>{{ item }}</span><i/></div>
        <div class="delivery-note"><i>✓</i><span><small>SECURE DELIVERY</small><strong>Message delivered</strong></span></div>
      </div>

      <div class="content">
        <header class="content__header">
          <span class="eyebrow">Why Smardove</span>
          <h2 id="benefits-title">Why Professional Email<br><mark>Moves Business Forward</mark></h2>
          <p>Smardove combines branded business email, dependable delivery, and intelligent protection in one clean platform—so your team can communicate with confidence.</p>
        </header>

        <div class="benefit-list">
          <article v-for="(benefit, index) in benefits" :key="benefit.title" :style="{ '--delay': `${.32 + index * .12}s` }">
            <span class="benefit-dot"><i/></span>
            <div><h3>{{ benefit.title }}</h3><p>{{ benefit.text }}</p></div>
            <b>{{ String(index + 1).padStart(2, '0') }}</b>
          </article>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.email-benefits,.email-benefits *{box-sizing:border-box}.email-benefits{--ink:#0d0d0d;--green:#c9e6a8;--green-deep:#91bd67;--yellow:#f3ee9a;--muted:#737a71;width:100%;overflow:hidden;padding:clamp(70px,8vw,125px) clamp(17px,5vw,72px);background:radial-gradient(circle at 8% 12%,rgba(243,238,154,.24),transparent 28%),radial-gradient(circle at 95% 88%,rgba(201,230,168,.25),transparent 30%),#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.email-benefits__inner{display:grid;width:min(1320px,100%);grid-template-columns:1.08fr .92fr;align-items:start;gap:clamp(35px,5vw,78px);margin:auto}.visual{position:sticky;top:40px;min-height:540px;overflow:hidden;border:1px solid #dce4d8;border-radius:25px;background:linear-gradient(145deg,#eff7e7,#f8f5c7);box-shadow:0 28px 75px -48px rgba(30,44,23,.42);opacity:0;transform:translateX(-28px)}.is-visible .visual{animation:visualIn .85s .1s forwards}.visual__grid{position:absolute;inset:0;background-image:linear-gradient(rgba(80,105,61,.07) 1px,transparent 1px),linear-gradient(90deg,rgba(80,105,61,.07) 1px,transparent 1px);background-size:38px 38px;mask-image:linear-gradient(#000,transparent)}.visual__glow{position:absolute;right:-80px;bottom:-100px;width:330px;height:330px;border-radius:50%;background:var(--green);filter:blur(85px);opacity:.45}.performance-line{position:absolute;z-index:1;top:28px;left:5%;width:90%;height:220px;overflow:visible;fill:none}.performance-line__shadow{stroke:rgba(13,13,13,.11);stroke-width:10;filter:blur(8px)}.performance-line__path{stroke:#111;stroke-width:3;stroke-linecap:round;stroke-linejoin:round;stroke-dasharray:1;stroke-dashoffset:1}.is-visible .performance-line__path{animation:draw 1.6s .55s forwards}.timer{position:absolute;z-index:4;top:47px;left:29%;display:grid;width:58px;height:58px;place-items:center;border:5px solid #fff;border-radius:50%;background:var(--yellow);box-shadow:0 13px 30px rgba(50,55,27,.18);opacity:0;transform:scale(.6)}.is-visible .timer{animation:pop .55s 1.15s forwards}.timer svg{width:34px;fill:none;stroke:#1a1d19;stroke-width:2;stroke-linecap:round}.mail-window{position:absolute;z-index:3;top:145px;left:18%;width:68%;height:310px;overflow:hidden;border:7px solid #111;border-radius:16px;background:#fff;box-shadow:0 27px 55px rgba(31,43,24,.23);transform:translateY(35px) scale(.94);opacity:0}.is-visible .mail-window{animation:rise .8s .35s forwards}.window-bar{display:flex;height:31px;align-items:center;padding:0 9px;background:#f3f5f1;color:#9aa097}.window-bar>span{display:flex;gap:4px}.window-bar i{display:block;width:6px;height:6px;border-radius:50%;background:#d2d7d0}.window-bar i:nth-child(2){background:var(--yellow)}.window-bar i:nth-child(3){background:var(--green)}.window-bar small{margin:auto;font-size:5px}.window-bar b{font-size:7px}.window-body{display:grid;height:calc(100% - 31px);grid-template-columns:42px 1fr}.window-body aside{display:flex;align-items:center;flex-direction:column;gap:15px;padding-top:10px;background:#111}.window-body aside strong{display:grid;width:22px;height:22px;place-items:center;border-radius:7px;background:var(--yellow);font-size:7px}.window-body aside i{width:15px;height:5px;border-radius:8px;background:#4f544e}.window-body aside i.active{height:15px;background:var(--green)}.window-body main>header{display:flex;height:48px;align-items:center;padding:0 12px;border-bottom:1px solid #e7ebe4}.window-body main>header span{display:flex;flex-direction:column}.window-body main>header small{color:#979e95;font-size:4px}.window-body main>header b{font-size:7px}.window-body main>header em{display:grid;width:22px;height:22px;margin-left:auto;place-items:center;border-radius:50%;background:var(--green);font-size:5px;font-style:normal;font-weight:800}.dashboard{padding:11px}.summary{display:flex;align-items:center;justify-content:space-between}.summary>span{display:flex;flex-direction:column}.summary small{color:#969d94;font-size:4px}.summary strong{margin:2px 0;font-size:18px}.summary em{color:#78a154;font-size:4px;font-style:normal}.summary-ring{display:grid;width:42px;height:42px;place-items:center;border-radius:50%;background:conic-gradient(var(--green-deep) 0 99%,#e7ebe4 99%);box-shadow:inset 0 0 0 5px #fff;font-size:9px;font-weight:700}.summary-ring small{font-size:4px}.bar-chart{display:flex;height:55px;align-items:flex-end;gap:7px;margin:6px 0}.bar-chart i{width:10%;border-radius:3px 3px 0 0;background:#e4e9e1}.bar-chart i:nth-child(1){height:25%}.bar-chart i:nth-child(2){height:48%;background:var(--yellow)}.bar-chart i:nth-child(3){height:34%}.bar-chart i:nth-child(4){height:68%;background:var(--green)}.bar-chart i:nth-child(5){height:52%}.bar-chart i:nth-child(6){height:81%;background:#222}.bar-chart i:nth-child(7){height:63%}.bar-chart i:nth-child(8){height:90%;background:var(--green)}.mail-row{display:flex;align-items:center;gap:7px;padding:7px 0;border-top:1px solid #e7ebe4}.mail-row>i{display:grid;width:20px;height:20px;place-items:center;border-radius:50%;background:var(--green);font-size:4px;font-style:normal;font-weight:800}.mail-row:nth-child(4)>i{background:var(--yellow)}.mail-row>span{display:flex;flex-direction:column}.mail-row b{font-size:5px}.mail-row small{color:#969c94;font-size:4px}.mail-row em{margin-left:auto;color:#969c94;font-size:4px;font-style:normal}.person{position:absolute;z-index:5;width:39px;height:39px;padding:3px;border-radius:50%;background:#fff;box-shadow:0 9px 22px rgba(31,43,24,.18);opacity:0;transform:scale(.6)}.person span{display:grid;width:100%;height:100%;place-items:center;border-radius:50%;background:#1b1e1a;color:#fff;font-size:7px;font-weight:800}.person i{position:absolute;right:1px;bottom:1px;width:9px;height:9px;border:2px solid #fff;border-radius:50%;background:var(--green-deep)}.person--1{top:215px;right:8%}.person--2{top:268px;right:3%}.person--3{top:330px;right:9%}.person--4{right:19%;bottom:44px}.person--5{right:31%;bottom:23px}.person--6{right:43%;bottom:52px}.is-visible .person{animation:pop .48s calc(.85s + var(--i,0s)) forwards}.person--2{animation-delay:.96s!important}.person--3{animation-delay:1.07s!important}.person--4{animation-delay:1.18s!important}.person--5{animation-delay:1.29s!important}.person--6{animation-delay:1.4s!important}.delivery-note{position:absolute;z-index:7;right:4%;bottom:24px;display:flex;align-items:center;gap:9px;padding:10px 13px;border:1px solid #d9e3d4;border-radius:12px;background:rgba(255,255,255,.92);box-shadow:0 16px 34px rgba(31,43,24,.15);opacity:0;transform:translateY(15px);backdrop-filter:blur(12px)}.is-visible .delivery-note{animation:rise .55s 1.35s forwards}.delivery-note>i{display:grid;width:27px;height:27px;place-items:center;border-radius:8px;background:var(--green);font-size:8px;font-style:normal}.delivery-note span{display:flex;flex-direction:column}.delivery-note small{color:#929990;font-size:4px}.delivery-note strong{font-size:6px}.content__header{opacity:0;transform:translateY(22px)}.is-visible .content__header{animation:rise .72s .18s forwards}.eyebrow{display:inline-flex;margin-bottom:18px;padding:7px 13px;border:1px solid #c4dcb0;border-radius:999px;background:#f6fbf1;font-size:8px;font-weight:750;letter-spacing:.1em;text-transform:uppercase}.content h2{margin:0;font-family:var(--font-display,var(--font-sans));font-size:clamp(35px,3.8vw,56px);font-weight:430;line-height:1.04;letter-spacing:-.05em}.content h2 mark{padding:0 2px;background:linear-gradient(transparent 64%,var(--yellow) 64%);color:#8b9189}.content__header>p{max-width:580px;margin:22px 0 28px;color:var(--muted);font-size:clamp(11px,.93vw,14px);line-height:1.68}.benefit-list{display:flex;flex-direction:column;gap:13px}.benefit-list article{position:relative;display:grid;min-height:103px;grid-template-columns:20px 1fr auto;align-items:start;gap:13px;padding:21px 23px;border:1px solid #dfe5dc;border-radius:16px;background:rgba(255,255,255,.85);box-shadow:0 11px 32px rgba(30,43,23,.045);opacity:0;transform:translateX(24px);transition:border-color .25s ease,transform .25s ease,box-shadow .25s ease}.is-visible .benefit-list article{animation:cardIn .6s var(--delay) forwards}.benefit-list article:hover{border-color:#bdd7a6;box-shadow:0 16px 38px rgba(30,43,23,.09);transform:translateX(-5px)}.benefit-dot{display:grid;width:19px;height:19px;place-items:center;border-radius:50%;background:rgba(201,230,168,.35)}.benefit-dot i{width:7px;height:7px;border-radius:50%;background:var(--green-deep);box-shadow:0 0 0 4px rgba(145,189,103,.12)}.benefit-list article:nth-child(even) .benefit-dot{background:rgba(243,238,154,.42)}.benefit-list article:nth-child(even) .benefit-dot i{background:#d0c546}.benefit-list h3{margin:0 0 7px;font-size:clamp(13px,1.05vw,16px);font-weight:680;letter-spacing:-.025em}.benefit-list p{margin:0;color:#858b83;font-size:clamp(9px,.75vw,11px);line-height:1.55}.benefit-list article>b{color:#d7ddd4;font-size:10px}
@keyframes rise{to{opacity:1;transform:translateY(0) scale(1)}}@keyframes visualIn{to{opacity:1;transform:translateX(0)}}@keyframes cardIn{to{opacity:1;transform:translateX(0)}}@keyframes draw{to{stroke-dashoffset:0}}@keyframes pop{70%{opacity:1;transform:scale(1.15)}100%{opacity:1;transform:scale(1)}}
@media(max-width:900px){.email-benefits__inner{grid-template-columns:1fr}.visual{position:relative;top:auto;min-height:520px}.content{max-width:700px;margin:auto}}
@media(max-width:600px){.email-benefits{padding:55px 14px}.visual{min-height:460px;border-radius:20px}.mail-window{top:135px;left:8%;width:75%;height:275px}.timer{left:20%}.person{width:33px;height:33px}.delivery-note{right:2%;bottom:13px}.content h2{font-size:clamp(35px,10vw,47px)}.benefit-list article{padding:19px 17px}}
@media(prefers-reduced-motion:reduce){.visual,.mail-window,.timer,.person,.delivery-note,.content__header,.benefit-list article{opacity:1!important;transform:none!important;animation:none!important}.performance-line__path{stroke-dashoffset:0!important;animation:none!important}}
</style>
