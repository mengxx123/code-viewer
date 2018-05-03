<template>
    <my-page title="项目文件浏览器">
        <div class="left-box">
            <ul class="file-list">
                <li class="item" v-for="file in files" @click="selectFile(file)">
                    {{ file.name }}
                </li>
            </ul>
        </div>
        <div class="right-box">
            <pre>{{ fileContent }}</pre>
        </div>
    </my-page>
</template>

<script>
    export default {
        data () {
            return {
                files: [],
                cache: {},
                fileContent: '',
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
                this.loadPath('')
            },
            loadFile(path) {
                // TODO
                // if (this.cache[path]) {
                //     this.files = this.cache[path]
                //     return
                // }
                let url = path
                this.$http.get(url).then(
                    response => {
                        let data = response.data
                        console.log(data)
                        this.fileContent = data
                        this.cache[path] = data
                    },
                    response => {
                        console.log(response)
                    })
            },
            loadPath(path) {
                // TODO
                // if (this.cache[path]) {
                //     this.files = this.cache[path]
                //     return
                // }
                let url = 'https://api.github.com/repos/yunser/doc-example/contents/' + path
                this.$http.get(url).then(
                    response => {
                        let data = response.data
                        console.log(data)
                        this.files = data
                        this.cache[path] = data
                    },
                    response => {
                        console.log(response)
                    })
            },
            selectFile(file) {
                if (file.type === 'file') {
                    console.log(file)
                    this.loadFile(file.download_url)
                } else {
                    this.loadPath(file.path)
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
.file-list {
    .item {
        height: 48px;
        padding-left: 16px;
        line-height: 48px;
        cursor: pointer;
        &:hover {
            background-color: #f1f1f1;
        }
    }
}
.left-box {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    width: 400px;
    border-right: 1px solid #eee;
}
.right-box {
    position: absolute;
    top: 0;
    left: 400px;
    bottom: 0;
    right: 0;
    padding: 16px;
    border-right: 1px solid #eee;
}
</style>
