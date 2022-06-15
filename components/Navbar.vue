<template>
  <div class="container">
    <nav class="navbar is-transparent">
      <div class="navbar-brand">
        <div class="navbar-burger" data-target="navbarExampleTransparentExample">
          <span />
          <span />
          <span />
        </div>
      </div>

      <div id="navbarExampleTransparentExample" class="navbar-menu">
        <div class="navbar-start">
          <NuxtLink to="/" class="navbar-item">
            Home
          </NuxtLink>
        </div>
        <div class="navbar-end">
          <NuxtLink to="/conversation-balance" class="navbar-item">
            Conversation Balance
          </NuxtLink>
          <NuxtLink to="/time-management" class="navbar-item">
            Time Management
          </NuxtLink>
        </div>
      </div>
    </nav>
  </div>
  </nav>
</template>
