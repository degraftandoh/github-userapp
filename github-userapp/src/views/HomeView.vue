
<script setup>
import { ref } from 'vue';
import axios from 'axios';



const userdata = ref(null);
const username = ref('');
const fetchErroressage = ref('');

async function getuserdata() {
  try {
    
    const answer = await axios.get(`https://api.github.com/users/${username.value}`);
    userdata.value = answer.data;
    
  } catch (dataError) {
   
    dataErrorMessage.value = 'No results'; 
    userdata.value = null;
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
    <div class="profileSection">
    
    <div class="query">
      <div class="text_query">
      <img src="../assets/Shape 2.svg">
      <input type="text" placeholder="Search GitHub Username_" v-model="username">
      </div>
      <div class="fetchError">
      <p>{{ fetchErrorMessage }}</p>
      <searchButton @click="getuserdata">Search</searchButton>
      </div>
    </div>
    
    <userProfileSection v-if="userdata">
      <img :src="userdata.avatar_url" alt="User Avatar" class="desktopAvatar">
    <div class="profile">
      <div class="userHeader">
        <img :src="userdata.avatar_url" alt="User Avatar" class="mobileAvatar">]
        <div class="userHeader_text">
          <div>
            <h2>{{ userdata.name }}</h2>
            <h3>{{ userdata.login }}</h3>
          </div>
          <div>
            <p>Joined {{ formatDate(userdata.created_at) }}</p>
          </div>
          
          
        </div>
        <div>

        </div>
        
      </div>
      <div class="userBio">
        <p v-if="userdata.userBio">{{ userdata.userBio }}</p>
        <p v-else>This profile has no userBio</p>
      </div>
      <div class="userStats">
        <div class="repos">
          <p>Repos</p>
          <h3>{{ userdata.public_repos }}</h3>
        </div>
        <div class="userFollowers">
          <p>Followers</p>
          <h3>{{ userdata.followers }}</h3>
        </div>
        <div class="userFollowing">
          <p>Following</p>
          <h3>{{ userdata.following }}</h3>
        </div>
      </div>

      <div class="bottom_profile">
        <div class="contactInfo">
          <div class="userLocation">
          <img src="../assets/003-pin.png">
          <p v-if="userdata.userLocation">{{ userdata.userLocation }}</p>
          <p v-else class="unavailable">Not available</p>
        </div>
        <div class="userWebsite">
          <img src="../assets/002-url.png">
          <p>{{ userdata.blog }}</p>
          <p v-if="userdata.blog">{{ userdata.blog }}</p>
          <p v-else class="unavailable">Not available</p>
        </div>
        </div>
        
        <div class="additionalLinks">
          <div class="twitter">
          <img src="../assets/004-twitter.png">
          <p>{{ userdata.twitter_username }}</p>
          <p v-if="userdata.twitter_username">{{ userdata.twitter_username }}</p>
          <p v-else class="unavailable">Not available</p>
        </div>
        <div class="github">
          <img src="../assets/001-office-building.png">
          <p v-if="userdata.company">{{ userdata.company }}</p>
          <p v-else class="unavailable">Not available</p>
        </div>
        </div>
      </div>
    </div> 
    </userProfileSection> 
    </div>
    </div>
    </div>
  </main>
</template>

<style scoped>
main{
  background: #141D2F;
}
.desktopAvatar{
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
.query{
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-radius: 15px;
  background: #1E2A47;
  
  padding: 7px;
}
.text_query{
  display: flex;
  align-items: center;
  gap: 7px;
}
searchButton{
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
.fetchError{
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
.userSection{
  display: flex;
  flex-direction: column;
  gap: 16px;
}
userProfileSection{
  display: flex;
  background-color: #1E2A47;
  padding: 32px 24px;
  border-radius: 15px;
  flex-direction: column;
}
.user{
  
  display: flex;
  flex-direction: column;
  gap: 23px;
  
}
.userHeader{
  display: flex;
  gap: 20px;
}
.userHeader_image{
  border-radius: 70px;
  width: 70px;
  height: 70px;
}
.userHeader_text h2{
  color: #FFF;
  font-family: 'Space Mono';
  font-size: 16px;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
}
.userHeader_text p{
  color: #FFF;
  font-family: 'Space Mono';
  font-size: 13px;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
}
.userHeader_text h3{
  color: #0079FF;
  font-family: 'Space Mono';
  font-size: 13px;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
  padding: 6px 0px;
}
.userBio{
  padding-top: 10px;
}
.userBio p{
  color: #FFF;
  font-family: 'Space Mono';
  font-size: 13px;
  font-style: normal;
  font-weight: 400;
  line-height: 25px; 
}
.userStats{
  border-radius: 10px;
  background: #141D2F;
  padding: 18px 15px;
  display: flex;
  justify-content: space-between;

}

.userStats p{
  color: #FFF;
  text-align: center;
  font-family: 'Space Mono';
  font-size: 11px;
  font-style: normal;
  font-weight: 400;
  line-height: normal;
}
.userStats h3{
  color: #FFF;
  text-align: center;
  font-family: 'Space Mono';
  font-size: 16px;
  font-style: normal;
  font-weight: 700;
  line-height: normal;
  text-transform: uppercase;
}
.repos, .userFollowers, .userFollowing{
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
.userLocation{
  display: flex;
  gap: 25px;
}
.userWebsite{
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
userProfileSection{
  display: flex;
}
.contactInfo, .additionalLinks{
  display: flex;
  flex-direction: column;
  gap: 17px;
}



@media screen and (min-width: 1000px) {
  
  .body{
    padding: 145px 200px;
  }

  userProfileSection {
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

  .desktopAvatar {
    display: block;
    width: 117px;
    height: 117px;
    border-radius: 117px;
    margin-right: 32px;
  }

  .mobileAvatar {
    display: none;
  }
  .userHeader_text{
    display: flex;
    justify-content: space-between;
    flex: 1;
  }
  .bottom_profile{
    flex-direction: row;
    justify-content: space-between;
  }
  
  searchButton{
    font-size: 16px;
  }
  .text_query{
    gap: 24px;
  }
  .text_query img{
    padding-left: 24px;
  }
  input{
    font-size: 18px;
    font-weight: 400;
  }
  .userHeader_text h2{
    font-size: 26px;
    font-weight: 700;
  }
  .userHeader_text h3{
    font-size: 16px;
    font-weight: 400;
  }
  .userHeader_text p{
    font-size: 15px;
    font-weight: 400;
    padding-top: 7px;
  }
  .userBio p{
    font-size: 15px;
  }
  .profileStats{
    padding: 15px 32px;
  }
  .profileStats p{
    font-size: 13px;
  }
  .profileStats h3{
    font-size: 22px;
  }
}
.bottom_profile p{
  font-size: 15px;
}
</style>
