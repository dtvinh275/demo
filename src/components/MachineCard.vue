<template>
  <div class="content-container">
    <div class="section content-title-group">
      <h2 class="title">List of Machine cards</h2>
    </div>
    <div class="columns">
      <div class="column is-3">
        <div class="card" v-show="devices.length">
          <header class="card-header">
            <p class="card-header-title">devices</p>
          </header>
          <ul class="list is-hoverable">
            <li v-for="device in devices" :key="device.id">
              <a
                class="list-item"
                @click="selectDevice(device)"
                :class="{ 'is-active': selectedDevice === device }"
              >
                <span>{{ device.deviceName }}</span>
              </a>
            </li>
          </ul>
        </div>
        <div class="notification is-info" v-show="message">{{ message }}</div>
      </div>

      <div class="column is-4" v-if="selectedDevice">
        <div class="card">
          <header class="card-header">
            <p class="card-header-title">{{ fullName }}</p>
          </header>
          <div class="card-content">
            <div class="content">
              <div class="field">
                <label class="label" for="id">ID</label>
                <label class="input" id="id" readonly>{{
                  selectedDevice.id
                }}</label>
              </div>
              <div class="field">
                <label class="label" for="deviceName">Device name</label>
                <input
                  class="input"
                  id="deviceName"
                  v-model="selectedDevice.deviceName"
                />
              </div>
              <div class="field">
                <label class="label" for="type">Type</label>
                <input
                  class="input"
                  id="type"
                  v-model="selectedDevice.type"
                />
              </div>
              <div class="field">
                <label class="label" for="version">Version</label>
                <input
                  class="input"
                  id="version"
                  v-model="selectedDevice.version"
                />
              </div>
              <div class="field">
                <label class="label" for="macAddress">MAC address</label>
                <input
                  class="input"
                  id="macAddress"
                  v-model="selectedDevice.macAddress"
                />
              </div>
              <div class="field">
                <label class="label" for="articleNumber">Article</label>
                <input
                  class="input"
                  id="articleNumber"
                  v-model="selectedDevice.articleNumber"
                />
              </div>
            </div>
          </div>
          <footer class="card-footer">
            <button
              class="link card-footer-item cancel-button"
              @click="cancelDevice()"
            >
              <i class="fas fa-undo"></i>
              <span>Cancel</span>
            </button>
            <button class="link card-footer-item" @click="saveDevice()">
              <i class="fas fa-save"></i>
              <span>Save</span>
            </button>
          </footer>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
const ourDevices = [
  {
    id: 1,
    deviceName: 'PLC_A1',
    type: '1214C DC/DC/DC',
    version: 2.0,
    macAddress: '00-1C-06-06-92-D3',
    articleNumber: '214-1AE30-0XB0',
  },
  {
    id: 2,
    deviceName: 'PLC_A2',
    type: '1214C DC/DC/DC',
    version: 2.0,
    macAddress: '00-1C-06-06-92-D5',
    articleNumber: '214-1AE30-0XB0',
  },
  {
    id: 3,
    deviceName: 'PLC_A3',
    type: '1214C DC/DC/DC',
    version: 2.0,
    macAddress: '00-1C-06-06-92-91',
    articleNumber: '214-1AE30-0XB0',
  },
  {
    id: 4,
    deviceName: 'PLC_A4',
    type: '1214C DC/DC/DC',
    version: 2.0,
    macAddress: '00-1C-06-06-92-A5',
    articleNumber: '214-1AE30-0XB0',
  },
];
export default {
  name: 'MachineCard',
  data() {
    return {
      devices: [],
      selectedDevice: undefined,
    };
  },
  computed: {
    fullName() {
      return `${this.selectedDevice.deviceName}`;
    },
  },
  created() {
    this.loadDevices();
  },
  methods: {
    async getDevices() {
      return new Promise(resolve => {
        setTimeout(() => resolve(ourDevices), 1500);
      });
    },
    async loadDevices() {
      this.devices = [];
      this.message = 'Loading';
      this.devices = await this.getDevices();
      this.message = '';
    },
    cancelDevice() {
      this.selectedDevice = undefined;
      this.message = '';
    },
    saveDevice() {
      // This only updates when you click the save button
      this.message = JSON.stringify(this.selectedDevice, null, '\n ');
    },
    selectDevice(device) {
      this.selectedDevice = device;
    },
  },
};
</script>
