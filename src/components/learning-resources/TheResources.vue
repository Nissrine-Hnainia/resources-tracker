<template>
    <base-card>
        <base-button
            @click="setSelectedTab('stored-resources')"
            :mode="storedButtonMode"
            >Stored Resources</base-button
        >
        <base-button
            @click="setSelectedTab('add-resource')"
            :mode="addButtonMode"
            >Add Resources
        </base-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab" @add-new-resource="addResource">
        </component>
    </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
    components: {
        StoredResources,
        AddResource,
    },
    computed: {
        storedButtonMode() {
            return this.selectedTab === 'stored-resources' ? null : 'flat';
        },
        addButtonMode() {
            return this.selectedTab === 'add-resource' ? null : 'flat';
        },
    },
    data() {
        return {
            selectedTab: 'stored-resources',
            storedResources: [
                {
                    id: 'first',
                    title: 'Official Vue Guide',
                    description: 'The official Vue.js documentation',
                    link: 'https://vuejs.org',
                },
                {
                    id: 'second',
                    title: 'Stackoverflow',
                    description: "The developer's go to friend",
                    link: 'https://stackoverflow.com/',
                },
            ],
        };
    },
    provide() {
        return {
            resources: this.storedResources,
            addResource: this.addResource,
        };
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        },
        addResource(title, description, url) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: url,
            };
            this.storedResources.push(newResource);
            this.selectedTab = 'stored-resources';
        },
    },
};
</script>
