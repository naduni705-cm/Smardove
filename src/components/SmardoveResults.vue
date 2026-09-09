<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const visible = ref(false)
let observer

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
  }, { threshold: 0.2 })

  if (root.value) observer.observe(root.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section ref="root" class="results" :class="{ 'is-visible': visible }" aria-labelledby="results-title">
    <div class="results__glow results__glow--aqua" aria-hidden="true" />
    <div class="results__glow results__glow--blue" aria-hidden="true" />

    <div class="results__inner">
      <header class="results__heading">
        <span class="eyebrow"><i /> Proven performance</span>
        <h2 id="results-title">Businesses trust Smardove—<mark>and the results show.</mark></h2>
        <p>Reliable, secure business email built to keep teams connected and every message moving.</p>
      </header>

      <div class="results-grid">
        <article class="result-card result-card--delivery" style="--delay:.08s">
          <span class="result-card__label">DELIVERABILITY</span>
          <strong>99.98%</strong>
          <p>successful email delivery across protected business mailboxes</p>

          <svg class="trend" viewBox="0 0 180 95" aria-hidden="true">
            <defs>
              <linearGradient id="trendFill" x1="0" y1="0" x2="0" y2="1">
                <stop offset="0" stop-color="#4476e6" stop-opacity=".25" />
                <stop offset="1" stop-color="#4476e6" stop-opacity="0" />
              </linearGradient>
            </defs>
            <path d="M5 87 31 65 55 74 80 44 105 52 134 18 175 7V94H5Z" fill="url(#trendFill)" />
            <path d="M5 87 31 65 55 74 80 44 105 52 134 18 175 7" fill="none" stroke="#4476e6" stroke-width="4" stroke-linecap="round" stroke-linejoin="round" />
            <circle cx="175" cy="7" r="6" fill="#fff" stroke="#4476e6" stroke-width="4" />
          </svg>
        </article>

        <article class="result-card result-card--customers" style="--delay:.16s">
          <span class="result-card__label">CUSTOMER GROWTH</span>
          <div class="result-card__arrow">↑</div>
          <h3>Growing teams</h3>
          <div class="customer-row">
            <div class="avatars" aria-hidden="true">
              <i>AM</i><i>JD</i><i>SK</i>
            </div>
            <strong>12K+</strong>
          </div>
          <p>mailboxes securely managed</p>
        </article>

        <article class="result-card result-card--rating" style="--delay:.24s">
          <div class="stars" aria-label="Five star rating">★★★★★</div>
          <strong>4.9/5</strong>
          <p>average customer rating</p>
        </article>

        <article class="result-card result-card--security" style="--delay:.32s">
          <span class="result-card__label">SECURITY</span>
          <strong>2.4M+</strong>
          <p>threats and unwanted messages blocked</p>

          <div class="shield" aria-hidden="true">
            <svg viewBox="0 0 80 92">
              <path d="M40 4 72 16v25c0 22-13 37-32 47C21 78 8 63 8 41V16L40 4Z" />
              <path d="m25 44 10 10 21-25" />
            </svg>
          </div>
        </article>

        <article class="result-card result-card--support" style="--delay:.4s">
          <h3>Business results:</h3>
          <div class="support-grid">
            <div><strong>24/7</strong><span>expert support</span></div>
            <div><strong>&lt;1 sec</strong><span>smart routing</span></div>
            <div><strong>500GB</strong><span>mailbox storage</span></div>
          </div>
        </article>
      </div>

      <footer class="results__footer">
        <span><i>✓</i> Secure email for businesses of every size</span>
        <a href="https://smardove.com/pricing/">Explore email packages <b>→</b></a>
      </footer>
    </div>
  </section>
</template>

<style scoped>
.results,.results *{box-sizing:border-box}.results{--ink:#0d0d0d;--charcoal:#20242b;--muted:#737985;--aqua:#00e0ab;--teal:#00cab6;--blue:#4476e6;--indigo:#4864f0;--soft-aqua:#7ce6d2;--periwinkle:#aabff2;--ice:#f7f9fc;--line:#e6eaf0;position:relative;isolation:isolate;overflow:hidden;width:100%;padding:clamp(75px,8vw,125px) clamp(16px,4vw,64px);background:#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.results__inner{width:min(1320px,100%);margin:auto}.results__glow{position:absolute;z-index:-1;width:390px;height:390px;border-radius:50%;filter:blur(130px);opacity:.09}.results__glow--aqua{top:-220px;left:-150px;background:var(--aqua)}.results__glow--blue{right:-190px;bottom:-220px;background:var(--blue)}.results__heading{max-width:800px;margin:0 auto clamp(48px,5vw,72px);text-align:center;opacity:0;transform:translateY(20px)}.is-visible .results__heading{animation:rise .7s forwards}.eyebrow{display:inline-flex;align-items:center;gap:9px;margin-bottom:18px;padding:8px 14px;border:1px solid var(--line);border-radius:99px;color:#53606b;font-size:9px;font-weight:800;letter-spacing:.11em;text-transform:uppercase}.eyebrow i{width:8px;height:8px;border-radius:50%;background:linear-gradient(135deg,var(--aqua),var(--teal));box-shadow:0 0 0 4px rgba(0,224,171,.12)}.results__heading h2{margin:0;font-size:clamp(37px,4.8vw,66px);font-weight:420;line-height:1.04;letter-spacing:-.052em}.results__heading mark{padding:0 .03em;background:linear-gradient(transparent 70%,rgba(170,191,242,.76) 70%);color:inherit}.results__heading p{max-width:600px;margin:19px auto 0;color:var(--muted);font-size:13px;line-height:1.7}.results-grid{display:grid;grid-template-columns:1.05fr 1.05fr .82fr 1.12fr 1.1fr;align-items:end;gap:14px}.result-card{position:relative;overflow:hidden;border:1px solid rgba(255,255,255,.82);border-radius:24px;padding:22px;background:var(--ice);box-shadow:0 26px 58px -44px rgba(31,54,84,.68);opacity:0;transform:translateY(25px);transition:transform .3s,box-shadow .3s}.is-visible .result-card{animation:rise .65s var(--delay) forwards}.result-card:hover{transform:translateY(-7px);box-shadow:0 32px 65px -39px rgba(31,54,84,.72)}.result-card__label{display:block;margin-bottom:15px;color:#3563b9;font-size:7px;font-weight:850;letter-spacing:.12em}.result-card>strong{display:block;font-size:clamp(26px,2.6vw,41px);font-weight:650;letter-spacing:-.055em}.result-card p{margin:8px 0 0;color:#596673;font-size:9px;line-height:1.5}.result-card--delivery{height:285px;background:linear-gradient(155deg,#dff9f2,#c5f1e6)}.trend{position:absolute;right:18px;bottom:20px;left:18px;width:calc(100% - 36px);height:92px}.result-card--customers{height:245px;background:linear-gradient(155deg,#c9f5eb,#8ee5d5)}.result-card__arrow{position:absolute;top:18px;right:18px;display:grid;width:28px;height:28px;place-items:center;border:1px solid rgba(13,13,13,.12);border-radius:50%;font-size:13px}.result-card h3{margin:0;font-size:15px;line-height:1.2;letter-spacing:-.03em}.customer-row{position:absolute;right:20px;bottom:42px;left:20px;display:flex;align-items:center;justify-content:space-between}.customer-row strong{font-size:22px;letter-spacing:-.04em}.avatars{display:flex}.avatars i{display:grid;width:31px;height:31px;place-items:center;margin-right:-8px;border:3px solid #a9eadf;border-radius:50%;background:#fff;color:#246456;font-size:6px;font-style:normal;font-weight:800}.avatars i:nth-child(2){background:#dbe5ff;color:#365aa5}.result-card--customers>p{position:absolute;right:20px;bottom:20px}.result-card--rating{height:175px;text-align:center;background:#fff}.stars{margin:15px 0 13px;color:var(--blue);font-size:10px;letter-spacing:2px}.result-card--rating>strong{font-size:34px}.result-card--rating p{text-align:center}.result-card--security{height:255px;background:linear-gradient(155deg,#dfe7ff,#aabff2)}.shield{position:absolute;right:-7px;bottom:-14px;width:105px;transform:rotate(8deg)}.shield svg{width:100%}.shield path:first-child{fill:#fff;filter:drop-shadow(0 12px 15px rgba(44,72,120,.16))}.shield path:last-child{fill:none;stroke:var(--blue);stroke-width:7;stroke-linecap:round;stroke-linejoin:round}.result-card--support{height:285px;background:linear-gradient(155deg,#ddf8f1,#cce1ff)}.result-card--support h3{max-width:120px;font-size:17px}.support-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:8px;margin-top:25px}.support-grid div{min-height:70px;padding:12px 10px;border:1px solid rgba(255,255,255,.78);border-radius:13px;background:rgba(255,255,255,.58)}.support-grid div:last-child{grid-column:1/-1}.support-grid strong{display:block;font-size:14px}.support-grid span{display:block;margin-top:4px;color:#65727e;font-size:7px}.results__footer{display:flex;align-items:center;justify-content:space-between;gap:25px;margin-top:30px;padding-top:26px;border-top:1px solid var(--line);opacity:0}.is-visible .results__footer{animation:fade .6s .65s forwards}.results__footer>span{display:flex;align-items:center;gap:9px;color:var(--muted);font-size:9px}.results__footer>span i{display:grid;width:24px;height:24px;place-items:center;border-radius:50%;background:rgba(0,202,182,.13);color:#08786a;font-style:normal}.results__footer a{display:flex;align-items:center;gap:14px;color:var(--ink);font-size:10px;font-weight:750;text-decoration:none}.results__footer a b{display:grid;width:33px;height:33px;place-items:center;border-radius:50%;background:linear-gradient(135deg,var(--blue),var(--indigo));color:#fff}@keyframes rise{to{opacity:1;transform:translateY(0)}}@keyframes fade{to{opacity:1}}@media(max-width:1050px){.results-grid{grid-template-columns:repeat(3,1fr)}.result-card{height:245px}.result-card--support{grid-column:span 2}}@media(max-width:680px){.results{padding-inline:14px}.results-grid{grid-template-columns:repeat(2,1fr)}.result-card--support{grid-column:span 2}.results__footer{align-items:flex-start;flex-direction:column}}@media(max-width:430px){.results-grid{grid-template-columns:1fr}.result-card,.result-card--support{grid-column:auto;height:230px}.result-card--rating{height:170px}.results__heading h2{font-size:38px}}@media(prefers-reduced-motion:reduce){.results__heading,.result-card,.results__footer{opacity:1!important;transform:none!important;animation:none!important}.result-card{transition:none!important}}
</style>
