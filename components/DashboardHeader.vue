<template>
  <div class="flex justify-between items-center mb-6">
    <div class="w-3/4 mr-6">
      <h2 class="text-4xl text-gray-900 mb-2 font-medium">Dashboard</h2>
      <ul class="flex mt-2">
        <li class="mr-6">
          <nuxt-link class="text-gray-800 font-bold" to="/dashboard">
            Your Projects
          </nuxt-link>
        </li>
        <li class="mr-6">
          <nuxt-link
            class="text-gray-800 font-bold"
            to="/dashboard/transactions"
          >
            Your Transactions
          </nuxt-link>
        </li>
      </ul>
    </div>
    <div class="w-1/4 text-right">
      <nuxt-link
        to="/dashboard/projects/create"
        class="
          bg-orange-button
          hover:bg-green-button
          text-white
          font-bold
          py-4
          px-4
          rounded
          inline-flex
          items-center
        "
      >
        + Create Campaign
      </nuxt-link>
    </div>
  </div>
</template>

<style>
a.nuxt-link-active {
  font-weight: bold;
}
/* exact link will show the primary color for only the exact matching link */
a.nuxt-link-exact-active {
  color: #00c58e;
}
</style>
