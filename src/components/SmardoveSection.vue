<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const visible = ref(false)
let observer

const emailCount = ref(0)
const barFilled = ref(false)
const TARGET_COUNT = 105

function animateCount () {
  const duration = 1100
  const start = performance.now()
  function tick (now) {
    const progress = Math.min((now - start) / duration, 1)
    const eased = 1 - Math.pow(1 - progress, 3)
    emailCount.value = Math.round(eased * TARGET_COUNT)
    if (progress < 1) requestAnimationFrame(tick)
  }
  requestAnimationFrame(tick)
}

onMounted(() => {
  if (!('IntersectionObserver' in window)) {
    visible.value = true
    animateCount()
    barFilled.value = true
    return
  }
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) {
      visible.value = true
      setTimeout(animateCount, 200)
      setTimeout(() => { barFilled.value = true }, 300)
      observer.disconnect()
    }
  }, { threshold: .12 })
  if (root.value) observer.observe(root.value)
})
onBeforeUnmount(() => observer?.disconnect())

const inboxStats = [
  { label: 'Unread', count: '59 mails', color: '#4476e6' },
  { label: 'Flagged', count: '13 mails', color: '#aabff2' },
  { label: 'Archived', count: '83 mails', color: '#00cab6' },
  { label: 'Spam', count: '27 mails', color: '#7ce6d2' }
]

const messages = [
  { name: 'Henry Mason', sub: 'is typing…', time: '9:30 AM', badge: 1, initials: 'HM', color: '#4476e6', typing: true },
  { name: 'Moni Roy', sub: 'Online', time: '9:30 AM', badge: 0, initials: 'MR', color: '#00cab6' },
  { name: 'Liam Parker', sub: '"Hey, are we still on track for…"', time: '9:30 AM', badge: 1, initials: 'LP', color: '#aabff2' },
  { name: 'Emma Collins', sub: 'Online', time: '9:30 AM', badge: 0, initials: 'EC', color: '#7ce6d2' },
  { name: 'Moni Roy', sub: 'Online', time: '9:30 AM', badge: 0, initials: 'MR', color: '#00cab6' }
]

const mailboxes = [
  { name: 'Sales', team: ['S', 'K', 'P'], colors: ['#4476e6', '#00cab6', '#aabff2'] },
  { name: 'Marketing', team: ['Z', 'J', 'H'], colors: ['#7ce6d2', '#4476e6', '#00cab6'] },
  { name: 'Customer Support', team: ['A', 'B', 'M'], colors: ['#aabff2', '#7ce6d2', '#00cab6'] }
]
</script>

