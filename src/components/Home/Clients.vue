<script setup>
import { onBeforeUnmount, onMounted, ref } from "vue";

const sectionRef = ref(null);
const visible = ref(false);
let observer;

const googleLogo = (domain) =>
  `https://www.google.com/s2/favicons?domain=${domain}&sz=128`;

const smardoveUpload = "https://smardove.com/wp-content/uploads/2023/05/";

const makeClient = ({ name, domain, fallback, tone = "mint" }, index) => ({
  id: `${name}-${index}`.toLowerCase().replace(/[^a-z0-9]+/g, "-"),
  name,
  src: googleLogo(domain),
  fallback: fallback ? `${smardoveUpload}${fallback}` : null,
  tone,
});

const topClients = [
  {
    name: "Araliya Beach",
    domain: "araliyaresorts.com",
    fallback: "image-e1683523236677.png",
    tone: "mint",
  },
  {
    name: "Dhinu",
    domain: "dhinu.com",
    fallback: "image-1.png",
    tone: "blue",
  },
  {
    name: "Heaven Seven",
    domain: "heavenseven.lk",
    fallback: "image-3-e1683704348961.png",
    tone: "lime",
  },
  {
    name: "CocoBay",
    domain: "cocobayunawatuna.com",
    fallback: "image-5.png",
    tone: "aqua",
  },
  {
    name: "Ipsova",
    domain: "ipsova.com",
    fallback: "image-6.png",
    tone: "blue",
  },
  {
    name: "Hotel Sudu Araliya",
    domain: "hotelsuduaraliya.com",
    fallback: "image-36-e1683524422398.png",
    tone: "mint",
  },
  {
    name: "Cartinn",
    domain: "cartinn.lk",
    fallback: "image-7.png",
    tone: "lime",
  },
  {
    name: "Voxinnova",
    domain: "voxinnova.com",
    fallback: "image-8.png",
    tone: "aqua",
  },
  {
    name: "Tree of Life Travels",
    domain: "treeoflifetravels.com",
    fallback: "image-9.png",
    tone: "green",
  },
  {
    name: "Yummy.lk",
    domain: "yummy.lk",
    fallback: "image-10.png",
    tone: "yellow",
  },
  {
    name: "BSS America",
    domain: "bssamerica.com",
    fallback: "image-11.png",
    tone: "blue",
  },
  {
    name: "Glory Swim Shop",
    domain: "gloryswimshop.com",
    fallback: "image-12-PhotoRoom.png-PhotoRoom.png",
    tone: "mint",
  },
  {
    name: "CDEM",
    domain: "cdem.lk",
    fallback: "image-13.png",
    tone: "lime",
  },
  {
    name: "AGRL Home Decor",
    domain: "agrl.lk",
    fallback: "AGRL_NEW5_WHITE_web_logo.png",
    tone: "aqua",
  },
  {
    name: "Araliya Group",
    domain: "araliyagroup.com",
    fallback: "image-14.png",
    tone: "green",
  },
  {
    name: "BPO Direct",
    domain: "bpodirect.com",
    fallback: "image-15.png",
    tone: "yellow",
  },
].map(makeClient);

