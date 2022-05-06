<template>
  <div>
    <header class="absolute z-50 w-full px-2 py-2 bg-black md:static">
      <div class="mx-auto md:max-w-3xl md:flex md:items-center">
        <div
          class="flex items-center justify-between w-full h-16 px-6 mx-auto md:flex md:px-0"
        >
          <h1>
            <nuxt-link
              class="inline-block py-2 mr-4 text-2xl font-bold leading-relaxed text-white whitespace-no-wrap"
              to="/"
            >
              Nuxt Cafe
            </nuxt-link>
          </h1>
          <div class="text-white md:hidden">
            <button class="focus:outline-none" @click="toggleStatus">
              <!-- ハンバーガーメーニューのSVG：https://reffect.co.jp/html/tailwind-for-beginners-navigation-menu -->
              <svg
                v-show="!showMenu"
                class="w-6 h-6 fill-current"
                viewBox="0 0 24 24"
              >
                <title>メニューを開くボタン</title>
                <path
                  d="M24 6h-24v-4h24v4zm0 4h-24v4h24v-4zm0 8h-24v4h24v-4z"
                />
              </svg>
              <svg
                v-show="showMenu"
                id="gNav"
                class="w-6 h-6 fill-current"
                viewBox="0 0 24 24"
              >
                <title>メニューを閉じるボタン</title>
                <path
                  d="M24 20.188l-8.315-8.209 8.2-8.282-3.697-3.697-8.212 8.318-8.31-8.203-3.666 3.666 8.321 8.24-8.206 8.313 3.666 3.666 8.237-8.318 8.285 8.203z"
                />
              </svg>
            </button>
          </div>
        </div>
        <nav
          :class="showMenu ? 'sm:block' : 'sm:hidden'"
          class="absolute left-0 z-20 w-full bg-black md:block md:static md:bg-none"
        >
          <ul class="md:flex md:justify-end md:items-end">
            <li class="w-full md:w-auto md:ml-5">
              <nuxt-link
                to="/"
                class="inline-block w-full px-5 py-5 text-xl font-bold leading-loose text-gray-300 hover:text-white sm:hover:bg-gray-700 md:block md:py-0 md:px-0"
                :class="{ current: isCurrentPage('') }"
                :aria-current="isCurrentPage('') ? 'page' : undefined"
                >ホーム</nuxt-link
              >
            </li>
            <li class="w-full md:w-auto md:ml-5">
              <nuxt-link
                to="/shop"
                class="inline-block w-full px-5 py-5 text-xl font-bold leading-loose text-gray-300 hover:text-white sm:hover:bg-gray-700 md:block md:py-0 md:px-0"
                :class="{ current: isCurrentPage('shop') }"
                :aria-current="isCurrentPage('shop') ? 'page' : undefined"
                >店舗情報</nuxt-link
              >
            </li>
            <li class="w-full md:w-auto md:ml-5">
              <nuxt-link
                to="/menu"
                class="inline-block w-full px-5 py-5 text-xl font-bold leading-loose text-gray-300 hover:text-white sm:hover:bg-gray-700 md:block md:py-0 md:px-0"
                :class="{ current: isCurrentPage('menu') }"
                :aria-current="isCurrentPage('menu') ? 'page' : undefined"
                >メニュー</nuxt-link
              >
            </li>
            <li class="w-full md:w-auto md:ml-5">
              <nuxt-link
                to="/information"
                class="inline-block w-full px-5 py-5 text-xl font-bold leading-loose text-gray-300 hover:text-white sm:hover:bg-gray-700 md:block md:py-0 md:px-0"
                :class="{ current: isCurrentPage('information') }"
                :aria-current="
                  isCurrentPage('information') ? 'page' : undefined
                "
                >お知らせ</nuxt-link
              >
            </li>
          </ul>
        </nav>
      </div>
    </header>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, useRoute } from '@nuxtjs/composition-api'

export default defineComponent({
  name: 'Navigation',
  setup() {
    const route = useRoute()

    const isCurrentPage = (page: string) => {
      const regExp = new RegExp(`^/${page}$`)
      return route.value.path.match(regExp)
    }

    const showMenu = ref(false)

    const toggleStatus = () => {
      showMenu.value = !showMenu.value
    }

    return {
      isCurrentPage,
      showMenu,
      toggleStatus,
    }
  },
})
</script>

<style scoped>
.current {
  color: white;
  border-bottom: 2px solid white;

  /* SP */
  @media (max-width: 767px) {
    background-color: #374151;
  }
}
</style>
