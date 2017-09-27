<template>
    <div id="app">
        <div class="container">
            <form @submit.prevent="generator">
                <div class="row">
                    <div class="col-md-6">
                        <div class="form-group">
                            <label for="name">Name:</label>
                            <input type="text" v-model="name" class="form-control">
                        </div>
                    </div>
                    <div class="col-md-6">
                        <div class="form-group">
                            <label for="prefix">Prefix:</label>
                            <input type="text" v-model="prefix" class="form-control">
                        </div>
                    </div>
                    <div class="col-md-6">
                        <div class="form-group">
                            <label for="description">Description:</label>
                            <input type="text" v-model="description" class="form-control">
                        </div>
                    </div>
                    <div class="col-md-6">
                        <div class="form-group">
                            <label for="text">Body:</label>
                            <textarea class="form-control" v-model="text" cols="30" rows="10"></textarea>
                        </div>
                    </div>
                </div>
                <div class="text-center">
                    <button class="btn" type="submit">generator</button>
                </div>
                <hr>
                <div class="form-group">
                    <label for="text">Body:</label>
                    <textarea class="form-control" v-model="resp" cols="30" rows="10"></textarea>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import { html } from 'common-tags'
import 'jquery';
import 'bootstrap-loader'

export default {
    name: 'app',
    methods: {
        generator() {
            const spSnippet = this.text.replace(/"/g, '\\"').split('\n'),
                spSnippetLength = spSnippet.length,
                newSnippet = spSnippet.map((line, index) => {
                    return index === spSnippetLength - 1 ? `"${line}"` : `"${line}",`
                }),
            ns = newSnippet.join('\n').replace(/\s{4}/g, '\\t')

this.resp = html`"${this.name}": {
    "prefix": "${this.prefix}",
    "body": [
        ${ns}
    ],
    "description": "${this.description}"
},`
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
.container {
    padding-top: 20px;
}
</style>