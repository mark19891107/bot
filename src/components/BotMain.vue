<template>
  <div :class="size">
    <div class="title">
      Minibot
      <button class="minimize" @click="mini()">-</button>
      <button class="maximize" @click="max()">+</button>
    </div>
    <div class="body" ref="data">
      <div v-for="(c,i) in content" :key="i" :class="c.type">{{c.text}}</div>
    </div>
    <div class="input">
      <input type="text" placeholder="type here..." @keypress.enter="enter" v-model="textIn"/>
      <div class="send" @click="enter">send</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      content: [
        {
          type:"bot",
          text:"HI, Please type something .."
        }
      ],
      textIn:"",
      size:"big"
    };
  },
  methods: {
    mini() {
      this.size = "big mini";
    },
    max() {
      this.size = "big";
    },
    toEnd(){
      setTimeout(()=>{
        this.$refs.data.scrollTop = this.$refs.data.scrollHeight;
      },10)
    },
    async enter(){
      this.content.push({type:"user",text:this.textIn})
      this.textIn = ""
      this.toEnd()
      let res = await fetch('https://jsonplaceholder.typicode.com/todos/1').then(response => response.json())
      this.content.push({type:"bot",text:res.title})
      this.toEnd()
    }
  },
};
</script>

<style>
.send{
    background: #1b53d0;
    color: white;
    border: none;
    border-radius: 5px;
    padding: 6px;
    display: block;
    cursor: pointer;
}

.big {
  background-color: white;
  position: absolute;
  right: 5px;
  top: 5px;
  height: calc(100vh - 20px);
  width: 500px;
  box-shadow: 0px 0px 20px 6px #32323233;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  transition: all 0.5s ease;
}

.title {
  background-color: #1b53d0;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
  padding: 10px 15px;
  color: white;
  font-family: system-ui;
  font-size: larger;
  font-weight: 900;
  letter-spacing: 2px;
  transition: all 0.5s ease;
}

.body {
  flex: 1;
  background: #f4f4f4;
  border-bottom: 2px solid #d3d3d329;
  display: flex;
  flex-direction: column;
  overflow-y: scroll;
  transition: all 0.5s ease;
}

.bot {
  max-width: 70%;
  margin: 10px;
  background: white;
  padding: 10px 15px;
  border-radius: 5px;
  color: black;
  font-family: system-ui;
  text-align: left;
}

.user {
  max-width: 70%;
  margin: 10px;
  background: #1b53d0;
  padding: 10px 15px;
  border-radius: 5px;
  color: white;
  font-family: system-ui;
  text-align: left;
  margin-left: auto;
}

.input {
  padding: 10px;
  height: 30px;
  display: flex;
  justify-content: space-between;
  overflow: hidden;
  transition: all 0.5s ease;
}

.input input {
  border: none;
  flex: 1;
}

.input button {
  float: right;
}

input:focus {
  outline: none;
}

.mini .body {
  height: 0px;
}

.mini .input {
  height: 0px;
  padding: 0px;
}

.mini.big {
  height: 10px;
  width: 200px;
  top: calc(100vh - 50px);
}

.mini .minimize {
  display: none;
}

.big .maximize {
  display: none;
}

.mini.big .maximize {
  display: inline;
}
</style>