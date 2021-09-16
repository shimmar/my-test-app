<template>
  <div>
    <v-btn @click="fetchTest">Fetch</v-btn><span v-text="var1"></span
    ><span v-text="var2"></span>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

interface HomeType {
  var1: number;
  var2: string | null;
}

export default Vue.extend({
  name: "Home",
  data(): HomeType {
    return { var1: 0, var2: "" };
  },
  methods: {
    fetchSettings: async function () {
      const res = await fetch("http://127.0.0.1:5000/get_setting", {
        method: "GET",
      });
      return res.json();
    },
    fetchTest: function () {
      this.fetchSettings()
        .then((data) => {
          console.log(data);
          this.var1 = data.num;
          this.var2 = data.msg;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
});
</script>
