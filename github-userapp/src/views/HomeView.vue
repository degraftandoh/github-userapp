
<script setup>
import { ref } from 'vue';
import axios from 'axios';



const userinfo = ref(null);
const username = ref('');
const mistakeessage = ref('');

async function getuserinfo() {
  try {
    
    const answer = await axios.get(`https://api.github.com/users/${username.value}`);
    userinfo.value = answer.info;
    console.log(answer);
    
  } catch (mistake) {
    console.mistake(mistake);
    mistakeessage.value = 'No results'; 
    userinfo.value = null;
  }
}

function formatDate(dateString) {
  const options = { day: 'numeric', month: 'short', year: 'numeric' };
  return new Date(dateString).toLocaleDateString('en-US', options);
}
</script>

<template>
  <main>
    
    <div class="body">
    <div>
    <img class="logo" src="../assets/devfinder.svg">
    <div class="content">
    
    <div class="search">
      <div class="search_text">
      <img src="../assets/Shape 2.svg">
      <input type="text" placeholder="Search GitHub Username_" v-model="username">
      </div>
      <div class="mistake">
      <p>{{ mistakeessage }}</p>
      <button @click="getuserinfo">Search</button>
      </div>
    </div>
    
    <section v-if="userinfo">
      <img :src="userinfo.avatar_url" alt="User Avatar" class="desktop_image">
    <div class="profile">
      <div class="top_profile">
        <img :src="userinfo.avatar_url" alt="User Avatar" class="mobile_image">
        <div class="top_profile_text">
          <div>
            <h2>{{ userinfo.name }}</h2>
            <h3>{{ userinfo.login }}</h3>
          </div>
          <div>
            <p>Joined {{ formatDate(userinfo.created_at) }}</p>
          </div>
          
          
        </div>
        <div>

        </div>
        
      </div>
      <div class="background">
        <p v-if="userinfo.background">{{ userinfo.background }}</p>
        <p v-else>This profile has no background</p>
      </div>
      <div class="middle_profile">
        <div class="repos">
          <p>Repos</p>
          <h3>{{ userinfo.public_repos }}</h3>
        </div>
        <div class="followers">
          <p>Followers</p>
          <h3>{{ userinfo.followers }}</h3>
        </div>
        <div class="following">
          <p>Following</p>
          <h3>{{ userinfo.following }}</h3>
        </div>
      </div>

      <div class="bottom_profile">
        <div class="upper_links">
          <div class="location">
          <img src="../assets/003-pin.png">
          <p v-if="userinfo.location">{{ userinfo.location }}</p>
          <p v-else class="unavailable">Not available</p>
        </div>
        <div class="link">
          <img src="../assets/002-url.png">
          <p>{{ userinfo.blog }}</p>
          <p v-if="userinfo.blog">{{ userinfo.blog }}</p>
          <p v-else class="unavailable">Not available</p>
        </div>
        </div>
        
        <div class="bottom_links">
          <div class="twitter">
          <img src="../assets/004-twitter.png">
          <p>{{ userinfo.twitter_username }}</p>
          <p v-if="userinfo.twitter_username">{{ userinfo.twitter_username }}</p>
          <p v-else class="unavailable">Not available</p>
        </div>
        <div class="github">
          <img src="../assets/001-office-building.png">
          <p v-if="userinfo.company">{{ userinfo.company }}</p>
          <p v-else class="unavailable">Not available</p>
        </div>
        </div>
      </div>
    </div> 
    </section> 
    </div>
    </div>
    </div>
  </main>
</template>

