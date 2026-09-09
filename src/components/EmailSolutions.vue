<script setup>
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'

const current = ref(0)
const perView = ref(4)

const solutions = [
  { tag: 'SELL SMARTER', title: 'Turn email into revenue', text: 'Build trust, follow up faster and turn professional conversations into loyal customers.', stat: '+28%', statLabel: 'reply rate', type: 'sales', color: 'aqua' },
  { tag: 'DELIVERABILITY', title: 'Reach every inbox', text: 'Keep important business messages moving with secure, dependable email delivery.', stat: '99.9%', statLabel: 'delivery uptime', type: 'delivery', color: 'blue' },
  { tag: 'SECURITY', title: 'Protect every message', text: 'Built-in spam filtering, antivirus and policy controls protect your team around the clock.', stat: '24/7', statLabel: 'protection', type: 'security', color: 'indigo' },
  { tag: 'COLLABORATION', title: 'Work better together', text: 'Combine email, contacts, calendars, tasks and team conversations in one workspace.', stat: '1', statLabel: 'connected space', type: 'team', color: 'teal' },
  { tag: 'STORAGE', title: 'Scale without limits', text: 'Choose flexible mailbox storage from 2GB to 500GB as your organization grows.', stat: '500GB', statLabel: 'maximum storage', type: 'storage', color: 'blue' },
  { tag: 'EMAIL ARCHIVE', title: 'Keep every record', text: 'Store and recover important business messages in a secure, audit-ready archive.', stat: '100%', statLabel: 'searchable', type: 'archive', color: 'aqua' },
  { tag: 'MOBILE MAIL', title: 'Stay productive anywhere', text: 'Give your team a consistent and professional inbox across desktop and mobile.', stat: 'Any', statLabel: 'device', type: 'mobile', color: 'indigo' },
  { tag: 'ADMIN CONTROL', title: 'Manage with confidence', text: 'Control users, domains, storage and security policies from one simple dashboard.', stat: '1', statLabel: 'admin console', type: 'admin', color: 'teal' }
]

const maxIndex = computed(() => Math.max(0, solutions.length - perView.value))
const progress = computed(() => ((current.value + perView.value) / solutions.length) * 100)

function updatePerView() {
  const width = window.innerWidth
  perView.value = width < 620 ? 1 : width < 900 ? 2 : width < 1180 ? 3 : 4
  current.value = Math.min(current.value, maxIndex.value)
}
function previous() { current.value = Math.max(0, current.value - perView.value) }
function next() { current.value = Math.min(maxIndex.value, current.value + perView.value) }

onMounted(() => { updatePerView(); window.addEventListener('resize', updatePerView) })
onBeforeUnmount(() => window.removeEventListener('resize', updatePerView))
</script>

