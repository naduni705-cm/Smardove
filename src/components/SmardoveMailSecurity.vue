<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const sectionRef = ref(null)
const isVisible = ref(false)
let observer

onMounted(() => {
  const reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches

  if (reduceMotion || !('IntersectionObserver' in window)) {
    isVisible.value = true
    return
  }

  observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        isVisible.value = true
        observer.disconnect()
      }
    },
    { threshold: 0.18 }
  )

  if (sectionRef.value) observer.observe(sectionRef.value)
})

onBeforeUnmount(() => observer?.disconnect())

const browserSupport = ['Chrome', 'Safari', 'Firefox', 'Edge']
</script>

<template>
  <section
    ref="sectionRef"
    class="mail-security"
    :class="{ 'mail-security--visible': isVisible }"
    aria-labelledby="mail-security-title"
  >
    <div class="mail-security__glow mail-security__glow--left" />
    <div class="mail-security__glow mail-security__glow--right" />

    <div class="mail-security__shell">
      <div class="mail-security__eyebrow">
        <span>Smardove Mail Security</span>
        <span class="mail-security__eyebrow-line" />
      </div>

      <div class="mail-security__grid">
        <!-- Left column: intro copy -->
        <article class="mail-security__intro">
          <div>
            <p class="mail-security__kicker">Secure email, anywhere</p>
            <h2 id="mail-security-title">
              Powerful Client <mark>Webmail</mark>
            </h2>

            <div class="mail-security__meta-row">
              <span>Webmail Client</span>
              <i aria-hidden="true" />
            </div>
          </div>

          <div class="mail-security__copy">
            <p>
              Compatible with all major desktop and mobile web browsers, the
              Smardove webmail client removes the need for separate email and
              calendar software.
            </p>
            <p>
              Free up disk space and system resources while reducing the
              maintenance required on laptops and personal computers.
            </p>
          </div>

          <div class="mail-security__trust">
            <span class="mail-security__trust-icon" aria-hidden="true">
              <svg viewBox="0 0 24 24">
                <path d="M12 3 5 6v5c0 4.7 2.8 8.3 7 10 4.2-1.7 7-5.3 7-10V6l-7-3Z" />
                <path d="m9 12 2 2 4-5" />
              </svg>
            </span>
            <span>Protected by Smardove Mail Security</span>
          </div>

          <div class="mail-security__browser-logos" aria-label="Supported browsers">
            <div><strong>Google</strong><small>Chrome</small></div>
            <div><strong>Apple</strong><small>Safari</small></div>
            <div><strong>Mozilla</strong><small>Firefox</small></div>
            <div><strong>Microsoft</strong><small>Edge</small></div>
          </div>
        </article>

        <!-- Right column: feature cards -->
        <div class="mail-security__cards">
          <article class="feature-card feature-card--main">
            <div class="feature-card__topline">
              <span>01 / Webmail</span>
              <span class="round-icon" aria-hidden="true">↗</span>
            </div>

            <div class="feature-card__main-copy">
              <p>Work From Anywhere</p>
              <h3>Your inbox.<br />Always within reach.</h3>
            </div>

            <div class="browser-window" aria-hidden="true">
              <div class="browser-window__bar">
                <span /><span /><span />
                <div class="browser-window__address">mail.smardove.com</div>
              </div>
              <div class="browser-window__body">
                <aside class="browser-window__sidebar">
                  <strong>S</strong>
                  <i /><i /><i /><i />
                </aside>
                <div class="browser-window__messages">
                  <div class="browser-window__heading">
                    <strong>Inbox</strong>
                    <span>•••</span>
                  </div>
                  <div v-for="n in 4" :key="n" class="message-row">
                    <span class="message-row__avatar">{{ ['A', 'M', 'J', 'S'][n - 1] }}</span>
                    <span class="message-row__lines"><i /><i /></span>
                    <span class="message-row__time">{{ 9 + n }}:2{{ n }}</span>
                  </div>
                </div>
              </div>
            </div>
          </article>

          <div class="mail-security__small-grid">
            <article class="feature-card feature-card--green">
              <div class="feature-card__topline">
                <span>Browser compatibility</span>
                <span class="round-icon round-icon--light" aria-hidden="true">↗</span>
              </div>
              <div class="browser-count">4</div>
              <p class="feature-card__caption">Major browsers supported</p>
              <div class="browser-list">
                <span v-for="browser in browserSupport" :key="browser">{{ browser }}</span>
              </div>
            </article>

            <article class="feature-card feature-card--yellow">
              <div class="feature-card__topline">
                <span>Less software</span>
                <span class="round-icon" aria-hidden="true">+</span>
              </div>
              <div class="device-visual" aria-hidden="true">
                <svg viewBox="0 0 220 120">
                  <rect x="18" y="20" width="122" height="78" rx="8" />
                  <path d="M8 104h142l-10 8H20l-12-8Z" />
                  <rect x="90" y="42" width="112" height="66" rx="10" />
                  <path d="m108 62 38 27 38-27" />
                  <path d="M108 62v30h76V62" />
                </svg>
              </div>
              <p class="feature-card__caption">
                Email and calendar access with no extra desktop apps.
              </p>
            </article>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* ==========================================================================
   Base / tokens
   ========================================================================== */
