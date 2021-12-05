<template>
    <base-dialog
        v-if="inputInvalid"
        title="Invalid Input"
        @close-dialog="checkOut"
    >
        <template #default>
            <p>At least one of your inputs is empty</p>
            <p>Please, make sure to add a value for each input</p>
        </template>
        <template #actions>
            <base-button @click="checkOut"> close </base-button>
        </template>
    </base-dialog>
    <base-card>
        <form @submit.prevent="addNewResource">
            <div class="form-control">
                <label for="title">Title</label>
                <input id="title" name="title" type="text" ref="newTitle" />
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea
                    id="description"
                    name="description"
                    rows="3"
                    ref="newDescription"
                >
                </textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input id="link" name="link" type="url" ref="newLink" />
            </div>
            <div>
                <base-button type="submit">Add Resource</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
export default {
    components: { BaseButton },
    inject: ['addResource'],
    data() {
        return {
            inputInvalid: false,
        };
    },
    methods: {
        addNewResource() {
            const titleInput = this.$refs.newTitle.value;
            const descriptionInput = this.$refs.newDescription.value;
            const linkInput = this.$refs.newLink.value;

            if (
                titleInput.trim() === '' ||
                descriptionInput.trim() === '' ||
                linkInput.trim() === ''
            ) {
                this.inputInvalid = true;
                return;
            }
            this.addResource(titleInput, descriptionInput, linkInput);
        },
        checkOut() {
            this.inputInvalid = false;
        },
    },
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
