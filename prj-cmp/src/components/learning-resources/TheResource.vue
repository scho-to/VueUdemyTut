<template>
  <base-card>
    <base-button 
      @click="setSelectedResource('stored-resources')"
      :mode="storedResButtonMode"
    >Stored Resources</base-button>
    <base-button 
      @click="setSelectedResource('add-resource')"
      :mode="addResButtonMode"
    >Add Resource</base-button>
  </base-card>
  <component :is="selectedTab"></component>
</template>

<script>
  import StoredResources from './StoredResources.vue';
  import AddResource from './AddResource.vue';
  import faker from 'faker';
  export default {
    components: {
      StoredResources,
      AddResource
    },
    data(){
      return {
        selectedTab: "stored-resources",
        storedResources: [
        {
          id: faker.random.uuid,
          title: faker.lorem.words(3),
          description: faker.lorem.sentences(4, " "),
          link: "#"
        },
        {
          id: faker.random.uuid,
          title: faker.lorem.words(1),
          description: faker.lorem.sentences(3, " "),
          link: "#"
        }
        ]
      }
    },
    provide(){
      return {
        resources: this.storedResources,
        addResource: this.addResource,
        removeResource: this.removeResource
      }
    },
    computed: {
      storedResButtonMode(){
        return this.selectedTab === 'stored-resources' ? null : 'flat';
      },
      addResButtonMode(){
        return this.selectedTab === 'add-resource' ? null : 'flat';
      }
    },
    methods: {
      setSelectedResource(resource) {
        this.selectedTab = resource;
      },
      addResource(title, description, link) {
        const newResource = {
          id: faker.random.uuid,
          title: title,
          description: description,
          link: link
        };
        this.storedResources.unshift(newResource);
        this.selectedTab = "stored-resources";
      },
      removeResource(resId){
        const resIndex = this.storedResources.findIndex(res => res.id === resId);
        this.storedResources.splice(resIndex,1);
      }
    }
  }
</script>

<style scoped>

</style>