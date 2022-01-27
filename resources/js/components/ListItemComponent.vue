<template>
<div class="todo-item mt-3">
	<ul class="list-unstyled">	
		<li class="ui-state-default">
            <span class="mr-1">
				<input type="checkbox" 
				v-model="item.completed"
				@change="updateCheck()" 
				id="defaultCheck" 
				/>
            </span>
            <label :class="[item.completed ? 'todo-completed' :'todo']" for="defaultCheck">{{ item.name }}</label>
            <div class="d-flex float-right">
                <div class="mr-2">
                    <label class="mr-2"><small>{{ item.created_at|formatDate }}</small></label>
                </div>
                <div class="ml-auto">
                    <button type="button" @click="removeItem()" class="btn btn-danger btn-sm float-md-right"><i class="fa fa-trash"></i></button>
                </div>
            </div>
        </li>
    </ul>
</div>
</template>

<script>
    export default {
        props: ['item'],
        methods: {
            updateCheck() {
                axios.put('api/item/' + this.item.id, {
                  item: this.item
                }).then((response) => {
                  // TODO
                }).catch((error) => {
                  console.log(error);
                })
            },
            removeItem() {
                axios.delete('api/item/' + this.item.id)
                .then((response) => {
                    if (response.status == 200) {
                        this.$emit('itemchanged');
                    }
                })
                .catch((error) => {
                  console.log(error);
                })
            }
        }
      }
</script>

<style>
.todo-item {
    padding: 15px;
    margin: 5px 0;
    border-radius: 0;
    background: #F0F0F0;
}

.todo-completed {
    font-weight: bold;
    text-decoration: line-through;
    color:red;
    word-break:break-all;
}

.todo{
    word-break:break-all;
}

input{
    display: inline-block;
    vertical-align: middle;
}

.list-unstyled{
	height:10px;
}

div.checker span {
    display: -moz-inline-box;
    display: inline-block;
    zoom: 1.5;
    text-align: center;
    background-position: 0 -260px;
}

.checker {
    word-wrap: break-word;
    font-size: 15px;
}
.checker input {
    vertical-align: middle;
}
</style>
