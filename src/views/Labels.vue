<template>
    <Layout>
        <div class="tags">
            <router-link class="tag" v-for="tag in tags" :key="tag.id" :to="`/labels/edit/${tag.id}`">
                <span>{{tag.name}}</span>
                <Icon name="right"/>
            </router-link>
        </div>
        <div class="createTag-wrapper">
            <Button class="createTag" @click="createTag">新建标签</Button>
        </div>
    </Layout>
</template>

<script lang='ts'>
    import {Component} from 'vue-property-decorator';
    import Button from '@/components/Button.vue';
    import {mixins} from 'vue-class-component';
    import TagHelper from '@/mixins/TagHelper';


    @Component({
        components: {Button},
    })
    export default class Labels extends mixins(TagHelper) {
        get tags() {
            return this.$store.state.tagList;
        }

        beforeCreate() {
            this.$store.commit('fetchTags');
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