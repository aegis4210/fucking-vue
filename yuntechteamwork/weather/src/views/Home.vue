<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    
    <h1>asd</h1>
    <p>{{respons}}</p>
    <input type="text" v-model="location" placeholder="請輸入地點">
    <button @click="local">確認</button>
{{location}}
{{respons}}
ˊ
  </div>
</template>

<script>
//https://medium.com/vuejs-%E5%AF%A6%E6%88%B0/vuejs-ajax%E7%AF%87-axios-%E4%B8%80-672c90a32c3f
//https://hackmd.io/@YunNet21st/r13B0t9wL?fbclid=IwAR1aN8QWvns3nkhjjvbHAdpx1yDUHYNADhWFpXeOifajzMGr3bS9_U1M4qg#/
// @ is an alias to /src


export default { 
  name: "Home",
  data() {
    return {
      respons: "",
      message: "",
      location: "",
    };
  },
  methods: {
    getMessage() {
      return "Hi I am a sync message";
    },
    asyncMessage() {
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve("I am an async message");
        }, 1000);
      }).then((res) => {
        this.message = res;
      });
    },
    local() {
      let api =
        "https://api.mapbox.com/geocoding/v5/mapbox.places/"+"res"+".json?access_token=pk.eyJ1Ijoic3RldmUxOTk5IiwiYSI6ImNrOHAxMGFyNzFiaG4zbGwzNjM5dzVmM3UifQ.Y1r0Pt22JU9aMno4_mcSAA";
      return this.axios.get(api)
      .then((res) => {
        let place = res.data.features[0].place_name;
        let coordinate = `${res.data.features[0].center[1]}, ${res.data.features[0].center[0]}`;
        this.location = `${place} at ${coordinate}`;
      })
      .catch(()=>{alert("error")});
    }
  }
};
</script>
 //HelloWorld
 //import HelloWorld from "@/components/HelloWorld.vue";
