<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const visible = ref(false)
let observer

const plans = [
  {
    name: 'Starter', price: '$4.99', unit: '/user/month', description: 'For individuals and small teams', featured: false,
    features: ['25 GB mailbox storage', 'Custom domain email', 'Advanced spam protection', 'Webmail & mobile access', 'Email forwarding', 'Standard support']
  },
  {
    name: 'Business Pro', price: '$9.99', unit: '/user/month', description: 'For growing businesses and teams', featured: true,
    features: ['50 GB mailbox storage', 'Unlimited email aliases', 'Premium threat protection', 'Calendars & contacts', 'Easy email migration', 'Priority support']
  },
  {
    name: 'Enterprise', price: 'Custom', unit: '', description: 'For organisations with advanced needs', featured: false,
    features: ['Custom mailbox storage', 'Advanced admin controls', 'Dedicated mail security', 'Compliance assistance', 'Managed migration', 'Dedicated account support']
  }
]

onMounted(() => {
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) { visible.value = true; observer.disconnect() }
  }, { threshold: 0.12 })
  if (root.value) observer.observe(root.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section ref="root" class="pricing" :class="{ 'is-visible': visible }" aria-labelledby="pricing-title">
    <div class="pricing__orb pricing__orb--one" aria-hidden="true" />
    <div class="pricing__orb pricing__orb--two" aria-hidden="true" />
    <div class="pricing__inner">
      <header class="pricing__header">
        <span class="pricing-pill">Pricing Plans</span>
        <h2 id="pricing-title">Flexible <mark>Email Plans</mark></h2>
        <p>Choose a professional email plan that grows with your business.<br>No hidden fees, reliable delivery, and protection included.</p>
      </header>

      <div class="plans">
        <article v-for="(plan, index) in plans" :key="plan.name" class="plan" :class="{ 'plan--featured': plan.featured }" :style="{ '--delay': `${.18 + index * .13}s` }">
          <div v-if="plan.featured" class="popular">Most Popular</div>
          <div class="plan__summary">
            <span class="plan__name">{{ plan.name }}</span>
            <div class="plan__price"><strong>{{ plan.price }}</strong><small>{{ plan.unit }}</small></div>
            <p>{{ plan.description }}</p>
          </div>

          <ul class="plan__features">
            <li v-for="feature in plan.features" :key="feature"><i>✓</i>{{ feature }}</li>
          </ul>

          <a :href="plan.featured ? 'https://smardove.com/pricing/' : 'https://smardove.com/contact/'">
            {{ plan.price === 'Custom' ? 'Contact Sales' : 'Get Started Now' }}
            <span>↗</span>
          </a>

          <div v-if="plan.featured" class="featured-lines" aria-hidden="true"><i/><i/><i/></div>
        </article>
      </div>

      <footer class="pricing__footer"><span><i>✓</i> Secure checkout</span><span><i>✓</i> Cancel anytime</span><span><i>✓</i> Migration support</span></footer>
    </div>
  </section>
</template>

<style scoped>
.pricing,.pricing *{box-sizing:border-box}.pricing{--ink:#0d0d0d;--muted:#747a72;--green:#c9e6a8;--green-deep:#92bd68;--yellow:#f3ee9a;position:relative;isolation:isolate;overflow:hidden;width:100%;padding:clamp(70px,8vw,120px) clamp(16px,3vw,42px) clamp(55px,6vw,90px);background:radial-gradient(circle at 8% 8%,rgba(243,238,154,.5),transparent 30%),radial-gradient(circle at 94% 88%,rgba(201,230,168,.55),transparent 32%),linear-gradient(180deg,#fff,#f8fbf4);color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.pricing::before{position:absolute;z-index:-2;inset:0;background-image:linear-gradient(rgba(13,13,13,.018) 1px,transparent 1px),linear-gradient(90deg,rgba(13,13,13,.018) 1px,transparent 1px);background-size:50px 50px;mask-image:linear-gradient(#000,transparent 47%);content:""}.pricing__orb{position:absolute;z-index:-1;border:1px solid rgba(255,255,255,.76);border-radius:50%;pointer-events:none}.pricing__orb--one{top:140px;left:-180px;width:520px;height:520px}.pricing__orb--two{top:90px;right:-240px;width:600px;height:600px}.pricing__inner{width:min(1420px,100%);margin:auto}.pricing__header{text-align:center;opacity:0;transform:translateY(24px)}.is-visible .pricing__header{animation:rise .75s forwards}.pricing-pill{display:inline-flex;padding:9px 17px;border:1px solid #bfdaa5;border-radius:999px;background:rgba(255,255,255,.72);box-shadow:0 8px 25px rgba(30,43,24,.06);font-size:11px;font-weight:650}.pricing h2{margin:13px 0 14px;font-family:var(--font-display,var(--font-sans));font-size:clamp(39px,4.7vw,68px);font-weight:420;line-height:1.04;letter-spacing:-.055em}.pricing h2 mark{padding:0 3px;background:linear-gradient(transparent 64%,var(--yellow) 64%);color:inherit}.pricing__header p{margin:0;color:var(--muted);font-size:clamp(11px,1vw,15px);line-height:1.55}.plans{display:flex;flex-direction:column;gap:20px;margin-top:clamp(46px,5vw,72px)}.plan{position:relative;display:grid;min-height:205px;grid-template-columns:235px 1fr 205px;align-items:center;gap:clamp(25px,4vw,65px);overflow:hidden;padding:clamp(28px,3.5vw,48px) clamp(28px,4vw,70px);border:1px solid rgba(219,226,215,.94);border-radius:26px;background:rgba(255,255,255,.9);box-shadow:0 22px 62px -48px rgba(30,44,23,.36);opacity:0;transform:translateY(28px);transition:transform .3s ease,border-color .3s ease,box-shadow .3s ease}.is-visible .plan{animation:rise .72s var(--delay) forwards}.plan:hover{border-color:#c8dbb9;box-shadow:0 29px 72px -43px rgba(30,44,23,.46);transform:translateY(-5px)}.plan--featured{border-color:#242824;background:linear-gradient(115deg,#0d0f0d,#1b2018);color:#fff;box-shadow:0 28px 70px -37px rgba(13,18,11,.65)}.plan--featured:hover{border-color:#3d4938;box-shadow:0 34px 78px -35px rgba(13,18,11,.76)}.popular{position:absolute;top:0;left:50%;padding:7px 18px;border-radius:0 0 12px 12px;background:var(--green);color:#25331e;font-size:8px;font-weight:800;letter-spacing:.1em;text-transform:uppercase;transform:translateX(-50%)}.plan__summary{position:relative;z-index:2}.plan__name{font-size:14px;font-weight:700}.plan__price{display:flex;align-items:flex-end;gap:7px;margin:9px 0 7px}.plan__price strong{font-size:clamp(34px,3.3vw,49px);font-weight:500;line-height:1;letter-spacing:-.055em}.plan__price small{padding-bottom:5px;color:#8a9187;font-size:8px}.plan--featured .plan__price small{color:#aeb7aa}.plan__summary p{margin:0;color:var(--muted);font-size:9px}.plan--featured .plan__summary p{color:#bbc2b8}.plan__features{position:relative;z-index:2;display:grid;grid-template-columns:1fr 1fr;gap:17px 30px;margin:0;padding:0;list-style:none}.plan__features li{display:flex;align-items:center;gap:10px;color:#60675e;font-size:clamp(10px,.88vw,13px)}.plan--featured .plan__features li{color:#eff2ed}.plan__features i{display:grid;width:19px;height:19px;flex:0 0 auto;place-items:center;border-radius:50%;background:#edf6e5;color:#5e843f;font-style:normal;font-size:8px;font-weight:900}.plan--featured .plan__features i{background:var(--yellow);color:#292913}.plan>a{position:relative;z-index:2;display:flex;min-height:54px;align-items:center;justify-content:center;gap:14px;padding:10px 13px;border:1px solid #b9d89b;border-radius:999px;background:#fff;color:#20251e;font-size:11px;font-weight:700;text-decoration:none;transition:background .25s ease,transform .25s ease}.plan>a:hover{background:var(--green);transform:scale(1.025)}.plan>a span{font-size:17px}.plan--featured>a{border-color:var(--green);background:var(--green);color:#1e2a18}.plan--featured>a:hover{background:var(--yellow);border-color:var(--yellow)}.featured-lines{position:absolute;right:-4%;bottom:-115px;left:0;height:210px;opacity:.28}.featured-lines i{position:absolute;bottom:0;width:48%;height:170px;border:1px solid #dce5d7;border-radius:50% 50% 0 0}.featured-lines i:nth-child(1){left:-7%}.featured-lines i:nth-child(2){left:29%;height:190px}.featured-lines i:nth-child(3){right:-7%}.pricing__footer{display:flex;align-items:center;justify-content:center;gap:clamp(20px,5vw,70px);margin-top:35px;color:#747b72;font-size:9px}.pricing__footer span{display:flex;align-items:center;gap:8px}.pricing__footer i{display:grid;width:20px;height:20px;place-items:center;border-radius:50%;background:var(--yellow);color:#454411;font-style:normal;font-size:8px;font-weight:900}
@keyframes rise{to{opacity:1;transform:translateY(0)}}
@media(max-width:960px){.plan{grid-template-columns:190px 1fr}.plan>a{grid-column:1/-1;width:220px;justify-self:end}.plan__features{gap:14px 20px}}
@media(max-width:650px){.pricing{padding:58px 14px}.pricing h2{font-size:clamp(38px,11vw,52px)}.pricing__header p br{display:none}.plans{gap:15px}.plan{grid-template-columns:1fr;gap:25px;padding:31px 24px;border-radius:22px}.plan__features{grid-template-columns:1fr}.plan>a{grid-column:auto;width:100%}.popular{right:20px;left:auto;transform:none}.pricing__footer{align-items:flex-start;flex-direction:column;gap:12px;padding-left:18px}.pricing__orb{display:none}}
@media(prefers-reduced-motion:reduce){.pricing__header,.plan{opacity:1!important;transform:none!important;animation:none!important}.plan{transition:none}}
</style>
