<template>
  <div class="container">
    <h2>Add contact</h2>
    <form>
      <label for="first_name">First name</label>
      <input v-model="first_name" id="" class="form-control" type="text">
      <label for="last_name">Last name</label>
      <input v-model="last_name" id="" class="form-control" type="text">
      <label for="email" >Email</label>
      <input v-model="email" id="" class="form-control" type="text" required>
      <label for="created_at">created_at</label>
      <input v-model="created_at" id="created_at" class="form-control" type="text">
      <label for="updated_at">updated_at</label>
      <input v-model="updated_at" id="updated_at" class="form-control" type="text">
      <button v-show="!editMode" @click.prevent="addContact" class="btn btn-success">Create contact</button>
      <button v-show="editMode" @click.prevent="saveNewData" class="btn btn-success">Create contact</button>
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
      <tr v-for="(contact, i) in contactsArray" :key="i">
        <td>{{ returnProperty(contact.first_name) }}</td>
        <td>{{ returnProperty(contact.last_name) }}</td>
        <td>{{ returnProperty(contact.email) }}</td>
        <td>{{ returnProperty(contact.created_at) }}</td>
        <td>{{ returnProperty(contact.updated_at) }}</td>
        <td><button @click="deleteContact(contact)" class="btn btn-danger">Delete</button></td>
        <td><button @click="showContact(contact)" class="btn btn-warning">Edit</button></td>
      </tr>
    </table>
  </div>
</template>


<script>
export default {
  name: 'ContactList',
  data(){
    return {
      editMode: false,
      whatToEdit:'',
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
        created_at: this.created_at,
        updated_at: this.updated_at,
      }
    },

    addContact(){
      this.contacts.unshift(this.createContact());
    },

    deleteContact(contact){
      const index = this.contacts.indexOf(contact);
      this.contacts.splice(index, 1);
    },

    returnProperty(property){
      return property || 'Nepoznato';
    },

    showContact(contact){
      this.editMode = true;
      this.whatToEdit = contact;
      this.first_name = contact.first_name;
      this.last_name = contact.last_name;
      this.email = contact.email;
      this.created_at = contact.created_at;
      this.updated_at = contact.updated_at;
    },

    saveNewData(){
      /* RESENJE BROJ JEDAN (RADI)
      this.addContact();
      this.deleteContact(this.whatToEdit);
      */
     /*resenje broj 2 (RADI)
      const indexx = this.contacts.indexOf(this.whatToEdit);
      this.contacts[indexx].first_name = this.first_name;
      this.contacts[indexx].last_name = this.last_name;
      this.contacts[indexx].email = this.email;
      this.contacts[indexx].created_at = this.created_at;
      this.contacts[indexx].updated_at = this.updated_at;
      */
     //RESENJE BROJ 3
     const indexx = this.contacts.indexOf(this.whatToEdit);
     //console.log(indexx);
     //console.log(this.whatToEdit);
     this.contacts[indexx] = this.createContact();
     //console.log(this.contacts[indexx]);
     //console.log(this.createContact());
     //console.log(this.contacts);
    this.contacts = JSON.parse(JSON.stringify(this.contacts));//ovo je ovde potrebno za resenje broj 3. Sta se ovde desava? Iz nekog razloga Vue ne zna da smo promenili, editovali objekat, pa nije automatski refreshovao DOM, pa zato ne vidimo rezultat editovanja. Medjutim, sa ovim JSON stringify i parsiranjem Vue ovo primeti. Ovo sa JSON stvara novu referencu za objekat. Pa sa ovim, automatski kada editujemo contact, odamh se vidi rezultat.
    }

   
  },

  computed: {
    contactsArray(){
      return this.contacts;
    }
  }
}
</script>

<style scoped>

</style>