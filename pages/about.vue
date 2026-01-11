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

const { $gsap, $ScrollTrigger } = useNuxtApp()

const aboutContent = ref(null)
const titleTextRef = ref(null)
const skillsSection = ref(null)
const experienceSection = ref(null)
const awardsSection = ref(null)
const contactSection = ref(null)
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
  // Header Animation
  const headerElements = aboutContent.value.querySelectorAll('.header-animate')
  $gsap.from(headerElements, {
    duration: 1,
    y: 50,
    opacity: 0,
    stagger: 0.1,
    ease: 'power4.out',
  })

  // Skills Animation
  if (skillsSection.value) {
    const sections = skillsSection.value.querySelectorAll('.skill-group')
    sections.forEach((section) => {
      $gsap.from(section, {
        scrollTrigger: {
          trigger: section,
          start: 'top 85%',
          toggleActions: 'play none none reverse',
          invalidateOnRefresh: true
        },
        y: 30,
        opacity: 0,
        duration: 0.8,
        ease: 'power3.out'
      })
    })
  }

  // Experience Animation
  if (experienceSection.value) {
    const items = experienceSection.value.querySelectorAll('.experience-item')
    $gsap.from(items, {
      scrollTrigger: {
        trigger: experienceSection.value,
        start: 'top 80%',
        toggleActions: 'play none none reverse',
        invalidateOnRefresh: true
      },
      y: 30,
      opacity: 0,
      duration: 0.8,
      stagger: 0.15,
      ease: 'power3.out'
    })
  }

  // Awards Animation
  if (awardsSection.value) {
    const items = awardsSection.value.querySelectorAll('.award-item')
    $gsap.from(items, {
      scrollTrigger: {
        trigger: awardsSection.value,
        start: 'top 90%',
        toggleActions: 'play none none reverse',
        invalidateOnRefresh: true
      },
      y: 30,
      opacity: 0,
      duration: 0.8,
      stagger: 0.15,
      ease: 'power3.out'
    })
  }

  // Contact Animation
  if (contactSection.value) {
    $gsap.from(contactSection.value.children, {
      scrollTrigger: {
        trigger: contactSection.value,
        start: 'top 90%',
        toggleActions: 'play none none reverse',
        invalidateOnRefresh: true
      },
      y: 30,
      opacity: 0,
      duration: 0.8,
      stagger: 0.1,
      ease: 'power3.out'
    })
  }

  // Refresh ScrollTrigger to ensure positions are correct after layout
  setTimeout(() => {
    $ScrollTrigger.refresh()
  }, 500)
})
</script>

