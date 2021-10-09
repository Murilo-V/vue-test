<template>
    <button :class="{ primary: btnPrimary, secondary: btnSecondary, }">{{ text }}</button>
</template>

<script>
export default {
    name: "Button",
    props: {
        text: String,
        btnPrimary: Boolean,
        btnSecondary: Boolean,
    },
}
</script>

<style scoped>
    .primary {
        border-radius: 0.75rem;
        background-color: #483698;
        color: #fff;
        font-weight: bold;
        border: none;
        font-size: 14pt;
    }

    .secondary {
        border-radius: 0.75rem;
        background-color: #f8de40;
        color: #282828;
        font-weight: bold;
        border: none;
        font-size: 16pt;
    }
</style>