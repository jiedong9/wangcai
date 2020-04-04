<template>
    <Layout>
        <div class="navBar">
            <Icon class="leftIcon" name="left" @click="goBack"/>
            <span class="title">编辑标签</span>
            <span class="rightIcon"></span>

        </div>
        <div class="form-wrapper">
            <FormItem :value="tag.name"
                      @update:value="updateTag"
                      field-name="标签名" placeholder="请输入标签名"/>
        </div>
        <div class="button-wrapper">
            <Button @click="remove">删除标签</Button>
        </div>
    </Layout>

</template>

<script lang='ts'>
    import Vue from 'vue'
    import {Component} from 'vue-property-decorator'
    import FormItem from '@/components/Money/FormItem.vue'
    import Button from '@/components/Button.vue'
    import {store} from '@/store/index2'

    @Component({
        components: {Button, FormItem}
    })
    export default class EditLabel extends Vue {
        tag?: Tag = undefined

        created() {
            this.tag = store.findTag(this.$route.params.id)
            if (!this.tag) {
                this.$router.replace('/404') // 路由器进行分发
            }
        }

        updateTag(name: string) {
            if (this.tag) {
                store.updateTag(this.tag.id, name)
            }
        }

        remove() {
            if (this.tag) {
                if (store.removeTag(this.tag.id))
                    this.$router.back()
            }
        }

        goBack() {
            this.$router.back()
        }

    }
</script>

<style lang='scss' scoped>
    .navBar {
        display: flex;
        align-items: center;
        justify-content: space-between;
        height: 48px;
        font-size: 16px;
        text-align: center;
        padding: 12px 16px;

        > .leftIcon {
            font-size: 24px;
        }

        > .rightIcon {
            font-size: 24px;
        }
    }

    .form-wrapper {
        border-top: 1px solid #e6e6e6;
        margin-top: 8px;
    }

    .button-wrapper {
        text-align: center;
        padding: 16px;
        margin-top: 44px;
    }
</style>