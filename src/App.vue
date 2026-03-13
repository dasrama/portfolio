<script setup>
import { nextTick, ref } from 'vue'
import ExperienceTechStack from './components/ExperienceTechStack.vue'
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

const showTechStackPage = ref(false)
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

function openTechStackPage() {
  showTechStackPage.value = true
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
        <PrimaryButton class="hidden md:inline-flex">Resume</PrimaryButton>
        <IconButton icon="menu" label="Open menu" class="md:hidden" @click="drawerOpen = true" />
      </template>
    </TopWebBar>

    <SideDrawer v-model="drawerOpen" title="Navigation">
      <Column gap="1rem" align="stretch">
        <button class="text-left text-sm font-medium text-slate-200" type="button" @click="goHome(); drawerOpen = false">Home</button>
        <button class="text-left text-sm font-medium text-slate-200" type="button" @click="navigateToSection('about'); drawerOpen = false">About</button>
        <button class="text-left text-sm font-medium text-slate-200" type="button" @click="openTechStackPage(); drawerOpen = false">Tech Stack</button>
        <button class="text-left text-sm font-medium text-slate-200" type="button" @click="navigateToSection('projects'); drawerOpen = false">Projects</button>
        <PrimaryButton @click="drawerOpen = false">Resume</PrimaryButton>
      </Column>
    </SideDrawer>

    <div
      v-if="!showTechStackPage"
      class="relative min-h-screen overflow-x-hidden bg-background-light font-display text-slate-900 selection:bg-primary/30 dark:bg-background-dark dark:text-slate-100"
    >
      <div class="pointer-events-none fixed inset-0 grid-bg"></div>

      <Container size="xl" as="main" class="relative z-10 pb-28">
        <section class="overflow-hidden pb-20 pt-20">
          <Breadcrumb :items="[{ label: 'Home' }, { label: 'Portfolio' }]" />

          <Row justify="space-between" align="center" gap="4rem" class="mt-8 flex-col lg:flex-row">
            <Column gap="1.5rem" class="max-w-2xl text-center lg:text-left">
              <div class="inline-flex items-center gap-2 self-center rounded-full border border-primary/20 bg-primary/10 px-3 py-1 lg:self-start">
                <span class="relative flex h-2 w-2">
                  <span class="absolute inline-flex h-full w-full animate-ping rounded-full bg-primary opacity-75"></span>
                  <span class="relative inline-flex h-2 w-2 rounded-full bg-primary"></span>
                </span>
                <span class="text-xs font-bold uppercase tracking-widest text-primary">Available for new systems</span>
              </div>

              <h1 class="bg-gradient-to-r from-white via-white to-secondary/50 bg-clip-text text-5xl font-bold leading-tight text-transparent lg:text-7xl">
                Backend Engineer &amp; <br />Systems Builder
              </h1>

              <p class="text-lg text-slate-400">
                Building resilient distributed systems with
                <span class="border-b-2 border-primary text-white">FastAPI, Python, MongoDB, Redis, Docker, and AWS</span>.
              </p>

              <Row justify="center" gap="1rem" class="lg:justify-start">
                <PrimaryButton @click="scrollToId('projects')">View Work</PrimaryButton>
                <SecondaryButton>GitHub</SecondaryButton>
              </Row>
            </Column>

            <Card class="w-full max-w-2xl blue-glow">
              <div class="mb-4 flex items-center justify-between border-b border-secondary/10 pb-3">
                <Row gap="0.375rem">
                  <div class="size-3 rounded-full bg-red-500/50"></div>
                  <div class="size-3 rounded-full bg-amber-500/50"></div>
                  <div class="size-3 rounded-full bg-primary/50"></div>
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
          </Row>
        </section>

        <section id="about" class="py-24">
          <SectionHeader
            icon="person"
            eyebrow="01"
            title="About the Architect"
            subtitle="I specialize in building high-throughput backend systems at the intersection of cloud infrastructure and performance engineering."
          />

          <Grid :cols="2" gap="1rem" min-col-width="240px">
            <Card>
              <h3 class="text-xl font-bold text-primary">50+</h3>
              <p class="mt-2 text-xs font-bold uppercase tracking-widest text-slate-500">APIs Deployed</p>
            </Card>
            <Card>
              <h3 class="text-xl font-bold text-secondary">99.9%</h3>
              <p class="mt-2 text-xs font-bold uppercase tracking-widest text-slate-500">Uptime Target</p>
            </Card>
            <Card>
              <h3 class="text-xl font-bold text-white">5ms</h3>
              <p class="mt-2 text-xs font-bold uppercase tracking-widest text-slate-500">Avg Latency</p>
            </Card>
            <Card>
              <h3 class="text-xl font-bold text-primary">10k+</h3>
              <p class="mt-2 text-xs font-bold uppercase tracking-widest text-slate-500">Docker Pulls</p>
            </Card>
          </Grid>
        </section>

        <section id="projects" class="py-24">
          <SectionHeader icon="folder_special" eyebrow="02" title="Featured Projects" />

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

        <section id="contact" class="py-24">
          <SectionHeader
            icon="mail"
            eyebrow="03"
            title="Connect With Me"
            subtitle="Looking for a systems architect or backend specialist? Let's discuss your next infrastructure project."
          />

          <Card class="blue-glow">
            <form @submit.prevent="submitMessage">
              <Grid :cols="2" gap="1rem" min-col-width="220px">
                <label class="flex flex-col gap-2 text-xs font-bold uppercase tracking-widest text-slate-500">
                  Name
                  <input class="rounded-xl border border-secondary/20 bg-background-dark/50 px-4 py-3 text-white focus:border-secondary focus:outline-none" type="text" placeholder="John Doe" />
                </label>

                <label class="flex flex-col gap-2 text-xs font-bold uppercase tracking-widest text-slate-500">
                  Email
                  <input class="rounded-xl border border-secondary/20 bg-background-dark/50 px-4 py-3 text-white focus:border-secondary focus:outline-none" type="email" placeholder="john@example.com" />
                </label>
              </Grid>

              <label class="mt-4 flex flex-col gap-2 text-xs font-bold uppercase tracking-widest text-slate-500">
                Message
                <textarea class="rounded-xl border border-secondary/20 bg-background-dark/50 px-4 py-3 text-white focus:border-secondary focus:outline-none" rows="5" placeholder="Tell me about your system requirements..."></textarea>
              </label>

              <LoadingButton class="mt-6" :loading="sendingMessage" loading-text="Sending..." full-width type="submit">
                Send Mission Brief
              </LoadingButton>
            </form>
          </Card>
        </section>
      </Container>

      <footer class="relative z-10 border-t border-secondary/10 bg-background-dark px-6 py-10">
        <Container size="xl" as="div" class="flex flex-col items-center justify-between gap-6 md:flex-row">
          <div class="flex items-center gap-3">
            <div class="flex size-8 items-center justify-center rounded-lg border border-primary/30 bg-primary/20">
              <span class="material-symbols-outlined text-sm text-primary">terminal</span>
            </div>
            <span class="text-sm font-bold uppercase tracking-widest">System<span class="text-primary">.io</span></span>
          </div>
          <Row gap="1rem">
            <IconButton icon="public" label="Twitter" size="sm" />
            <IconButton icon="code" label="GitHub" size="sm" />
            <IconButton icon="mail" label="Email" size="sm" />
          </Row>
        </Container>
      </footer>

      <BottomNavigation v-model="activeBottomNav" :items="mobileNavItems" @navigate="onBottomNavigate" />
      <FloatingActionButton icon="north" label="Back to top" @click="scrollToId('about')" />
    </div>

    <ExperienceTechStack v-else />
  </div>
</template>