.mail-security,
.mail-security * {
  box-sizing: border-box;
}

.mail-security {
  --ink: #0d0d0d;
  --sub: #686d72;
  --line: rgba(13, 13, 13, 0.14);
  --green: #c9e6a8;
  --green-deep: #b6dc8d;
  --yellow: #f3ee9a;
  --radius-lg: 26px;
  --shadow-card: 0 24px 60px -42px rgba(20, 26, 16, 0.32);

  position: relative;
  overflow: hidden;
  isolation: isolate;
  background:
    radial-gradient(circle at 4% 94%, rgba(243, 238, 154, 0.5), transparent 24%),
    radial-gradient(circle at 94% 88%, rgba(201, 230, 168, 0.55), transparent 29%),
    #fff;
  color: var(--ink);
  padding: clamp(72px, 8vw, 138px) clamp(18px, 4vw, 64px);
  font-family: var(--font-sans, "Plus Jakarta Sans", Arial, sans-serif);
}

.mail-security__glow {
  position: absolute;
  z-index: -1;
  width: 38vw;
  height: 38vw;
  border-radius: 50%;
  filter: blur(95px);
  opacity: 0.28;
  pointer-events: none;
}

.mail-security__glow--left {
  left: -24vw;
  bottom: -18vw;
  background: linear-gradient(135deg, var(--yellow), var(--green));
}

.mail-security__glow--right {
  right: -24vw;
  top: 4vw;
  background: linear-gradient(135deg, var(--green), var(--yellow));
}

.mail-security__shell {
  width: min(92vw, 1440px);
  margin: 0 auto;
}

/* ==========================================================================
   Eyebrow
   ========================================================================== */
.mail-security__eyebrow {
  display: flex;
  align-items: center;
  gap: 22px;
  padding-bottom: 16px;
  border-bottom: 1px solid var(--line);
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 0.01em;
}

.mail-security__eyebrow-line {
  flex: 1;
  height: 1px;
  background: transparent;
}

/* ==========================================================================
   Layout grid
   ========================================================================== */
.mail-security__grid {
  display: grid;
  grid-template-columns: minmax(320px, 0.92fr) minmax(520px, 1.28fr);
  gap: clamp(42px, 6vw, 96px);
  padding-top: clamp(36px, 4vw, 64px);
}

/* ==========================================================================
   Intro column
   ========================================================================== */
.mail-security__intro {
  min-height: 660px;
  display: flex;
  flex-direction: column;
}

.mail-security__kicker {
  margin: 0 0 18px;
  color: var(--sub);
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 0.09em;
  text-transform: uppercase;
}

.mail-security h2 {
  margin: 0;
  font-family: var(--font-display);
  font-size: clamp(30px, 4.6vw, 68px);
  font-weight: 380;
  line-height: 1.08;
  letter-spacing: -0.01em;
}

.mail-security h2 mark {
  padding: 0 2px;
  background: linear-gradient(transparent 62%, var(--yellow) 62%);
  color: inherit;
}

.mail-security__meta-row {
  display: flex;
  align-items: center;
  gap: 18px;
  width: 100%;
  margin-top: clamp(34px, 4vw, 58px);
}

.mail-security__meta-row span {
  flex: 0 0 auto;
  padding: 10px 20px;
  border-radius: 999px;
  background: linear-gradient(100deg, var(--yellow), var(--green));
  color: var(--ink);
  font-size: 11px;
  font-weight: 750;
  letter-spacing: 0.07em;
}

.mail-security__meta-row i {
  width: min(52%, 330px);
  height: 1px;
  background: var(--line);
}

