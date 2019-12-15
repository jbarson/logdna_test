<template>
  <div id="app">
    <aside class="aside">
      <div class="logo">
        <img src="@/assets/ld-logo-square-64.png" alt="LogDNA logo" />
      </div>
      <div  v-for="option in menuOptions" :key="option.id">
        <div @click="activeOption = option.id">
          <transition name="fade">
            <span v-if="activeOption === option.id" class="active-indicator" />
          </transition>
          <div class="pretend-icon"></div>
          <p class="center">{{option.name}}</p>
        </div>
      </div>
    </aside>

    <div class="content">
      <header>
        <h1>What is Lorem Ipsum?</h1>
      </header>
      <div class="main-content">
        <div class="posts-list">
          <div class="post" v-for="post in posts" :key="post.id">
            <h2>{{post.title}}</h2>
            <p>{{post.content | capText}}</p>
          </div>
        </div>
        <div class="inner-content">
          <div class="main">
            <h2>Aenean cursus efficitur tellus sedluctus.</h2>
            <h3>Proin sed justo a ligula lobortis suscipit ut vel urna.</h3>
            <p>Ipsum nunc aliquet bibendum enim facilisis gravida neque convallis a. Condimentum lacinia quis vel eros. Faucibus purus in massa tempor nec. Posuere lorem ipsum dolor sit amet. Aliquam faucibus purus in massa tempor nec feugiat. Pretium lectus quam id leo in. Ultrices gravida dictum fusce ut placerat orci nulla pellentesque. Vitae turpis massa sed elementum tempus egestas sed sed. Pellentesque sit amet porttitor eget dolor morbi non arcu. Faucibus in ornare quam viverra orci sagittis. Enim tortor at auctor urna. At elementum eu facilisis sed odio morbi quis. Eget sit amet tellus cras adipiscing enim. Et tortor at risus viverra adipiscing at in. Vel orci porta non pulvinar neque. Et ultrices neque ornare aenean euismod elementum nisi quis eleifend.</p>
            <figure>
              <img src="https://placekitten.com/400/250"
                  alt="Placekitten for the win!">
              <figcaption>Aenean cursus efficitur tellus sedluctus.</figcaption>
            </figure>
          </div>
          <div class="text-input">
            <input type="text" v-model="messageText" placeholder="Message..." />
            <button @click="postMessage(messageText)">Submit</button>
            <transition name="fade">
              <div class="error-text" v-if="errorText">{{errorText}}</div>
            </transition>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'app',
  components: {
  },
  data () {
    return {
      menuOptions: [
        { name: '⌘1', id: 1 },
        { name: '⌘2', id: 2 },
        { name: '⌘3', id: 3 }
      ],
      activeOption: 1,
      posts: [
        { id: 1, title: 'Lorem Ipsum', content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.' },
        { id: 2, title: 'Lorem Ipsum', content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.' },
        { id: 3, title: 'Lorem Ipsum', content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.' },
        { id: 4, title: 'Lorem Ipsum', content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.' },
        { id: 5, title: 'Lorem Ipsum', content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.' },
        { id: 6, title: 'Lorem Ipsum', content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.' },
        { id: 7, title: 'Lorem Ipsum', content: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.' }

      ],
      messageText: '',
      errorText: ''
    }
  },
  filters: {
    capText (value) {
      if (!value) return ''
      value = value.toString()
      return `${value.slice(75)}...`
    }
  },
  methods: {
    postMessage (message) {
      console.log(message)
      axios.post('http://localhost:3000/messages', { text: message, id: Date.now() }, {
        headers: {
          'Content-Type': 'application/json'
        }
      })
        .then(response => {
          console.log(response)
        })
        .catch(error => {
          this.errorText = error
          setTimeout(() => {
            this.errorText = ''
          }, 3000)
        })
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat:200&display=swap');
$beige: #cecece;
$dark-beige: #bbbbbb;
$dark-gray: #444444;
body {
  padding: 0;
  margin: 0;
  background: $beige;
  color: $dark-gray
}
#app {
  font-family: "Avenir";
  display: flex;
  height: 100vh;
}
aside {
  background: #333333;
  flex: 0 0;
  color: $beige;
  font-weight: lighter;
  .logo {
    background: #ffffff;
    padding: 10px;
  }
  .pretend-icon {
    height: 48px;
    width: 48px;
    border-radius: 8px;
    background: $beige;
    margin: 10px auto;
  }
  .active-indicator {
    display: inline-block;
    position: absolute;
    background: #db0a5b;
    height: 6px;
    width: 6px;
    border-radius: 3px;
    box-shadow: 0 0 4px 4px #db0a5b;
    margin-left: -3px;
    margin-top: 18px;
  }
  p.center {
    text-align: center;
  }
}
header {
  background: $beige;
  flex: 0 0;
  display: flex;
  align-items: center;
  font-family: 'Montserrat', sans-serif;
  font-weight: 200;
  padding-left: 48px;
  min-height: 10vh;
  border-bottom: 1px solid $dark-gray;
}
.content {
  display: flex;
  flex-direction: column;
  flex: 1 0;
}
.main-content {
  display: flex;
  flex: 1 0;

  .posts-list {
    width: 30%;
    height:90vh;
    background: $dark-beige;
    overflow: scroll;
    .post {
      padding: 12px;
      font-size: 12px;
      border-bottom: 1px solid $dark-gray;
    }
  }
  .inner-content {
    display: flex;
    flex:1 0;
    flex-direction: column;
    .main{
      flex: 1;
      padding:12px 24px;
      h1 {
        font-weight: 900;
      }
      h3 {
        font-weight: 500;
      }
      figure {
        margin: auto;
        text-align: center;
        font-style: italic;
      }
    }
    .text-input{
      padding:12px;
      border-top: 1px solid $dark-gray;
      display: flex;
      margin-right: 8px;
      .error-text {
        background: $dark-beige;
        position: absolute;
        border: 1px solid red;
        color:red;
        bottom: 100px;
        padding: 10px;
      }
      input {
        flex: 1;
        border-bottom: 1px solid $dark-gray;
        border-radius: 4px;
        padding:8px;
        background: $beige;
      }
      button {
        display: inline-block;
        border: none;
        padding: 0.5rem 1rem;
        margin: 0;
        text-decoration: none;
        border: 1px solid $dark-gray;
        background: $beige;
        border-radius: 4px;
        // background: #0069ed;
        // color: #ffffff;
        // font-family: sans-serif;
        // font-size: 1rem;
        cursor: pointer;
        text-align: center;
        transition: background 250ms ease-in-out,
        transform 150ms ease;
        -webkit-appearance: none;
        -moz-appearance: none;
        }

        button:hover,
        button:focus {
            background: $dark-beige;
        }
      }
    }
  }

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
