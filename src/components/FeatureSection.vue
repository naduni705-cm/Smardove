<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const sectionRef = ref(null)
const isVisible = ref(false)
const cardTilt = ref([{}, {}, {}])

let observer
let prefersReducedMotion = false

onMounted(() => {
  prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches

  if (prefersReducedMotion || !('IntersectionObserver' in window)) {
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
    { threshold: 0.2 }
  )

  if (sectionRef.value) observer.observe(sectionRef.value)
})

onBeforeUnmount(() => observer?.disconnect())

// Subtle cursor-driven tilt on each card. No-ops under reduced motion.
function onCardMove(event, index) {
  if (prefersReducedMotion) return

  const rect = event.currentTarget.getBoundingClientRect()
  const px = (event.clientX - rect.left) / rect.width - 0.5
  const py = (event.clientY - rect.top) / rect.height - 0.5

  cardTilt.value[index] = {
    transform: `perspective(900px) rotateX(${(py * -6).toFixed(2)}deg) rotateY(${(px * 6).toFixed(2)}deg) translateY(-6px)`
  }
}

function onCardLeave(index) {
  cardTilt.value[index] = {}
}

const features = [
  {
    id: 'hosting',
    title: 'Business Email Hosting',
    description: 'Professional mailboxes, generous storage, and reliable access',
    href: 'https://smardove.com/features/'
  },
  {
    id: 'security',
    title: 'Advanced Mail Security',
    description: 'Powerful spam filtering, malware protection, and secure delivery',
    href: 'https://smardove.com/features/'
  },
  {
    id: 'migration',
    title: 'Easy Email Migration',
    description: 'Move existing mailboxes, calendars, and contacts with confidence',
    href: 'https://smardove.com/switch-to-smardove/'
  }
]
</script>

