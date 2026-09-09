<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const active = ref(false)
let observer

onMounted(() => {
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      active.value = true
      observer.disconnect()
    }
  }, { threshold: 0.16 })
  if (root.value) observer.observe(root.value)
})

onBeforeUnmount(() => observer?.disconnect())

const stats = [
  { value: '99.9%', label: 'Delivery uptime' },
  { value: '700+', label: 'Businesses' },
  { value: '24/7', label: 'Mail protection' }
]

const features = [
  { icon: '✉', text: 'Business email' },
  { icon: '▦', text: 'Team mailboxes' },
  { icon: '↗', text: 'Easy migration' },
  { icon: '▣', text: 'Live support' }
]
</script>

<template>
  <section ref="root" class="community" :class="{ 'is-active': active }" aria-labelledby="community-title">
    <div class="community__glow community__glow--yellow" aria-hidden="true" />
    <div class="community__glow community__glow--green" aria-hidden="true" />

    <div class="network" aria-hidden="true">
      <svg class="network__lines" viewBox="0 0 1200 520" preserveAspectRatio="none">
        <path class="network__line network__line--outer" pathLength="1" d="M72 486C190 42 1000 10 1135 486" />
        <path class="network__line network__line--inner" pathLength="1" d="M190 486C285 130 902 105 1014 486" />
        <path class="network__dash" pathLength="1" d="M72 486C190 42 1000 10 1135 486" />
      </svg>

      <div class="float-item float-item--vote"><i>✓</i> Delivery completed</div>
      <div class="float-item float-item--posts"><span class="mini-avatar">NA</span> 12 new messages</div>
      <div class="float-item float-item--like"><i>♥</i> 128</div>
      <div class="float-item float-item--comment"><i>□</i> 24</div>
      <div class="float-item float-item--secure"><i>◆</i><small>256-bit</small></div>

      <div class="person person--one"><svg viewBox="0 0 64 64"><rect width="64" height="64" rx="32" fill="#f3ee9a"/><path d="M12 64c1-15 9-23 20-23s19 8 20 23" fill="#202420"/><circle cx="32" cy="27" r="14" fill="#b97855"/><path d="M18 27c0-13 7-19 15-19 10 0 16 8 14 21-4-2-7-7-9-12-5 7-11 10-20 10Z" fill="#26221f"/><circle cx="27" cy="28" r="1.2"/><circle cx="37" cy="28" r="1.2"/><path d="M28 34c3 2 5 2 8 0" fill="none" stroke="#713d30" stroke-linecap="round"/></svg><i /></div>
      <div class="person person--two"><svg viewBox="0 0 64 64"><rect width="64" height="64" rx="32" fill="#c9e6a8"/><path d="M11 64c2-15 9-22 21-22s19 7 21 22" fill="#f8f9f6"/><circle cx="32" cy="27" r="14" fill="#9d674c"/><path d="M18 25C18 13 24 7 33 7c11 0 16 9 14 20-5-2-9-6-12-11-4 6-9 9-17 9Z" fill="#161815"/><circle cx="27" cy="28" r="1.2"/><circle cx="37" cy="28" r="1.2"/><path d="M28 34c3 2 5 2 8 0" fill="none" stroke="#653a2e" stroke-linecap="round"/></svg><i /></div>
      <div class="person person--three"><svg viewBox="0 0 64 64"><rect width="64" height="64" rx="32" fill="#ecefe9"/><path d="M10 64c2-15 10-23 22-23s20 8 22 23" fill="#171a17"/><circle cx="32" cy="27" r="14" fill="#70462f"/><path d="M18 25C18 13 24 7 33 7c10 0 16 8 14 20-5-1-10-5-13-10-4 6-9 8-16 8Z" fill="#17120f"/><circle cx="27" cy="28" r="1.2"/><circle cx="37" cy="28" r="1.2"/><path d="M28 34c3 2 5 2 8 0" fill="none" stroke="#4b281e" stroke-linecap="round"/></svg><i /></div>
      <div class="person person--four"><svg viewBox="0 0 64 64"><rect width="64" height="64" rx="32" fill="#f3ee9a"/><path d="M10 64c2-15 10-23 22-23s20 8 22 23" fill="#c9e6a8"/><circle cx="32" cy="27" r="14" fill="#d09a78"/><path d="M18 28C16 16 22 7 32 7c12 0 17 10 15 22-4-8-10-12-18-12-2 5-6 9-11 11Z" fill="#4a2f24"/><circle cx="27" cy="29" r="1.2"/><circle cx="37" cy="29" r="1.2"/><path d="M28 35c3 2 5 2 8 0" fill="none" stroke="#814b3d" stroke-linecap="round"/></svg><i /></div>

      <div class="mail-node mail-node--one"><svg viewBox="0 0 24 24"><path d="m4 7 8 6 8-6M5 5h14a2 2 0 0 1 2 2v10a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V7a2 2 0 0 1 2-2Z"/></svg></div>
      <div class="mail-node mail-node--two"><svg viewBox="0 0 24 24"><path d="M12 3 20 6v5c0 5-3 8-8 10-5-2-8-5-8-10V6Z"/><path d="m8.5 12 2.2 2.2 4.8-5"/></svg></div>
    </div>

    <div class="community__content">
      <div class="stats" aria-label="Smardove statistics">
        <div v-for="(stat, index) in stats" :key="stat.label" class="stat" :style="{ '--delay': `${.55 + index * .12}s` }">
          <strong>{{ stat.value }}</strong>
          <span>{{ stat.label }}</span>
        </div>
      </div>

      <h2 id="community-title">We Build Better Connections<br><mark>Through Smarter Email</mark></h2>

      <div class="feature-pills">
        <span v-for="(feature, index) in features" :key="feature.text" :style="{ '--delay': `${.95 + index * .09}s` }">
          <i>{{ feature.icon }}</i>{{ feature.text }}
        </span>
      </div>
    </div>

    <div class="side-actions">
      <a href="https://smardove.com/features/" aria-label="Explore Smardove features">
        <svg viewBox="0 0 34 34"><path d="M7 14V7h7M27 20v7h-7M8 8l8 8M26 26l-8-8"/></svg>
      </a>
      <button type="button" aria-label="Replay animation" @click="active = false; requestAnimationFrame(() => active = true)">
        <svg viewBox="0 0 34 34"><path d="M27 13a11 11 0 1 0 1 10M27 7v7h-7"/><path d="m26 22 2 2 4-5"/></svg>
      </button>
    </div>
  </section>
