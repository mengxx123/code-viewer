<template>
    <my-page title="项目文件浏览器">
        <div>请输入 GitHub 的项目地址</div>
        <input v-model="input" placeholder="yunser/doc-example" />
        <br>
        <ui-raised-button label="浏览" primary @click="start" />
    </my-page>
</template>

<script>
    export default {
        data () {
            return {
                input: 'yunser/doc-example',
                page: {
                    menu: [
                        {
                            type: 'icon',
                            icon: 'help',
                            to: '/help'
                        }
                    ]
                }
            }
        },
        mounted() {
            this.init()
        },
        methods: {
            init() {
            },
            start() {
                this.$router.push('view')
            }
        }
    }
</script>

<style lang="scss" scoped>
</style>
