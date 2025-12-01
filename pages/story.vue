<script setup>
import { onMounted, ref } from 'vue'

// SEO Meta Tags for Story Page
useSeoMeta({
  title: 'My Story - Exequel Adizon',
  description: 'The full story of Exequel Adizon (@adiluexe), from early design experiments to becoming a full-stack developer.',
  ogTitle: 'My Story - Exequel Adizon',
  ogDescription: 'The full story of Exequel Adizon (@adiluexe), from early design experiments to becoming a full-stack developer.',
  ogImage: '/images/og-image.jpg',
  twitterTitle: 'My Story - Exequel Adizon',
  twitterDescription: 'The full story of Exequel Adizon (@adiluexe), from early design experiments to becoming a full-stack developer.',
  twitterImage: '/images/og-image.jpg',
  twitterCard: 'summary_large_image'
})

const { $gsap } = useNuxtApp()

const storyContent = ref(null)
const titleTextRef = ref(null)
let morphTimeline = null

const texts = [
  '<span class="font-spice">M</span>y <span class="font-spice">S</span>tory',
  '<span class="font-spice">J</span>ourney',
  '<span class="font-spice">P</span>ath'
]
let currentIndex = 0

const startMorphEffect = () => {
  if (morphTimeline) morphTimeline.kill()
  
  morphTimeline = $gsap.timeline({ repeat: -1 })
  
  morphTimeline
    .to({}, { duration: 0.8 })
    .add(() => {
      currentIndex = (currentIndex + 1) % texts.length
    })
    .to(titleTextRef.value, {
      duration: 0.25,
      scaleY: 0.7,
      scaleX: 1.3,
      skewX: 15,
      filter: 'blur(2px)',
      ease: 'power2.inOut'
    })
    .to(titleTextRef.value, {
      duration: 0.2,
      scaleY: 0.3,
      scaleX: 0.6,
      skewX: -20,
      rotationY: 45,
      filter: 'blur(4px)',
      ease: 'power2.inOut'
    })
    .call(() => {
      titleTextRef.value.innerHTML = texts[currentIndex]
    })
    .to(titleTextRef.value, {
      duration: 0.2,
      scaleY: 1.4,
      scaleX: 0.8,
      skewX: 10,
      rotationY: -20,
      filter: 'blur(3px)',
      ease: 'power2.inOut'
    })
    .to(titleTextRef.value, {
      duration: 0.35,
      scaleY: 1,
      scaleX: 1,
      skewX: 0,
      rotationY: 0,
      filter: 'blur(0px)',
      ease: 'elastic.out(1, 0.8)'
    })
    .to({}, { duration: 0.6 })
}

const stopMorphEffect = () => {
  if (morphTimeline) {
    morphTimeline.kill()
    morphTimeline = null
  }
  
  currentIndex = 0
  titleTextRef.value.innerHTML = texts[0]
  $gsap.to(titleTextRef.value, {
    duration: 0.6,
    scaleX: 1,
    scaleY: 1,
    skewX: 0,
    rotationY: 0,
    filter: 'blur(0px)',
    ease: 'elastic.out(1, 0.7)'
  })
}

onMounted(() => {
  $gsap.from(storyContent.value.children, {
    duration: 1,
    y: 50,
    opacity: 0,
    stagger: 0.1,
    ease: 'power4.out',
  })
})
</script>

