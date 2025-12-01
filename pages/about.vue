<script setup>
import { onMounted, ref } from 'vue'

// SEO Meta Tags for About Page
useSeoMeta({
  title: 'About - Exequel Adizon',
  description: 'Creative Developer & Designer based in Taguig, Philippines. Specialized in UI/UX Design and Full-stack Development.',
  ogTitle: 'About - Exequel Adizon',
  ogDescription: 'Creative Developer & Designer based in Taguig, Philippines. Specialized in UI/UX Design and Full-stack Development.',
  ogImage: '/images/og-image.jpg',
  twitterTitle: 'About - Exequel Adizon',
  twitterDescription: 'Creative Developer & Designer based in Taguig, Philippines. Specialized in UI/UX Design and Full-stack Development.',
  twitterImage: '/images/og-image.jpg',
  twitterCard: 'summary_large_image'
})

const { $gsap } = useNuxtApp()

const aboutContent = ref(null)
const titleTextRef = ref(null)
let morphTimeline = null

const texts = [
  '<span class="font-spice">A</span>bout',
  '<span class="font-spice">S</span>kills',
  '<span class="font-spice">A</span>wards'
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
  $gsap.from(aboutContent.value.children, {
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
    <div ref="aboutContent" class="w-full max-w-6xl">
      <h1 
        class="text-4xl sm:text-5xl md:text-6xl lg:text-7xl xl:text-8xl font-normal uppercase tracking-tighter mt-16 md:mt-12 lg:mt-0 xl:mt-0 mb-6 sm:mb-8 md:mb-10 lg:mb-12 xl:mb-16 font-satoshi cursor-hover leading-none"
        @mouseenter="startMorphEffect"
        @mouseleave="stopMorphEffect"
      >
        <span ref="titleTextRef"><span class="font-spice">A</span>bout</span>
      </h1>
      <div class="w-full h-32 sm:h-40 md:h-48 lg:h-56 xl:h-64 bg-primary mx-auto mb-8 sm:mb-12"></div>

      <!-- Short Bio -->
      <div class="max-w-3xl mx-auto mb-12 sm:mb-16 text-lg sm:text-xl md:text-2xl uppercase leading-tight px-4 tracking-tighter">
        <p>
          I'm <span class="text-primary font-bold">Exequel Adizon</span>, a developer and designer based in Taguig, Philippines. 
          I bridge the gap between <span class="text-primary">design</span> and <span class="text-primary">technology</span> to craft immersive digital experiences.
        </p>
        <div class="mt-8">
            <NuxtLink to="/story" class="inline-block border-2 border-text px-6 py-3 rounded-full hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 text-sm sm:text-base font-bold tracking-wider cursor-hover">
                My Story
            </NuxtLink>
        </div>
      </div>

      <div class="w-px h-12 sm:h-16 bg-text mx-auto mb-12 sm:mb-16"></div>

      <!-- Skills Section -->
      <div class="w-full max-w-6xl mx-auto mb-16 sm:mb-20 px-4">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-12 sm:gap-16">
          <!-- Design Column -->
          <div class="text-left">
            <div class="flex items-center gap-4 mb-8">
              <div class="w-12 h-12 rounded-full border border-primary flex items-center justify-center text-primary">
                <Icon name="ph:paint-brush-bold" class="text-2xl" />
              </div>
              <h3 class="text-3xl sm:text-4xl font-normal text-primary uppercase tracking-tighter"><span class="font-spice">D</span>esign</h3>
            </div>
            
            <div class="space-y-8">
              <div>
                <h4 class="text-lg font-bold uppercase mb-4 opacity-70">Core Competencies</h4>
                <div class="flex flex-wrap gap-3">
                  <span class="px-4 py-2 border border-text/20 rounded-full text-sm uppercase tracking-wider hover:border-primary hover:text-primary transition-colors cursor-default">UI/UX Design</span>
                  <span class="px-4 py-2 border border-text/20 rounded-full text-sm uppercase tracking-wider hover:border-primary hover:text-primary transition-colors cursor-default">Web Design</span>
                  <span class="px-4 py-2 border border-text/20 rounded-full text-sm uppercase tracking-wider hover:border-primary hover:text-primary transition-colors cursor-default">Mobile App Design</span>
                  <span class="px-4 py-2 border border-text/20 rounded-full text-sm uppercase tracking-wider hover:border-primary hover:text-primary transition-colors cursor-default">Prototyping</span>
                  <span class="px-4 py-2 border border-text/20 rounded-full text-sm uppercase tracking-wider hover:border-primary hover:text-primary transition-colors cursor-default">Interaction Design</span>
                  <span class="px-4 py-2 border border-text/20 rounded-full text-sm uppercase tracking-wider hover:border-primary hover:text-primary transition-colors cursor-default">Branding</span>
                </div>
              </div>
              
              <div>
                <h4 class="text-lg font-bold uppercase mb-4 opacity-70">Tools</h4>
                <div class="grid grid-cols-2 sm:grid-cols-3 gap-4">
                  <div class="flex items-center gap-2 opacity-80 hover:opacity-100 transition-opacity">
                    <Icon name="ph:figma-logo-bold" class="text-xl" /> <span>Figma</span>
                  </div>
                  <div class="flex items-center gap-2 opacity-80 hover:opacity-100 transition-opacity">
                    <Icon name="ph:image-bold" class="text-xl" /> <span>Photoshop</span>
                  </div>
                  <div class="flex items-center gap-2 opacity-80 hover:opacity-100 transition-opacity">
                    <Icon name="ph:pen-nib-bold" class="text-xl" /> <span>Illustrator</span>
                  </div>
                  <div class="flex items-center gap-2 opacity-80 hover:opacity-100 transition-opacity">
                    <Icon name="ph:film-strip-bold" class="text-xl" /> <span>After Effects</span>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Development Column -->
          <div class="text-left">
            <div class="flex items-center gap-4 mb-8">
              <div class="w-12 h-12 rounded-full border border-primary flex items-center justify-center text-primary">
                <Icon name="ph:code-bold" class="text-2xl" />
              </div>
              <h3 class="text-3xl sm:text-4xl font-normal text-primary uppercase tracking-tighter"><span class="font-spice">D</span>evelopment</h3>
            </div>
            
            <div class="space-y-8">
              <div>
                <h4 class="text-lg font-bold uppercase mb-4 opacity-70">Core Competencies</h4>
                <div class="flex flex-wrap gap-3">
                  <span class="px-4 py-2 border border-text/20 rounded-full text-sm uppercase tracking-wider hover:border-primary hover:text-primary transition-colors cursor-default">Frontend Dev</span>
                  <span class="px-4 py-2 border border-text/20 rounded-full text-sm uppercase tracking-wider hover:border-primary hover:text-primary transition-colors cursor-default">Backend Dev</span>
                  <span class="px-4 py-2 border border-text/20 rounded-full text-sm uppercase tracking-wider hover:border-primary hover:text-primary transition-colors cursor-default">Mobile Dev</span>
                  <span class="px-4 py-2 border border-text/20 rounded-full text-sm uppercase tracking-wider hover:border-primary hover:text-primary transition-colors cursor-default">Creative Coding</span>
                  <span class="px-4 py-2 border border-text/20 rounded-full text-sm uppercase tracking-wider hover:border-primary hover:text-primary transition-colors cursor-default">Responsive Design</span>
                </div>
              </div>
              
              <div>
                <h4 class="text-lg font-bold uppercase mb-4 opacity-70">Tech Stack</h4>
                <div class="grid grid-cols-2 sm:grid-cols-3 gap-4">
                  <div class="flex items-center gap-2 opacity-80 hover:opacity-100 transition-opacity">
                    <Icon name="ph:file-html-bold" class="text-xl" /> <span>HTML/CSS/JS</span>
                  </div>
                  <div class="flex items-center gap-2 opacity-80 hover:opacity-100 transition-opacity">
                    <Icon name="ph:atom-bold" class="text-xl" /> <span>React / Next</span>
                  </div>
                  <div class="flex items-center gap-2 opacity-80 hover:opacity-100 transition-opacity">
                    <Icon name="ph:vue-logo-bold" class="text-xl" /> <span>Vue / Nuxt</span>
                  </div>
                  <div class="flex items-center gap-2 opacity-80 hover:opacity-100 transition-opacity">
                    <Icon name="ph:device-mobile-bold" class="text-xl" /> <span>Flutter</span>
                  </div>
                  <div class="flex items-center gap-2 opacity-80 hover:opacity-100 transition-opacity">
                    <Icon name="ph:database-bold" class="text-xl" /> <span>Node / SQL</span>
                  </div>
                  <div class="flex items-center gap-2 opacity-80 hover:opacity-100 transition-opacity">
                    <Icon name="ph:paint-brush-broad-bold" class="text-xl" /> <span>Tailwind</span>
                  </div>
                  <div class="flex items-center gap-2 opacity-80 hover:opacity-100 transition-opacity">
                    <Icon name="ph:magic-wand-bold" class="text-xl" /> <span>GSAP</span>
                  </div>
                  <div class="flex items-center gap-2 opacity-80 hover:opacity-100 transition-opacity">
                    <Icon name="ph:git-branch-bold" class="text-xl" /> <span>Git</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Awards Section -->
      <div class="max-w-4xl mx-auto mb-16 sm:mb-20 px-4 tracking-tighter">
        <h2 class="text-3xl sm:text-4xl font-bold uppercase mb-8 sm:mb-12">Awards & Recognition</h2>
        <div class="space-y-6 text-left">
            <!-- Award 1 -->
            <div class="group border-b border-text/20 pb-6 hover:border-primary transition-colors duration-300">
                <div class="flex flex-col md:flex-row md:items-baseline justify-between gap-2">
                    <h3 class="text-xl sm:text-2xl font-bold uppercase group-hover:text-primary transition-colors">Champion</h3>
                    <span class="text-sm sm:text-base opacity-60 font-mono">2025</span>
                </div>
                <p class="text-base sm:text-lg uppercase mt-2">GDAP GameOn - Professional Track Category</p>
            </div>

            <!-- Award 2 -->
            <div class="group border-b border-text/20 pb-6 hover:border-primary transition-colors duration-300">
                <div class="flex flex-col md:flex-row md:items-baseline justify-between gap-2">
                    <h3 class="text-xl sm:text-2xl font-bold uppercase group-hover:text-primary transition-colors">Finalist</h3>
                    <span class="text-sm sm:text-base opacity-60 font-mono">2025</span>
                </div>
                <p class="text-base sm:text-lg uppercase mt-2">C(Old) (St)art Hackathon by Old.St Labs</p>
            </div>

            <!-- Award 3 -->
            <div class="group border-b border-text/20 pb-6 hover:border-primary transition-colors duration-300">
                <div class="flex flex-col md:flex-row md:items-baseline justify-between gap-2">
                    <h3 class="text-xl sm:text-2xl font-bold uppercase group-hover:text-primary transition-colors">Best Paper Presentation</h3>
                    <span class="text-sm sm:text-base opacity-60 font-mono">2025</span>
                </div>
                <p class="text-base sm:text-lg uppercase mt-2">Innovative Solutions - UMak 8th Research Congress</p>
            </div>
        </div>
      </div>

      <div class="w-px h-12 sm:h-16 md:h-20 lg:h-24 bg-text mx-auto mb-3 sm:mb-4"></div>
      <div class="text-center w-full max-w-4xl mx-auto px-2 sm:px-4">
        <a 
          href="mailto:exequel.adizon@gmail.com"
          class="group relative inline-flex items-center gap-1 sm:gap-2 cursor-hover transition-all duration-300 mb-3 sm:mb-4 flex-wrap justify-center"
        >
          <span class="relative group-hover:text-primary transition-colors duration-300 text-lg sm:text-2xl md:text-3xl lg:text-4xl break-all">
        EXEQUEL.ADIZON@GMAIL.COM
        <span class="absolute bottom-0 left-0 w-0 h-0.5 bg-primary transition-all duration-300 ease-out group-hover:w-full"></span>
          </span>
          <svg class="w-4 h-4 sm:w-5 sm:h-5 md:w-6 md:h-6 transition-all duration-300 group-hover:translate-x-1 group-hover:-translate-y-1 group-hover:text-primary flex-shrink-0" fill="currentColor" viewBox="0 0 24 24">
        <path d="M5,17.59L15.59,7H9V5H19V15H17V8.41L6.41,19L5,17.59Z" />
          </svg>
        </a>
        <div class="flex items-center justify-center gap-2 sm:gap-4 text-lg sm:text-2xl md:text-3xl lg:text-4xl flex-wrap">
          <a 
        href="https://github.com/adiluexe" 
        target="_blank"
        class="group relative flex items-center gap-1 sm:gap-2 cursor-hover transition-all duration-300"
          >
        <span class="relative group-hover:text-primary transition-colors duration-300">
          GITHUB
          <span class="absolute bottom-0 left-0 w-0 h-0.5 bg-primary transition-all duration-300 ease-out group-hover:w-full"></span>
        </span>
        <svg class="w-4 h-4 sm:w-5 sm:h-5 md:w-6 md:h-6 transition-all duration-300 group-hover:translate-x-1 group-hover:-translate-y-1 group-hover:text-primary flex-shrink-0" fill="currentColor" viewBox="0 0 24 24">
          <path d="M5,17.59L15.59,7H9V5H19V15H17V8.41L6.41,19L5,17.59Z" />
        </svg>
          </a>
          <span class="text-lg sm:text-2xl md:text-3xl lg:text-4xl font-satoshi">/</span>
          <a 
        href="https://www.linkedin.com/in/exequel-adizon/" 
        target="_blank"
        class="group relative flex items-center gap-1 sm:gap-2 cursor-hover transition-all duration-300"
          >
        <span class="relative group-hover:text-primary transition-colors duration-300">
          LINKEDIN
          <span class="absolute bottom-0 left-0 w-0 h-0.5 bg-primary transition-all duration-300 ease-out group-hover:w-full"></span>
        </span>
        <svg class="w-4 h-4 sm:w-5 sm:h-5 md:w-6 md:h-6 transition-all duration-300 group-hover:translate-x-1 group-hover:-translate-y-1 group-hover:text-primary flex-shrink-0" fill="currentColor" viewBox="0 0 24 24">
          <path d="M5,17.59L15.59,7H9V5H19V15H17V8.41L6.41,19L5,17.59Z" />
        </svg>
          </a>
        </div>
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
