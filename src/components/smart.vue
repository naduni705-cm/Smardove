<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const section = ref(null)
const activeIndex = ref(0)
const isVisible = ref(false)
let observer
let rotationTimer

const features = [
  {
    label: 'Mailboxes',
    short: 'Professional email for every member of your team',
    title: 'Create professional mailboxes instantly',
    description:
      'Launch branded business email on your own domain, add team members in seconds, and manage every mailbox from one calm workspace.',
    eyebrow: 'Mailbox growth',
    metric: '2.4K',
    metricLabel: 'Active mailboxes',
    bars: [44, 58, 72, 92, 76],
    values: ['420', '680', '1.1K', '2.4K', '1.9K']
  },
  {
    label: 'Security',
    short: 'Advanced protection for every incoming message',
    title: 'Keep every conversation protected',
    description:
      'Stop spam, phishing, malware, and suspicious attachments before they reach your team—with always-on scanning and secure delivery.',
    eyebrow: 'Threat protection',
    metric: '99.9%',
    metricLabel: 'Threats blocked',
    bars: [62, 78, 68, 88, 96],
    values: ['98.7%', '99.1%', '99.0%', '99.6%', '99.9%']
  },
  {
    label: 'Migration',
    short: 'Move email, contacts, and calendars with confidence',
    title: 'Switch without disrupting your work',
    description:
      'Bring existing messages, folders, contacts, and calendars into Smardove with a guided migration built to keep your business moving.',
    eyebrow: 'Migration progress',
    metric: '18K+',
    metricLabel: 'Messages moved',
    bars: [28, 46, 65, 84, 100],
    values: ['20%', '42%', '65%', '84%', '100%']
  },
  {
    label: 'Insights',
    short: 'See delivery, activity, and storage at a glance',
    title: 'Understand email performance clearly',
    description:
      'Monitor delivery health, mailbox activity, security events, and storage from a focused dashboard that makes every signal easy to act on.',
    eyebrow: 'Delivery health',
    metric: '99.98%',
    metricLabel: 'Successful delivery',
    bars: [54, 69, 81, 74, 94],
    values: ['96%', '97%', '98%', '97%', '99%']
  }
]

const setActive = (index) => {
  activeIndex.value = index
  restartRotation()
}

const startRotation = () => {
  window.clearInterval(rotationTimer)
  rotationTimer = window.setInterval(() => {
    activeIndex.value = (activeIndex.value + 1) % features.length
  }, 6500)
}

const restartRotation = () => {
  if (!window.matchMedia('(prefers-reduced-motion: reduce)').matches) startRotation()
}

const pauseRotation = () => window.clearInterval(rotationTimer)

onMounted(() => {
  observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        isVisible.value = true
        observer.disconnect()
      }
    },
    { threshold: 0.16 }
  )

  if (section.value) observer.observe(section.value)
  restartRotation()
})

onBeforeUnmount(() => {
  observer?.disconnect()
  window.clearInterval(rotationTimer)
})
</script>

