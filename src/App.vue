<script setup>
import { nextTick, ref } from 'vue'
import {
  TopWebBar,
  PrimaryButton,
  SecondaryButton,
  IconButton,
  FloatingActionButton,
  LoadingButton,
  Container,
  Card,
  Grid,
  Row,
  Column,
  SectionHeader,
  BottomNavigation,
  SideDrawer,
  Breadcrumb,
  Tabs,
} from './components/ui'

const drawerOpen = ref(false)
const projectTab = ref('featured')
const sendingMessage = ref(false)
const activeBottomNav = ref('home')

const projectTabs = [
  { key: 'featured', label: 'Featured', value: 'featured' },
  { key: 'infra', label: 'Infrastructure', value: 'infra' },
]

const mobileNavItems = [
  { key: 'home', label: 'Home', icon: 'home' },
  { key: 'about', label: 'About', icon: 'person' },
  { key: 'tech', label: 'Tech', icon: 'developer_board' },
  { key: 'projects', label: 'Projects', icon: 'folder' },
]

const profileLinks = {
  github: 'https://github.com/dasrama',
  linkedin: 'https://www.linkedin.com/in/rama-das/',
  resume: 'https://drive.google.com/file/d/1ba-nA_uwBCBLvl1npZn22uDEYVbnTllp/view?usp=sharing',
  email: 'ramaprasad047@gmail.com',
  leetcode: 'https://leetcode.com/rama047',
}