<template>
  <div class="w-full min-h-screen flex flex-col items-center justify-center text-center py-8 sm:py-12 md:py-16 lg:py-24 xl:py-32 px-4 sm:px-6 md:px-8 lg:px-12 xl:px-0">
    <div ref="aboutContent" class="w-full max-w-6xl">
      <h1 
        class="text-4xl sm:text-5xl md:text-6xl lg:text-7xl xl:text-8xl font-normal uppercase tracking-tighter mt-16 md:mt-12 lg:mt-0 xl:mt-0 mb-6 sm:mb-8 md:mb-10 lg:mb-12 xl:mb-16 font-satoshi cursor-hover leading-none header-animate"
        @mouseenter="startMorphEffect"
        @mouseleave="stopMorphEffect"
      >
        <span ref="titleTextRef"><span class="font-spice">A</span>bout</span>
      </h1>
      <!-- <div class="w-full h-32 sm:h-40 md:h-48 lg:h-56 xl:h-64 bg-primary mx-auto mb-8 sm:mb-12"></div> -->

      <!-- Short Bio -->
      <div class="max-w-3xl mx-auto mb-12 sm:mb-16 text-lg sm:text-xl md:text-2xl uppercase leading-tight px-4 tracking-tighter header-animate">
        <p class="mb-8">
          I'm <span class="font-bold text-primary">Exequel Adizon</span>, a Software Engineer based in Taguig, Philippines. 
          I bridge the gap between <span class="font-bold">aesthetic design</span> and <span class="font-bold">robust engineering</span>, building digital experiences that look good and work even better.
        </p>
        
        <!-- Call to Action -->
        <div class="flex justify-center gap-4">
            <a href="/adizon_resume.pdf" target="_blank" class="inline-flex items-center gap-2 px-6 py-3 border border-text rounded-full hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 text-sm sm:text-base font-bold tracking-wider cursor-hover group">
                <span>Download Resume</span>
                <Icon name="ph:arrow-down-bold" class="group-hover:translate-y-1 transition-transform" />
            </a>
        </div>
      </div>

      <!-- Skills Section -->
      <div ref="skillsSection" class="w-full max-w-5xl mx-auto mb-16 sm:mb-24 px-4 space-y-16 sm:space-y-24">
        <h2 class="text-3xl sm:text-4xl font-bold uppercase tracking-tighter">Skills & Expertise</h2>
        
        <!-- Design Section -->
        <div class="text-left skill-group space-y-8">
          <h3 class="text-2xl sm:text-3xl font-bold uppercase tracking-tighter">Design</h3>
          <div class="flex flex-wrap gap-2 sm:gap-3">
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">UI/UX Design</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Web Design</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Mobile App Design</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Prototyping & Wireframing</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Interaction Design</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Design Systems</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Brand Identity</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Figma</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Adobe Photoshop</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Adobe Illustrator</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Adobe After Effects</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Adobe Premiere Pro</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Canva</span>
          </div>
        </div>

        <!-- Full Stack Development Section -->
        <div class="text-left skill-group space-y-8">
          <h3 class="text-2xl sm:text-3xl font-bold uppercase tracking-tighter">Frontend</h3>
          <div class="flex flex-wrap gap-2 sm:gap-3">
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">JavaScript / ES6+</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">TypeScript</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">React / JSX</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Next.js</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Vue.js / Composition API</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Nuxt.js</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Tailwind CSS</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">HTML5 / CSS3 / SCSS</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">GSAP / Web Animation</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Vite / Module Bundler</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Webpack</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">ESLint / Code Quality</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Prettier / Code Formatter</span>
          </div>
        </div>

        <div class="text-left skill-group space-y-8">
          <h3 class="text-2xl sm:text-3xl font-bold uppercase tracking-tighter">Mobile</h3>
          <div class="flex flex-wrap gap-2 sm:gap-3">
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Flutter / Dart</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">React Native</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Kotlin / Android</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">iOS / Swift</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Cross-Platform Development</span>
          </div>
        </div>

        <div class="text-left skill-group space-y-8">
          <h3 class="text-2xl sm:text-3xl font-bold uppercase tracking-tighter">Backend</h3>
          <div class="flex flex-wrap gap-2 sm:gap-3">
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Node.js / Runtime</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Python</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Java</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">PHP</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Express.js</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">FastAPI / Framework</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">PostgreSQL / RDBMS</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">MySQL</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Firebase / BaaS</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Supabase</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">RESTful APIs</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">GraphQL</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">OAuth 2.0 / JWT</span>
          </div>
        </div>

        <div class="text-left skill-group space-y-8">
          <h3 class="text-2xl sm:text-3xl font-bold uppercase tracking-tighter">DevOps & Cloud</h3>
          <div class="flex flex-wrap gap-2 sm:gap-3">
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Docker / Containerization</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">GitHub / Version Control</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">GitHub Actions / CI-CD</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Git / SCM</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">CI/CD Pipelines</span>
          </div>
        </div>

        <!-- AI & Automation Section -->
        <div class="text-left skill-group space-y-8">
          <h3 class="text-2xl sm:text-3xl font-bold uppercase tracking-tighter">AI & Machine Learning</h3>
          <div class="flex flex-wrap gap-2 sm:gap-3">
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Claude (Anthropic)</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">ChatGPT / GPT-4 (OpenAI)</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Gemini (Google)</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">DeepSeek</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Generative AI</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">LangChain / LLM Framework</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Prompt Engineering</span>
          </div>
        </div>

        <div class="text-left skill-group space-y-8">
          <h3 class="text-2xl sm:text-3xl font-bold uppercase tracking-tighter">AI Dev Tools</h3>
          <div class="flex flex-wrap gap-2 sm:gap-3">
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Cursor IDE</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Windsurf IDE</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">GitHub Copilot</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">AI-Assisted Pair Programming</span>
          </div>
        </div>

        <div class="text-left skill-group space-y-8">
          <h3 class="text-2xl sm:text-3xl font-bold uppercase tracking-tighter">Automation & Integration</h3>
          <div class="flex flex-wrap gap-2 sm:gap-3">
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">n8n</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">n8n / Workflow Automation</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Business Process Automation</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">API Integration / Middleware</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Webhooks / Event-Driven</span>
            <span class="px-3 py-1.5 border border-text/30 rounded-md text-xs sm:text-sm font-medium hover:bg-primary hover:text-background hover:border-primary transition-all duration-300 cursor-default">Real-time Systems</span>
          </div>
        </div>
      </div>

      <!-- Experience Section -->
      <div ref="experienceSection" class="w-full max-w-5xl mx-auto mb-16 sm:mb-24 px-4">
        <h2 class="text-3xl sm:text-4xl font-bold uppercase mb-12 sm:mb-16 tracking-tighter">Experience & Education</h2>
        
        <div class="relative border-l border-text/20 ml-3 sm:ml-6 space-y-12 sm:space-y-16 text-left">
            
            <!-- Education Item -->
            <div class="relative pl-8 sm:pl-12 experience-item">
                <!-- Dot -->
                <div class="absolute -left-[5px] top-2 w-2.5 h-2.5 rounded-full bg-primary"></div>
                
                <div class="flex flex-col sm:flex-row sm:items-baseline justify-between gap-1 mb-2">
                    <h3 class="text-xl sm:text-2xl font-bold uppercase text-primary">Bachelor of Science in Computer Science</h3>
                    <span class="text-sm font-mono opacity-60 shrink-0">Aug 2022 — Aug 2026</span>
                </div>
                <h4 class="text-lg font-medium uppercase mb-4 opacity-80">University of Makati</h4>
            </div>

            <!-- Experience Item 1 -->
            <div class="relative pl-8 sm:pl-12 experience-item">
                <div class="absolute -left-[5px] top-2 w-2.5 h-2.5 rounded-full bg-text"></div>
                
                <div class="flex flex-col sm:flex-row sm:items-baseline justify-between gap-1 mb-2">
                    <h3 class="text-xl sm:text-2xl font-bold uppercase">Frontend Developer</h3>
                    <span class="text-sm font-mono opacity-60 shrink-0">Aug 2025 — Nov 2025</span>
                </div>
                <h4 class="text-lg font-medium uppercase mb-4 text-primary">EdLab Ltd.</h4>
                <ul class="list-disc list-outside ml-4 space-y-2 text-base sm:text-lg opacity-80 leading-relaxed">
                    <li>Maintained production CodeIgniter (PHP) codebase, debugging complex dynamic PDF generation tools to ensure accurate report delivery for 500+ student performance reviews monthly</li>
                    <li>Bridged the design-engineering gap by creating high-fidelity Figma prototypes and marketing assets, ensuring strict brand consistency across web products and social channels with 95% stakeholder approval rate</li>
                    <li>Reduced PDF generation errors by 40% through systematic debugging and code optimization</li>
                </ul>
            </div>

            <!-- Experience Item 2 -->
            <div class="relative pl-8 sm:pl-12 experience-item">
                <div class="absolute -left-[5px] top-2 w-2.5 h-2.5 rounded-full bg-text"></div>
                
                <div class="flex flex-col sm:flex-row sm:items-baseline justify-between gap-1 mb-2">
                    <h3 class="text-xl sm:text-2xl font-bold uppercase">Technical Support Staff</h3>
                    <span class="text-sm font-mono opacity-60 shrink-0">Feb 2025 — May 2025</span>
                </div>
                <h4 class="text-lg font-medium uppercase mb-4 text-primary">Commission on Elections (COMELEC)</h4>
                <ul class="list-disc list-outside ml-4 space-y-2 text-base sm:text-lg opacity-80 leading-relaxed">
                    <li>Provided critical on-site technical support during the National Elections, ensuring zero-failure operation of Automated Counting Machines (ACMs) across 8 precincts in a high-pressure environment</li>
                    <li>Troubleshot hardware and software discrepancies in real-time with 98% issue resolution rate, maintaining the integrity and speed of voting data processing for 8,000+ voters</li>
                </ul>
            </div>

            <!-- Experience Item 3 -->
            <div class="relative pl-8 sm:pl-12 experience-item">
                <div class="absolute -left-[5px] top-2 w-2.5 h-2.5 rounded-full bg-text"></div>
                
                <div class="flex flex-col sm:flex-row sm:items-baseline justify-between gap-1 mb-2">
                    <h3 class="text-xl sm:text-2xl font-bold uppercase">Head of Graphics</h3>
                    <span class="text-sm font-mono opacity-60 shrink-0">Apr 2023 — Apr 2025</span>
                </div>
                <h4 class="text-lg font-medium uppercase mb-4 text-primary">Fortem Ardeas Esports</h4>
                <ul class="list-disc list-outside ml-4 space-y-2 text-base sm:text-lg opacity-80 leading-relaxed">
                    <li>Built the organization's foundational visual identity from scratch, establishing a scalable design system and UI/UX guidelines for all digital, broadcast, and physical assets</li>
                    <li>Designed dynamic graphics for internal tournaments and partner collaborations (Moonton Philippines, Tier One Entertainment), achieving 100K+ engagements by creating cohesive social campaigns, live‑stream overlays, and event branding.</li>
                </ul>
            </div>

        </div>
      </div>

      <!-- Awards Section -->
      <div ref="awardsSection" class="max-w-4xl mx-auto mb-16 sm:mb-20 px-4 tracking-tighter">
        <h2 class="text-3xl sm:text-4xl font-bold uppercase mb-8 sm:mb-12">Awards & Recognition</h2>
        <div class="space-y-6 text-left">
            <!-- Award 1 -->
            <div class="group border-b border-text/20 pb-6 hover:border-primary hover:pl-4 transition-all duration-300 cursor-default award-item">
                <div class="flex flex-col md:flex-row md:items-baseline justify-between gap-2">
                    <h3 class="text-xl sm:text-2xl font-bold uppercase group-hover:text-primary transition-colors">Champion</h3>
                    <span class="text-sm sm:text-base opacity-60 font-mono">2025</span>
                </div>
                <p class="text-base sm:text-lg uppercase mt-2 text-text/80 group-hover:text-text transition-colors">C(Old) (St)art Hackathon by Old.St Labs</p>
            </div>

            <!-- Award 2 -->
            <div class="group border-b border-text/20 pb-6 hover:border-primary hover:pl-4 transition-all duration-300 cursor-default award-item">
                <div class="flex flex-col md:flex-row md:items-baseline justify-between gap-2">
                    <h3 class="text-xl sm:text-2xl font-bold uppercase group-hover:text-primary transition-colors">Finalist</h3>
                    <span class="text-sm sm:text-base opacity-60 font-mono">2025</span>
                </div>
                <p class="text-base sm:text-lg uppercase mt-2 text-text/80 group-hover:text-text transition-colors">GDAP GameOn Awards - Professional Track Category</p>
            </div>

            <!-- Award 3 -->
            <div class="group border-b border-text/20 pb-6 hover:border-primary hover:pl-4 transition-all duration-300 cursor-default award-item">
                <div class="flex flex-col md:flex-row md:items-baseline justify-between gap-2">
                    <h3 class="text-xl sm:text-2xl font-bold uppercase group-hover:text-primary transition-colors">Best Paper Presentation</h3>
                    <span class="text-sm sm:text-base opacity-60 font-mono">2025</span>
                </div>
                <p class="text-base sm:text-lg uppercase mt-2 text-text/80 group-hover:text-text transition-colors">UMAK 8th Research Congress</p>
            </div>
        </div>
      </div>

      <div ref="contactSection" class="text-center w-full max-w-4xl mx-auto px-2 sm:px-4">
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
        <div class="flex items-center justify-center gap-4 sm:gap-8 text-lg sm:text-2xl md:text-3xl lg:text-4xl flex-wrap uppercase tracking-tighter">
          <a 
        href="https://github.com/exadizon" 
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
          <a 
        href="https://www.linkedin.com/in/exadizon/" 
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
          <a 
        href="/adizon_resume.pdf" 
        target="_blank"
        class="group relative flex items-center gap-1 sm:gap-2 cursor-hover transition-all duration-300"
          >
        <span class="relative group-hover:text-primary transition-colors duration-300">
          RESUME
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
