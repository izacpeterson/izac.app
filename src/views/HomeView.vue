<script setup></script>

<template>
  <main class="bg-zinc-900 text-white h-screen flex flex-col items-center overflow-hidden">
    <section>
      <h1 class="text-[180px] font-thin text-primary">I Z A C</h1>
    </section>
    <section>
      <form action="https://google.com/search" class="w-1/4 flex justify-center items-center">
        <span class="p-2 border-l-2 border-y-2 border-primary rounded-l">Google:
        </span>
        <input type="text" name="q"
          class="grow my-2 p-2 bg-zinc-900 border-y-2 border-solid border-primary outline-none" />
        <button type="submit"
          class="my-2 p-2 border-y-2 border-r-2 border-solid border-primary bg-primary hover:bg-none rounded-r">
          Search
        </button>
      </form>
    </section>

    <section>
      <div class="flex w-1/3 justify-evenly items-center">
        <div>
          <img :src="weather.image" alt="">
          <span class="capitalize">{{ weather.condition }}</span>
        </div>
        <div class="flex flex-col">
          <span>Temperature: {{ weather.temp }}&deg;</span>
          <span>Humidity: {{ weather.humi }}%</span>
          <span>Clouds: {{ weather.clouds }}%</span>
        </div>
      </div>
    </section>
    <section>
      <ul class="p-10 flex w-full justify-evenly text-primary underline">
        <li v-for="link in links">
          <a :href="link.url">{{ link.name }}</a>
        </li>
      </ul>
    </section>
  </main>
</template>
<script>
export default {
  data() {
    return {
      links: [
        {
          name: "Gmail",
          url: "https://mail.google.com/mail/u/0/#inbox",
        },
        {
          name: "Github",
          url: "https://github.com/",
        },
        {
          name: "Youtube",
          url: "https://www.youtube.com/",
        },
        {
          name: "Blade HQ",
          url: "https://www.bladehq.com/",
        },
      ],
      weather: {
        temp: 10,
        humi: 0,
        clouds: 0,
      },
    };
  },
  mounted() {
    // this.getWweather();
    // this.tester();
    this.getweather();
  },
  methods: {
    getweather() {
      navigator.geolocation.getCurrentPosition((position) => {
        console.log(position);
        fetch(`https://weather.izacpeterson.com/api/current?lat=${position.coords.latitude}&lon=${position.coords.longitude}`)
          .then((raw) => raw.json().then((data) => {
            console.log(data);
            this.weather.temp = data.temp;
            this.weather.humi = data.humidity;
            this.weather.clouds = data.clouds;
            this.weather.image = `http://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`;
            this.weather.condition = data.weather[0].description;
          }))
      });
    }
  },

};
</script>
<style>
section{
  width: 100%;
  display: flex;
  justify-content: center;
  padding: 60px;
}
</style>