<script setup>
import { onMounted, ref } from 'vue'

// SEO Meta Tags for Works Page
useSeoMeta({
  title: 'Works - Exequel Adizon',
  description: 'Explore the creative works and projects by Exequel Adizon (@adiluexe). From web development to mobile apps, discover innovative digital solutions and creative projects.',
  ogTitle: 'Works - Exequel Adizon',
  ogDescription: 'Explore the creative works and projects by Exequel Adizon (@adiluexe). From web development to mobile apps, discover innovative digital solutions and creative projects.',
  ogImage: '/images/og-image.jpg',
  twitterTitle: 'Works - Exequel Adizon',
  twitterDescription: 'Explore the creative works and projects by Exequel Adizon (@adiluexe). From web development to mobile apps, discover innovative digital solutions and creative projects.',
  twitterImage: '/images/og-image.jpg',
  twitterCard: 'summary_large_image'
})

const { $gsap } = useNuxtApp()

const worksContent = ref(null)
const titleTextRef = ref(null)
let morphTimeline = null

const texts = [
  '<span class="font-spice">W</span>orks',
  '<span class="font-spice">P</span>rojects',
  '<span class="font-spice">C</span>reations'
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

const projects = ref([
  { 
    id: 1, 
    name: 'ALARP', 
    description: 'A full-stack Flutter app featuring interactive 3D anatomical models and a custom 2D collimation simulator. Architected with Supabase and PostgreSQL to handle secure authentication and a real-time leaderboard for 100+ concurrent users.',
    stack: 'FLUTTER / SUPABASE / CUSTOMPAINT / 3DVIEWER',
    image: '/works/alarp_showcase.png',
    github: 'https://github.com/adiluexe/alarp',
    website: null, // Mobile app - no website
    type: 'Mobile'
  },
  { 
    id: 2, 
    name: 'FLOWFIT', 
    description: 'Champion of the C(Old) (St)art Hackathon 2025. A gamified health app featuring a "Virtual Pet" system that evolves based on real-time user habits. Architected the frontend logic to translate complex health metrics into an intuitive, child-friendly interface using Flutter and WearOS.',
    stack: 'FLUTTER / TENSORFLOW / WEARABLES',
    image: '/works/flowfit_showcase.png',
    color: '#4ECDC4', // Teal/Aqua for fitness/water
    github: 'https://github.com/KpG782/flowfit',
    website: null,
    type: 'Hackathon Winner'
  },
  { 
    id: 3, 
    name: 'BATHALA', 
    description: 'GDAP GameOn 2025 Finalist. A web-based roguelike built with a modular, component-driven architecture. Features a complex state management system and a rule-based Dynamic Difficulty Adjustment (DDA) algorithm that adapts gameplay in real-time based on player performance metrics.',
    stack: 'PHASER.JS / TYPESCRIPT',
    image: '/works/bathala_showcase.png',
    color: '#8D5B4C', // Brown/Earth for mythology
    github: 'https://github.com/devlocke-acsad/bathala',
    website: 'https://bathala.quest',
    type: 'Game + Web'
  },
  { 
    id: 4, 
    name: 'ARS (AUTO REPAIR SERVICE)', 
    description: 'Best Paper Presentation at the University of Makati 8th Research Congress. An "Uber for repairs" platform connecting users with mechanics through real-time booking and geolocation. Features a dual-interface system for service requests and job management.',
    stack: 'FLUTTER / GOOGLE MAPS',
    image: '/works/ars_showcase.png',
    color: '#FF6B6B', // Red/Orange for urgency/repair
    github: null,
    website: null,
    type: 'Mobile'
  },
  { 
    id: 5, 
    name: 'HERONFIT', 
    description: 'A fitness app for the University of Makati gym that helps you track workouts, monitor progress, get personalized recommendations, and book sessions—with an integrated gym management system.',
    stack: 'FLUTTER / NEXT.JS / REACT / SUPABASE / FLASK',
    image: '/works/heronfit_showcase.png',
    github: 'https://github.com/skypiea-tech/heronfit',
    website: null, // Mobile app - no website
    type: 'Mobile + Web'
  },
  { 
    id: 6, 
    name: 'LET\'S WORK TOGETHER', 
    description: 'Have a project in mind? Let\'s collaborate and create something amazing',
    stack: 'YOUR IDEAS + MY SKILLS',
    image: null, // Special case for collaboration card
    github: null,
    website: 'mailto:exequel.adizon@gmail.com',
    type: 'Collaboration'
  }
])

onMounted(() => {
  $gsap.from(worksContent.value.children, {
    duration: 1,
    y: 50,
    opacity: 0,
    stagger: 0.1,
    ease: 'power4.out',
  })
})
</script>

<template>
  <div class="w-full min-h-screen flex flex-col justify-center text-center py-8 sm:py-12 md:py-16 lg:py-24 xl:py-32 px-4 sm:px-6 md:px-8 lg:px-12 xl:px-0">
    <div ref="worksContent" class="w-full mx-auto">
      <h1 
        class="text-4xl sm:text-5xl md:text-6xl lg:text-7xl xl:text-8xl font-normal uppercase tracking-tighter mt-16 md:mt-12 lg:mt-0 xl:mt-0 font-satoshi cursor-hover leading-none mb-6 sm:mb-8 md:mb-10 lg:mb-12 xl:mb-16"
        @mouseenter="startMorphEffect"
        @mouseleave="stopMorphEffect"
      >
        <span ref="titleTextRef"><span class="font-spice">W</span>orks</span>
      </h1>
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-4 sm:gap-6 md:gap-8 p-4 sm:p-6 md:p-8">
        <ProjectCard v-for="project in projects" :key="project.id" :project="project" />
      </div>
    </div>
  </div>
</template>
