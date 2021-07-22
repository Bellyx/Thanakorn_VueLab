<template>
  <h1 class="font-black mb-3">Devices</h1>
  <div class="grid grid-cols-3 gap-4 border border-black ml-0 mr-5 p-3">
    <ul v-for="device in devices" :key="device.id">
      <li>
        <router-link
          :to="{
            name: 'device',
            params: { id: device.id },
          }"
        >
          <img :src="device.Photo" />
          {{ device.DeviceName }}
        </router-link>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: {
    manufacturerId: Number,
  },
  data: () => ({
    devices: [
      { id: 1, DeviceName: "Asus ROG" },
      { id: 2, DeviceName: "Dell XP13" },
    ],
  }),
  created() {
    console.log("factId:", this.manufacturerId);
    this.getDeviceByManufacturer(this.newId);
  },
  watch: {
    manufacturerId: function (newId, oldId) {
      // watch it
      console.log("Prop changed: ", newId, " | was: ", oldId);
      this.getDeviceByManufacturer(newId);
    },
  },
  methods: {
    getDeviceByManufacturer(id) {
      axios
        .get(
          `https://service2.ahead-coop.work/devices?ManufacturerID=${this.manufacturerId}`
        )
        .then((res) => {
          this.devices = res.data;
        });
    },
  },
};
</script>