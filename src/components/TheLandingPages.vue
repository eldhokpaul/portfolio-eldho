<template>
  <fragment>
    <section class="h-full py-8 max-w-screen-lg mx-auto flex flex-col items-center justify-center">
      <transition name="fade" appear>
        <h1 class="text-7xl text-gray-800 dark:text-white text-center font-semibold leading-none tracking-tighter mb-4">Eldho K Paul</h1>
      </transition>
      <transition name="fade" appear>
        <h2 class="text-2xl text-gray-600 dark:text-gray-400 opacity-75 font-normal leading-tight mb-8">Senior Software Engineer</h2>
      </transition>
      <Transition name="fade" appear>
        <div class="flex flex-row space-x-4">
          <button class="bg-sky-blue dark:bg-dark-primary py-3 px-7 rounded-md text-white flex items-center gap-3" @click="navigateToGithub">
            <v-icon name="brands/github" class="fill-current" />
            Github
          </button>
          <button class="bg-sky-blue dark:bg-dark-primary py-3 px-7 rounded-md text-white flex items-center gap-3" @click="navigateToGithub">
            <v-icon name="brands/github" class="fill-current" />
            Github2
          </button>
          <button class="bg-sky-blue dark:bg-dark-primary py-3 px-7 rounded-md text-white flex items-center gap-3" @click="navigateToGithub">
            <v-icon name="brands/github" class="fill-current" />
            Github3
          </button>
        </div>
      </Transition>
    </section>

    <section class="h-1/3 bg-light-primary dark:bg-dark-primary">
      <div class="flex-1 flex flex-row max-w-screen-lg w-full mx-auto gap-x-3 md:py-3 overflow-y-hidden">
        <nav
          class="fixed h-full md:bg-transparent dark:md:bg-transparent md:border-0 md:relative md:w-1/5 order-first overflow-y-auto md:transition-none transition-[width] duration-500 ease-in-out"
          :class="{
            'bg-white dark:bg-dark-secondary w-60 border-r border-gray-100 dark:border-gray-600': mobileMenuIsOpen,
            'w-0': !mobileMenuIsOpen,
          }"
          v-click-outside="clickOutside"
          v-if="hasSidebarSlot">
          <slot :name="slotsNames.sidebar" />
        </nav>

        <main class="flex-1 overflow-y-auto box">
          <slot :name="slotsNames.content" />
        </main>
      </div>
    </section>

    <section class="h-full">
      <div class="h-full max-w-screen-lg mx-auto flex flex-col items-center justify-center">
        <h1 class="text-7xl text-gray-800 dark:text-white font-semibold leading-none tracking-tighter mb-4">features</h1>
        <div class="max-w-sm mx-auto grid gap-6 md:grid-cols-2 lg:grid-cols-3 items-start md:max-w-2xl lg:max-w-none mt-8">
          <UiFeatureCard icon="th-large" header="Layouts" description="3 responsive layouts" />
          <UiFeatureCard icon="tailwind" header="Tailwind" description="Design based on Tailwind" />
          <UiFeatureCard icon="moon" header="Themes" description="Black & white themes" />
        </div>
      </div>
    </section>
  </fragment>
</template>

<script>
import { themes } from "@/store";
import UiFeatureCard from "@/components/ui/UiFeatureCard";
import mobileSidebarMixin from "@/layouts/mixins/mobileSidebarMixin";
// import CenteredLayout from "@/layouts/CenteredLayout";

export default {
  name: "TheLandingPages",
  mixins: [mobileSidebarMixin],
  components: { UiFeatureCard },
  computed: {
    currentThemeIsDark() {
      return this.$store.state.theme === themes.dark;
    },
    hasSidebarSlot() {
      return !!this.$slots[this.slotsNames.sidebar];
    },
  },
  methods: {
    navigateToGithub() {
      window.location.href = "https://github.com/eldhokpaul";
    },
  },
  data() {
    return {
      slotsNames: {
        sidebar: "sidebar",
        content: "content",
      },
      clickOutside: {
        handler: "closeMobileSidebar",
        exclude: ["mobileSidebarButton"],
      },
    };
  },
};
</script>
