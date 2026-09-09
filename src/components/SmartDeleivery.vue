<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const section = ref(null)
const isVisible = ref(false)
let observer

const activity = [
  { day: 'Mon', value: 46 },
  { day: 'Tue', value: 63 },
  { day: 'Wed', value: 57 },
  { day: 'Thu', value: 82 },
  { day: 'Fri', value: 94 },
  { day: 'Sat', value: 72 },
  { day: 'Sun', value: 86 }
]

onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        isVisible.value = true
        observer.disconnect()
      }
    },
    { threshold: 0.18 }
  )

  if (section.value) observer.observe(section.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section
    ref="section"
    class="smart-delivery"
    :class="{ 'is-visible': isVisible }"
    aria-labelledby="smart-delivery-title"
  >
    <div class="smart-delivery__dots" aria-hidden="true" />

    <div class="smart-delivery__inner">
      <header class="smart-delivery__header">
        <span class="feature-pill">
          <svg viewBox="0 0 18 18" aria-hidden="true">
            <path d="M9 1.5v3M9 13.5v3M1.5 9h3M13.5 9h3M3.7 3.7l2.1 2.1M12.2 12.2l2.1 2.1M14.3 3.7l-2.1 2.1M5.8 12.2l-2.1 2.1" />
          </svg>
          Features
        </span>

        <h2 id="smart-delivery-title">
          Smarter email delivery for<br />
          <mark>modern growing businesses</mark>
        </h2>

        <p>
          Professional business email with reliable delivery, powerful protection,
          and simple tools your whole team can use.
        </p>
      </header>

      <article class="feature-card">
        <div class="feature-card__glow feature-card__glow--yellow" aria-hidden="true" />
        <div class="feature-card__glow feature-card__glow--green" aria-hidden="true" />

        <div class="feature-card__copy">
          <span class="feature-icon" aria-hidden="true">
            <svg viewBox="0 0 28 28">
              <path d="M5 9.5h18v13H5z" />
              <path d="m6 11 8 6 8-6" />
              <path d="M10 6h8M12.5 3h3" />
            </svg>
          </span>

          <span class="feature-card__eyebrow">Intelligent delivery</span>
          <h3>Send every important email with confidence</h3>
          <p>
            Smardove automatically protects your messages, monitors delivery health,
            and helps your team maintain professional communication without complexity.
          </p>

          <div class="feature-list">
            <span><i>✓</i> Advanced spam protection</span>
            <span><i>✓</i> Real-time delivery insights</span>
            <span><i>✓</i> Reliable business mailboxes</span>
          </div>

          <a href="https://smardove.com/features/">
            Explore Features
            <span aria-hidden="true">↗</span>
          </a>
        </div>

        <div class="mail-visual" aria-label="Smardove email delivery dashboard preview">
          <div class="mail-window">
            <header class="mail-window__bar">
              <span class="window-dots" aria-hidden="true"><i /><i /><i /></span>
              <span class="window-address">
                <svg viewBox="0 0 18 18" aria-hidden="true">
                  <rect x="3" y="5" width="12" height="9" rx="2" />
                  <path d="m4 7 5 3.5L14 7" />
                </svg>
                app.smardove.com
              </span>
              <span class="window-status"><i /> Secure</span>
            </header>

            <div class="mail-window__body">
              <aside class="mail-sidebar" aria-hidden="true">
                <span class="brand-mark">S</span>
                <i class="is-active" /><i /><i /><i />
                <span class="profile-dot">NA</span>
              </aside>

              <div class="mail-main">
                <header class="mail-main__header">
                  <div>
                    <small>Good morning, Naduni</small>
                    <h4>Delivery overview</h4>
                  </div>
                  <button type="button" aria-label="Dashboard notifications">
                    <svg viewBox="0 0 20 20" aria-hidden="true">
                      <path d="M5.5 8.5a4.5 4.5 0 0 1 9 0v3l1.5 2H4l1.5-2Z" />
                      <path d="M8.5 16h3" />
                    </svg>
                  </button>
                </header>

                <div class="summary-grid">
                  <div><span>Delivered</span><strong>24,892</strong><small>↗ 18.4%</small></div>
                  <div><span>Protected</span><strong>99.9%</strong><small>All secure</small></div>
                  <div><span>Active users</span><strong>186</strong><small>+12 this month</small></div>
                </div>

                <div class="activity-card">
                  <header>
                    <div><small>Weekly activity</small><strong>Message delivery</strong></div>
                    <span>Last 7 days⌄</span>
                  </header>

                  <div class="bar-chart" aria-hidden="true">
                    <span class="grid-line grid-line--one" />
                    <span class="grid-line grid-line--two" />
                    <span class="grid-line grid-line--three" />
                    <div v-for="(item, index) in activity" :key="item.day" class="bar-item">
                      <span
                        class="bar-item__fill"
                        :class="{ 'is-highlighted': index === 4 }"
                        :style="{ '--height': `${item.value}%`, '--delay': `${index * 85}ms` }"
                      />
                      <small>{{ item.day }}</small>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <div class="floating-card floating-card--delivery">
            <span class="floating-card__icon">
              <svg viewBox="0 0 24 24" aria-hidden="true">
                <path d="M4 7h16v11H4z" />
                <path d="m5 9 7 5 7-5" />
              </svg>
            </span>
            <span><strong>Email delivered</strong><small>sales@yourbrand.com</small></span>
            <i>✓</i>
          </div>

          <div class="floating-card floating-card--security">
            <span class="shield">
              <svg viewBox="0 0 24 24" aria-hidden="true">
                <path d="M12 3 5 6v5c0 4.5 2.6 7.8 7 10 4.4-2.2 7-5.5 7-10V6Z" />
                <path d="m9 12 2 2 4-5" />
              </svg>
            </span>
            <span><strong>Threat blocked</strong><small>Mailbox protected</small></span>
          </div>
        </div>
      </article>
    </div>
  </section>
</template>

<style scoped>
.smart-delivery,
.smart-delivery * {
  box-sizing: border-box;
}

.smart-delivery {
  --ink: #0d0d0d;
  --muted: #737970;
  --line: #e4e9df;
  --green: #c9e6a8;
  --green-deep: #749c51;
  --yellow: #f3ee9a;
  position: relative;
  isolation: isolate;
  overflow: hidden;
  width: 100%;
  padding: clamp(76px, 8vw, 128px) clamp(15px, 3vw, 46px) clamp(64px, 7vw, 105px);
  background: #fff;
  color: var(--ink);
  font-family: var(--font-sans, "Plus Jakarta Sans", Arial, sans-serif);
}

.smart-delivery__dots {
  position: absolute;
  z-index: -2;
  top: 0;
  right: 0;
  left: 0;
  height: min(49%, 520px);
  background-image: radial-gradient(circle, rgba(73, 82, 68, .22) 2.1px, transparent 2.2px);
  background-position: center top;
  background-size: 50px 50px;
  mask-image: linear-gradient(#000 0 72%, transparent 100%);
  -webkit-mask-image: linear-gradient(#000 0 72%, transparent 100%);
}

.smart-delivery__inner {
  width: min(1220px, 100%);
  margin: 0 auto;
}

.smart-delivery__header {
  max-width: 870px;
  margin: 0 auto clamp(65px, 8vw, 104px);
  text-align: center;
  opacity: 0;
  transform: translateY(25px);
}

.is-visible .smart-delivery__header {
  animation: reveal-up .8s cubic-bezier(.2, .8, .2, 1) forwards;
}

.feature-pill {
  display: inline-flex;
  min-height: 33px;
  align-items: center;
  gap: 6px;
  margin-bottom: 23px;
  padding: 6px 14px;
  border: 1px solid rgba(119, 153, 89, .17);
  border-radius: 999px;
  background: linear-gradient(105deg, rgba(201, 230, 168, .9), rgba(243, 238, 154, .92));
  box-shadow: 0 8px 26px rgba(78, 103, 58, .08);
  font-size: 12px;
  font-weight: 700;
}

.feature-pill svg {
  width: 13px;
  fill: none;
  stroke: currentColor;
  stroke-linecap: round;
}

.smart-delivery h2 {
  margin: 0;
  font-family: var(--font-display, var(--font-sans));
  font-size: clamp(36px, 4.6vw, 68px);
  font-weight: 380;
  line-height: 1.07;
  letter-spacing: -.045em;
}

.smart-delivery h2 mark {
  padding: 0 2px;
  background: linear-gradient(transparent 63%, var(--yellow) 63%);
  color: inherit;
}

.smart-delivery__header > p {
  max-width: 680px;
  margin: 21px auto 0;
  color: var(--muted);
  font-size: clamp(13px, 1.2vw, 16px);
  line-height: 1.65;
}

.feature-card {
  position: relative;
  display: grid;
  min-height: 580px;
  grid-template-columns: .84fr 1.16fr;
  align-items: center;
  gap: clamp(45px, 6vw, 92px);
  overflow: hidden;
  padding: clamp(48px, 6vw, 82px) clamp(34px, 6vw, 86px);
  border: 1px solid rgba(182, 207, 158, .42);
  border-radius: clamp(25px, 3vw, 39px);
  background:
    linear-gradient(130deg, rgba(243, 238, 154, .62), rgba(231, 242, 213, .8) 46%, rgba(201, 230, 168, .73));
  box-shadow: 0 35px 90px -57px rgba(42, 63, 27, .38), inset 0 1px 0 rgba(255,255,255,.8);
  opacity: 0;
  transform: translateY(42px) scale(.985);
}

.is-visible .feature-card {
  animation: card-reveal .9s .18s cubic-bezier(.2, .8, .2, 1) forwards;
}

.feature-card::before {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255,255,255,.2) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,.2) 1px, transparent 1px);
  background-size: 42px 42px;
  mask-image: linear-gradient(90deg, transparent, #000 55%, transparent);
  content: "";
  pointer-events: none;
}

.feature-card__glow {
  position: absolute;
  width: 380px;
  height: 380px;
  border-radius: 50%;
  filter: blur(90px);
  opacity: .42;
  pointer-events: none;
}

.feature-card__glow--yellow { bottom: -240px; left: 8%; background: var(--yellow); }
.feature-card__glow--green { top: -250px; right: 7%; background: var(--green); }

.feature-card__copy {
  position: relative;
  z-index: 2;
}

.feature-icon {
  display: grid;
  width: 65px;
  height: 65px;
  margin-bottom: 28px;
  place-items: center;
  border: 1px solid rgba(255,255,255,.9);
  border-radius: 17px;
  background: rgba(255,255,255,.84);
  box-shadow: 0 17px 40px rgba(58, 78, 42, .11), inset 0 1px 0 #fff;
}

.feature-icon svg {
  width: 29px;
  fill: none;
  stroke: var(--ink);
  stroke-width: 1.65;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.feature-card__eyebrow {
  display: block;
  margin-bottom: 12px;
  color: #5f7d46;
  font-size: 10px;
  font-weight: 800;
  letter-spacing: .13em;
  text-transform: uppercase;
}

.feature-card h3 {
  max-width: 480px;
  margin: 0;
  font-family: var(--font-display, var(--font-sans));
  font-size: clamp(32px, 3.5vw, 52px);
  font-weight: 410;
  line-height: 1.08;
  letter-spacing: -.045em;
}

.feature-card__copy > p {
  max-width: 470px;
  margin: 20px 0 24px;
  color: #626a5e;
  font-size: 14px;
  line-height: 1.68;
}

.feature-list {
  display: grid;
  gap: 10px;
  margin-bottom: 30px;
  color: #4d5549;
  font-size: 11px;
  font-weight: 650;
}

.feature-list span {
  display: flex;
  align-items: center;
  gap: 9px;
}

.feature-list i {
  display: grid;
  width: 20px;
  height: 20px;
  place-items: center;
  border-radius: 50%;
  background: rgba(255,255,255,.72);
  color: #53713c;
  font-style: normal;
  font-size: 8px;
  font-weight: 900;
}

.feature-card__copy > a {
  display: inline-flex;
  min-height: 48px;
  align-items: center;
  gap: 18px;
  padding: 10px 12px 10px 21px;
  border-radius: 999px;
  background: var(--ink);
  color: #fff;
  font-size: 12px;
  font-weight: 700;
  text-decoration: none;
  transition: transform .25s ease, box-shadow .25s ease;
}

.feature-card__copy > a span {
  display: grid;
  width: 28px;
  height: 28px;
  place-items: center;
  border-radius: 50%;
  background: var(--yellow);
  color: var(--ink);
  font-size: 14px;
}

.feature-card__copy > a:hover {
  box-shadow: 0 14px 30px rgba(13,13,13,.19);
  transform: translateY(-3px);
}

.feature-card__copy > a:focus-visible {
  outline: 3px solid #fff;
  outline-offset: 3px;
}

.mail-visual {
  position: relative;
  z-index: 2;
  min-height: 460px;
  perspective: 1200px;
}

.mail-window {
  position: absolute;
  top: 15px;
  right: 0;
  width: min(100%, 600px);
  min-height: 415px;
  overflow: hidden;
  border: 1px solid rgba(255,255,255,.92);
  border-radius: 24px;
  background: rgba(255,255,255,.92);
  box-shadow: 0 35px 72px rgba(48, 69, 34, .19), inset 0 1px 0 #fff;
  backdrop-filter: blur(18px);
  transform: rotateY(-3deg) rotateX(1.5deg);
  transform-origin: center;
  animation: window-float 6.5s ease-in-out infinite;
}

.mail-window__bar {
  display: grid;
  min-height: 53px;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  gap: 17px;
  padding: 0 18px;
  border-bottom: 1px solid #edf0ea;
  background: rgba(255,255,255,.93);
}

.window-dots { display: flex; gap: 5px; }
.window-dots i { width: 7px; height: 7px; border-radius: 50%; background: #dfe4dc; }
.window-dots i:first-child { background: var(--yellow); }
.window-dots i:nth-child(2) { background: var(--green); }

.window-address {
  display: flex;
  width: min(255px, 100%);
  min-height: 28px;
  align-items: center;
  gap: 7px;
  justify-self: center;
  padding: 5px 10px;
  border-radius: 8px;
  background: #f6f8f4;
  color: #8a9086;
  font-size: 8px;
}

.window-address svg {
  width: 12px;
  fill: none;
  stroke: #798173;
  stroke-width: 1.4;
}

.window-status {
  display: flex;
  align-items: center;
  gap: 5px;
  color: #6f776a;
  font-size: 8px;
  font-weight: 700;
}

.window-status i { width: 6px; height: 6px; border-radius: 50%; background: #8abf62; box-shadow: 0 0 0 4px rgba(201,230,168,.45); }

.mail-window__body {
  display: grid;
  min-height: 362px;
  grid-template-columns: 56px 1fr;
}

.mail-sidebar {
  display: flex;
  align-items: center;
  flex-direction: column;
  gap: 20px;
  padding: 16px 0;
  border-right: 1px solid #edf0ea;
  background: #fbfcfa;
}

.brand-mark,
.profile-dot {
  display: grid;
  width: 27px;
  height: 27px;
  place-items: center;
  border-radius: 8px;
  background: var(--ink);
  color: #fff;
  font-size: 9px;
  font-weight: 800;
}

.mail-sidebar > i {
  position: relative;
  width: 15px;
  height: 12px;
  border: 1.5px solid #b6bdb2;
  border-radius: 4px;
}

.mail-sidebar > i.is-active { border-color: #668c48; background: var(--green); }
.mail-sidebar > i.is-active::before { position: absolute; left: -12px; width: 3px; height: 12px; border-radius: 0 3px 3px 0; background: #779e58; content: ""; }
.profile-dot { margin-top: auto; border-radius: 50%; background: var(--yellow); color: #53572f; font-size: 6px; }

.mail-main { padding: 25px clamp(18px, 2.5vw, 31px); }

.mail-main__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.mail-main__header small { color: #92998e; font-size: 8px; }
.mail-main__header h4 { margin: 4px 0 0; font-size: clamp(16px, 1.7vw, 21px); letter-spacing: -.035em; }
.mail-main__header button { display: grid; width: 30px; height: 30px; place-items: center; border: 1px solid #e8ece5; border-radius: 9px; background: #fff; }
.mail-main__header button svg { width: 15px; fill: none; stroke: #7c8477; stroke-width: 1.5; }

.summary-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 9px;
  margin-top: 23px;
}

.summary-grid > div {
  min-width: 0;
  padding: 13px;
  border: 1px solid #edf0ea;
  border-radius: 12px;
  background: #fff;
}

.summary-grid span,
.summary-grid strong,
.summary-grid small { display: block; }
.summary-grid span { overflow: hidden; color: #858c81; font-size: 7px; text-overflow: ellipsis; white-space: nowrap; }
.summary-grid strong { margin: 6px 0; font-size: clamp(13px, 1.4vw, 18px); letter-spacing: -.035em; }
.summary-grid small { color: #668b4b; font-size: 6px; font-weight: 700; }

.activity-card {
  margin-top: 12px;
  padding: 16px 17px 12px;
  border: 1px solid #edf0ea;
  border-radius: 14px;
  background: #fff;
}

.activity-card > header { display: flex; align-items: center; justify-content: space-between; }
.activity-card > header div small,
.activity-card > header div strong { display: block; }
.activity-card > header div small { color: #91978d; font-size: 6px; }
.activity-card > header div strong { margin-top: 4px; font-size: 9px; }
.activity-card > header > span { padding: 5px 8px; border: 1px solid #e9ede6; border-radius: 7px; color: #858c80; font-size: 6px; }

.bar-chart {
  position: relative;
  display: flex;
  height: 140px;
  align-items: flex-end;
  justify-content: space-between;
  gap: 7px;
  margin-top: 11px;
  padding: 10px 4px 19px;
}

.grid-line { position: absolute; right: 0; left: 0; height: 1px; background: repeating-linear-gradient(90deg,#e8ece5 0 4px,transparent 4px 8px); }
.grid-line--one { top: 18%; }.grid-line--two { top: 48%; }.grid-line--three { top: 77%; }

.bar-item { position: relative; z-index: 1; display: flex; width: 12%; height: 100%; align-items: center; flex-direction: column; justify-content: flex-end; }
.bar-item__fill { width: min(31px, 76%); height: var(--height); border-radius: 7px 7px 3px 3px; background: linear-gradient(180deg,#dcead0,#bddaa3); box-shadow: inset 0 1px 0 rgba(255,255,255,.7); transform: scaleY(0); transform-origin: bottom; animation: grow-bar .8s var(--delay) cubic-bezier(.2,.85,.25,1) forwards; }
.bar-item__fill.is-highlighted { background: linear-gradient(180deg,var(--yellow),#ddd366); box-shadow: 0 7px 16px rgba(160,151,56,.14),inset 0 1px 0 #fff; }
.bar-item small { position: absolute; bottom: -14px; color: #969c92; font-size: 6px; }

.floating-card {
  position: absolute;
  z-index: 5;
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 11px 13px;
  border: 1px solid rgba(255,255,255,.9);
  border-radius: 15px;
  background: rgba(255,255,255,.94);
  box-shadow: 0 19px 44px rgba(39,57,27,.17);
  backdrop-filter: blur(14px);
}

.floating-card--delivery { top: -8px; right: -22px; animation: float-card 5s ease-in-out infinite; }
.floating-card--security { bottom: 2px; left: -30px; animation: float-card 5.8s .6s ease-in-out infinite reverse; }
.floating-card > span:nth-child(2) strong,
.floating-card > span:nth-child(2) small { display: block; }
.floating-card > span:nth-child(2) strong { font-size: 9px; }
.floating-card > span:nth-child(2) small { margin-top: 3px; color: #899084; font-size: 6px; }
.floating-card > i { display: grid; width: 19px; height: 19px; margin-left: 7px; place-items: center; border-radius: 50%; background: var(--green); color: #466331; font-style: normal; font-size: 8px; font-weight: 900; }

.floating-card__icon,
.shield { display: grid; width: 32px; height: 32px; flex: 0 0 auto; place-items: center; border-radius: 9px; background: var(--yellow); }
.floating-card__icon svg,
.shield svg { width: 17px; fill: none; stroke: var(--ink); stroke-width: 1.6; stroke-linecap: round; stroke-linejoin: round; }
.shield { border-radius: 50%; background: var(--green); }

@keyframes reveal-up { to { opacity: 1; transform: translateY(0); } }
@keyframes card-reveal { to { opacity: 1; transform: translateY(0) scale(1); } }
@keyframes grow-bar { to { transform: scaleY(1); } }
@keyframes float-card { 0%,100% { transform: translateY(0); } 50% { transform: translateY(-9px); } }
@keyframes window-float { 0%,100% { transform: rotateY(-3deg) rotateX(1.5deg) translateY(0); } 50% { transform: rotateY(-1deg) rotateX(.5deg) translateY(-8px); } }

@media (max-width: 930px) {
  .feature-card { grid-template-columns: 1fr; gap: 55px; }
  .feature-card__copy { max-width: 650px; }
  .mail-visual { width: min(680px,100%); margin: 0 auto; }
}

@media (max-width: 620px) {
  .smart-delivery { padding-inline: 13px; }
  .smart-delivery h2 br { display: none; }
  .smart-delivery__dots { background-size: 34px 34px; }
  .feature-card { min-height: auto; padding: 40px 20px 35px; border-radius: 25px; }
  .feature-card h3 { font-size: clamp(31px, 9.5vw, 43px); }
  .mail-visual { min-height: 380px; }
  .mail-window { min-height: 345px; transform: none; }
  .mail-window__bar { grid-template-columns: auto 1fr; }
  .window-status { display: none; }
  .mail-window__body { min-height: 292px; grid-template-columns: 43px 1fr; }
  .mail-sidebar { gap: 17px; }
  .mail-main { padding: 19px 12px; }
  .summary-grid { grid-template-columns: repeat(2,1fr); }
  .summary-grid > div:last-child { display: none; }
  .bar-chart { height: 113px; }
  .floating-card--delivery { top: -9px; right: -5px; }
  .floating-card--delivery > span:nth-child(2) { display: none; }
  .floating-card--delivery > i { margin-left: 0; }
  .floating-card--security { bottom: -4px; left: -5px; }
}

@media (prefers-reduced-motion: reduce) {
  .smart-delivery__header,
  .feature-card { opacity: 1 !important; transform: none !important; animation: none !important; }
  .mail-window,
  .floating-card,
  .bar-item__fill { animation: none !important; }
  .bar-item__fill { transform: scaleY(1); }
}
</style>
