<template>
  <div class="grid grid-cols-2 gap-4 border-blue-300">
    <div class="ml-10 mr-0">
      <h1 class="font-black mb-2">Manufacturer</h1>
      <ul
        v-for="m in manufacturer"
        :key="m.id"
        class="border-2 border-blue-300"
      >
        <li>
          <button @click="changeManufacturerId(m.id)">
            <img :src="m.Logo" width="100" />
          </button>
        </li>
      </ul>
    </div>
    <div>
      <slot :factId="currentMenufactID"></slot>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Manufacturer',
  components: {},
  data() {
    return {
      currentMenufactID: 0,
      manufacturer: [
        { id: 1, Title: 'Asus' },
        { id: 2, Title: 'Dell' },
      ],
    };
  },
  created() {
    this.getManufacturer();
  },
  methods: {
    getManufacturer() {
      axios.get('https://demo.yume-dev.me/manufacturers').then((res) => {
        // console.log(res);
        this.manufacturer = res.data;
      });
    },
    changeManufacturerId(id) {
      console.log('changeManufacturerId :::', id);
      this.currentMenufactID = id;
    },
  },
};
</script>
