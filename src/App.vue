<script>
export default {
  data() {
    return {
      user: { name: null, email: null }
    };
  },
  methods: {
    //Callback
    Callback() {
      this.NameCallback((error, name) => {
        if (error) {
          console.error("Error:", error);
        } else {
          this.user.name = name;
          this.EmailCallback((error, email) => {
            if (!error) this.user.email = email;
          });
        }
      });
    },
    NameCallback(callback) {
      setTimeout(() => {
        callback(null, "Laras");
      }, 2000);
    },
    EmailCallback(callback) {
      setTimeout(() => {
        callback(null, "Laras11@Gmail.com");
      }, 200);
    },
    
    //Promise
    Promise() {
      this.getUserNamePromise()
        .then((name) => {
          this.user.name = name;
          return this.getUserEmailPromise();
        })
        .then((email) => {
          this.user.email = email;
        })
        .catch((error) => {
          console.error("Kesalahan:", error);
        });
    },
    getUserNamePromise() {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve("Laras");
        }, 200);
      });
    },
    getUserEmailPromise() {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve("Laras11@Gmail.com");
        }, 2000);
      });
    },
    
    // Async/Await
    async AsyncAwait() {
      try {
        this.user.name = await this.getUserNamePromise();
        this.user.email = await this.getUserEmailPromise();
      } catch (error) {
        console.error("Error:", error);
      }
    }
  }
};
</script>

<template>
  <div>
    <h2>ber</h2>
    <h2>JavaScript</h2>
    <h2>Asynchronous JavaScript</h2>
    <h1>PERTEMUAN 6 PBK</h1>
    <button @click="Callback">Ambil dengan Callback</button>
    <button @click="Promise">Ambil dengan Promise</button>
    <button @click="AsyncAwait">Ambil dengan Async/Await</button>
    <div v-if="user.name">
      <p><strong>Nama:</strong> {{ user.name }}</p>
    </div>
    <div v-if="user.email">
      <p><strong>Email:</strong> {{ user.email }}</p>
    </div>
  </div>
</template>

<style>

</style>

