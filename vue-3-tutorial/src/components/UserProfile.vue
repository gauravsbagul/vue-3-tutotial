<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.userName }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile__follower-count">
        <strong>followers: </strong> {{ followers }}
      </div>
      <form
        class="user-profile__create-tweet"
        @submit.prevent="createNewTween"
      >
        <label for="newTweet">New Tweet</label>
        <textarea id="newTweet" rows="4" v-model="newTweetContent" />
        <div class="user-profile__create-tweet-type">
          <label for="newTweetType"> </label>
          <strong>Tpye:</strong>
          <select id="newTwetype" v-model="selectedTweetType">
            <option
              class="user-profile__option"
              :value="option.value"
              v-for="(option, index) in tweetTypes"
              :key="index"
            >
              {{ option.name }}
            </option>
          </select>
        </div>
        <button :disabled="this.selectedTweetType == 'draft'" >Tweet</button>
      </form>
    </div>
    <div class="user-profile__tweets-wrapper">
      <div
        v-for="(tweet, index) in user.tweets"
        :key="tweet.id"
        @click="toggleFavoouriteTweet(tweet.id, index)"
      >
        <div class="tweet-item">
          <div class="user-profile__tweet">
            <div class="tweet-item__user">@{{ user.userName }}</div>
            <div class="tweet-item__content">
              {{ tweet.content }}
            </div>
            <div class="tweet-favourite" v-if="tweet.isFavourite" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import TweetItem from "./TweetItem";

export default {
  name: "UserProfile",
  data() {
    return {
      newTweetContent: "",
      selectedTweetType: "instant",
      tweetTypes: [
        {
          value: "draft",
          name: "Draft",
        },
        {
          value: "instant",
          name: "Instant",
        },
      ],
      followers: 0,
      user: {
        id: 1,
        userName: "gauravsbagul",
        firstName: "gaurav",
        lastName: "bagul",
        emial: "g@gmail.com",
        isAdmin: true,
        tweets: [
          {
            id: 1,
            content: "first tweet",
            isFavourite: false,
          },
          {
            id: 2,
            content: "second tweet",
            isFavourite: false,
          },
        ],
      },
    };
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  watch: {
    followers(newFollowerCount, oldFollowerCOunt) {
      if (oldFollowerCOunt < newFollowerCount) {
        // console.log(`Log: ~> ${this.user.userName} has gained the follower`);
      }
    },
  },
  methods: {
    toggleFavoouriteTweet(id, index) {
      this.user.tweets[index].isFavourite = !this.user.tweets[index]
        .isFavourite;
    },
    createNewTween() {
      if (this.newTweetContent && this.selectedTweetType != "draft") {
        this.user.tweets.unshift({
          id: this.user.tweets.length + 1,
          content: this.newTweetContent,
          isFavourite: false,
        });
        this.newTweetContent =""
      }
    },
  },
  mounted() {},
};
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  widows: 100%;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}

.user-profile__admin-badge {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
  margin-bottom: 10px;
}

h1 {
  margin: 0;
}

.tweet-item {
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  box-sizing: border-box;
  cursor: pointer;
  transition: all 0.25s ease;
  margin: 10px;
}

.tweet-item:hover {
  transform: scale(1.1, 1.1);
}

.tweet-item__user {
  font-weight: bold;
}

.tweet-favourite {
  background-color: gold;
  height: 10pt;
  width: 10pt;
  border-radius: 5pt;
}

.user-profile__create-tweet {
  display: flex;
  flex-direction: column;
  border-top: 1px solid #dfe3e8;
  padding-top: 20px;
}
</style>
