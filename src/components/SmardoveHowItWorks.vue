<script setup>
const stories = [
  { title: 'Sell more with professional email', author: 'Smardove Growth', image: 'https://images.unsplash.com/photo-1556761175-b413da4baf72?auto=format&fit=crop&w=900&q=85' },
  { title: 'Protect every business conversation', author: 'Smardove Security', image: 'https://images.unsplash.com/photo-1563013544-824ae1b704d3?auto=format&fit=crop&w=900&q=85' },
  { title: 'Keep your whole team connected', author: 'Smardove Workspace', image: 'https://images.unsplash.com/photo-1521737711867-e3b97375f902?auto=format&fit=crop&w=900&q=85' },
  { title: 'Manage email from any device', author: 'Smardove Mobile', image: 'https://images.unsplash.com/photo-1516321318423-f06f85e504b3?auto=format&fit=crop&w=900&q=85' },
  { title: 'Move to Smardove with confidence', author: 'Migration Experts', image: 'https://images.unsplash.com/photo-1551434678-e076c223a692?auto=format&fit=crop&w=900&q=85' },
  { title: 'Understand delivery performance', author: 'Smardove Analytics', image: 'https://images.unsplash.com/photo-1551288049-bebda4e38f71?auto=format&fit=crop&w=900&q=85' },
  { title: 'Recover important messages fast', author: 'Smardove Archive', image: 'https://images.unsplash.com/photo-1497366754035-f200968a6e72?auto=format&fit=crop&w=900&q=85' },
  { title: 'Control every mailbox in one place', author: 'Smardove Admin', image: 'https://images.unsplash.com/photo-1552664730-d307ca884978?auto=format&fit=crop&w=900&q=85' }
]

const marqueeStories = [...stories, ...stories]
</script>

<template>
  <section class="email-marquee" aria-labelledby="email-marquee-title">
    <div class="email-marquee__glow email-marquee__glow--aqua" />
    <div class="email-marquee__glow email-marquee__glow--blue" />

    <div class="email-marquee__heading">
      <span class="eyebrow"><i /> Smardove insights</span>
      <h2 id="email-marquee-title">Discover smarter ways to use <mark>business email.</mark></h2>
      <p>Explore practical ideas for secure communication, teamwork and business growth.</p>
    </div>

    <div class="marquee" aria-label="Smardove email insights">
      <div class="marquee__fade marquee__fade--left" />
      <div class="marquee__fade marquee__fade--right" />

      <div class="marquee__track">
        <article
          v-for="(story, index) in marqueeStories"
          :key="`${story.title}-${index}`"
          class="story-card"
          :aria-hidden="index >= stories.length"
        >
          <img :src="story.image" :alt="index < stories.length ? story.title : ''" loading="lazy">
          <div class="story-card__overlay" />

          <div class="story-card__copy">
            <h3>{{ story.title }}</h3>
            <span>{{ story.author }}</span>
          </div>

          <a
            class="story-card__button"
            href="https://smardove.com/features/"
            :tabindex="index >= stories.length ? -1 : 0"
            :aria-label="`Explore ${story.title}`"
          >
            <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M9 7.3v9.4L17 12 9 7.3Z" /></svg>
          </a>

          <span class="story-card__number">{{ String((index % stories.length) + 1).padStart(2, '0') }}</span>
        </article>
      </div>
    </div>

    <div class="email-marquee__footer">
      <span><i /> Continuously exploring better business communication</span>
      <a href="https://smardove.com/blog/">View all insights <b>↗</b></a>
    </div>
  </section>
</template>

