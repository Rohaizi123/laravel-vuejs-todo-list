<template>
<div class="todo-item mt-3">
	<ul class="list-unstyled">	
		<li class="ui-state-default">
            <span>
				<input type="checkbox" 
				v-model="item.completed"
				@change="updateCheck()" 
				id="defaultCheck" 
				/>
            </span>
            <label :class="[item.completed ? 'completed' :'item']" for="defaultCheck">{{ item.name }}</label>
            <button type="button" @click="removeItem()" class="btn btn-danger btn-sm float-md-right"><i class="fa fa-trash"></i>
            </button>
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

.completed {
    text-decoration: line-through;
    color:red;
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
