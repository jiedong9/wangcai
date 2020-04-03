<template>
    <Layout>
        <ol class="tags">
            <li class="tag" v-for="tag in tags" :key="tag">
                <span>{{tag}}</span>
                <Icon name="right"/>
            </li>
        </ol>
        <div class="createTag-wrapper">
            <button class="createTag" @click="createTag">新建标签</button>
        </div>
    </Layout>
</template>

<script lang='ts'>
    import Vue from 'vue'
    import {Component} from 'vue-property-decorator'
    import {tagListModel} from '@/models/tagListModel'

    tagListModel.fetch()
    @Component
    export default class Labels extends Vue {
        tags = tagListModel.data

        createTag() {
            const name = window.prompt('请输入标签名')
            if (name) {
                const message = tagListModel.create(name)
                if (message === 'duplicated') {
                    window.alert('嘿伙计，标签重复了，换个吧')
                }
            }
        }
    }
</script>

<style lang='scss' scoped>
    .tags {
        background: white;
        font-size: 16px;

        > .tag {
            min-height: 44px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid #e6e6e6;

            > span {
                padding-left: 16px;
            }

            > svg {
                margin-right: 16px;
            }
        }
    }

    .createTag {
        background: #CCCCCC;
        color: #333333;
        border-radius: 4px;
        border: none;
        height: 40px;
        padding: 0 16px;

        &-wrapper {
            text-align: center;
            padding: 16px;
            margin-top: 44-16px;
        }

    }
</style>