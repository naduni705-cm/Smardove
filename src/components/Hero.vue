<script setup>
import { ref } from 'vue'
import ChartSVG from './ChartSVG.vue'

const accounts = ref([
  { icon: '$', bg: '#e9e9ea', color: '#3d3d40', label: 'Main account, USD', amount: '$51,206.40' },
  { icon: '€', bg: '#d9e6f5', color: '#2c6bb0', label: 'Saving, EUR', amount: '€25,603.20' },
  { icon: '◈', bg: '#2c7fd1', color: '#fff', label: 'Ton', amount: '19,202.40 TON' },
  { icon: '₿', bg: '#e79b1f', color: '#fff', label: 'Bitcoin wallet', amount: '15,392.50 BTC' },
  { icon: '£', bg: '#eadfce', color: '#8a6a34', label: 'Saving, GBP', amount: '£12,801.25' }
])

const transactions = ref([
  { name: 'Square Inc.', date: '30 Jan', amount: '+ $2,503.40', pos: true, dir: 'down' },
  { name: 'Orange, Inc', date: '30 Jan', amount: '- $515.50', pos: false, dir: 'up' },
  { name: 'Google', date: '28 Jan', amount: '- $1000.00', pos: false, dir: 'up' },
  { name: 'Amazon', date: '28 Jan', amount: '- $289.00', pos: false, dir: 'up' },
  { name: 'Square Inc.', date: '27 Jan', amount: '+ $1,499.20', pos: true, dir: 'down' }
])

const months = ['Sep', 'Oct', 'Nov', 'Dec', 'Jan', 'Feb']
</script>