<template>
  <section class="email-solutions" aria-labelledby="solutions-title">
    <div class="email-solutions__glow email-solutions__glow--aqua" />
    <div class="email-solutions__glow email-solutions__glow--blue" />

    <div class="email-solutions__inner">
      <header class="section-head">
        <div>
          <span class="eyebrow"><i /> Smardove business email</span>
          <h2 id="solutions-title">Everything your business needs<br><mark>to communicate and grow.</mark></h2>
        </div>
        <div class="section-head__side">
          <p>Secure email, powerful collaboration and dependable support—built into one professional platform.</p>
          <a href="https://smardove.com/pricing/">View email packages <span>↗</span></a>
        </div>
      </header>

      <div class="slider" aria-roledescription="carousel">
        <div class="slider__top">
          <span>Explore solutions</span>
          <div class="slider__controls">
            <button type="button" aria-label="Previous solutions" :disabled="current === 0" @click="previous">←</button>
            <button type="button" aria-label="Next solutions" :disabled="current >= maxIndex" @click="next">→</button>
          </div>
        </div>

        <div class="slider__viewport">
          <div class="slider__track" :style="{ '--current': current, '--per-view': perView }">
            <article v-for="(item, index) in solutions" :key="item.title" class="solution-card" :class="`solution-card--${item.color}`">
              <div class="solution-card__visual" :class="`visual--${item.type}`">
                <span class="card-number">{{ String(index + 1).padStart(2, '0') }}</span>
                <div class="mini-window">
                  <div class="mini-window__bar"><i/><i/><i/><span>mail.smardove.com</span></div>
                  <div class="mini-window__body">
                    <template v-if="item.type === 'sales'">
                      <small>Sales conversations</small><b>Revenue activity</b>
                      <div class="bars"><i/><i/><i/><i/><i/></div>
                    </template>
                    <template v-else-if="item.type === 'delivery'">
                      <small>Delivery health</small><b>All systems operational</b>
                      <div class="delivery-ring">99<span>%</span></div>
                    </template>
                    <template v-else-if="item.type === 'security'">
                      <div class="shield">✓</div><b>Mailbox protected</b><small>Threat monitoring is active</small>
                    </template>
                    <template v-else-if="item.type === 'team'">
                      <small>Team workspace</small><b>8 members online</b>
                      <div class="avatars"><i>AM</i><i>JD</i><i>SK</i><i>+5</i></div>
                    </template>
                    <template v-else-if="item.type === 'storage'">
                      <small>Mailbox capacity</small><b>Storage that grows</b>
                      <div class="storage"><i/><span>328GB available</span></div>
                    </template>
                    <template v-else-if="item.type === 'archive'">
                      <small>Email archive</small><b>Find any message</b>
                      <div class="search">Search archived email <i>⌕</i></div>
                    </template>
                    <template v-else-if="item.type === 'mobile'">
                      <div class="phone"><span>●</span><b>Inbox</b><i/><i/><i/></div>
                    </template>
                    <template v-else>
                      <small>Administration</small><b>Domain overview</b>
                      <div class="settings"><span>Users <i>186</i></span><span>Security <i>On</i></span></div>
                    </template>
                  </div>
                </div>
                <div class="floating-stat"><strong>{{ item.stat }}</strong><span>{{ item.statLabel }}</span></div>
              </div>

              <div class="solution-card__copy">
                <span class="tag">{{ item.tag }}</span>
                <h3>{{ item.title }}</h3>
                <p>{{ item.text }}</p>
                <a href="https://smardove.com/features/" :aria-label="`Learn more about ${item.title}`">Learn more <span>→</span></a>
              </div>
            </article>
          </div>
        </div>

        <div class="slider__footer">
          <div class="progress"><i :style="{ width: `${progress}%` }" /></div>
          <span>{{ String(current + 1).padStart(2, '0') }} — {{ String(Math.min(current + perView, solutions.length)).padStart(2, '0') }} / {{ String(solutions.length).padStart(2, '0') }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.email-solutions,.email-solutions *{box-sizing:border-box}.email-solutions{--ink:#0d0d0d;--charcoal:#20242b;--muted:#737985;--aqua:#00e0ab;--teal:#00cab6;--blue:#4476e6;--indigo:#4864f0;--soft-aqua:#7ce6d2;--periwinkle:#aabff2;--ice:#f7f9fc;--line:#e6eaf0;position:relative;isolation:isolate;overflow:hidden;width:100%;padding:clamp(76px,8vw,128px) clamp(16px,4vw,64px);background:#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.email-solutions__inner{width:min(1460px,100%);margin:auto}.email-solutions__glow{position:absolute;z-index:-1;width:430px;height:430px;border-radius:50%;filter:blur(130px);opacity:.11}.email-solutions__glow--aqua{top:-240px;left:-150px;background:var(--aqua)}.email-solutions__glow--blue{right:-210px;bottom:-200px;background:var(--blue)}.section-head{display:grid;grid-template-columns:1.45fr .55fr;align-items:end;gap:clamp(30px,6vw,100px);margin-bottom:clamp(48px,6vw,80px)}.eyebrow{display:inline-flex;align-items:center;gap:9px;margin-bottom:19px;color:#52606c;font-size:10px;font-weight:800;letter-spacing:.11em;text-transform:uppercase}.eyebrow i{width:8px;height:8px;border-radius:50%;background:linear-gradient(135deg,var(--aqua),var(--teal));box-shadow:0 0 0 5px rgba(0,224,171,.12)}.section-head h2{margin:0;font-size:clamp(38px,5vw,72px);font-weight:420;line-height:1.02;letter-spacing:-.055em}.section-head mark{background:linear-gradient(transparent 70%,rgba(124,230,210,.55) 70%);color:inherit}.section-head__side{padding-bottom:6px}.section-head__side p{margin:0 0 24px;color:var(--muted);font-size:13px;line-height:1.65}.section-head__side a{display:inline-flex;align-items:center;gap:16px;color:var(--ink);font-size:11px;font-weight:800;text-decoration:none}.section-head__side a span{display:grid;width:34px;height:34px;place-items:center;border-radius:50%;background:linear-gradient(135deg,var(--blue),var(--indigo));color:#fff}.slider__top{display:flex;align-items:center;justify-content:space-between;margin-bottom:18px}.slider__top>span{font-size:11px;font-weight:750}.slider__controls{display:flex;gap:8px}.slider__controls button{display:grid;width:42px;height:42px;place-items:center;border:1px solid var(--line);border-radius:50%;background:#fff;color:var(--ink);font-size:17px;cursor:pointer;transition:.25s}.slider__controls button:hover:not(:disabled){border-color:var(--blue);background:var(--blue);color:#fff;transform:translateY(-2px)}.slider__controls button:disabled{cursor:not-allowed;opacity:.3}.slider__viewport{overflow:hidden}.slider__track{display:flex;gap:16px;transform:translateX(calc(var(--current) * (-1 * ((100% - (var(--per-view) - 1) * 16px) / var(--per-view) + 16px))));transition:transform .65s cubic-bezier(.22,1,.36,1)}.solution-card{flex:0 0 calc((100% - (var(--per-view) - 1) * 16px) / var(--per-view));overflow:hidden;border:1px solid var(--line);border-radius:25px;background:#fff;box-shadow:0 24px 55px -42px rgba(27,47,74,.48);transition:transform .3s,box-shadow .3s}.solution-card:hover{transform:translateY(-7px);box-shadow:0 30px 65px -38px rgba(27,47,74,.55)}.solution-card__visual{position:relative;height:250px;overflow:hidden;padding:28px;background:linear-gradient(145deg,#d9f8ef,#effbf7)}.solution-card--blue .solution-card__visual{background:linear-gradient(145deg,#dce7ff,#f1f5ff)}.solution-card--indigo .solution-card__visual{background:linear-gradient(145deg,#dcdffd,#f1f2ff)}.solution-card--teal .solution-card__visual{background:linear-gradient(145deg,#c9f5ed,#effbf8)}.card-number{position:absolute;top:19px;left:20px;color:rgba(13,13,13,.4);font-size:9px;font-weight:800;letter-spacing:.1em}.mini-window{position:absolute;right:-12px;bottom:-12px;width:84%;height:185px;overflow:hidden;border:1px solid rgba(255,255,255,.9);border-radius:17px 0 0 0;background:rgba(255,255,255,.91);box-shadow:0 22px 45px -28px rgba(39,70,94,.45);backdrop-filter:blur(8px);transition:transform .35s}.solution-card:hover .mini-window{transform:translate(-5px,-5px)}.mini-window__bar{display:flex;align-items:center;gap:5px;height:31px;padding:0 11px;border-bottom:1px solid rgba(13,13,13,.06)}.mini-window__bar>i{width:5px;height:5px;border-radius:50%;background:#c9d5ce}.mini-window__bar>span{margin-left:5px;color:#a1aaa5;font-size:5px}.mini-window__body{display:flex;height:calc(100% - 31px);justify-content:center;flex-direction:column;padding:17px}.mini-window__body>small{margin-bottom:5px;color:#849089;font-size:7px;text-transform:uppercase;letter-spacing:.08em}.mini-window__body>b{font-size:11px}.bars{display:flex;height:61px;align-items:flex-end;gap:7px;margin-top:13px;border-bottom:1px solid #e8eeea}.bars i{flex:1;border-radius:4px 4px 0 0;background:linear-gradient(var(--aqua),var(--teal))}.bars i:nth-child(1){height:28%}.bars i:nth-child(2){height:47%}.bars i:nth-child(3){height:66%}.bars i:nth-child(4){height:55%}.bars i:nth-child(5){height:90%;background:linear-gradient(var(--blue),var(--indigo))}.delivery-ring{display:grid;width:76px;height:76px;place-items:center;margin:13px auto 0;border:9px solid rgba(68,118,230,.14);border-top-color:var(--blue);border-right-color:var(--indigo);border-radius:50%;font-size:20px;font-weight:750}.delivery-ring span{font-size:8px}.shield{display:grid;width:62px;height:68px;place-items:center;margin:0 auto 9px;border-radius:25px 25px 30px 30px;background:linear-gradient(135deg,var(--blue),var(--indigo));clip-path:polygon(50% 0,95% 17%,87% 72%,50% 100%,13% 72%,5% 17%);color:#fff;font-size:21px}.visual--security .mini-window__body{text-align:center}.avatars{display:flex;margin-top:21px}.avatars i{display:grid;width:37px;height:37px;place-items:center;margin-right:-7px;border:3px solid #fff;border-radius:50%;background:#c4f1e5;color:#176d5e;font-style:normal;font-size:7px;font-weight:800}.avatars i:nth-child(even){background:#dce5ff;color:#375ead}.storage{margin-top:20px}.storage i{display:block;width:100%;height:9px;border-radius:99px;background:linear-gradient(90deg,var(--teal) 72%,#e9eeeb 72%)}.storage span{display:block;margin-top:8px;color:#7d8982;font-size:7px}.search{display:flex;align-items:center;justify-content:space-between;margin-top:20px;padding:10px;border:1px solid #e5ebe7;border-radius:9px;color:#a0aaa4;font-size:7px}.search i{color:var(--blue);font-size:13px}.phone{width:92px;height:135px;margin:auto;padding:13px;border:4px solid #20242b;border-radius:18px;background:#fff}.phone>span{display:block;text-align:center;font-size:6px}.phone>b{display:block;margin:12px 0;font-size:10px}.phone i{display:block;height:7px;margin:8px 0;border-radius:9px;background:#e5e9f0}.phone i:nth-of-type(2){width:75%;background:#c7f1e6}.settings{display:grid;gap:9px;margin-top:16px}.settings span{display:flex;justify-content:space-between;padding:10px;border-radius:9px;background:#f4f7f5;font-size:8px}.settings i{color:#08786a;font-style:normal}.floating-stat{position:absolute;top:24px;right:18px;display:flex;min-width:74px;flex-direction:column;padding:10px 12px;border:1px solid rgba(255,255,255,.9);border-radius:12px;background:rgba(255,255,255,.86);box-shadow:0 14px 30px -22px rgba(27,47,74,.6);backdrop-filter:blur(8px)}.floating-stat strong{font-size:12px}.floating-stat span{margin-top:2px;color:#7d8782;font-size:6px;text-transform:uppercase}.solution-card__copy{min-height:230px;padding:25px 23px}.tag{color:#08786a;font-size:8px;font-weight:850;letter-spacing:.12em}.solution-card--blue .tag,.solution-card--indigo .tag{color:#365fb8}.solution-card h3{margin:11px 0 12px;font-size:20px;line-height:1.18;letter-spacing:-.035em}.solution-card p{min-height:67px;margin:0;color:var(--muted);font-size:11px;line-height:1.6}.solution-card__copy>a{display:flex;align-items:center;justify-content:space-between;margin-top:21px;padding-top:17px;border-top:1px solid var(--line);color:var(--ink);font-size:10px;font-weight:750;text-decoration:none}.solution-card__copy>a span{display:grid;width:27px;height:27px;place-items:center;border-radius:50%;background:var(--ice);transition:.25s}.solution-card:hover .solution-card__copy>a span{background:var(--blue);color:#fff}.slider__footer{display:flex;align-items:center;gap:18px;margin-top:26px}.progress{height:3px;flex:1;overflow:hidden;border-radius:99px;background:#eef1f4}.progress i{display:block;height:100%;border-radius:inherit;background:linear-gradient(90deg,var(--aqua),var(--blue));transition:width .65s}.slider__footer>span{color:#929ba5;font-size:9px;font-weight:750;letter-spacing:.08em}@media(max-width:850px){.section-head{grid-template-columns:1fr}.section-head h2 br{display:none}.section-head__side{max-width:560px}}@media(max-width:620px){.email-solutions{padding-inline:14px}.section-head{margin-bottom:40px}.solution-card__visual{height:235px}.solution-card__copy{min-height:215px}.slider__controls button{width:39px;height:39px}}@media(prefers-reduced-motion:reduce){.slider__track,.solution-card,.mini-window,.slider__controls button,.progress i{transition:none!important}}
</style>
