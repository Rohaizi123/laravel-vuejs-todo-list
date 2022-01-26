<template>
    <div>
        <div class="todolist" v-for="(item, index) in items" :key="index">
            <list-item-component 
                :item="item"
                v-on:itemchanged="$emit('reloadlist')"
            >
            </list-item-component> 
        </div>
    </div>
</template>

<script>
    import ListItemComponent from "./ListItemComponent"
    export default {
        props:['items'],
        components: {
            ListItemComponent
        }
    }
</script>
