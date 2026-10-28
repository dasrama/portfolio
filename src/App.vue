<script setup>
import { ref } from 'vue'
import {
  TopWebBar,
  PrimaryButton,
  SecondaryButton,
  IconButton,
  FloatingActionButton,
  Container,
  Card,
  Grid,
  Row,
  Column,
  SectionHeader,
  BottomNavigation,
  SideDrawer,
} from './components/ui'

const drawerOpen = ref(false)
const activeBottomNav = ref('home')

const mobileNavItems = [
  { key: 'home', label: 'Home', icon: 'home' },
  { key: 'experience', label: 'Experience', icon: 'work_history' },
  { key: 'tech-stack', label: 'Skills', icon: 'developer_board' },
  { key: 'projects', label: 'Projects', icon: 'folder' },
  { key: 'connect-with-me', label: 'Contact', icon: 'connect_without_contact' },
]

const profileLinks = {
  github: 'https://github.com/dasrama',
  linkedin: 'https://www.linkedin.com/in/rama-das/',
  resume: 'https://drive.google.com/file/d/1ba-nA_uwBCBLvl1npZn22uDEYVbnTllp/view?usp=sharing',
  email: 'ramaprasad047@gmail.com',
  leetcode: 'https://leetcode.com/rama047',
}

function goHome() {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function scrollToId(id) {
  const target = document.getElementById(id)
  if (target) {
    target.scrollIntoView({ behavior: 'smooth' })
  }
}

function navigateToSection(id) {
  scrollToId(id)
}

function onBottomNavigate(item) {
  const key = item.key
  if (key === 'home') {
    goHome()
    return
  }
  scrollToId(key)
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
  <div class="min-h-screen bg-background-light font-display text-slate-900 selection:bg-primary/30 dark:bg-background-dark dark:text-slate-100">
    <TopWebBar title="Rama Prasad Das">
      <template #left>
        <button
          type="button"
          class="terminal-glow flex size-10 items-center justify-center rounded-lg bg-primary transition-transform hover:scale-105"
          @click="goHome"
        >
          <span class="material-symbols-outlined font-bold text-black">terminal</span>
        </button>
      </template>

      <template #center>
        <button class="text-sm font-medium text-slate-300 transition-colors hover:text-secondary" type="button" @click="goHome">
          Home
        </button>
        <button class="text-sm font-medium text-slate-300 transition-colors hover:text-secondary" type="button" @click="navigateToSection('experience')">
          Experience
        </button>
        <button class="text-sm font-medium text-slate-300 transition-colors hover:text-secondary" type="button" @click="navigateToSection('tech-stack')">
          Skills
        </button>
        <button class="text-sm font-medium text-slate-300 transition-colors hover:text-secondary" type="button" @click="navigateToSection('projects')">
          Projects
        </button>
        <button class="text-sm font-medium text-slate-300 transition-colors hover:text-secondary" type="button" @click="navigateToSection('connect-with-me')">
          Contact
        </button>
      </template>

      <template #right>
        <PrimaryButton class="hidden md:inline-flex" @click="openResume">Resume</PrimaryButton>
        <IconButton icon="menu" label="Open menu" class="md:hidden" @click="drawerOpen = true" />
      </template>
    </TopWebBar>

    <SideDrawer v-model="drawerOpen" title="Navigation">
      <Column gap="1rem" align="stretch">
        <button class="text-left text-sm font-medium text-slate-200 transition-colors hover:text-primary" type="button" @click="goHome(); drawerOpen = false">Home</button>
        <button class="text-left text-sm font-medium text-slate-200 transition-colors hover:text-primary" type="button" @click="navigateToSection('experience'); drawerOpen = false">Experience</button>
        <button class="text-left text-sm font-medium text-slate-200 transition-colors hover:text-primary" type="button" @click="navigateToSection('tech-stack'); drawerOpen = false">Skills</button>
        <button class="text-left text-sm font-medium text-slate-200 transition-colors hover:text-primary" type="button" @click="navigateToSection('projects'); drawerOpen = false">Projects</button>
        <button class="text-left text-sm font-medium text-slate-200 transition-colors hover:text-primary" type="button" @click="navigateToSection('connect-with-me'); drawerOpen = false">Contact</button>
        <PrimaryButton
          class="mt-2"
          @click="
            openResume();
            drawerOpen = false
          "
        >
          Resume
        </PrimaryButton>
      </Column>
    </SideDrawer>

    <div class="relative overflow-x-hidden">
      <div class="pointer-events-none fixed inset-0 grid-bg"></div>

      <Container size="xl" as="main" class="relative z-10 pb-8 md:pb-12">
        <section id="hero" class="scroll-mt-24 overflow-hidden pt-4 md:pt-8">
          <Row justify="space-between" align="center" gap="2.5rem" class="flex-col lg:flex-row">
            <Column gap="1.25rem" class="max-w-2xl text-center lg:text-left">
              <div class="inline-flex items-center gap-2 self-center rounded-full border border-primary/20 bg-primary/10 px-3 py-1 lg:self-start">
                <span class="relative flex h-2 w-2">
                  <span class="absolute inline-flex h-full w-full animate-ping rounded-full bg-primary opacity-75"></span>
                  <span class="relative inline-flex h-2 w-2 rounded-full bg-primary"></span>
                </span>
                <span class="text-xs font-bold uppercase tracking-widest text-primary">Open to Backend / SWE Roles</span>
              </div>

              <h1 class="bg-gradient-to-r from-white via-white to-secondary/50 bg-clip-text font-bold leading-tight text-transparent text-4xl lg:text-6xl">
                Rama Prasad Das — Software Developer
              </h1>

              <p class="text-lg text-slate-400">
                Software developer focused on backend systems, LLM integration, RAG, and distributed services. Experienced with
                <span class="border-b-2 border-primary text-white">FastAPI, Python, React, Vue, MongoDB, Redis, RabbitMQ, Docker, and AWS</span>.
              </p>

              <Row justify="center" gap="1rem" class="pt-2 lg:justify-start">
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
                  <span class="text-[10px] font-bold uppercase tracking-widest text-slate-500">pipeline_worker.py</span>
                </div>
                <pre class="overflow-x-auto font-mono text-xs md:text-sm leading-relaxed text-slate-300"><code><span class="text-slate-500"># Async Event Consumer &amp; Classification</span>
<span class="text-purple-400">@app.post</span>(<span class="text-emerald-300">"/v1/ingest"</span>)
<span class="text-primary font-semibold">async def</span> <span class="text-sky-300">process_event</span>(task: <span class="text-amber-300">TaskPayload</span>):
    cached = <span class="text-primary font-semibold">await</span> redis.get(<span class="text-emerald-300">f"cache:{task.id}"</span>)
    <span class="text-primary font-semibold">if</span> cached:
        <span class="text-primary font-semibold">return</span> json.loads(cached)

    result = <span class="text-primary font-semibold">await</span> rag_pipeline.classify(task.data)
    <span class="text-primary font-semibold">await</span> rabbitmq.publish(<span class="text-emerald-300">"events"</span>, result)
    <span class="text-primary font-semibold">return</span> {<span class="text-emerald-300">"status"</span>: <span class="text-emerald-300">"dispatched"</span>, <span class="text-emerald-300">"id"</span>: task.id}</code></pre>
              </Card>
            </Column>
          </Row>
        </section>

        <section id="experience" class="scroll-mt-24">
          <SectionHeader icon="work_history" title="Work Experience" />

          <Column gap="1rem" align="stretch">
            <Card>
              <div class="flex flex-wrap items-center justify-between gap-2">
                <span class="text-xs font-bold uppercase tracking-widest text-primary">May 2025 — June 2026</span>
                <span class="rounded-full border border-secondary/20 bg-secondary/10 px-2.5 py-0.5 text-xs font-semibold text-secondary">Internship</span>
              </div>
              <h3 class="mt-2 text-xl font-bold text-white">Backend Engineer Intern</h3>
              <p class="mt-0.5 text-sm font-medium text-slate-400">Easework AI</p>
              <ul class="mt-4 list-disc pl-5 space-y-2 text-sm leading-relaxed text-slate-300">
                <li>Authored and deployed an LLM-powered classification and RAG system to auto-determine purchase request categories and trigger workflows, improving decision accuracy from 60% to 90% and reducing manual approvals by 10%.</li>
                <li>Collaborated on shared logging and metrics (Prometheus, Loki) across microservices, cutting debug time by 20%.</li>
                <li>Designed MongoDB Atlas Search indexes with custom analyzers, enabling full-text search and reducing query latency by 25% while maintaining auditability.</li>
                <li>Led development of a configurable Kanban workflow engine with rule-based validations, automating ~70% of manual approval checks.</li>
              </ul>
            </Card>

            <Card>
              <div class="flex flex-wrap items-center justify-between gap-2">
                <span class="text-xs font-bold uppercase tracking-widest text-secondary">May 2024 — November 2024</span>
                <span class="rounded-full border border-secondary/20 bg-secondary/10 px-2.5 py-0.5 text-xs font-semibold text-secondary">Internship</span>
              </div>
              <h3 class="mt-2 text-xl font-bold text-white">Backend Engineer Intern</h3>
              <p class="mt-0.5 text-sm font-medium text-slate-400">Splitkaro</p>
              <ul class="mt-4 list-disc pl-5 space-y-2 text-sm leading-relaxed text-slate-300">
                <li>Built referral and reward system with scratch-card logic, boosting user engagement by 8% and accelerating subscriptions.</li>
                <li>Optimized expense computation using MongoDB aggregation pipelines, reducing latency by 12% under production load.</li>
                <li>Standardized currency conversion across 15 subsidiaries, reducing reconciliation errors by 22%.</li>
              </ul>
            </Card>
          </Column>
        </section>

        <section id="education" class="scroll-mt-24">
          <SectionHeader icon="school" title="Education" />
          <Column gap="1rem" align="stretch">
            <Card>
              <div class="flex flex-wrap items-center justify-between gap-2">
                <span class="text-xs font-bold uppercase tracking-widest text-secondary">2022 — 2026</span>
                <span class="rounded-full border border-primary/20 bg-primary/10 px-2.5 py-0.5 text-xs font-semibold text-primary">Undergraduate</span>
              </div>
              <h3 class="mt-2 text-xl font-bold text-white">IIIT Bhubaneswar</h3>
              <p class="mt-0.5 text-sm font-medium text-slate-400">Bachelor of Technology (B.Tech) in Computer Engineering</p>
            </Card>
          </Column>
        </section>

        <section id="tech-stack" class="scroll-mt-24">
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
              <p class="mt-3 text-slate-300">Git, GitHub Actions, Docker, AWS, CI/CD, Postman, Selenium</p>
            </Card>
            <Card>
              <h4 class="text-sm font-bold uppercase tracking-widest text-secondary">AI & Messaging</h4>
              <p class="mt-3 text-slate-300">LLM integration, RAG, Prompt engineering, RabbitMQ, Redis</p>
            </Card>
          </Grid>
        </section>

        <section id="projects" class="scroll-mt-24">
          <SectionHeader icon="folder_special" title="Featured Projects" />

          <Grid :cols="2" gap="1rem" min-col-width="280px">
            <Card interactive class="flex flex-col justify-between">
              <div>
                <h3 class="text-lg font-bold text-primary">Event-Driven Video-to-MP3 Converter</h3>
                <div class="mt-2.5 flex flex-wrap gap-1.5">
                  <span class="rounded-md border border-primary/20 bg-primary/10 px-2 py-0.5 text-xs font-medium text-primary">RabbitMQ</span>
                  <span class="rounded-md border border-primary/20 bg-primary/10 px-2 py-0.5 text-xs font-medium text-primary">Docker</span>
                  <span class="rounded-md border border-primary/20 bg-primary/10 px-2 py-0.5 text-xs font-medium text-primary">Microservices</span>
                </div>
                <p class="mt-3 text-sm leading-relaxed text-slate-400">Event-driven microservice architecture using RabbitMQ for upload, conversion and notifications; Dockerized for independent deployments and 35% faster end-to-end processing.</p>
              </div>
              <Row justify="end" class="mt-4 pt-2">
                <SecondaryButton @click="() => openExternalLink('https://github.com/dasrama/vmp3')">View on GitHub</SecondaryButton>
              </Row>
            </Card>

            <Card interactive class="flex flex-col justify-between">
              <div>
                <h3 class="text-lg font-bold text-primary">Heal AI — Discord Medical Assistant</h3>
                <div class="mt-2.5 flex flex-wrap gap-1.5">
                  <span class="rounded-md border border-primary/20 bg-primary/10 px-2 py-0.5 text-xs font-medium text-primary">Gemini AI</span>
                  <span class="rounded-md border border-primary/20 bg-primary/10 px-2 py-0.5 text-xs font-medium text-primary">Redis</span>
                  <span class="rounded-md border border-primary/20 bg-primary/10 px-2 py-0.5 text-xs font-medium text-primary">Discord API</span>
                </div>
                <p class="mt-3 text-sm leading-relaxed text-slate-400">AI-powered Discord assistant using Gemini AI, with Redis session caching and concurrency-safe handling supporting 1,000+ simultaneous interactions.</p>
              </div>
              <Row justify="end" class="mt-4 pt-2">
                <SecondaryButton @click="() => openExternalLink('https://github.com/dasrama/HealAI-Chatbot')">View on GitHub</SecondaryButton>
              </Row>
            </Card>

            <Card interactive class="flex flex-col justify-between">
              <div>
                <h3 class="text-lg font-bold text-primary">RBI Macro Data Automation</h3>
                <div class="mt-2.5 flex flex-wrap gap-1.5">
                  <span class="rounded-md border border-primary/20 bg-primary/10 px-2 py-0.5 text-xs font-medium text-primary">Selenium</span>
                  <span class="rounded-md border border-primary/20 bg-primary/10 px-2 py-0.5 text-xs font-medium text-primary">Pandas</span>
                  <span class="rounded-md border border-primary/20 bg-primary/10 px-2 py-0.5 text-xs font-medium text-primary">ETL Pipeline</span>
                </div>
                <p class="mt-3 text-sm leading-relaxed text-slate-400">Automated data extraction and ingestion pipeline using Selenium and Python to scrape, validate, and structure macroeconomic time-series data from the Reserve Bank of India (RBI) portal.</p>
              </div>
              <Row justify="end" class="mt-4 pt-2">
                <SecondaryButton @click="() => openExternalLink('https://github.com/dasrama/rbi-macro-automation')">View on GitHub</SecondaryButton>
              </Row>
            </Card>
          </Grid>
        </section>

        <section id="connect-with-me" class="scroll-mt-24">
          <SectionHeader icon="connect_without_contact" title="Connect With Me" />

          <Card class="relative overflow-hidden text-center py-4">
            <div class="pointer-events-none absolute inset-0 glow-overlay-green opacity-30"></div>
            <div class="relative z-10">
              <h3 class="mb-3 text-2xl font-bold">Let's Connect!</h3>
              <p class="mx-auto mb-6 max-w-lg text-slate-400">
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

      <footer class="relative z-10 border-t border-secondary/10 bg-background-dark px-6 py-8 pb-24 md:pb-8">
        <Container size="xl" as="div" class="flex flex-col items-center justify-between gap-4 md:flex-row">
          <div class="flex items-center gap-3">
            <div class="flex size-8 items-center justify-center rounded-lg border border-primary/30 bg-primary/20">
              <span class="material-symbols-outlined text-sm text-primary">terminal</span>
            </div>
            <span class="text-sm font-bold uppercase tracking-widest text-slate-300">Rama Prasad Das</span>
          </div>
          <p class="text-xs text-slate-500">© {{ new Date().getFullYear() }} Rama Prasad Das. All rights reserved.</p>
        </Container>
      </footer>

    </div>
  </div>
</template>
