<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const visible = ref(false)
let observer

const partners = ['Northstar', 'Vertex', 'Momentum', 'Orbit', 'Luma', 'Nexus']
const messages = [
  ['AM', 'Alex Morgan', 'Q4 project proposal', 'Now'],
  ['SK', 'Sarah Kim', 'Design review notes', '10:24'],
  ['JD', 'James Dean', 'Invoice #2048', '09:45']
]

onMounted(() => {
  if (!('IntersectionObserver' in window)) return (visible.value = true)
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      visible.value = true
      observer.disconnect()
    }
  }, { threshold: 0.12 })
  if (root.value) observer.observe(root.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section ref="root" class="trusted-email" :class="{ show: visible }" aria-labelledby="trusted-title">
    <div class="glow glow--aqua" /><div class="glow glow--blue" />
    <div class="inner">
      <header class="heading">
        <span class="eyebrow"><i /> Trusted business email</span>
        <h2 id="trusted-title">Professional communication.<br><mark>Protected by design.</mark></h2>
        <p>Give every employee a polished business inbox with secure delivery, simple administration and reliable access on every device.</p>
      </header>

      <div class="marquee" aria-label="Companies using Smardove">
        <div class="marquee__track">
          <div v-for="copy in 2" :key="copy" class="marquee__group" :aria-hidden="copy === 2">
            <span v-for="(partner, index) in partners" :key="partner"><i :class="`brand brand--${index % 4}`"><b/><b/><b/><b/></i>{{ partner }}</span>
          </div>
        </div>
      </div>

      <div class="grid">
        <article class="workspace">
          <div class="workspace__copy">
            <span class="label">Smardove workspace</span>
            <h3>One calm place for every business conversation.</h3>
            <p>Manage mailboxes, conversations and delivery health without complicated tools or distracting interfaces.</p>
            <a href="https://smardove.com/features/">Explore features <i>↗</i></a>
            <div class="proof"><span>✓ SSL protected</span><span>✓ Any device</span></div>
          </div>

          <div class="mail-window">
            <header><span class="dots"><i/><i/><i/></span><small>mail.smardove.com</small><b>NA</b></header>
            <div class="mail-layout">
              <aside><strong>S</strong><i class="active"/><i/><i/><i/><span/></aside>
              <main>
                <div class="inbox-top"><span><small>WORKSPACE</small><h4>Good morning, Naduni</h4></span><button>Compose <b>＋</b></button></div>
                <div class="stats"><div><small>Delivered today</small><strong>12,482</strong><em>↑ 18.4%</em></div><div><small>Protected</small><strong>99.98%</strong><em>Healthy</em></div></div>
                <div class="inbox-label"><strong>Priority inbox</strong><span>View all</span></div>
                <div class="messages">
                  <div v-for="(message, index) in messages" :key="message[1]">
                    <i :class="`avatar avatar--${index}`">{{ message[0] }}</i>
                    <span><b>{{ message[1] }}</b><small>{{ message[2] }}</small></span>
                    <em>Delivered</em><time>{{ message[3] }}</time>
                  </div>
                </div>
              </main>
            </div>
            <div class="toast"><i>✉</i><span><b>Message delivered</b><small>Protected by Smardove</small></span><strong>✓</strong></div>
          </div>
        </article>

        <article class="security">
          <header><span class="label label--dark">Always protected</span><span class="live"><i/> Live</span></header>
          <h3>Security that works quietly in the background.</h3>
          <p>Every incoming message is checked before it reaches your team.</p>
          <div class="orbit">
            <i class="ring ring--one"/><i class="ring ring--two"/>
            <div class="shield"><svg viewBox="0 0 64 72"><path d="M32 4 56 14v19c0 17-10 28-24 35C18 61 8 50 8 33V14L32 4Z"/><path d="m22 35 7 7 14-16"/></svg></div>
            <span class="chip chip--one">Spam blocked</span><span class="chip chip--two">Malware scanned</span>
          </div>
          <div class="security-stats"><div><b>99.9%</b><span>Uptime</span></div><div><b>24/7</b><span>Protection</span></div><div><b>&lt;1s</b><span>Mail scan</span></div></div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.trusted-email,.trusted-email *{box-sizing:border-box}.trusted-email{--ink:#0d0d0d;--muted:#737985;--aqua:#00e0ab;--teal:#00cab6;--blue:#4476e6;--indigo:#4864f0;--soft:#7ce6d2;--peri:#aabff2;position:relative;isolation:isolate;overflow:hidden;padding:clamp(78px,8vw,128px) clamp(16px,4vw,58px);background:#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.inner{width:min(1450px,100%);margin:auto}.glow{position:absolute;z-index:-1;width:430px;height:430px;border-radius:50%;filter:blur(120px);opacity:.16}.glow--aqua{top:5%;left:-230px;background:var(--aqua)}.glow--blue{right:-250px;bottom:0;background:var(--blue)}
.heading{max-width:880px;margin:auto;text-align:center;opacity:0;transform:translateY(22px)}.show .heading{animation:rise .72s forwards}.eyebrow{display:inline-flex;align-items:center;gap:9px;margin-bottom:18px;padding:8px 13px;border:1px solid #e6eaf0;border-radius:99px;color:#59616c;font-size:10px;font-weight:750;letter-spacing:.09em;text-transform:uppercase}.eyebrow i{width:8px;height:8px;border-radius:50%;background:linear-gradient(135deg,var(--aqua),var(--teal));box-shadow:0 0 0 4px rgba(0,224,171,.12)}.heading h2{margin:0;font-family:var(--font-display,var(--font-sans));font-size:clamp(38px,5vw,70px);font-weight:390;line-height:1.04;letter-spacing:-.05em}.heading mark{padding:0 .04em;background:linear-gradient(transparent 68%,rgba(124,230,210,.72) 68%);color:inherit}.heading p{max-width:670px;margin:21px auto 0;color:var(--muted);font-size:clamp(12px,1vw,15px);line-height:1.7}
.marquee{width:min(1180px,100%);margin:clamp(40px,5vw,66px) auto clamp(38px,5vw,64px);overflow:hidden;opacity:0;mask-image:linear-gradient(90deg,transparent,#000 9%,#000 91%,transparent)}.show .marquee{animation:fade .7s .18s forwards}.marquee__track{display:flex;width:max-content;animation:marquee 28s linear infinite}.marquee:hover .marquee__track{animation-play-state:paused}.marquee__group{display:flex;flex-shrink:0}.marquee__group>span{display:flex;min-width:190px;align-items:center;justify-content:center;gap:10px;color:#9ba2ac;font-size:14px;font-weight:700}.brand{display:grid;width:28px;height:28px;place-items:center;border:2px solid #cbd1da;border-radius:9px}.brand--0{transform:rotate(45deg)}.brand--0:after{width:8px;height:8px;border-radius:2px;background:var(--soft);content:""}.brand--1{border-style:dashed;border-radius:50%}.brand--1:after{width:9px;height:9px;border-radius:50%;background:var(--peri);content:""}.brand--2{border-radius:50%}.brand--2:after{color:var(--blue);content:"↯"}.brand--3{grid-template-columns:1fr 1fr;padding:5px;border-radius:50%}.brand--3 b{width:4px;height:4px;border-radius:50%;background:#aab2be}
.grid{display:grid;grid-template-columns:minmax(0,1.65fr) minmax(310px,.75fr);gap:24px}.workspace,.security{border-radius:clamp(22px,2vw,30px);opacity:0;transform:translateY(28px)}.show .workspace{animation:rise .78s .28s forwards}.show .security{animation:rise .78s .42s forwards}.workspace{position:relative;display:grid;min-height:610px;grid-template-columns:.72fr 1.28fr;overflow:hidden;border:1px solid #dfe5ed;background:linear-gradient(145deg,#f9fbfd,#f4f8fa);box-shadow:0 28px 80px -52px rgba(30,50,72,.3)}.workspace:before{position:absolute;right:-12%;bottom:-31%;width:68%;aspect-ratio:1;border-radius:50%;background:linear-gradient(135deg,rgba(0,224,171,.2),rgba(68,118,230,.17));content:""}.workspace__copy{z-index:2;display:flex;justify-content:center;flex-direction:column;padding:clamp(34px,4vw,64px)}.label{width:max-content;padding:8px 12px;border:1px solid rgba(0,202,182,.22);border-radius:99px;background:rgba(124,230,210,.2);color:#087665;font-size:9px;font-weight:800;letter-spacing:.09em;text-transform:uppercase}.workspace h3,.security h3{margin:24px 0 15px;font-size:clamp(28px,3vw,47px);font-weight:430;line-height:1.06;letter-spacing:-.045em}.workspace p,.security>p{margin:0;color:var(--muted);font-size:clamp(11px,.9vw,14px);line-height:1.7}.workspace__copy>a{display:flex;width:max-content;align-items:center;gap:22px;margin-top:27px;padding:8px 9px 8px 19px;border-radius:99px;background:var(--ink);color:#fff;font-size:11px;font-weight:700;text-decoration:none}.workspace__copy>a i{display:grid;width:31px;height:31px;place-items:center;border-radius:50%;background:linear-gradient(135deg,var(--blue),var(--indigo));font-style:normal}.proof{display:flex;gap:17px;margin-top:31px;color:#606873;font-size:9px}
.mail-window{position:absolute;top:12%;right:-7%;width:64%;height:76%;border:1px solid #fff;border-radius:19px;background:#fff;box-shadow:0 34px 65px -30px rgba(35,51,76,.28);transform:perspective(1200px) rotateY(-4deg)}.mail-window>header{display:flex;height:48px;align-items:center;padding:0 15px;border-bottom:1px solid #edf0f4}.dots{display:flex;gap:5px}.dots i{width:6px;height:6px;border-radius:50%;background:#dde2e8}.dots i:nth-child(2){background:var(--soft)}.dots i:nth-child(3){background:var(--peri)}.mail-window>header small{margin:auto;color:#a1a8b1;font-size:7px}.mail-window>header>b{display:grid;width:26px;height:26px;place-items:center;border-radius:50%;background:#111;color:#fff;font-size:6px}.mail-layout{display:grid;height:calc(100% - 48px);grid-template-columns:54px 1fr}.mail-layout aside{display:flex;align-items:center;flex-direction:column;gap:20px;padding:17px 0;border-radius:0 0 0 19px;background:#111318}.mail-layout aside strong{display:grid;width:29px;height:29px;place-items:center;border-radius:9px;background:linear-gradient(135deg,var(--aqua),var(--teal));font-size:10px}.mail-layout aside i{width:17px;height:5px;border-radius:9px;background:#383c45}.mail-layout aside i.active{height:17px;background:var(--blue)}.mail-layout aside span{width:23px;height:23px;margin-top:auto;border-radius:50%;background:#fff}.mail-layout main{padding:24px;overflow:hidden}.inbox-top{display:flex;align-items:center;justify-content:space-between}.inbox-top small{color:#a0a7b0;font-size:6px}.inbox-top h4{margin:5px 0;font-size:16px}.inbox-top button{display:flex;align-items:center;gap:6px;padding:6px 7px 6px 10px;border:0;border-radius:99px;background:#111;color:#fff;font-size:7px}.inbox-top button b{display:grid;width:20px;height:20px;place-items:center;border-radius:50%;background:var(--blue)}.stats{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin:22px 0}.stats>div{display:grid;grid-template-columns:1fr auto;gap:5px;padding:12px;border:1px solid #edf0f4;border-radius:12px}.stats small{grid-column:1/-1;color:#939ba6;font-size:6px}.stats strong{font-size:21px}.stats em{align-self:end;color:#078471;font-size:6px;font-style:normal}.inbox-label{display:flex;justify-content:space-between;padding-bottom:9px;border-bottom:1px solid #edf0f4;font-size:8px}.inbox-label span{color:var(--blue);font-size:6px}.messages>div{display:grid;grid-template-columns:30px 1fr auto auto;align-items:center;gap:8px;padding:11px 0;border-bottom:1px solid #edf0f4}.avatar{display:grid;width:28px;height:28px;place-items:center;border-radius:50%;background:rgba(124,230,210,.5);font-style:normal;font-size:6px}.avatar--1{background:rgba(170,191,242,.6)}.avatar--2{background:#edf0f4}.messages span{display:flex;flex-direction:column}.messages b{font-size:7px}.messages small,.messages time{color:#9299a3;font-size:6px}.messages em{color:#078471;font-size:6px;font-style:normal}.toast{position:absolute;right:7%;bottom:-24px;display:flex;min-width:220px;align-items:center;gap:10px;padding:12px;border:1px solid #e8ecf1;border-radius:14px;background:#fff;box-shadow:0 20px 45px -24px #19273b}.toast>i{display:grid;width:34px;height:34px;place-items:center;border-radius:10px;background:rgba(0,224,171,.2);font-style:normal}.toast span{display:flex;flex:1;flex-direction:column}.toast b{font-size:7px}.toast small{color:#9299a3;font-size:6px}.toast>strong{color:#087665}
.security{position:relative;overflow:hidden;padding:clamp(30px,3vw,44px);background:linear-gradient(155deg,#171a21,#0d0f14);color:#fff}.security:before{position:absolute;top:-28%;right:-35%;width:100%;aspect-ratio:1;border-radius:50%;background:radial-gradient(circle,rgba(68,118,230,.38),transparent 67%);content:""}.security>header{position:relative;z-index:2;display:flex;justify-content:space-between}.label--dark{border-color:rgba(124,230,210,.23);background:rgba(0,224,171,.11);color:var(--soft)}.live{display:flex;align-items:center;gap:6px;color:#b7bec8;font-size:8px}.live i{width:7px;height:7px;border-radius:50%;background:var(--aqua)}.security h3{position:relative;z-index:2;font-size:clamp(27px,2.5vw,39px)}.security>p{position:relative;z-index:2;color:#a9b0bb}.orbit{position:relative;height:260px;margin:23px 0}.ring{position:absolute;top:50%;left:50%;border:1px solid rgba(170,191,242,.2);border-radius:50%;transform:translate(-50%,-50%)}.ring--one{width:190px;height:190px}.ring--two{width:255px;height:255px;border-style:dashed}.shield{position:absolute;z-index:3;top:50%;left:50%;display:grid;width:96px;height:96px;place-items:center;border-radius:28px;background:linear-gradient(135deg,var(--aqua),var(--blue));box-shadow:0 24px 50px -18px var(--blue);transform:translate(-50%,-50%) rotate(-5deg)}.shield svg{width:48px;fill:none;stroke:#fff;stroke-width:3;stroke-linecap:round;stroke-linejoin:round}.chip{position:absolute;z-index:4;padding:9px 12px;border:1px solid rgba(255,255,255,.12);border-radius:99px;background:rgba(31,35,44,.86);color:#d9dee6;font-size:7px}.chip--one{top:22%;left:0}.chip--two{right:-2%;bottom:22%}.security-stats{display:grid;grid-template-columns:repeat(3,1fr);padding-top:24px;border-top:1px solid rgba(255,255,255,.1)}.security-stats div{display:flex;align-items:center;flex-direction:column;border-right:1px solid rgba(255,255,255,.1)}.security-stats div:last-child{border:0}.security-stats b{font-size:23px}.security-stats span{color:#8f97a4;font-size:7px}
@keyframes rise{to{opacity:1;transform:translateY(0)}}@keyframes fade{to{opacity:1}}@keyframes marquee{from{transform:translateX(-50%)}to{transform:translateX(0)}}@media(max-width:1050px){.grid{grid-template-columns:1fr}.security{min-height:570px}.chip--one{left:18%}.chip--two{right:17%}}@media(max-width:760px){.trusted-email{padding-inline:14px}.workspace{display:block;min-height:auto;padding-bottom:38px}.workspace__copy{padding:35px 25px}.mail-window{position:relative;top:auto;right:auto;width:calc(100% - 30px);height:440px;margin:0 15px;transform:none}.partner{min-width:165px}.marquee__track{animation-duration:21s}}@media(max-width:480px){.heading h2 br{display:none}.mail-window{height:410px}.stats{grid-template-columns:1fr}.stats>div:nth-child(2){display:none}.messages>div{grid-template-columns:28px 1fr auto}.messages em{display:none}.chip--one{left:1%}.chip--two{right:0}}@media(prefers-reduced-motion:reduce){.heading,.marquee,.workspace,.security{opacity:1!important;transform:none!important;animation:none!important}.marquee{overflow-x:auto;mask-image:none}.marquee__track{animation:none}.marquee__group:nth-child(2){display:none}}
</style>
