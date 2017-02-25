<template>
    <div id="catApp">
        <h2> {{ title }} </h2>
        <h4>  New Cat <h4>

        <form v-on:submit.prevent="onSubmit">
            <div>
                <input name="title" type="text" placeholder="name" v-model="cat.name" />
            </div>
            <div>
                <input name="year" type="text" placeholder="age" v-model="cat.age" />
            </div>
            <div>
                <input name="owner" type="text" placeholder="owner" v-model="cat.owner" />
            </div>
            <div>
                <label for="pregnant">Pregnant?</label>
                <input type="checkbox" v-model="cat.pregnant" name="pregnant" id="pregnant" />
            </div>
            <button v-if="add">Add</button>
            <button v-else>Add</button>
        </form>
    </div>
</template>

<script>
    export default {
            name: 'catApp',
            data() {
                 return {
                    title: 'Manage Cats',
                    add:  false,
                    updating: false,
                    updateIndex: 0,
                    cats: [],
                    cat: {
                        name: '',
                        age: '',
                        owner: '',
                        pregnant: false
                     }
                 }
            },

            methods: {
                onSubmit() {
                    if(this.add){
                        this.onUpdate();
                        return;
                    }
                    this.cats.push(this.cat);
                    this.cat = {
                        name: '',
                        age: '',
                        owner: '',
                        pregnant: false
                    }
                }
            }
        }

</script>




<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
