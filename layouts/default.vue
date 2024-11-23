<template>
  <div
    class="default-layout"
    @click="useAppStore().current_x_size >= 1024 ? '' : (isMinimized = true)"
  >
    <TheSidebar
      class="hidden lg:block"
      :links="sideBarlinks"
      :isMinimized="isMinimized"
      @toggleSidebar="toggleSidebar"
      @closeSideBar="isMinimized = true"
    />

    <div
      class="group inside-view rounded-xl fixed end-[var(--sidebar-navbar-x-margin)] lg:transition-all lg:duration-[800ms] overflow-y-scroll hide-scrollbar"
      :class="{
        'sidebar-minimized': isMinimized,
        'sidebar-not-minimized': !isMinimized,
      }"
    >
      <TheNavbar :isMinimized="isMinimized" />

      <!-- Pages -->
      <slot />

      <!-- Mobile Sidebar -->
      <aside
        @click.stop
        class="shadow-lg rounded-se-3xl rounded-ee-3xl bg-whiteColor fixed group-[.sidebar-not-minimized]:start-0 -start-[250px] top-0 h-full w-[250px] lg:hidden transition-all duration-[800ms] z-[999]"
      >
        <SideBarContent
          :isMinimized="isMinimized"
          @closeSideBar="isMinimized = true"
        />

        <div
          class="lg:hidden absolute -end-8 top-1/2 -translate-y-1/2 z-50"
          aria-label="close"
          role="button"
        >
          <SidebarMenuIcon
            class="shadow-black"
            :isMinimized="isMinimized"
            @toggleSidebar="toggleSidebar"
          />
        </div>
      </aside>
    </div>
  </div>
</template>

<script setup lang="ts">
const isMinimized = ref(false);

const toggleSidebar = () => {
  isMinimized.value = !isMinimized.value;
};

const sideBarlinks = [
  {
    label: "Home",
    icon: "i-heroicons-chart-bar",
    to: "/",
  },
  {
    label: "Users",
    icon: "i-heroicons-users",
    to: "/users",
  },
];
</script>

<style lang="postcss" scoped>
.inside-view {
  width: calc(100vw - (var(--sidebar-navbar-x-margin) * 2));
  height: calc(100vh - ((var(--navbar-top-margin) * 2) + var(--navbar-height)));
  max-height: calc(100vh - (var(--navbar-top-margin) * 2));

  top: calc(var(--navbar-top-margin) + var(--navbar-height));

  @screen lg {
    width: calc(
      100vw - var(--max-sidebar-width) - (var(--sidebar-navbar-x-margin) * 2)
    );

    &.sidebar-minimized {
      width: calc(
        100vw - var(--min-sidebar-width) - (var(--sidebar-navbar-x-margin) * 2)
      );
    }
  }
}
</style>
