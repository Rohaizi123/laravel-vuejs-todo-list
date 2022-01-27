<template>
    <div class="row mx-auto">
        <div class="col-md-12">
            <div class="row bg-white rounded shadow-sm p-2 add-todo-wrapper align-items-center justify-content-center">
                <div class="col">
                    <input class="form-control form-control-lg border-0 add-todo-input bg-transparent rounded" type="text" v-model="item.name" placeholder="Add new task .." required>
                </div>
                <div class="col-auto px-0 mx-0 mr-2">
                    <button type="button" class="btn btn-primary"
                        :disabled='!isDisabled()'
                        @click="addItem()"
                        >Add
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data:function () {
            return {
                item : {
                    name : ""
                }
            }
        },
        methods: {
            addItem() {
            if (this.item.name == '') {
                return;
            }
              axios.post('api/item/store', {
                  item: this.item
              }).then((response) => {
                  if (response.status == 201) {
                    this.item.name = "";
                    this.$emit('reloadlist');
                }
            }).catch((error) => {
              console.log(error);
          })
        },
        isDisabled() {
            return this.item.name;
        }
      }
    }
</script>

<style>
.add-todo-input,
.edit-todo-input {
    outline: none;
}

.add-todo-input:focus,
.edit-todo-input:focus {
    border: none !important;
    box-shadow: none !important;
}
</style>
