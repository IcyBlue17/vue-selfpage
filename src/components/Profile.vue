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
      <a>     </a>
      <a :href="socialMediaLinks.telegram" target="_blank">
        <font-awesome-icon :icon="['fab', 'telegram']" />
      </a>
      <a>     </a>
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
}
</script>

<style scoped>

.profile {
  width: max-content ;
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
}

.avatar {
  width: 150px; /* Adjust the size as needed */
  height: 150px; /* Make sure this is the same as the width to maintain the circular shape */
  border-radius: 50%; /* Make the image circular */
  margin-bottom: 20px; /* Add some space below the image */
  transition: transform 0.3s ease-in-out; /* Add a transition effect for the hover effect */
}

.avatar:hover {
  transform: scale(1.1); /* Make the image 10% larger when hovered */
}

</style>
