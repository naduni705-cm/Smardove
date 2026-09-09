<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const visible = ref(false)
let observer

const steps = [
  {
    number: '01',
    title: 'Choose your email package',
    text: 'Tell us your team size, storage needs and business goals. We will help you choose the right Smardove package.',
    side: 'right',
    image: 'https://images.unsplash.com/photo-1556761175-b413da4baf72?auto=format&fit=crop&w=900&q=85',
    badge: 'Package selected',
    type: 'form'
  },
  {
    number: '02',
    title: 'Connect your domain',
    text: 'Our specialists securely connect your domain, create mailboxes and configure the policies your organization needs.',
    side: 'left',
    image: 'https://images.unsplash.com/photo-1516321318423-f06f85e504b3?auto=format&fit=crop&w=900&q=85',
    badge: 'Domain verified',
    type: 'domain'
  },
  {
    number: '03',
    title: 'Migrate your email',
    text: 'We move existing messages, contacts and calendars with minimal disruption while keeping your business protected.',
    side: 'right',
    image: 'https://images.unsplash.com/photo-1551434678-e076c223a692?auto=format&fit=crop&w=900&q=85',
    badge: 'Migration complete',
    type: 'migration'
  },
  {
    number: '04',
    title: 'Start working smarter',
    text: 'Your team can immediately use secure email, calendars, contacts, tasks, chat and collaboration from any device.',
    side: 'left',
    image: 'https://images.unsplash.com/photo-1521737711867-e3b97375f902?auto=format&fit=crop&w=900&q=85',
    badge: 'Your team is live',
    type: 'live'
  }
]