<template>
  <section
    ref="sectionRef"
    class="business-needs"
    :class="{ 'business-needs--visible': isVisible }"
    aria-labelledby="business-needs-title"
  >
    <div class="business-needs__glow business-needs__glow--yellow" />
    <div class="business-needs__glow business-needs__glow--green" />

    <div class="business-needs__inner">
      <h2 id="business-needs-title">
        <span><mark>Everything</mark> Modern</span>
        <span>Business Needs <mark>in One Place</mark></span>
      </h2>

      <div class="business-needs__grid">
        <article
          v-for="(feature, i) in features"
          :key="feature.id"
          class="business-card"
          :style="cardTilt[i]"
          @mousemove="onCardMove($event, i)"
          @mouseleave="onCardLeave(i)"
        >
          <div class="business-card__visual" aria-hidden="true">
            <svg v-if="feature.id === 'hosting'" viewBox="0 0 320 245">
              <g class="soft-lines">
                <ellipse cx="156" cy="126" rx="104" ry="34" transform="rotate(-25 156 126)" />
                <ellipse cx="156" cy="126" rx="114" ry="45" transform="rotate(30 156 126)" />
                <path d="M92 58c-16 4-27 14-29 28" />
                <path d="m58 80 4 8 8-3" />
              </g>
              <g class="main-lines">
                <circle cx="158" cy="126" r="82" />
                <ellipse cx="158" cy="126" rx="37" ry="82" />
                <path d="M77 126h162M91 84c40 18 94 18 134 0M91 168c40-18 94-18 134 0" />
                <circle cx="61" cy="91" r="13" />
                <path d="M55 91h12M61 85v12" />
                <circle cx="251" cy="173" r="13" />
                <path d="m245 173 4 4 8-9" />
                <path d="m158 111-8 15h11l-5 16 17-22h-12l6-9Z" />
              </g>
            </svg>

            <svg v-else-if="feature.id === 'security'" viewBox="0 0 320 245">
              <g class="soft-lines">
                <path d="M64 80c14-30 41-44 80-43" />
                <path d="m137 29 10 8-10 8" />
                <path d="M256 165c-14 30-41 44-80 43" />
                <path d="m183 216-10-8 10-8" />
              </g>
              <g class="main-lines">
                <path d="M81 83c21 0 39 14 45 34" />
                <path d="m75 75 7 9-9 6" />
                <path d="M239 162c-21 0-39-14-45-34" />
                <path d="m245 170-7-9 9-6" />
                <g transform="translate(174 54) rotate(11)">
                  <ellipse cx="0" cy="0" rx="37" ry="15" />
                  <path d="M-37 0v17c0 8 17 15 37 15s37-7 37-15V0" />
                  <path d="M-37 9c0 8 17 15 37 15s37-7 37-15" />
                  <path d="M-4-9v18M6-8C0-13-7-10-7-5c0 7 14 4 14 11 0 5-8 7-14 2" />
                </g>
                <g transform="translate(143 167) rotate(-11)">
                  <ellipse cx="0" cy="0" rx="37" ry="15" />
                  <path d="M-37 0v17c0 8 17 15 37 15s37-7 37-15V0" />
                  <path d="M-37 9c0 8 17 15 37 15s37-7 37-15" />
                  <path d="M0-10v20M-8-3h16" />
                </g>
              </g>
            </svg>

            <svg v-else viewBox="0 0 320 245">
              <g class="soft-lines">
                <path d="m73 157 123 47 70-55" />
                <path d="m73 142 123 47 70-55" />
              </g>
              <g class="main-lines">
                <g transform="translate(42 21) rotate(-8 130 95)">
                  <rect x="34" y="41" width="214" height="132" rx="11" />
                  <path d="M34 75h214" />
                  <circle cx="53" cy="58" r="3" />
                  <circle cx="64" cy="58" r="3" />
                  <circle cx="75" cy="58" r="3" />
                  <path d="M53 98h63M53 111h45M53 137h68" />
                  <rect x="145" y="94" width="80" height="51" rx="7" />
                  <path d="m152 101 33 25 33-25" />
                  <path d="M152 101v37h66v-37" />
                </g>
                <path d="M77 38 58 22M58 22h17M58 22v17" />
                <path d="M259 189 278 205M278 205h-17M278 205v-17" />
              </g>
            </svg>
          </div>

          <div class="business-card__content">
            <h3>{{ feature.title }}</h3>
            <p>{{ feature.description }}</p>
            <a :href="feature.href">
              <span>Learn More</span>
              <svg class="link-arrow" viewBox="0 0 16 16" aria-hidden="true">
                <path d="M3 8h9M8 3l5 5-5 5" />
              </svg>
            </a>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.business-needs,
.business-needs * {
  box-sizing: border-box;
}

.business-needs {
  --ink: #0d0d0d;
  --sub: #9a9c9d;
  --line: #ededeb;
  --yellow: #f3ee9a;
  --green: #c9e6a8;
  position: relative;
  isolation: isolate;
  overflow: hidden;
  width: 100%;
  padding: clamp(80px, 8vw, 128px) clamp(16px, 3vw, 48px) clamp(54px, 5vw, 82px);
  background: #fff;
  color: var(--ink);
  font-family: var(--font-sans, "Plus Jakarta Sans", Arial, sans-serif);
}

.business-needs::after {
  position: absolute;
  z-index: -2;
  right: 0;
  bottom: 0;
  left: 0;
  height: 31%;
  border-radius: 50% 50% 0 0 / 16% 16% 0 0;
  background: linear-gradient(100deg, rgba(201,230,168,.42), rgba(243,238,154,.34), rgba(201,230,168,.42));
  content: "";
}

.business-needs__glow {
  position: absolute;
  z-index: -1;
  bottom: -20%;
  width: 44vw;
  height: 34vw;
  border-radius: 50%;
  filter: blur(88px);
  opacity: .46;
  pointer-events: none;
}

.business-needs__glow--yellow { left: 22%; background: var(--yellow); }
.business-needs__glow--green { right: -10%; background: var(--green); }

