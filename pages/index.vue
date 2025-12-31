<script setup>
import { onMounted, ref } from 'vue'

// SEO Meta Tags for Home Page
useSeoMeta({
  title: 'Exequel Adizon - Creative Developer & Designer',
  description: 'Exequel Adizon (@adiluexe) is a designer and developer based in Taguig, Philippines. Passionate about crafting seamless and captivating digital experiences from design to code.',
  ogTitle: 'Exequel Adizon - Creative Developer & Designer',
  ogDescription: 'Exequel Adizon (@adiluexe) is a designer and developer based in Taguig, Philippines. Passionate about crafting seamless and captivating digital experiences from design to code.',
  ogImage: '/images/og-image.jpg',
  twitterTitle: 'Exequel Adizon - Creative Developer & Designer',
  twitterDescription: 'Exequel Adizon (@adiluexe) is a designer and developer based in Taguig, Philippines. Passionate about crafting seamless and captivating digital experiences from design to code.',
  twitterImage: '/images/og-image.jpg',
  twitterCard: 'summary_large_image'
})

const { $gsap } = useNuxtApp()

const heroTitle = ref(null)
const heroTextRef = ref(null)
let glitchTimeline = null

const texts = [
  'Exequel<span class="hidden sm:inline">&nbsp;</span><span class="block sm:inline">Adizon</span>',
  'Frontend Development',
  'Mobile Development',
  'Product<span class="hidden sm:inline">&nbsp;</span><span class="block sm:inline">Design</span>'
]
let currentIndex = 0

const startGlitchEffect = () => {
  if (glitchTimeline) glitchTimeline.kill()
  
  glitchTimeline = $gsap.timeline({ repeat: -1 })
  
  // Liquid morphing effect - faster version
  glitchTimeline
    .to({}, { duration: 0.8 }) // Shorter initial hold
    .add(() => {
      // Cycle to next text
      currentIndex = (currentIndex + 1) % texts.length
    })
    // Start morphing - stretch and distort
    .to(heroTextRef.value, {
      duration: 0.25,
      scaleY: 0.7,
      scaleX: 1.3,
      skewX: 15,
      filter: 'blur(2px)',
      ease: 'power2.inOut'
    })
    // Compress and twist
    .to(heroTextRef.value, {
      duration: 0.2,
      scaleY: 0.3,
      scaleX: 0.6,
      skewX: -20,
      rotationY: 45,
      filter: 'blur(4px)',
      ease: 'power2.inOut'
    })
    // Change text at peak distortion
    .call(() => {
      heroTextRef.value.innerHTML = texts[currentIndex]
    })
    // Expand and flow
    .to(heroTextRef.value, {
      duration: 0.2,
      scaleY: 1.4,
      scaleX: 0.8,
      skewX: 10,
      rotationY: -20,
      filter: 'blur(3px)',
      ease: 'power2.inOut'
    })
    // Settle into final form
    .to(heroTextRef.value, {
      duration: 0.35,
      scaleY: 1,
      scaleX: 1,
      skewX: 0,
      rotationY: 0,
      filter: 'blur(0px)',
      ease: 'elastic.out(1, 0.8)'
    })
    .to({}, { duration: 0.6 }) // Shorter hold before next cycle
}

const stopGlitchEffect = () => {
  if (glitchTimeline) {
    glitchTimeline.kill()
    glitchTimeline = null
  }
  
  // Reset to original text and position with liquid settle
  currentIndex = 0
  heroTextRef.value.innerHTML = texts[0]
  $gsap.to(heroTextRef.value, {
    duration: 0.6,
    x: 0,
    y: 0,
    scaleX: 1,
    scaleY: 1,
    skewX: 0,
    rotationY: 0,
    filter: 'blur(0px)',
    ease: 'elastic.out(1, 0.7)'
  })
}

onMounted(() => {
  $gsap.from(heroTitle.value, {
    duration: 1.5,
    y: 100, // Start 100px below its final position
    opacity: 0, // Start fully transparent
    ease: 'power4.out',
  })
  
  // Animate mobile layout elements
  $gsap.from('.mobile-icon', {
    duration: 1,
    y: 50,
    opacity: 0,
    delay: 0.3,
    ease: 'power4.out',
  })
  
  $gsap.from('.mobile-text', {
    duration: 1,
    y: 50,
    opacity: 0,
    stagger: 0.1,
    delay: 0.5,
    ease: 'power4.out',
  })
  
  $gsap.from('.mobile-image', {
    duration: 1,
    y: 50,
    opacity: 0,
    delay: 0.8,
    ease: 'power4.out',
  })
  
  // Animate desktop layout elements
  $gsap.from('.desktop-column', {
    duration: 1,
    y: 50,
    opacity: 0,
    stagger: 0.2,
    delay: 0.4,
    ease: 'power4.out',
  })

  // Animate footer links
  $gsap.from('.footer-link', {
    duration: 1,
    y: 20,
    opacity: 0,
    stagger: 0.1,
    delay: 1.2,
    ease: 'power4.out',
  })
})
</script>

