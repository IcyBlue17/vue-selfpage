<template>
  <div class="profile">
    <img class="avatar" :src="avatarUrl" alt="Avatar of IcyMichiko">
    <div class="name-container" v-if="isMobile">
      <h1 class="name">IcyMichiko</h1>
    </div>
    <div class="name-container" v-else>
      <h1 class="name">👋Hi,I am IcyMichiko</h1>
      <span class="subtitle">/ 只是一个普通学生</span>
    </div>
    <p class="poetry" v-if="!isMobile">{{ hitokoto }}</p>
    <div class="social-media-links">

      <a :href="socialMediaLinks.blog" target="_blank" :title="'IcyBlog'">
        <i class="mdui-icon material-icons mdui">&#xe157;</i>
      </a>

      <a :href="socialMediaLinks.github" target="_blank" :title="'Github'">
        <font-awesome-icon :icon="['fab', 'github']" />
      </a>

      <a :href="socialMediaLinks.telegram" target="_blank" :title="'Telegram'">
        <font-awesome-icon :icon="['fab', 'telegram']" />
      </a>

      <a :href="socialMediaLinks.twitter" target="_blank" :title="'Twitter'">
        <font-awesome-icon :icon="['fab', 'twitter']" />

      </a>

      <a :href="socialMediaLinks.blbl" target="_blank" :title="'Bilibili'">
        <font-awesome-icon :icon="['fab', 'bilibili']" />
      </a>

      <a :href="socialMediaLinks.wubaipx" target="_blank">
        <font-awesome-icon :icon="['fab', '500px']" />
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
      isMobile: false,
       avatarUrl: 'https://static.ick.moe/images/avatar.png',
      socialMediaLinks: {
        github: 'https://github.com/IcyBlue17',
        telegram: 'https://t.me/IcyLiqu1d',
        twitter: 'https://twitter.com/IcyLiqu1d',
        wubaipx: 'https://500px.com.cn/Icy0',
        blog: 'https://blog.icybit.cn',
       blbl: 'https://space.bilibili.com/326609625',
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
    this.isMobile = window.matchMedia('(max-width: 600px)').matches;
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

.mdui {
  font-size: 1.5em;
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
html, body {
  overflow: hidden;
}
@media (max-width: 600px) {
  html, body {
    height: 100%;
    width: 100%;
    overflow: hidden;
    margin: 0;
    padding: 0;
  }
  .profile {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    width: 100%;
    padding: 10px;
    text-align: center;
    height: 100%;
    position: relative;
    animation: flyIn 0.5s ease-out forwards;
    word-break: break-word;

  }

  .name {
    font-size: 3.3em;
  }

  .subtitle {
    font-size: 1.1em;
  }

  .poetry {
    font-size: 1.1em;
  }

  .social-media-links a {
    font-size: 2.2em;
  }

  .avatar {
    width: 110px;
    height: 110px;
  }

  .profile, .name, .subtitle, .poetry, .social-media-links a, .avatar {
    transform: scale(1.1);
  }
}
</style>