<template>
  <div class="container">
    <h2>Add contact</h2>
    <form>
      <label for="first_name">First name</label>
      <input v-model="first_name" id="" class="form-control" type="text">
      <label for="last_name">Last name</label>
      <input v-model="last_name" id="" class="form-control" type="text">
      <label for="email" required>Email</label>
      <input v-model="email" id="" class="form-control" type="text">
      <button @click.prevent="addContact" class="btn btn-success">Create contact</button>
    </form>
    <hr>

    <h2>Contact list</h2>
    <table class="table">
      <tr>
        <th>First name</th>
        <th>Last name</th>
        <th>Email</th>
        <th>Created at</th>
        <th>Updated at</th>
      </tr>
      <tr v-for="(contact, i) in contacts" :key="i">
        <td>{{ returnProperty(contact.first_name) }}</td>
        <td>{{ returnProperty(contact.last_name) }}</td>
        <td>{{ returnProperty(contact.email) }}</td>
        <td>{{ returnProperty(contact.created_at) }}</td>
        <td>{{ returnProperty(contact.updated_at) }}</td>
        <td><button @click="deleteContact(contact)" class="btn btn-danger">Delete</button></td>
      </tr>
    </table>
    
  </div>
</template>


<script>
export default {
  name: 'ContactList',
  data(){
    return {
      first_name: '',
      last_name: '',
      email: '',
      created_at: '',
      updated_at: '',
      contacts: [
        { first_name: 'Ziki', last_name: 'Zikic', email: 'ziki@gmail.com', created_at: '', updated_at: ''},
        { first_name: 'Miki', last_name: 'Mikic', email: 'miki@gmail.com', created_at: '', updated_at: ''}
      ],
    }
  },
  methods:{
    createContact(){
      return {
        first_name: this.first_name,
        last_name: this.last_name,
        email: this.email,
        created_at:'',
        updated_at:'',
      }
    },

    addContact(){
      this.contacts.unshift(this.createContact());
    },

    deleteContact(contact){
      const index = this.contacts.indexOf(contact);
      //console.log(index);
      this.contacts.splice(index, 1);
    },

    returnProperty(property){
      return property || 'Nepoznato';
    },
  }
  
}
</script>

<style scoped>

</style>