<template>
  <section
    ref="section"
    class="email-benefits"
    :class="{ 'is-visible': isVisible }"
    aria-labelledby="email-benefits-title"
  >
    <div class="email-benefits__glow email-benefits__glow--yellow" aria-hidden="true" />
    <div class="email-benefits__glow email-benefits__glow--green" aria-hidden="true" />

    <div class="email-benefits__inner">
      <header class="email-benefits__header">
        <span class="email-benefits__pill">
          <svg viewBox="0 0 16 16" aria-hidden="true">
            <path d="M8 1.5v3M8 11.5v3M1.5 8h3M11.5 8h3M3.4 3.4l2.1 2.1M10.5 10.5l2.1 2.1M12.6 3.4l-2.1 2.1M5.5 10.5l-2.1 2.1" />
          </svg>
          Smardove Benefits
        </span>

        <h2 id="email-benefits-title">
          Business email<br />
          <mark>connected and ,productive.</mark>
        </h2>

        <p>
          Everything growing businesses need to communicate professionally—without
          complicated setup, hidden costs, or unreliable delivery.
        </p>
      </header>

      <div class="feature-shell" @mouseenter="pauseRotation" @mouseleave="restartRotation">
        <div class="feature-tabs" role="tablist" aria-label="Smardove email benefits">
          <button
            v-for="(feature, index) in features"
            :id="`feature-tab-${index}`"
            :key="feature.label"
            class="feature-tab"
            :class="{ 'is-active': activeIndex === index }"
            type="button"
            role="tab"
            :aria-selected="activeIndex === index"
            :aria-controls="`feature-panel-${index}`"
            @click="setActive(index)"
          >
            <span class="feature-tab__number">0{{ index + 1 }}</span>
            <strong>{{ feature.label }}</strong>
            <small>{{ feature.short }}</small>
          </button>
        </div>

        <Transition name="panel" mode="out-in">
          <article
            :id="`feature-panel-${activeIndex}`"
            :key="activeIndex"
            class="feature-panel"
            role="tabpanel"
            :aria-labelledby="`feature-tab-${activeIndex}`"
          >
            <div class="feature-panel__copy">
              <span class="feature-panel__kicker">{{ features[activeIndex].eyebrow }}</span>
              <h3>{{ features[activeIndex].title }}</h3>
              <p>{{ features[activeIndex].description }}</p>
              <a href="https://smardove.com/features/">
                Explore Features
                <span aria-hidden="true">↗</span>
              </a>

              <div class="feature-panel__proof">
                <span class="proof-avatars" aria-hidden="true">
                  <i>AM</i><i>JD</i><i>SK</i>
                </span>
                <span><strong>4.9/5</strong> from growing teams</span>
              </div>
            </div>

            <div class="dashboard-scene" aria-label="Animated email performance dashboard">
              <div class="dashboard-scene__halo" aria-hidden="true" />

              <div class="delivery-card">
                <header class="delivery-card__header">
                  <div>
                    <span>Smardove Analytics</span>
                    <h4>{{ features[activeIndex].eyebrow }}</h4>
                  </div>
                  <button type="button" aria-label="Open dashboard menu">•••</button>
                </header>

                <div class="delivery-card__summary">
                  <div>
                    <strong>{{ features[activeIndex].metric }}</strong>
                    <span>{{ features[activeIndex].metricLabel }}</span>
                  </div>
                  <span class="positive"><i>↗</i> 18.4%</span>
                </div>

                <div class="chart" aria-hidden="true">
                  <span class="chart__line chart__line--one" />
                  <span class="chart__line chart__line--two" />
                  <span class="chart__line chart__line--three" />

                  <div
                    v-for="(height, index) in features[activeIndex].bars"
                    :key="`${activeIndex}-${index}`"
                    class="chart__column"
                  >
                    <span class="chart__value">{{ features[activeIndex].values[index] }}</span>
                    <span
                      class="chart__bar"
                      :style="{ '--bar-height': `${height}%`, '--bar-delay': `${index * 90}ms` }"
                    />
                    <small>{{ ['Mon', 'Tue', 'Wed', 'Thu', 'Fri'][index] }}</small>
                  </div>
                </div>
              </div>

              <div class="message-card message-card--top">
                <span class="message-card__icon">
                  <svg viewBox="0 0 24 24" aria-hidden="true">
                    <rect x="3" y="5" width="18" height="14" rx="4" />
                    <path d="m5 8 7 5 7-5" />
                  </svg>
                </span>
                <span><strong>Message delivered</strong><small>Protected by Smardove</small></span>
                <i>✓</i>
              </div>

              <div class="message-card message-card--bottom">
                <span class="security-ring"><i>✓</i></span>
                <span><strong>All systems secure</strong><small>Scanning every message</small></span>
              </div>
            </div>
          </article>
        </Transition>
      </div>
    </div>
  </section>
</template>

<style scoped>
.email-benefits,
.email-benefits * {
  box-sizing: border-box;
}

.email-benefits {
  --ink: #0d0d0d;
  --muted: #70766d;
  --line: #e6eae3;
  --panel: #f5f7f1;
  --green: #c9e6a8;
  --green-deep: #729a50;
  --yellow: #f3ee9a;
  position: relative;
  isolation: isolate;
  overflow: hidden;
  width: 100%;
  padding: clamp(82px, 9vw, 142px) clamp(16px, 3vw, 46px);
  background: #fdfdfb;
  color: var(--ink);
  font-family: var(--font-sans, "Plus Jakarta Sans", Arial, sans-serif);
}