.mail-security__copy {
  max-width: 580px;
  margin-top: auto;
  padding-top: 70px;
  color: var(--sub);
  font-size: clamp(15px, 1.1vw, 18px);
  line-height: 1.7;
}

.mail-security__copy p {
  margin: 0 0 14px;
}

.mail-security__trust {
  display: flex;
  align-items: center;
  gap: 12px;
  padding-top: 24px;
  margin-top: 18px;
  border-top: 1px solid var(--line);
  font-size: 13px;
  font-weight: 650;
}

.mail-security__trust-icon {
  display: grid;
  width: 36px;
  height: 36px;
  place-items: center;
  border-radius: 50%;
  background: var(--green);
}

.mail-security__trust-icon svg {
  width: 19px;
  fill: none;
  stroke: currentColor;
  stroke-width: 1.7;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.mail-security__browser-logos {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 14px;
  margin-top: 28px;
  padding: 24px 0 18px;
  border-top: 1px solid var(--line);
  border-bottom: 1px solid var(--line);
}

.mail-security__browser-logos div {
  display: flex;
  min-width: 0;
  flex-direction: column;
}

.mail-security__browser-logos strong {
  overflow: hidden;
  font-family: Georgia, "Times New Roman", serif;
  font-size: clamp(15px, 1.35vw, 22px);
  font-weight: 700;
  letter-spacing: -0.04em;
  line-height: 1;
  text-overflow: ellipsis;
}

.mail-security__browser-logos small {
  margin-top: 5px;
  color: var(--sub);
  font-size: 8px;
  font-weight: 750;
  letter-spacing: 0.11em;
  text-transform: uppercase;
}

/* ==========================================================================
   Feature cards
   ========================================================================== */
.mail-security__cards {
  display: grid;
  gap: 16px;
}

.feature-card {
  overflow: hidden;
  border: 1px solid var(--line);
  border-radius: var(--radius-lg);
  background-color: rgba(255, 255, 255, 0.94);
  box-shadow: var(--shadow-card);
}

.feature-card__topline {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
  font-size: 12px;
  font-weight: 650;
}

.round-icon {
  display: grid;
  width: 38px;
  height: 38px;
  flex: 0 0 auto;
  place-items: center;
  border: 1px solid rgba(13, 13, 13, 0.34);
  border-radius: 50%;
  font-size: 19px;
}

.round-icon--light {
  border-color: rgba(13, 13, 13, 0.34);
}

/* -- Main (large) card -- */
.feature-card--main {
  position: relative;
  min-height: 360px;
  padding: 24px 26px 0;
  background:
    radial-gradient(circle at 92% 90%, rgba(201, 230, 168, 0.82), transparent 42%),
    radial-gradient(circle at 70% 108%, rgba(243, 238, 154, 0.9), transparent 38%),
    rgba(255, 255, 255, 0.96);
}

.feature-card__main-copy {
  position: relative;
  z-index: 2;
  margin-top: 48px;
}

.feature-card__main-copy p {
  margin: 0 0 10px;
  font-size: 11px;
  font-weight: 750;
  letter-spacing: 0.11em;
  text-transform: uppercase;
}

.feature-card h3 {
  margin: 0;
  max-width: 410px;
  font-size: clamp(31px, 3vw, 48px);
  font-weight: 480;
  letter-spacing: -0.045em;
  line-height: 1.02;
}

.browser-window {
  position: absolute;
  right: -24px;
  bottom: -48px;
  width: min(57%, 430px);
  min-width: 300px;
  overflow: hidden;
  border: 1px solid rgba(13, 13, 13, 0.14);
  border-radius: 17px 17px 0 0;
  background: rgba(255, 255, 255, 0.94);
  box-shadow: 0 24px 60px rgba(48, 72, 32, 0.2);
  transform: rotate(-2deg);
}

.browser-window__bar {
  display: flex;
  align-items: center;
  gap: 5px;
  height: 32px;
  padding: 0 10px;
  background: #f3f3f1;
  border-bottom: 1px solid #e4e4e1;
}

.browser-window__bar > span {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #c8c8c4;
}

.browser-window__address {
  width: 55%;
  margin: 0 auto;
  padding: 4px;
  border-radius: 6px;
  background: #fff;
  color: #8a8e8a;
  font-size: 7px;
  text-align: center;
}

.browser-window__body {
  display: flex;
  height: 185px;
}

.browser-window__sidebar {
  display: flex;
  width: 48px;
  flex-direction: column;
  align-items: center;
  gap: 14px;
  padding-top: 13px;
  background: #171817;
  color: #fff;
}

.browser-window__sidebar strong {
  display: grid;
  width: 23px;
  height: 23px;
  place-items: center;
  border-radius: 7px;
  background: var(--green);
  color: #111;
  font-size: 10px;
}

.browser-window__sidebar i {
  width: 15px;
  height: 3px;
  border-radius: 4px;
  background: #565956;
}

.browser-window__messages {
  flex: 1;
  padding: 17px;
}

.browser-window__heading {
  display: flex;
  justify-content: space-between;
  padding-bottom: 12px;
  font-size: 11px;
}

.message-row {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 9px 0;
  border-top: 1px solid #ecece9;
}

.message-row__avatar {
  display: grid;
  width: 22px;
  height: 22px;
  flex: 0 0 auto;
  place-items: center;
  border-radius: 50%;
  background: #edf3e7;
  font-size: 7px;
  font-style: normal;
}

.message-row__lines {
  display: grid;
  flex: 1;
  gap: 5px;
}

.message-row__lines i {
  width: 80%;
  height: 4px;
  border-radius: 4px;
  background: #d7d9d5;
}

.message-row__lines i:last-child {
  width: 56%;
  background: #eceeeb;
}

.message-row__time {
  color: #9a9c98;
  font-size: 7px;
}

/* -- Small cards row -- */
.mail-security__small-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 16px;
}