.business-needs__inner {
  width: min(95vw, 1500px);
  margin: 0 auto;
}

.business-needs h2 {
  margin: 0 auto clamp(56px, 6vw, 88px);
  text-align: center;
  font-size: clamp(36px, 4vw, 64px);
  font-weight: 400;
  letter-spacing: -.045em;
  line-height: 1.08;
}

.business-needs h2 span { display: block; }

.business-needs h2 mark {
  padding: 0 .03em;
  color: inherit;
  background: linear-gradient(transparent 69%, var(--yellow) 69%);
  background-repeat: no-repeat;
}

.business-needs__grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: clamp(20px, 2.6vw, 42px);
}

.business-card {
  position: relative;
  display: flex;
  min-height: clamp(510px, 39vw, 620px);
  flex-direction: column;
  overflow: hidden;
  border: 1px solid var(--line);
  border-radius: clamp(16px, 1.5vw, 24px);
  background: rgba(255,255,255,.94);
  box-shadow: 0 18px 54px -42px rgba(15,20,12,.24);
  will-change: transform;
}

/* Glossy sweep that plays across the card on hover */
.business-card::before {
  content: "";
  position: absolute;
  inset: 0;
  z-index: 1;
  background: linear-gradient(120deg, transparent 32%, rgba(255,255,255,.5) 46%, transparent 60%);
  transform: translateX(-130%);
  pointer-events: none;
}

.business-card:hover::before {
  transition: transform .9s ease;
  transform: translateX(130%);
}

.business-card__visual {
  position: relative;
  z-index: 0;
  display: grid;
  min-height: clamp(270px, 22vw, 350px);
  flex: 1;
  place-items: center;
  padding: clamp(28px, 3vw, 54px) clamp(30px, 4vw, 68px) 16px;
}