<template>
  <div class="w-full min-h-screen flex flex-col items-center justify-center text-center py-8 sm:py-12 md:py-16 lg:py-24 xl:py-32 px-4 sm:px-6 md:px-8 lg:px-12 xl:px-0">
    <div ref="storyContent" class="w-full max-w-6xl">
      <h1 
        class="text-4xl sm:text-5xl md:text-6xl lg:text-7xl xl:text-8xl font-normal uppercase tracking-tighter mt-16 md:mt-12 lg:mt-0 xl:mt-0 mb-6 sm:mb-8 md:mb-10 lg:mb-12 xl:mb-16 font-satoshi cursor-hover leading-none"
        @mouseenter="startMorphEffect"
        @mouseleave="stopMorphEffect"
      >
        <span ref="titleTextRef"><span class="font-spice">M</span>y <span class="font-spice">S</span>tory</span>
      </h1>
      <div class="w-full h-32 sm:h-40 md:h-48 lg:h-56 xl:h-64 bg-primary mx-auto mb-3 sm:mb-4"></div>
      <div class="w-px h-12 sm:h-16 md:h-20 lg:h-24 bg-text mx-auto mb-3 sm:mb-4"></div>
      
      <div class="w-full max-w-4xl mx-auto text-sm sm:text-base md:text-lg space-y-4 sm:space-y-6 mb-3 sm:mb-4 tracking-tight text-center uppercase px-2 sm:px-4">
        <div>
          <h2 class="text-lg sm:text-xl md:text-2xl font-bold mb-3 sm:mb-4 uppercase">ABOUT ME</h2>
          <p>Hi, I'm <span class="highlight-text">Exequel Adizon</span>! I'm currently an incoming fourth-year <span class="highlight-text">Computer Science student</span> with a <span class="highlight-text">keen interest in both design and development</span>. I'm exploring career paths as a <span class="highlight-text">UI/UX Designer and Full-stack Developer.</span></p>
        </div>

        <div>
          <h3 class="text-lg sm:text-xl md:text-2xl font-bold mb-3 sm:mb-4 uppercase">My Journey into Design</h3>
          <p class="mb-3 sm:mb-4">My passion for design actually started with a love for drawing when I was young, which naturally led me to more creative pursuits. I delved into editing early on, experimenting with tools like Pizap, PicsArt, and Canva, before eventually mastering <span class="highlight-text">professional design software</span> like <span class="highlight-text">Adobe Photoshop, Illustrator, and Figma.</span></p>
          
          <p class="mb-3 sm:mb-4">I entered the design field quite early. In high school, I was already editing posts and graphics for various Facebook pages. This led to my role as the <span class="highlight-text">layout artist for</span> our school's <span class="highlight-text">English journalism publication, "The Masonry,"</span> where our newspaper proudly <span class="highlight-text">won several awards at the DSPC and RSPC</span></p>
          
          <p class="mb-3 sm:mb-4">In university, I had the honor of being the inaugural <span class="highlight-text">Head of Graphics for Fortem Ardeas Esports</span>, the University of Makati's premier esports organization. There, I <span class="highlight-text">established the brand identity and managed a vast array of graphics</span>, from live broadcast visuals to real-time graphic edits. I also created deliverables for internal events and <span class="highlight-text">collaborated with prominent esports brands such as Moonton Philippines, AcadArena, and Tier One Entertainment.</span></p>

          <p>
            Around this time, I was also <span class="highlight-text">taking on freelance design projects alongside my organizational work and academics</span>. The money was good, but I eventually hit a <span class="highlight-text">burnout</span>; designing wasn't fun anymore, and I started losing interest. This experience led me to <span class="highlight-text">make an account purely for posting whatever I wanted to create</span>. This proved to be a very therapeutic process, giving me the confidence I needed to fall back in love with design. The works you see in my "playground" section are all from that account, which <span class="highlight-text">amassed over 1 million views and half a million likes</span> in just a month of posting. Although I've stopped posting on that account to focus on more programming related activities, I'm incredibly grateful for that experience and aspire to replicate its success someday.
          </p>
        </div>

        <div>
          <h3 class="text-lg sm:text-xl md:text-2xl font-bold mb-3 sm:mb-4 uppercase">My Exploration into Development</h3>
          <p class="mb-3 sm:mb-4">I first discovered programming in 9th grade during my ICT classes, where I learned to build websites using HTML, CSS, and JavaScript. That same year, I was also the <span class="highlight-text">programmer for</span> our school's <span class="highlight-text">robotics team, "THS Overdrive"</span>, where we even <span class="highlight-text">won first place in the Programming Category of VEX IQ Robotics Competition.</span></p>
          
          <p class="mb-3 sm:mb-4">Honestly, it wasn't until college (and very recently) that I truly immersed myself in Computer Science and reignited my passion for programming. Looking back, I sometimes regret not pursuing it more seriously when I was younger, but I'm making up for lost time. This past year alone has been incredibly transformative. I've <span class="highlight-text">participated in three hackathons</span> (no wins yet, but the experience has been invaluable).</p>
          
          <p>I've gained proficiency in <span class="highlight-text">mobile app development using Flutter and React Native</span>, and I've moved beyond vanilla web development to explore powerful <span class="highlight-text">frameworks and libraries like Next.js and React</span>. To truly call myself a full-stack developer, I've also delved into <span class="highlight-text">backend development</span>, building and managing <span class="highlight-text">databases and APIs</span>. On top of all this, I've <span class="highlight-text">successfully completed several freelance programming projects.</span></p>
        </div>

        <div>
          <Icon name="custom:adiluexe-logo" class="block mb-3 sm:mb-4 mx-auto text-sm animate-bounce" />
          <h3 class="text-lg sm:text-xl md:text-2xl font-bold mb-3 sm:mb-4 uppercase">Let's Connect</h3>
          <p>If you're looking for someone who's <span class="highlight-text">proficient in both design and programming</span>—someone who <span class="highlight-text">blends technical skills with a creative mindset</span>—please feel free to reach out! I'm still <span class="highlight-text">open to freelance opportunities</span>, but I'm particularly <span class="highlight-text">keen on gaining more formal experience in the tech industry</span>, as most of my work thus far has been self-driven.</p>
        </div>
      </div>
      
      <div class="w-px h-12 sm:h-16 md:h-20 lg:h-24 bg-text mx-auto mb-3 sm:mb-4"></div>
      
      <div class="text-center w-full max-w-4xl mx-auto px-2 sm:px-4">
        <NuxtLink to="/about" class="inline-block border-2 border-text px-6 py-3 rounded-full hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 text-sm sm:text-base font-bold tracking-wider cursor-hover mb-8 uppercase">
            Back to About
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<style scoped>
.highlight-text {
  color: var(--color-primary);
  font-weight: 500;
  position: relative;
}
</style>
