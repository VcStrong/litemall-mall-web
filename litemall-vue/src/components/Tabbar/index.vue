<template>
    <van-tabbar v-model="active" style="z-index: 1999">
        <van-tabbar-item
                v-for="(tab, index) in tabbar"
                :icon="tab.icon"
                :to="tab.path"
                :dot="tab.dot"
                :info="tab.info"
                :key="index">
            {{tab.name}}
        </van-tabbar-item>
    </van-tabbar>
</template>


<script>
    import {Tabbar, TabbarItem} from 'vant';
    import Home from '../../views/home/tabbar-home'
    import {Catalog} from '../../views/items/tabbar-catalog'
    import {Cart} from '../../views/order/tabbar-cart'
    import {User} from '../../views/user/tabbar-user'

    export default {
        data() {
            return {
                active: 0,
                tabbar: [
                    {
                        name: '精选',
                        path: '/',
                        pathName: 'home',
                        icon: 'compass-full',
                        dot: false,
                        info: ''
                    },
                    {
                        name: '分类',
                        path: '/items',
                        pathName: 'class',
                        icon: 'class-full',
                        dot: false,
                        info: ''
                    },
                    {
                        name: '购物车',
                        path: '/order',
                        pathName: 'cart',
                        icon: 'cart-full',
                        dot: false,
                        info: ''
                    },
                    {
                        name: '我的',
                        path: '/user',
                        pathName: 'user',
                        icon: 'wode',
                        dot: false,
                        info: ''
                    }
                ]
            };
        },

        watch: {
            $route: 'changeActive'
        },

        created() {
            const toName = this.$route.name;
            this.setActive(toName);
        },

        methods: {
            changeActive({name}) {
                this.setActive(name);
            },
            setActive(name) {
                this.tabbar.forEach((tab, i) => {
                    if (tab.pathName == name) {
                        console.info(i + '  ' + name + '   ' + tab.path);
                        this.active = i;
                        return false;
                    }
                });
            }
        },

        components: {
            [Tabbar.name]: Tabbar,
            [TabbarItem.name]: TabbarItem
        }
    };
</script>