<template>
  <div class="w-full min-h-screen flex flex-col px-4 sm:px-6 md:px-8">
    <!-- Main Hero Name -->
    <div class="flex-1 flex items-center justify-center pt-24 pb-8 sm:pt-20 md:pt-24">
      <h1 
        ref="heroTitle" 
        class="text-6xl sm:text-7xl md:text-7xl lg:text-8xl xl:text-9xl tracking-[-0.075em] text-accent cursor-hover leading-tight text-center uppercase"
        @mouseenter="startGlitchEffect"
        @mouseleave="stopGlitchEffect"
      >
        <span ref="heroTextRef">Exequel<span class="hidden sm:inline">&nbsp;</span><span class="block sm:inline">Adizon</span></span>
      </h1>
    </div>

    <!-- Three-column Info Section -->
    <div class="w-full pb-20 sm:pb-24 md:pb-32 px-4 sm:px-6 md:px-8">
      <div class="container mx-auto max-w-7xl">
        <!-- Mobile Layout: Single Column Stack -->
        <div class="block md:hidden space-y-8">
          <!-- Spinning Icon -->
          <div class="text-center mobile-icon">
            <Icon name="custom:adiluexe-logo" class="block mx-auto text-lg animate-spin-slow" />
          </div>
          
          <!-- Content Text -->
          <div class="text-center space-y-4">
            <p class="text-lg sm:text-base uppercase leading-tight px-2 mobile-text">
              Exequel Adizon (@exadizon) is a Software Engineer based in Taguig, Philippines
            </p>
            <p class="text-lg sm:text-base uppercase leading-tight px-2 mobile-text">
              Specializing in Frontend (React), Mobile Development (Flutter), and Product Design
            </p>
          </div>
          
          <!-- Hero Image -->
          <div class="text-center mobile-image">
            <div class="relative inline-block">
              <img src="/hero/hero.png" alt="Exequel Adizon" class="h-64 sm:h-72 mx-auto object-contain" />
              <div class="absolute inset-0 bg-accent opacity-10"></div>
            </div>
          </div>
        </div>

        <!-- Tablet and Desktop Layout: Three Columns -->
        <div class="hidden md:flex justify-between items-center text-sm lg:text-base xl:text-lg uppercase">
          <!-- Left Column -->
          <div class="w-1/3 max-w-xs text-center desktop-column">
            <Icon name="custom:adiluexe-logo" class="block mb-4 lg:mb-6 xl:mb-8 mx-auto text-lg lg:text-xl animate-spin-slow" />
            <p class="leading-tight">Exequel Adizon (@exadizon) is a Software Engineer based in Taguig, Philippines</p>
          </div>
          <!-- Middle Column -->
          <div class="w-1/3 max-w-xs text-center desktop-column">
            <!-- Animated hero image / illustration goes here -->
            <div class="relative inline-block">
              <img src="/hero/hero.png" alt="Exequel Adizon" class="h-48 md:h-56 lg:h-64 xl:h-80 mx-auto object-contain" />
              <div class="absolute inset-0 bg-accent opacity-10"></div>
            </div>
          </div>
          <!-- Right Column -->
          <div class="w-1/3 max-w-xs text-center desktop-column">
            <Icon name="custom:adiluexe-logo" class="block mb-4 lg:mb-6 xl:mb-8 mx-auto text-lg lg:text-xl animate-spin-slow" />
            <p class="leading-tight">Specializing in Frontend (React), Mobile Development (Flutter), and Product Design</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Fixed Footer -->
    <div class="fixed bottom-0 left-0 w-full py-6 flex justify-center items-center z-50 pointer-events-none">
      <div class="flex gap-6 sm:gap-8 md:gap-10 text-sm sm:text-base tracking-tight pointer-events-auto text-black mix-blend-difference lowercase font-bold">
        <a href="https://www.linkedin.com/in/exadizon/" target="_blank" class="footer-link relative group">
          <span>linkedin</span>
          <span class="absolute -bottom-1 left-0 w-full h-[1px] bg-current scale-x-0 group-hover:scale-x-100 transition-transform duration-300 ease-out origin-left"></span>
        </a>
        <a href="mailto:exequeladizon@gmail.com" class="footer-link relative group">
          <span>email</span>
          <span class="absolute -bottom-1 left-0 w-full h-[1px] bg-current scale-x-0 group-hover:scale-x-100 transition-transform duration-300 ease-out origin-left"></span>
        </a>
        <a href="https://github.com/exadizon" target="_blank" class="footer-link relative group">
          <span>github</span>
          <span class="absolute -bottom-1 left-0 w-full h-[1px] bg-current scale-x-0 group-hover:scale-x-100 transition-transform duration-300 ease-out origin-left"></span>
        </a>
        <a href="/adizon_resume.pdf" target="_blank" class="footer-link relative group">
          <span>resume</span>
          <span class="absolute -bottom-1 left-0 w-full h-[1px] bg-current scale-x-0 group-hover:scale-x-100 transition-transform duration-300 ease-out origin-left"></span>
        </a>
      </div>
    </div>
  </div>
</template>
