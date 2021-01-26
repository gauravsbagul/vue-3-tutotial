<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@{{ user.userName }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile__follower-count">
        <strong>followers: </strong> {{ followers }}
      </div>
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
            <div class="tweet-favourite"  v-if="tweet.isFavourite"/>
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
          {
            id: 3,
            content: "third tweet",
            isFavourite: false,
          },
          {
            id: 4,
            content: "fourth tweet",
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
  },
  mounted() {
    this.followUser();
  },
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
</style>
