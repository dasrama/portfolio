<script setup>
import { ref } from 'vue'
import {
  PrimaryButton,
  SecondaryButton,
  Container,
  Card,
  Grid,
  Row,
  Column,
  SectionHeader,
  Breadcrumb,
  Tabs,
} from './ui'

const activeStackTab = ref('backend')

const stackTabs = [
  { key: 'backend', label: 'Backend', value: 'backend' },
  { key: 'devops', label: 'DevOps', value: 'devops' },
]
</script>

<template>
  <div class="relative min-h-screen overflow-x-hidden bg-background-light font-display text-slate-900 selection:bg-primary selection:text-black dark:bg-background-dark dark:text-slate-100">
    <div class="pointer-events-none fixed inset-0 particle-bg"></div>
    <div class="pointer-events-none fixed left-[-10%] top-[-10%] h-[50%] w-[50%] rounded-full glow-overlay-green opacity-50"></div>
    <div class="pointer-events-none fixed bottom-[-10%] right-[-10%] h-[50%] w-[50%] rounded-full glow-overlay-blue opacity-50"></div>

    <div class="relative z-10">
      <Container size="lg" as="main" class="py-12 md:py-20">
        <Breadcrumb :items="[{ label: 'Home' }, { label: 'Experience & Tech Stack' }]" />

        <section id="about" class="mb-20 mt-8 scroll-mt-32">
          <h1 class="mb-6 bg-gradient-to-r from-slate-900 via-primary to-secondary bg-clip-text text-5xl font-bold leading-tight tracking-tighter text-transparent dark:from-white dark:via-primary dark:to-secondary md:text-7xl">
            Experience &amp; <br />Tech Stack
          </h1>
          <p class="max-w-2xl border-l-2 border-secondary/30 pl-6 text-lg text-slate-600 dark:text-slate-400 md:text-xl">
            A journey through backend engineering, scalable cloud architectures, and building intelligent AI-driven systems.
          </p>
        </section>

        <section class="mb-24">
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

        <section id="tech-stack" class="mb-24 scroll-mt-32">
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

        <section id="projects" class="mb-24 scroll-mt-32">
          <SectionHeader icon="folder_special" title="Selected Projects" />

          <Card class="relative overflow-hidden text-center">
            <div class="pointer-events-none absolute inset-0 glow-overlay-blue opacity-30"></div>
            <div class="relative z-10">
              <h3 class="mb-4 text-2xl font-bold">Interested in collaborating?</h3>
              <p class="mx-auto mb-8 max-w-lg text-slate-400">
                I'm always open to discussing backend challenges, AI implementation, or cloud scaling strategies.
              </p>
              <Row justify="center" gap="0.75rem">
                <PrimaryButton>Send Message</PrimaryButton>
                <SecondaryButton>LinkedIn</SecondaryButton>
              </Row>
            </div>
          </Card>
        </section>
      </Container>
    </div>
  </div>
</template>
