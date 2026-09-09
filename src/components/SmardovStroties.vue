<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const visible = ref(false)
let observer

const profiles = [
  { name: 'Amelia', role: 'Migration specialist', image: 'https://images.unsplash.com/photo-1494790108377-be9c29b29330?auto=format&fit=crop&w=300&q=85' },
  { name: 'Daniel', role: 'Security engineer', image: 'https://images.unsplash.com/photo-1500648767791-00dcc994a43e?auto=format&fit=crop&w=300&q=85' },
  { name: 'Sophia', role: 'Customer success', image: 'https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&w=300&q=85' },
  { name: 'James', role: 'Email specialist', image: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?auto=format&fit=crop&w=300&q=85' },
  { name: 'Maya', role: 'Support lead', image: 'https://images.unsplash.com/photo-1531123897727-8f129e1688ce?auto=format&fit=crop&w=300&q=85' },
  { name: 'Noah', role: 'Solutions expert', image: 'https://images.unsplash.com/photo-1506794778202-cad84cf45f1d?auto=format&fit=crop&w=300&q=85' }
]

onMounted(() => {
  if (!('IntersectionObserver' in window)) return (visible.value = true)
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      visible.value = true
      observer.disconnect()
    }
  }, { threshold: .15 })
  if (root.value) observer.observe(root.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section ref="root" class="experts" :class="{ 'is-visible': visible }" aria-labelledby="experts-title">
    <div class="experts__glow experts__glow--aqua" />
    <div class="experts__glow experts__glow--blue" />

    <div class="experts__inner">
      <header class="experts__heading">
        <span class="eyebrow"><i /> People behind your inbox</span>
        <h2 id="experts-title"><mark>365-day support</mark> from email experts</h2>
        <p>Experienced specialists helping your business communicate securely, migrate confidently and stay connected.</p>
      </header>

      <div class="experts-layout">
        <div class="trust-list trust-list--left">
          <article>
            <span class="trust-icon">✓</span>
            <div><h3>Proven experience</h3><p>Our specialists understand business email, security, migration and reliable delivery.</p></div>
          </article>
          <article>
            <span class="trust-icon">↗</span>
            <div><h3>Continuous training</h3><p>Every expert stays current with modern email standards and security practices.</p></div>
          </article>
        </div>

        <div class="expert-orbit" aria-label="Smardove email specialist team">
          <div class="orbit orbit--outer" />
          <div class="orbit orbit--inner" />
          <div class="orbit-glow" />

          <div class="brand-center">
            <svg viewBox="0 0 54 40" aria-hidden="true">
              <path d="M4 7h29c7 0 13 6 13 13s-6 13-13 13H4l13-13L4 7Z" />
              <path d="m5 8 19 15L44 8" />
            </svg>
            <strong>Smardove</strong>
            <span>Email experts</span>
          </div>

          <div
            v-for="(profile, index) in profiles"
            :key="profile.name"
            class="profile"
            :class="`profile--${index + 1}`"
          >
            <img :src="profile.image" :alt="`${profile.name}, ${profile.role}`" loading="lazy">
            <span><b>{{ profile.name }}</b>{{ profile.role }}</span>
          </div>

          <span class="verified verified--1">✓</span>
          <span class="verified verified--2">✓</span>
          <span class="verified verified--3">✓</span>
        </div>

        <div class="trust-list trust-list--right">
          <article>
            <span class="trust-icon">✓</span>
            <div><h3>Expert verification</h3><p>Every team member is carefully assessed before supporting your organization.</p></div>
          </article>
          <article>
            <span class="trust-icon">✓</span>
            <div><h3>Personal assessment</h3><p>We verify communication skills, technical knowledge and customer-first service.</p></div>
          </article>
        </div>
      </div>

      <footer class="experts__footer">
        <span><i /> Support available every day of the year</span>
        <a href="https://smardove.com/contact/">Talk to an expert <b>→</b></a>
      </footer>
    </div>
  </section>
</template>

<style scoped>
.experts,.experts *{box-sizing:border-box}.experts{--ink:#0d0d0d;--muted:#737985;--aqua:#00e0ab;--teal:#00cab6;--blue:#4476e6;--indigo:#4864f0;--soft:#7ce6d2;--peri:#aabff2;--ice:#f7f9fc;--line:#e6eaf0;position:relative;isolation:isolate;overflow:hidden;width:100%;padding:clamp(78px,8vw,128px) clamp(16px,4vw,64px);background:#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.experts__inner{width:min(1400px,100%);margin:auto}.experts__glow{position:absolute;z-index:-1;width:420px;height:420px;border-radius:50%;filter:blur(140px);opacity:.09}.experts__glow--aqua{top:-230px;left:-170px;background:var(--aqua)}.experts__glow--blue{right:-200px;bottom:-230px;background:var(--blue)}.experts__heading{max-width:780px;margin:0 auto clamp(52px,6vw,82px);text-align:center;opacity:0;transform:translateY(20px)}.is-visible .experts__heading{animation:rise .7s forwards}.eyebrow{display:inline-flex;align-items:center;gap:9px;margin-bottom:18px;padding:8px 14px;border:1px solid var(--line);border-radius:99px;color:#53606b;font-size:9px;font-weight:800;letter-spacing:.11em;text-transform:uppercase}.eyebrow i{width:8px;height:8px;border-radius:50%;background:linear-gradient(135deg,var(--aqua),var(--teal));box-shadow:0 0 0 4px rgba(0,224,171,.12)}.experts__heading h2{margin:0;font-size:clamp(39px,5vw,68px);font-weight:420;line-height:1.04;letter-spacing:-.052em}.experts__heading mark{background:linear-gradient(transparent 70%,rgba(124,230,210,.64) 70%);color:inherit}.experts__heading p{max-width:620px;margin:19px auto 0;color:var(--muted);font-size:13px;line-height:1.7}.experts-layout{display:grid;grid-template-columns:minmax(220px,.75fr) minmax(500px,1.5fr) minmax(220px,.75fr);align-items:center;gap:clamp(20px,3vw,45px)}.trust-list{display:grid;gap:clamp(55px,8vw,105px);opacity:0}.is-visible .trust-list--left{animation:slideRight .7s .2s forwards}.is-visible .trust-list--right{animation:slideLeft .7s .2s forwards}.trust-list article{display:flex;align-items:flex-start;gap:13px}.trust-icon{display:grid;width:30px;height:30px;flex:0 0 30px;place-items:center;border-radius:50%;background:linear-gradient(135deg,rgba(0,224,171,.16),rgba(68,118,230,.14));color:#08786a;font-size:10px;font-weight:900}.trust-list h3{margin:3px 0 9px;font-size:15px;letter-spacing:-.025em}.trust-list p{margin:0;color:var(--muted);font-size:10px;line-height:1.55}.expert-orbit{position:relative;width:min(100%,610px);aspect-ratio:1;margin:auto;opacity:0;transform:scale(.94)}.is-visible .expert-orbit{animation:scaleIn .8s .12s forwards}.orbit{position:absolute;top:50%;left:50%;border:1px solid rgba(68,118,230,.14);border-radius:50%;transform:translate(-50%,-50%)}.orbit--outer{width:88%;height:88%;animation:spin 35s linear infinite}.orbit--inner{width:61%;height:61%;border-color:rgba(0,202,182,.2);animation:spinReverse 27s linear infinite}.orbit--outer::before,.orbit--inner::before{position:absolute;top:50%;left:-4px;width:8px;height:8px;border-radius:50%;background:var(--aqua);box-shadow:0 0 0 5px rgba(0,224,171,.11);content:""}.orbit-glow{position:absolute;top:50%;left:50%;width:52%;height:52%;border-radius:50%;background:radial-gradient(circle,rgba(124,230,210,.18),transparent 70%);transform:translate(-50%,-50%)}.brand-center{position:absolute;top:50%;left:50%;z-index:2;display:flex;width:230px;height:230px;align-items:center;justify-content:center;flex-direction:column;border:1px solid rgba(255,255,255,.9);border-radius:50%;background:rgba(255,255,255,.86);box-shadow:0 30px 70px -44px rgba(35,66,108,.55);transform:translate(-50%,-50%);backdrop-filter:blur(12px)}.brand-center svg{width:43px;margin-bottom:10px;fill:none;stroke:url(#none);stroke:var(--teal);stroke-width:2.4;stroke-linecap:round;stroke-linejoin:round}.brand-center strong{font-size:28px;letter-spacing:-.05em}.brand-center span{margin-top:4px;color:var(--muted);font-size:8px;text-transform:uppercase;letter-spacing:.1em}.profile{position:absolute;z-index:3;width:86px;height:86px;border:5px solid #fff;border-radius:50%;background:#d8f5ed;box-shadow:0 17px 30px -18px rgba(24,55,82,.6);transition:transform .3s}.profile:hover{z-index:5;transform:scale(1.12)}.profile img{width:100%;height:100%;border-radius:50%;object-fit:cover}.profile>span{position:absolute;top:50%;left:calc(100% + 8px);display:none;min-width:100px;padding:7px 9px;border:1px solid var(--line);border-radius:9px;background:#fff;box-shadow:0 12px 25px -18px rgba(25,49,80,.5);font-size:6px;transform:translateY(-50%)}.profile:hover>span{display:block}.profile>span b{display:block;margin-bottom:2px;font-size:8px}.profile--1{top:1%;left:39%}.profile--2{top:18%;left:3%}.profile--3{top:11%;right:5%}.profile--4{right:4%;bottom:16%}.profile--5{bottom:3%;left:39%}.profile--6{bottom:18%;left:3%}.profile--2,.profile--4,.profile--6{width:76px;height:76px}.verified{position:absolute;z-index:4;display:grid;width:28px;height:28px;place-items:center;border:5px solid #fff;border-radius:50%;background:linear-gradient(135deg,var(--aqua),var(--blue));box-shadow:0 10px 20px -13px rgba(26,59,100,.7);color:#fff;font-size:7px}.verified--1{top:17%;left:55%}.verified--2{top:49%;right:3%}.verified--3{bottom:6%;left:57%}.experts__footer{display:flex;align-items:center;justify-content:space-between;gap:25px;margin-top:55px;padding-top:26px;border-top:1px solid var(--line);opacity:0}.is-visible .experts__footer{animation:fade .6s .7s forwards}.experts__footer>span{display:flex;align-items:center;gap:9px;color:var(--muted);font-size:9px}.experts__footer>span i{width:7px;height:7px;border-radius:50%;background:var(--aqua);box-shadow:0 0 0 4px rgba(0,224,171,.11)}.experts__footer a{display:flex;align-items:center;gap:14px;color:var(--ink);font-size:10px;font-weight:750;text-decoration:none}.experts__footer a b{display:grid;width:33px;height:33px;place-items:center;border-radius:50%;background:linear-gradient(135deg,var(--blue),var(--indigo));color:#fff}@keyframes rise{to{opacity:1;transform:translateY(0)}}@keyframes scaleIn{to{opacity:1;transform:scale(1)}}@keyframes slideRight{from{transform:translateX(-20px)}to{opacity:1;transform:translateX(0)}}@keyframes slideLeft{from{transform:translateX(20px)}to{opacity:1;transform:translateX(0)}}@keyframes fade{to{opacity:1}}@keyframes spin{to{transform:translate(-50%,-50%) rotate(360deg)}}@keyframes spinReverse{to{transform:translate(-50%,-50%) rotate(-360deg)}}@media(max-width:1050px){.experts-layout{grid-template-columns:1fr 1.5fr}.trust-list--right{grid-column:1}.expert-orbit{grid-column:2;grid-row:1/span 2}.trust-list{gap:40px}}@media(max-width:760px){.experts{padding-inline:14px}.experts-layout{grid-template-columns:1fr}.expert-orbit{grid-column:1;grid-row:1;width:min(100%,530px)}.trust-list--left{grid-row:2}.trust-list--right{grid-column:1;grid-row:3}.trust-list{grid-template-columns:1fr 1fr;gap:20px}.experts__footer{align-items:flex-start;flex-direction:column}}@media(max-width:520px){.expert-orbit{margin-block:10px}.brand-center{width:150px;height:150px}.brand-center strong{font-size:21px}.profile{width:62px;height:62px}.profile--2,.profile--4,.profile--6{width:55px;height:55px}.verified{width:23px;height:23px}.trust-list{grid-template-columns:1fr}.experts__heading h2{font-size:38px}}@media(prefers-reduced-motion:reduce){.experts__heading,.trust-list,.expert-orbit,.experts__footer{opacity:1!important;transform:none!important;animation:none!important}.orbit{animation:none!important}.profile{transition:none!important}}
</style>