.email-benefits::before {
  position: absolute;
  z-index: -2;
  inset: 0;
  background-image:
    linear-gradient(rgba(13, 13, 13, .018) 1px, transparent 1px),
    linear-gradient(90deg, rgba(13, 13, 13, .018) 1px, transparent 1px);
  background-size: 56px 56px;
  mask-image: linear-gradient(transparent, #000 25%, #000 80%, transparent);
  content: "";
}

.email-benefits__glow {
  position: absolute;
  z-index: -1;
  width: min(48vw, 650px);
  aspect-ratio: 1;
  border-radius: 50%;
  filter: blur(120px);
  opacity: .32;
  pointer-events: none;
}

.email-benefits__glow--yellow {
  top: -28%;
  left: -12%;
  background: var(--yellow);
}

.email-benefits__glow--green {
  right: -16%;
  bottom: -28%;
  background: var(--green);
}

.email-benefits__inner {
  width: min(1180px, 100%);
  margin: 0 auto;
}

.email-benefits__header {
  max-width: 850px;
  margin: 0 auto clamp(55px, 7vw, 92px);
  text-align: center;
  opacity: 0;
  transform: translateY(25px);
}

.is-visible .email-benefits__header {
  animation: rise-in .8s cubic-bezier(.2, .8, .2, 1) forwards;
}

.email-benefits__pill {
  display: inline-flex;
  min-height: 31px;
  align-items: center;
  gap: 7px;
  margin-bottom: 22px;
  padding: 6px 13px;
  border: 1px solid rgba(114, 154, 80, .2);
  border-radius: 999px;
  background: linear-gradient(100deg, rgba(201, 230, 168, .78), rgba(243, 238, 154, .75));
  box-shadow: 0 8px 24px rgba(79, 105, 58, .08);
  font-size: 11px;
  font-weight: 700;
}

.email-benefits__pill svg {
  width: 13px;
  fill: none;
  stroke: currentColor;
  stroke-linecap: round;
}

.email-benefits h2 {
  margin: 0;
  font-family: var(--font-display, var(--font-sans));
  font-size: clamp(34px, 4.4vw, 64px);
  font-weight: 380;
  line-height: 1.08;
  letter-spacing: -.04em;
}

.email-benefits h2 mark {
  padding: 0 2px;
  background: linear-gradient(transparent 64%, var(--yellow) 64%);
  color: inherit;
}

.email-benefits__header > p {
  max-width: 670px;
  margin: 20px auto 0;
  color: var(--muted);
  font-size: clamp(13px, 1.2vw, 16px);
  line-height: 1.65;
}

.feature-shell {
  opacity: 0;
  transform: translateY(38px);
}

.is-visible .feature-shell {
  animation: rise-in .9s .2s cubic-bezier(.2, .8, .2, 1) forwards;
}

.feature-tabs {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  align-items: stretch;
}

.feature-tab {
  position: relative;
  min-height: 158px;
  padding: 30px 28px 26px;
  border: 0;
  border-radius: 23px 23px 0 0;
  background: transparent;
  color: var(--ink);
  font: inherit;
  text-align: left;
  cursor: pointer;
  transition: background .4s ease, transform .35s ease;
}

.feature-tab::after {
  position: absolute;
  right: 28px;
  bottom: 17px;
  left: 28px;
  height: 2px;
  border-radius: 2px;
  background: var(--green-deep);
  content: "";
  opacity: 0;
  transform: scaleX(0);
  transform-origin: left;
  transition: opacity .3s ease, transform .45s ease;
}

.feature-tab:hover {
  transform: translateY(-3px);
}

.feature-tab.is-active {
  background: var(--panel);
  transform: none;
}

.feature-tab.is-active::after {
  opacity: 1;
  transform: scaleX(1);
}

.feature-tab:focus-visible {
  z-index: 2;
  outline: 3px solid var(--yellow);
  outline-offset: -4px;
}

.feature-tab__number {
  position: absolute;
  top: 15px;
  right: 22px;
  color: #a2a89f;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: .08em;
}

.feature-tab strong,
.feature-tab small {
  display: block;
}

.feature-tab strong {
  margin-bottom: 9px;
  font-size: 16px;
  font-weight: 700;
  letter-spacing: -.025em;
}

.feature-tab small {
  max-width: 210px;
  color: var(--muted);
  font-size: 12px;
  line-height: 1.55;
}

.feature-panel {
  display: grid;
  min-height: 560px;
  grid-template-columns: .82fr 1.18fr;
  align-items: center;
  gap: clamp(40px, 6vw, 90px);
  overflow: hidden;
  padding: clamp(52px, 7vw, 92px) clamp(34px, 6vw, 86px);
  border-radius: 0 0 28px 28px;
  background: var(--panel);
  box-shadow: 0 34px 90px -62px rgba(24, 38, 16, .38);
}

.feature-panel__copy {
  position: relative;
  z-index: 3;
}

.feature-panel__kicker {
  display: inline-block;
  margin-bottom: 17px;
  color: var(--green-deep);
  font-size: 10px;
  font-weight: 800;
  letter-spacing: .12em;
  text-transform: uppercase;
}

.feature-panel h3 {
  max-width: 440px;
  margin: 0;
  font-family: var(--font-display, var(--font-sans));
  font-size: clamp(32px, 3.2vw, 49px);
  font-weight: 420;
  line-height: 1.08;
  letter-spacing: -.045em;
}

.feature-panel__copy > p {
  max-width: 460px;
  margin: 21px 0 29px;
  color: var(--muted);
  font-size: 14px;
  line-height: 1.7;
}

.feature-panel__copy > a {
  display: inline-flex;
  min-height: 48px;
  align-items: center;
  gap: 16px;
  padding: 10px 13px 10px 21px;
  border-radius: 999px;
  background: var(--ink);
  color: #fff;
  font-size: 12px;
  font-weight: 700;
  text-decoration: none;
  transition: transform .25s ease, box-shadow .25s ease;
}

.feature-panel__copy > a span {
  display: grid;
  width: 28px;
  height: 28px;
  place-items: center;
  border-radius: 50%;
  background: var(--yellow);
  color: var(--ink);
  font-size: 14px;
}

.feature-panel__copy > a:hover {
  box-shadow: 0 13px 28px rgba(13, 13, 13, .18);
  transform: translateY(-3px);
}

.feature-panel__proof {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-top: 39px;
  color: var(--muted);
  font-size: 10px;
}

.feature-panel__proof strong {
  color: var(--ink);
}

.proof-avatars {
  display: flex;
  padding-left: 8px;
}

.proof-avatars i {
  display: grid;
  width: 28px;
  height: 28px;
  margin-left: -8px;
  place-items: center;
  border: 2px solid var(--panel);
  border-radius: 50%;
  background: var(--green);
  color: #37452f;
  font-style: normal;
  font-size: 7px;
  font-weight: 800;
}

.proof-avatars i:nth-child(2) { background: var(--yellow); }
.proof-avatars i:nth-child(3) { background: #d9ddd5; }

.dashboard-scene {
  position: relative;
  min-height: 430px;
  perspective: 1100px;
}

.dashboard-scene__halo {
  position: absolute;
  inset: -8% -12% 0 2%;
  border-radius: 38% 55% 36% 60%;
  background:
    radial-gradient(circle at 28% 72%, rgba(243, 238, 154, .95), transparent 38%),
    radial-gradient(circle at 70% 30%, rgba(201, 230, 168, .92), transparent 48%),
    linear-gradient(135deg, #eef4e7, #fbf8cf);
  filter: saturate(.9);
  opacity: .9;
  transform: rotate(-3deg);
  animation: halo-breathe 7s ease-in-out infinite;
}

.delivery-card {
  position: absolute;
  z-index: 2;
  top: 22px;
  right: 0;
  width: min(94%, 550px);
  min-height: 390px;
  padding: clamp(23px, 3vw, 35px);
  border: 1px solid rgba(255, 255, 255, .92);
  border-radius: 23px;
  background: rgba(255, 255, 255, .9);
  box-shadow: 0 34px 70px rgba(68, 88, 49, .16), inset 0 1px 0 #fff;
  backdrop-filter: blur(18px);
  transform: rotateY(-4deg) rotateX(2deg);
  transform-origin: center;
  animation: dashboard-float 6s ease-in-out infinite;
}

.delivery-card__header,
.delivery-card__summary {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
}

.delivery-card__header span {
  color: #8a9185;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: .09em;
  text-transform: uppercase;
}

.delivery-card h4 {
  margin: 5px 0 0;
  font-size: clamp(17px, 1.7vw, 22px);
  font-weight: 700;
  letter-spacing: -.03em;
}

.delivery-card__header button {
  width: 31px;
  height: 31px;
  border: 1px solid var(--line);
  border-radius: 9px;
  background: #fff;
  color: #92988e;
  cursor: pointer;
}

.delivery-card__summary {
  align-items: flex-end;
  margin-top: 31px;
}

.delivery-card__summary div strong,
.delivery-card__summary div span {
  display: block;
}

.delivery-card__summary div strong {
  font-size: clamp(28px, 3vw, 40px);
  font-weight: 600;
  letter-spacing: -.05em;
}

.delivery-card__summary div span {
  margin-top: 4px;
  color: var(--muted);
  font-size: 10px;
}

.positive {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 6px 9px;
  border-radius: 999px;
  background: rgba(201, 230, 168, .62);
  color: #486533;
  font-size: 9px;
  font-weight: 800;
}

.positive i { font-style: normal; }

.chart {
  position: relative;
  display: flex;
  height: 190px;
  align-items: flex-end;
  justify-content: space-between;
  gap: clamp(8px, 2vw, 19px);
  margin-top: 27px;
  padding: 13px 8px 25px;
  border-bottom: 1px solid #e7ebe4;
}

.chart__line {
  position: absolute;
  right: 0;
  left: 0;
  height: 1px;
  background: repeating-linear-gradient(90deg, #e5e9e1 0 4px, transparent 4px 8px);
}

.chart__line--one { top: 20%; }
.chart__line--two { top: 48%; }
.chart__line--three { top: 76%; }

.chart__column {
  position: relative;
  z-index: 1;
  display: flex;
  width: 20%;
  height: 100%;
  align-items: center;
  flex-direction: column;
  justify-content: flex-end;
}

.chart__value {
  margin-bottom: 5px;
  color: #677060;
  font-size: 8px;
  font-weight: 700;
  opacity: 0;
  animation: value-in .35s calc(var(--bar-delay) + .55s) forwards;
}

.chart__bar {
  width: min(52px, 72%);
  height: var(--bar-height);
  border-radius: 10px 10px 4px 4px;
  background: linear-gradient(180deg, var(--green), #a8d37e);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, .8), 0 8px 18px rgba(86, 119, 59, .12);
  transform: scaleY(0);
  transform-origin: bottom;
  animation: bar-grow .8s var(--bar-delay) cubic-bezier(.2, .85, .25, 1) forwards;
}

.chart__column:nth-of-type(even) .chart__bar {
  background: linear-gradient(180deg, var(--yellow), #e1d866);
}

.chart__column small {
  position: absolute;
  bottom: -20px;
  color: #92978e;
  font-size: 8px;
}

.message-card {
  position: absolute;
  z-index: 4;
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 11px 13px;
  border: 1px solid rgba(255, 255, 255, .9);
  border-radius: 15px;
  background: rgba(255, 255, 255, .93);
  box-shadow: 0 18px 45px rgba(42, 61, 28, .16);
  backdrop-filter: blur(15px);
}

.message-card--top {
  top: -4px;
  right: -20px;
  animation: card-float 5s .4s ease-in-out infinite;
}

.message-card--bottom {
  bottom: 0;
  left: -23px;
  animation: card-float 5.8s ease-in-out infinite reverse;
}

.message-card > span:nth-child(2) strong,
.message-card > span:nth-child(2) small {
  display: block;
}

.message-card > span:nth-child(2) strong {
  font-size: 10px;
}

.message-card > span:nth-child(2) small {
  margin-top: 3px;
  color: var(--muted);
  font-size: 7px;
}

.message-card > i {
  display: grid;
  width: 20px;
  height: 20px;
  margin-left: 8px;
  place-items: center;
  border-radius: 50%;
  background: var(--green);
  color: #496334;
  font-style: normal;
  font-size: 9px;
  font-weight: 900;
}

.message-card__icon,
.security-ring {
  display: grid;
  width: 33px;
  height: 33px;
  flex: 0 0 auto;
  place-items: center;
  border-radius: 10px;
  background: var(--yellow);
}

.message-card__icon svg {
  width: 17px;
  fill: none;
  stroke: var(--ink);
  stroke-width: 1.7;
}

.security-ring {
  border-radius: 50%;
  background: var(--green);
}

.security-ring i {
  display: grid;
  width: 19px;
  height: 19px;
  place-items: center;
  border: 1px solid rgba(62, 86, 44, .35);
  border-radius: 50%;
  color: #486134;
  font-style: normal;
  font-size: 8px;
  font-weight: 900;
}

.panel-enter-active,
.panel-leave-active {
  transition: opacity .3s ease, transform .35s ease;
}

.panel-enter-from {
  opacity: 0;
  transform: translateY(13px);
}

.panel-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}

@keyframes rise-in {
  to { opacity: 1; transform: translateY(0); }
}

@keyframes bar-grow {
  to { transform: scaleY(1); }
}

@keyframes value-in {
  to { opacity: 1; }
}

@keyframes dashboard-float {
  0%, 100% { transform: rotateY(-4deg) rotateX(2deg) translateY(0); }
  50% { transform: rotateY(-2deg) rotateX(1deg) translateY(-8px); }
}

@keyframes card-float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-9px); }
}

@keyframes halo-breathe {
  0%, 100% { transform: rotate(-3deg) scale(1); }
  50% { transform: rotate(1deg) scale(1.025); }
}

@media (max-width: 900px) {
  .feature-tabs {
    grid-template-columns: repeat(2, 1fr);
    gap: 7px;
    margin-bottom: 7px;
  }

  .feature-tab,
  .feature-tab.is-active {
    min-height: 130px;
    border-radius: 18px;
  }

  .feature-tab.is-active { background: #eef3e8; }

  .feature-panel {
    grid-template-columns: 1fr;
    border-radius: 25px;
  }

  .feature-panel__copy { max-width: 620px; }
  .dashboard-scene { width: min(680px, 100%); margin: 10px auto 0; }
}

@media (max-width: 600px) {
  .email-benefits { padding-inline: 13px; }
  .email-benefits h2 br { display: none; }

  .feature-tabs {
    display: flex;
    overflow-x: auto;
    padding-bottom: 5px;
    scroll-snap-type: x mandatory;
    scrollbar-width: none;
  }

  .feature-tabs::-webkit-scrollbar { display: none; }

  .feature-tab {
    min-width: 220px;
    scroll-snap-align: start;
  }

  .feature-panel {
    min-height: auto;
    gap: 42px;
    padding: 43px 23px 35px;
  }

  .feature-panel__proof { margin-top: 30px; }
  .dashboard-scene { min-height: 350px; }

  .delivery-card {
    top: 20px;
    left: 0;
    width: 100%;
    min-height: 320px;
    padding: 21px 18px;
    transform: none;
  }

  .chart { height: 150px; gap: 5px; }
  .message-card--top { top: 1px; right: -7px; }
  .message-card--bottom { bottom: -11px; left: -4px; }
  .message-card--top > span:nth-child(2) { display: none; }
  .message-card--top > i { margin-left: 0; }
}

@media (prefers-reduced-motion: reduce) {
  .email-benefits__header,
  .feature-shell {
    opacity: 1 !important;
    transform: none !important;
    animation: none !important;
  }

  .dashboard-scene__halo,
  .delivery-card,
  .message-card,
  .chart__bar,
  .chart__value {
    animation: none !important;
  }

  .chart__bar { transform: scaleY(1); }
  .chart__value { opacity: 1; }
  .panel-enter-active,
  .panel-leave-active { transition: none; }
}
</style>
