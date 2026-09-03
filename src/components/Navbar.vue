<script setup>
import { ref } from 'vue'

const links = [
  { label: 'Home', href: 'https://smardove.com/', active: true },
  { label: 'Pricing', href: 'https://smardove.com/pricing/' },
  { label: 'Features', href: 'https://smardove.com/#' },
  { label: 'Resources & Support', href: 'https://smardove.com/#' },
  { label: 'Switch to Smardove', href: 'https://smardove.com/switch-to-smardove/' },
  { label: 'Clients', href: 'https://smardove.com/clients/' },
  { label: 'Blog', href: 'https://smardove.com/blog/' },
  { label: 'About', href: 'https://smardove.com/about/' },
  { label: 'Contact', href: 'https://smardove.com/contact/' }
]

const menuOpen = ref(false)
</script>

<template>
  <header class="navbar">
    <div class="navbar__inner">
      <a class="navbar__logo" href="https://smardove.com/">
        <img class="navbar__logo-img" src="/images/logo.png" alt="Smardove" />
      </a>

      <nav class="navbar__links" :class="{ 'navbar__links--open': menuOpen }">
        <a
          v-for="link in links"
          :key="link.label"
          :href="link.href"
          class="navbar__link"
          :class="{ 'navbar__link--active': link.active }"
        >
          {{ link.label }}
        </a>
      </nav>

      <div class="navbar__actions">
        <a href="https://smardove.com/login/" class="navbar__cta">Email Login</a>
        <button
          class="navbar__toggle"
          type="button"
          :aria-expanded="menuOpen"
          aria-label="Toggle navigation"
          @click="menuOpen = !menuOpen"
        >
          <svg v-if="!menuOpen" viewBox="0 0 24 24">
            <path d="M4 7h16M4 12h16M4 17h16" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" />
          </svg>
          <svg v-else viewBox="0 0 24 24">
            <path d="M6 6l12 12M18 6L6 18" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" />
          </svg>
        </button>
      </div>
    </div>
  </header>
</template>

<style scoped>
.navbar {
  position: sticky;
  top: 0;
  z-index: 50;
  width: 100%;
  background: rgba(255, 255, 255, 0.85);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border-bottom: 1px solid var(--line);
}

.navbar__inner {
  max-width: 1700px;
  width: 92vw;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: clamp(16px, 2vw, 32px);
  padding: clamp(12px, 1.4vw, 18px) 0;
}

.navbar__logo {
  display: flex;
  align-items: center;
  gap: 8px;
  text-decoration: none;
  color: var(--ink);
  flex-shrink: 0;
}
.navbar__logo-img {
  height: clamp(26px, 2.2vw, 34px);
  width: auto;
  display: block;
}

.navbar__links {
  display: flex;
  align-items: center;
  gap: clamp(14px, 1.6vw, 28px);
  flex-wrap: wrap;
}

.navbar__link {
  font-size: clamp(12px, 0.9vw, 14.5px);
  font-weight: 500;
  color: var(--sub);
  text-decoration: none;
  white-space: nowrap;
  transition: color 0.15s ease;
}
.navbar__link:hover {
  color: var(--ink);
}
.navbar__link--active {
  color: var(--ink);
  font-weight: 600;
}

.navbar__actions {
  display: flex;
  align-items: center;
  gap: clamp(10px, 1vw, 16px);
  flex-shrink: 0;
}

.navbar__cta {
  font-size: clamp(12px, 0.9vw, 14px);
  font-weight: 500;
  border-radius: 999px;
  padding: clamp(9px, 0.85vw, 12px) clamp(18px, 1.6vw, 24px);
  background: var(--ink);
  color: #fff;
  text-decoration: none;
  white-space: nowrap;
}

.navbar__toggle {
  display: none;
  width: clamp(32px, 2.6vw, 38px);
  height: clamp(32px, 2.6vw, 38px);
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  border: 1px solid var(--line);
  background: #fff;
  color: var(--ink);
  cursor: pointer;
}
.navbar__toggle svg {
  width: 60%;
  height: 60%;
}

@media (max-width: 900px) {
  .navbar__links {
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background: #fff;
    border-bottom: 1px solid var(--line);
    flex-direction: column;
    align-items: flex-start;
    gap: 4px;
    padding: 12px 4vw 18px;
    display: none;
  }
  .navbar__links--open {
    display: flex;
  }
  .navbar__link {
    width: 100%;
    padding: 10px 0;
    border-bottom: 1px solid var(--line);
  }
  .navbar__toggle {
    display: flex;
  }
}
</style>