<template>
  <section class="hero">
    <div class="glow glow--left"></div>
    <div class="glow glow--mid"></div>
    <div class="glow glow--right"></div>

    <div class="hero__head">
      <h1 class="hero__title">
        <mark>Boost Your Revenue</mark><br />
        with Tailored Financial Tools
      </h1>
      <p class="hero__subtitle">
        All-in-one solutions for global scaling: payments, crypto, and corporate cards*
      </p>
      <div class="hero__ctas">
        <button class="btn btn--primary">Open Account</button>
        <button class="btn btn--ghost">Let's Chat</button>
      </div>
    </div>

    <div class="stage">
      <div class="panel main-panel">
        <aside class="sidebar">
          <div class="sidebar__org">
            <div class="avatar">A</div>
            <span>Ant Corp.</span>
            <svg class="chev" viewBox="0 0 24 24"><path d="M6 9l6 6 6-6" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
          </div>
          <div class="sidebar__cta">Send Money</div>
          <nav class="nav">
            <div class="nav-item active">
              <svg class="ic" viewBox="0 0 24 24"><rect x="3" y="4" width="18" height="4" rx="1" fill="none" stroke="currentColor" stroke-width="1.6"/><rect x="3" y="10" width="18" height="4" rx="1" fill="none" stroke="currentColor" stroke-width="1.6"/><rect x="3" y="16" width="18" height="4" rx="1" fill="none" stroke="currentColor" stroke-width="1.6"/></svg>
              Overview
            </div>
            <div class="nav-item">
              <svg class="ic" viewBox="0 0 24 24"><path d="M3 10l9-6 9 6" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/><path d="M5 10v9h14v-9" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/><path d="M9 19v-6h6v6" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/></svg>
              Banking
              <svg class="chev" viewBox="0 0 24 24"><path d="M18 15l-6-6-6 6" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
            </div>
            <div class="nav-sub">
              <div>Accounts</div>
              <div>Transactions</div>
            </div>
            <div class="nav-item">
              <svg class="ic" viewBox="0 0 24 24"><rect x="2" y="5" width="20" height="14" rx="2.5" fill="none" stroke="currentColor" stroke-width="1.6"/><path d="M2 10h20" stroke="currentColor" stroke-width="1.6"/></svg>
              Cards
            </div>
            <div class="nav-item">
              <svg class="ic" viewBox="0 0 24 24"><circle cx="12" cy="12" r="9" fill="none" stroke="currentColor" stroke-width="1.6"/><path d="M9.5 9.2c0-1 .9-1.7 2.3-1.7 1.5 0 2.4.7 2.4 1.8 0 2.4-3.6 1.6-3.6 4h4" fill="none" stroke="currentColor" stroke-width="1.4" stroke-linecap="round"/><path d="M9 16h5" stroke="currentColor" stroke-width="1.4" stroke-linecap="round"/></svg>
              Crypto
            </div>
            <div class="nav-item">
              <svg class="ic" viewBox="0 0 24 24"><circle cx="12" cy="12" r="9" fill="none" stroke="currentColor" stroke-width="1.6"/><path d="M12 7v5l3.5 2" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/></svg>
              Payroll
            </div>
          </nav>
          <div class="sidebar__logo">S</div>
        </aside>

        <div class="content">
          <h2>Overview</h2>

          <div class="card balance-card">
            <div class="card__top">
              <div>
                <div class="card__label">Total balance</div>
                <div class="card__value">$128,016<small>.00</small></div>
              </div>
              <div class="pill">
                Half a year
                <svg viewBox="0 0 24 24"><path d="M6 9l6 6 6-6" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
              </div>
            </div>
            <div class="chart-wrap">
              <ChartSVG color="#8b8f95" fill-id="grad-main" />
            </div>
            <div class="chart-labels">
              <span v-for="m in months" :key="m">{{ m }}</span>
            </div>
          </div>

          <div class="two-col">
            <div class="col">
              <h3>Accounts</h3>
              <div class="row" v-for="a in accounts" :key="a.label">
                <div class="row__left">
                  <div class="row__icon" :style="{ background: a.bg, color: a.color }">{{ a.icon }}</div>
                  <div class="row__text"><div class="name">{{ a.label }}</div></div>
                </div>
                <div class="row__amount">{{ a.amount }}</div>
              </div>
            </div>
            <div class="col">
              <h3>Recent transaction</h3>
              <div class="row" v-for="t in transactions" :key="t.name + t.date + t.amount">
                <div class="row__left">
                  <div class="row__icon row__icon--muted">
                    <svg v-if="t.dir === 'down'" viewBox="0 0 24 24"><path d="M12 5v14M6 13l6 6 6-6" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/></svg>
                    <svg v-else viewBox="0 0 24 24"><path d="M7 17L17 7M8 7h9v9" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/></svg>
                  </div>
                  <div class="row__text">
                    <div class="name">{{ t.name }}</div>
                    <div class="sub">{{ t.date }}</div>
                  </div>
                </div>
                <div class="row__amount" :class="{ pos: t.pos }">{{ t.amount }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="panel income-card">
        <div class="toggle">
          <span class="active">Income</span>
          <span>Money spent</span>
        </div>
        <div class="card__top">
          <div class="card__value">$94,422<small>.00</small></div>
          <div class="pill">
            Half a year
            <svg viewBox="0 0 24 24"><path d="M6 9l6 6 6-6" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></svg>
          </div>
        </div>
        <div class="chart-wrap">
          <ChartSVG color="#6b7280" fill-id="grad-income" />
        </div>
        <div class="chart-labels">
          <span v-for="m in months" :key="m">{{ m }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
* {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
.hero {
  position: relative;
  width: 100%;
  padding: clamp(48px, 6vw, 96px) clamp(16px, 4vw, 64px) clamp(80px, 10vw, 160px);
  overflow: hidden;
  isolation: isolate;
}

/* soft corner glows — mesh-gradient wash matching the reference */
.glow {
  position: absolute;
  z-index: -1;
  filter: blur(clamp(45px, 5.5vw, 100px));
  pointer-events: none;
}
.glow--left {
  left: -14vw;
  bottom: -20vh;
  width: 46vw;
  height: 62vh;
  opacity: 0.6;
  background: radial-gradient(
    ellipse at 40% 60%,
    #bfe396 0%,
    #cdea9f 35%,
    rgba(205, 234, 159, 0.4) 60%,
    transparent 80%
  );
}
.glow--mid {
  left: 16vw;
  bottom: -22vh;
  width: 28vw;
  height: 42vh;
  opacity: 0.65;
  background: radial-gradient(
    ellipse at 50% 55%,
    #eef0a0 0%,
    #f1efa4 40%,
    rgba(241, 239, 164, 0.35) 65%,
    transparent 82%
  );
}
.glow--right {
  right: -16vw;
  top: 6vh;
  width: 50vw;
  height: 90vh;
  opacity: 0.5;
  background: radial-gradient(
    ellipse at 45% 40%,
    #bfe0c8 0%,
    #cdeac0 30%,
    rgba(205, 234, 175, 0.3) 58%,
    transparent 78%
  );
}

.hero__head {
  text-align: center;
  max-width: 62vw;
  margin: 0 auto clamp(28px, 3.4vw, 44px);
}

.hero__title {
  font-family: var(--font-display);
  font-size: clamp(30px, 4.6vw, 68px);
  line-height: 1.08;
  font-weight: 380;
  letter-spacing: -0.01em;
  margin: 0;
}

.hero__title mark {
  background: linear-gradient(transparent 62%, var(--accent-yellow) 62%);
  padding: 0 2px;
  color: inherit;
}

.hero__subtitle {
  margin: clamp(16px, 2vw, 24px) auto 0;
  max-width: 46vw;
  font-size: clamp(13px, 1.05vw, 17px);
  color: var(--sub);
  line-height: 1.5;
}

.hero__ctas {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: clamp(16px, 1.6vw, 24px);
  margin-top: clamp(24px, 3vw, 40px);
}

.btn {
  font-size: clamp(13px, 0.95vw, 15px);
  font-weight: 500;
  border-radius: clamp(20px, 2vw, 28px);
  padding: clamp(10px, 1.1vw, 14px) clamp(20px, 2.2vw, 30px);
  cursor: pointer;
  border: none;
  font-family: inherit;
}
.btn--primary {
  background: var(--ink);
  color: #fff;
}
.btn--ghost {
  background: transparent;
  color: var(--ink);
}

/* ---- dashboard mock ---- */
.stage {
  position: relative;
  max-width: 1700px;
  width: 92vw;
  margin: clamp(56px, 7vw, 88px) auto 0;
  min-height: 44vw;
}

.panel {
  background: var(--card);
  border: 1px solid var(--line);
  border-radius: clamp(14px, 1.4vw, 22px);
  box-shadow: 0 20px 60px -30px rgba(20, 20, 20, 0.18);
}

.main-panel {
  display: flex;
  width: 82%;
  min-height: 40vw;
  position: relative;
  z-index: 1;
  overflow: hidden;
}

.sidebar {
  width: 26%;
  flex-shrink: 0;
  border-right: 1px solid var(--line);
  padding: clamp(16px, 1.4vw, 26px) clamp(14px, 1.2vw, 20px);
  display: flex;
  flex-direction: column;
}

.sidebar__org {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: clamp(11px, 0.85vw, 14px);
  font-weight: 500;
  padding-bottom: clamp(14px, 1.4vw, 22px);
  border-bottom: 1px solid var(--line);
  margin-bottom: clamp(12px, 1.2vw, 18px);
}
.sidebar__org .avatar {
  width: clamp(22px, 1.8vw, 28px);
  height: clamp(22px, 1.8vw, 28px);
  border-radius: 8px;
  background: #ece9f8;
  color: #5b4fc4;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 0.8em;
  flex-shrink: 0;
}
.sidebar__org .chev {
  margin-left: auto;
  color: #9a9ba0;
}

.sidebar__cta {
  background: #f1f1ef;
  border-radius: clamp(10px, 1vw, 14px);
  padding: clamp(10px, 1vw, 14px);
  font-size: clamp(11px, 0.9vw, 15px);
  font-weight: 500;
  margin-bottom: clamp(10px, 1vw, 16px);
}

.nav {
  display: flex;
  flex-direction: column;
  gap: 2px;
  font-size: clamp(11px, 0.85vw, 14px);
  color: #3d3d40;
  flex: 1;
}
.nav-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: clamp(7px, 0.7vw, 10px) clamp(8px, 0.7vw, 10px);
  border-radius: 10px;
}
.nav-item.active {
  background: #f1f1ef;
  font-weight: 600;
}
.nav-item .ic {
  width: 1.15em;
  height: 1.15em;
  color: #87888c;
  flex-shrink: 0;
}
.nav-item.active .ic {
  color: var(--ink);
}
.nav-item .chev {
  margin-left: auto;
  width: 0.9em;
  height: 0.9em;
  color: #9a9ba0;
}
.nav-sub {
  display: flex;
  flex-direction: column;
  gap: 2px;
  padding-left: clamp(26px, 2.2vw, 34px);
  margin: 2px 0 4px;
}
.nav-sub div {
  padding: clamp(5px, 0.55vw, 8px) 0;
  color: #6b6c70;
}

.sidebar__logo {
  margin-top: auto;
  padding-top: 14px;
  font-size: clamp(16px, 1.3vw, 20px);
  font-weight: 700;
}

.content {
  flex: 1;
  min-width: 0;
  padding: clamp(18px, 1.6vw, 28px) clamp(18px, 1.8vw, 30px);
  display: flex;
  flex-direction: column;
}

.content h2 {
  margin: 0 0 clamp(14px, 1.3vw, 20px);
  font-size: clamp(15px, 1.35vw, 22px);
  font-weight: 600;
}

.card {
  background: var(--card-soft);
  border: 1px solid var(--line);
  border-radius: clamp(12px, 1.1vw, 18px);
  padding: clamp(14px, 1.3vw, 22px);
}

.balance-card {
  margin-bottom: clamp(18px, 1.6vw, 26px);
}

.card__top {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  margin-bottom: clamp(6px, 0.6vw, 10px);
}
.card__label {
  font-size: clamp(10.5px, 0.85vw, 13px);
  color: var(--sub);
}
.card__value {
  font-size: clamp(19px, 1.7vw, 28px);
  font-weight: 600;
}
.card__value small {
  font-size: 0.55em;
  font-weight: 500;
  color: var(--sub);
}

.pill {
  display: flex;
  align-items: center;
  gap: 4px;
  font-size: clamp(9.5px, 0.75vw, 12px);
  color: #3d3d40;
  background: #fff;
  border: 1px solid var(--line);
  border-radius: 999px;
  padding: 5px 10px;
  flex-shrink: 0;
}
.pill svg {
  width: 0.9em;
  height: 0.9em;
}

.chart-wrap {
  position: relative;
  margin-top: clamp(6px, 0.7vw, 10px);
}
.chart-labels {
  display: flex;
  justify-content: space-between;
  font-size: clamp(9px, 0.72vw, 11.5px);
  color: var(--sub);
  margin-top: 4px;
}

.two-col {
  display: flex;
  gap: clamp(16px, 1.6vw, 26px);
  flex: 1;
}
.col {
  flex: 1;
  min-width: 0;
}
.col h3 {
  margin: 0 0 clamp(8px, 0.8vw, 14px);
  font-size: clamp(13px, 1.05vw, 16px);
  font-weight: 600;
}

.row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: clamp(8px, 0.75vw, 12px) 0;
  border-bottom: 1px solid var(--line);
  font-size: clamp(11px, 0.85vw, 13.5px);
}
.row:last-child {
  border-bottom: none;
}
.row__left {
  display: flex;
  align-items: center;
  gap: 10px;
  min-width: 0;
}
.row__icon {
  width: clamp(22px, 1.9vw, 30px);
  height: clamp(22px, 1.9vw, 30px);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  font-size: 0.85em;
  font-weight: 700;
}
.row__icon--muted {
  background: #eeeeee;
  color: #3d3d40;
}
.row__icon--muted svg {
  width: 0.9em;
  height: 0.9em;
}
.row__text .name {
  font-weight: 500;
  color: var(--ink);
}
.row__text .sub {
  color: var(--sub);
  font-size: 0.9em;
  margin-top: 2px;
}
.row__amount {
  font-weight: 500;
  white-space: nowrap;
}
.row__amount.pos {
  color: var(--pos);
}

/* floating income card */
.income-card {
  position: absolute;
  top: -7%;
  right: 0;
  width: 38%;
  padding: clamp(16px, 1.6vw, 26px);
  z-index: 2;
}
.toggle {
  display: inline-flex;
  background: #f1f1ef;
  border-radius: 999px;
  padding: 4px;
  font-size: clamp(10px, 0.8vw, 13px);
  margin-bottom: clamp(10px, 1vw, 16px);
}
.toggle span {
  padding: 6px 14px;
  border-radius: 999px;
  color: var(--sub);
}
.toggle span.active {
  background: #fff;
  color: var(--ink);
  font-weight: 500;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
}
.income-card .card__top {
  align-items: center;
  margin-bottom: 2px;
}
.income-card .card__value {
  margin-bottom: clamp(4px, 0.5vw, 8px);
}

@media (max-width: 700px) {
  .hero__head {
    max-width: 92vw;
  }
  .hero__subtitle {
    max-width: 88vw;
  }
  .stage {
    width: 96vw;
    min-height: auto;
  }
  .main-panel {
    width: 100%;
    flex-direction: column;
    min-height: auto;
  }
  .sidebar {
    width: 100%;
    border-right: none;
    border-bottom: 1px solid var(--line);
  }
  .nav {
    flex-direction: row;
    flex-wrap: wrap;
  }
  .nav-sub {
    display: none;
  }
  .two-col {
    flex-direction: column;
  }
  .income-card {
    position: static;
    width: 100%;
    margin-top: 16px;
  }
}
</style>