onMounted(() => {
  if (!('IntersectionObserver' in window)) return (visible.value = true)
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      visible.value = true
      observer.disconnect()
    }
  }, { threshold: .08 })
  if (root.value) observer.observe(root.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section ref="root" class="how" :class="{ 'is-visible': visible }" aria-labelledby="how-title">
    <div class="how__glow how__glow--aqua" aria-hidden="true" />
    <div class="how__glow how__glow--blue" aria-hidden="true" />

    <div class="how__inner">
      <header class="how__heading">
        <span class="eyebrow"><i /> Simple onboarding</span>
        <h2 id="how-title">How it <mark>works.</mark></h2>
        <p>Launch secure business email in four simple steps—with expert support from start to finish.</p>
      </header>

      <div class="timeline">
        <div class="timeline__line" aria-hidden="true"><i /></div>

        <article
          v-for="(step, index) in steps"
          :key="step.number"
          class="step"
          :class="`step--${step.side}`"
          :style="{ '--delay': `${index * .14}s` }"
        >
          <div class="step__copy">
            <span>{{ step.number }} · GET STARTED</span>
            <h3>{{ step.title }}</h3>
            <p>{{ step.text }}</p>
            <a v-if="index === steps.length - 1" href="https://smardove.com/pricing/">View packages <b>→</b></a>
          </div>

          <div class="step__dot" aria-hidden="true">{{ step.number }}</div>

          <div class="step__visual">
            <img :src="step.image" :alt="step.title" loading="lazy">
            <div class="step__shade" />

            <div v-if="step.type === 'form'" class="mock mock--form">
              <strong>Get started</strong><i/><i/><button>Continue →</button>
            </div>

            <div v-else-if="step.type === 'domain'" class="mock mock--domain">
              <small>YOUR DOMAIN</small><strong>company.com</strong><span><i /> Verified</span>
            </div>

            <div v-else-if="step.type === 'migration'" class="mock mock--migration">
              <span>Old inbox</span><b>→</b><span>Smardove</span>
              <i><strong /></i><small>100% complete</small>
            </div>

            <div v-else class="mock mock--live">
              <strong>All systems operational</strong>
              <div><i>AM</i><i>JD</i><i>SK</i><span>+12</span></div>
            </div>

            <div class="success-badge"><i>✓</i><span>{{ step.badge }}<small>Protected by Smardove</small></span></div>
          </div>
        </article>
      </div>

      <div class="launch-panel">
        <span class="eyebrow"><i /> Built around your business</span>
        <h2>Professional email that fits<br><mark>the way your team works.</mark></h2>
        <div class="launch-panel__copy">
          <p>Smardove combines reliable email delivery, enterprise security, collaboration and simple administration in one connected platform.</p>
          <p>Choose flexible storage, support for your preferred devices and expert migration assistance without unnecessary complexity.</p>
        </div>
        <a href="https://smardove.com/contact/">Talk to an email specialist <b>→</b></a>
      </div>
    </div>
  </section>
</template>

<style scoped>
.how,.how *{box-sizing:border-box}.how{--ink:#0d0d0d;--muted:#737985;--aqua:#00e0ab;--teal:#00cab6;--blue:#4476e6;--indigo:#4864f0;--soft:#7ce6d2;--peri:#aabff2;--ice:#f7f9fc;--line:#e6eaf0;position:relative;isolation:isolate;overflow:hidden;width:100%;padding:clamp(78px,8vw,128px) clamp(16px,4vw,64px);background:#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.how__inner{width:min(1180px,100%);margin:auto}.how__glow{position:absolute;z-index:-1;width:400px;height:400px;border-radius:50%;filter:blur(135px);opacity:.09}.how__glow--aqua{top:12%;left:-230px;background:var(--aqua)}.how__glow--blue{right:-230px;bottom:10%;background:var(--blue)}.how__heading{max-width:700px;margin:0 auto clamp(60px,7vw,95px);text-align:center;opacity:0;transform:translateY(18px)}.is-visible .how__heading{animation:rise .7s forwards}.eyebrow{display:inline-flex;align-items:center;gap:9px;margin-bottom:17px;padding:8px 14px;border:1px solid var(--line);border-radius:99px;color:#53606b;font-size:9px;font-weight:800;letter-spacing:.11em;text-transform:uppercase}.eyebrow i{width:8px;height:8px;border-radius:50%;background:linear-gradient(135deg,var(--aqua),var(--teal));box-shadow:0 0 0 4px rgba(0,224,171,.12)}.how__heading h2,.launch-panel h2{margin:0;font-size:clamp(40px,5vw,68px);font-weight:420;line-height:1.04;letter-spacing:-.052em}.how mark{background:linear-gradient(transparent 70%,rgba(124,230,210,.62) 70%);color:inherit}.how__heading p{max-width:540px;margin:18px auto 0;color:var(--muted);font-size:13px;line-height:1.65}.timeline{position:relative}.timeline__line{position:absolute;top:0;bottom:0;left:50%;width:2px;background:linear-gradient(var(--aqua),var(--blue),var(--aqua));transform:translateX(-50%)}.timeline__line i{position:absolute;inset:0;background:linear-gradient(transparent,rgba(255,255,255,.85),transparent);animation:scan 3s linear infinite}.step{display:grid;grid-template-columns:1fr 70px 1fr;align-items:center;min-height:390px;opacity:0;transform:translateY(25px)}.is-visible .step{animation:rise .7s var(--delay) forwards}.step--right .step__copy{grid-column:1;text-align:left}.step--right .step__dot{grid-column:2}.step--right .step__visual{grid-column:3}.step--left .step__visual{grid-column:1;grid-row:1}.step--left .step__dot{grid-column:2;grid-row:1}.step--left .step__copy{grid-column:3;grid-row:1}.step__copy{max-width:380px;padding:30px}.step__copy>span{color:#08786a;font-size:8px;font-weight:850;letter-spacing:.11em}.step__copy h3{margin:12px 0;font-size:clamp(22px,2.3vw,32px);letter-spacing:-.04em}.step__copy p{margin:0;color:var(--muted);font-size:11px;line-height:1.65}.step__copy a{display:inline-flex;align-items:center;gap:14px;margin-top:22px;padding:8px 9px 8px 17px;border-radius:99px;background:linear-gradient(135deg,var(--aqua),var(--teal));color:#07352c;font-size:9px;font-weight:800;text-decoration:none}.step__copy a b{display:grid;width:28px;height:28px;place-items:center;border-radius:50%;background:#fff}.step__dot{position:relative;z-index:3;display:grid;width:34px;height:34px;place-items:center;justify-self:center;border:8px solid #fff;border-radius:50%;background:linear-gradient(135deg,var(--aqua),var(--blue));box-shadow:0 6px 18px rgba(38,94,137,.25);color:transparent;font-size:0}.step__visual{position:relative;width:min(100%,390px);height:285px;overflow:hidden;justify-self:center;border-radius:26px;background:linear-gradient(145deg,#c9f5eb,#aabff2);box-shadow:0 30px 65px -42px rgba(27,51,84,.72);transition:transform .35s}.step__visual:hover{transform:translateY(-7px)}.step__visual>img{width:100%;height:100%;object-fit:cover;filter:saturate(.78);transition:transform .7s}.step__visual:hover>img{transform:scale(1.05)}.step__shade{position:absolute;inset:0;background:linear-gradient(145deg,rgba(0,224,171,.28),rgba(68,118,230,.24))}.mock{position:absolute;border:1px solid rgba(255,255,255,.85);background:rgba(255,255,255,.9);box-shadow:0 18px 38px -25px rgba(23,45,76,.62);backdrop-filter:blur(10px)}.mock--form{top:20px;right:18px;width:132px;padding:13px;border-radius:13px}.mock--form strong{display:block;font-size:8px}.mock--form>i{display:block;height:12px;margin-top:7px;border-radius:4px;background:#edf1f4}.mock--form button{width:100%;margin-top:8px;padding:7px;border:0;border-radius:6px;background:linear-gradient(135deg,var(--aqua),var(--blue));color:#fff;font-size:6px}.mock--domain{top:23px;left:20px;padding:13px 15px;border-radius:13px}.mock--domain small{display:block;color:#829087;font-size:5px}.mock--domain strong{display:block;margin:5px 0 9px;font-size:11px}.mock--domain span{display:flex;align-items:center;gap:5px;color:#08786a;font-size:6px}.mock--domain span i{width:6px;height:6px;border-radius:50%;background:var(--aqua)}.mock--migration{top:22px;right:18px;left:18px;display:flex;align-items:center;justify-content:center;gap:9px;padding:14px;border-radius:13px;font-size:7px}.mock--migration>span{padding:7px 9px;border-radius:7px;background:#eef4f2}.mock--migration>i{position:absolute;right:14px;bottom:7px;left:14px;height:4px;border-radius:99px;background:#e7ecea}.mock--migration>i strong{display:block;width:100%;height:100%;border-radius:inherit;background:linear-gradient(90deg,var(--aqua),var(--blue))}.mock--migration>small{position:absolute;right:14px;bottom:-12px;color:#fff;font-size:5px}.mock--live{top:18px;left:18px;padding:13px;border-radius:13px}.mock--live>strong{font-size:7px}.mock--live>div{display:flex;margin-top:10px}.mock--live i,.mock--live div span{display:grid;width:25px;height:25px;place-items:center;margin-right:-5px;border:2px solid #fff;border-radius:50%;background:#c7f1e6;color:#27665a;font-size:5px;font-style:normal;font-weight:800}.mock--live i:nth-child(2){background:#dbe4ff;color:#34589f}.success-badge{position:absolute;right:17px;bottom:16px;display:flex;align-items:center;gap:8px;padding:9px 11px;border:1px solid rgba(255,255,255,.9);border-radius:12px;background:rgba(255,255,255,.92);box-shadow:0 15px 30px -23px rgba(20,44,77,.65);backdrop-filter:blur(8px)}.success-badge>i{display:grid;width:23px;height:23px;place-items:center;border-radius:50%;background:rgba(0,202,182,.15);color:#08786a;font-style:normal;font-size:8px}.success-badge>span{font-size:7px;font-weight:800}.success-badge small{display:block;margin-top:2px;color:#849089;font-size:5px;font-weight:500}.launch-panel{margin-top:clamp(75px,9vw,130px);padding:clamp(40px,6vw,78px);border:1px solid var(--line);border-radius:32px;background:radial-gradient(circle at 90% 15%,rgba(68,118,230,.1),transparent 30%),radial-gradient(circle at 10% 90%,rgba(0,224,171,.1),transparent 32%),var(--ice);text-align:center}.launch-panel h2{font-size:clamp(34px,4vw,55px)}.launch-panel__copy{display:grid;grid-template-columns:1fr 1fr;gap:30px;max-width:740px;margin:30px auto}.launch-panel__copy p{margin:0;color:var(--muted);font-size:11px;line-height:1.7;text-align:left}.launch-panel>a{display:inline-flex;align-items:center;gap:15px;padding:9px 10px 9px 20px;border-radius:99px;background:#0d0d0d;color:#fff;font-size:9px;font-weight:750;text-decoration:none}.launch-panel>a b{display:grid;width:30px;height:30px;place-items:center;border-radius:50%;background:linear-gradient(135deg,var(--blue),var(--indigo))}@keyframes rise{to{opacity:1;transform:translateY(0)}}@keyframes scan{from{transform:translateY(-100%)}to{transform:translateY(100%)}}@media(max-width:760px){.timeline__line{left:17px}.step{grid-template-columns:35px 1fr;gap:10px;min-height:0;margin-bottom:55px}.step__dot,.step--left .step__dot,.step--right .step__dot{grid-column:1;grid-row:1;align-self:start;margin-top:4px}.step__copy,.step--left .step__copy,.step--right .step__copy{grid-column:2;grid-row:1;padding:0 0 20px}.step__visual,.step--left .step__visual,.step--right .step__visual{grid-column:2;grid-row:2;width:100%;height:270px}.launch-panel__copy{grid-template-columns:1fr}.launch-panel__copy p{text-align:center}}@media(max-width:450px){.how{padding-inline:14px}.how__heading h2{font-size:40px}.step__visual{height:245px}.launch-panel{padding:35px 20px}.launch-panel h2 br{display:none}}@media(prefers-reduced-motion:reduce){.how__heading,.step{opacity:1!important;transform:none!important;animation:none!important}.timeline__line i{animation:none}.step__visual,.step__visual img{transition:none!important}}
</style>
