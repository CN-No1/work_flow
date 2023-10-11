<template>
  <div></div>
</template>

<script>
import { getToken } from "@/utils/auth";
export default {
  data() {
    return {
      interval: null,
    };
  },
  mounted() {
    this.$store
      .dispatch("Login", { username: this.$route.query.username })
      .then(() => {
        this.interval = setInterval(() => {
          this.redirect();
        }, 1000);
      })
      .catch(() => {});
  },
  methods: {
    redirect() {
      if (getToken()) {
        clearInterval(this.interval);
        this.$router
          .push({ path: this.$route.query.redirect || "/" })
          .catch(() => {});
      }
    },
  },
};
</script>
