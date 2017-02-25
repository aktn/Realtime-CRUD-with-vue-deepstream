<template>
    <div id="catApp" class="center">
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


         <h4> All Cat Lists</h4>
            <table>
                <tr>
                    <th> Name </th>
                    <th> Age </th>
                    <th> Owner </th>
                    <th> Pregnant </th>
                    <th> Update </th>
                    <th> Delete </th>
                </tr>
                <tr v-for="(c, index) in cats">
                    <td>{{ c.name }}</td>
                    <td>{{ c.age }}</td>
                    <td>{{ c.owner }}</td>
                    <td v-if="c.pregnant">✓</td>
                    <td v-else>✗</td>
                    <td v-on:click.prevent="onEdit(index)"><a>Edit</a></td>
                    <td v-on:click.prevent="onDelete(index)"><a>Delete</a></td>
                </tr>
            </table>
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
                },

                onEdit(index) {
                    this.updating = true;
                    this.updateIndex = index;
                    this.cat = this.cats[index];
                },

                onUpdate() {
                    this.updating = false;
                    this.cats[this.updateIndex] = this.cat;
                     this.cat = {
                        'name': '',
                        'age': '',
                        'owner': '',
                        'pregnant': false
                    }
                },

                onDelete(index){
                    this.cats.splice(index, 1)
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
table {
    border-collapse: collapse;
}

table, th, td {
    border: 1px solid black;
}
.center {
    margin: auto;
    width: 50%;
    border: 3px solid green;
    padding: 10px;
}
</style>
