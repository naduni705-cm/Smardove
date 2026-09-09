<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const section = ref(null)
const visible = ref(false)
let observer

onMounted(() => {
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      visible.value = true
      observer.disconnect()
    }
  }, { threshold: 0.18 })
  if (section.value) observer.observe(section.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section ref="section" class="overview" :class="{ 'is-visible': visible }" aria-labelledby="overview-title">
    <div class="overview__wash" aria-hidden="true" />
    <div class="overview__orb overview__orb--one" aria-hidden="true" />
    <div class="overview__orb overview__orb--two" aria-hidden="true" />

    <div class="overview__inner">
      <div class="eyebrow"><span>01</span><b>Product</b><i /></div>
      <header class="overview__header">
        <h2 id="overview-title">Overview <mark>Product</mark></h2>
        <p>Professional business email designed for secure communication, effortless management, and dependable growth.</p>
      </header>

      <div class="showcase">
        <svg class="route route--left" viewBox="0 0 240 200" aria-hidden="true"><path pathLength="1" d="M226 10C82 24 202 163 18 185" /></svg>
        <svg class="route route--right" viewBox="0 0 250 170" aria-hidden="true"><path pathLength="1" d="M10 8c139 4 86 139 230 151" /></svg>

        <div class="profile profile--left" aria-label="Connected team member"><span>AM</span><i /></div>
        <div class="profile profile--top" aria-label="Connected company"><span>NA</span><i /></div>

        <div class="trust-card">
          <span class="trust-card__icon">
            <svg viewBox="0 0 24 24"><path d="M12 3 20 6v5c0 5.2-3.1 8.3-8 10-4.9-1.7-8-4.8-8-10V6Z"/><path d="m8.5 12 2.2 2.2 4.8-5"/></svg>
          </span>
          <span><small>TRUSTED BUSINESS EMAIL</small><strong>Powering companies worldwide</strong></span>
        </div>

        <div class="laptop" aria-label="Smardove email product dashboard">
          <div class="laptop__screen">
            <div class="app">
              <aside class="app__side">
                <div class="app__logo">S</div>
                <i class="active"/><i/><i/><i/><i/>
              </aside>
              <main class="app__main app__main--premium">
                <div class="app__top premium-top">
                  <div class="premium-title"><small>WORKSPACE</small><span>Good morning, Naduni</span></div>
                  <div class="premium-actions"><button aria-label="Search">⌕</button><button class="notification" aria-label="Notifications">●</button><b>NA</b></div>
                </div>
                <div class="premium-content">
                  <div class="premium-intro"><div><h4>Email command center</h4><p>Monitor performance, security and team activity.</p></div><button>+ New mailbox</button></div>
                  <div class="premium-grid">
                    <section class="delivery-panel">
                      <div class="panel-heading"><span><small>DELIVERY PERFORMANCE</small><strong>24,827</strong></span><b>+18.4%</b></div>
                      <div class="mail-chart premium-chart">
                        <svg viewBox="0 0 520 118" preserveAspectRatio="none"><defs><linearGradient id="premiumArea" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#c9e6a8" stop-opacity=".6"/><stop offset="1" stop-color="#c9e6a8" stop-opacity="0"/></linearGradient></defs><path class="area" d="M0 100C50 92 75 72 120 77s72 10 110-20 76-29 111-2 67 40 100 8 43-45 79-43v98H0Z"/><path class="line" pathLength="1" d="M0 100C50 92 75 72 120 77s72 10 110-20 76-29 111-2 67 40 100 8 43-45 79-43"/><circle cx="441" cy="63" r="5"/></svg>
                      </div>
                    </section>
                    <aside class="security-panel"><div class="security-ring"><span>99.9<small>%</small></span></div><strong>Protection score</strong><small>Spam and malware blocked</small><div class="secure-status"><i/> All systems secure</div></aside>
                  </div>
                  <div class="activity-row"><div><span class="activity-icon">✉</span><span><strong>Message delivered</strong><small>hello@smardove.com · 2 min ago</small></span></div><b>Delivered</b></div>
                </div>
              </main>
            </div>
          </div>
          <div class="laptop__base"><i /></div>
        </div>

        <aside class="value-card">
          <span class="value-card__icon"><svg viewBox="0 0 32 32"><path d="M7 25V13l9-6 9 6v12M11 25v-8h10v8M4 25h24"/><path d="M13 12h6"/></svg></span>
          <h3>Built for modern business</h3>
          <p>Secure mailboxes, intelligent protection, and simple control—all in one clean platform.</p>
          <a href="https://smardove.com/features/">Explore features <span>↗</span></a>
        </aside>
      </div>

      <div class="overview__foot"><span>Smardove Business Email</span><i/><b>Secure. Simple. Professional.</b></div>
    </div>
  </section>
</template>

<style scoped>
.overview,.overview *{box-sizing:border-box}.overview{--ink:#0d0d0d;--green:#c9e6a8;--green-deep:#a9cf7e;--yellow:#f3ee9a;--muted:#6f756d;position:relative;isolation:isolate;min-height:760px;overflow:hidden;padding:clamp(28px,4vw,58px) clamp(16px,5vw,72px) 28px;background:#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.overview__wash{position:absolute;z-index:-3;inset:0 0 16%;background:radial-gradient(circle at 10% 8%,rgba(243,238,154,.92),transparent 34%),radial-gradient(circle at 92% 10%,rgba(169,207,126,.9),transparent 37%),linear-gradient(115deg,#f7f4ba 0%,#dcebb9 50%,#b8dd91 100%);clip-path:ellipse(92% 82% at 50% 0)}.overview__wash::after{position:absolute;inset:0;background-image:linear-gradient(rgba(255,255,255,.13) 1px,transparent 1px),linear-gradient(90deg,rgba(255,255,255,.13) 1px,transparent 1px);background-size:52px 52px;mask-image:linear-gradient(#000,transparent 75%);content:""}.overview__orb{position:absolute;z-index:-2;border:1px dashed rgba(13,13,13,.18);border-radius:50%}.overview__orb--one{top:-88px;right:-54px;width:250px;height:250px}.overview__orb--two{top:182px;left:14%;width:138px;height:138px}.overview__inner{width:min(1420px,100%);margin:auto}.eyebrow{display:flex;align-items:center;gap:24px;color:rgba(13,13,13,.64);font-size:12px}.eyebrow span{font-weight:800}.eyebrow b{font-weight:650}.eyebrow i{display:block;width:42px;height:1px;background:rgba(13,13,13,.48)}.overview__header{position:relative;z-index:2;max-width:840px;margin:7px auto 0;text-align:center;opacity:0;transform:translateY(20px)}.is-visible .overview__header{animation:rise .75s .08s forwards}.overview__header h2{margin:0;font-family:var(--font-display,var(--font-sans));font-size:clamp(42px,5.8vw,82px);font-weight:380;line-height:1.04;letter-spacing:-.045em}.overview__header mark{padding:0 3px;background:linear-gradient(transparent 64%,var(--yellow) 64%);color:inherit}.overview__header p{max-width:740px;margin:18px auto 0;color:rgba(13,13,13,.6);font-size:clamp(12px,1vw,15px);line-height:1.7}.showcase{position:relative;min-height:520px;margin-top:6px}.route{position:absolute;z-index:0;overflow:visible;fill:none;stroke:rgba(13,13,13,.24);stroke-width:1.3;stroke-dasharray:5 7}.route path{stroke-dasharray:1;stroke-dashoffset:1}.is-visible .route path{animation:draw 1.4s .65s forwards}.route--left{top:50px;left:8%;width:235px}.route--right{top:42px;right:10%;width:250px}.profile{position:absolute;z-index:5;display:grid;width:76px;height:76px;place-items:center;border:5px solid rgba(255,255,255,.9);border-radius:50%;background:linear-gradient(145deg,#252925,#0d0d0d);box-shadow:0 18px 38px rgba(33,45,26,.2);color:var(--yellow);font-size:17px;font-weight:800;opacity:0;transform:scale(.7)}.profile i{position:absolute;right:1px;bottom:2px;width:14px;height:14px;border:3px solid #fff;border-radius:50%;background:#83b951}.profile--left{top:220px;left:7%}.profile--top{top:32px;left:34%}.is-visible .profile{animation:pop .55s .7s forwards}.is-visible .profile--top{animation-delay:.83s}.trust-card{position:absolute;z-index:6;top:47px;left:38%;display:flex;min-width:330px;align-items:center;gap:13px;padding:13px 18px;border:1px solid rgba(220,227,216,.85);border-radius:16px;background:rgba(255,255,255,.9);box-shadow:0 17px 45px rgba(39,53,31,.13);backdrop-filter:blur(14px);opacity:0;transform:translateY(18px)}.is-visible .trust-card{animation:rise .6s .85s forwards}.trust-card__icon{display:grid;width:39px;height:39px;place-items:center;border-radius:11px;background:var(--green)}.trust-card svg{width:21px;fill:none;stroke:var(--ink);stroke-width:1.7;stroke-linecap:round;stroke-linejoin:round}.trust-card>span:last-child{display:flex;flex-direction:column}.trust-card small{color:#8a9087;font-size:7px;letter-spacing:.1em}.trust-card strong{margin-top:3px;font-size:12px}.laptop{position:absolute;z-index:2;top:75px;left:50%;width:min(58vw,780px);transform:translateX(-50%) translateY(34px);opacity:0}.is-visible .laptop{animation:laptopIn .9s .28s cubic-bezier(.18,.86,.26,1) forwards}.laptop__screen{height:390px;padding:12px 12px 0;border-radius:24px 24px 10px 10px;background:#111;box-shadow:0 32px 65px rgba(34,44,28,.23)}.app{display:grid;height:100%;grid-template-columns:58px 1fr;overflow:hidden;border-radius:14px 14px 4px 4px;background:#fff}.app__side{display:flex;align-items:center;flex-direction:column;gap:24px;padding:18px 0;background:#111}.app__logo{display:grid;width:30px;height:30px;place-items:center;margin-bottom:8px;border-radius:9px;background:var(--yellow);font-size:12px;font-weight:900}.app__side>i{width:20px;height:6px;border-radius:99px;background:#555}.app__side>i.active{height:20px;background:var(--green);box-shadow:0 0 0 5px rgba(201,230,168,.15)}.app__main{min-width:0}.app__top{display:flex;height:55px;align-items:center;justify-content:space-between;padding:0 23px;border-bottom:1px solid #edf0eb;font-size:11px;font-weight:700}.app__top>div{display:flex;align-items:center;gap:10px}.app__top i{width:8px;height:8px;border-radius:50%;background:var(--green)}.app__top i:nth-child(2){background:var(--yellow)}.app__top b{display:grid;width:28px;height:28px;place-items:center;border-radius:50%;background:#111;color:#fff;font-size:8px}.app__content{padding:21px 25px}.metric{display:flex;align-items:baseline;gap:12px}.metric small{color:#999;font-size:7px;letter-spacing:.1em}.metric strong{font-size:29px;font-weight:500;letter-spacing:-.05em}.metric span{color:#719b50;font-size:7px}.mini-metrics{display:flex;gap:7px;margin:11px 0}.mini-metrics>span{display:flex;min-width:88px;flex-direction:column;padding:8px 10px;border:1px solid #edf0eb;border-radius:9px;background:#fafbf9}.mini-metrics b{font-size:11px}.mini-metrics small{color:#999;font-size:6px}.mail-chart{height:103px}.mail-chart svg{width:100%;height:100%;overflow:visible}.mail-chart .area{fill:rgba(201,230,168,.32)}.mail-chart .line{fill:none;stroke:#171917;stroke-width:2;stroke-linecap:round;stroke-dasharray:1;stroke-dashoffset:1}.is-visible .mail-chart .line{animation:draw 1.45s 1s forwards}.app__stats{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;border-top:1px solid #edf0eb;padding-top:12px}.app__stats span{display:flex;flex-direction:column}.app__stats b{font-size:15px}.app__stats small{color:#999;font-size:6px}.laptop__base{position:relative;width:112%;height:22px;margin-left:-6%;border-radius:3px 3px 50% 50%;background:linear-gradient(#e8eae7,#8a8f89 55%,#383b38);box-shadow:0 15px 17px rgba(10,14,9,.22)}.laptop__base i{position:absolute;top:0;left:43%;width:14%;height:5px;border-radius:0 0 6px 6px;background:#aaa}.value-card{position:absolute;z-index:7;top:145px;right:4%;width:min(31vw,390px);padding:30px 32px;border:1px solid rgba(225,230,222,.95);border-radius:22px;background:rgba(255,255,255,.94);box-shadow:0 28px 70px rgba(34,46,27,.18);backdrop-filter:blur(18px);opacity:0;transform:translateX(30px)}.is-visible .value-card{animation:sideIn .72s .72s forwards}.value-card__icon{display:grid;width:50px;height:50px;place-items:center;margin-bottom:21px;border-radius:15px;background:linear-gradient(145deg,var(--yellow),#fffbc2)}.value-card svg{width:26px;fill:none;stroke:var(--ink);stroke-width:1.6;stroke-linecap:round;stroke-linejoin:round}.value-card h3{margin:0 0 11px;font-size:clamp(18px,1.6vw,24px);font-weight:620;letter-spacing:-.035em}.value-card p{margin:0;color:var(--muted);font-size:12px;line-height:1.65}.value-card a{display:inline-flex;align-items:center;gap:9px;margin-top:20px;color:var(--ink);font-size:11px;font-weight:750;text-decoration:none}.value-card a span{display:grid;width:23px;height:23px;place-items:center;border-radius:50%;background:var(--green)}.overview__foot{display:flex;align-items:center;gap:16px;margin-top:4px;color:#7c827a;font-size:10px}.overview__foot i{width:38px;height:1px;background:#d9ded6}.overview__foot b{color:#30342f;font-weight:650}
@keyframes rise{to{opacity:1;transform:translateY(0)}}@keyframes sideIn{to{opacity:1;transform:translateX(0)}}@keyframes laptopIn{to{opacity:1;transform:translateX(-50%) translateY(0)}}@keyframes draw{to{stroke-dashoffset:0}}@keyframes pop{70%{opacity:1;transform:scale(1.12)}100%{opacity:1;transform:scale(1)}}
@media(max-width:980px){.overview{min-height:auto;padding-bottom:70px}.overview__wash{bottom:28%;clip-path:ellipse(120% 76% at 50% 0)}.showcase{min-height:720px}.laptop{top:105px;width:min(86vw,760px)}.value-card{top:410px;right:3%;width:340px}.profile--left{top:330px;left:1%}.trust-card{top:73px;left:34%}.route--left{top:170px;left:1%}.overview__foot{margin-top:0}}
@media(max-width:650px){.overview{padding-inline:14px}.overview__wash{bottom:43%;clip-path:ellipse(170% 74% at 50% 0)}.eyebrow{gap:14px}.overview__header{margin-top:23px}.overview__header h2{font-size:clamp(42px,13vw,62px)}.showcase{min-height:745px;margin-top:25px}.laptop{top:100px;width:96%}.laptop__screen{height:300px;padding:7px 7px 0;border-radius:15px 15px 7px 7px}.app{grid-template-columns:38px 1fr}.app__side{gap:16px;padding-top:12px}.app__logo{width:23px;height:23px}.app__side>i{width:15px}.app__content{padding:13px 12px}.app__top{height:42px;padding:0 12px}.mini-metrics>span{min-width:0;flex:1;padding:6px}.mail-chart{height:74px}.app__stats{gap:4px}.app__stats b{font-size:11px}.trust-card{top:55px;left:50%;min-width:260px;padding:10px 12px;transform:translateX(-50%) translateY(18px)}.is-visible .trust-card{animation:mobileTrust .6s .85s forwards}.profile{width:58px;height:58px;border-width:4px;font-size:12px}.profile--top{top:25px;left:5%}.profile--left{top:330px;left:4%}.route{display:none}.value-card{top:430px;right:0;left:0;width:100%;padding:25px;border-radius:20px}.overview__foot{align-items:flex-start;flex-direction:column;gap:7px}.overview__foot i{display:none}}
@keyframes mobileTrust{to{opacity:1;transform:translateX(-50%) translateY(0)}}
/* Premium laptop product UI */
.app__main--premium{background:#f5f7f3}.premium-top{height:58px;background:rgba(255,255,255,.92);box-shadow:0 1px 0 #e8ece6}.premium-title{display:flex;flex-direction:column;gap:2px}.premium-title small{color:#9aa097;font-size:5px;font-weight:800;letter-spacing:.14em}.premium-title span{font-size:11px;font-weight:700;letter-spacing:-.02em}.premium-actions{display:flex!important;align-items:center;gap:7px!important}.premium-actions button{display:grid;width:26px;height:26px;padding:0;place-items:center;border:1px solid #e4e9e1;border-radius:8px;background:#fff;color:#687066;font:600 13px/1 Arial}.premium-actions .notification{position:relative;color:#9bc76f;font-size:8px}.premium-actions .notification::after{position:absolute;top:4px;right:4px;width:4px;height:4px;border:1px solid #fff;border-radius:50%;background:#e3c94d;content:""}.premium-content{padding:18px 20px}.premium-intro{display:flex;align-items:center;justify-content:space-between;margin-bottom:13px}.premium-intro h4{margin:0 0 3px;font-size:14px;font-weight:680;letter-spacing:-.035em}.premium-intro p{margin:0;color:#929990;font-size:6px}.premium-intro>button{padding:8px 11px;border:0;border-radius:8px;background:#111;color:#fff;font-size:6px;font-weight:750;box-shadow:0 6px 14px rgba(13,13,13,.13)}.premium-grid{display:grid;grid-template-columns:1.6fr .75fr;gap:10px}.delivery-panel,.security-panel{border:1px solid #e5eae2;border-radius:12px;background:#fff;box-shadow:0 9px 24px rgba(39,49,34,.045)}.delivery-panel{padding:12px 13px 4px}.panel-heading{display:flex;align-items:flex-start;justify-content:space-between}.panel-heading>span{display:flex;flex-direction:column}.panel-heading small{color:#989f96;font-size:5px;font-weight:800;letter-spacing:.11em}.panel-heading strong{margin-top:3px;font-size:19px;font-weight:530;letter-spacing:-.05em}.panel-heading>b{padding:4px 6px;border-radius:999px;background:#eef7e5;color:#759d52;font-size:5px}.premium-chart{height:76px;margin-top:-4px}.premium-chart .area{fill:url(#premiumArea)}.premium-chart circle{fill:#f3ee9a;stroke:#111;stroke-width:2}.security-panel{display:flex;align-items:center;flex-direction:column;padding:12px 8px;text-align:center}.security-ring{display:grid;width:62px;height:62px;place-items:center;margin-bottom:7px;border-radius:50%;background:conic-gradient(var(--green-deep) 0 92%,#edf0eb 92%);box-shadow:inset 0 0 0 7px #fff}.security-ring span{font-size:15px;font-weight:650;letter-spacing:-.05em}.security-ring small{font-size:7px}.security-panel>strong{font-size:7px}.security-panel>small{margin-top:2px;color:#9aa097;font-size:5px}.secure-status{display:flex;align-items:center;gap:4px;margin-top:8px;padding:4px 6px;border-radius:99px;background:#f3f8ee;color:#718266;font-size:5px;font-weight:700}.secure-status i{width:4px;height:4px;border-radius:50%;background:#84b55e}.activity-row{display:flex;align-items:center;justify-content:space-between;margin-top:9px;padding:8px 10px;border:1px solid #e5eae2;border-radius:10px;background:#fff}.activity-row>div{display:flex;align-items:center;gap:8px}.activity-icon{display:grid;width:25px;height:25px;place-items:center;border-radius:7px;background:var(--yellow);font-size:9px}.activity-row>div>span:last-child{display:flex;flex-direction:column}.activity-row strong{font-size:6px}.activity-row small{margin-top:2px;color:#9aa097;font-size:5px}.activity-row>b{padding:4px 7px;border-radius:99px;background:#edf7e5;color:#70934f;font-size:5px}
@media(max-width:650px){.premium-top{height:43px}.premium-content{padding:10px}.premium-intro{margin-bottom:8px}.premium-intro h4{font-size:10px}.premium-intro p{font-size:5px}.premium-intro>button{padding:6px 8px}.premium-grid{grid-template-columns:1.55fr .8fr;gap:6px}.delivery-panel{padding:8px 8px 2px}.panel-heading strong{font-size:14px}.premium-chart{height:53px}.security-panel{padding:8px 4px}.security-ring{width:44px;height:44px;box-shadow:inset 0 0 0 5px #fff}.security-ring span{font-size:11px}.secure-status{margin-top:4px}.activity-row{margin-top:5px;padding:5px 7px}.activity-icon{width:19px;height:19px}.premium-actions button{width:22px;height:22px}.premium-title span{font-size:8px}}
@media(prefers-reduced-motion:reduce){.overview__header,.laptop,.profile,.trust-card,.value-card{opacity:1!important;animation:none!important}.overview__header,.profile,.value-card{transform:none!important}.laptop{transform:translateX(-50%)!important}.trust-card{transform:none!important}.route path,.mail-chart .line{stroke-dashoffset:0!important;animation:none!important}}
</style>
