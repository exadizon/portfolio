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
  $gsap.from(aboutContent.value.children, {
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
          toggleActions: 'play none none reverse'
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
        toggleActions: 'play none none reverse'
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
        start: 'top 80%',
        toggleActions: 'play none none reverse'
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
        toggleActions: 'play none none reverse'
      },
      y: 30,
      opacity: 0,
      duration: 0.8,
      stagger: 0.1,
      ease: 'power3.out'
    })
  }
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
      <!-- <div class="w-full h-32 sm:h-40 md:h-48 lg:h-56 xl:h-64 bg-primary mx-auto mb-8 sm:mb-12"></div> -->

      <!-- Short Bio -->
      <div class="max-w-3xl mx-auto mb-12 sm:mb-16 text-lg sm:text-xl md:text-2xl uppercase leading-tight px-4 tracking-tighter">
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
        
        <!-- Design Section -->
        <div class="text-left skill-group">
          <div class="flex items-center gap-4 mb-8 border-b border-text/10 pb-4">
            <div class="w-10 h-10 sm:w-12 sm:h-12 rounded-full border border-primary flex items-center justify-center text-primary shrink-0">
              <Icon name="ph:paint-brush-bold" class="text-xl sm:text-2xl" />
            </div>
            <h3 class="text-2xl sm:text-3xl md:text-4xl text-primary font-bold uppercase tracking-tighter">Design</h3>
          </div>

          <div class="grid grid-cols-1 md:grid-cols-12 gap-8 md:gap-12">
            <!-- Left: Competencies -->
            <div class="md:col-span-4 space-y-6">
              <h4 class="text-sm font-bold uppercase tracking-widest opacity-60">Core Competencies</h4>
              <div class="flex flex-wrap gap-2">
                <span class="px-4 py-2 bg-text/5 rounded-md text-xs sm:text-sm uppercase tracking-wide hover:bg-primary hover:text-background transition-all duration-300 cursor-default">UI/UX Design</span>
                <span class="px-4 py-2 bg-text/5 rounded-md text-xs sm:text-sm uppercase tracking-wide hover:bg-primary hover:text-background transition-all duration-300 cursor-default">Web Design</span>
                <span class="px-4 py-2 bg-text/5 rounded-md text-xs sm:text-sm uppercase tracking-wide hover:bg-primary hover:text-background transition-all duration-300 cursor-default">Mobile App Design</span>
                <span class="px-4 py-2 bg-text/5 rounded-md text-xs sm:text-sm uppercase tracking-wide hover:bg-primary hover:text-background transition-all duration-300 cursor-default">Prototyping</span>
                <span class="px-4 py-2 bg-text/5 rounded-md text-xs sm:text-sm uppercase tracking-wide hover:bg-primary hover:text-background transition-all duration-300 cursor-default">Interaction Design</span>
                <span class="px-4 py-2 bg-text/5 rounded-md text-xs sm:text-sm uppercase tracking-wide hover:bg-primary hover:text-background transition-all duration-300 cursor-default">Branding</span>
              </div>
            </div>

            <!-- Right: Tools -->
            <div class="md:col-span-8 space-y-6">
              <h4 class="text-sm font-bold uppercase tracking-widest opacity-60">Tools</h4>
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-x-12 gap-y-4">
                <div class="flex items-center gap-3 group cursor-default">
                  <Icon name="ph:figma-logo-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                  <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Figma</span>
                </div>
                <div class="flex items-center gap-3 group cursor-default">
                  <Icon name="ph:image-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                  <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Photoshop</span>
                </div>
                <div class="flex items-center gap-3 group cursor-default">
                  <Icon name="ph:pen-nib-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                  <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Illustrator</span>
                </div>
                <div class="flex items-center gap-3 group cursor-default">
                  <Icon name="ph:film-strip-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                  <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">After Effects</span>
                </div>
                <div class="flex items-center gap-3 group cursor-default">
                  <Icon name="ph:video-camera-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                  <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Premiere Pro</span>
                </div>
                <div class="flex items-center gap-3 group cursor-default">
                  <Icon name="ph:paint-bucket-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                  <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Canva</span>
                </div>
                <div class="flex items-center gap-3 group cursor-default">
                  <Icon name="ph:bezier-curve-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                  <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Affinity</span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Development Section -->
        <div class="text-left skill-group">
          <div class="flex items-center gap-4 mb-8 border-b border-text/10 pb-4">
            <div class="w-10 h-10 sm:w-12 sm:h-12 rounded-full border border-primary flex items-center justify-center text-primary shrink-0">
              <Icon name="ph:code-bold" class="text-xl sm:text-2xl" />
            </div>
            <h3 class="text-2xl sm:text-3xl md:text-4xl text-primary font-bold uppercase tracking-tighter">Development</h3>
          </div>

          <div class="grid grid-cols-1 md:grid-cols-12 gap-8 md:gap-12">
            <!-- Left: Competencies -->
            <div class="md:col-span-4 space-y-6">
              <h4 class="text-sm font-bold uppercase tracking-widest opacity-60">Core Competencies</h4>
              <div class="flex flex-wrap gap-2">
                <span class="px-4 py-2 bg-text/5 rounded-md text-xs sm:text-sm uppercase tracking-wide hover:bg-primary hover:text-background transition-all duration-300 cursor-default">Full Stack Engineering</span>
                <span class="px-4 py-2 bg-text/5 rounded-md text-xs sm:text-sm uppercase tracking-wide hover:bg-primary hover:text-background transition-all duration-300 cursor-default">Cross-Platform Mobile</span>
                <span class="px-4 py-2 bg-text/5 rounded-md text-xs sm:text-sm uppercase tracking-wide hover:bg-primary hover:text-background transition-all duration-300 cursor-default">RESTful API Design</span>
                <span class="px-4 py-2 bg-text/5 rounded-md text-xs sm:text-sm uppercase tracking-wide hover:bg-primary hover:text-background transition-all duration-300 cursor-default">Cloud Infrastructure</span>
                <span class="px-4 py-2 bg-text/5 rounded-md text-xs sm:text-sm uppercase tracking-wide hover:bg-primary hover:text-background transition-all duration-300 cursor-default">Database Architecture</span>
                <span class="px-4 py-2 bg-text/5 rounded-md text-xs sm:text-sm uppercase tracking-wide hover:bg-primary hover:text-background transition-all duration-300 cursor-default">Agile Methodologies</span>
              </div>
            </div>

            <!-- Right: Tech Stack -->
            <div class="md:col-span-8 space-y-8">
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-x-12 gap-y-10">
                <!-- Frontend Group -->
                <div class="space-y-4">
                  <h5 class="text-xs font-bold uppercase tracking-widest text-primary opacity-80 border-b border-text/10 pb-2">Frontend</h5>
                  <div class="space-y-3">
                    <div class="flex items-center gap-3 group cursor-default">
                      <Icon name="ph:atom-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                      <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">React / Next.js</span>
                    </div>
                    <div class="flex items-center gap-3 group cursor-default">
                      <Icon name="ph:brackets-angle-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                      <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Vue / Nuxt</span>
                    </div>
                    <div class="flex items-center gap-3 group cursor-default">
                      <Icon name="ph:magic-wand-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                      <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Tailwind / GSAP</span>
                    </div>
                    <div class="flex items-center gap-3 group cursor-default">
                      <Icon name="ph:file-html-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                      <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">HTML / CSS / JS</span>
                    </div>
                  </div>
                </div>

                <!-- Mobile Group -->
                <div class="space-y-4">
                  <h5 class="text-xs font-bold uppercase tracking-widest text-primary opacity-80 border-b border-text/10 pb-2">Mobile</h5>
                  <div class="space-y-3">
                    <div class="flex items-center gap-3 group cursor-default">
                      <Icon name="ph:device-mobile-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                      <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Flutter</span>
                    </div>
                    <div class="flex items-center gap-3 group cursor-default">
                      <Icon name="ph:atom-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                      <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">React Native</span>
                    </div>
                    <div class="flex items-center gap-3 group cursor-default">
                      <Icon name="ph:android-logo-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                      <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Kotlin / Java</span>
                    </div>
                  </div>
                </div>

                <!-- Backend Group -->
                <div class="space-y-4">
                  <h5 class="text-xs font-bold uppercase tracking-widest text-primary opacity-80 border-b border-text/10 pb-2">Backend</h5>
                  <div class="space-y-3">
                    <div class="flex items-center gap-3 group cursor-default">
                      <Icon name="ph:terminal-window-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                      <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Node.js / Python / PHP</span>
                    </div>
                    <div class="flex items-center gap-3 group cursor-default">
                      <Icon name="ph:cloud-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                      <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Supabase / Firebase / Appwrite</span>
                    </div>
                    <div class="flex items-center gap-3 group cursor-default">
                      <Icon name="ph:database-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                      <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">MySQL / PostgreSQL</span>
                    </div>
                  </div>
                </div>

                <!-- Tools Group -->
                <div class="space-y-4">
                  <h5 class="text-xs font-bold uppercase tracking-widest text-primary opacity-80 border-b border-text/10 pb-2">Tools</h5>
                  <div class="space-y-3">
                    <div class="flex items-center gap-3 group cursor-default">
                      <Icon name="ph:git-branch-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                      <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Git / GitHub / Docker</span>
                    </div>
                    <div class="flex items-center gap-3 group cursor-default">
                      <Icon name="ph:chat-circle-text-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                      <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">Gemini / ChatGPT / Claude / Qwen</span>
                    </div>
                    <div class="flex items-center gap-3 group cursor-default">
                      <Icon name="ph:robot-bold" class="text-xl opacity-60 group-hover:text-primary group-hover:opacity-100 transition-all" /> 
                      <span class="text-sm font-medium group-hover:translate-x-1 transition-transform duration-300">GitHub Copilot / Cursor / Windsurf</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
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