<template>
  <section ref="root" class="premium" :class="{ visible }" aria-labelledby="premium-title">
    <div class="premium__inner">
      <header class="premium__header">
        <span class="eyebrow">
          <i class="eyebrow__dot"></i>
          Email features
        </span>
        <h2 id="premium-title">Unlock Premium Benefits With<br />Our Advanced <mark>Email Features.</mark></h2>
        <p>Unlock premium benefits with advanced features designed to scale your inbox.</p>
      </header>

      <div class="bento">

        <!-- 1. Smart Inbox Organization -->
        <article class="bento-card bento-card--blue span-1" :style="{ '--delay': '0s' }">
          <div class="bento-card__text">
            <h3>Smart Inbox Organization</h3>
            <p>Create, categorize, and prioritize emails with ease using flexible folders, labels, and rules.</p>
          </div>

          <div class="panel">
            <div class="panel__row panel__row--top">
              <div>
                <small>Current Total</small>
                <strong class="big">{{ emailCount }} Emails</strong>
              </div>
              <button class="pill-btn">
                <svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.6"><rect x="3" y="4" width="14" height="13" rx="2"/><path d="M3 8h14"/></svg>
                View Details
              </button>
            </div>

            <ul class="stat-list">
              <li v-for="(s, i) in inboxStats" :key="s.label" :style="{ '--i': i }">
                <span class="dot" :style="{ background: s.color }"></span>
                <span class="label">{{ s.label }}</span>
                <span class="count">{{ s.count }}</span>
              </li>
            </ul>

            <div class="segbar">
              <i class="segbar__fill" :class="{ filled: barFilled }" style="--w:44%;background:#4476e6;--d:0s"></i>
              <i class="segbar__fill" :class="{ filled: barFilled }" style="--w:13%;background:#aabff2;--d:.1s"></i>
              <i class="segbar__fill" :class="{ filled: barFilled }" style="--w:22%;background:#00cab6;--d:.2s"></i>
              <i class="segbar__fill" :class="{ filled: barFilled }" style="--w:21%;background:#7ce6d2;--d:.3s"></i>
            </div>
          </div>
        </article>

        <!-- 2. Automated Workflows -->
        <article class="bento-card bento-card--soft-blue span-1" :style="{ '--delay': '.08s' }">
          <div class="bento-card__text">
            <h3>Automated Email Rules</h3>
            <p>Streamline your inbox with automation for sorting, replies, and reminders.</p>
          </div>

          <div class="panel">
            <div class="panel__row panel__row--top">
              <strong>Rules</strong>
              <button class="text-btn">
                <svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M13 4l3 3-9 9H4v-3z"/></svg>
                Edit
              </button>
            </div>

            <div class="rule-card">
              <span class="rule-tag rule-tag--muted">New Lead</span>
              <p class="rule-title">Auto-tag &amp; forward inbound<br />sales inquiries</p>
              <div class="rule-foot">
                <span class="rule-tag rule-tag--solid">Sales Inbox</span>
                <span class="avatar avatar--sm" style="background:#4476e6">AR</span>
              </div>
            </div>

            <button class="add-btn">
              <span class="add-btn__icon">+</span>
              Add new rule
            </button>
          </div>
        </article>

        <!-- 3. Team Inbox & Comments -->
        <article class="bento-card bento-card--ink span-1" :style="{ '--delay': '.16s' }">
          <div class="bento-card__text">
            <h3>Team Inbox &amp; Comments</h3>
            <p>Consolidate everything with email comments, attachments, and feedback threads.</p>
          </div>

          <div class="panel panel--stack">
            <div class="msg-card">
              <div class="msg-card__head">
                <span>New Messages</span>
                <span class="count-badge">2</span>
                <svg class="dots" viewBox="0 0 20 20" fill="currentColor"><circle cx="4" cy="10" r="1.6"/><circle cx="10" cy="10" r="1.6"/><circle cx="16" cy="10" r="1.6"/></svg>
              </div>
              <ul class="msg-list">
                <li v-for="(m, i) in messages" :key="i" :style="{ '--i': i }">
                  <span class="avatar" :style="{ background: m.color }">{{ m.initials }}</span>
                  <span class="msg-body">
                    <b>{{ m.name }}</b>
                    <small :class="{ typing: m.typing }">
                      <template v-if="m.typing">
                        <span class="typing-dots"><i/><i/><i/></span>
                      </template>
                      <template v-else>{{ m.sub }}</template>
                    </small>
                  </span>
                  <span class="msg-time">
                    <em v-if="m.badge" class="dot-badge">{{ m.badge }}</em>
                    <small v-else>✓</small>
                    <small>{{ m.time }}</small>
                  </span>
                </li>
              </ul>
            </div>
          </div>
        </article>

        <!-- 4. Real-Time tracking (text only) -->
        <article class="bento-card bento-card--pale bento-card--plain span-wide" :style="{ '--delay': '.24s' }">
          <div class="bento-card__text bento-card__text--center">
            <h3>Real-Time Delivery Tracking</h3>
            <p>Track opens, replies, and deliverability with live status updates and visual indicators.</p>
          </div>
          <div class="pulse-ring">
            <span class="pulse-ring__core"></span>
            <span class="pulse-ring__wave"></span>
            <span class="pulse-ring__wave" style="animation-delay:.6s"></span>
          </div>
        </article>

        <!-- 5. Mailbox Overview -->
        <article class="bento-card bento-card--mint span-wide" :style="{ '--delay': '.32s' }">
          <div class="panel panel--table">
            <strong class="table-title">Mailbox Overview</strong>
            <div class="table-head">
              <span>Mailbox Name</span>
              <span>Team</span>
            </div>
            <ul class="table-rows">
              <li v-for="(mb, i) in mailboxes" :key="mb.name" :style="{ '--i': i }">
                <span>{{ mb.name }}</span>
                <span class="avatar-group">
                  <span v-for="(t, j) in mb.team" :key="j" class="avatar avatar--sm" :style="{ background: mb.colors[j], '--j': j }">{{ t }}</span>
                </span>
              </li>
            </ul>
          </div>
        </article>

      </div>
    </div>
  </section>
