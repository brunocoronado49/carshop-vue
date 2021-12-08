<template>
    <div>
        <h4>{{ author }}</h4>
    </div>
</template>

<script>
export default {
    name: "Credits",
    props: {
        author: String,
    }
}
</script>