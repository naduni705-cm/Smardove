<script setup>
import { onBeforeUnmount, onMounted, ref } from "vue";

const menuOpen = ref(false);
const scrolled = ref(false);

const links = [
  { label: "Home", href: "/" },
  { label: "Pricing", href: "/pricing/" },
  { label: "Features", href: "/#features" },
  { label: "Resources", href: "/blog/" },
  { label: "Switch to Smardove", href: "/switch-to-smardove/" },
  { label: "About", href: "/about/" },
];

const updateNavbar = () => {
  scrolled.value = window.scrollY > 40;
};

onMounted(() => {
  updateNavbar();
  window.addEventListener("scroll", updateNavbar, { passive: true });
});

onBeforeUnmount(() => window.removeEventListener("scroll", updateNavbar));
</script>

<template>
  <section class="email-hero" aria-labelledby="hero-title">
    <!-- Teleport prevents the hero overflow from hiding the sticky navbar. -->
    <Teleport to="body">
      <nav
        class="hero-nav"
        :class="{ 'hero-nav--scrolled': scrolled }"
        aria-label="Main navigation"
      >
        <a class="hero-nav__brand" href="/" aria-label="Smardove home">
          <img src="/images/logo.png" alt="" />
          <strong>Smardove</strong>
        </a>

        <div
          class="hero-nav__links"
          :class="{ 'hero-nav__links--open': menuOpen }"
        >
          <a
            v-for="link in links"
            :key="link.label"
            :href="link.href"
            @click="menuOpen = false"
          >
            {{ link.label }}
          </a>
          <a class="hero-nav__mobile-login" href="/login/">Email Login</a>
        </div>

        <a class="hero-nav__login" href="/login/">
          <span>Email Login</span>
          <i aria-hidden="true">↗</i>
        </a>

        <button
          class="hero-nav__toggle"
          type="button"
          :aria-expanded="menuOpen"
          aria-label="Toggle navigation"
          @click="menuOpen = !menuOpen"
        >
          <span></span><span></span>
        </button>
      </nav>
    </Teleport>

    <img
      class="email-hero__background"
      src="/images/1.png"
      alt="Professional using secure Smardove business email"
    />
    <div class="email-hero__wash" aria-hidden="true"></div>
    <div class="email-hero__shade" aria-hidden="true"></div>

    <header class="email-hero__heading">
      <span class="email-hero__eyebrow"><i></i> SMARDOVE MAIL</span>
      <h1 id="hero-title">
        Business email,
        <!-- <strong>beautifully simple.</strong> -->
      </h1>
      <p>Secure email and effortless teamwork for modern businesses.</p>

      <div class="email-hero__actions">
        <a class="hero-button hero-button--primary" href="/get-started/">
          Start for free <i aria-hidden="true">→</i>
        </a>
        <a class="hero-button hero-button--secondary" href="/#features">
          Explore features
        </a>
      </div>
    </header>

    <div class="email-hero__cards">
      <a class="service-card service-card--email" href="/business-email">
        <div class="service-card__top">
          <div>
            <span>PROFESSIONAL EMAIL</span>
            <h2>Business Email</h2>
            <p>Secure email for your business.</p>
          </div>
          <i class="service-card__arrow" aria-hidden="true">›</i>
        </div>

        <div class="mail-preview" aria-hidden="true">
          <div class="preview-bar">
            <i></i><i></i><i></i><span>mail.smardove.com</span>
          </div>
          <div class="mail-preview__body">
            <div class="mail-preview__side"><b>S</b><i></i><i></i><i></i></div>
            <div class="mail-preview__inbox">
              <small>Good morning</small>
              <strong>Primary inbox</strong>
              <div class="message message--active">
                <b>AM</b
                ><span
                  ><strong>New business proposal</strong
                  ><small>Project details are ready</small></span
                ><i>Now</i>
              </div>
              <div class="message">
                <b>SK</b
                ><span
                  ><strong>Weekly report</strong
                  ><small>Your performance summary</small></span
                ><i>8m</i>
              </div>
            </div>
          </div>
        </div>
      </a>

      <a class="service-card service-card--workspace" href="/workspace">
        <div class="service-card__top">
          <div>
            <span>CONNECTED TEAMWORK</span>
            <h2>Smardove Workspace</h2>
            <p>Email and teamwork in one place.</p>
          </div>
          <i class="service-card__arrow" aria-hidden="true">›</i>
        </div>

        <div class="workspace-preview" aria-hidden="true">
          <div class="workspace-preview__head">
            <b>NA</b
            ><span
              ><small>Smardove Workspace</small
              ><strong>Marketing Team</strong></span
            ><i>● Live</i>
          </div>
          <div class="workspace-preview__stat">
            <small>Team activity</small><strong>2,486</strong
            ><span>+18.4% this month</span>
          </div>
          <div class="workspace-preview__chart">
            <i style="--h: 34%"></i><i style="--h: 52%"></i
            ><i style="--h: 43%"></i><i style="--h: 69%"></i
            ><i style="--h: 56%"></i><i class="hot" style="--h: 88%"></i
            ><i style="--h: 64%"></i>
          </div>
        </div>
      </a>
    </div>
  </section>
