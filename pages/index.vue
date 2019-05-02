<template>
  <section class="container">
    <div class="input-box">
      <input v-model="message" class="text-box" name="message" type="text"/>
      <input class="submit-button" type="submit" @click="sendMessage"/>
    </div>
    <div class="message-box">
      <div v-for="(post, key) in posts" :key="key" class="message">
        <p>{{post.message}}</p>
      </div>
    </div>
  </section>
</template>

<script>
import firebase from 'firebase/app'
import 'firebase/firestore'

var config = {
    apiKey: "AIzaSyDJ5SRYLdQ4f_LrMepaYD5Okr7f37YIz40",
    authDomain: "test-blog-6f23b.firebaseapp.com",
    databaseURL: "https://test-blog-6f23b.firebaseio.com",
    projectId: "test-blog-6f23b",
    storageBucket: "test-blog-6f23b.appspot.com",
    messagingSenderId: "1009099037896"
  };

if (!firebase.apps.length) {
  firebase.initializeApp(config);
}

const db = firebase.firestore()


export default {
  data() {
    return {
      message: "",
      posts: [],
    }
  },
  created() {
    const latest_post = this.posts[0]
    let posts = this.posts
    db.collection('posts').orderBy('created_at').onSnapshot(function(querySnapshot) {
      querySnapshot.forEach(function(doc) {
        if (!latest_post) {
          posts.unshift(doc.data())
        }
        else if (doc.data().created_at > latest_post.created_at) {
          posts.unshift(doc.data())
        }
      })
    })
  },
  methods: {
    sendMessage() {
      const post = {
        message: this.message,
        created_at: Date.now(),
      }
      console.log(post)
      const postRef = db.collection('posts')
      postRef.add(post)
      this.message = ""
    },
  }
}

</script>

<style>
.container {
  min-height: 100vh;
  text-align: center;
}

.input-box {
  display: inline-block;
  margin: 50px auto 0;
}

.text-box {
  width: 300px;
  height: 40px;
  border: 1px solid gray;
  padding: 10px 10px;
}

.submit-button {
  background-color: #22aaaa;
  width: 60px;
  height: 40px;
  border: 1px solid #22aaaa;
}

.message-box {
  width: 600px;
  min-height: 100px;
  margin: 20px auto;
}
.message {
  width: 400px;
  border: 1px solid gray;
  margin: 10px auto;
  padding: 20px 40px;
  text-align: left;
}
</style>