<style scoped>
.email-marquee,.email-marquee *{box-sizing:border-box}.email-marquee{--ink:#0d0d0d;--muted:#737985;--aqua:#00e0ab;--teal:#00cab6;--blue:#4476e6;--indigo:#4864f0;--soft:#7ce6d2;--line:#e6eaf0;position:relative;isolation:isolate;overflow:hidden;width:100%;padding:clamp(78px,8vw,125px) 0;background:#fff;color:var(--ink);font-family:var(--font-sans,"Plus Jakarta Sans",Arial,sans-serif)}.email-marquee__glow{position:absolute;z-index:-1;width:420px;height:420px;border-radius:50%;filter:blur(135px);opacity:.1}.email-marquee__glow--aqua{top:-230px;left:-170px;background:var(--aqua)}.email-marquee__glow--blue{right:-200px;bottom:-230px;background:var(--blue)}.email-marquee__heading{max-width:820px;margin:0 auto clamp(45px,5vw,68px);padding:0 20px;text-align:center}.eyebrow{display:inline-flex;align-items:center;gap:9px;margin-bottom:18px;padding:8px 14px;border:1px solid var(--line);border-radius:99px;color:#53606b;font-size:9px;font-weight:800;letter-spacing:.11em;text-transform:uppercase}.eyebrow i{width:8px;height:8px;border-radius:50%;background:linear-gradient(135deg,var(--aqua),var(--teal));box-shadow:0 0 0 4px rgba(0,224,171,.12)}.email-marquee__heading h2{margin:0;font-size:clamp(38px,5vw,68px);font-weight:430;line-height:1.04;letter-spacing:-.052em}.email-marquee__heading mark{padding:0 .03em;background:linear-gradient(transparent 70%,rgba(124,230,210,.62) 70%);color:inherit}.email-marquee__heading p{max-width:590px;margin:19px auto 0;color:var(--muted);font-size:13px;line-height:1.7}.marquee{position:relative;width:100%;overflow:hidden}.marquee__track{display:flex;width:max-content;gap:16px;padding:12px 0;animation:marquee-scroll 52s linear infinite;will-change:transform}.marquee:hover .marquee__track,.marquee:focus-within .marquee__track{animation-play-state:paused}.marquee__fade{position:absolute;top:0;bottom:0;z-index:5;width:clamp(24px,7vw,120px);pointer-events:none}.marquee__fade--left{left:0;background:linear-gradient(90deg,#fff,rgba(255,255,255,0))}.marquee__fade--right{right:0;background:linear-gradient(-90deg,#fff,rgba(255,255,255,0))}.story-card{position:relative;width:clamp(240px,22vw,330px);height:clamp(390px,38vw,510px);flex-shrink:0;overflow:hidden;border:1px solid rgba(255,255,255,.85);border-radius:28px;background:linear-gradient(145deg,var(--soft),var(--blue));box-shadow:0 28px 65px -42px rgba(28,53,78,.72);transform:translateZ(0);transition:transform .35s,box-shadow .35s}.story-card:hover{transform:translateY(-8px);box-shadow:0 37px 77px -39px rgba(25,50,84,.78)}.story-card img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;filter:saturate(.84) contrast(.96);transition:transform .75s,filter .35s}.story-card:hover img{filter:saturate(1);transform:scale(1.055)}.story-card__overlay{position:absolute;inset:0;background:linear-gradient(180deg,rgba(7,20,31,.66),rgba(7,20,31,.05) 44%,rgba(7,20,31,.4)),linear-gradient(135deg,rgba(0,224,171,.13),rgba(68,118,230,.14));pointer-events:none}.story-card__copy{position:absolute;top:0;right:0;left:0;z-index:2;padding:25px 20px;color:#fff;text-align:center;text-shadow:0 2px 18px rgba(0,0,0,.42)}.story-card__copy h3{max-width:230px;margin:auto;font-size:clamp(14px,1.2vw,17px);line-height:1.35}.story-card__copy span{display:block;margin-top:6px;font-size:8px;font-weight:650;opacity:.78}.story-card__button{position:absolute;top:50%;left:50%;z-index:3;display:grid;width:55px;height:55px;place-items:center;border:1px solid rgba(255,255,255,.88);border-radius:50%;background:rgba(255,255,255,.94);box-shadow:0 18px 38px -22px rgba(0,0,0,.75);color:var(--blue);transform:translate(-50%,-50%);transition:transform .25s}.story-card__button:hover{transform:translate(-50%,-50%) scale(1.1)}.story-card__button svg{width:24px;fill:currentColor}.story-card__number{position:absolute;right:17px;bottom:16px;z-index:2;display:grid;width:34px;height:34px;place-items:center;border:1px solid rgba(255,255,255,.58);border-radius:50%;background:rgba(13,13,13,.18);color:#fff;font-size:8px;font-weight:800;backdrop-filter:blur(9px)}.email-marquee__footer{display:flex;width:min(1380px,calc(100% - 32px));align-items:center;justify-content:space-between;gap:25px;margin:34px auto 0;padding-top:25px;border-top:1px solid var(--line)}.email-marquee__footer>span{display:flex;align-items:center;gap:9px;color:var(--muted);font-size:9px}.email-marquee__footer>span i{width:7px;height:7px;border-radius:50%;background:var(--aqua);box-shadow:0 0 0 4px rgba(0,224,171,.11)}.email-marquee__footer>a{display:flex;align-items:center;gap:14px;color:var(--ink);font-size:10px;font-weight:750;text-decoration:none}.email-marquee__footer>a b{display:grid;width:33px;height:33px;place-items:center;border-radius:50%;background:linear-gradient(135deg,var(--blue),var(--indigo));color:#fff}@keyframes marquee-scroll{from{transform:translateX(0)}to{transform:translateX(calc(-50% - 8px))}}@media(max-width:600px){.email-marquee__heading h2{font-size:38px}.story-card{width:265px;height:430px}.marquee__track{animation-duration:38s}.email-marquee__footer{align-items:flex-start;flex-direction:column}}@media(prefers-reduced-motion:reduce){.marquee__track{animation-play-state:paused}.story-card,.story-card img,.story-card__button{transition:none!important}}
</style>