const bottomClients = [
  {
    name: "Araliya Engineering",
    domain: "araliyaengineering.com",
    fallback: "image-PhotoRoom.png-PhotoRoom.png",
    tone: "blue",
  },
  {
    name: "Wijaya Products",
    domain: "wijayaproducts.com",
    fallback: "image-1-2.png",
    tone: "mint",
  },
  {
    name: "Araliya Amtrad",
    domain: "araliyaamtrad.com",
    fallback: "image-2-1.png",
    tone: "green",
  },
  {
    name: "Finenic",
    domain: "finenic.com",
    fallback: "image-18.png",
    tone: "aqua",
  },
  {
    name: "Office Network",
    domain: "officenetwork.lk",
    fallback: "image-1-PhotoRoom.png-PhotoRoom.png",
    tone: "blue",
  },
  {
    name: "Semini Motors",
    domain: "seminimotors.lk",
    fallback: "image-19.png",
    tone: "lime",
  },
  {
    name: "Standard Industries",
    domain: "standardindustries.lk",
    fallback: "image-1-3.png",
    tone: "yellow",
  },
  {
    name: "Edirisinghe Brothers",
    domain: "edirisinghebrothers.com",
    fallback: "image-20.png",
    tone: "mint",
  },
  {
    name: "PG Travels",
    domain: "pgtravels.lk",
    fallback: "image-21.png",
    tone: "green",
  },
  {
    name: "Lake Serenity Spa",
    domain: "lakeserenityspa.com",
    fallback: "image-22.png",
    tone: "aqua",
  },
  {
    name: "Wimma",
    domain: "wimma.lk",
    fallback: "image-23-e1683522542185.png",
    tone: "lime",
  },
  {
    name: "Roomitra",
    domain: "roomitra.com",
    fallback: "image-24.png",
    tone: "yellow",
  },
  {
    name: "Vimana",
    domain: "vimana.lk",
    fallback: "image-37-e1683524760363.png",
    tone: "blue",
  },
  {
    name: "Nastars",
    domain: "nastars.com",
    fallback: "Nastars-logo-font-black-1-150x17-1.png",
    tone: "mint",
  },
  {
    name: "Nilkamal",
    domain: "nilkamal.com",
    fallback: "image-32-e1683523569709.png",
    tone: "green",
  },
  {
    name: "PNG Embroidery",
    domain: "pngembroidery.com",
    fallback: "image-35-e1683524358179.png",
    tone: "aqua",
  },
].map(makeClient);

const onLogoError = (event, fallback) => {
  if (!fallback || event.target.dataset.fallbackUsed === "true") return;
  event.target.dataset.fallbackUsed = "true";
  event.target.src = fallback;
};

onMounted(() => {
  if (!("IntersectionObserver" in window)) {
    visible.value = true;
    return;
  }

  observer = new IntersectionObserver(
    ([entry]) => {
      if (entry.isIntersecting) {
        visible.value = true;
        observer.disconnect();
      }
    },
    { threshold: 0.16 },
  );

  if (sectionRef.value) observer.observe(sectionRef.value);
});

onBeforeUnmount(() => observer?.disconnect());
</script>

<template>
  <section
    ref="sectionRef"
    class="clients"
    :class="{ 'is-visible': visible }"
    aria-labelledby="clients-title"
  >
    <div class="clients__orb clients__orb--left" aria-hidden="true"></div>
    <div class="clients__orb clients__orb--right" aria-hidden="true"></div>

    <div class="clients__inner">
      <header class="clients__header">
        <span class="clients__eyebrow">
          <i></i>
          Our clients
        </span>
        <h2 id="clients-title">
          Trusted by growing teams using Smardove Mail.
        </h2>
        <p>
          Business email, secure delivery, and everyday collaboration for brands
          that need reliable communication.
        </p>
      </header>

      <div class="clients__marquees" aria-label="Smardove client logos">
        <div class="clients__marquee clients__marquee--right">
          <div class="clients__track">
            <div
              v-for="copy in 2"
              :key="`top-${copy}`"
              class="clients__group"
              :aria-hidden="copy === 2"
            >
              <a
                v-for="client in topClients"
                :key="`${copy}-${client.id}`"
                class="client-logo"
                :class="`client-logo--${client.tone}`"
                href="/clients/"
                :aria-label="client.name"
              >
                <span class="client-logo__mark">
                  <img
                    :src="client.src"
                    :alt="client.name"
                    loading="lazy"
                    decoding="async"
                    @error="onLogoError($event, client.fallback)"
                  />
                </span>
                <span class="client-logo__name">{{ client.name }}</span>
              </a>
            </div>
          </div>
        </div>

        <div class="clients__marquee clients__marquee--left">
          <div class="clients__track">
            <div
              v-for="copy in 2"
              :key="`bottom-${copy}`"
              class="clients__group"
              :aria-hidden="copy === 2"
            >
              <a
                v-for="client in bottomClients"
                :key="`${copy}-${client.id}`"
                class="client-logo"
                :class="`client-logo--${client.tone}`"
                href="/clients/"
                :aria-label="client.name"
              >
                <span class="client-logo__mark">
                  <img
                    :src="client.src"
                    :alt="client.name"
                    loading="lazy"
                    decoding="async"
                    @error="onLogoError($event, client.fallback)"
                  />
                </span>
                <span class="client-logo__name">{{ client.name }}</span>
              </a>
            </div>
          </div>
        </div>
      </div>

      <div class="clients__footer">
        <div class="clients__stat">
          <strong>99.9%</strong>
          <span>business email uptime</span>
        </div>
        <a class="clients__button" href="/clients/">
          View all clients
          <span aria-hidden="true">→</span>
        </a>
        <div class="clients__stat">
          <strong>24/7</strong>
          <span>secure mail protection</span>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
