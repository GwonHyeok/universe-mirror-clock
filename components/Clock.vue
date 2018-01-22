<template>
    <div id="clock-app">
        <div class="time"> 
          <span class="hours">{{ time | moment('HH') }}</span><span class="indicator" v-bind:class="{active: !isHideIndicator}">:</span><span class="minutes">{{ time | moment('mm') }}</span><span class="seconds">{{ time | moment('ss') }}</span>
        </div>
        <div>{{ time | moment("ddd, MMMM DD") | toUpperCase }} </div>
    </div>
</template>

<script>
export default {
  watch: {
    time: function() {
      this.blinkIndicator();
    }
  },
  data: function() {
    return {
      time: new Date(),
      isHideIndicator: false
    };
  },
  mounted: function() {
    setInterval(() => (this.time = new Date()), 1000);
  },
  methods: {
    blinkIndicator: function() {
      setTimeout(() => (this.isHideIndicator = !this.isHideIndicator), 1000);
    }
  },
  filters: {
    toUpperCase: function(value) {
      if (!value) return "";
      return value.toString().toUpperCase();
    }
  }
};
</script>
<style lang="scss" scoped>
#clock-app {
  display: inline-block;
  text-align: center;
}

.time {
  font-size: 5rem;

  .seconds {
    font-size: 1.2rem;
    display: none;
  }

  .hours {
    font-weight: bold;
  }

  .minutes {
    font-weight: 200;
  }

  .indicator {
    color: transparent;
    -moz-transition: all 0.6s ease-out;
    -o-transition: all 0.6s ease-out;
    -webkit-transition: all 0.6s ease-out;
    transition: all 0.6s ease-out;
  }

  .indicator.active {
    color: white;
  }
}
</style>