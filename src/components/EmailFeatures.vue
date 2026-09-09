<script setup>
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const visible = ref(false)
const page = ref(0)
const perPage = ref(4)
let observer

const features = [
  { title:'Increase Sales', tag:'Business growth', desc:'Build trusted customer relationships and turn email conversations into revenue.', result:'Convert more leads', second:'Faster follow-ups', icon:'M4 19V9m5 10V5m5 14v-7m5 7V3M3 21h18', tone:'blue', image:'/images/smardove-feature-illustration.png' },
  { title:'Smardove Client', tag:'Professional inbox', desc:'Manage business email in a fast, focused and easy-to-use Smardove inbox.', result:'One clean inbox', second:'Work from anywhere', icon:'M3 6h18v12H3V6Zm0 1 9 6 9-6', tone:'aqua' },
  { title:'Group Chat', tag:'Instant communication', desc:'Message colleagues instantly without moving everyday conversations to another tool.', result:'Faster decisions', second:'Connected teams', icon:'M4 5h16v11H9l-5 4V5Zm4 5h8', tone:'violet' },
  { title:'Team Spaces', tag:'Team collaboration', desc:'Keep shared messages, files and project discussions organized in dedicated spaces.', result:'Organized projects', second:'Shared knowledge', icon:'M8 11a3 3 0 1 0 0-6 3 3 0 0 0 0 6Zm8-1a2.5 2.5 0 1 0 0-5M3 20c0-4 2-7 5-7s5 3 5 7m1-7c4 0 7 2 7 6', tone:'blue' },
  { title:'Video Conferencing', tag:'Secure meetings', desc:'Start reliable video meetings and share your screen directly with your team.', result:'Face-to-face calls', second:'Screen sharing', icon:'M3 6h13v12H3V6Zm13 4 5-3v10l-5-3', tone:'ink' },
  { title:'2GB–500GB Storage', tag:'Flexible storage', desc:'Select the right mailbox capacity today and expand it as your business grows.', result:'Up to 500GB', second:'Scalable mailboxes', icon:'M4 6c0-2 4-3 8-3s8 1 8 3-4 3-8 3-8-1-8-3Zm0 0v6c0 2 4 3 8 3s8-1 8-3V6m-16 6v6c0 2 4 3 8 3s8-1 8-3v-6', tone:'aqua' },
  { title:'365 Days Support', tag:'Always available', desc:'Get dependable technical guidance whenever your business needs assistance.', result:'Everyday support', second:'Helpful specialists', icon:'M4 13a8 8 0 0 1 16 0v5h-4v-6h4M4 18H2v-5h2m5 3h6', tone:'green' },
  { title:'Contacts', tag:'Address book', desc:'Keep customer and colleague details organized, searchable and ready to use.', result:'Find people fast', second:'Shared contacts', icon:'M12 12a4 4 0 1 0 0-8 4 4 0 0 0 0 8ZM5 21c0-4 2-7 7-7s7 3 7 7', tone:'violet' },
  { title:'Calendaring', tag:'Smart scheduling', desc:'Plan meetings, reminders and company events using shared business calendars.', result:'Simple scheduling', second:'Shared events', icon:'M4 5h16v16H4V5Zm4-2v4m8-4v4M4 10h16', tone:'blue' },
  { title:'Notes', tag:'Quick capture', desc:'Save useful ideas and important information without leaving your workspace.', result:'Never lose an idea', second:'Easy organization', icon:'M5 3h14v18H5V3Zm3 5h8m-8 4h8m-8 4h5', tone:'aqua' },
  { title:'Tasks', tag:'Productivity', desc:'Convert messages into clear actions, assign work and follow team progress.', result:'Clear next steps', second:'Track completion', icon:'M9 6h11M9 12h11M9 18h11M4 6l1 1 2-2m-3 7 1 1 2-2m-3 7 1 1 2-2', tone:'green' },
  { title:'Desktop Client', tag:'Desktop access', desc:'Use a focused desktop email experience for productive work throughout the day.', result:'Quick desktop access', second:'Focused workflow', icon:'M3 4h18v13H3V4Zm5 17h8m-4-4v4', tone:'ink' },
  { title:'Reporting', tag:'Business insights', desc:'Understand email delivery, user activity and storage through clear reports.', result:'Actionable insights', second:'Clear performance', icon:'M4 20V10h4v10m4 0V4h4v16m4 0v-7h4v7', tone:'blue' },
  { title:'Remote Management', tag:'Admin control', desc:'Manage users, domains, devices and security policies securely from anywhere.', result:'Control anywhere', second:'Central administration', icon:'M12 3a9 9 0 1 0 9 9M3 12h18M12 3c3 3 3 15 0 18m0-18c-3 3-3 15 0 18', tone:'aqua' },
  { title:'Multi Language', tag:'Global teams', desc:'Let every employee use Smardove comfortably in their preferred language.', result:'Global accessibility', second:'Local experience', icon:'M4 5h10M9 3v2m-3 5c3 0 6-2 7-5m-6 1c1 3 3 5 6 6m3 8 3-8 3 8m-5-3h4', tone:'violet' }
]

