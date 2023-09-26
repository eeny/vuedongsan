<template>
    <div v-for="(data, idx) in oneRooms" :key="idx">
        <img :src="data.image" class="room-img">
        <!-- <h4 :style="fontcolor[idx]" @click="modalIsOpen = true; selNum = idx">{{data.title}}</h4> -->
        <h4 :style="fontcolor[idx]" @click="send(data.id)">{{data.title}}</h4>
        <p>{{ data.price }}원</p>
    </div>
</template>

<script>
export default {
    name: 'CardComp',
    props: {
        oneRooms: Array,
        fontcolor: Array,
    },
    methods: {
        send(id){
            this.$emit('openModal', id)
        }
    },
}
</script>

<style>

</style>