<style scoped>
main{
  background: #141D2F;
}
.desktop_image{
  display: none;
}
.body{
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  
  padding-top: 31px;
  padding-left: 24px;
  padding-right: 24px;
  padding-bottom: 80px;
}
.search{
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-radius: 15px;
  background: #1E2A47;
  
  padding: 7px;
}
.search_text{
  display: flex;
  align-items: center;
  gap: 7px;
}
button{
  color: #FFF;
  font-family: 'Space Mono';
  font-size: 14px;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
  padding: 12.5px 16px;
  border-radius: 10px;
  background: #0079FF;
  border: none;
}
input{
  color: #FFF;
  font-family: 'Space Mono';
  font-size: 13px;
  font-style: normal;
  font-weight: 400;
  line-height: 25px;
  background-color: #1E2A47;
  border: none;
  width: 100%;
}
.logo{
  padding-bottom: 35px;
}
.mistake{
  display: flex;
  align-items: center;
  gap: 20px;
  color: #F74646;
  font-family: 'Space Mono';
  font-size: 14px;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
}
.content{
  display: flex;
  flex-direction: column;
  gap: 16px;
}
section{
  display: flex;
  background-color: #1E2A47;
  padding: 32px 24px;
  border-radius: 15px;
  flex-direction: column;
}
.profile{
  
  display: flex;
  flex-direction: column;
  gap: 23px;
  
}
.top_profile{
  display: flex;
  gap: 20px;
}
.top_profile_image{
  border-radius: 70px;
  width: 70px;
  height: 70px;
}
.top_profile_text h2{
  color: #FFF;
  font-family: 'Space Mono';
  font-size: 16px;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
}
.top_profile_text p{
  color: #FFF;
  font-family: 'Space Mono';
  font-size: 13px;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
}
.top_profile_text h3{
  color: #0079FF;
  font-family: 'Space Mono';
  font-size: 13px;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
  padding: 6px 0px;
}
.background{
  padding-top: 10px;
}
.background p{
  color: #FFF;
  font-family: 'Space Mono';
  font-size: 13px;
  font-style: normal;
  font-weight: 400;
  line-height: 25px; 
}
.middle_profile{
  border-radius: 10px;
  background: #141D2F;
  padding: 18px 15px;
  display: flex;
  justify-content: space-between;

}

.middle_profile p{
  color: #FFF;
  text-align: center;
  font-family: 'Space Mono';
  font-size: 11px;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
}
.middle_profile h3{
  color: #FFF;
  text-align: center;
  font-family: 'Space Mono';
  font-size: 16px;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
  text-transform: uppercase;
}
.repos, .followers, .following{
  display: flex;
  flex-direction: column;
  gap: 8px;
}
.bottom_profile{
  display: flex;
  flex-direction: column;
  gap: 17px;
}
.bottom_profile p {
  color: #FFF;
  font-family: Space Mono;
  font-size: 13px;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
}
.location{
  display: flex;
  gap: 25px;
}
.link{
  display: flex;
  gap: 10px;
}
.twitter{
  display: flex;
  gap: 10px;
}
.github{
  display: flex;
  gap: 20px;
}
.unavailable{
  opacity: 0.5;
}
section{
  display: flex;
}
.upper_links, .bottom_links{
  display: flex;
  flex-direction: column;
  gap: 17px;
}



@media screen and (min-width: 1000px) {
  
  .body{
    padding: 145px 200px;
  }

  section {
    gap: 37px;
    padding: 48px;
    display: flex;
    flex-direction: row;
  }

  .profile {
    flex: 1;
    padding: 32px 0;
    display: flex;
    flex-direction: column;
    gap: 23px;
    background-color: #1E2A47;
    border-radius: 15px;
  }

  .desktop_image {
    display: block;
    width: 117px;
    height: 117px;
    border-radius: 117px;
    margin-right: 32px;
  }

  .mobile_image {
    display: none;
  }
  .top_profile_text{
    display: flex;
    justify-content: space-between;
    flex: 1;
  }
  .bottom_profile{
    flex-direction: row;
    justify-content: space-between;
  }
  
  button{
    font-size: 16px;
  }
  .search_text{
    gap: 24px;
  }
  .search_text img{
    padding-left: 24px;
  }
  input{
    font-size: 18px;
    font-weight: 400;
  }
  .top_profile_text h2{
    font-size: 26px;
    font-weight: 700;
  }
  .top_profile_text h3{
    font-size: 16px;
    font-weight: 400;
  }
  .top_profile_text p{
    font-size: 15px;
    font-weight: 400;
    padding-top: 7px;
  }
  .background p{
    font-size: 15px;
  }
  .middle_profile{
    padding: 15px 32px;
  }
  .middle_profile p{
    font-size: 13px;
  }
  .middle_profile h3{
    font-size: 22px;
  }
}
.bottom_profile p{
  font-size: 15px;
}
</style>
