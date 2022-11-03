<template>
  <div class="project-page">
    <section class="dashboard-header pt-5">
      <div class="container mx-auto relative">
        <Navbar />
      </div>
    </section>
    <section class="container mx-auto pt-8">
      <DashboardHeader></DashboardHeader>
      <hr />
      <div class="block mb-2">
        <div class="w-full lg:max-w-full lg:flex mb-4" v-for="campaign in campaigns.data.data" :key="campaign">
          <div
            class="
              h-48
              lg:h-auto lg:w-48
              flex-none
              bg-cover
              rounded-t
              lg:rounded-t-none lg:rounded-l
              text-center
              overflow-hidden"
            :style="'background-color: #bbb; background-position; center; background-image:url(\'' + $axios.defaults.baseURL + '/' + campaign.image_url + '\')'"
          ></div>
          <nuxt-link
            :to="'/dashboard/projects/' + campaign.id"
            class="w-full border-r border-b border-l border-gray-400 lg:border-l-0 lg:border-t lg:border-gray-400 bg-white rounded-b lg:rounded-b-none lg:rounded-r p-8 flex flex-col justify-between leading-normal"
          >
            <div class="mb-8">
              <div class="text-gray-900 font-bold text-xl mb-1">
                {{ campaign.name }}
              </div>
              <p class="text-sm text-gray-600 flex items-center mb-2">
                Rp. {{ campaign.goal_amount.toLocaleString('id-ID') }} &middot; {{ (campaign.current_amount / campaign.goal_amount) * 100 }}%
              </p>
              <p class="text-gray-700 text-base">
                {{ campaign.short_description }}
              </p>
            </div>
            <div class="flex items-center">
              <button
                class="bg-green-button text-white py-2 px-4 rounded"
              >
                Detail
              </button>
            </div>
          </nuxt-link>
        </div>
      </div>
    </section>
    <div class="cta-clip -mt-20"></div>
    <section class="call-to-action bg-purple-progress pt-64 pb-10"></section>
    <Footer></Footer>
  </div>
</template>

<script>
export default {
  middleware: 'auth',
  async asyncData({$axios, app}){
    // console.log(app.$auth.state.user.data.id)
    const campaigns = await $axios.get('/api/v1/campaigns?user_id=' + app.$auth.state.user.data.id)
    return {campaigns}
  }
}
</script>