const pageCount = computed(() => Math.ceil(features.length / perPage.value))
const currentFeatures = computed(() => {
  const start = page.value * perPage.value
  return features.slice(start, start + perPage.value).map((feature, index) => ({ ...feature, number:start + index + 1 }))
})

function updateLayout(){
  perPage.value = window.innerWidth < 600 ? 1 : window.innerWidth < 960 ? 2 : 4
  if(page.value >= pageCount.value) page.value = Math.max(0, pageCount.value - 1)
}
function next(){ page.value = (page.value + 1) % pageCount.value }
function previous(){ page.value = (page.value - 1 + pageCount.value) % pageCount.value }

onMounted(() => {
  updateLayout()
  window.addEventListener('resize', updateLayout)
  if(!('IntersectionObserver' in window)){ visible.value = true; return }
  observer = new IntersectionObserver(([entry]) => {
    if(entry.isIntersecting){ visible.value = true; observer.disconnect() }
  }, { threshold:.12 })
  if(root.value) observer.observe(root.value)
})
onBeforeUnmount(() => {
  observer?.disconnect()
  window.removeEventListener('resize', updateLayout)
})
</script>

<template>
  <section ref="root" class="features" :class="{ visible }" aria-labelledby="features-title">
    <div class="features__inner">
      <header class="heading">
        <span class="eyebrow"><i/> Smardove email features</span>
        <h2 id="features-title">Everything your team needs<br><mark>to communicate and grow.</mark></h2>
        <p>Explore practical business tools built into one secure email platform.</p>
      </header>

      <div class="carousel-head">
        <div><strong>Explore features</strong><span>{{ page * perPage + 1 }}–{{ Math.min((page + 1) * perPage, features.length) }} of {{ features.length }}</span></div>
        <div class="arrows">
          <button type="button" aria-label="Previous features" @click="previous"><span>←</span></button>
          <button type="button" aria-label="Next features" @click="next"><span>→</span></button>
        </div>
      </div>

      <TransitionGroup name="slide" tag="div" class="card-grid">
        <article v-for="feature in currentFeatures" :key="feature.title" class="feature-card" :class="`feature-card--${feature.tone}`">
          <div
            class="visual"
            :class="{ 'visual--image': feature.image }"
            :style="feature.image ? { backgroundImage: `linear-gradient(180deg, rgba(8,31,52,.03), rgba(8,31,52,.48)), url('${feature.image}')` } : undefined"
          >
            <span class="visual__number">{{ String(feature.number).padStart(2,'0') }}</span>
            <span class="visual__icon" aria-hidden="true"><svg viewBox="0 0 24 24"><path :d="feature.icon"/></svg></span>
            <div class="visual__message"><i>✓</i><span><small>Business benefit</small><b>{{ feature.result }}</b></span></div>
            <span class="visual__line visual__line--one"/><span class="visual__line visual__line--two"/>
          </div>
          <div class="content">
            <span class="tag">{{ feature.tag }}</span>
            <h3>{{ feature.title }}</h3>
            <p>{{ feature.desc }}</p>
            <ul><li><i>✓</i>{{ feature.result }}</li><li><i>✓</i>{{ feature.second }}</li></ul>
          </div>
        </article>
      </TransitionGroup>

      <div class="pagination" aria-label="Feature pages">
        <button v-for="dot in pageCount" :key="dot" type="button" :class="{ active:page === dot-1 }" :aria-label="`Show feature page ${dot}`" @click="page=dot-1"/>
      </div>
    </div>
  </section>
