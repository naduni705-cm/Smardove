<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const visible = ref(false)
let observer

const services = [
  { number: '01', title: 'Business Email', text: 'Branded mailboxes for your entire team.', icon: 'mail' },
  { number: '02', title: 'Advanced Security', text: 'Always-on spam and malware protection.', icon: 'shield' },
  { number: '03', title: 'Email Archive', text: 'Secure, searchable long-term storage.', icon: 'archive' }
]

onMounted(() => {
  if (!('IntersectionObserver' in window)) return (visible.value = true)
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      visible.value = true
      observer.disconnect()
    }
  }, { threshold: 0.14 })
  if (root.value) observer.observe(root.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section ref="root" class="email-product" :class="{ visible }" aria-labelledby="product-title">
    <div class="email-product__inner">
      <header class="section-head">
        <div>
          <span class="kicker"><i /> Email infrastructure</span>
          <h2 id="product-title">Everything your team needs<br>to communicate <mark>with confidence.</mark></h2>
        </div>
        <div class="head-aside">
          <p>Professional business email, built-in security and dependable storage in one beautifully simple platform.</p>
          <a href="https://smardove.com/pricing/">Choose your plan <i>↗</i></a>
        </div>
      </header>

      <div class="product-layout">
        <article class="console-card">
          <header class="console-card__head">
            <span><i /> Smardove Console</span>
            <div><b>All systems operational</b><button aria-label="More options">•••</button></div>
          </header>

          <div class="console-card__body">
            <div class="console-copy">
              <span class="index">01 / BUSINESS EMAIL</span>
              <h3>One workspace.<br>Every conversation.</h3>
              <p>Create accounts, protect messages and manage your organization without unnecessary complexity.</p>
              <div class="console-metrics">
                <div><strong>99.9%</strong><span>Uptime</span></div>
                <div><strong>25 GB</strong><span>Storage</span></div>
                <div><strong>24/7</strong><span>Protection</span></div>
              </div>
            </div>

            <div class="dashboard" aria-label="Smardove email admin dashboard">
              <header><span><i/><i/><i/></span><small>admin.smardove.com</small><b>NA</b></header>
              <div class="dashboard__layout">
                <aside><strong>S</strong><i class="on"/><i/><i/><i/><span/></aside>
                <main>
                  <div class="dashboard-title"><span><small>DELIVERY OVERVIEW</small><h4>Mailbox health</h4></span><button>＋ Add account</button></div>
                  <div class="health-row"><div><small>Successful delivery</small><strong>99.98%</strong><em>↑ 18.4%</em></div><div class="bars"><i/><i/><i/><i/><i/><i/></div></div>
                  <div class="accounts-title"><b>Active mailboxes</b><span>View all</span></div>
                  <div class="account"><i>AM</i><span><b>Alex Morgan</b><small>alex@northstar.com</small></span><em>12.4 GB</em><strong>Active</strong></div>
                  <div class="account"><i>SK</i><span><b>Sarah Kim</b><small>sarah@northstar.com</small></span><em>8.1 GB</em><strong>Active</strong></div>
                  <div class="account"><i>JD</i><span><b>James Dean</b><small>james@northstar.com</small></span><em>5.6 GB</em><strong>Active</strong></div>
                </main>
              </div>
            </div>

            <div class="floating-card floating-card--delivery"><i>✉</i><span><b>Delivery protected</b><small>12,482 messages today</small></span><strong>✓</strong></div>
            <div class="floating-card floating-card--security"><i>⌁</i><span><b>No threats detected</b><small>Last scan: just now</small></span></div>
          </div>
        </article>

        <aside class="service-stack">
          <article v-for="(service, index) in services" :key="service.title" :class="{ featured: index === 1 }" :style="{ '--delay': `${.35 + index * .12}s` }">
            <header><span>{{ service.number }}</span><i>↗</i></header>
            <div class="service-icon">
              <svg v-if="service.icon === 'mail'" viewBox="0 0 24 24"><path d="M3 5h18v14H3zM3 6l9 7 9-7"/></svg>
              <svg v-else-if="service.icon === 'shield'" viewBox="0 0 24 24"><path d="M12 3 20 6v6c0 5-3 8-8 10-5-2-8-5-8-10V6l8-3Z"/><path d="m8.5 12 2.2 2.2 4.8-5"/></svg>
              <svg v-else viewBox="0 0 24 24"><path d="M4 7h16v13H4zM2 4h20v4H2zM9 12h6"/></svg>
            </div>
            <div><h3>{{ service.title }}</h3><p>{{ service.text }}</p></div>
          </article>
        </aside>
      </div>

      <footer class="trust-line"><span>Trusted infrastructure for modern teams</span><i/><b>SSL / TLS</b><i/><b>IMAP / POP3</b><i/><b>Mobile ready</b><i/><b>365-day support</b></footer>
    </div>
  </section>
</template>

<style scoped>
.email-product,.email-product *{box-sizing:border-box}.email-product{--ink:#0d0d0d;--charcoal:#20242b;--muted:#737985;--aqua:#00e0ab;--teal:#00cab6;--blue:#4476e6;--indigo:#4864f0;--soft:#7ce6d2;--peri:#aabff2;--ice:#f7f9fc;--line:#e6eaf0;width:100%;overflow:hidden;padding:clamp(76px,8vw,126px) clamp(16px,4vw,60px);background:radial-gradient(circle at 5% 55%,rgba(0,224,171,.07),transparent 23%),#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.email-product__inner{width:min(1500px,100%);margin:auto}.section-head{display:grid;grid-template-columns:1.3fr .7fr;align-items:end;gap:clamp(40px,7vw,110px);margin-bottom:clamp(46px,6vw,82px)}.section-head>div{opacity:0;transform:translateY(20px)}.visible .section-head>div:first-child{animation:rise .7s forwards}.visible .head-aside{animation:rise .7s .12s forwards}.kicker{display:inline-flex;align-items:center;gap:9px;margin-bottom:20px;color:#5c6470;font-size:10px;font-weight:800;letter-spacing:.11em;text-transform:uppercase}.kicker i{width:9px;height:9px;border-radius:50%;background:linear-gradient(135deg,var(--aqua),var(--teal));box-shadow:0 0 0 5px rgba(0,224,171,.1)}h2{margin:0;font-family:var(--font-display,var(--font-sans));font-size:clamp(39px,5vw,72px);font-weight:380;line-height:1.03;letter-spacing:-.052em}h2 mark{padding:0 .04em;background:linear-gradient(transparent 69%,rgba(170,191,242,.72) 69%);color:inherit}.head-aside p{max-width:500px;margin:0 0 24px;color:var(--muted);font-size:clamp(12px,1vw,15px);line-height:1.7}.head-aside a{display:inline-flex;align-items:center;gap:20px;color:var(--ink);font-size:12px;font-weight:750;text-decoration:none}.head-aside a i{display:grid;width:38px;height:38px;place-items:center;border-radius:50%;background:linear-gradient(135deg,var(--blue),var(--indigo));color:#fff;font-style:normal;transition:transform .25s}.head-aside a:hover i{transform:rotate(45deg)}
.product-layout{display:grid;grid-template-columns:minmax(0,1.65fr) minmax(280px,.55fr);gap:20px}.console-card{overflow:hidden;border-radius:clamp(24px,2.4vw,34px);background:linear-gradient(155deg,#171a21,#0c0e13);box-shadow:0 35px 90px -50px rgba(17,29,60,.58);color:#fff;opacity:0;transform:translateY(30px)}.visible .console-card{animation:rise .82s .2s forwards}.console-card__head{display:flex;height:68px;align-items:center;justify-content:space-between;padding:0 clamp(24px,3vw,42px);border-bottom:1px solid rgba(255,255,255,.08);color:#aab1bd;font-size:9px}.console-card__head>span{display:flex;align-items:center;gap:9px;font-weight:750;letter-spacing:.08em;text-transform:uppercase}.console-card__head>span i{width:8px;height:8px;border-radius:50%;background:var(--aqua);box-shadow:0 0 0 5px rgba(0,224,171,.1)}.console-card__head>div{display:flex;align-items:center;gap:18px}.console-card__head>div b{color:#9de6d8;font-size:8px}.console-card__head button{border:0;background:none;color:#89919e}.console-card__body{position:relative;display:grid;min-height:610px;grid-template-columns:.63fr 1.37fr;overflow:hidden}.console-card__body:before{position:absolute;right:-16%;bottom:-45%;width:75%;aspect-ratio:1;border-radius:50%;background:radial-gradient(circle,rgba(68,118,230,.34),transparent 67%);content:""}.console-copy{z-index:2;display:flex;justify-content:center;flex-direction:column;padding:clamp(30px,3.5vw,52px)}.index{color:var(--soft);font-size:8px;font-weight:800;letter-spacing:.12em}.console-copy h3{margin:23px 0 16px;font-size:clamp(30px,3.2vw,48px);font-weight:410;line-height:1.04;letter-spacing:-.045em}.console-copy>p{margin:0;color:#9fa7b3;font-size:11px;line-height:1.65}.console-metrics{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-top:42px}.console-metrics div{display:flex;flex-direction:column;gap:5px}.console-metrics strong{font-size:clamp(16px,1.5vw,22px);font-weight:550}.console-metrics span{color:#78818e;font-size:7px}
.dashboard{position:absolute;z-index:2;right:-7%;bottom:-4%;width:67%;height:79%;overflow:hidden;border:1px solid rgba(255,255,255,.23);border-radius:20px 20px 0 0;background:#fff;box-shadow:0 35px 75px rgba(0,0,0,.35);color:var(--ink);transform:perspective(1200px) rotateY(-5deg)}.dashboard>header{display:flex;height:45px;align-items:center;padding:0 13px;border-bottom:1px solid #edf0f4}.dashboard>header>span{display:flex;gap:5px}.dashboard>header i{width:6px;height:6px;border-radius:50%;background:#dce1e7}.dashboard>header i:nth-child(2){background:var(--soft)}.dashboard>header i:nth-child(3){background:var(--peri)}.dashboard>header small{margin:auto;color:#9ca4ae;font-size:6px}.dashboard>header>b{display:grid;width:25px;height:25px;place-items:center;border-radius:50%;background:#111;color:#fff;font-size:6px}.dashboard__layout{display:grid;height:calc(100% - 45px);grid-template-columns:50px 1fr}.dashboard__layout aside{display:flex;align-items:center;flex-direction:column;gap:17px;padding:14px 0;background:#111318}.dashboard__layout aside strong{display:grid;width:28px;height:28px;place-items:center;border-radius:8px;background:linear-gradient(135deg,var(--aqua),var(--teal));font-size:9px}.dashboard__layout aside i{width:16px;height:5px;border-radius:99px;background:#3c414b}.dashboard__layout aside i.on{height:16px;background:var(--blue)}.dashboard__layout aside span{width:22px;height:22px;margin-top:auto;border-radius:50%;background:#fff}.dashboard__layout main{padding:clamp(17px,2vw,27px)}.dashboard-title{display:flex;align-items:center;justify-content:space-between}.dashboard-title small{color:#9aa2ad;font-size:6px}.dashboard-title h4{margin:4px 0;font-size:clamp(13px,1.3vw,19px)}.dashboard-title button{padding:8px 10px;border:0;border-radius:99px;background:var(--blue);color:#fff;font-size:6px}.health-row{display:grid;grid-template-columns:.7fr 1.3fr;gap:12px;margin:21px 0;padding:13px;border:1px solid #edf0f4;border-radius:13px}.health-row>div:first-child{display:flex;flex-direction:column}.health-row small{color:#929ba6;font-size:6px}.health-row strong{margin:5px 0;font-size:24px}.health-row em{color:#078471;font-size:6px;font-style:normal}.bars{display:flex;align-items:flex-end;gap:6px}.bars i{width:14%;border-radius:4px 4px 0 0;background:#dfe4ea;animation:bar 3s ease-in-out infinite}.bars i:nth-child(1){height:30%}.bars i:nth-child(2){height:50%;background:var(--soft)}.bars i:nth-child(3){height:42%}.bars i:nth-child(4){height:75%;background:var(--blue)}.bars i:nth-child(5){height:62%}.bars i:nth-child(6){height:88%;background:var(--aqua)}.accounts-title{display:flex;justify-content:space-between;padding-bottom:9px;border-bottom:1px solid #edf0f4;font-size:8px}.accounts-title span{color:var(--blue);font-size:6px}.account{display:grid;grid-template-columns:28px 1fr auto auto;align-items:center;gap:8px;padding:10px 0;border-bottom:1px solid #edf0f4}.account>i{display:grid;width:27px;height:27px;place-items:center;border-radius:50%;background:rgba(124,230,210,.45);font-style:normal;font-size:6px}.account:nth-of-type(2)>i{background:rgba(170,191,242,.5)}.account>span{display:flex;flex-direction:column}.account b{font-size:7px}.account small,.account em{color:#929aa5;font-size:6px;font-style:normal}.account>strong{color:#078471;font-size:6px}.floating-card{position:absolute;z-index:5;display:flex;align-items:center;gap:9px;padding:11px 13px;border:1px solid rgba(255,255,255,.16);border-radius:13px;background:rgba(31,35,44,.88);box-shadow:0 20px 40px rgba(0,0,0,.24);backdrop-filter:blur(12px)}.floating-card>i{display:grid;width:31px;height:31px;place-items:center;border-radius:9px;background:rgba(0,224,171,.18);color:var(--soft);font-style:normal}.floating-card span{display:flex;flex-direction:column}.floating-card b{font-size:7px}.floating-card small{color:#8f97a4;font-size:6px}.floating-card>strong{color:var(--aqua)}.floating-card--delivery{top:7%;right:3%}.floating-card--security{right:44%;bottom:7%}
.service-stack{display:grid;grid-template-rows:repeat(3,1fr);gap:14px}.service-stack article{display:grid;grid-template-columns:1fr auto;grid-template-rows:auto 1fr;overflow:hidden;padding:24px;border:1px solid var(--line);border-radius:24px;background:#fff;box-shadow:0 18px 45px -38px rgba(28,45,71,.35);opacity:0;transform:translateX(25px);transition:transform .3s,box-shadow .3s}.visible .service-stack article{animation:slide .65s var(--delay) forwards}.service-stack article:hover{transform:translateX(-5px);box-shadow:0 24px 55px -38px rgba(28,45,71,.48)}.service-stack article.featured{border-color:transparent;background:linear-gradient(145deg,var(--blue),var(--indigo));color:#fff}.service-stack article>header{display:contents}.service-stack header span{color:#9aa2ad;font-size:8px}.service-stack .featured header span{color:rgba(255,255,255,.65)}.service-stack header i{display:grid;width:33px;height:33px;place-items:center;border:1px solid #e4e8ed;border-radius:50%;font-style:normal}.service-stack .featured header i{border-color:rgba(255,255,255,.24)}.service-icon{display:grid;width:50px;height:50px;align-self:end;place-items:center;border-radius:15px;background:rgba(124,230,210,.2)}.featured .service-icon{background:rgba(255,255,255,.13)}.service-icon svg{width:23px;fill:none;stroke:currentColor;stroke-width:1.5;stroke-linecap:round;stroke-linejoin:round}.service-stack article>div:last-child{align-self:end}.service-stack h3{margin:0 0 7px;font-size:clamp(17px,1.5vw,23px);font-weight:600;letter-spacing:-.03em}.service-stack p{margin:0;color:var(--muted);font-size:9px;line-height:1.5}.service-stack .featured p{color:rgba(255,255,255,.68)}.trust-line{display:flex;align-items:center;justify-content:center;gap:clamp(16px,3vw,42px);padding-top:31px;color:#949ba5;font-size:8px;text-transform:uppercase;letter-spacing:.08em;opacity:0}.visible .trust-line{animation:fade .7s .72s forwards}.trust-line b{color:#59616d}.trust-line i{width:4px;height:4px;border-radius:50%;background:var(--aqua)}
@keyframes rise{to{opacity:1;transform:translateY(0)}}@keyframes slide{to{opacity:1;transform:translateX(0)}}@keyframes fade{to{opacity:1}}@keyframes bar{50%{transform:scaleY(.9);transform-origin:bottom}}@media(prefers-reduced-motion:no-preference){.floating-card{animation:float 4s ease-in-out infinite}.floating-card--security{animation-delay:-1.8s}}@keyframes float{50%{translate:0 -7px}}
@media(max-width:1000px){.product-layout{grid-template-columns:1fr}.service-stack{grid-template-columns:repeat(3,1fr);grid-template-rows:none}.service-stack article{min-height:220px}.console-card__body{min-height:620px}}
@media(max-width:720px){.email-product{padding-inline:14px}.section-head{grid-template-columns:1fr;gap:25px}.section-head h2 br{display:none}.console-card__body{display:block;min-height:790px}.console-copy{padding:32px 25px}.dashboard{right:-8%;bottom:0;width:92%;height:53%;transform:none}.floating-card--delivery{top:38%}.floating-card--security{right:auto;bottom:2%;left:2%}.service-stack{grid-template-columns:1fr}.service-stack article{min-height:190px}.trust-line{align-items:flex-start;flex-direction:column;gap:10px}.trust-line i{display:none}}
@media(max-width:470px){.console-metrics{gap:5px}.dashboard{width:97%;height:50%}.floating-card{transform:scale(.88)}.floating-card--delivery{right:-6%}.account{grid-template-columns:28px 1fr auto}.account em{display:none}}
@media(prefers-reduced-motion:reduce){.section-head>div,.console-card,.service-stack article,.trust-line{opacity:1!important;transform:none!important;animation:none!important}.bars i,.floating-card{animation:none!important}}
</style>
