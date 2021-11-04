<template>
  <view class="header-container">
    <view class="header">
      <text class="title">{{title}} {{info}}</text>
      <touchable-opacity :on-press="getNewName" class='refresh-button'>
        <image :source='refreshIcon' class='image-style'/>
      </touchable-opacity>
    </view>
    <view class="divider"/>
  </view>
</template>

<script>
import refreshIcon from '../assets/refresh_icon.png';
import axios from "axios";

export default {
  data: function() {
    return {
      refreshIcon,
      info: null,
    };
  },
  mounted() {
      const options = {
      method: 'GET',
      url: 'https://randomuser.me/api/',
      };
       
      axios
      .get('https://randomuser.me/api/')
      .then(response => {
        this.info = response.data.results[0].name.first
      })
      .catch(error => {
        console.log(error)
        this.info = "Raphael"
      })
  },
  props: {
    title: String,
  },
  methods: {
    getNewName: function(){
      const options = {
      method: 'GET',
      url: 'https://randomuser.me/api/',
      };
       
      axios
      .get('https://randomuser.me/api/')
      .then(response => {
        this.info = response.data.results[0].name.first
      })
      .catch(error => {
        console.log(error)
        this.info = "Raphael"
      })
    },
  }
};
</script>

<style>
.header {
  justify-content: space-between;
  display: flex;
  flex-direction: row;
}
.title {
  color: #505050;
  font-size: 30px;
  text-align: left;
  font-weight: bold;
}
.divider {
  border-bottom-color: #505050;
  border-bottom-width: 1px;
  opacity: .3;
  margin-top: 10px;
  margin-bottom: 10px;
}
.image-style { 
  height: 20;
  width: 20;
}
.refresh-button {
  padding-top: 7;
  padding-bottom: 5;
}
</style>