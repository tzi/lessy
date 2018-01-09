<template>
  <header class="app-header">
    <h1 class="app-header-title">{{ title }}</h1>
    <nav v-if="$slots.default" class="app-header-nav">
      <div class="app-header-nav-container">
        <slot></slot>
      </div>
    </nav>
    <div class="app-header-user">
      <div class="app-header-user-name">{{ user.displayedName }}</div>
      <div>
        <ly-button type="ghost" @click="logout">{{ $t('app.appHeader.logout') }}</ly-button>
      </div>
    </div>
  </header>
</template>

<script>
  import { mapGetters } from 'vuex'

  export default {
    props: {
      title: { type: String, required: true },
    },

    computed: {
      ...mapGetters({
        user: 'users/current',
      }),
    },

    methods: {
      logout () {
        this.$store.dispatch('users/logout')
        this.$router.push('/')
      },
    },
  }
</script>

<style lang="scss">
  .app-header {
    display: flex;

    align-items: stretch;

    color: $ly-color-white;

    > .app-header-nav {
      flex-shrink: 1;
      flex-grow: 1;
    }
    > .app-header-user {
      flex-basis: 0;
      display: flex;
      align-items: center;
      margin-left: auto;
    }
    > .app-header-user-name {
      flex-basis: 0;
      margin-right: 0.5rem;
      color: $ly-color-grey-90;
      
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
  }

  .app-header-title,
  .app-header-nav {
    display: flex;

    flex-direction: column;
    justify-content: center;
  }

  .app-header-title {
    margin-top: 0;
    margin-bottom: 0;
    padding: 1rem 2rem;

    font-size: 1.1rem;
    font-weight: normal;
    text-transform: uppercase;
  }

  .app-header-nav-container {
    padding: .5rem 2rem;

    border-left: 1px solid $ly-color-white;
  }

  .app-header-user {
    padding: 1rem 2rem 1rem 6rem;

    background: linear-gradient(45deg, $ly-color-pine-60 3.5rem,
                                       $ly-color-grey-20 3.5rem,
                                       $ly-color-grey-20 4rem,
                                       $ly-color-pine-60 4rem,
                                       $ly-color-pine-60 4.5rem,
                                       $ly-color-grey-20 4.5rem);
  }

  @media(max-width: $small-screen-width) {
    .app-header-nav {
      white-space: nowrap;
      overflow-x: auto;
    }

    .app-header-nav-container {
      padding: .5rem 1rem 1rem;

      border-left: none;
    }

    .app-header-title,
    .app-header-user {
      display: none;
    }
  }
</style>
