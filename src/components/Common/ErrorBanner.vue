<template>
    <div class="container" v-if="isVisible">
        <p>{{ message }}</p>    
    </div>
</template>

<script>
export default {
    name: 'ErrorBanner',
    components: {},
    props: {
        message: {
            required: true,
            type: String
        },
        isVisible: {
            default: false,
            type: Boolean
        }
    }
}
</script>

<style>
    .container {
        padding-bottom: 10px;
        background-color: #ff0033;
        border-radius: 10px;
        margin-bottom: 20px;
    }
    .container > p {
        display: inline;
        vertical-align: middle;
        padding-left: 20px;
        padding-top: 10px;
        font-weight: bold;
    }
</style>