<template>
    <div>

        <a :href="record.html_url"
            target="_blank"
            class="commit">{{ record.number }}</a> - <span class="message">{{ record.title | truncate }}</span>
        <br> by
        <span class="author"><a :href="record.user.html_url" target="_blank">{{ record.user.login }}</a></span> at
        <span class="date">{{ record.created_at | formatDate }}</span>

    </div>
</template>

<script>
export default {

    props: ['record']

}
</script>