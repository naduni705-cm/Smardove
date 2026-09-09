<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const visible = ref(false)
let observer

const categories = [
  'Business email',
  'Email security',
  'Team collaboration',
  'Email archive',
  'Mobile mail',
  'Administration',
  'Migration'
]

onMounted(() => {
  if (!('IntersectionObserver' in window)) {
    visible.value = true
    return
  }

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
  <section ref="root" class="specialists" :class="{ 'is-visible': visible }" aria-labelledby="specialists-title">
    <div class="specialists__glow specialists__glow--aqua" aria-hidden="true" />
    <div class="specialists__glow specialists__glow--blue" aria-hidden="true" />

    <div class="specialists__inner">
      <header class="specialists__heading">
        <span class="eyebrow"><i /> One complete email platform</span>
        <h2 id="specialists-title">Smardove specializes in<br><mark>everything business email.</mark></h2>
        <p>From secure communication and team collaboration to migration and administration, everything your business needs is built into one reliable platform.</p>
      </header>

      <nav class="category-list" aria-label="Smardove service categories">
        <a v-for="category in categories" :key="category" href="https://smardove.com/features/">{{ category }}</a>
      </nav>

      <div class="service-grid">
        <article class="service-card service-card--webmail" style="--delay:.08s">
          <img
            class="card-photo card-photo--webmail"
            src="https://images.unsplash.com/photo-1516321318423-f06f85e504b3?auto=format&fit=crop&w=900&q=85"
            alt="Professional using Smardove business email"
            loading="lazy"
          >
          <div class="card-photo-shade" aria-hidden="true" />
          <div class="service-card__copy">
            <span>01 · COMMUNICATE</span>
            <h3>Webmail &amp;<br>team chat</h3>
          </div>

          <div class="device-scene" aria-hidden="true">
            <div class="laptop">
              <div class="laptop__top"><i/><i/><i/></div>
              <div class="laptop__mail">
                <aside><b>S</b><i/><i/><i/></aside>
                <main><span>Good morning</span><strong>Your secure inbox</strong><i/><i/><i/></main>
              </div>
            </div>
            <div class="phone">
              <span>9:41</span>
              <b>Inbox</b>
              <i/><i/><i/>
            </div>
            <div class="online-dot">● Online</div>
          </div>
        </article>

        <article class="service-card service-card--support" style="--delay:.16s">
          <img
            class="card-photo card-photo--support"
            src="https://images.unsplash.com/photo-1551836022-d5d88e9218df?auto=format&fit=crop&w=900&q=85"
            alt="Smardove customer support specialist"
            loading="lazy"
          >
          <div class="card-photo-shade card-photo-shade--support" aria-hidden="true" />
          <div class="service-card__copy">
            <span>02 · SUPPORT</span>
            <h3>365 days<br>expert support</h3>
          </div>

          <div class="support-scene" aria-hidden="true">
            <div class="support-window">
              <div><i/> Smardove support</div>
              <p>How can we help?</p>
              <span>Average reply &lt; 5 min</span>
            </div>
          </div>
        </article>

        <article class="service-card service-card--schedule" style="--delay:.24s">
          <div class="clock" aria-hidden="true">
            <i />
          </div>
          <h3>Schedule work<br>at the right time</h3>
          <p>Plan messages, calendar events and team tasks without leaving your inbox.</p>
          <span class="status"><i /> Synced</span>
        </article>

        <article class="service-card service-card--setup" style="--delay:.32s">
          <span class="service-card__tag">04 · EASY SETUP</span>
          <h3>Ready in<br><strong>minutes</strong></h3>
          <p>Simple onboarding and guided migration.</p>
          <div class="setup-progress" aria-hidden="true">
            <span>Domain connected</span><i><b /></i>
          </div>
        </article>

        <article class="service-card service-card--global" style="--delay:.4s">
          <span class="service-card__tag">05 · WORK ANYWHERE</span>
          <h3>From any<br>location</h3>

          <div class="network" aria-hidden="true">
            <svg viewBox="0 0 240 190">
              <path d="M38 67 91 44l49 32 58-30M38 67l31 68 71-59 58 48M69 135l129-11M91 44l-22 91" />
              <circle cx="38" cy="67" r="8" />
              <circle cx="91" cy="44" r="8" />
              <circle cx="140" cy="76" r="8" />
              <circle cx="198" cy="46" r="8" />
              <circle cx="69" cy="135" r="8" />
              <circle cx="198" cy="124" r="8" />
            </svg>
            <div class="network__center">S</div>
          </div>
        </article>
      </div>

      <footer class="specialists__footer">
        <span><i>✓</i> Secure. Connected. Built for business.</span>
        <a href="https://smardove.com/pricing/">Find your email package <b>→</b></a>
      </footer>
    </div>
  </section>
</template>

<style scoped>
.specialists,.specialists *{box-sizing:border-box}.specialists{--ink:#0d0d0d;--charcoal:#20242b;--muted:#737985;--aqua:#00e0ab;--teal:#00cab6;--blue:#4476e6;--indigo:#4864f0;--soft-aqua:#7ce6d2;--periwinkle:#aabff2;--ice:#f7f9fc;--line:#e6eaf0;position:relative;isolation:isolate;overflow:hidden;width:100%;padding:clamp(78px,8vw,128px) clamp(16px,4vw,64px);background:#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.specialists__inner{width:min(1350px,100%);margin:auto}.specialists__glow{position:absolute;z-index:-1;width:420px;height:420px;border-radius:50%;filter:blur(135px);opacity:.09}.specialists__glow--aqua{top:-250px;left:-170px;background:var(--aqua)}.specialists__glow--blue{right:-220px;bottom:-220px;background:var(--blue)}.specialists__heading{max-width:860px;margin:auto;text-align:center;opacity:0;transform:translateY(20px)}.is-visible .specialists__heading{animation:rise .7s forwards}.eyebrow{display:inline-flex;align-items:center;gap:9px;margin-bottom:19px;padding:8px 14px;border:1px solid var(--line);border-radius:99px;color:#53606b;font-size:9px;font-weight:800;letter-spacing:.11em;text-transform:uppercase}.eyebrow i{width:8px;height:8px;border-radius:50%;background:linear-gradient(135deg,var(--aqua),var(--teal));box-shadow:0 0 0 4px rgba(0,224,171,.12)}.specialists__heading h2{margin:0;font-size:clamp(39px,5vw,68px);font-weight:420;line-height:1.03;letter-spacing:-.054em}.specialists__heading mark{padding:0 .03em;background:linear-gradient(transparent 70%,rgba(124,230,210,.62) 70%);color:inherit}.specialists__heading p{max-width:690px;margin:20px auto 0;color:var(--muted);font-size:13px;line-height:1.65}.category-list{display:flex;max-width:930px;align-items:center;justify-content:center;flex-wrap:wrap;gap:10px 25px;margin:clamp(34px,4vw,50px) auto clamp(44px,5vw,67px);opacity:0}.is-visible .category-list{animation:fade .6s .15s forwards}.category-list a{position:relative;color:#54616d;font-size:10px;font-weight:720;text-decoration:none}.category-list a::after{position:absolute;right:0;bottom:-5px;left:0;height:1px;background:linear-gradient(90deg,var(--aqua),var(--blue));content:"";transform:scaleX(0);transition:transform .25s}.category-list a:hover{color:var(--ink)}.category-list a:hover::after{transform:scaleX(1)}.service-grid{display:grid;grid-template-columns:1.12fr 1.12fr .82fr 1.02fr 1.08fr;align-items:end;gap:14px}.service-card{position:relative;overflow:hidden;border:1px solid var(--line);border-radius:25px;background:var(--ice);box-shadow:0 28px 60px -44px rgba(28,50,80,.68);opacity:0;transform:translateY(24px);transition:transform .3s,box-shadow .3s}.is-visible .service-card{animation:rise .65s var(--delay) forwards}.service-card:hover{transform:translateY(-7px);box-shadow:0 34px 70px -40px rgba(28,50,80,.74)}.service-card__copy{position:relative;z-index:2;padding:24px}.service-card__copy>span,.service-card__tag{display:block;margin-bottom:10px;color:#84daca;font-size:7px;font-weight:850;letter-spacing:.12em}.service-card h3{margin:0;font-size:clamp(16px,1.55vw,22px);line-height:1.18;letter-spacing:-.035em}.service-card--webmail{height:325px;border-color:#102c3b;background:#102f40;color:#fff}.device-scene{position:absolute;right:0;bottom:0;left:0;height:220px}.laptop{position:absolute;right:20px;bottom:0;width:190px;height:143px;overflow:hidden;border:6px solid #fff;border-bottom:12px solid #fff;border-radius:13px 13px 4px 4px;background:#f8faf9;box-shadow:0 18px 28px -18px #000}.laptop__top{display:flex;gap:4px;height:18px;align-items:center;padding-left:8px;background:#eef2ef}.laptop__top i{width:4px;height:4px;border-radius:50%;background:#bfc8c2}.laptop__mail{display:flex;height:108px;color:#17241e}.laptop__mail aside{display:flex;width:34px;align-items:center;flex-direction:column;gap:9px;padding:8px 0;background:#17221d}.laptop__mail aside b{display:grid;width:17px;height:17px;place-items:center;border-radius:5px;background:var(--aqua);font-size:6px}.laptop__mail aside i{width:14px;height:4px;border-radius:4px;background:#68716d}.laptop__mail main{flex:1;padding:13px 10px}.laptop__mail main span{display:block;color:#91a099;font-size:5px}.laptop__mail main strong{display:block;margin:6px 0 13px;font-size:10px}.laptop__mail main i{display:block;width:100%;height:12px;margin:5px 0;border-radius:4px;background:#e6f0ec}.phone{position:absolute;bottom:1px;left:18px;width:72px;height:135px;padding:14px 9px;border:5px solid #fff;border-radius:18px;background:#f8faf9;color:#14231d;box-shadow:0 17px 28px -18px #000}.phone span{display:block;text-align:center;font-size:5px}.phone b{display:block;margin:12px 0;font-size:8px}.phone i{display:block;height:13px;margin:7px 0;border-radius:5px;background:#d9f4ec}.online-dot{position:absolute;right:12px;bottom:15px;padding:7px 9px;border-radius:99px;background:#fff;color:#08786a;font-size:6px;font-weight:800}.service-card--support{height:285px;background:linear-gradient(150deg,#d0f6ed,#aabff2)}.support-scene{position:absolute;right:0;bottom:0;left:0;height:185px}.support-person{position:absolute;bottom:-3px;left:25px;width:92px;height:145px}.support-person .head{position:absolute;top:0;left:27px;width:39px;height:45px;border-radius:48% 48% 45% 45%;background:#ecc2a7}.support-person .head::before{position:absolute;top:-7px;right:-1px;left:-2px;height:21px;border-radius:25px 25px 10px 10px;background:#273451;content:""}.support-person .body{position:absolute;right:0;bottom:0;left:0;height:104px;border-radius:45px 45px 7px 7px;background:linear-gradient(135deg,var(--blue),var(--indigo))}.support-person .headset{position:absolute;top:4px;left:21px;width:51px;height:34px;border:4px solid #fff;border-bottom:0;border-radius:28px 28px 0 0}.support-window{position:absolute;right:15px;bottom:20px;width:130px;padding:13px;border:1px solid rgba(255,255,255,.9);border-radius:14px;background:rgba(255,255,255,.86);box-shadow:0 15px 30px -23px rgba(30,53,90,.6);backdrop-filter:blur(8px)}.support-window div{font-size:7px;font-weight:750}.support-window div i{display:inline-block;width:6px;height:6px;border-radius:50%;background:var(--aqua)}.support-window p{margin:13px 0 8px;font-size:10px;font-weight:700}.support-window span{color:#738078;font-size:6px}.service-card--schedule{height:235px;padding:25px 20px;background:#fff}.clock{display:grid;width:39px;height:39px;place-items:center;margin-bottom:26px;border-radius:50%;background:linear-gradient(135deg,rgba(0,224,171,.16),rgba(68,118,230,.13))}.clock i{position:relative;width:17px;height:17px;border:2px solid #30435c;border-radius:50%}.clock i::before{position:absolute;top:3px;left:7px;width:2px;height:6px;background:#30435c;content:""}.clock i::after{position:absolute;top:8px;left:7px;width:5px;height:2px;background:#30435c;content:""}.service-card--schedule p{margin:13px 0 20px;color:var(--muted);font-size:9px;line-height:1.5}.status{display:inline-flex;align-items:center;gap:6px;color:#08786a;font-size:7px;font-weight:750}.status i{width:6px;height:6px;border-radius:50%;background:var(--aqua)}.service-card--setup{height:285px;padding:25px 22px;background:linear-gradient(155deg,#253957,#17273c);color:#fff}.service-card--setup h3{margin-top:35px;color:#b9c5d4;font-size:16px;font-weight:500}.service-card--setup h3 strong{display:block;margin-top:8px;color:#fff;font-size:36px;font-weight:540}.service-card--setup p{margin:12px 0 0;color:#afbac8;font-size:8px;line-height:1.5}.setup-progress{position:absolute;right:22px;bottom:24px;left:22px}.setup-progress span{display:block;margin-bottom:9px;color:#dce4ec;font-size:7px}.setup-progress>i{display:block;height:5px;border-radius:99px;background:rgba(255,255,255,.14)}.setup-progress b{display:block;width:86%;height:100%;border-radius:inherit;background:linear-gradient(90deg,var(--aqua),var(--blue))}.service-card--global{height:325px;padding:25px 22px;background:linear-gradient(155deg,#effbf7,#eef3ff)}.service-card--global h3{font-size:21px}.network{position:absolute;right:7px;bottom:4px;left:7px;height:205px}.network svg{width:100%;height:100%}.network path{fill:none;stroke:rgba(68,118,230,.28);stroke-width:2;stroke-dasharray:5 6}.network circle{fill:#fff;stroke:var(--teal);stroke-width:5;filter:drop-shadow(0 8px 9px rgba(23,85,76,.14))}.network__center{position:absolute;top:50%;left:50%;display:grid;width:45px;height:45px;place-items:center;border:5px solid #fff;border-radius:50%;background:linear-gradient(135deg,var(--aqua),var(--blue));box-shadow:0 12px 22px -14px rgba(32,66,110,.5);color:#fff;font-size:12px;font-weight:900;transform:translate(-50%,-50%)}.specialists__footer{display:flex;align-items:center;justify-content:space-between;gap:25px;margin-top:30px;padding-top:26px;border-top:1px solid var(--line);opacity:0}.is-visible .specialists__footer{animation:fade .6s .65s forwards}.specialists__footer>span{display:flex;align-items:center;gap:9px;color:var(--muted);font-size:9px}.specialists__footer>span i{display:grid;width:24px;height:24px;place-items:center;border-radius:50%;background:rgba(0,202,182,.13);color:#08786a;font-style:normal}.specialists__footer a{display:flex;align-items:center;gap:14px;color:var(--ink);font-size:10px;font-weight:750;text-decoration:none}.specialists__footer a b{display:grid;width:33px;height:33px;place-items:center;border-radius:50%;background:linear-gradient(135deg,var(--blue),var(--indigo));color:#fff}@keyframes rise{to{opacity:1;transform:translateY(0)}}@keyframes fade{to{opacity:1}}@media(max-width:1080px){.service-grid{grid-template-columns:repeat(3,1fr)}.service-card{height:285px}.service-card--global{grid-column:span 2}}@media(max-width:700px){.specialists{padding-inline:14px}.specialists__heading h2 br{display:none}.service-grid{grid-template-columns:repeat(2,1fr)}.service-card--global{grid-column:span 2}.specialists__footer{align-items:flex-start;flex-direction:column}}@media(max-width:460px){.service-grid{grid-template-columns:1fr}.service-card,.service-card--global{grid-column:auto;height:290px}.specialists__heading h2{font-size:38px}}@media(prefers-reduced-motion:reduce){.specialists__heading,.category-list,.service-card,.specialists__footer{opacity:1!important;transform:none!important;animation:none!important}.service-card{transition:none!important}}
</style>

<style scoped>
/* Real card photography */
.card-photo {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform .7s cubic-bezier(.22, 1, .36, 1), filter .35s ease;
}

.card-photo--webmail {
  object-position: 56% center;
  filter: saturate(.78) brightness(.62) contrast(1.04);
}

.card-photo--support {
  object-position: center 42%;
  filter: saturate(.75) brightness(.92);
}

.card-photo-shade {
  position: absolute;
  inset: 0;
  background: linear-gradient(180deg, rgba(8, 35, 49, .78) 0%, rgba(8, 35, 49, .2) 50%, rgba(8, 35, 49, .48) 100%);
}

.card-photo-shade--support {
  background: linear-gradient(180deg, rgba(20, 70, 91, .5) 0%, rgba(0, 202, 182, .08) 52%, rgba(35, 69, 105, .34) 100%);
}

.service-card--webmail:hover .card-photo,
.service-card--support:hover .card-photo {
  transform: scale(1.055);
}

.service-card--support .service-card__copy {
  color: #fff;
  text-shadow: 0 2px 16px rgba(14, 37, 55, .42);
}

.service-card--support .service-card__copy > span {
  color: #c7fff2;
}

.service-card--support .support-window {
  right: 14px;
  bottom: 17px;
}

.service-card--webmail .device-scene,
.service-card--support .support-scene {
  z-index: 2;
}
</style>
