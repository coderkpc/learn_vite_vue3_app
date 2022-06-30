<template>
    <button @click="handleChange">change</button>
    <p>{{r1}}</p>
    <p>{{r2}}</p>
</template>


<script setup lang="ts">
import { customRef, ref, shallowRef } from 'vue';

// options API
defineOptions({
    name: 'App',
});

function MyRef<T> (value: T) {
    return customRef((track, trigger) => {
        return {
            get () {
                track()
                return value
            },
            set (newVal: T) {
                value = newVal
                console.log(value)
                trigger()
            }
        }
    })
}

// let msg = MyRef<string>('小柯')

let r1 = shallowRef({
    foo: '小柯',
    bar: '真帅'
})

let r2 = ref('去你的')

const handleChange = () => {
    r1.value.foo = '大柯'
    r2.value = '我不去'
    console.log(r1);
    // 因为ref的set方法底层调用了triggerRefValue所以会产生视图更新
}
</script>
 
<style>

</style>
