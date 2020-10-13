<template>
<div class="container mt-4">
  <h4>Editable Table</h4>
    <table class="table table-bordered mt-4">
      <thead class="thead-light">
        <tr>
          <th width="1">#</th>
          <th width="10%">Remitter ID</th>
          <th width="10%">Name</th>
          <th width="10%">Father's Name</th>
          <th width="10%">Mother's Name</th>
          <th width="10%">Address</th>
          <th width="10%">Contact No.</th>
          <th width="10%">email</th>
          <th width="10%">Description</th>
          <th width="300%">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in items" :key="index">
          <td>{{ index + 1 }}</td>
          <td>
            <span v-if="editIndex !== index">{{ item.id }}</span>
            <span v-if="editIndex === index">
              <input class="form-control form-control-sm" v-model="item.id" />
            </span>
          </td>
          <td>
            <span v-if="editIndex !== index">{{ item.name }}</span>
            <span v-if="editIndex === index">
              <input class="form-control form-control-sm" v-model="item.name" />
            </span>
          </td>
          <td>
            <span v-if="editIndex !== index">{{ item.father }}</span>
            <span v-if="editIndex === index">
              <input
                class="form-control form-control-sm"
                v-model="item.father"
              />
            </span>
          </td>
          <td>
            <span v-if="editIndex !== index">{{ item.mother }}</span>
            <span v-if="editIndex === index">
              <input
                class="form-control form-control-sm"
                v-model.number="item.mother"
              />
            </span>
          </td>
          <td>
            <span v-if="editIndex !== index">{{ item.address }}</span>
            <span v-if="editIndex === index">
              <input class="form-control form-control-sm" v-model="item.address" />
            </span>
          </td>
          <td>
            <span v-if="editIndex !== index">{{ item.phone }}</span>
            <span v-if="editIndex === index">
              <input
                class="form-control form-control-sm"
                v-model.number="item.phone"
              />
            </span>
          </td>
          <td>
            <span v-if="editIndex !== index">{{ item.email }}</span>
            <span v-if="editIndex === index">
              <input
                class="form-control form-control-sm"
                v-model.number="item.email"
              />
            </span>
          </td>
          <td>
            <div class="text-right">{{ subtotal(item) | money }}</div>
          </td>
          <td>
            <span v-if="editIndex !== index">
              <button
                @click="edit(item, index)"
                class="btn btn-raised btn-success mr-2"
              >
                Edit
              </button>
              <button
                @click="remove(item, index)"
                class="btn btn-raised btn-success mr-2"
              >
                Remove
              </button>
            </span>
            <span v-else>
              <button
                class="btn btn-raised btn-success mr-2"
                @click="cancel(item)"
              >
                Cancel
              </button>
              <button
                class="btn btn-raised btn-success mr-2"
                @click="save(item)"
              >
                Save
              </button>
            </span>
          </td>
        </tr>
      </tbody>
    </table>

    <div class="col-3 offset-9 text-right my-3">
      <button v-show="!editIndex" @click="add" class="btn btn-raised btn-success">
        Add item
      </button>
    </div>

    <div class="col-3 offset-9">
    </div>
  </div>
</template>
<script>
export default {
  name: "Uhuy",

  filters: {
    money: value =>
      new Intl.NumberFormat("id-ID", {
        style: "currency",
        currency: "IDR"
      }).format(value)
  },

  data() {
    return {
      editIndex: null,
      originalData: null,
      items: [
        {
          id: "1010",
          name: "John",
          father: "Jack",
          mother: "Lily",
          address: "edburgh",
          phone: "01727772300",
          email: "rbm@gmail.com"
        },
        {
          id: "1010",
          name: "Michael",
          father: "Cane",
          mother: "Susan",
          address: "Bristol",
          phone: "01727772340",
          email: "rbq@gmail.com"
        },
        {
          id: "1010",
          name: "Morris",
          father: "James",
          mother: "Natasha",
          address: "Asgard",
          phone: "01727772450",
          email: "rbsgm@gmail.com"
        },
        {
          id: "1010",
          name: "Malfoy",
          father: "Sam",
          mother: "Mave",
          address: "Alabama",
          phone: "01727772300",
          email: "berm@gmail.com"
        },
        {
          id: "1010",
          name: "Monty",
          father: "Anderson",
          mother: "Ammy",
          address: "south",
          phone: "01725552300",
          email: "rb44@gmail.com"
        },
        {
          id: "1010",
          name: "Neymar",
          father: "John Jr.",
          mother: "Leya",
          address: "pitsburgh",
          phone: "01727772300",
          email: "rbmqq@gmail.com"
        }
      ],
    };
  },

  methods: {
    add() {
      this.originalData = null;
      this.items.push({
        id: "",
        name: "",
        father: "",
        mother: "",
        address: "",
        phone: "",
        email: ""
      });
      this.editIndex = this.items.length - 1;
    },

    edit(item, index) {
      this.originalData = Object.assign({}, item);
      this.editIndex = index;
    },

    cancel(item) {
      this.editIndex = null;

      if (!this.originalData) {
        this.items.splice(this.items.indexOf(item), 1);
        return;
      }

      Object.assign(item, this.originalData);
      this.originalData = null;
    },

    remove(item, index) {
      this.items.splice(index, 1);
    },

    save(item) {
      this.originalData = null;
      this.editIndex = null;
    },

    subtotal(item) {
  
    }
  },

};
</script>

<style>
input[type="number"] {
  text-align: right;
}
</style>
