<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const visible = ref(false)
let observer

const messages = [
  { initials: 'AM', name: 'Alex Morgan', subject: 'Q3 proposal draft', time: '9:41', unread: true },
  { initials: 'SK', name: 'Sarah Kim', subject: 'Meeting notes attached', time: '9:12', unread: true },
  { initials: 'JD', name: 'James Dean', subject: 'Invoice #2048 received', time: 'Yesterday', unread: false },
  { initials: 'RT', name: 'Rita Torres', subject: 'Re: onboarding checklist', time: 'Yesterday', unread: false }
]

onMounted(() => {
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
  <section ref="root" class="plans" :class="{ 'is-visible': visible }" aria-labelledby="plans-title">
    <div class="plans__inner">
      <header class="plans__header">
        <div class="plans__intro">
          <span class="plans__eyebrow">Email hosting</span>
          <h2 id="plans-title">
            Discover the
            <span class="highlight">freedom<svg class="squiggle" viewBox="0 0 220 26" aria-hidden="true"><path d="M4 18c30-22 60-22 90 0s60 22 90 0" /></svg></span>
            of email on your terms
          </h2>
        </div>
        <div class="plans__aside">
          <p>Get branded addresses, spam filtering, storage, and support — all in one scalable plan.</p>
          <a class="plans__cta" href="#get-started">
            Get started
            <span><svg viewBox="0 0 20 20"><path d="M5 10h10M11 6l4 4-4 4" /></svg></span>
          </a>
        </div>
      </header>

      <div class="plan-grid">
        <article class="plan-card plan-card--personal">
          <div class="plan-card__copy">
            <h3>Personal</h3>
            <p>The all-in-one plan for solo work. One branded address, everywhere access, a single flat price.</p>
          </div>

          <div class="inbox-mock" aria-hidden="true">
            <div class="inbox-mock__frame">
              <div class="inbox-mock__notch"></div>
              <div class="inbox-mock__head">
                <span>Inbox</span>
                <b>4 new</b>
              </div>
              <ul class="inbox-mock__list">
                <li v-for="m in messages" :key="m.initials" :class="{ 'is-unread': m.unread }">
                  <i>{{ m.initials }}</i>
                  <span>
                    <b>{{ m.name }}</b>
                    <small>{{ m.subject }}</small>
                  </span>
                  <em>{{ m.time }}</em>
                </li>
              </ul>
              <button class="inbox-mock__compose" type="button" aria-label="Compose">
                <svg viewBox="0 0 20 20"><path d="M10 4v12M4 10h12" /></svg>
              </button>
            </div>
          </div>

          <div class="plan-widget" aria-hidden="true">
            <div class="plan-widget__row">
              <span class="chip chip--accent"><svg viewBox="0 0 20 20"><path d="M10 4v12M4 10h12" /></svg></span>
              <span class="chip chip--stat">23<i>unread</i></span>
              <span class="chip"><svg viewBox="0 0 20 20"><path d="M4 8V6a3 3 0 0 1 3-3h6a3 3 0 0 1 3 3v2" /><rect x="3" y="8" width="14" height="9" rx="2" /></svg></span>
            </div>
            <div class="plan-widget__row">
              <span class="chip chip--group"><i>A</i><i>S</i><i>J</i></span>
              <span class="chip"><svg viewBox="0 0 20 20"><rect x="3" y="3" width="6" height="6" rx="1.4" /><rect x="11" y="3" width="6" height="6" rx="1.4" /><rect x="3" y="11" width="6" height="6" rx="1.4" /><rect x="11" y="11" width="6" height="6" rx="1.4" /></svg></span>
            </div>
          </div>

          <button class="plan-card__arrow" type="button" aria-label="Explore the Personal plan">
            <svg viewBox="0 0 20 20"><path d="M5 10h10M11 6l4 4-4 4" /></svg>
          </button>
        </article>

        <article class="plan-card plan-card--tint plan-card--business">
          <span class="plan-card__blob plan-card__blob--a"></span>
          <span class="plan-card__blob plan-card__blob--b"></span>
          <span class="plan-tag">Business</span>
        </article>

        <article class="plan-card plan-card--tint plan-card--team">
          <span class="plan-card__blob plan-card__blob--a"></span>
          <span class="plan-card__blob plan-card__blob--b"></span>
          <span class="plan-tag">Team</span>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.plans, .plans * { box-sizing: border-box; }

.plans {
  --ink: #0d0d0d;
  --green: #00cab6;
  --mint: #7ce6d2;
  --lavender: #aabff2;
  --muted: #6f746b;
  --paper: #ffffff;
  width: 100%;
  padding: clamp(48px, 6vw, 90px) clamp(18px, 4vw, 60px);
  background: var(--paper);
  color: var(--ink);
  font-family: var(--font-sans, "Plus Jakarta Sans", Arial, sans-serif);
}

.plans__inner { width: min(1280px, 100%); margin: 0 auto; }

/* --- header --- */
.plans__header {
  display: grid;
  grid-template-columns: 1.5fr 1fr;
  gap: 32px;
  align-items: end;
  margin-bottom: clamp(32px, 4vw, 52px);
  opacity: 0;
  transform: translateY(14px);
}
.is-visible .plans__header { animation: rise .6s forwards; }

.plans__eyebrow {
  display: inline-block;
  margin-bottom: 14px;
  color: var(--green);
  font-size: 12px;
  font-weight: 700;
  letter-spacing: .08em;
  text-transform: uppercase;
}

.plans__intro h2 {
  margin: 0;
  font-size: clamp(32px, 4vw, 54px);
  font-weight: 480;
  line-height: 1.06;
  letter-spacing: -.035em;
}

.highlight { position: relative; display: inline-block; }
.squiggle {
  position: absolute;
  left: 0;
  bottom: -.16em;
  width: 100%;
  height: .28em;
  fill: none;
  stroke: var(--green);
  stroke-width: 5;
  stroke-linecap: round;
}

.plans__aside {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 18px;
  padding-bottom: 6px;
}
.plans__aside p { margin: 0; max-width: 34ch; color: var(--muted); font-size: 14.5px; line-height: 1.55; }

.plans__cta {
  display: inline-flex;
  align-items: center;
  gap: 16px;
  padding: 8px 8px 8px 22px;
  border-radius: 999px;
  background: var(--ink);
  color: #fff;
  font-size: 13.5px;
  font-weight: 650;
  text-decoration: none;
  transition: gap .2s ease;
}
.plans__cta:hover { gap: 22px; }
.plans__cta span {
  display: grid;
  width: 34px;
  height: 34px;
  place-items: center;
  border-radius: 50%;
  background: #fff;
}
.plans__cta svg { width: 16px; fill: none; stroke: var(--ink); stroke-width: 2; stroke-linecap: round; stroke-linejoin: round; }

/* --- plan grid --- */
.plan-grid {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  gap: 16px;
  opacity: 0;
  transform: translateY(20px);
}
.is-visible .plan-grid { animation: rise .7s .12s forwards; }

.plan-card {
  position: relative;
  overflow: hidden;
  min-height: clamp(360px, 40vw, 480px);
  border-radius: 26px;
  transition: transform .3s ease;
}
.plan-card:hover { transform: translateY(-5px); }

/* --- personal card: illustrated inbox instead of a stock photo --- */
.plan-card--personal {
  background: linear-gradient(150deg, var(--mint) 0%, #eaf9d8 45%, var(--lavender) 100%);
}

.plan-card__copy {
  position: relative;
  z-index: 2;
  padding: clamp(24px, 2.6vw, 34px) clamp(24px, 2.6vw, 34px) 0;
  color: var(--ink);
}
.plan-card__copy h3 { margin: 0 0 10px; font-size: clamp(22px, 2.2vw, 28px); font-weight: 600; }
.plan-card__copy p { max-width: 26ch; margin: 0; font-size: 13.5px; line-height: 1.55; color: #3b3f36; }

.inbox-mock {
  position: absolute;
  right: clamp(10px, 3vw, 34px);
  bottom: 0;
  width: clamp(190px, 22vw, 250px);
  height: clamp(300px, 34vw, 400px);
  filter: drop-shadow(0 30px 45px rgba(13, 13, 13, .25));
  transition: transform .5s ease;
}
.plan-card--personal:hover .inbox-mock { transform: translateY(-6px); }

.inbox-mock__frame {
  position: relative;
  width: 100%;
  height: 100%;
  padding: 22px 14px 16px;
  border: 6px solid var(--ink);
  border-radius: 34px;
  background: #fff;
}
.inbox-mock__notch {
  position: absolute;
  top: 10px;
  left: 50%;
  width: 46px;
  height: 6px;
  border-radius: 999px;
  background: var(--ink);
  transform: translateX(-50%);
}
.inbox-mock__head {
  display: flex;
  align-items: baseline;
  justify-content: space-between;
  margin-bottom: 12px;
}
.inbox-mock__head span { font-size: 17px; font-weight: 700; }
.inbox-mock__head b { color: var(--green); font-size: 10px; font-weight: 700; }

.inbox-mock__list { display: grid; gap: 10px; padding: 0; margin: 0; list-style: none; }
.inbox-mock__list li {
  display: grid;
  grid-template-columns: 26px 1fr auto;
  align-items: center;
  gap: 8px;
}
.inbox-mock__list i {
  display: grid;
  width: 26px;
  height: 26px;
  place-items: center;
  border-radius: 50%;
  background: #eef0ea;
  font-style: normal;
  font-size: 9px;
  font-weight: 700;
  color: var(--muted);
}
.inbox-mock__list .is-unread i { background: var(--mint); color: #06231c; }
.inbox-mock__list span { display: flex; flex-direction: column; overflow: hidden; }
.inbox-mock__list b { overflow: hidden; font-size: 10px; font-weight: 700; text-overflow: ellipsis; white-space: nowrap; }
.inbox-mock__list small { overflow: hidden; color: var(--muted); font-size: 8.5px; text-overflow: ellipsis; white-space: nowrap; }
.inbox-mock__list em { font-style: normal; font-size: 7.5px; color: var(--muted); }
.inbox-mock__list .is-unread b { color: var(--ink); }

.inbox-mock__compose {
  position: absolute;
  right: 14px;
  bottom: 14px;
  display: grid;
  width: 34px;
  height: 34px;
  place-items: center;
  border: none;
  border-radius: 50%;
  background: var(--ink);
  cursor: pointer;
}
.inbox-mock__compose svg { width: 14px; fill: none; stroke: #fff; stroke-width: 2; stroke-linecap: round; }

.plan-widget {
  position: absolute;
  z-index: 2;
  left: clamp(20px, 2.4vw, 30px);
  bottom: clamp(20px, 2.4vw, 30px);
  display: grid;
  gap: 10px;
  padding: 14px;
  border-radius: 20px;
  background: rgba(255, 255, 255, .96);
  box-shadow: 0 20px 40px -22px rgba(13, 13, 13, .35);
}
.plan-widget__row { display: flex; gap: 10px; }
.chip {
  display: grid;
  place-items: center;
  width: 50px;
  height: 50px;
  border-radius: 14px;
  background: #f1f2ee;
  color: var(--ink);
}
.chip svg { width: 18px; fill: none; stroke: var(--ink); stroke-width: 1.8; stroke-linecap: round; stroke-linejoin: round; }
.chip--accent { background: linear-gradient(135deg, var(--mint), var(--green)); }
.chip--accent svg { stroke: #06231c; }
.chip--stat { flex-direction: column; gap: 1px; font-size: 15px; font-weight: 700; }
.chip--stat i { font-size: 8px; font-weight: 600; font-style: normal; color: var(--muted); }
.chip--group { display: flex; width: auto; padding: 0 10px 0 0; gap: 0; background: transparent; }
.chip--group i {
  display: grid;
  width: 26px;
  height: 26px;
  margin-left: -8px;
  place-items: center;
  border: 2px solid #fff;
  border-radius: 50%;
  background: var(--lavender);
  font-style: normal;
  font-size: 9px;
  font-weight: 700;
  color: var(--ink);
}
.chip--group i:first-child { margin-left: 0; }

.plan-card__arrow {
  position: absolute;
  z-index: 2;
  right: clamp(18px, 2vw, 26px);
  top: clamp(18px, 2vw, 26px);
  display: grid;
  width: 46px;
  height: 46px;
  place-items: center;
  border: none;
  border-radius: 50%;
  background: var(--ink);
  cursor: pointer;
  transition: transform .2s ease;
}
.plan-card__arrow:hover { transform: rotate(45deg); }
.plan-card__arrow svg { width: 18px; fill: none; stroke: #fff; stroke-width: 2; stroke-linecap: round; stroke-linejoin: round; }

/* --- business / team tinted cards --- */
.plan-card--tint { display: flex; align-items: flex-end; background: var(--ink); }
.plan-card__blob {
  position: absolute;
  width: 140%;
  aspect-ratio: 1;
  border-radius: 50%;
  filter: blur(40px);
  opacity: .8;
  animation: drift 14s ease-in-out infinite;
}
.plan-card--business .plan-card__blob--a { top: -35%; left: -30%; background: radial-gradient(circle, var(--mint), transparent 65%); }
.plan-card--business .plan-card__blob--b { bottom: -40%; right: -25%; background: radial-gradient(circle, var(--green), transparent 65%); animation-delay: -6s; }
.plan-card--team .plan-card__blob--a { top: -35%; right: -30%; background: radial-gradient(circle, var(--lavender), transparent 65%); }
.plan-card--team .plan-card__blob--b { bottom: -40%; left: -25%; background: radial-gradient(circle, #6f83d6, transparent 65%); animation-delay: -6s; }

.plan-tag {
  position: relative;
  z-index: 2;
  margin: clamp(20px, 2.4vw, 28px);
  writing-mode: vertical-rl;
  transform: rotate(180deg);
  color: #fff;
  font-size: clamp(24px, 2.4vw, 32px);
  font-weight: 650;
  letter-spacing: -.02em;
}

@keyframes rise { to { opacity: 1; transform: translateY(0); } }
@keyframes drift {
  0%, 100% { transform: translate(0, 0) scale(1); }
  50% { transform: translate(4%, -3%) scale(1.06); }
}

@media (max-width: 980px) {
  .plans__header { grid-template-columns: 1fr; align-items: start; }
  .plan-grid { grid-template-columns: 1fr 1fr; }
  .plan-card--personal { grid-column: 1 / -1; }
}

@media (max-width: 620px) {
  .plan-grid { grid-template-columns: 1fr; }
  .plan-card { min-height: 340px; }
  .inbox-mock { position: static; margin: 18px auto 0; }
  .plan-widget { position: static; margin: 14px clamp(24px, 2.6vw, 34px) clamp(24px, 2.6vw, 34px); }
  .plan-card__arrow { top: clamp(18px, 2vw, 26px); }
}

@media (prefers-reduced-motion: reduce) {
  .plans__header, .plan-grid, .inbox-mock { opacity: 1 !important; transform: none !important; animation: none !important; }
  .plan-card__blob { animation: none !important; }
}
</style>
