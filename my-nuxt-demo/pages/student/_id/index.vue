<template>
    <div>
        详情{{$route.params.id}}
    </div>
</template>

<script>
    export default {
        // 使用validate方法进行路由参数校验,这个方法必须返回一个布尔值,
        validate(obj) {
            return /^\d+$/.test(obj.params.id)
        }
    }
</script>

<style lang="sass" scoped>

</style>