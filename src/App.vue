<script setup lang="ts">

</script>

<template>
  <section class="blue-bg">
    <h1>IP Address Tracker</h1>
    <!-- form -->
    <form>
      <label for="ip-address" class="visually-hidden">
        Search for IP Address
      </label>
      <input type="text" placeholder="Search for any IP address or domain" name="ip-address">
      <button type="submit">
        <img src="/images/icon-arrow.svg" alt="">
      </button>
    </form>

    <!-- location details display -->
    <div class="location">
      <div class="location-item">
        <p class="location-item__title">
          IP address
        </p>
        <p>192.212.174.101</p>
      </div>
      <div class="location-item">
        <p class="location-item__title">
          location
        </p>
        <p>
          Brooklyn, NY
          10001
        </p>
      </div>
      <div class="location-item">
        <p class="location-item__title">
          Timezone
        </p>
        <p>UTC -05:00</p>
      </div>
      <div class="location-item">
        <p class="location-item__title">
          ISP
        </p>
        <p>SpaceX Starlink</p>
      </div>
    </div>
  </section>
  <section>
    <!-- MAP goes here -->
    map goes here
  </section>
</template>

<style>
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0 0 0 0);
  white-space: nowrap;
  border: 0;
}
form {
  border: 1px solid red;
}
</style>
