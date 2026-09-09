<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const root = ref(null)
const visible = ref(false)
let observer

onMounted(() => {
  observer = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting) { visible.value = true; observer.disconnect() }
  }, { threshold: 0.16 })
  if (root.value) observer.observe(root.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>

<template>
  <section ref="root" class="mobile-mail" :class="{ 'is-visible': visible }" aria-labelledby="mobile-mail-title">
    <div class="glow glow--yellow" aria-hidden="true" />
    <div class="glow glow--green" aria-hidden="true" />

    <header class="mobile-mail__header">
      <span class="section-pill">Email On the Go</span>
      <h2 id="mobile-mail-title">Manage Your Business Email<br>From <mark>Anywhere</mark></h2>
      <p>Read messages, protect your inbox, and manage professional mailboxes<br>wherever your business takes you.</p>
      <div class="access-buttons">
        <a href="https://smardove.com/features/"><svg viewBox="0 0 24 24"><path d="M16.7 12.7c0-2.4 2-3.6 2.1-3.7a4.5 4.5 0 0 0-3.5-1.9c-1.5-.2-2.9.9-3.6.9-.8 0-1.9-.9-3.1-.9A4.7 4.7 0 0 0 4.7 9.5c-1.7 3-.4 7.4 1.2 9.8.8 1.2 1.8 2.5 3.1 2.4 1.2 0 1.7-.8 3.2-.8s1.9.8 3.2.8c1.3 0 2.2-1.2 3-2.4a10 10 0 0 0 1.4-2.9 4.2 4.2 0 0 1-3.1-3.7ZM14.3 5.5A4.3 4.3 0 0 0 15.4 2a4.4 4.4 0 0 0-3 1.7 4 4 0 0 0-1.1 3.2 3.7 3.7 0 0 0 3-1.4Z"/></svg><span><small>ACCESS ON</small><strong>iPhone &amp; iPad</strong></span></a>
        <a href="https://smardove.com/features/"><svg viewBox="0 0 24 24"><path d="m4 3 11 9L4 21V3Z"/><path d="m15 12 4-3c1-.7 2-.2 2 .8v4.4c0 1-1 1.5-2 .8Z"/></svg><span><small>ACCESS ON</small><strong>Android Devices</strong></span></a>
      </div>
    </header>

    <div class="phones" aria-label="Smardove mobile email interface previews">
      <div class="phone phone--left">
        <div class="phone__screen">
          <div class="status"><span>9:41</span><i/><i/><i/></div>
          <div class="appbar"><b>S</b><span>Inbox</span><em>NA</em></div>
          <div class="tabs"><strong>Primary</strong><span>Updates</span><span>Sent</span></div>
          <div class="search">⌕ &nbsp; Search messages</div>
          <div class="message"><i class="avatar green">AM</i><span><b>Alex Morgan</b><small>Updated project proposal</small><em>Here is the final document...</em></span><time>Now</time></div>
          <div class="message"><i class="avatar yellow">SK</i><span><b>Sarah Kim</b><small>Meeting confirmed</small><em>See you tomorrow at 10...</em></span><time>10:24</time></div>
          <div class="message"><i class="avatar dark">JD</i><span><b>James Dean</b><small>Invoice #2048</small><em>Your payment was received...</em></span><time>09:45</time></div>
          <button class="compose">+</button>
        </div>
      </div>

      <div class="phone phone--center">
        <div class="phone__screen">
          <div class="status"><span>9:41</span><i/><i/><i/></div>
          <div class="appbar"><b>S</b><span>Overview</span><em>NA</em></div>
          <div class="welcome"><small>GOOD MORNING</small><strong>Your email is performing well.</strong></div>
          <div class="metric-grid"><span><small>Delivered</small><b>12.4K</b><em>+18%</em></span><span><small>Protected</small><b>3.2K</b><em>+8%</em></span><span><small>Mailboxes</small><b>48</b><em>Active</em></span><span><small>Storage</small><b>62%</b><em>Healthy</em></span></div>
          <div class="delivery-card"><span><small>DELIVERY PERFORMANCE</small><strong>99.9%</strong></span><div class="mini-bars"><i/><i/><i/><i/><i/><i/></div></div>
          <div class="safe"><i>✓</i><span><b>All systems secure</b><small>Threat protection is active</small></span></div>
        </div>
      </div>

      <div class="phone phone--right">
        <div class="phone__screen">
          <div class="status"><span>9:41</span><i/><i/><i/></div>
          <div class="appbar"><b>S</b><span>Mailboxes</span><em>NA</em></div>
          <div class="team-head"><span><small>YOUR TEAM</small><strong>48 mailboxes</strong></span><button>+ Add</button></div>
          <div class="member"><i class="avatar green">NA</i><span><b>Naduni Ameesha</b><small>admin@company.com</small></span><em>Admin</em></div>
          <div class="member"><i class="avatar yellow">AM</i><span><b>Alex Morgan</b><small>alex@company.com</small></span><em>Active</em></div>
          <div class="member"><i class="avatar dark">SK</i><span><b>Sarah Kim</b><small>sarah@company.com</small></span><em>Active</em></div>
          <div class="storage"><span><b>Storage usage</b><small>31 GB of 50 GB</small></span><div><i/></div></div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.mobile-mail,.mobile-mail *{box-sizing:border-box}.mobile-mail{--ink:#0d0d0d;--green:#c9e6a8;--green-deep:#91bd67;--yellow:#f3ee9a;--muted:#717870;position:relative;isolation:isolate;min-height:clamp(700px,62vw,900px);overflow:hidden;padding:clamp(60px,6vw,95px) 18px 0;background:radial-gradient(circle at 10% 8%,rgba(243,238,154,.52),transparent 29%),radial-gradient(circle at 90% 85%,rgba(201,230,168,.64),transparent 35%),linear-gradient(180deg,#fff 0%,#f1f7e9 54%,#c9e6a8 100%);color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.mobile-mail::before{position:absolute;z-index:-2;inset:0;background-image:linear-gradient(rgba(13,13,13,.018) 1px,transparent 1px),linear-gradient(90deg,rgba(13,13,13,.018) 1px,transparent 1px);background-size:50px 50px;mask-image:linear-gradient(#000,transparent 50%);content:""}.glow{position:absolute;z-index:-1;width:390px;height:390px;border-radius:50%;filter:blur(110px);opacity:.35}.glow--yellow{top:-260px;left:8%;background:var(--yellow)}.glow--green{right:5%;bottom:-230px;background:var(--green)}.mobile-mail__header{position:relative;z-index:5;text-align:center;opacity:0;transform:translateY(22px)}.is-visible .mobile-mail__header{animation:rise .75s forwards}.section-pill{display:inline-flex;padding:8px 16px;border:1px solid #b8d79a;border-radius:999px;background:rgba(255,255,255,.78);box-shadow:0 8px 23px rgba(30,43,23,.06);font-size:10px;font-weight:700}.mobile-mail h2{margin:16px 0 13px;font-family:var(--font-display,var(--font-sans));font-size:clamp(37px,4vw,59px);font-weight:420;line-height:1.05;letter-spacing:-.05em}.mobile-mail h2 mark{padding:0 3px;background:linear-gradient(transparent 64%,var(--yellow) 64%);color:inherit}.mobile-mail__header>p{margin:0;color:var(--muted);font-size:clamp(11px,.95vw,14px);line-height:1.55}.access-buttons{display:flex;justify-content:center;gap:12px;margin-top:24px}.access-buttons a{display:flex;min-width:155px;align-items:center;gap:10px;padding:8px 15px;border-radius:999px;background:#0d0d0d;color:#fff;text-align:left;text-decoration:none;box-shadow:0 10px 24px rgba(13,13,13,.16);transition:transform .25s ease,background .25s ease}.access-buttons a:hover{background:#242824;transform:translateY(-3px)}.access-buttons svg{width:22px;fill:#fff;stroke:#fff;stroke-width:1.2}.access-buttons span{display:flex;flex-direction:column}.access-buttons small{font-size:5px;letter-spacing:.08em}.access-buttons strong{font-size:10px}.phones{position:relative;width:min(690px,92vw);height:500px;margin:42px auto 0;perspective:1200px}.phone{position:absolute;bottom:-45px;width:245px;height:480px;padding:8px;border:2px solid #252825;border-radius:36px;background:#111;box-shadow:0 32px 60px rgba(30,43,23,.23);opacity:0}.phone::before{position:absolute;z-index:5;top:13px;left:50%;width:68px;height:19px;border-radius:99px;background:#111;transform:translateX(-50%);content:""}.phone__screen{position:relative;height:100%;overflow:hidden;border-radius:28px;background:#f5f7f3}.phone--left{left:42px;transform:translateY(70px) rotate(-13deg) rotateY(12deg)}.phone--center{z-index:3;left:50%;transform:translateX(-50%) translateY(75px)}.phone--right{right:42px;transform:translateY(70px) rotate(13deg) rotateY(-12deg)}.is-visible .phone--left{animation:leftPhone .9s .35s cubic-bezier(.17,.84,.28,1.1) forwards,floatLeft 5s 1.4s ease-in-out infinite}.is-visible .phone--center{animation:centerPhone .9s .2s cubic-bezier(.17,.84,.28,1.1) forwards,floatCenter 4.7s 1.25s ease-in-out infinite}.is-visible .phone--right{animation:rightPhone .9s .48s cubic-bezier(.17,.84,.28,1.1) forwards,floatRight 5.2s 1.5s ease-in-out infinite}.status{display:flex;height:31px;align-items:center;justify-content:flex-end;gap:4px;padding:7px 12px 0;font-size:6px}.status span{margin-right:auto}.status i{width:5px;height:5px;border-radius:50%;background:#6e756c}.appbar{display:flex;height:46px;align-items:center;gap:9px;padding:0 11px;background:#111;color:#fff}.appbar>b{display:grid;width:24px;height:24px;place-items:center;border-radius:8px;background:var(--yellow);color:#111;font-size:8px}.appbar span{font-size:9px;font-weight:700}.appbar em{display:grid;width:24px;height:24px;margin-left:auto;place-items:center;border-radius:50%;background:var(--green);color:#24321d;font-size:6px;font-style:normal;font-weight:800}.tabs{display:flex;gap:15px;padding:14px 12px 8px;color:#929991;font-size:6px}.tabs strong{padding-bottom:6px;border-bottom:2px solid var(--green-deep);color:#252a24}.search{margin:0 10px 8px;padding:8px;border-radius:8px;background:#e9ece7;color:#9ca29a;font-size:6px}.message,.member{display:flex;align-items:center;gap:8px;padding:11px 10px;border-bottom:1px solid #e2e7df}.avatar{display:grid;width:29px;height:29px;flex:0 0 auto;place-items:center;border-radius:50%;font-size:6px;font-style:normal;font-weight:800}.avatar.green{background:var(--green)}.avatar.yellow{background:var(--yellow)}.avatar.dark{background:#222;color:#fff}.message>span,.member>span{display:flex;min-width:0;flex-direction:column}.message b,.member b{font-size:7px}.message small,.message em,.member small{overflow:hidden;max-width:115px;color:#8f968d;font-size:5px;font-style:normal;text-overflow:ellipsis;white-space:nowrap}.message time{margin-left:auto;color:#989f96;font-size:5px}.compose{position:absolute;right:14px;bottom:16px;width:40px;height:40px;border:0;border-radius:50%;background:#111;color:#fff;font-size:20px}.welcome{display:flex;flex-direction:column;padding:17px 13px 10px}.welcome small{color:#949b92;font-size:5px;letter-spacing:.12em}.welcome strong{margin-top:4px;font-size:10px}.metric-grid{display:grid;grid-template-columns:1fr 1fr;gap:7px;padding:0 11px}.metric-grid span{display:flex;flex-direction:column;padding:10px;border:1px solid #e1e6df;border-radius:10px;background:#fff}.metric-grid small{color:#929990;font-size:5px}.metric-grid b{margin:3px 0;font-size:13px}.metric-grid em{color:#79a254;font-size:5px;font-style:normal}.delivery-card{margin:8px 11px;padding:11px;border-radius:11px;background:#fff}.delivery-card>span{display:flex;align-items:center;justify-content:space-between}.delivery-card small{color:#90978e;font-size:5px}.delivery-card strong{font-size:14px}.mini-bars{display:flex;height:48px;align-items:flex-end;gap:8px;margin-top:7px}.mini-bars i{width:13%;border-radius:3px 3px 0 0;background:#dfe5dc}.mini-bars i:nth-child(1){height:25%}.mini-bars i:nth-child(2){height:47%;background:var(--yellow)}.mini-bars i:nth-child(3){height:35%}.mini-bars i:nth-child(4){height:68%;background:var(--green)}.mini-bars i:nth-child(5){height:55%}.mini-bars i:nth-child(6){height:82%;background:#222}.safe{display:flex;align-items:center;gap:8px;margin:8px 11px;padding:10px;border-radius:10px;background:#edf7e5}.safe>i{display:grid;width:24px;height:24px;place-items:center;border-radius:50%;background:var(--green);font-size:7px;font-style:normal}.safe span{display:flex;flex-direction:column}.safe b{font-size:6px}.safe small{color:#7e8a77;font-size:5px}.team-head{display:flex;align-items:center;justify-content:space-between;padding:18px 11px 9px}.team-head>span{display:flex;flex-direction:column}.team-head small{color:#979e95;font-size:5px}.team-head strong{margin-top:3px;font-size:11px}.team-head button{padding:6px 8px;border:0;border-radius:7px;background:var(--green);font-size:6px;font-weight:700}.member em{margin-left:auto;padding:4px 6px;border-radius:99px;background:#edf7e5;color:#71964f;font-size:5px;font-style:normal}.storage{margin:13px 10px;padding:12px;border-radius:11px;background:#fff}.storage>span{display:flex;justify-content:space-between}.storage b{font-size:6px}.storage small{color:#929990;font-size:5px}.storage>div{height:6px;margin-top:9px;overflow:hidden;border-radius:99px;background:#e8ece6}.storage>div i{display:block;width:62%;height:100%;border-radius:inherit;background:linear-gradient(90deg,var(--green-deep),var(--yellow))}
@keyframes rise{to{opacity:1;transform:translateY(0)}}@keyframes leftPhone{to{opacity:1;transform:translateY(0) rotate(-13deg) rotateY(12deg)}}@keyframes centerPhone{to{opacity:1;transform:translateX(-50%) translateY(0)}}@keyframes rightPhone{to{opacity:1;transform:translateY(0) rotate(13deg) rotateY(-12deg)}}@keyframes floatLeft{50%{translate:0 -8px}}@keyframes floatCenter{50%{translate:0 -11px}}@keyframes floatRight{50%{translate:0 -7px}}
@media(max-width:700px){.mobile-mail{min-height:790px;padding-inline:12px}.mobile-mail__header>p br{display:none}.access-buttons{flex-wrap:wrap}.phones{height:470px;margin-top:38px}.phone{width:205px;height:420px}.phone--left{left:5px}.phone--right{right:5px}.message{padding-block:9px}.metric-grid span{padding:8px}}
@media(max-width:480px){.mobile-mail h2{font-size:clamp(36px,10.5vw,48px)}.access-buttons a{min-width:145px}.phones{width:370px;max-width:110vw;left:50%;transform:translateX(-50%)}.phone{width:175px;height:385px;border-radius:28px}.phone__screen{border-radius:21px}.phone--left{left:7px}.phone--right{right:7px}.phone--center{width:190px}.appbar{height:41px}.delivery-card{margin-top:6px}.mini-bars{height:38px}}
@media(prefers-reduced-motion:reduce){.mobile-mail__header,.phone{opacity:1!important;animation:none!important}.mobile-mail__header{transform:none!important}.phone--left{transform:rotate(-13deg)!important}.phone--center{transform:translateX(-50%)!important}.phone--right{transform:rotate(13deg)!important}}
</style>
