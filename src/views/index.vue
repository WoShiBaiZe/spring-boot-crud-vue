<template>
<!--    <el-container style="height: 500px; border: 1px solid #eee">-->
<!--        <el-aside width="200px" style="background-color: rgb(238, 241, 246)">-->
<!--            <el-menu router :default-openeds="['0','1']">-->
<!--                <el-submenu v-for="(item,index) in $router.options.routes" :index="index+''">-->
<!--                    <template slot="title"><i class="el-icon-setting"></i>{{item.name}}</template>-->
<!--                    <el-menu-item v-for="(item2,index2) in item.children" :index="index+'-'+index2">{{item2.name}}</el-menu-item>-->
<!--                    <el-menu-item v-for="(item2,index2) in item.children" :index="item2.path" :class="$route.path==item2.paht?'is-active':''">{{item2.name}}</el-menu-item>-->
<!--                </el-submenu>-->
<!--            </el-menu>-->
<!--        </el-aside>-->
<!--        <el-main>-->
<!--            <router-view></router-view>-->
<!--        </el-main>-->
<!--    </el-container>-->
    <router-view></router-view>
</template>

<script>
    export default {
        name: "index"
    }
</script>

<style scoped>

</style>