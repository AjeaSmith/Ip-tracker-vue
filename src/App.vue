<script setup lang="ts">

</script>

<template>
  <section class="main-bg">
    <section class="main-content">
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
  </section>
  <section style="background-color: green;">
    <!-- MAP goes here -->
    map goes here
  </section>
</template>

<style>
.main-bg {
  background: url("./images/pattern-bg-mobile.png") no-repeat center;
  background-size: cover;
  height: 300px;
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

@media (min-width: 48rem) {
  .main-bg {
    height: 280px;
    background: url("./images/pattern-bg-desktop.png") no-repeat center;
  }
}

@media (min-width: 69.375rem) {
  .main-content {
    margin: 0 auto;
  }
  .location {
    margin-top: 3rem;
    padding-block: 2rem;
    grid-template-columns: repeat(4, 1fr);
    text-align: left;

    .location-item {
      word-break: break-word;
      padding-left: 2rem;
      border-left: 1px solid #979797;
    }
    .location-item:first-child {
      border-left: none;
    }
  }
}
</style>
