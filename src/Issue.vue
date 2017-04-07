<template>
    <div>

        <a :href="record.html_url"
            target="_blank"
            class="commit">{{ record.number }}</a> - <span class="message">{{ record.title }}</span><span v-bind:class="[record.is_insiders ? 'is_insiders' : 'is_stable']">Insiders</span>
        <br> by
        <span class="author"><a :href="record.user.html_url" target="_blank">{{ record.user.login }}</a></span> at
        <span class="date">{{ record.created_at }}</span>

    </div>
</template>

<script>
export default {

    props: ['record']

}
</script>

<style>
.is_insiders {
    font-weight: bold;
    color: green;
    border: 1px solid;
    margin-left: 25px;
}

.is_stable {
    display: none;
}
</style>