<template>
    <div>
        <a :href="record.html_url"
        target="_blank"
        class="commit">{{ record.sha.slice(0, 7) }}</a>

        - <span class="message">{{ record.commit.message | truncate }}</span>
        <br> by
        <span class="author"><a :href="record.author.html_url" target="_blank">{{ record.commit.author.name }}</a></span>
        at
        <span class="date">{{ record.commit.author.date | formatDate }}</span>
    </div>
</template>

<script>
export default {

    props: ['record'],

}
</script>