.business-card__visual svg {
  display: block;
  width: min(100%, 330px);
  height: auto;
  overflow: visible;
  fill: none;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.main-lines { stroke: #8d918d; stroke-width: 1.55; }
.soft-lines { stroke: #cfe5b6; stroke-width: 1.5; stroke-dasharray: 3 5; }

.business-card__content {
  position: relative;
  z-index: 0;
  padding: 12px clamp(22px, 2.5vw, 38px) clamp(36px, 3vw, 48px);
  text-align: center;
}

.business-card h3 {
  margin: 0;
  font-size: clamp(21px, 1.65vw, 27px);
  font-weight: 500;
  letter-spacing: -.035em;
}

.business-card p {
  max-width: 360px;
  min-height: 44px;
  margin: 12px auto 25px;
  color: var(--sub);
  font-size: clamp(12px, .95vw, 15px);
  line-height: 1.35;
}

.business-card a {
  display: inline-flex;
  min-height: 43px;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 10px 24px;
  border-radius: 8px;
  background: #080808;
  color: #fff;
  font-size: 13px;
  font-weight: 600;
  text-decoration: none;
  transition: transform .2s ease, background .2s ease;
}

.business-card a .link-arrow {
  width: 14px;
  height: 14px;
  fill: none;
  stroke: currentColor;
  stroke-width: 1.6;
  stroke-linecap: round;
  stroke-linejoin: round;
  transition: transform .25s ease;
}

.business-card a:hover { transform: translateY(-2px); background: #272727; }
.business-card a:hover .link-arrow { transform: translateX(4px); }
.business-card a:focus-visible { outline: 3px solid var(--yellow); outline-offset: 3px; }

@media (prefers-reduced-motion: no-preference) {
  .business-card {
    transition: transform .28s ease, box-shadow .28s ease;
  }

  .business-card:hover {
    box-shadow: 0 28px 65px -38px rgba(15,20,12,.3);
  }

  /* Entrance state: hidden until the section scrolls into view */
  .business-needs h2 span {
    opacity: 0;
    transform: translateY(28px);
    filter: blur(5px);
  }

  .business-needs h2 span mark {
    background-size: 0% 100%;
  }

  .business-card {
    opacity: 0;
    transform: translateY(48px) scale(.975);
  }

  .business-card__visual svg path,
  .business-card__visual svg circle,
  .business-card__visual svg ellipse,
  .business-card__visual svg rect {
    stroke-dasharray: 720;
    stroke-dashoffset: 720;
  }

  /* Title lines reveal in sequence, each followed by its highlight sweep */
  .business-needs--visible h2 span:nth-child(1) {
    animation: needs-title-in .85s cubic-bezier(.22,.7,.2,1) .08s forwards;
  }

  .business-needs--visible h2 span:nth-child(2) {
    animation: needs-title-in .85s cubic-bezier(.22,.7,.2,1) .22s forwards;
  }

  .business-needs--visible h2 span:nth-child(1) mark {
    animation: needs-mark-sweep .55s ease .55s forwards;
  }

  .business-needs--visible h2 span:nth-child(2) mark {
    animation: needs-mark-sweep .55s ease .68s forwards;
  }

  .business-needs--visible .business-card:nth-child(1) {
    animation: needs-card-in .85s cubic-bezier(.22,.7,.2,1) .3s forwards;
  }

  .business-needs--visible .business-card:nth-child(2) {
    animation: needs-card-in .85s cubic-bezier(.22,.7,.2,1) .44s forwards;
  }

  .business-needs--visible .business-card:nth-child(3) {
    animation: needs-card-in .85s cubic-bezier(.22,.7,.2,1) .58s forwards;
  }

  .business-needs--visible .business-card__visual svg path,
  .business-needs--visible .business-card__visual svg circle,
  .business-needs--visible .business-card__visual svg ellipse,
  .business-needs--visible .business-card__visual svg rect {
    animation: needs-line-draw 1.7s ease .7s forwards;
  }

  .business-needs--visible .business-card__visual svg {
    animation: needs-visual-float 4.5s ease-in-out 2.4s infinite;
  }

  .business-needs--visible .business-needs__glow--yellow {
    animation: needs-yellow-glow 8s ease-in-out infinite alternate;
  }

  .business-needs--visible .business-needs__glow--green {
    animation: needs-green-glow 9s ease-in-out infinite alternate;
  }
}

@keyframes needs-title-in {
  to { opacity: 1; transform: translateY(0); filter: blur(0); }
}

@keyframes needs-mark-sweep {
  to { background-size: 100% 100%; }
}

@keyframes needs-card-in {
  to { opacity: 1; transform: translateY(0) scale(1); }
}

@keyframes needs-line-draw {
  to { stroke-dashoffset: 0; }
}

@keyframes needs-visual-float {
  0%, 100% { transform: translateY(0) rotate(0); }
  50% { transform: translateY(-8px) rotate(.7deg); }
}

@keyframes needs-yellow-glow {
  to { transform: translate(4vw, -2vw) scale(1.12); }
}

@keyframes needs-green-glow {
  to { transform: translate(-4vw, -1vw) scale(1.08); }
}

@media (max-width: 960px) {
  .business-needs__grid { grid-template-columns: 1fr 1fr; }
  .business-card:last-child { grid-column: 1 / -1; width: calc(50% - 10px); margin: 0 auto; }
}

@media (max-width: 650px) {
  .business-needs { padding-inline: 14px; }
  .business-needs__inner { width: 100%; }
  .business-needs h2 { font-size: clamp(34px, 10.5vw, 50px); }
  .business-needs__grid { grid-template-columns: 1fr; }
  .business-card:last-child { grid-column: auto; width: 100%; }
  .business-card { min-height: 500px; }
  .business-card__visual { min-height: 290px; }
}

/* Cursor-tilt is a fine-pointer enhancement only */
@media (hover: none) {
  .business-card { transform: none !important; }
}
</style>
