<script setup lang="ts">
import { ref } from "vue"
const tweets = ref([
  { id: 0, discription: "hello" },
  { id: 1, discription: "hooooooooooo" },
])

const inputtingDescriptioon = ref<string>("")

const postTweet = () => {
  console.log(inputtingDescriptioon.value)
  if (inputtingDescriptioon.value === "") {
    return false
  }
    const tweet = {
      id: Math.random(),
      discription: inputtingDescriptioon.value,
    }
  tweets.value.push(tweet)
  inputtingDescriptioon.value = ""
}

const deleteTweet = (id: number) => {
  tweets.value = tweets.value.filter((t) => t.id !== id)
}
</script>

<template>
  <div class="container">
    <h1>Tweeter</h1>
    <div class="form-container">
      <input v-model="inputtingDescriptioon" />
      <button class="save-botton" @click="postTweet()">post</button>
    </div>
    <div class="tweet-container">
      <p v-show="tweets.length <= 0">No tweets have been added</p>
      <ul>
        <li v-for="tweet in tweets" :key="tweet.id" class="tweet-list">
          <span>{{ tweet.discription }}</span>
          <button class="delete-button" @click="deleteTweet(tweet.id)">
            削除
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: aliceblue;
  padding: 24px 0;
  width: 60%;
  margin-bottom: 12px;
  border-radius: 4px;
}

.tweet-list {
  list-style: none;
  margin-bottom: 12px;
  border-radius: 4px;
  font-size: 12px;
  display: flex;
  justify-content: space-between;
  background: #95ccf6;
  padding: 8px 20px;
  width: 300px;
}

.save-button {
  width: 60px;
  height: 22px;
  color: #fff;
  font-weight: bold;
  background: #68c9c9;
  border-radius: 2px;
  border: none;
}

.save-button:hover {
  background: #37bdbd;
}
.delete-button {
  width: 60px;
  height: 22px;
  color: #fff;
  font-weight: bold;
  background: #c99a68;
  border-radius: 2px;
  border: none;
}

.delete-button:hover {
  background: #ac783f;
}

ul {
  padding: 0;
}

input {
  margin-bottom: 16px;
}
</style>