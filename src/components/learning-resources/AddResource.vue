<template>
    <base-card>
        <form @submit.prevent="addNewResource">
            <div class="form-control">
                <label for="title">Title</label>
                <input id="title" name="title" type="text" v-model="newTitle" />
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea
                    id="description"
                    name="description"
                    rows="3"
                    v-model="newDescription"
                >
                </textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input id="link" name="link" type="url" v-model="newLink" />
            </div>
            <div>
                <base-button type="submit">Add Resource</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>
export default {
    data() {
        return {
            newTitle: '',
            newDescription: '',
            newLink: '',
        };
    },
    methods: {
        addNewResource() {
            this.$emit(
                'add-new-resource',
                this.newTitle,
                this.newDescription,
                this.newLink
            );
        },
    },
    emits: ['add-new-resource'],
};
</script>

<style>
label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
}

input,
textarea {
    display: block;
    width: 100%;
    font: inherit;
    padding: 0.15rem;
    border: 1px solid #ccc;
}

input:focus,
textarea:focus {
    outline: none;
    border-color: #3a0061;
    background-color: #f7ebff;
}

.form-control {
    margin: 1rem 0;
}
</style>
