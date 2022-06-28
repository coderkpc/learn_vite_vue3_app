<template>
    <button @click="handleChange">change</button>
    <p>{{msg}}</p>
</template>


<script setup lang="ts">
import { customRef, triggerRef } from 'vue';

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

let msg = MyRef<string>('小柯')

const handleChange = () => {
    msg.value = '大柯'    
}
</script>
 
<style>

</style>
