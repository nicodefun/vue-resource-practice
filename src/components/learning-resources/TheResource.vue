<template>
  <base-card>
    <base-button
      @click="setSelectedTab('store-resources')"
      :mode="storedResBtnMode"
      >Stored Resources</base-button
    >
    <base-button @click="setSelectedTab('add-resource')"
    :mode=" adddResBtnMode"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
  
</template>
<script>
import StoreResources from './StoreResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoreResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: 'store-resources',
      storeResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js ddocumentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn how to google....',
          link: 'https://google.org',
        },
      ],
    };
  },
  computed:{
    storedResBtnMode(){
        return this.selectedTab === 'store-resources' ? null : 'flat';
    },
    adddResBtnMode(){
        return this.selectedTab === 'add-resource' ? null : 'flat';
    }
  },
  provide() {
    return {
      resources: this.storeResources,
      addResource: this.addResource,
      removeResource: this.removeResource
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, des, url){
      const newResource = {
        id: new Date().toISOString,
        title,
        des,
        url
      };
      this.storeResources.unshift(newResource);
      this.selectedTab = 'store-resources';
    },
    removeResource(id){
      const resIndex = this.storeResources.findIndex(res=>res.id === id);
      this.storeResources.splice(resIndex, 1);
    }
  },
};
</script>
