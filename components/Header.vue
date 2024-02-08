<template>
  <header>
    <nav class="px-5 md:px-7 lg:px-6 py-5 opacity-0 scroll-trigger-header" :class="{ 'opacity-100': header }">
      <div class="flex flex-wrap justify-between items-center mx-auto max-w-screen-lg py-1 md:py-2">
        <a href="#" class="flex lg:basis-1/3 md:basis-1/4 sm:basis-full shrink items-center w-auto">
          <portfolio-header-name />
        </a>
        <div class="flex lg:basis-1/3 md:basis-1/4 sm:basis-full shrink gap-5 md:gap-3 md:order-2 w-auto justify-end">
          <ClientOnly>
            <template v-for="(social, index) in socialLinks" :key="index">
              <a :href="social.link" target="_blank" class="text-2xl text-gray-200 hover:text-white transition">
                <!-- <font-awesome-layers> -->
                <font-awesome-icon :icon="['fab', social.icon]" />
                <!-- </font-awesome-layers> -->
              </a>
            </template>
          </ClientOnly>
        </div>
        <div class="flex lg:basis-1/3 md:basis-1/2 sm:basis-full justify-between items-center shrink w-full md:w-auto md:order-1 pt-0 lg:px-0 md:px-4 sm:md:px-7">
          <ul class="flex mt-4 font-normal justify-between flex-row space-x-8 md:mt-0 w-full">
            <template v-for="(nav, index) in navLinks" :key="index">
              <li>
                <a
                  href="#"
                  class="group text-gray-200 hover:text-white py-3 relative w-full transition"
                  @click="smoothScrollTo(nav.target)"
                >
                  {{ nav.link }}
                  <span class="ease absolute bottom-0 h-0.5 block w-0 bg-gradient-to-r group-hover:from-teal-400 group-hover:to-yellow-200 transition-all duration-200 group-hover:w-full"></span>
                </a>
              </li>
            </template>
          </ul>
        </div>
        <!-- Hamburger icon -->
        <!-- <div class="md:hidden flex basis-1/2 justify-end">
          <button
            type="button"
            class="text-white bg-white hover:bg-gray-900 focus:outline-none focus:ring-4 focus:ring-gray-300 font-medium rounded-lg text-sm px-3 py-2.5 me-2 dark:bg-gray-800 dark:hover:bg-gray-700 dark:focus:ring-gray-700 dark:border-gray-700"
          >
            <svg xmlns="http://www.w3.org/2000/svg" fill="currentColor" height="16" width="14" viewBox="0 0 448 512">
              <path d="M0 96C0 78.3 14.3 64 32 64H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H32C14.3 128 0 113.7 0 96zM0 256c0-17.7 14.3-32 32-32H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H32c-17.7 0-32-14.3-32-32zM448 416c0 17.7-14.3 32-32 32H32c-17.7 0-32-14.3-32-32s14.3-32 32-32H416c17.7 0 32 14.3 32 32z"/>
            </svg>
          </button>
        </div> -->
      </div>
    </nav>
  </header>
</template>

<script setup lang="ts">
// import { userAccountStore } from '@/stores/account'

// Enable before deploying in the production
// const { $gsap, $ScrollTrigger } = useNuxtApp()

// Temporarily enabled as '$ScrollSmoother' needs subscription when deployed in the production
const { $gsap, $ScrollSmoother, $ScrollTrigger } = useNuxtApp()

const header = ref(false)
// const accountStore = userAccountStore()

// Temporarily enabled as '$ScrollSmoother' needs subscription when deployed in the production
let smoother = null

// Utilizing reactive with provide and inject
// const state = inject('counter_state')
// watch(() => state.counter, (newVal, oldVal) => {
//   console.log('Counter value: ', newVal)
// })

const socialLinks = ref([
  { link: 'https://www.facebook.com/8.chiee', icon: 'facebook' },
  { link: 'https://www.linkedin.com/in/archie-galangue-81ba89141/', icon: 'linkedin' },
  { link: 'https://github.com/chie-ai', icon: 'github' }
])

const navLinks = ref([
  { link: 'Projects', target: 'projects' },
  { link: 'Technology', target: 'technology' },
  { link: 'Work Experience', target: 'work-experience' }
])

onBeforeMount(() => {
  header.value = true

  // Temporarily enabled as '$ScrollSmoother' needs subscription when deployed in the production
  // create the smooth scroller FIRST!
  smoother = $ScrollSmoother.create({ smooth: 1, effects: true })
})

onMounted(() => {
  $gsap.fromTo('.scroll-trigger-header', { y: -100, opacity: 0 }, { y: 0, duration: 1.1, opacity: 1 })

  /**
   * Set token in the account store with pinia
   *
    setTimeout(() => {
      accountStore.setToken('eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJPbmxpbmUgSldUIEJ1aWxkZXIiLCJpYXQiOjE3MDEzOTQxOTUsImV4cCI6MTczMjkzMDE5NSwiYXVkIjoid3d3LmV4YW1wbGUuY29tIiwic3ViIjoianJvY2tldEBleGFtcGxlLmNvbSIsIkdpdmVuTmFtZSI6IkpvaG5ueSIsIlN1cm5hbWUiOiJSb2NrZXQiLCJFbWFpbCI6Impyb2NrZXRAZXhhbXBsZS5jb20iLCJSb2xlIjpbIk1hbmFnZXIiLCJQcm9qZWN0IEFkbWluaXN0cmF0b3IiXX0.3TycB3XqozWTz0FVDGp5QFp_RSq0IJVk1m9Rgu31gtQ')
    }, 3000)
   */
})

const smoothScrollTo = (target: string) => {
  $gsap.to(window, {
    duration: 1,
    scrollTo: `#${target}`,
    ease: "power2",
  })
}
</script>
