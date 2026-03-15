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

function openLinkedInMessage() {
  openExternalLink(`${profileLinks.linkedin}?trk=public_profile_message-button`)
}

function openResume() {
  openExternalLink(profileLinks.resume)
}
</script>

<template>
  <div>
    <TopWebBar title="System.io">
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
                Backend Engineer &amp; <br />Systems Builder
              </h1>

              <p class="text-lg text-slate-400">
                Building resilient distributed systems with
                <span class="border-b-2 border-primary text-white">FastAPI, Python, MongoDB, Redis, Docker, and AWS</span>.
              </p>

              <Row justify="center" gap="1rem" class="lg:justify-start">
                <PrimaryButton @click="scrollToId('projects')">View Work</PrimaryButton>
                <SecondaryButton @click="openGitHub">GitHub</SecondaryButton>
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
          <SectionHeader icon="work_history" title="Professional Path" />

          <Column gap="1rem" align="stretch">
            <Card>
              <p class="text-sm font-bold uppercase tracking-widest text-primary">Jan 2022 - Present</p>
              <h3 class="mt-2 text-2xl font-bold">Backend Developer</h3>
              <p class="mt-1 font-medium text-slate-400">Early-Stage AI Startup</p>
              <ul class="mt-4 space-y-2 text-slate-300">
                <li>Architected real-time AI inference pipelines processing 1M+ requests daily.</li>
                <li>Optimized AWS Lambda cold starts by 40% through runtime and image optimizations.</li>
                <li>Implemented vector indexing for high-performance semantic search.</li>
              </ul>
            </Card>

            <Card>
              <p class="text-sm font-bold uppercase tracking-widest text-slate-500">Mar 2020 - Dec 2021</p>
              <h3 class="mt-2 text-2xl font-bold">Software Engineer</h3>
              <p class="mt-1 font-medium text-slate-400">CloudSystems Tech</p>
              <ul class="mt-4 space-y-2 text-slate-300">
                <li>Designed distributed microservices handling transactional data with 99.9% uptime.</li>
                <li>Built internal dashboards with Prometheus and Grafana.</li>
              </ul>
            </Card>
          </Column>
        </section>

        <section id="tech-stack" class="scroll-mt-32">
          <SectionHeader icon="developer_board" title="Technical Arsenal" />

          <Tabs v-model="activeStackTab" :tabs="stackTabs">
            <template #panel="{ active }">
              <Grid :cols="2" gap="1rem" min-col-width="260px">
                <Card>
                  <h4 class="text-sm font-bold uppercase tracking-widest text-secondary">Core Backend</h4>
                  <p class="mt-3 text-slate-300" :class="active === 'backend' ? 'text-primary' : ''">Node.js, Python, Go, FastAPI</p>
                </Card>
                <Card>
                  <h4 class="text-sm font-bold uppercase tracking-widest text-secondary">Databases</h4>
                  <p class="mt-3 text-slate-300" :class="active === 'backend' ? 'text-primary' : ''">PostgreSQL, Redis, Pinecone, MongoDB</p>
                </Card>
                <Card>
                  <h4 class="text-sm font-bold uppercase tracking-widest text-secondary">DevOps & Cloud</h4>
                  <p class="mt-3 text-slate-300" :class="active === 'devops' ? 'text-secondary' : ''">AWS, Docker, Terraform, CI/CD</p>
                </Card>
                <Card>
                  <h4 class="text-sm font-bold uppercase tracking-widest text-secondary">Tools</h4>
                  <p class="mt-3 text-slate-300" :class="active === 'devops' ? 'text-secondary' : ''">Git, Grafana, Postman, Sentry</p>
                </Card>
              </Grid>
            </template>
          </Tabs>
        </section>

        <section id="projects">
          <SectionHeader icon="folder_special" title="Featured Projects" />

          <Tabs v-model="projectTab" :tabs="projectTabs">
            <template #panel="{ active }">
              <Grid :cols="2" gap="1rem" min-col-width="280px">
                <Card interactive>
                  <h3 class="text-lg font-bold" :class="active === 'featured' ? 'text-primary' : 'text-white'">Distributed Load Balancer</h3>
                  <p class="mt-3 text-sm text-slate-400">Go-based load balancer with health checks and service discovery.</p>
                </Card>
                <Card interactive>
                  <h3 class="text-lg font-bold" :class="active === 'infra' ? 'text-secondary' : 'text-white'">Real-time Analytics Engine</h3>
                  <p class="mt-3 text-sm text-slate-400">Kafka + FastAPI analytics with low-latency Redis cache.</p>
                </Card>
              </Grid>
            </template>
          </Tabs>
        </section>

        <section id="connect-with-me" class="scroll-mt-32">
          <SectionHeader icon="connect_without_contact" title="Connect With Me" />

          <Card class="relative overflow-hidden text-center">
            <div class="pointer-events-none absolute inset-0 glow-overlay-green opacity-30"></div>
            <div class="relative z-10">
              <h3 class="mb-4 text-2xl font-bold">Let's Connect!</h3>
              <p class="mx-auto mb-8 max-w-lg text-slate-400">
                Feel free to reach out for collaborations or backend engineering discussions.
              </p>
              <Row justify="center" gap="0.75rem">
                <PrimaryButton>Contact Me</PrimaryButton>
                <SecondaryButton @click="openLinkedInMessage">LinkedIn Message</SecondaryButton>
                <SecondaryButton @click="openGitHub">GitHub</SecondaryButton>
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
            <span class="text-sm font-bold uppercase tracking-widest">System<span class="text-primary">.io</span></span>
          </div>
        </Container>
      </footer>

      <BottomNavigation v-model="activeBottomNav" :items="mobileNavItems" @navigate="onBottomNavigate" />
      <FloatingActionButton icon="north" label="Back to top" @click="scrollToId('about')" />
    </div>
  </div>
</template>
