<template>
  <div class="profile">
    <img class="avatar" :src="avatarUrl" alt="Avatar of IcyMichiko">
    <div class="name-container">
      <h1 class="name">{{ name }}</h1>
      <span class="subtitle">/ 只是一个普通学生</span>
    </div>
    <p class="poetry">{{ hitokoto }}</p>
    <div class="social-media-links">
      <a :href="socialMediaLinks.github" target="_blank">
        <font-awesome-icon :icon="['fab', 'github']" />
      </a>

      <a :href="socialMediaLinks.telegram" target="_blank">
        <font-awesome-icon :icon="['fab', 'telegram']" />
      </a>

      <a :href="socialMediaLinks.twitter" target="_blank">
        <font-awesome-icon :icon="['fab', 'twitter']" />
      </a>
    </div>
  </div>

</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { library } from '@fortawesome/fontawesome-svg-core'
import { fab } from '@fortawesome/free-brands-svg-icons'
import axios from 'axios';
import vuetyped from 'vue3typed';

library.add(fab)

export default {
  name: 'Profile',
  components: {
    FontAwesomeIcon
  },
  data() {
    return {
      name: '👋Hi,I am IcyMichiko',
      hitokoto: '一言获取中...',
       avatarUrl: 'https://static.ick.moe/images/avatar.png',
      socialMediaLinks: {
        github: 'https://github.com/IcyBlue17',
        telegram: 'https://t.me/IcyLiqu1d',
        twitter: 'https://twitter.com/IcyLiqu1d',
      }
    }
  },
  created() {
    axios.get('https://v1.hitokoto.cn/?c=f&encode=text')
        .then(response => {
          this.hitokoto = response.data;
        })
        .catch(error => {
          console.error(error);
        });
  },
  mounted() {
    document.querySelector('link[rel="icon"]').href = this.avatarUrl;
  }


}
</script>

<style scoped>
.profile {
  width: max-content;
  position: relative;
  animation: flyIn 0.5s ease-out forwards;
  word-break: break-word;
}

@keyframes flyIn {
  from {
    transform: translateX(-100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

.name-container {
  display: block;
}

.name {
  font-size: 4.5em;
  font-weight: bold;
  margin-bottom: 10px;
  display: inline;
}

.subtitle {
  font-size: 2em;
  color: gray;
  margin-left: 10px;
  display: inline;
}

.poetry {
  font-size: 2em;
  text-align: left;
  color: grey;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  margin-bottom: 10px;
}

.poetry:hover {
  background-color: transparent;
}

.social-media-links a {
  font-size: 3em;
  margin-bottom: 10px;
  transition: filter 0.5s ease-in-out, transform 0.3s ease-in-out;
  filter: grayscale(0%);
  margin-right: 15px

}

.social-media-links a:hover {
  filter: grayscale(100%); /* 悬停时变为灰色 */
  transform: scale(1.2);
}

.social-media-links a:active {
  transform: scale(0.9);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);}

.avatar {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  margin-bottom: 20px;
  transition: filter 0.5s ease-in-out, transform 0.3s ease-in-out;
}

.avatar:hover {
  transform: scale(1.2);
}

.avatar:active {
  transform: scale(0.9);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
}

</style>