</template>

<style scoped>
.community,.community *{box-sizing:border-box}.community{--ink:#0d0d0d;--muted:#8a9088;--green:#c9e6a8;--green-deep:#91bd67;--yellow:#f3ee9a;position:relative;isolation:isolate;min-height:clamp(680px,59vw,900px);overflow:hidden;padding:clamp(70px,8vw,120px) clamp(90px,9vw,150px) 70px;background:#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.community::before{position:absolute;z-index:-2;inset:0;background-image:linear-gradient(rgba(13,13,13,.018) 1px,transparent 1px),linear-gradient(90deg,rgba(13,13,13,.018) 1px,transparent 1px);background-size:48px 48px;mask-image:linear-gradient(transparent,#000 40%,transparent);content:""}.community__glow{position:absolute;z-index:-1;width:420px;height:420px;border-radius:50%;filter:blur(110px);opacity:.18;pointer-events:none}.community__glow--yellow{top:-240px;left:10%;background:var(--yellow)}.community__glow--green{right:4%;bottom:-270px;background:var(--green)}.network{position:absolute;top:56px;left:50%;width:min(1120px,80vw);height:500px;transform:translateX(-50%)}.network__lines{position:absolute;inset:0;width:100%;height:100%;overflow:visible;fill:none}.network__line{stroke:#e9ede7;stroke-width:1.5;stroke-dasharray:1;stroke-dashoffset:1}.network__line--inner{stroke:#dfe5dc}.network__dash{stroke:url(#none);stroke-width:1}.is-active .network__line{animation:draw 1.55s .12s cubic-bezier(.25,.7,.2,1) forwards}.is-active .network__line--inner{animation-delay:.3s}.float-item{position:absolute;z-index:3;display:flex;min-height:34px;align-items:center;gap:8px;padding:7px 13px;border:1px solid #e4e9e1;border-radius:999px;background:rgba(255,255,255,.92);box-shadow:0 10px 28px rgba(26,38,21,.08);backdrop-filter:blur(12px);color:#6f766d;font-size:10px;font-weight:650;white-space:nowrap;opacity:0;transform:translateY(12px) scale(.94)}.is-active .float-item{animation:badgeIn .55s .65s forwards,float 4.5s 1.3s ease-in-out infinite}.float-item i{display:grid;place-items:center;width:18px;height:18px;border-radius:50%;background:var(--green);color:#365126;font-style:normal;font-size:8px}.float-item--vote{top:165px;left:1%;border-color:#b8d99a;background:#ebf7df;color:#5f7f45}.float-item--posts{top:15px;left:45%;animation-delay:.72s!important}.float-item--like{top:60px;right:21%;animation-delay:.86s!important}.float-item--like i{background:var(--yellow);color:#8e6d21}.float-item--comment{top:236px;right:-1%;animation-delay:.94s!important}.float-item--comment i{background:#f1f3ef}.float-item--secure{top:65px;left:19%;border-radius:12px;animation-delay:1.02s!important}.float-item--secure small{font-size:7px}.mini-avatar{display:grid;width:20px;height:20px;place-items:center;border-radius:50%;background:#151815;color:var(--yellow);font-size:6px;font-weight:800}.person{position:absolute;z-index:3;display:grid;width:57px;height:57px;place-items:center;border:4px solid #fff;border-radius:50%;background:linear-gradient(145deg,#272b27,#0d0d0d);box-shadow:0 12px 30px rgba(27,39,21,.14),0 0 0 2px rgba(201,230,168,.35);color:var(--yellow);font-size:11px;font-weight:800;opacity:0;transform:scale(.6)}.person i{position:absolute;right:-1px;bottom:1px;width:12px;height:12px;border:3px solid #fff;border-radius:50%;background:var(--green-deep)}.is-active .person{animation:personIn .55s .68s forwards,personFloat 4s 1.3s ease-in-out infinite}.person--one{top:245px;left:12%;animation-delay:.75s!important}.person--two{top:96px;left:47%;animation-delay:.88s!important}.person--three{top:89px;right:8%;animation-delay:1s!important}.person--four{top:237px;right:23%;animation-delay:1.1s!important}.mail-node{position:absolute;z-index:3;display:grid minima;display:grid;width:54px;height:54px;place-items:center;border:1px solid #dfe7da;border-radius:16px;background:#f6fbf1;box-shadow:0 12px 28px rgba(33,48,25,.08);opacity:0;transform:rotate(-8deg) scale(.7)}.mail-node svg{width:24px;fill:none;stroke:#53614d;stroke-width:1.6;stroke-linecap:round;stroke-linejoin:round}.is-active .mail-node{animation:nodeIn .55s .82s forwards,nodeFloat 5s 1.4s ease-in-out infinite}.mail-node--one{top:145px;right:20%}.mail-node--two{top:234px;left:24%;background:#fffdf0}.community__content{position:relative;z-index:5;max-width:780px;margin:330px auto 0;text-align:center}.stats{display:flex;align-items:flex-start;justify-content:center;gap:clamp(34px,6vw,78px)}.stat{display:flex;min-width:120px;flex-direction:column;opacity:0;transform:translateY(18px)}.is-active .stat{animation:rise .65s var(--delay) forwards}.stat strong{color:#182118;font-size:clamp(34px,4vw,57px);font-weight:450;line-height:1;letter-spacing:-.055em}.stat span{margin-top:9px;color:var(--muted);font-size:11px}.community h2{margin:clamp(34px,4vw,55px) 0 30px;font-family:var(--font-display,var(--font-sans));font-size:clamp(34px,3.5vw,53px);font-weight:380;line-height:1.09;letter-spacing:-.04em;opacity:0;transform:translateY(20px)}.is-active h2{animation:rise .72s .75s forwards}.community h2 mark{padding:0 3px;background:linear-gradient(transparent 64%,var(--yellow) 64%);color:inherit}.feature-pills{display:flex;flex-wrap:wrap;justify-content:center;gap:10px}.feature-pills>span{display:inline-flex;min-height:42px;align-items:center;gap:9px;padding:9px 17px;border:1px solid #e2e7df;border-radius:10px;background:rgba(255,255,255,.9);box-shadow:0 9px 26px rgba(27,38,23,.045);color:#737970;font-size:10px;font-weight:620;opacity:0;transform:translateY(15px);transition:border-color .25s ease,transform .25s ease,box-shadow .25s ease}.is-active .feature-pills>span{animation:rise .55s var(--delay) forwards}.feature-pills>span:hover{border-color:#c8dcba;box-shadow:0 13px 28px rgba(30,44,23,.09);transform:translateY(-4px)}.feature-pills i{display:grid;width:20px;height:20px;place-items:center;border-radius:6px;background:#f2f7ed;color:#3f4b39;font-style:normal}.feature-pills>span:nth-child(odd) i{background:#fffbd2}.side-actions{position:absolute;z-index:8;right:clamp(20px,3vw,48px);bottom:65px;display:flex;flex-direction:column;gap:15px}.side-actions a,.side-actions button{display:grid;width:76px;height:76px;padding:0;place-items:center;border:1px solid #eef1eb;border-radius:50%;background:rgba(255,255,255,.94);box-shadow:0 17px 38px rgba(28,39,23,.07);color:var(--ink);cursor:pointer;transition:transform .28s ease,background .28s ease}.side-actions a:hover,.side-actions button:hover{transform:scale(1.06) rotate(4deg);background:#f7fbea}.side-actions svg{width:34px;fill:none;stroke:currentColor;stroke-width:2.2;stroke-linecap:round;stroke-linejoin:round}
@keyframes draw{to{stroke-dashoffset:0}}@keyframes rise{to{opacity:1;transform:translateY(0)}}@keyframes badgeIn{to{opacity:1;transform:translateY(0) scale(1)}}@keyframes personIn{to{opacity:1;transform:scale(1)}}@keyframes nodeIn{to{opacity:1;transform:rotate(0) scale(1)}}@keyframes float{50%{translate:0 -6px}}@keyframes personFloat{50%{translate:0 -8px}}@keyframes nodeFloat{50%{translate:0 7px}}
@media(max-width:1000px){.community{padding-inline:35px}.network{width:92vw}.side-actions{right:18px;bottom:25px}.side-actions a,.side-actions button{width:60px;height:60px}.side-actions svg{width:28px}}
@media(max-width:700px){.community{min-height:760px;padding:50px 14px 95px}.network{top:30px;width:110vw;height:390px}.network__lines{opacity:.8}.float-item{font-size:8px;padding:6px 9px}.float-item--vote{top:145px;left:8%}.float-item--posts{left:38%}.float-item--comment{right:7%;top:203px}.float-item--secure,.float-item--like{display:none}.person{width:45px;height:45px}.person--one{top:220px;left:13%}.person--two{top:80px}.person--three{top:84px;right:10%}.person--four{top:205px}.mail-node{width:42px;height:42px;border-radius:13px}.mail-node--one{top:135px}.mail-node--two{top:205px}.community__content{margin-top:280px}.stats{gap:12px}.stat{min-width:0;flex:1}.stat strong{font-size:clamp(27px,9vw,39px)}.stat span{font-size:8px}.community h2{margin-top:38px;font-size:clamp(34px,10vw,47px)}.feature-pills{display:grid;grid-template-columns:1fr 1fr}.feature-pills>span{justify-content:center;padding:8px;font-size:8px}.side-actions{right:14px;bottom:18px;flex-direction:row}.side-actions a,.side-actions button{width:52px;height:52px}}
@media(prefers-reduced-motion:reduce){.network__line{stroke-dashoffset:0!important}.float-item,.person,.mail-node,.stat,.community h2,.feature-pills>span{opacity:1!important;transform:none!important;animation:none!important}.feature-pills>span:hover{transform:none}}
/* Smardove theme background and inline profile portraits */
.community{background:radial-gradient(circle at 8% 6%,rgba(243,238,154,.58),transparent 28%),radial-gradient(circle at 92% 12%,rgba(201,230,168,.62),transparent 31%),linear-gradient(180deg,#fbfcf8 0%,#fff 52%,#f8fbf4 100%)}.community::after{position:absolute;z-index:-2;top:-32%;left:50%;width:118%;height:73%;border:1px solid rgba(255,255,255,.72);border-radius:0 0 50% 50%;background:linear-gradient(112deg,rgba(243,238,154,.24),rgba(255,255,255,.32) 45%,rgba(201,230,168,.3));transform:translateX(-50%);content:"";pointer-events:none}.network__line--outer{stroke:rgba(122,153,93,.23)}.network__line--inner{stroke:rgba(195,179,80,.22)}.person{overflow:visible;padding:0;border-color:rgba(255,255,255,.96);background:#fff;color:transparent}.person>svg{display:block;width:100%;height:100%;overflow:hidden;border-radius:50%;filter:saturate(.92) contrast(.98)}.person::after{position:absolute;inset:-7px;border:1px solid rgba(201,230,168,.42);border-radius:50%;content:"";animation:avatarRing 2.8s ease-in-out infinite}.person--one::after,.person--four::after{border-color:rgba(243,238,154,.65)}.float-item,.feature-pills>span{background:rgba(255,255,255,.82);box-shadow:0 14px 38px rgba(38,51,31,.09);backdrop-filter:blur(16px)}.community h2{color:#111}.stat strong{color:#172017}.side-actions a,.side-actions button{background:rgba(255,255,255,.84);backdrop-filter:blur(16px)}
@keyframes avatarRing{50%{transform:scale(1.09);opacity:.35}}
@media(prefers-reduced-motion:reduce){.person::after{animation:none!important}}
</style>
