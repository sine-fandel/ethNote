<template>
  <div id="app">
    <div class="app-header">
      <div class="descp">
        <div class="descp-title">ethNote</div>
        <div class="descp-subtitle">- a note DAPP built on ethereum</div>
      </div>
    </div>
    <div class="app-main">
      <div class="userinfo">
        <div class="userinfo-usernum">
          <span>目前总用户数: </span>
          <span>{{userCount}}</span>
        </div>
        <div class="userinfo-current">
          <span>当前用户: </span>
          <span>{{currentUser}}</span>
        </div>
        <button class="userinfo-signinbtn" @click="signinClick">切换用户</button>
        <button class="userinfo-signupbtn" @click="signupClick">注册用户</button>
      </div>

      <div class="note">
        <div class="note-content">{{note}}</div>
        <button class="note-getbtn" @click="getNoteClick">获取Note</button>
        <button class="note-setbtn" @click="setNoteClick">修改Note</button>
      </div>
    </div>
    <div class="app-bottom"></div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'app',
  data: () => {
    return {
      userCount: 0,
      currentUser: null,
      note: ''
    }
  },
  methods: {
    signinClick: () => {
      var username = 'sefaice1'
      var _self = this
      axios
      .post('/signin', {
        username: username
      })
      .then((response) => {
        _self.note = response
        console.log(this)
        console.log(_self)
        console.log(response)
      })
      .catch((error) => {
        // this seems to be error in console
        //Uncaught (in promise) TypeError: Cannot set property 'note' of undefined
        _self.note = error
      })
    }
  }
}
</script>

<style>
:root {
  --purple: #503C58;
  --blue: #5C7EAB;
  --gray: #707070;
}

body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.app-header {
  width: 100%;
  height: 140px;
  top: 0;
  background-color: var(--gray);
  overflow: hidden;
}

.app-main {
  width: 100%;
  height: calc(100vh - 200px);
  overflow: hidden;
}

.app-bottom {
  width: 100%;
  height: 60px;
  background-color: var(--gray);
}

.descp {
  text-align: center;
  color: black;
  font-weight: bolder;
}

.descp-title {
  margin-top: 20px;
  font-size: 40px;
}

.descp-subtitle {
  margin-top: 20px;
  margin-left: 400px;
  font-size: 24px;
}

.userinfo {
  margin: auto;
  width: 300px;
  border: 1px solid black;
}

.userinfo-usernum {
  margin-top: 20px;
  margin-left: 40px;
  font-size: 24px;
}

.userinfo-current {
  margin-top: 20px;
  margin-left: 40px;
  font-size: 24px;
}

.userinfo-signinbtn {
  margin-top: 20px;
  margin-left: 60px;
  width: 80px;
  height: 30px;
}

.userinfo-signupbtn {
  margin-top: 20px;
  margin-left: 20px;
  width: 80px;
  height: 30px;
}

.note {
  width: 600px;
  margin: auto;
  margin-top: 40px;
  border: 1px solid black;
}

.note-content {
  height: 200px;
  padding: 20px;
  background-color: #f5f5f5;
  border: 1px solid var(--light-black);
  border-radius: 5px;
  font-weight: lighter;
  font-size: 14px;
  color: #3a3f44;
}

.note-getbtn {
  margin-top: 20px;
  margin-left: 210px;
  width: 80px;
  height: 30px;
}

.note-setbtn {
  margin-top: 20px;
  margin-left: 20px;
  width: 80px;
  height: 30px;
}
</style>