.feature-card--green,
.feature-card--yellow {
  min-height: 310px;
  padding: 24px;
}

.feature-card--green {
  background:
    radial-gradient(circle at 14% 110%, rgba(201, 230, 168, 0.8), transparent 48%),
    rgba(255, 255, 255, 0.96);
  color: var(--ink);
}

.feature-card--yellow {
  background:
    radial-gradient(circle at 84% 112%, rgba(243, 238, 154, 0.96), transparent 48%),
    radial-gradient(circle at 10% 112%, rgba(201, 230, 168, 0.5), transparent 44%),
    rgba(255, 255, 255, 0.96);
}

.browser-count {
  margin-top: 42px;
  font-size: clamp(72px, 8vw, 112px);
  font-weight: 400;
  letter-spacing: -0.075em;
  line-height: 0.8;
}

.feature-card__caption {
  max-width: 260px;
  margin: 22px 0 0;
  font-size: 13px;
  line-height: 1.5;
}

.browser-list {
  display: flex;
  flex-wrap: wrap;
  gap: 7px;
  margin-top: 22px;
}

.browser-list span {
  padding: 7px 10px;
  border: 1px solid rgba(13, 13, 13, 0.16);
  border-radius: 999px;
  color: #555a55;
  font-size: 9px;
}

.device-visual {
  height: 145px;
  margin: 24px -8px -2px;
}

