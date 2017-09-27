<template>
    <div id="app">
        <input type="text" v-model="name" placeholder="name">
        <br />
        <input type="text" v-model="prefix" placeholder="prefix">
        <br />
        <input type="text" v-model="description" placeholder="description">
        <br />
        <textarea v-model="text" cols="30" rows="10"></textarea>
        <br />
        <button @click.prevent="generator">generator</button>
        <br />
        <textarea v-model="resp" cols="30" rows="10"></textarea>
    </div>
</template>

<script>
export default {
    name: 'app',
    methods: {
        generator() {
            const spSnippet = this.text.replace(/"/g, '\\"').split('\n'),
                spSnippetLength = spSnippet.length,
                newSnippet = spSnippet.map((line, index) => {
                    return index === spSnippetLength - 1 ? `"${line}"` : `"${line}",`;
                })
            this.body = newSnippet.join('\n').replace(/\s{4}/g, '\\t')
            
this.resp =`"${this.name}": {
    "prefix": "${this.prefix}",
    "body": [
        ${this.body}
    ],
    "description": "${this.description}"
}`
        }
    },
    data() {
        return {
            name: '',
            prefix: '',
            body: '',
            description: '',
            text: '',
            resp: ''
        }
    }
}
</script>

<style>

</style>