</template>

<style scoped>
.premium,.premium *{box-sizing:border-box}
.premium{--ink:#0d0d0d;--green:#00cab6;--mint:#7ce6d2;--lavender:#aabff2;--blue:#4476e6;width:100%;padding:clamp(64px,7vw,110px) clamp(16px,4vw,60px);background:#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif);overflow:hidden}
.premium__inner{width:min(1300px,100%);margin:auto}

.premium__header{max-width:760px;margin:0 auto clamp(40px,5vw,60px);text-align:center;opacity:0;transform:translateY(16px)}
.visible .premium__header{animation:rise .6s forwards}
.eyebrow{display:inline-flex;align-items:center;gap:7px;margin-bottom:16px;padding:8px 13px;border-radius:99px;background:linear-gradient(135deg,rgba(0,224,171,.14),rgba(68,118,230,.13));color:#08786a;font-size:10px;font-weight:800;letter-spacing:.1em;text-transform:uppercase}
.eyebrow__dot{width:6px;height:6px;border-radius:50%;background:#00cab6;animation:blink 1.6s ease-in-out infinite}
.premium__header h2{margin:0;font-size:clamp(28px,3.6vw,44px);font-weight:700;line-height:1.16;letter-spacing:-.03em;color:var(--ink)}
.premium__header h2 mark{background:linear-gradient(transparent 70%,rgba(170,191,242,.8) 70%);color:inherit;background-size:200% 100%;animation:sweep 2.6s ease .8s 1}
.premium__header p{max-width:480px;margin:16px auto 0;color:#737985;font-size:15px;line-height:1.6}

.bento{display:grid;grid-template-columns:repeat(3,1fr);grid-auto-rows:auto;gap:16px}
.span-1{grid-column:span 1}
.span-wide{grid-column:span 1}
@media(min-width:860px){
  .bento{grid-template-columns:repeat(6,1fr)}
  .bento > .span-1{grid-column:span 2}
  .bento > .span-wide{grid-column:span 3}
}

.bento-card{position:relative;display:flex;flex-direction:column;gap:20px;padding:26px 24px 24px;border-radius:20px;border:1px solid rgba(255,255,255,.82);opacity:0;transform:translateY(22px) scale(.98);transition:transform .35s cubic-bezier(.2,.8,.3,1),box-shadow .35s ease}
.visible .bento-card{animation:card-rise .68s cubic-bezier(.2,.8,.3,1) var(--delay) forwards}
.bento-card:hover{transform:translateY(-6px) scale(1.005);box-shadow:0 28px 54px -32px rgba(13,13,13,.32)}
.bento-card--plain{justify-content:center;min-height:200px}

.bento-card__text h3{margin:0 0 8px;font-size:17px;font-weight:700;letter-spacing:-.015em;color:var(--ink)}
.bento-card__text p{margin:0;max-width:38ch;color:inherit;opacity:.66;font-size:13px;line-height:1.65}
.bento-card--plain .bento-card__text p{opacity:.7}
.bento-card--plain .bento-card__text{max-width:340px}

.bento-card--blue{background:linear-gradient(155deg,#dce7ff 0%,#eef3ff 60%,#e4efff 100%)}
.bento-card--soft-blue{background:linear-gradient(155deg,#d7e3ff 0%,#edf2ff 52%,#e6edff 100%)}
.bento-card--mint{background:linear-gradient(165deg,#cdf3e5,#e8f9f1)}
.bento-card--pale{background:linear-gradient(165deg,#e3f2dc,#f3f8ef)}
.bento-card--ink{background:#151817;color:#fff}
.bento-card--ink .bento-card__text p{opacity:.62}

/* Panel */
.panel{flex:1;display:flex;flex-direction:column;gap:14px;padding:18px;border-radius:16px;background:#fff;box-shadow:0 18px 40px -30px rgba(13,13,13,.4);color:#17201c;opacity:0;transform:translateY(10px)}
.visible .panel{animation:panel-in .6s ease .5s forwards}
.panel--stack{padding:14px}

.panel__row{display:flex;align-items:center;justify-content:space-between}
.panel__row--top small{display:block;margin-bottom:4px;color:#8a938c;font-size:11px}
.big{font-size:20px;font-weight:800;color:#0d0d0d;font-variant-numeric:tabular-nums}

.pill-btn{display:flex;align-items:center;gap:6px;padding:8px 12px;border:1px solid #e6ede8;border-radius:99px;background:#fff;color:#3a4740;font-size:11px;font-weight:600;cursor:pointer;transition:transform .2s ease,box-shadow .2s ease}
.pill-btn:hover{transform:translateY(-2px);box-shadow:0 8px 16px -10px rgba(13,13,13,.35)}
.pill-btn svg{width:13px;height:13px}
.text-btn{display:flex;align-items:center;gap:5px;background:none;border:none;color:#7d8980;font-size:12px;font-weight:600;cursor:pointer}
.text-btn svg{width:13px;height:13px}

.stat-list{list-style:none;margin:0;padding:0;display:flex;flex-direction:column;gap:11px}
.stat-list li{display:flex;align-items:center;gap:9px;font-size:12.5px;opacity:0;transform:translateX(-8px)}
.visible .stat-list li{animation:slide-in .45s ease forwards;animation-delay:calc(.7s + var(--i) * .08s)}
.stat-list .dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;box-shadow:0 0 0 0 currentColor}
.stat-list li:first-child .dot{animation:dot-pulse 2.2s ease-in-out infinite 1.4s;color:#4476e6}
.stat-list .label{color:#3a4740;font-weight:600}
.stat-list .count{margin-left:auto;color:#8a938c}

.segbar{display:flex;height:9px;border-radius:99px;overflow:hidden;background:#eef0ed}
.segbar__fill{display:block;width:0;flex:0 0 auto;transition:width 1s cubic-bezier(.2,.8,.2,1) var(--d)}
.segbar__fill.filled{width:var(--w)}

/* Rule card */
.rule-card{padding:14px;border-radius:14px;background:#f4f6f4;border:1px solid #eef0ed;opacity:0;transform:translateY(8px)}
.visible .rule-card{animation:panel-in .5s ease .75s forwards}
.rule-tag{display:inline-block;padding:4px 10px;border-radius:99px;font-size:10px;font-weight:700}
.rule-tag--muted{background:rgba(68,118,230,.14);color:#355fc2}
.rule-tag--solid{background:var(--blue);color:#fff}
.rule-title{margin:10px 0 12px;font-size:13px;font-weight:700;line-height:1.4;color:#0d0d0d}
.rule-foot{display:flex;align-items:center;justify-content:space-between}

.add-btn{display:flex;align-items:center;justify-content:center;gap:8px;padding:12px;border:1px dashed #cfd9d3;border-radius:12px;background:#fafcfa;color:#3a4740;font-size:12.5px;font-weight:700;cursor:pointer;transition:background .2s ease,transform .2s ease}
.add-btn:hover{background:#f0f4f0;transform:translateY(-2px)}
.add-btn__icon{display:grid;width:18px;height:18px;place-items:center;border-radius:50%;background:var(--blue);color:#fff;font-size:13px;animation:spin-in 2.4s ease-in-out infinite 1.6s}

/* Avatars */
.avatar{display:grid;place-items:center;width:26px;height:26px;border-radius:50%;color:#fff;font-size:9.5px;font-weight:800;flex-shrink:0}
.avatar--sm{width:22px;height:22px;font-size:8.5px;border:2px solid #fff}
.avatar-group{display:flex}
.avatar-group .avatar--sm{opacity:0;transform:scale(.5)}
.visible .avatar-group .avatar--sm{animation:pop-in .4s cubic-bezier(.34,1.56,.64,1) forwards;animation-delay:calc(1s + var(--j) * .1s)}
.avatar-group .avatar--sm:not(:first-child){margin-left:-8px}

/* Messages card */
.msg-card{border-radius:14px;overflow:hidden}
.msg-card__head{display:flex;align-items:center;gap:8px;padding:4px 4px 12px;font-size:14px;font-weight:800;color:#fff}
.count-badge{display:grid;place-items:center;width:18px;height:18px;border-radius:50%;background:var(--blue);color:#fff;font-size:10px;font-weight:800;animation:badge-pulse 1.8s ease-in-out infinite}
.dots{width:16px;height:16px;margin-left:auto;color:#5a625d}
.msg-list{list-style:none;margin:0;padding:0;display:flex;flex-direction:column;gap:12px}
.msg-list li{display:flex;align-items:center;gap:10px;opacity:0;transform:translateY(8px)}
.visible .msg-list li{animation:panel-in .45s ease forwards;animation-delay:calc(.6s + var(--i) * .08s)}
.msg-body{display:flex;flex-direction:column;flex:1;min-width:0}
.msg-body b{font-size:12.5px;color:#fff}
.msg-body small{margin-top:2px;color:#8f978f;font-size:11px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;display:flex;align-items:center}
.typing-dots{display:inline-flex;gap:3px}
.typing-dots i{width:4px;height:4px;border-radius:50%;background:#4476e6;animation:typing-bounce 1.2s ease-in-out infinite}
.typing-dots i:nth-child(2){animation-delay:.15s}
.typing-dots i:nth-child(3){animation-delay:.3s}
.msg-time{display:flex;flex-direction:column;align-items:flex-end;gap:4px}
.msg-time small{color:#8f978f;font-size:10px}
.dot-badge{display:grid;place-items:center;width:15px;height:15px;border-radius:50%;background:var(--blue);color:#fff;font-size:8px;font-style:normal;font-weight:800}

/* Pulse ring (real-time tracking visual) */
.pulse-ring{position:absolute;right:26px;top:50%;transform:translateY(-50%);width:64px;height:64px}
.pulse-ring__core{position:absolute;inset:22px;border-radius:50%;background:var(--blue);box-shadow:0 6px 16px -4px rgba(68,118,230,.6)}
.pulse-ring__wave{position:absolute;inset:0;border-radius:50%;border:2px solid var(--blue);opacity:0;animation:ring-out 2.4s ease-out infinite}
@media(max-width:640px){.pulse-ring{display:none}}

/* Table */
.panel--table{gap:10px}
.table-title{font-size:14px;font-weight:800;color:#0d0d0d}
.table-head{display:flex;justify-content:space-between;padding-bottom:8px;border-bottom:1px solid #eef0ed;color:#8a938c;font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:.04em}
.table-rows{list-style:none;margin:0;padding:0;display:flex;flex-direction:column}
.table-rows li{display:flex;align-items:center;justify-content:space-between;padding:12px 0;border-bottom:1px solid #f4f5f2;font-size:13px;font-weight:600;color:#3a4740;opacity:0;transform:translateX(-10px)}
.visible .table-rows li{animation:slide-in .5s ease forwards;animation-delay:calc(.8s + var(--i) * .1s)}
.table-rows li:last-child{border-bottom:none}

/* Keyframes */
@keyframes rise{to{opacity:1;transform:translateY(0)}}
@keyframes card-rise{to{opacity:1;transform:translateY(0) scale(1)}}
@keyframes panel-in{to{opacity:1;transform:translateY(0)}}
@keyframes slide-in{to{opacity:1;transform:translateX(0)}}
@keyframes pop-in{to{opacity:1;transform:scale(1)}}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.25}}
@keyframes sweep{from{background-position:200% 0}to{background-position:0 0}}
@keyframes dot-pulse{0%{box-shadow:0 0 0 0 rgba(68,118,230,.45)}70%{box-shadow:0 0 0 7px rgba(68,118,230,0)}100%{box-shadow:0 0 0 0 rgba(68,118,230,0)}}
@keyframes badge-pulse{0%,100%{transform:scale(1)}50%{transform:scale(1.15)}}
@keyframes typing-bounce{0%,60%,100%{transform:translateY(0);opacity:.5}30%{transform:translateY(-3px);opacity:1}}
@keyframes spin-in{0%,100%{transform:rotate(0)}50%{transform:rotate(180deg)}}
@keyframes ring-out{0%{transform:scale(.4);opacity:.55}100%{transform:scale(1.9);opacity:0}}

@media(max-width:540px){.premium{padding-inline:14px}}
@media(prefers-reduced-motion:reduce){
  .premium__header,.bento-card,.panel,.rule-card,.stat-list li,.avatar-group .avatar--sm,.msg-list li,.table-rows li{opacity:1!important;transform:none!important;animation:none!important;transition:none!important}
  .segbar__fill{width:var(--w)!important;transition:none!important}
  .eyebrow__dot,.pulse-ring__wave,.count-badge,.typing-dots i,.add-btn__icon,.stat-list li:first-child .dot{animation:none!important}
}
</style>