</template>

<style scoped>
.features,.features *{box-sizing:border-box}.features{--ink:#0d0d0d;--text:#20242b;--muted:#737985;--aqua:#00e0ab;--teal:#00cab6;--blue:#4476e6;--indigo:#4864f0;--peri:#aabff2;position:relative;overflow:hidden;padding:clamp(76px,8vw,126px) clamp(14px,4vw,60px);background:radial-gradient(circle at 5% 30%,rgba(0,224,171,.06),transparent 24%),radial-gradient(circle at 96% 75%,rgba(68,118,230,.07),transparent 25%),#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.features__inner{width:min(1450px,100%);margin:auto}.heading{max-width:850px;margin:0 auto clamp(48px,5.5vw,76px);text-align:center;opacity:0;transform:translateY(18px)}.visible .heading{animation:rise .65s forwards}.eyebrow{display:inline-flex;align-items:center;gap:9px;margin-bottom:19px;padding:8px 13px;border:1px solid #e1e7ed;border-radius:99px;color:#52606d;font-size:9px;font-weight:800;letter-spacing:.1em;text-transform:uppercase}.eyebrow i{width:8px;height:8px;border-radius:50%;background:linear-gradient(135deg,var(--aqua),var(--blue));box-shadow:0 0 0 4px rgba(0,224,171,.1)}.heading h2{margin:0;font-size:clamp(36px,4.8vw,66px);font-weight:410;line-height:1.04;letter-spacing:-.055em}.heading mark{background:linear-gradient(transparent 70%,rgba(170,191,242,.78) 70%);color:inherit}.heading p{margin:18px 0 0;color:var(--muted);font-size:14px}.carousel-head{display:flex;align-items:flex-end;justify-content:space-between;margin-bottom:17px}.carousel-head>div:first-child{display:flex;flex-direction:column;gap:5px}.carousel-head strong{font-size:13px}.carousel-head>div:first-child span{color:#99a3ae;font-size:9px;font-weight:750;letter-spacing:.07em;text-transform:uppercase}.arrows{display:flex;gap:8px}.arrows button{display:grid;width:44px;height:44px;place-items:center;border:1px solid #dce4ec;border-radius:50%;background:#fff;color:#17212b;cursor:pointer;box-shadow:0 14px 28px -23px rgba(25,52,91,.6);transition:.23s ease}.arrows button:hover{border-color:transparent;background:linear-gradient(135deg,var(--blue),var(--indigo));color:#fff;transform:translateY(-2px)}.arrows span{font-size:16px}.card-grid{position:relative;display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:16px}.feature-card{overflow:hidden;border:1px solid #dfe6ed;border-radius:25px;background:#fff;box-shadow:0 22px 55px -43px rgba(27,56,96,.42);transition:transform .28s ease,box-shadow .28s ease,border-color .28s ease}.feature-card:hover{border-color:#b9cbed;box-shadow:0 32px 65px -40px rgba(36,73,137,.46);transform:translateY(-7px)}.visual{--accent:var(--blue);position:relative;height:210px;overflow:hidden;background:linear-gradient(145deg,#dfe9ff,#f1f5ff)}.feature-card--aqua .visual,.feature-card--green .visual{--accent:#009d87;background:linear-gradient(145deg,#caf5eb,#effbf7)}.feature-card--violet .visual{--accent:var(--indigo);background:linear-gradient(145deg,#e1e4ff,#f4f2ff)}.feature-card--ink .visual{--accent:var(--aqua);background:linear-gradient(145deg,#1d2220,#101312)}.visual::before{position:absolute;right:-35px;bottom:-75px;width:190px;height:190px;border:1px solid rgba(255,255,255,.75);border-radius:50%;background:rgba(255,255,255,.18);content:""}.visual__number{position:absolute;top:17px;left:18px;color:rgba(26,43,62,.46);font-size:9px;font-weight:800;letter-spacing:.1em}.feature-card--ink .visual__number{color:rgba(255,255,255,.45)}.visual__icon{position:absolute;top:50%;left:50%;display:grid;width:78px;height:78px;place-items:center;border:1px solid rgba(255,255,255,.82);border-radius:24px;background:rgba(255,255,255,.77);box-shadow:0 24px 45px -29px rgba(26,55,99,.6);transform:translate(-50%,-61%);backdrop-filter:blur(12px)}.feature-card--ink .visual__icon{border-color:rgba(255,255,255,.1);background:rgba(255,255,255,.08)}.visual__icon svg{width:36px;height:36px;fill:none;stroke:var(--accent);stroke-width:1.5;stroke-linecap:round;stroke-linejoin:round}.visual__message{position:absolute;right:16px;bottom:16px;left:16px;display:flex;align-items:center;gap:9px;padding:10px 12px;border:1px solid rgba(255,255,255,.85);border-radius:13px;background:rgba(255,255,255,.83);box-shadow:0 14px 30px -23px rgba(25,52,91,.55);backdrop-filter:blur(10px)}.feature-card--ink .visual__message{border-color:rgba(255,255,255,.1);background:rgba(255,255,255,.09);color:#fff}.visual__message>i{display:grid;width:27px;height:27px;place-items:center;border-radius:9px;background:var(--accent);color:#fff;font-style:normal;font-size:9px}.visual__message span{display:flex;flex-direction:column;gap:2px}.visual__message small{color:#85909b;font-size:6px;text-transform:uppercase;letter-spacing:.08em}.feature-card--ink .visual__message small{color:rgba(255,255,255,.45)}.visual__message b{font-size:9px}.visual__line{position:absolute;height:1px;background:rgba(68,118,230,.16)}.visual__line--one{top:49px;right:17px;width:52px}.visual__line--two{top:56px;right:17px;width:35px}.content{padding:23px 21px 22px}.tag{display:block;margin-bottom:9px;color:#087a69;font-size:8px;font-weight:800;letter-spacing:.1em;text-transform:uppercase}.feature-card--blue .tag,.feature-card--violet .tag{color:#3b61bf}.content h3{min-height:46px;margin:0 0 10px;font-size:19px;font-weight:720;line-height:1.18;letter-spacing:-.032em}.content p{min-height:58px;margin:0;color:var(--muted);font-size:11px;line-height:1.58}.content ul{display:grid;gap:8px;margin:16px 0 0;padding:14px 0 0;border-top:1px solid #e8edf2;list-style:none}.content li{display:flex;align-items:center;gap:8px;color:#46525f;font-size:9px;font-weight:650}.content li i{display:grid;width:17px;height:17px;place-items:center;border-radius:50%;background:rgba(0,202,182,.12);color:#07806d;font-style:normal;font-size:7px}.pagination{display:flex;justify-content:center;gap:7px;margin-top:24px}.pagination button{width:7px;height:7px;padding:0;border:0;border-radius:99px;background:#ced7e0;cursor:pointer;transition:.25s}.pagination button.active{width:28px;background:linear-gradient(90deg,var(--teal),var(--blue))}.slide-enter-active,.slide-leave-active{transition:opacity .3s ease,transform .3s ease}.slide-enter-from{opacity:0;transform:translateX(20px)}.slide-leave-to{opacity:0;transform:translateX(-20px)}.slide-leave-active{position:absolute}@keyframes rise{to{opacity:1;transform:translateY(0)}}@media(max-width:960px){.card-grid{grid-template-columns:repeat(2,1fr)}}@media(max-width:600px){.features{padding-inline:13px}.heading h2 br{display:none}.card-grid{grid-template-columns:1fr}.visual{height:220px}.content h3,.content p{min-height:0}.carousel-head{align-items:flex-end}}@media(prefers-reduced-motion:reduce){.heading{opacity:1;transform:none;animation:none}.feature-card,.arrows button,.slide-enter-active,.slide-leave-active{transition:none}}
.visual--image{background-repeat:no-repeat!important;background-position:68% center!important;background-size:cover!important}.visual--image::before{display:none}.visual--image .visual__number{padding:6px 9px;border:1px solid rgba(255,255,255,.7);border-radius:99px;background:rgba(255,255,255,.86);color:#263646;box-shadow:0 10px 22px -17px rgba(0,0,0,.55);backdrop-filter:blur(8px)}.visual--image .visual__icon{background:rgba(255,255,255,.9)}.visual--image .visual__message{background:rgba(255,255,255,.92)}
</style>