* {
  box-sizing: border-box;
}

.clients {
  --ink: #102f35;
  --muted: #65787e;
  --blue: #61b8ff;
  --mint: #39dcc2;
  --green: #8bd65a;
  --yellow: #e8ef8a;
  position: relative;
  width: 100%;
  overflow: hidden;
  color: var(--ink);
  background:
    radial-gradient(
      circle at 11% 17%,
      rgba(97, 184, 255, 0.22),
      transparent 30%
    ),
    radial-gradient(
      circle at 88% 76%,
      rgba(57, 220, 194, 0.25),
      transparent 32%
    ),
    linear-gradient(112deg, #f5f8ff 0%, #ffffff 47%, #edfdf8 100%);
  isolation: isolate;
}

.clients::before {
  position: absolute;
  inset: 0;
  z-index: -2;
  background-image:
    linear-gradient(rgba(16, 47, 53, 0.035) 1px, transparent 1px),
    linear-gradient(90deg, rgba(16, 47, 53, 0.035) 1px, transparent 1px);
  background-size: clamp(34px, 3vw, 54px) clamp(34px, 3vw, 54px);
  mask-image: linear-gradient(
    to bottom,
    transparent 0%,
    #000 18%,
    #000 82%,
    transparent 100%
  );
  content: "";
}

.clients__inner {
  position: relative;
  width: min(100%, 1840px);
  margin: 0 auto;
  padding: clamp(74px, 7.4vw, 124px) 0 clamp(62px, 6.4vw, 104px);
}

.clients__header {
  width: min(88vw, 820px);
  margin: 0 auto clamp(44px, 5vw, 74px);
  text-align: center;
  opacity: 0;
  transform: translateY(22px);
  transition:
    opacity 0.75s ease,
    transform 0.75s ease;
}

.clients.is-visible .clients__header {
  opacity: 1;
  transform: translateY(0);
}

.clients__eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 9px;
  margin-bottom: clamp(13px, 1.4vw, 18px);
  padding: 8px 13px;
  border: 1px solid rgba(57, 220, 194, 0.24);
  border-radius: 999px;
  color: #087e70;
  background: rgba(255, 255, 255, 0.72);
  box-shadow: 0 12px 28px rgba(20, 82, 86, 0.06);
  font-size: clamp(9px, 0.7vw, 12px);
  font-weight: 850;
  letter-spacing: 0.16em;
  text-transform: uppercase;
}

.clients__eyebrow i {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--blue), var(--mint));
  box-shadow: 0 0 0 5px rgba(57, 220, 194, 0.14);
}

.clients__header h2 {
  max-width: 780px;
  margin: 0 auto;
  font-size: clamp(38px, 4.8vw, 58px);
  font-weight: 450;
  line-height: 0.98;
  letter-spacing: -0.06em;
}

.clients__header p {
  max-width: 640px;
  margin: clamp(15px, 1.5vw, 22px) auto 0;
  color: var(--muted);
  font-size: clamp(14px, 1.05vw, 17px);
  font-weight: 520;
  line-height: 1.7;
}

.clients__marquees {
  display: grid;
  gap: clamp(14px, 1.4vw, 22px);
  opacity: 0;
  transform: translateY(18px);
  transition:
    opacity 0.75s ease 0.18s,
    transform 0.75s ease 0.18s;
}

.clients.is-visible .clients__marquees {
  opacity: 1;
  transform: translateY(0);
}

.clients__marquee {
  width: 100%;
  overflow: hidden;
  padding-block: 4px;
  mask-image: linear-gradient(
    90deg,
    transparent,
    #000 7%,
    #000 93%,
    transparent
  );
}

