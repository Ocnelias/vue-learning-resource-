<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resource')"
      :mode="storedResButtonMode"
    >
      Stored Resources
    </base-button>
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
    >
      Add resource
    </base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedTab"> </component>
  </keep-alive>
</template>

<script>
import StoredResource from './StoredResource.vue';
import AddResource from './AddResource.vue';

export default {
  components: { StoredResource, AddResource },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.deleteResource,
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resource' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  data() {
    return {
      mode: '',
      selectedTab: 'stored-resource',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official guide',
          description: 'documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'google',
          description: 'documentation',
          link: 'https:google.org',
        },
      ],
    };
  },
  methods: {
    setSelectedTab(value) {
      this.selectedTab = value;
    },
    addResource(title, description, link) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: link,
      };
      this.storedResources.push(newResource);
      this.selectedTab = 'stored-resource';
    },
    deleteResource(resId) {
      const resIdx = this.storedResources.findIndex(res => res.id === resId);
      this.storedResources.splice(resIdx, 1);
    },
  },
};
</script>