function goHome() {
  if (showTechStackPage.value) {
    showTechStackPage.value = false
    nextTick(() => {
      window.scrollTo({ top: 0, behavior: 'smooth' })
    })
    return
  }

  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function scrollToId(id) {
  const target = document.getElementById(id)
  if (target) target.scrollIntoView({ behavior: 'smooth' })
}

function navigateToSection(id) {
  if (showTechStackPage.value) {
    showTechStackPage.value = false
    nextTick(() => {
      scrollToId(id)
    })
    return
  }

  scrollToId(id)
}

function onBottomNavigate(item) {
  const key = item.key
  if (key === 'tech') {
    openTechStackPage()
    return
  }

  if (key === 'home') {
    window.scrollTo({ top: 0, behavior: 'smooth' })
    return
  }

  scrollToId(key)
}

function submitMessage() { 
  sendingMessage.value = true
  setTimeout(() => {
    sendingMessage.value = false
  }, 1000)
}

function openExternalLink(url) {
  window.open(url, '_blank', 'noopener,noreferrer')
}

function openGitHub() {
  openExternalLink(profileLinks.github)
}

function openEmail() {
  openExternalLink(`mailto:${profileLinks.email}`)
}

function openLeetCode() {
  openExternalLink(profileLinks.leetcode)
}

function openLinkedInMessage() {
  openExternalLink(`${profileLinks.linkedin}?trk=public_profile_message-button`)
}

function openResume() {
  openExternalLink(profileLinks.resume)
}
</script>

<template>
  <div>
    <TopWebBar title="Rama Prasad Das">
      <template #left>
        <div class="terminal-glow flex size-10 items-center justify-center rounded-lg bg-primary">
          <span class="material-symbols-outlined font-bold text-black">terminal</span>
        </div>
      </template>

      <template #center>
        <button class="text-sm font-medium text-slate-200 transition-colors hover:text-secondary" type="button" @click="goHome">
          Home
        </button>
        <button class="text-sm font-medium text-slate-200 transition-colors hover:text-secondary" type="button" @click="navigateToSection('about')">
          About
        </button>
        <button class="text-sm font-medium text-slate-200 transition-colors hover:text-secondary" type="button" @click="openTechStackPage">
          Tech Stack
        </button>
        <button class="text-sm font-medium text-slate-200 transition-colors hover:text-secondary" type="button" @click="navigateToSection('projects')">
          Projects
        </button>
      </template>

      <template #right>
        <PrimaryButton class="hidden md:inline-flex" @click="openResume">Resume</PrimaryButton>
        <IconButton icon="menu" label="Open menu" class="md:hidden" @click="drawerOpen = true" />
      </template>
    </TopWebBar>

    <SideDrawer v-model="drawerOpen" title="Navigation">
      <Column gap="1rem" align="stretch">
        <button class="text-left text-sm font-medium text-slate-200" type="button" @click="goHome(); drawerOpen = false">Home</button>
        <button class="text-left text-sm font-medium text-slate-200" type="button" @click="navigateToSection('about'); drawerOpen = false">About</button>
        <button class="text-left text-sm font-medium text-slate-200" type="button" @click="openTechStackPage(); drawerOpen = false">Tech Stack</button>
        <button class="text-left text-sm font-medium text-slate-200" type="button" @click="navigateToSection('projects'); drawerOpen = false">Projects</button>
        <PrimaryButton
          @click="
            openResume();
            drawerOpen = false
          "
        >
          Resume
        </PrimaryButton>
      </Column>
    </SideDrawer>

    <div
      v-if="!showTechStackPage"
      class="relative min-h-screen overflow-x-hidden bg-background-light font-display text-slate-900 selection:bg-primary/30 dark:bg-background-dark dark:text-slate-100"
    >
      <div class="pointer-events-none fixed inset-0 grid-bg"></div>

      <Container size="xl" as="main" class="relative z-10 pb-20">
        <section class="overflow-hidden">
          <Row justify="space-between" align="center" gap="3rem" class="mt-6 flex-col lg:flex-row">
            <Column gap="1rem" class="max-w-2xl text-center lg:text-left">
              <div class="inline-flex items-center gap-2 self-center rounded-full border border-primary/20 bg-primary/10 px-3 py-1 lg:self-start">
                <span class="relative flex h-2 w-2">
                  <span class="absolute inline-flex h-full w-full animate-ping rounded-full bg-primary opacity-75"></span>
                  <span class="relative inline-flex h-2 w-2 rounded-full bg-primary"></span>
                </span>
                <span class="text-xs font-bold uppercase tracking-widest text-primary">Available for new systems</span>
              </div>

              <h1 class="bg-gradient-to-r from-white via-white to-secondary/50 bg-clip-text font-bold leading-tight text-transparent text-4xl lg:text-6xl">
                Rama Prasad Das — Software Developer
              </h1>

              <p class="text-lg text-slate-400">
                Software developer focused on backend systems, LLM integration, RAG, and distributed services. Experienced with
                <span class="border-b-2 border-primary text-white">FastAPI, Python, MongoDB, Redis, RabbitMQ, Docker, and AWS</span>.
              </p>

              <Row justify="center" gap="1rem" class="lg:justify-start">
                <PrimaryButton @click="scrollToId('projects')">View Work</PrimaryButton>
                <SecondaryButton @click="openGitHub">GitHub</SecondaryButton>
                <SecondaryButton @click="openEmail">Email</SecondaryButton>
              </Row>
            </Column>

            <Column class="w-full max-w-2xl lg:w-auto">
              <Card class="blue-glow">
                <div class="mb-4 flex items-center justify-between border-b border-secondary/10 pb-3">
                  <Row gap="0.375rem">
                    <div class="mac-dot red"></div>
                    <div class="mac-dot amber"></div>
                    <div class="mac-dot green"></div>
                  </Row>
                  <span class="text-[10px] font-bold uppercase tracking-widest text-slate-500">system_logs.py</span>
                </div>
                <pre class="overflow-x-auto font-mono text-sm leading-relaxed text-slate-300">class SystemArchitect:
    def __init__(self):
        self.stack = ["FastAPI", "Redis", "K8s"]
        self.status = "Optimizing..."

    async def deploy(self):
        return await self.scale_horizontally()</pre>
              </Card>
            </Column>
          </Row>
        </section>

        <section>
          <SectionHeader icon="work_history" title="Work Experience" />

            <Column gap="1rem" align="stretch">
              <Card>
                <p class="text-sm font-bold uppercase tracking-widest text-primary">May 2025 - Present</p>
                <h3 class="mt-2 text-2xl font-bold">Backend Developer, Easework AI</h3>
                <p class="mt-1 font-medium text-slate-400">Easework AI</p>
                <ul class="mt-4 space-y-2 text-slate-300">
                  <li>Authored and deployed an LLM-powered classification and RAG system to auto-determine purchase request categories and trigger workflows, improving decision accuracy from 60% to 90% and reducing manual approvals by 10%.</li>
                  <li>Collaborated on shared logging and metrics (Prometheus, Loki) across microservices, cutting debug time by 20%.</li>
                  <li>Designed MongoDB Atlas Search indexes with custom analyzers, enabling full-text search and reducing query latency by 25% while maintaining auditability.</li>
                  <li>Led development of a configurable Kanban workflow engine with rule-based validations, automating ~70% of manual approval checks.</li>
                </ul>
              </Card>

              <Card>
                <p class="text-sm font-bold uppercase tracking-widest text-secondary">May 2024 - Nov 2024</p>
                <h3 class="mt-2 text-2xl font-bold">Backend Developer Intern, Splitkaro</h3>
                <p class="mt-1 font-medium text-slate-400">Splitkaro</p>
                <ul class="mt-4 space-y-2 text-slate-300">
                  <li>Built referral and reward system with scratch-card logic, boosting user engagement by 8% and accelerating subscriptions.</li>
                  <li>Optimized expense computation using MongoDB aggregation pipelines, reducing latency by 12% under production load.</li>
                  <li>Standardized currency conversion across 15 subsidiaries, reducing reconciliation errors by 22%.</li>
                </ul>
              </Card>
            </Column>

          <SectionHeader icon="school" title="Education" />
            <Column gap="1rem" align="stretch">
              <Card>
                <p class="text-sm font-bold uppercase tracking-widest text-secondary">2022 -- 2026</p>
                <h3 class="mt-2 text-2xl font-bold">International Institute of Information Technology, Bhubaneswar</h3>
                <p class="mt-1 font-medium text-slate-400">Bachelor of Technology (B.Tech) in Computer Engineering</p>
              </Card>
            </Column>
        </section>

        <section id="tech-stack" class="scroll-mt-32">
          <SectionHeader icon="developer_board" title="Skills" />

          <Grid :cols="2" gap="1rem" min-col-width="260px">
            <Card>
              <h4 class="text-sm font-bold uppercase tracking-widest text-secondary">Programming Languages</h4>
              <p class="mt-3 text-slate-300">Python, Java, JavaScript, SQL, NoSQL</p>
            </Card>
            <Card>
              <h4 class="text-sm font-bold uppercase tracking-widest text-secondary">Frameworks & Databases</h4>
              <p class="mt-3 text-slate-300">FastAPI, Django, Flask, Vue.js, PostgreSQL, MongoDB, Redis</p>
            </Card>
            <Card>
              <h4 class="text-sm font-bold uppercase tracking-widest text-secondary">Tools & Platforms</h4>
              <p class="mt-3 text-slate-300">Git, GitHub Actions, Docker, AWS, CI/CD, Postman</p>
            </Card>
            <Card>
              <h4 class="text-sm font-bold uppercase tracking-widest text-secondary">AI & Messaging</h4>
              <p class="mt-3 text-slate-300">LLM integration, RAG, Prompt engineering, RabbitMQ, Redis</p>
            </Card>
          </Grid>
        </section>

        <section id="projects">
          <SectionHeader icon="folder_special" title="Featured Projects" />

          <Grid :cols="2" gap="1rem" min-col-width="280px">
            <Card interactive>
              <h3 class="text-lg font-bold text-primary">Event-Driven Video-to-MP3 Converter</h3>
              <p class="mt-3 text-sm text-slate-400">Event-driven microservice architecture using RabbitMQ for upload, conversion and notifications; Dockerized for independent deployments and 35% faster end-to-end processing.</p>
              <Row justify="end" class="mt-4">
                <SecondaryButton @click="() => openExternalLink('https://github.com/dasrama/vmp3')">View on GitHub</SecondaryButton>
              </Row>
            </Card>

            <Card interactive>
              <h3 class="text-lg font-bold text-primary">Heal AI — Discord Medical Assistant</h3>
              <p class="mt-3 text-sm text-slate-400">AI-powered Discord assistant using Gemini AI, with Redis session caching and concurrency-safe handling supporting 1,000+ simultaneous interactions.</p>
              <Row justify="end" class="mt-4">
                <SecondaryButton @click="() => openExternalLink('https://github.com/dasrama/HealAI-Chatbot')">View on GitHub</SecondaryButton>
              </Row>
            </Card>

            <Card interactive>
              <h3 class="text-lg font-bold text-primary">Secure Mail View</h3>
              <p class="mt-3 text-sm text-slate-400">Secure Gmail viewer built with OAuth2 and JWT-authenticated FastAPI endpoints and a Streamlit frontend for safe attachment access.</p>
              <Row justify="end" class="mt-4">
                <SecondaryButton @click="() => openExternalLink('https://github.com/dasrama/secure_mail_listings')">View on GitHub</SecondaryButton>
              </Row>
            </Card>
          </Grid>
        </section>

        <section id="connect-with-me" class="scroll-mt-32">
          <SectionHeader icon="connect_without_contact" title="Connect With Me" />

          <Card class="relative overflow-hidden text-center">
            <div class="pointer-events-none absolute inset-0 glow-overlay-green opacity-30"></div>
            <div class="relative z-10">
              <h3 class="mb-4 text-2xl font-bold">Let's Connect!</h3>
              <p class="mx-auto mb-8 max-w-lg text-slate-400">
                Reach out for collaborations, backend engineering, or AI projects.
              </p>
              <Row justify="center" gap="0.75rem">
                <PrimaryButton @click="openEmail">Email</PrimaryButton>
                <SecondaryButton @click="openLinkedInMessage">LinkedIn</SecondaryButton>
                <SecondaryButton @click="openGitHub">GitHub</SecondaryButton>
                <SecondaryButton @click="openLeetCode">LeetCode</SecondaryButton>
              </Row>
            </div>  
          </Card>
        </section>
      </Container>

      <footer class="relative z-10 border-t border-secondary/10 bg-background-dark px-6 py-8">
        <Container size="xl" as="div" class="flex flex-col items-center justify-between gap-6 md:flex-row">
          <div class="flex items-center gap-3">
            <div class="flex size-8 items-center justify-center rounded-lg border border-primary/30 bg-primary/20">
              <span class="material-symbols-outlined text-sm text-primary">terminal</span>
            </div>
            <span class="text-sm font-bold uppercase tracking-widest">Rama Prasad Das</span>
          </div>
        </Container>
      </footer>

      <BottomNavigation v-model="activeBottomNav" :items="mobileNavItems" @navigate="onBottomNavigate" />
      <FloatingActionButton icon="north" label="Back to top" @click="scrollToId('about')" />
    </div>
  </div>
</template>
