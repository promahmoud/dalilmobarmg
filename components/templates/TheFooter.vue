<template>
  <footer class="z-10 relative lg:block">
    <div>

      </div>
    <div
      class="pb-8 lg:pb-0 lg:pt-4 bg-light-elevatedSurface border-t border-light-border dark:border-dark-border dark:bg-dark-elevatedSurface"
    >
      <div class="container mx-auto px-4 ">
        <div
          class="flex flex-col sm:flex-row text-center sm:text-right items-center content-center justify-between pt-10 sm:py-10"
        >
          <div class="flex-1 w-full sm:w-auto mb-8 sm:mb-0 sm:text-right" :class="{'hidden lg:block': $route.name !== 'index'}">
            <h3 class="font-bold uppercase text-light-onSurfacePrimary dark:text-dark-onSurfacePrimary text-lg pb-4" >
              {{ $t(`footer.links.community.title`) }}
            </h3>
            <ul class="text-light-onSurfaceSecondary dark:text-dark-onSurfaceSecondary">
              <li class="py-2">
                <a
                  :href="$config.slackInvitationLink"
                  target="_blank"
                  class="transition duration-200 ease no-underline inline-flex btn px-4 py-3 bg-yellow-500 rounded hover:bg-yellow-400 text-light-onSurfacePrimary"
                >
                  <IconGroup class="w-6 h-6 ml-2" />
                  {{ $t('footer.links.community.slack') }}
                </a>
              </li>

              <li class="py-2">
                <a :href="$config.GithubLink" target="_blank" class="transition duration-200 ease no-underline inline-flex btn px-4 py-3 bg-black dark:bg-white text-white dark:text-black hover:bg-gray-900 dark:hover:bg-gray-400 rounded">
                  <GithubIcon class="w-6 h-6 ml-2" />
                  {{ $t('footer.links.community.github') }}
                </a>
              </li>
            </ul>
          </div>


          <nav
            v-for="(l, title, index) in links"
            :key="title"
            class="flex-1 w-full sm:w-auto mb-8 sm:mb-0"
            :class="{
              'sm:text-center hidden lg:block': index === 0,
              'sm:text-left': index === 1
            }"
          >
            <h3
              class="font-bold uppercase text-light-onSurfacePrimary dark:text-dark-onSurfacePrimary text-lg pb-4"
            >
              {{ $t(`footer.links.${title}.title`) }}
            </h3>
            <ul
              class="text-light-onSurfaceSecondary dark:text-dark-onSurfaceSecondary"
            >
              <li v-for="(link, i) in l" :key="i" class="py-2">
                <a
                  v-if="link.href"
                  :href="!link.disabled ? link.href : '#'"
                  target="_blank"
                  rel="noopener noreferrer"
                  :class="{'disabled text-gray-700': link.disabled, 'hover:text-dalil-lightindigo': !link.disabled}"
                >
                  {{ link.key }}
                </a>
                <NuxtLink
                  v-else
                  :to="!link.disabled ? link.to : ''"
                  exact
                  :class="{'disabled text-gray-700 cursor-default': link.disabled, 'hover:text-dalil-lightindigo': !link.disabled}"
                >
                  {{ link.key }}
                </NuxtLink>
              </li>
            </ul>
          </nav>
        </div>
      </div>
      <div
        class="border-t border-light-border dark:border-dark-border leading-relaxed transition-none"
      >
        <div class="container mx-auto px-4 text-center py-6" >
          {{$t('common.footer_copyrights')}}
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import GlobeIcon from '~/assets/icons/globe.svg?inline'
import IconGroup from '~/components/icons/IconGroup'
import GithubIcon from '~/assets/icons/github-3.svg?inline'

export default {
  components: {
    IconGroup,
    GithubIcon,
    GlobeIcon
  },
  data() {
    return {
      links: {
        links: [
          {
            key: this.$t('footer.links.links.home'),
            to: this.localePath('/')
          },
          {
            key: this.$t('footer.links.links.blog'),
            to: this.localePath({name: 'blog'})
          },
          {
            key: this.$t('footer.links.links.tests'),
            to: this.localePath('/tests'),
            disabled: true,
          }
        ],
        tutorials: [
          {
            key: this.$t('footer.links.tutorials.computer_and_systems'),
            to: this.localePath('/tutorials/computer/essentials/intro')
          },
          {
            key: this.$t('footer.links.tutorials.algorithms'),
            to: this.localePath('/tutorials/algorithms/fundamentals/print')
          },
          {
            key: this.$t('footer.links.tutorials.javascript'),
            to: this.localePath('/'),
            disabled: true
          },
        ],
      }
    }
  }
}
</script>