</template>

<style scoped>
* {
  box-sizing: border-box;
}

.email-hero {
  --ink: #0b3036;
  --blue: #e9edff;
  --aqua: #dffbf5;
  --teal: #08a999;
  --lime: #dff36a;
  position: relative;
  width: calc(100% - clamp(20px, 2vw, 38px));
  min-height: clamp(850px, 110svh, 1220px);
  margin: clamp(10px, 1vw, 18px) auto 0;
  overflow: hidden;
  border: 1px solid rgba(11, 48, 54, 0.11);
  border-radius: clamp(22px, 2vw, 36px);
  background: linear-gradient(105deg, #e9edff 0%, #f8fbff 48%, #dffbf5 100%);
  isolation: isolate;
}

.email-hero__background {
  position: absolute;
  inset: 0;
  z-index: -3;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center 38%;
}

.email-hero__wash {
  position: absolute;
  inset: 0;
  z-index: -2;
  background:
    linear-gradient(
      90deg,
      rgba(222, 229, 255, 0.72) 0%,
      rgba(255, 255, 255, 0.12) 49%,
      rgba(207, 252, 243, 0.67) 100%
    ),
    linear-gradient(
      180deg,
      rgba(255, 255, 255, 0.68) 0%,
      rgba(255, 255, 255, 0.06) 44%,
      rgba(18, 61, 58, 0.14) 72%,
      rgba(10, 45, 42, 0.7) 100%
    );
  pointer-events: none;
}

.email-hero__shade {
  position: absolute;
  inset: auto 0 0;
  z-index: -1;
  height: 43%;
  background: linear-gradient(180deg, transparent, rgba(10, 43, 43, 0.58));
  pointer-events: none;
}

.email-hero__heading {
  position: relative;
  z-index: 2;
  width: min(92%, 850px);
  margin: 0 auto;
  padding-top: clamp(120px, 14vh, 170px);
  color: var(--ink);
  text-align: center;
}

.email-hero__heading span {
  display: block;
  margin-bottom: clamp(8px, 1vw, 14px);
  font-size: clamp(9px, 0.68vw, 12px);
  font-weight: 800;
  letter-spacing: 0.18em;
}

.email-hero__eyebrow {
  display: inline-flex !important;
  align-items: center;
  justify-content: center;
  gap: 9px;
  width: auto;
}

.email-hero__eyebrow i {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: var(--teal);
  box-shadow: 0 0 0 5px rgba(8, 169, 153, 0.12);
}

.email-hero__heading h1 {
  margin: 0;
  font-family: inherit;
  font-size: clamp(46px, 5.1vw, 70px);
  font-weight: 200;
  line-height: 0.94;
  letter-spacing: -0.065em;
}

.email-hero__heading h1 strong {
  display: block;
  font: inherit;
  color: var(--ink);
}

.email-hero__heading p {
  max-width: 630px;
  margin: clamp(14px, 1.5vw, 22px) auto 0;
  color: #385b61;
  font-size: clamp(13px, 1vw, 17px);
  line-height: 1.55;
}

.email-hero__actions {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  margin-top: clamp(18px, 2vw, 28px);
}

.hero-button {
  display: inline-flex;
  min-height: 48px;
  align-items: center;
  justify-content: center;
  gap: 13px;
  padding: 10px 20px;
  border: 1px solid rgba(11, 48, 54, 0.14);
  border-radius: 999px;
  color: var(--ink);
  background: rgba(255, 255, 255, 0.62);
  box-shadow: 0 10px 30px rgba(11, 48, 54, 0.08);
  font-size: clamp(12px, 0.84vw, 14px);
  font-weight: 750;
  text-decoration: none;
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  transition:
    transform 0.25s ease,
    box-shadow 0.25s ease;
}

.hero-button--primary {
  padding-right: 7px;
  border-color: var(--ink);
  color: #fff;
  background: var(--ink);
}

.hero-button--primary i {
  display: grid;
  width: 34px;
  height: 34px;
  place-items: center;
  border-radius: 50%;
  color: var(--ink);
  background: linear-gradient(135deg, var(--lime), #8be5c5);
  font-size: 17px;
  font-style: normal;
}

.hero-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 14px 34px rgba(11, 48, 54, 0.14);
}

.email-hero__cards {
  position: absolute;
  z-index: 3;
  left: 50%;
  bottom: clamp(62px, 6vw, 104px);
  transform: translateX(-50%);
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: clamp(4px, 0.45vw, 8px);
  width: min(78%, 1320px);
}

.service-card {
  position: relative;
  min-width: 0;
  height: clamp(290px, 31vw, 430px);
  overflow: hidden;
  padding: clamp(22px, 2.2vw, 38px);
  color: var(--ink);
  text-decoration: none;
  border: 1px solid rgba(255, 255, 255, 0.82);
  border-radius: clamp(22px, 2vw, 34px);
  background: linear-gradient(
    135deg,
    rgba(234, 238, 255, 0.78),
    rgba(255, 255, 255, 0.55)
  );
  box-shadow:
    0 22px 70px rgba(7, 39, 34, 0.18),
    inset 0 1px 0 #fff;
  backdrop-filter: blur(22px) saturate(125%);
  -webkit-backdrop-filter: blur(22px) saturate(125%);
  transition:
    transform 0.35s ease,
    background 0.35s ease,
    box-shadow 0.35s ease;
}

.service-card--workspace {
  background: linear-gradient(
    135deg,
    rgba(255, 255, 255, 0.58),
    rgba(211, 252, 243, 0.76)
  );
}
.service-card:hover {
  transform: translateY(-7px);
  box-shadow:
    0 30px 80px rgba(7, 39, 34, 0.24),
    inset 0 1px 0 #fff;
}

.service-card__top {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 20px;
}
.service-card__top > div {
  min-width: 0;
}
.service-card__top span {
  color: #087f69;
  font-size: clamp(8px, 0.6vw, 11px);
  font-weight: 800;
  letter-spacing: 0.14em;
}
.service-card__top h2 {
  margin: 7px 0 6px;
  font-size: clamp(21px, 1.75vw, 31px);
  line-height: 1.1;
  letter-spacing: -0.04em;
}
.service-card__top p {
  margin: 0;
  color: #49666a;
  font-size: clamp(10px, 0.78vw, 14px);
  line-height: 1.45;
}

.service-card__arrow {
  display: grid;
  flex: 0 0 auto;
  width: clamp(42px, 3.5vw, 60px);
  aspect-ratio: 1;
  place-items: center;
  border-radius: 50%;
  background: #fff;
  box-shadow: 0 8px 24px rgba(10, 48, 54, 0.1);
  font-size: clamp(28px, 2.4vw, 40px);
  font-style: normal;
  font-weight: 300;
  transition:
    transform 0.3s ease,
    background 0.3s ease;
}
.service-card:hover .service-card__arrow {
  transform: translateX(4px);
  background: var(--lime);
}

.mail-preview,
.workspace-preview {
  position: absolute;
  right: clamp(20px, 2.2vw, 38px);
  bottom: -2px;
  left: clamp(20px, 2.2vw, 38px);
  height: 58%;
  overflow: hidden;
  border: 1px solid rgba(11, 48, 54, 0.09);
  border-radius: 16px 16px 0 0;
  background: rgba(255, 255, 255, 0.84);
  box-shadow: 0 14px 35px rgba(11, 48, 54, 0.12);
}

.preview-bar {
  display: flex;
  align-items: center;
  gap: 5px;
  height: 22%;
  padding: 0 14px;
  border-bottom: 1px solid #e9efec;
}
.preview-bar i {
  width: 5px;
  height: 5px;
  border-radius: 50%;
  background: #c4e77b;
}
.preview-bar i:nth-child(2) {
  background: #ffe570;
}
.preview-bar i:nth-child(3) {
  background: #8ee0bf;
}
.preview-bar span {
  margin: auto;
  color: #91a09d;
  font-size: clamp(5px, 0.42vw, 8px);
}
.mail-preview__body {
  display: grid;
  grid-template-columns: 11% 1fr;
  height: 78%;
}
.mail-preview__side {
  display: flex;
  align-items: center;
  flex-direction: column;
  gap: 9px;
  padding-top: 12px;
  border-right: 1px solid #edf0ef;
}
.mail-preview__side b {
  display: grid;
  width: 20px;
  height: 20px;
  place-items: center;
  border-radius: 6px;
  background: var(--ink);
  color: #fff;
  font-size: 8px;
}
.mail-preview__side i {
  width: 12px;
  height: 3px;
  border-radius: 8px;
  background: #dce6e2;
}
.mail-preview__side i:first-of-type {
  background: #33c99d;
}
.mail-preview__inbox {
  padding: 12px;
}
.mail-preview__inbox > small {
  display: block;
  color: #85918f;
  font-size: clamp(5px, 0.42vw, 8px);
}
.mail-preview__inbox > strong {
  display: block;
  margin-bottom: 8px;
  font-size: clamp(8px, 0.65vw, 11px);
}
.message {
  display: grid;
  grid-template-columns: 25px 1fr auto;
  align-items: center;
  gap: 8px;
  margin-bottom: 5px;
  padding: 7px;
  border-radius: 8px;
}
.message--active {
  background: #e8faf3;
}
.message > b {
  display: grid;
  width: 23px;
  height: 23px;
  place-items: center;
  border-radius: 50%;
  background: #d8f6e9;
  color: #14856e;
  font-size: 6px;
}
.message span strong,
.message span small {
  display: block;
  font-size: clamp(5px, 0.45vw, 8px);
}
.message span small,
.message > i {
  color: #8a9996;
  font-size: clamp(4px, 0.36vw, 7px);
  font-style: normal;
}

.workspace-preview {
  padding: clamp(13px, 1.2vw, 20px);
}
.workspace-preview__head {
  display: flex;
  align-items: center;
  gap: 8px;
}
.workspace-preview__head > b {
  display: grid;
  width: 27px;
  height: 27px;
  place-items: center;
  border-radius: 8px;
  color: #fff;
  background: linear-gradient(135deg, #16cfac, #4178ea);
  font-size: 8px;
}
.workspace-preview__head span small,
.workspace-preview__head span strong {
  display: block;
  font-size: clamp(5px, 0.44vw, 8px);
}
.workspace-preview__head span small {
  color: #8ca09b;
}
.workspace-preview__head > i {
  margin-left: auto;
  padding: 5px 9px;
  border-radius: 99px;
  color: #078b6f;
  background: #e3faf1;
  font-size: clamp(5px, 0.4vw, 7px);
  font-style: normal;
}
.workspace-preview__stat {
  margin-top: clamp(12px, 1.2vw, 20px);
}
.workspace-preview__stat small,
.workspace-preview__stat strong,
.workspace-preview__stat span {
  display: block;
}
.workspace-preview__stat small {
  color: #7e918d;
  font-size: clamp(5px, 0.42vw, 8px);
}
.workspace-preview__stat strong {
  font-size: clamp(20px, 1.8vw, 30px);
}
.workspace-preview__stat span {
  color: #0aa17f;
  font-size: clamp(5px, 0.42vw, 8px);
}
.workspace-preview__chart {
  position: absolute;
  right: 18px;
  bottom: 0;
  left: 18px;
  display: flex;
  align-items: flex-end;
  gap: 3%;
  height: 46%;
}
.workspace-preview__chart i {
  width: 12%;
  height: var(--h);
  border-radius: 5px 5px 0 0;
  background: #bfead0;
}
.workspace-preview__chart .hot {
  background: linear-gradient(180deg, #39d8a4, #3e70ef);
}

.hero-nav {
  position: fixed;
  z-index: 9999;
  top: clamp(14px, 2vw, 28px);
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  align-items: center;
  width: min(92%, 1080px);
  min-height: clamp(58px, 5vw, 72px);
  padding: 7px 9px 7px clamp(16px, 2vw, 28px);
  border: 1px solid rgba(255, 255, 255, 0.82);
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.42);
  box-shadow:
    0 14px 40px rgba(54, 75, 105, 0.12),
    inset 0 1px 0 rgba(255, 255, 255, 0.92);
  backdrop-filter: blur(18px) saturate(140%);
  -webkit-backdrop-filter: blur(18px) saturate(140%);
  transition:
    top 0.3s ease,
    width 0.3s ease,
    background 0.3s ease,
    box-shadow 0.3s ease;
}
.hero-nav--scrolled {
  top: 10px;
  width: min(94%, 1160px);
  border-color: rgba(255, 255, 255, 0.9);
  background: linear-gradient(
    100deg,
    rgba(226, 233, 255, 0.96),
    rgba(221, 252, 246, 0.96)
  );
  box-shadow: 0 15px 45px rgba(45, 76, 95, 0.2);
}
.hero-nav__brand {
  display: flex;
  align-items: center;
  gap: 9px;
  color: var(--ink);
  text-decoration: none;
}
.hero-nav__brand img {
  width: clamp(28px, 2.4vw, 38px);
  height: auto;
  filter: none;
}
.hero-nav__brand strong {
  font-size: clamp(18px, 1.45vw, 24px);
  letter-spacing: -0.04em;
}
.hero-nav__links {
  display: flex;
  align-items: center;
  gap: clamp(13px, 1.5vw, 25px);
  margin: auto;
}
.hero-nav__links a {
  color: rgba(11, 48, 54, 0.82);
  font-size: clamp(12px, 0.92vw, 16px);
  font-weight: 650;
  text-decoration: none;
  white-space: nowrap;
}
.hero-nav__links a:hover {
  color: var(--lime);
}

.hero-nav__links a:focus-visible,
.hero-nav__brand:focus-visible,
.hero-nav__login:focus-visible,
.hero-button:focus-visible,
.service-card:focus-visible,
.hero-nav__toggle:focus-visible {
  outline: 3px solid rgba(8, 169, 153, 0.42);
  outline-offset: 3px;
}
.hero-nav__login {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 5px 6px 5px clamp(16px, 1.4vw, 22px);
  border-radius: 999px;
  border: 1px solid rgba(255, 255, 255, 0.84);
  background: linear-gradient(
    100deg,
    rgba(229, 235, 255, 0.82),
    rgba(214, 250, 242, 0.84)
  );
  color: var(--ink);
  font-size: clamp(12px, 0.85vw, 15px);
  font-weight: 700;
  text-decoration: none;
  white-space: nowrap;
}
.hero-nav__login i {
  display: grid;
  width: clamp(38px, 3vw, 48px);
  aspect-ratio: 1;
  place-items: center;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.94);
  color: var(--ink);
  font-size: 17px;
  font-style: normal;
}
.hero-nav__toggle,
.hero-nav__mobile-login {
  display: none;
}

@media (max-width: 1040px) {
  .hero-nav__links {
    gap: 13px;
  }
  .hero-nav__links a {
    font-size: 12px;
  }
  .email-hero__cards {
    width: 88%;
  }
}

/* Smaller laptops: preserve the desktop composition without oversized content. */
@media (min-width: 901px) and (max-width: 1366px) {
  .email-hero {
    min-height: clamp(740px, 100svh, 900px);
  }

  .email-hero__background {
    object-position: center 42%;
  }

  .email-hero__heading {
    width: min(88%, 700px);
    padding-top: clamp(122px, 15vh, 148px);
  }

  .email-hero__heading h1 {
    font-size: clamp(48px, 5.4vw, 68px);
  }

  .email-hero__heading p {
    font-size: clamp(12px, 1vw, 14px);
  }

  .email-hero__cards {
    bottom: clamp(24px, 3.2vw, 44px);
    width: min(84%, 1060px);
  }

  .service-card {
    height: clamp(270px, 28vw, 350px);
    padding: clamp(20px, 2vw, 28px);
    border-radius: clamp(20px, 2vw, 28px);
  }

  .service-card__top h2 {
    font-size: clamp(20px, 1.8vw, 26px);
  }

  .mail-preview,
  .workspace-preview {
    right: clamp(18px, 2vw, 28px);
    left: clamp(18px, 2vw, 28px);
    height: 57%;
  }

  .hero-nav {
    width: min(90%, 1040px);
    min-height: 62px;
  }

  .hero-nav--scrolled {
    width: min(92%, 1080px);
  }

  .hero-nav__brand strong {
    font-size: clamp(18px, 1.65vw, 22px);
  }

  .hero-nav__links {
    gap: clamp(11px, 1.25vw, 18px);
  }

  .hero-nav__links a {
    font-size: clamp(11px, 0.92vw, 13px);
  }

  .hero-nav__login {
    font-size: 12px;
  }
}

@media (max-width: 900px) {
  .email-hero {
    min-height: 1120px;
  }
  .email-hero__background {
    object-position: 58% center;
  }
  .email-hero__heading {
    padding-top: 120px;
  }
  .email-hero__heading h1 {
    font-size: clamp(43px, 10vw, 68px);
  }
  .email-hero__heading p {
    max-width: 520px;
  }
  .email-hero__cards {
    bottom: 20px;
    grid-template-columns: 1fr;
    width: min(92%, 540px);
  }
  .service-card {
    height: 270px;
    padding: 22px;
  }
  .mail-preview,
  .workspace-preview {
    left: 22px;
    right: 22px;
  }
  .hero-nav {
    justify-content: space-between;
  }
  .hero-nav__links {
    position: fixed;
    top: calc(100% + 10px);
    right: 0;
    left: 0;
    display: none;
    flex-direction: column;
    align-items: stretch;
    gap: 0;
    padding: 12px;
    border: 1px solid rgba(255, 255, 255, 0.35);
    border-radius: 22px;
    background: linear-gradient(
      135deg,
      rgba(231, 236, 255, 0.98),
      rgba(218, 252, 245, 0.98)
    );
    box-shadow: 0 18px 45px rgba(4, 27, 30, 0.25);
  }
  .hero-nav__links--open {
    display: flex;
  }
  .hero-nav__links a {
    padding: 12px 14px;
    border-radius: 12px;
    font-size: 14px;
  }
  .hero-nav__links a:hover {
    background: rgba(255, 255, 255, 0.62);
  }
  .hero-nav__login {
    margin-left: auto;
    margin-right: 8px;
  }
  .hero-nav__toggle {
    display: grid;
    width: 42px;
    height: 42px;
    place-items: center;
    border: 0;
    border-radius: 50%;
    background: rgba(255, 255, 255, 0.72);
  }
  .hero-nav__toggle span {
    grid-area: 1/1;
    width: 17px;
    height: 1.5px;
    background: var(--ink);
    transform: translateY(-3px);
  }
  .hero-nav__toggle span:last-child {
    transform: translateY(3px);
  }
  .hero-nav__mobile-login {
    display: none !important;
  }
}

@media (max-width: 540px) {
  .email-hero {
    width: calc(100% - 12px);
    min-height: 1080px;
    border-radius: 20px;
  }
  .email-hero__background {
    object-position: 61% center;
  }
  .email-hero__heading {
    padding-top: 112px;
  }
  .email-hero__heading h1 {
    font-size: clamp(40px, 12vw, 56px);
  }
  .email-hero__heading p {
    width: 82%;
  }
  .email-hero__actions {
    width: min(92%, 340px);
    margin-right: auto;
    margin-left: auto;
  }
  .hero-button {
    flex: 1;
    min-height: 44px;
    padding: 8px 12px;
    white-space: nowrap;
  }
  .hero-button--primary {
    padding-right: 5px;
  }
  .hero-button--primary i {
    width: 32px;
    height: 32px;
  }
  .email-hero__cards {
    gap: 7px;
  }
  .service-card {
    height: 245px;
    border-radius: 20px;
  }
  .service-card__top p {
    max-width: 240px;
  }
  .hero-nav {
    top: 8px;
    width: calc(100% - 24px);
    min-height: 56px;
    padding-left: 16px;
  }
  .hero-nav__brand strong {
    font-size: 18px;
  }
  .hero-nav__login {
    padding-left: 12px;
  }
  .hero-nav__login span {
    font-size: 11px;
  }
  .hero-nav__login i {
    width: 34px;
  }
}

@media (prefers-reduced-motion: reduce) {
  .service-card,
  .service-card__arrow,
  .hero-nav {
    transition: none;
  }
}
</style>
