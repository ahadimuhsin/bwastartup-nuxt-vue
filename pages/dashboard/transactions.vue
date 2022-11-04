<template>
  <div class="project-page">
    <section class="dashboard-header pt-5">
      <div class="container mx-auto relative">
        <Navbar></Navbar>
      </div>
    </section>
    <section class="container mx-auto pt-8">
      <DashboardHeader></DashboardHeader>
      <hr />
      <!-- {{ transactions.data.data.length }} -->
      <div class="block mb-2" v-if="transactions.data.data.length > 0">
        <div class="w-full lg:max-w-full lg:flex mb-4"  v-for="transaction in transactions.data.data"
        :key="transaction.id">
          <div
            class="
              h-48
              lg:h-auto lg:w-48
              flex-none
              bg-cover
              rounded-t
              lg:rounded-t-none lg:rounded-l
              text-center
              overflow-hidden
            "
            :style="'background-color: #bbb; background-position; center; background-image:url(\'' + $axios.defaults.baseURL + '/' + transaction.campaign.image_url + '\')'"
          ></div>
          <div
            class="
              w-full
              border-r border-b border-l border-gray-400
              lg:border-l-0 lg:border-t lg:border-gray-400
              bg-white
              rounded-b
              lg:rounded-b-none lg:rounded-r
              p-8
              flex flex-col
              justify-between
              leading-normal
            "
          >
            <div>
              <div class="text-gray-900 font-bold text-xl mb-1">
                {{ transaction.campaign.name }}
              </div>
              <p class="text-sm text-gray-600 flex items-center mb-2">
                Rp. {{ transaction.amount.toLocaleString('id-ID') }}
                &middot; {{ dateFormat(transaction.created_at) }}
                &middot; {{ transaction.status }}
              </p>
            </div>
          </div>
        </div>
      </div>
      <div class="block mb-2" v-else>
      Transaksi Kosong
      </div>
    </section>
    <div class="cta-clip -mt-20"></div>
    <section class="call-to-action bg-purple-progress pt-64 pb-10"></section>
    <Footer></Footer>
  </div>
</template>


<script>
import moment from 'moment'
export default {
  middleware: 'auth',
  async asyncData({$axios, app}){
    // console.log(app.$auth.state.user.data.id)
    const transactions = await $axios.get('/api/v1/transactions')
    return {transactions}
  },

  methods:{
    dateFormat(value){
      if (value) {
           return moment(String(value)).format('DD MMMM Y')
          }
    }
  }
}
</script>