.clients__track {
  display: flex;
  width: max-content;
  will-change: transform;
}

.clients__group {
  display: flex;
  flex-shrink: 0;
  gap: clamp(12px, 1.25vw, 20px);
  padding-right: clamp(12px, 1.25vw, 20px);
}

.clients.is-visible .clients__marquee--left .clients__track {
  animation: marquee-left 54s linear infinite;
}

.clients.is-visible .clients__marquee--right .clients__track {
  animation: marquee-right 54s linear infinite;
}

.clients__marquee:hover .clients__track {
  animation-play-state: paused;
}

.client-logo {
  position: relative;
  display: flex;
  width: clamp(214px, 16vw, 286px);
  min-height: clamp(78px, 6vw, 96px);
  flex: 0 0 auto;
  align-items: center;
  gap: clamp(12px, 1.1vw, 17px);
  padding: clamp(14px, 1.2vw, 18px) clamp(16px, 1.5vw, 24px);
  overflow: hidden;
  border: 1px solid rgba(16, 47, 53, 0.075);
  border-radius: clamp(18px, 1.5vw, 26px);
  color: var(--ink);
  background: rgba(255, 255, 255, 0.82);
  box-shadow:
    0 18px 45px rgba(18, 61, 66, 0.08),
    inset 0 1px 0 rgba(255, 255, 255, 0.84);
  text-decoration: none;
  transform: translateZ(0);
  transition:
    transform 0.28s ease,
    border-color 0.28s ease,
    box-shadow 0.28s ease,
    background 0.28s ease;
}

.client-logo::before {
  position: absolute;
  inset: -1px;
  z-index: -1;
  opacity: 0;
  transition: opacity 0.28s ease;
  content: "";
}

.client-logo--mint::before {
  background: linear-gradient(
    135deg,
    rgba(57, 220, 194, 0.18),
    transparent 58%
  );
}

.client-logo--blue::before {
  background: linear-gradient(135deg, rgba(97, 184, 255, 0.2), transparent 58%);
}

.client-logo--green::before {
  background: linear-gradient(
    135deg,
    rgba(139, 214, 90, 0.22),
    transparent 58%
  );
}

.client-logo--lime::before {
  background: linear-gradient(
    135deg,
    rgba(213, 235, 109, 0.25),
    transparent 58%
  );
}

.client-logo--aqua::before {
  background: linear-gradient(
    135deg,
    rgba(106, 238, 226, 0.22),
    transparent 58%
  );
}

.client-logo--yellow::before {
  background: linear-gradient(
    135deg,
    rgba(232, 239, 138, 0.28),
    transparent 58%
  );
}

.client-logo:hover {
  z-index: 3;
  border-color: rgba(57, 220, 194, 0.3);
  background: rgba(255, 255, 255, 0.96);
  box-shadow:
    0 24px 56px rgba(18, 73, 76, 0.14),
    inset 0 1px 0 rgba(255, 255, 255, 0.94);
  transform: translateY(-6px) scale(1.015);
}

.client-logo:hover::before {
  opacity: 1;
}

