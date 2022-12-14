<template>
  <q-page class="window-height window-width row justify-center items-center">

    <div>
      <h1>{{profileName}}</h1>
      <q-avatar size="250px" >
        <img src="..\assets\bergquist-profile.jpeg" />
      </q-avatar>
   </div>

    <div>
      <p>{{bioText}}</p>
    </div>

    <div>
      <h2>Following</h2>
        <li v-for="user in following" :key="user.id">
          <profile-thumbnail :title="user.name" :image="user.image" size="50px" />
        </li>
    </div>

    <div>
      <h2>Followers</h2>
      <li v-for="user in followers" :key="user.id">
        <profile-thumbnail :title="user.name" :image="user.image" size="50px" />
      </li>
    </div>

      </q-page>
</template>

<script setup lang="ts">

  import { date } from 'quasar';
  import { createBlock, defineComponent, ref, computed, Ref} from 'vue';
  import ProfileThumbnail from 'src/components/profile-page-components/ProfileThumbnail.vue'

  const following = [
    {name: 'Luke Skywalker', image: '../../assets/bergquist-progile.jpeg', id: '1'},
    {name: 'Darth Vader', image: '../../assets/bergquist-progile.jpeg', id: '2'},
    {name: 'Jar Jar Binks', image: '../../assets/bergquist-progile.jpeg', id: '3'}
  ]

  const followers = [
    {name: 'Taiden Aylor', image: '../../assets/bergquist-progile.jpeg', id: '4'},
    {name: 'Sack Janford', image: '../../assets/bergquist-progile.jpeg', id: '5'},
    {name: 'Pautumn Elton', image: '../../assets/bergquist-progile.jpeg', id: '6'}
  ]

  const profPic = '..\assets\bergquist-profile.jpeg';
  const profileName = ref('Earl Bergquist');
  const bioText = ref("Hi, I'm Earl Bergquist. I'm a CTE teacher at Garfiled High School in Seattle. I like learning, Pop Tarts, and, above all, Star Wars.")

</script>

<style scoped>
  li {
    list-style: none;
  }
  .q-avatar {
    display: block;
    margin: auto;
  }

  div {
    margin: 20px;
  }

  h2 {
    text-align: center;
  }

  p {
    font-size: 16pt;
    text-align: center;
  }
</style>
