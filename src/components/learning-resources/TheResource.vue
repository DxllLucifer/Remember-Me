<template>
<base-card>
    <base-button @click="setSelectedTab('stored-resources')" :mode=" storedResButtonMode ">
        Stored Resource
    </base-button>
    <base-button @click="setSelectedTab('add-resource')" :mode=" addResButtonMode ">
        Add Resource
    </base-button>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
</base-card>
</template>

<script>
import StoredResources from './StoredResources.vue'
import AddResource from './AddResource.vue';
export default {
    components:{
        StoredResources,
        AddResource
    },
    provide(){
        return{
            resources: this.storedResources,
            addResource: this.addResource,
            deleteResource: this.removeResource
        };
    },
    computed:{
        storedResButtonMode(){
            return this.selectedTab === 'stored-resources' ? null : 'flat'
        },
        addResButtonMode(){
            return this.selectedTab === 'add-resource' ? null : 'flat'
        }
    },
data(){
    return{
        selectedTab:'stored-resources',
        storedResources:[
      { id: 'official-guid',
        title:'Official Guide',
        description: 'The official Vue.js documentation.',
        link:'https://vuejs.org/'
      },
      { id: 'google',
        title:'Google',
        description: 'Learn to google...',
        link:'https://www.google.com/'
      },
    ]
    }
},
methods:{
    setSelectedTab(tab){
        this.selectedTab = tab;
    },
    addResource(title, description, url){
        const newResource = {
            id: new Date().toISOString(),
            title:title,
            description: description,
            link: url
        };
        this.storedResources.unshift(newResource);
        this.selectedTab = 'stored-resources'
    },
    removeResource(resId){
       const resIndex =  this.storedResources.findIndex(res => res.id === resId);
       this.storedResources.splice(resIndex, 1);
    // this.storedResources = this.storedResources.filter((res) => res.id !== resId);
    // console.log(this.storedResources.length);
       
    },
}
}
</script>

<style>

</style>
