<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const section = ref(null)
const active = ref(false)
let observer

const benefits = [
  { icon: 'shield', title: 'Protected by default', text: 'Spam, malware and suspicious links are checked automatically.' },
  { icon: 'bolt', title: 'Fast everywhere', text: 'Reliable email access from desktop, browser and mobile.' },
  { icon: 'team', title: 'Simple team control', text: 'Create accounts, manage storage and apply policies in minutes.' }
]

const messages = [
  { initials: 'AM', name: 'Alex Morgan', subject: 'Project proposal approved', time: 'Now', tone: 'aqua' },
  { initials: 'SK', name: 'Sarah Kim', subject: 'Updated meeting notes', time: '10:24', tone: 'blue' },
  { initials: 'JD', name: 'James Dean', subject: 'Invoice #2048 received', time: '09:45', tone: 'grey' }
]

onMounted(() => {
  if (!('IntersectionObserver' in window)) return (active.value = true)
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      active.value = true
      observer.disconnect()
    }
  }, { threshold: 0.15 })
  if (section.value) observer.observe(section.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section ref="section" class="email-suite" :class="{ active }" aria-labelledby="suite-title">
    <div class="email-suite__inner">
      <div class="intro">
        <div class="intro__copy">
          <span class="pill"><i /> Smardove business email</span>
          <h2 id="suite-title">A smarter inbox for<br><mark>serious business.</mark></h2>
        </div>
        <div class="intro__aside">
          <p>Professional mailboxes, powerful security and effortless administration—designed to keep every team connected.</p>
          <a href="https://smardove.com/pricing/">Explore email plans <span>↗</span></a>
        </div>
      </div>

      <div class="suite-panel">
        <aside class="benefit-rail">
          <div class="rail-head"><span>Why Smardove</span><b>01—03</b></div>
          <article v-for="(benefit, index) in benefits" :key="benefit.title" :style="{ '--delay': `${.25 + index * .12}s` }">
            <div class="benefit-icon">
              <svg v-if="benefit.icon === 'shield'" viewBox="0 0 24 24"><path d="M12 3 20 6v6c0 5-3 8-8 10-5-2-8-5-8-10V6l8-3Z"/><path d="m8.5 12 2.2 2.2 4.8-5"/></svg>
              <svg v-else-if="benefit.icon === 'bolt'" viewBox="0 0 24 24"><path d="m13 2-8 12h6l-1 8 9-13h-6V2Z"/></svg>
              <svg v-else viewBox="0 0 24 24"><circle cx="9" cy="8" r="3"/><circle cx="17" cy="10" r="2.5"/><path d="M3.5 20c0-4 2-6 5.5-6s5.5 2 5.5 6M14 15c3.8-.8 6 1.2 6.5 4.5"/></svg>
            </div>
            <div><span>0{{ index + 1 }}</span><h3>{{ benefit.title }}</h3><p>{{ benefit.text }}</p></div>
          </article>
        </aside>

        <div class="product-stage">
          <div class="stage-glow" />
          <div class="browser">
            <header class="browser__bar">
              <span class="traffic"><i/><i/><i/></span>
              <div class="address"><i>⌕</i> mail.smardove.com</div>
              <b>NA</b>
            </header>
            <div class="app">
              <nav class="app-nav">
                <strong>S</strong><button class="selected">⌂</button><button>✉</button><button>⌁</button><button>⚙</button><i/>
              </nav>
              <main class="inbox">
                <header class="inbox__head"><div><small>OVERVIEW</small><h3>Welcome back, Naduni</h3></div><button>Compose <i>＋</i></button></header>
                <div class="insights">
                  <div class="insight"><span>Delivery health</span><strong>99.98%</strong><em>↑ 18.4%</em></div>
                  <div class="mini-chart" aria-hidden="true"><i/><i/><i/><i/><i/><i/><i/></div>
                </div>
                <div class="message-title"><b>Priority messages</b><span>View all</span></div>
                <div class="message" v-for="message in messages" :key="message.name">
                  <i :class="`avatar avatar--${message.tone}`">{{ message.initials }}</i>
                  <span><b>{{ message.name }}</b><small>{{ message.subject }}</small></span>
                  <em>Protected</em><time>{{ message.time }}</time>
                </div>
              </main>
            </div>
          </div>

          <div class="status-card status-card--top"><i>✓</i><span><b>All systems secure</b><small>Scanning every message</small></span></div>
          <div class="status-card status-card--bottom"><i>✉</i><span><b>Message delivered</b><small>London → Singapore</small></span><strong>0.8s</strong></div>
        </div>
      </div>

      <footer class="proof-bar">
        <span><b>99.9%</b> guaranteed uptime</span><i/><span><b>25 GB</b> mailbox storage</span><i/><span><b>24/7</b> threat protection</span><i/><span><b>Any OS</b> and email client</span>
      </footer>
    </div>
  </section>
</template>

<style scoped>
.email-suite,.email-suite *{box-sizing:border-box}.email-suite{--ink:#0d0d0d;--charcoal:#20242b;--muted:#737985;--aqua:#00e0ab;--teal:#00cab6;--blue:#4476e6;--indigo:#4864f0;--soft:#7ce6d2;--peri:#aabff2;--ice:#f7f9fc;--line:#e6eaf0;width:100%;overflow:hidden;padding:clamp(76px,8vw,128px) clamp(16px,4vw,60px);background:linear-gradient(180deg,#fff 0,#fff 45%,#f7f9fc 100%);color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.email-suite__inner{width:min(1450px,100%);margin:auto}.intro{display:grid;grid-template-columns:1.2fr .8fr;align-items:end;gap:60px;margin-bottom:clamp(45px,6vw,82px)}.intro__copy,.intro__aside{opacity:0;transform:translateY(20px)}.active .intro__copy{animation:rise .7s forwards}.active .intro__aside{animation:rise .7s .12s forwards}.pill{display:inline-flex;align-items:center;gap:9px;margin-bottom:21px;padding:8px 13px;border:1px solid var(--line);border-radius:99px;color:#5f6773;font-size:10px;font-weight:750;letter-spacing:.08em;text-transform:uppercase}.pill i{width:8px;height:8px;border-radius:50%;background:linear-gradient(135deg,var(--aqua),var(--teal));box-shadow:0 0 0 4px rgba(0,224,171,.12)}h2{margin:0;font-family:var(--font-display,var(--font-sans));font-size:clamp(42px,5.5vw,78px);font-weight:380;line-height:1.02;letter-spacing:-.055em}h2 mark{padding:0 .04em;background:linear-gradient(transparent 69%,rgba(124,230,210,.72) 69%);color:inherit}.intro__aside{padding-bottom:4px}.intro__aside p{max-width:520px;margin:0 0 24px;color:var(--muted);font-size:clamp(12px,1vw,15px);line-height:1.75}.intro__aside a{display:inline-flex;align-items:center;gap:18px;color:var(--ink);font-size:12px;font-weight:750;text-decoration:none}.intro__aside a span{display:grid;width:34px;height:34px;place-items:center;border-radius:50%;background:linear-gradient(135deg,var(--blue),var(--indigo));color:#fff;transition:transform .25s}.intro__aside a:hover span{transform:rotate(45deg)}
.suite-panel{display:grid;grid-template-columns:minmax(300px,.68fr) minmax(600px,1.32fr);min-height:670px;overflow:hidden;border:1px solid #dfe5ed;border-radius:clamp(24px,2.5vw,36px);background:#fff;box-shadow:0 35px 100px -65px rgba(28,45,78,.42);opacity:0;transform:translateY(30px)}.active .suite-panel{animation:rise .85s .2s forwards}.benefit-rail{display:flex;flex-direction:column;padding:clamp(28px,3.5vw,52px);border-right:1px solid var(--line);background:#fff}.rail-head{display:flex;justify-content:space-between;margin-bottom:auto;color:#9299a4;font-size:9px;font-weight:750;letter-spacing:.1em;text-transform:uppercase}.benefit-rail article{display:grid;grid-template-columns:50px 1fr;gap:17px;padding:25px 0;border-bottom:1px solid var(--line);opacity:0;transform:translateX(-16px)}.active .benefit-rail article{animation:slide .6s var(--delay) forwards}.benefit-icon{display:grid;width:48px;height:48px;place-items:center;border:1px solid #e2e7ed;border-radius:14px;background:var(--ice)}.benefit-icon svg{width:23px;fill:none;stroke:var(--charcoal);stroke-width:1.6;stroke-linecap:round;stroke-linejoin:round}.benefit-rail article:nth-of-type(2) .benefit-icon{background:rgba(124,230,210,.24)}.benefit-rail article:nth-of-type(3) .benefit-icon{background:rgba(170,191,242,.25)}.benefit-rail article>div>span{color:#a0a7b1;font-size:8px}.benefit-rail h3{margin:6px 0 8px;font-size:clamp(15px,1.25vw,19px);font-weight:650;letter-spacing:-.025em}.benefit-rail p{margin:0;color:var(--muted);font-size:10px;line-height:1.55}
.product-stage{position:relative;display:grid;min-width:0;place-items:center;overflow:hidden;background:radial-gradient(circle at 72% 25%,rgba(170,191,242,.26),transparent 29%),radial-gradient(circle at 22% 78%,rgba(124,230,210,.28),transparent 31%),linear-gradient(145deg,#f8fafc,#f4f8fa)}.product-stage:before{position:absolute;inset:0;background-image:linear-gradient(rgba(32,36,43,.035) 1px,transparent 1px),linear-gradient(90deg,rgba(32,36,43,.035) 1px,transparent 1px);background-size:42px 42px;content:""}.stage-glow{position:absolute;width:65%;aspect-ratio:1;border-radius:50%;background:linear-gradient(135deg,rgba(0,224,171,.25),rgba(68,118,230,.22));filter:blur(18px)}.browser{position:relative;z-index:2;width:78%;height:72%;overflow:hidden;border:1px solid rgba(255,255,255,.95);border-radius:19px;background:#fff;box-shadow:0 38px 75px -33px rgba(31,50,82,.38);transform:perspective(1300px) rotateY(-3deg) rotateX(1deg)}.browser__bar{display:flex;height:46px;align-items:center;padding:0 14px;border-bottom:1px solid #edf0f4}.traffic{display:flex;gap:5px}.traffic i{width:6px;height:6px;border-radius:50%;background:#dce1e7}.traffic i:nth-child(2){background:var(--soft)}.traffic i:nth-child(3){background:var(--peri)}.address{margin:auto;padding:7px 30px;border-radius:99px;background:#f5f7f9;color:#9aa2ad;font-size:6px}.browser__bar>b{display:grid;width:25px;height:25px;place-items:center;border-radius:50%;background:#111;color:#fff;font-size:6px}.app{display:grid;height:calc(100% - 46px);grid-template-columns:51px 1fr}.app-nav{display:flex;align-items:center;flex-direction:column;gap:15px;padding:15px 0;background:#111318}.app-nav strong{display:grid;width:27px;height:27px;place-items:center;margin-bottom:6px;border-radius:8px;background:linear-gradient(135deg,var(--aqua),var(--teal));font-size:9px}.app-nav button{width:27px;height:27px;border:0;border-radius:8px;background:transparent;color:#777f8d;font-size:11px}.app-nav button.selected{background:var(--blue);color:#fff}.app-nav i{width:22px;height:22px;margin-top:auto;border-radius:50%;background:#fff}.inbox{padding:clamp(18px,2.2vw,31px);overflow:hidden}.inbox__head{display:flex;align-items:center;justify-content:space-between}.inbox__head small{color:#9ba3ae;font-size:6px;letter-spacing:.12em}.inbox__head h3{margin:5px 0 0;font-size:clamp(14px,1.45vw,21px);font-weight:600}.inbox__head button{display:flex;align-items:center;gap:6px;padding:5px 6px 5px 10px;border:0;border-radius:99px;background:#111;color:#fff;font-size:7px}.inbox__head button i{display:grid;width:20px;height:20px;place-items:center;border-radius:50%;background:var(--blue);font-style:normal}.insights{display:grid;grid-template-columns:.7fr 1.3fr;gap:12px;margin:23px 0;padding:15px;border:1px solid #edf0f4;border-radius:14px}.insight{display:flex;flex-direction:column}.insight span{color:#8e97a3;font-size:6px}.insight strong{margin:7px 0 3px;font-size:clamp(19px,2vw,29px);font-weight:560}.insight em{color:#078471;font-size:6px;font-style:normal}.mini-chart{display:flex;align-items:flex-end;gap:6px}.mini-chart i{width:11%;border-radius:4px 4px 1px 1px;background:#dfe4ea;animation:bars 3s ease-in-out infinite}.mini-chart i:nth-child(1){height:27%}.mini-chart i:nth-child(2){height:48%;background:var(--soft)}.mini-chart i:nth-child(3){height:38%}.mini-chart i:nth-child(4){height:72%;background:var(--blue)}.mini-chart i:nth-child(5){height:58%}.mini-chart i:nth-child(6){height:86%;background:var(--aqua)}.mini-chart i:nth-child(7){height:70%;background:var(--peri)}.message-title{display:flex;justify-content:space-between;padding-bottom:10px;border-bottom:1px solid #edf0f4;font-size:8px}.message-title span{color:var(--blue);font-size:6px}.message{display:grid;grid-template-columns:30px 1fr auto auto;align-items:center;gap:8px;padding:11px 0;border-bottom:1px solid #edf0f4}.avatar{display:grid;width:28px;height:28px;place-items:center;border-radius:50%;font-style:normal;font-size:6px;font-weight:750}.avatar--aqua{background:rgba(124,230,210,.48)}.avatar--blue{background:rgba(170,191,242,.55)}.avatar--grey{background:#eef1f4}.message>span{display:flex;flex-direction:column;gap:2px}.message b{font-size:7px}.message small,.message time{color:#969da7;font-size:6px}.message em{color:#078471;font-size:6px;font-style:normal}
.status-card{position:absolute;z-index:4;display:flex;align-items:center;gap:10px;padding:12px 14px;border:1px solid rgba(255,255,255,.9);border-radius:14px;background:rgba(255,255,255,.9);box-shadow:0 20px 45px -22px rgba(30,49,77,.35);backdrop-filter:blur(12px);animation:float 4s ease-in-out infinite}.status-card>i{display:grid;width:33px;height:33px;place-items:center;border-radius:10px;background:rgba(0,224,171,.2);color:#087665;font-style:normal}.status-card span{display:flex;flex-direction:column}.status-card b{font-size:7px}.status-card small{color:#949ca7;font-size:6px}.status-card>strong{margin-left:14px;color:var(--blue);font-size:8px}.status-card--top{top:9%;right:4%}.status-card--bottom{bottom:8%;left:4%;animation-delay:-1.8s}.proof-bar{display:flex;align-items:center;justify-content:space-between;gap:20px;padding:28px clamp(10px,2vw,28px) 0;color:#737b87;font-size:10px;opacity:0}.active .proof-bar{animation:fade .7s .65s forwards}.proof-bar b{margin-right:4px;color:#222831;font-size:13px}.proof-bar i{width:1px;height:22px;background:#dfe4ea}
@keyframes rise{to{opacity:1;transform:translateY(0)}}@keyframes slide{to{opacity:1;transform:translateX(0)}}@keyframes fade{to{opacity:1}}@keyframes bars{50%{transform:scaleY(.9);transform-origin:bottom}}@keyframes float{50%{transform:translateY(-7px)}}
@media(max-width:1050px){.suite-panel{grid-template-columns:1fr;min-height:auto}.benefit-rail{display:grid;grid-template-columns:repeat(3,1fr);gap:18px;border-right:0;border-bottom:1px solid var(--line)}.rail-head{grid-column:1/-1}.benefit-rail article{grid-template-columns:45px 1fr}.product-stage{min-height:620px}.browser{height:74%}}
@media(max-width:720px){.email-suite{padding-inline:14px}.intro{grid-template-columns:1fr;gap:25px}.intro h2 br{display:none}.benefit-rail{grid-template-columns:1fr}.benefit-rail article{padding:17px 0}.product-stage{min-height:510px}.browser{width:92%;height:74%;transform:none}.status-card--top{top:4%}.status-card--bottom{bottom:3%}.proof-bar{align-items:flex-start;flex-direction:column}.proof-bar i{display:none}}
@media(max-width:480px){.product-stage{min-height:470px}.browser{height:79%}.inbox{padding:16px}.insights{grid-template-columns:1fr}.mini-chart{height:55px}.message{grid-template-columns:28px 1fr auto}.message em{display:none}.status-card{transform:scale(.87)}.status-card--top{right:-5%}.status-card--bottom{left:-5%}}
@media(prefers-reduced-motion:reduce){.intro__copy,.intro__aside,.suite-panel,.benefit-rail article,.proof-bar{opacity:1!important;transform:none!important;animation:none!important}.status-card,.mini-chart i{animation:none!important}}
</style>
