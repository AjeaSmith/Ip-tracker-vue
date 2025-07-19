<script setup lang="ts">
import { LMap, LMarker, LPopup, LTileLayer } from "@vue-leaflet/vue-leaflet";
import { useAsyncState } from "@vueuse/core";
import { Icon } from "leaflet";
import { ref, watch } from "vue";

const mapElement = ref("");
const center = ref<[number, number]>([40.7506, -73.9972]);
const locationIcon = new Icon({
  iconUrl: "./images/icon-location.svg",
  iconAnchor: [12, 41],
  popupAnchor: [1, -34],
  shadowSize: [41, 41],
});

const search = ref("");

const { state, isLoading, execute } = useAsyncState(() => fetch(`https://geo.ipify.org/api/v2/country,city?apiKey=${import.meta.env.VITE_API_KEY}&domain=${search.value}`).then(res => res.json()), {
  ip: "192.212.174.101",
  location: { city: "Brooklyn, NY 10001", timezone: "-05:00" },
  isp: "SpaceX Starlink",
}, { immediate: false });
async function handleSubmit() {
  if (!search.value)
    return;
  await execute();
}

watch(state, (newData) => {
  if (newData) {
    center.value = [newData?.location.lat, newData?.location.lng];
  }
});
</script>

<template>
  <section class="main-bg">
    <section class="main-content">
      <h1>IP Address Tracker</h1>
      <!-- form -->
      <form @submit.prevent="handleSubmit">
        <label for="ip-address" class="visually-hidden">
          Search for IP Address
        </label>
        <input v-model="search" type="text" placeholder="Search for any IP address or domain" name="ip-address">
        <button type="submit" aria-label="Search">
          <img src="/images/icon-arrow.svg" alt="">
        </button>
      </form>
      <div v-if="isLoading" style="margin-block: 2rem; color: white; font-weight: bold; font-size: 2rem;">
        Loading...
      </div>
      <!-- location details display -->
      <div v-else class="location">
        <div class="location-item">
          <p class="location-item__title">
            IP address
          </p>
          <p>
            {{ state?.ip }}
          </p>
        </div>
        <div class="location-item">
          <p class="location-item__title">
            location
          </p>
          <p>
            {{ state?.location?.city }}
          </p>
        </div>
        <div class="location-item">
          <p class="location-item__title">
            Timezone
          </p>
          <p>UTC {{ state?.location?.timezone }}</p>
        </div>
        <div class="location-item">
          <p class="location-item__title">
            ISP
          </p>
          <p style="padding-right: 0.7rem;">
            {{ state?.isp }}
          </p>
        </div>
      </div>
    </section>
  </section>
  <section>
    <LMap ref="mapElement" :zoom="14" :center="center" style="height: 80vh; z-index: -1" :zoom-control="false">
      <LTileLayer
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        layer-type="base"
        name="OpenStreetMap"
      />
      <LMarker :lat-lng="center" :icon="locationIcon">
        <LPopup>You are here</LPopup>
      </LMarker>
    </LMap>
  </section>
</template>

<style>
.main-bg {
  background: url("/images/pattern-bg-mobile.png") no-repeat center;
  background-size: cover;
  height: 300px;
  width: 100%;
}
.main-content {
  max-width: 69.375rem;
  padding-inline: 1.5rem;
  padding-block: 1.6rem;
  h1 {
    color: white;
    font-weight: 500;
    margin-bottom: 30px;
    text-align: center;
    font-size: 1.6rem;
  }
}
form {
  display: flex;
  justify-content: space-between;
  background-color: white;
  border-radius: 15px;
  height: 100%;
  input {
    font-size: 1.125rem;
    padding: 1rem;
    border-top-left-radius: 15px;
    border-bottom-left-radius: 15px;
    flex: 1;
    border: none;
  }
  ::placeholder {
    font-size: 1.125rem;
  }
  button {
    cursor: pointer;
    width: 50px;
    border-top-right-radius: 15px;
    border-bottom-right-radius: 15px;
    border: none;
    background-color: black;
  }
}

.location {
  position: relative;
  z-index: 100;
  display: grid;
  align-items: center;
  justify-content: center;
  gap: 1.5rem;
  text-align: center;
  margin-top: 1.5rem;
  padding-block: 1.6rem;
  background-color: white;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
  border-radius: 15px;

  .location-item__title {
    letter-spacing: 1.46px;
    text-transform: uppercase;
    font-size: 0.688rem;
    font-weight: 700;
    color: #2c2c2caa;
  }
  .location-item__title + p {
    color: #2c2c2c;
    font-size: 1.25rem;
    font-weight: 600;
    letter-spacing: 0.18px;
  }
}

.leaflet-touch .leaflet-bar a:first-child {
  display: none;
}
.leaflet-touch .leaflet-bar a:last-child {
  display: none;
}

@media (min-width: 48rem) {
  .main-bg {
    height: 280px;
    background: url("/images/pattern-bg-desktop.png") no-repeat center;
    background-size: cover;
  }
}

@media (min-width: 69.375rem) {
  .main-content {
    margin: 0 auto;
  }
  .location {
    padding-top: 2rem;
    align-items: baseline;
    height: 161px;
    margin-top: 3rem;
    grid-template-columns: repeat(4, 1fr);
    text-align: left;

    .location-item {
      padding-left: 2rem;
      border-left: 1px solid #979797;
    }
    .location-item__title {
      font-size: 0.75rem;
    }
    .location-item__title + p {
      font-size: 1.625rem;
    }
    .location-item:first-child {
      border-left: none;
    }
  }
}
</style>