.client-logo__mark {
  display: grid;
  width: clamp(44px, 3.5vw, 58px);
  height: clamp(44px, 3.5vw, 58px);
  flex: 0 0 auto;
  place-items: center;
  border: 1px solid rgba(16, 47, 53, 0.075);
  border-radius: 17px;
  background:
    radial-gradient(
      circle at 34% 22%,
      rgba(255, 255, 255, 0.96),
      transparent 42%
    ),
    linear-gradient(145deg, #eefeff, #eef8f0);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.9);
}

.client-logo__mark img {
  display: block;
  width: 66%;
  height: 66%;
  object-fit: contain;
  filter: saturate(1.2) contrast(1.02);
}

.client-logo__name {
  display: block;
  min-width: 0;
  overflow: hidden;
  color: #17373d;
  font-size: clamp(15px, 1.1vw, 19px);
  font-weight: 760;
  letter-spacing: -0.04em;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.clients__footer {
  display: flex;
  width: min(88vw, 860px);
  align-items: center;
  justify-content: center;
  gap: clamp(18px, 3vw, 48px);
  margin: clamp(44px, 5vw, 72px) auto 0;
  opacity: 0;
  transform: translateY(16px);
  transition:
    opacity 0.7s ease 0.35s,
    transform 0.7s ease 0.35s;
}

.clients.is-visible .clients__footer {
  opacity: 1;
  transform: translateY(0);
}

.clients__stat {
  min-width: 118px;
  text-align: center;
}

.clients__stat strong,
.clients__stat span {
  display: block;
}

.clients__stat strong {
  color: var(--ink);
  font-size: clamp(20px, 1.8vw, 30px);
  font-weight: 850;
  letter-spacing: -0.05em;
}

.clients__stat span {
  margin-top: 4px;
  color: var(--muted);
  font-size: clamp(11px, 0.82vw, 13px);
  font-weight: 650;
}

.clients__button {
  display: inline-flex;
  min-height: clamp(48px, 3.8vw, 58px);
  align-items: center;
  gap: 12px;
  padding: 8px 8px 8px clamp(20px, 1.5vw, 26px);
  border: 1px solid rgba(255, 255, 255, 0.7);
  border-radius: 999px;
  color: #fff;
  background: linear-gradient(120deg, #113941, #0aa994);
  box-shadow: 0 18px 38px rgba(15, 88, 91, 0.22);
  font-size: clamp(13px, 0.92vw, 15px);
  font-weight: 820;
  text-decoration: none;
  white-space: nowrap;
  transition:
    transform 0.25s ease,
    box-shadow 0.25s ease;
}

.clients__button span {
  display: grid;
  width: clamp(34px, 2.7vw, 42px);
  height: clamp(34px, 2.7vw, 42px);
  place-items: center;
  border-radius: 50%;
  color: #113941;
  background: linear-gradient(135deg, #e8ef8a, #ffffff);
}

.clients__button:hover {
  box-shadow: 0 22px 46px rgba(15, 88, 91, 0.3);
  transform: translateY(-3px);
}

.clients__orb {
  position: absolute;
  z-index: -3;
  width: clamp(340px, 38vw, 720px);
  aspect-ratio: 1;
  border-radius: 50%;
  filter: blur(42px);
  opacity: 0.5;
  pointer-events: none;
  animation: float-orb 12s ease-in-out infinite alternate;
}

.clients__orb--left {
  top: -34%;
  left: -18%;
  background: rgba(97, 184, 255, 0.3);
}

.clients__orb--right {
  right: -16%;
  bottom: -38%;
  background: rgba(57, 220, 194, 0.34);
  animation-delay: -5s;
}

@keyframes marquee-left {
  to {
    transform: translateX(-50%);
  }
}

@keyframes marquee-right {
  from {
    transform: translateX(-50%);
  }

  to {
    transform: translateX(0);
  }
}

@keyframes float-orb {
  to {
    transform: translate3d(5%, 4%, 0) scale(1.08);
  }
}

@media (max-width: 760px) {
  .clients__inner {
    padding-block: 64px 58px;
  }

  .clients__header {
    margin-bottom: 36px;
  }

  .clients__header h2 {
    font-size: clamp(36px, 11vw, 54px);
  }

  .clients__header p {
    font-size: 14px;
  }

  .clients__marquees {
    gap: 10px;
  }

  .client-logo {
    width: 205px;
    min-height: 76px;
    border-radius: 18px;
  }

  .clients.is-visible .clients__marquee--left .clients__track,
  .clients.is-visible .clients__marquee--right .clients__track {
    animation-duration: 42s;
  }

  .clients__footer {
    flex-direction: column;
    gap: 16px;
    margin-top: 38px;
  }

  .clients__stat {
    min-width: 0;
  }
}

@media (max-width: 460px) {
  .clients__marquee {
    mask-image: linear-gradient(
      90deg,
      transparent,
      #000 4%,
      #000 96%,
      transparent
    );
  }

  .client-logo {
    width: 190px;
    min-height: 72px;
    padding: 13px 15px;
  }

  .client-logo__name {
    font-size: 14px;
  }
}

@media (prefers-reduced-motion: reduce) {
  .clients__orb,
  .clients__track {
    animation: none !important;
  }

  .clients__header,
  .clients__marquees,
  .clients__footer {
    opacity: 1;
    transform: none;
    transition: none;
  }
}
</style>
