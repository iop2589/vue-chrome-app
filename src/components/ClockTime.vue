<template>
  <h2 id="clock" class="font-color todos-form">{{ clock }}</h2>
</template>

<script>
export default {
    data: function () {
        return {
            clock: ""
        }
    },
    mounted: function () {
        setInterval(this.getClock, 1000);
    },
    methods: {
        getClock: function () {
            const date = new Date();
            const hours = String(date.getHours()).padStart(2, "0");
            const minutes = String(date.getMinutes()).padStart(2, "0");
            const seconds = String(date.getSeconds()).padStart(2, "0");

            this.clock = `${hours}:${minutes}:${seconds}`;
        }
    }
}
</script>

<style>

</style>