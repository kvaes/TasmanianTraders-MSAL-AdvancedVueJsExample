<template>
  <AppHeaderDropdown right no-caret>
    <!-- Anonymous -->
    <template slot="header" v-if="!user" >
      <strong>Anonymous</strong>
    </template>
    <template slot="dropdown" v-if="!user">
      <b-dropdown-item @click="login"><i class="fa fa-lock" />Login</b-dropdown-item>
    </template>
    <!-- Authenticated -->
    <template slot="header" v-if="user">
      <strong>{{ user.name }}</strong>
    </template>
    <template slot="dropdown" v-if="user">
      <b-dropdown-header tag="div" class="text-center"><strong>Account</strong></b-dropdown-header>
      <b-dropdown-item><i class="fa fa-bell-o" /> Updates
        <b-badge variant="info">{{ itemsCount }}</b-badge>
      </b-dropdown-item>
      <b-dropdown-item><i class="fa fa-envelope-o" /> Messages
        <b-badge variant="success">{{ itemsCount }}</b-badge>
      </b-dropdown-item>
      <b-dropdown-item><i class="fa fa-tasks" /> Tasks
        <b-badge variant="danger">{{ itemsCount }}</b-badge>
      </b-dropdown-item>
      <b-dropdown-item><i class="fa fa-comments" /> Comments
        <b-badge variant="warning">{{ itemsCount }}</b-badge>
      </b-dropdown-item>
      <b-dropdown-header
        tag="div"
        class="text-center">
        <strong>Settings</strong>
      </b-dropdown-header>
      <b-dropdown-item><i class="fa fa-user" /> Profile</b-dropdown-item>
      <b-dropdown-item><i class="fa fa-wrench" /> Settings</b-dropdown-item>
      <b-dropdown-item><i class="fa fa-usd" /> Payments
        <b-badge variant="secondary">{{ itemsCount }}</b-badge>
      </b-dropdown-item>
      <b-dropdown-item><i class="fa fa-file" /> Projects
        <b-badge variant="primary">{{ itemsCount }}</b-badge>
      </b-dropdown-item>
      <b-dropdown-divider />
      <b-dropdown-item><i class="fa fa-shield" /> Lock Account</b-dropdown-item>
      <b-dropdown-item @click="logout"><i class="fa fa-lock" /> Logout</b-dropdown-item>
    </template>
  </AppHeaderDropdown>
</template>

<script>
import { HeaderDropdown as AppHeaderDropdown } from '@coreui/vue'
export default {
  name: 'DefaultHeaderDropdownAccnt',
  components: {
    AppHeaderDropdown
  },
  data: () => {
    return { 
      itemsCount: 42,
      user: null
    }
  },
  mounted() {
    this.setUser()
  },
  methods: {
    logout() {
      this.user = null
      this.$AuthService.logout()
    },
    login() {
      // this.$AuthService.loginPopup() //with a popup
      this.$AuthService.loginRedirect() //with a redirect
    },
    setUser() {
      this.user = this.$AuthService.getUser()
    }
  }
}
</script>