.device-visual svg {
  width: 100%;
  height: 100%;
  overflow: visible;
  fill: rgba(255, 255, 255, 0.52);
  stroke: #141414;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

/* ==========================================================================
   Responsive
   ========================================================================== */
@media (max-width: 1050px) {
  .mail-security__grid {
    grid-template-columns: 1fr;
  }

  .mail-security__intro {
    min-height: auto;
  }

  .mail-security__copy {
    margin-top: 54px;
    padding-top: 0;
  }
}

@media (max-width: 660px) {
  .mail-security {
    padding-inline: 16px;
  }

  .mail-security__shell {
    width: 100%;
  }

  .mail-security__eyebrow {
    font-size: 12px;
  }

  .mail-security h2 {
    font-size: clamp(42px, 14vw, 62px);
  }

  .mail-security__browser-logos {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    row-gap: 22px;
  }

  .feature-card--main {
    min-height: 510px;
  }

  .browser-window {
    right: -18px;
    width: 94%;
    min-width: 0;
  }

  .mail-security__small-grid {
    grid-template-columns: 1fr;
  }

  .feature-card--green,
  .feature-card--yellow {
    min-height: 290px;
  }
}

/* ==========================================================================
   Motion
   ========================================================================== */
@media (prefers-reduced-motion: no-preference) {
  .mail-security__eyebrow,
  .mail-security__kicker,
  .mail-security h2,
  .mail-security__meta-row,
  .mail-security__copy,
  .mail-security__trust,
  .mail-security__browser-logos,
  .feature-card {
    opacity: 0;
  }

  .mail-security__eyebrow { transform: translateY(-14px); }
  .mail-security__kicker,
  .mail-security h2,
  .mail-security__meta-row,
  .mail-security__copy,
  .mail-security__trust,
  .mail-security__browser-logos { transform: translateY(24px); }

  .feature-card--main { transform: translateX(50px) scale(.97); }
  .feature-card--green { transform: translateY(40px) rotate(-1.5deg); }
  .feature-card--yellow { transform: translateY(40px) rotate(1.5deg); }

  .mail-security--visible .mail-security__eyebrow {
    animation: security-reveal .65s ease .05s forwards;
  }
  .mail-security--visible .mail-security__kicker {
    animation: security-reveal .65s ease .16s forwards;
  }
  .mail-security--visible h2 {
    animation: security-title .85s cubic-bezier(.22,.7,.2,1) .22s forwards;
  }
  .mail-security--visible .mail-security__meta-row {
    animation: security-reveal .65s ease .38s forwards;
  }
  .mail-security--visible .mail-security__copy {
    animation: security-reveal .7s ease .5s forwards;
  }
  .mail-security--visible .mail-security__trust {
    animation: security-reveal .65s ease .62s forwards;
  }
  .mail-security--visible .mail-security__browser-logos {
    animation: security-reveal .7s ease .72s forwards;
  }

  .mail-security--visible .feature-card--main {
    animation: security-card-main .9s cubic-bezier(.22,.7,.2,1) .28s forwards;
  }
  .mail-security--visible .feature-card--green {
    animation: security-card-small .8s cubic-bezier(.22,.7,.2,1) .48s forwards;
  }
  .mail-security--visible .feature-card--yellow {
    animation: security-card-small .8s cubic-bezier(.22,.7,.2,1) .62s forwards;
  }

  .mail-security--visible .browser-window {
    animation: browser-window-float 5s ease-in-out 1.25s infinite;
  }

  .mail-security--visible .message-row {
    animation: message-pulse 4s ease-in-out infinite;
  }
  .mail-security--visible .message-row:nth-child(2) { animation-delay: 1.1s; }
  .mail-security--visible .message-row:nth-child(3) { animation-delay: 1.3s; }
  .mail-security--visible .message-row:nth-child(4) { animation-delay: 1.5s; }
  .mail-security--visible .message-row:nth-child(5) { animation-delay: 1.7s; }

  .mail-security--visible .device-visual svg {
    animation: device-float 4.5s ease-in-out 1.2s infinite;
  }

  .mail-security--visible .device-visual path,
  .mail-security--visible .device-visual rect {
    stroke-dasharray: 500;
    stroke-dashoffset: 500;
    animation: security-line-draw 1.7s ease .9s forwards;
  }

  .mail-security--visible .mail-security__glow--left {
    animation: security-glow-left 9s ease-in-out infinite alternate;
  }
  .mail-security--visible .mail-security__glow--right {
    animation: security-glow-right 10s ease-in-out infinite alternate;
  }

  .feature-card {
    transition: transform 220ms ease, box-shadow 220ms ease;
  }

  .feature-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 22px 50px rgba(18, 25, 15, 0.12);
  }
}

@keyframes security-reveal {
  to { opacity: 1; transform: translateY(0); }
}

@keyframes security-title {
  from { opacity: 0; transform: translateY(30px); filter: blur(6px); }
  to { opacity: 1; transform: translateY(0); filter: blur(0); }
}

@keyframes security-card-main {
  to { opacity: 1; transform: translateX(0) scale(1); }
}

@keyframes security-card-small {
  to { opacity: 1; transform: translateY(0) rotate(0); }
}

@keyframes browser-window-float {
  0%, 100% { transform: rotate(-2deg) translateY(0); }
  50% { transform: rotate(-.5deg) translateY(-10px); }
}

@keyframes message-pulse {
  0%, 100% { opacity: .72; transform: translateX(0); }
  50% { opacity: 1; transform: translateX(3px); }
}

@keyframes device-float {
  0%, 100% { transform: translateY(0) rotate(0); }
  50% { transform: translateY(-9px) rotate(1deg); }
}

@keyframes security-line-draw {
  to { stroke-dashoffset: 0; }
}

@keyframes security-glow-left {
  to { transform: translate(5vw, -3vw) scale(1.12); }
}

@keyframes security-glow-right {
  to { transform: translate(-4vw, 3vw) scale(1.1); }
}
</style>
