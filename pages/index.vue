<template>
  <v-container class="back"><p class="card-title">Profile Lists</p>
    <v-row>
      <template>
        <v-col v-for="item in obj" :key="item" cols="12" sm="4">
          <v-card style="min-height:400px; background-color:rgb(255, 180, 130);" class="pa-3 ma-3" :elevation="9" height="100%">
            <p class="img"><img :src=item.image width="279px" height="200px" /></p>
            <p class="data1">{{item.name}}</p>
            <p class="data"><span class="small">from</span> {{item.hometown}}</p>
            <p class="name">Introduction</p>
            <div class="outline"><text-area class="data">{{item.content}}</text-area></div>
          </v-card>
        </v-col>
      </template>  
    </v-row>
  </v-container>
</template>
<script>
export default {
  data: function() {
    return {
      obj: {},
    };
  },
  methods: {},
  computed: {},
  async mounted() {
    const res = await this.$axios.$get(`https://introinfo.s3-ap-northeast-1.amazonaws.com/data1`); //awaitで非同期でも順番に処理されるようにする
    //this.obj = res
    
    let array = []
    for (let i = 0; i < res.length; i++) {
      if (res[i]["name"] != null && res[i]["id"] != 7 && res[i]["id"] != 8 && res[i]["id"] != 9) {
        array.push(res[i]) //not array[i] = res[i] ← 空になる部分も代入している　
      } 
    }
    let arr = array[0].image.url.split("/")
    console.log(arr[arr.length-1])
    this.obj = array;
    console.log(this.obj)
    // console.log(res[i].content)
    
  },
};
</script>
<style>
.back {
  /* background-color:pink; */
  background-color:rgb(255, 180, 130);
}
.pa-3 {
  /* background:url(../assets/KTAkgZxWWvoy3Ec1606962477.jpg);  */
  /* background-color:orange; */
  background:url(../assets/BuZkp7qYqnsyzrr1606972441.jpg);
} 
.title {
  font-size:35px;
}
.card-title {
  color:rgb(253, 95, 36);
  font-size:30px;
  text-align:center;
  /* background-color:rgb(67, 68, 65); */
  background-color:rgb(255, 206, 204);
  font-weight:bold;
}
.ma-2 {
  padding:10px;
}
.name {
  color:red;
  font-weight:bold;
  margin:0;
}
.data1 {
  font-weight:bold;
  color:rgb(253, 95, 36);
  font-size:30px;
}
.data {
  color:rgb(253, 95, 36);
  font-size:20px;
}
.small {
  font-size:15px;
}
.outline {
  border:dotted;
  color:orange;
  padding:10px;
}
.img {
  text-align:center;
}
</style>