<!-- PersonList.vue -->
<template>
    <div>
      <h1>Person List</h1>
      <button @click="showAddForm" v-if="!showForm">Add Person</button>
      
      <!-- Add/Edit Person Form -->
      <div v-if="showForm">
        <h2>{{ isEditing ? "Edit Person" : "Add Person" }}</h2>
        <input v-model="newPerson.name" type="text" placeholder="Name" />
        <button @click="savePerson">{{ isEditing ? "Update" : "Add" }}</button>
      </div>

      <!-- List of Persons -->
      <table>
        <thead>
            <th>Name</th>
            <th>Actions</th>
        </thead>
        <tbody>
            <tr v-for="(person, index) in persons" :key="index">
                <td>{{ person.name }}</td>
                <td>
                    <button @click="editPerson(person)">Edit</button>
                    <button @click="deletePerson(index)">Delete</button>
                </td>
            </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        persons: [
          { name: "John Doe" },
          { name: "Jane Smith" },
          // Add more initial persons here
        ],
        newPerson: { name: "" },
        oldPerson: { name: "" },
        showForm: false,
        isEditing: false,
      };
    },
    methods: {
      showAddForm() {
        this.showForm = true;
        this.isEditing = false;
      },
      editPerson(person) {
        this.newPerson = { ...person };
        this.oldPerson = person
        this.showForm = true;
        this.isEditing = true;
      },
      savePerson() {
        if (this.isEditing) {
          // Update existing person
          const index = this.persons.indexOf(this.oldPerson);
          if(index > -1){
              this.persons[index] = { ...this.newPerson };
          }
          
        } else {
          // Add a new person
          this.persons.push({ ...this.newPerson });
        }
        this.newPerson = { name: "" };
        this.showForm = false;
      },
      deletePerson(index) {
        this.persons.splice(index, 1);
      },
    },
  };
  </script>
  <style>
    table {
        margin-top: 3%;
        margin-right: auto;
        margin-left: auto;
        border-collapse: collapse;
    }

    td, th {
        border: 1px solid #777;
        padding: 0.5rem;
        text-align: center;
    }

    tbody tr:nth-child(odd) {
        background: #eee;
    }
    
    caption {
        font-size: 0.8rem;
    }

    button{
        margin-left: 2px;
        margin-right: 2px;
    }

    input[type=text], select {
        padding: 12px 20px;
        margin: 8px 0;
        display: inline-block;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-sizing: border-box;
        margin-right: 5px;
    }
</style>