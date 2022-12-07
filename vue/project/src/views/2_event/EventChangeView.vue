<template>
  <div>
    <select name="" id="" @change="changeCity($event)" v-model="selectedCity">
      <option value="">==도시선택==</option>
      <option :value="city.code" :key="city.code" v-for="city in cityList">
        {{ city.title }}
      </option>
    </select>
    <select name="" id="">
      <option
        :value="dong.dongCode"
        :key="dong.dongCode"
        v-for="dong in selectedDongList"
      >
        {{ dong.dongTitle }}
      </option>
    </select>
    <!-- <select name="" id="">
      <option
        :value="dong.dongCode"
        :key="dong.dongCode"
        v-for="dong in this.dongList.filter(
          (dong) => dong.cityCode === this.selectedCity
        )"
      >
        {{ dong.dongTitle }}
      </option>
    </select> -->
  </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      selectedCity: '',
      cityList: [
        { code: '02', title: '서울' },
        { code: '051', title: '부산' },
        { code: '054', title: '제주' }
      ],
      dongList: [
        {
          cityCode: '02',
          dongCode: '1',
          dongTitle: '서울 1동'
        },
        {
          cityCode: '02',
          dongCode: '2',
          dongTitle: '서울 2동'
        },
        {
          cityCode: '02',
          dongCode: '3',
          dongTitle: '서울 3동'
        },
        {
          cityCode: '02',
          dongCode: '4',
          dongTitle: '서울 4동'
        },
        {
          cityCode: '051',
          dongCode: '1',
          dongTitle: '부산 1동'
        },
        {
          cityCode: '051',
          dongCode: '2',
          dongTitle: '부산 2동'
        },
        {
          cityCode: '051',
          dongCode: '3',
          dongTitle: '부산 3동'
        },
        {
          cityCode: '054',
          dongCode: '1',
          dongTitle: '제주 1동'
        },
        {
          cityCode: '054',
          dongCode: '2',
          dongTitle: '제주 2동'
        }
      ],
      selectedDongList: []
    }
  },
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {
    changeCity(event) {
      console.log(event.target.tagName) // event 받아오기
      this.selectedDongList = this.dongList.filter(
        (dong) => dong.cityCode === this.selectedCity
      )
    }
  }
}
</script>
