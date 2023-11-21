<template>
  <v-app>
    <!-- MAIN BAR -->
    <v-row>
      <v-app-bar elevation="0" color="primary">
        <v-col class="d-flex justify-center">
          <span class="material-symbols-outlined"> menu </span>
          <v-toolbar-title class="flex text-center">
            To-Do List
          </v-toolbar-title>
        </v-col>

        <!--DIALOG-->
        <v-dialog v-model="dialog" width="315">
          <template v-slot:activator="{ props }">
            <v-btn
              elevation="3"
              v-bind="props"
              @click="
                updateDialog = false;
                resetAddForm();
              "
            >
              <span class="material-symbols-outlined" style="font-size: 17px">
                add_circle </span
              >ADD
            </v-btn>
          </template>

          <v-form @submit.prevent="addItem" validate-on="submit">
            <v-card>
              <v-toolbar color="primary" v-if="updateDialog == false">
                <v-col class="d-flex">
                  <span class="material-symbols-outlined"> add_circle</span>
                  <v-toolbar-title><strong>Add Task</strong></v-toolbar-title>
                </v-col>
              </v-toolbar>
              <v-toolbar color="primary" v-if="updateDialog == true">
                <v-col class="d-flex">
                  <span class="material-symbols-outlined"> edit_square </span>
                  <v-toolbar-title>
                    <strong>Edit Task</strong>
                  </v-toolbar-title>
                </v-col>
              </v-toolbar>

              <v-card-text>
                <v-row>
                  <v-col cols="12">
                    <v-text-field
                      label="Title"
                      id="validate-title"
                      v-model="givenTitle"
                      variant="outlined"
                      :rules="titleRule"
                      v-if="updateDialog == false"
                    ></v-text-field>
                  </v-col>
                </v-row>

                <v-row>
                  <v-col cols="12">
                    <v-text-field
                      id="validate-description"
                      v-model="givenDescription"
                      variant="outlined"
                      label="Description"
                      :rules="descriptionRule"
                    ></v-text-field>
                  </v-col>
                </v-row>

                <!--Date Picker-->
                <v-row>
                  <v-col cols="12">
                    <v-menu
                      v-model="menu2"
                      :close-on-content-click="false"
                      :nudge-right="40"
                      lazy
                      transition="scale-transition"
                      offset-y
                      full-width
                    >
                      <template v-slot:activator="{ on }">
                        <v-text-field
                          type="text"
                          v-model="reformattedDate"
                          label="Deadline"
                          append-inner-icon="mdi-calendar"
                          readonly
                          variant="outlined"
                          v-on="on"
                          @click="menu2 = !menu2"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="givenDate"
                        no-title
                        color="primary"
                        @input="reformatDate"
                        @change="menu2 = false"
                      ></v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                <v-row>
                  <v-col cols="12">
                    <v-radio-group
                      v-model="givenPriority"
                      inline
                      off-icon="mdi-radiobox-blank"
                      on-icon="mdi-radiobox-marked"
                    >
                      <v-radio label="Low" value="low"></v-radio>
                      <v-radio label="Med" value="med"></v-radio>
                      <v-radio label="High" value="high"></v-radio>
                    </v-radio-group>
                  </v-col>
                </v-row>
              </v-card-text>
              <v-spacer></v-spacer>

              <v-col align="end">
                <v-btn
                  color="primary"
                  @click="addItem"
                  type="submit"
                  style="margin-right: 8px; width: 100px"
                  v-if="updateDialog == false"
                >
                  <span
                    class="material-symbols-outlined"
                    style="font-size: 18px"
                  >
                    add_circle
                  </span>
                  ADD
                </v-btn>
                <v-btn
                  v-if="updateDialog == true"
                  color="primary"
                  @click="editItem"
                  type="submit"
                  style="margin-right: 8px; width: 100px"
                >
                  <span
                    class="material-symbols-outlined"
                    style="font-size: 18px"
                  >
                    edit_square
                  </span>
                  Edit
                </v-btn>

                <v-btn color="red" @click="dialog = false" style="width: 100px">
                  <span
                    class="material-symbols-outlined"
                    style="font-size: 18px"
                  >
                    block
                  </span>
                  CANCEL
                </v-btn>
              </v-col>
            </v-card>
          </v-form>
        </v-dialog>
      </v-app-bar>
    </v-row>

    <!-- TABLE -->
    <v-row>
      <v-col cols="12">
        <v-table fixed-header height="560">
          <thead>
            <tr>
              <th class="text-center">Title</th>
              <th class="text-center">Description</th>
              <th class="text-center">Deadline</th>
              <th class="text-center">Priority</th>
              <th class="text-center">Is Complete</th>
              <th class="text-center">Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, index) in items" :key="item.Title">
              <td class="text-center">{{ item.Title }}</td>
              <td class="text-center">{{ item.Description }}</td>
              <td class="text-center">{{ item.Deadline }}</td>
              <td class="text-center">{{ item.Priority }}</td>
              <td class="text-center">
                <v-checkbox
                  v-model="item.isComplete"
                  @click="removeUpdateButton()"
                  style="
                    display: flex;
                    align-items: center;
                    justify-content: center;
                  "
                ></v-checkbox>
              </td>

              <td class="justify-center text-center">
                <v-col
                  cols="12"
                  style="
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    flex-direction: column;
                  "
                >
                  <v-btn
                    color="primary"
                    size="small"
                    @click="
                      updateDialog = true;
                      dialog = true;
                      populateUpdateItem(item);
                    "
                    v-if="!item.isComplete"
                    v-bind="props"
                  >
                    <span
                      class="material-symbols-outlined"
                      style="font-size: 18px"
                    >
                      edit_square
                    </span>
                    Update
                  </v-btn>

                  <v-btn color="red" size="small" @click="deleteItem(index)">
                    <span
                      class="material-symbols-outlined"
                      style="font-size: 18px"
                    >
                      cancel
                    </span>

                    Delete
                  </v-btn>
                </v-col>
              </td>
            </tr>
          </tbody>
        </v-table>
      </v-col>
    </v-row>
  </v-app>
</template>

<script>
import { ref } from 'vue';
import Dialog from './Dialog.vue';

export default {
  components: {
    Dialog,
  },
  data() {
    return {
      menu2: false,
      dialog: false,
      updateDialog: false, // Add this line
      givenPriority: 'low', // Initialize the variable with a default
      givenTitle: '',
      givenDescription: '',
      givenDate: null,
      reformattedDate: moment().format('MM/DD/YYYY'),

      titleRule: [
        (value) => {
          if (value) {
            // Check for uniqueness
            const isUnique = !this.items.some((item) => item.Title === value);
            // Return true if the title is unique, otherwise return an error message
            return isUnique || 'Title must be unique';
          }
          return 'Title is Required!';
        },
      ],
      descriptionRule: [
        (value) => {
          if (value) return true;
          return 'Description is Required!';
        },
      ],

      items: [],
    };
  },
  methods: {
    initDate() {
      this.reformattedDate = moment().format('MM/DD/YYYY');
    },

    reformatDate() {
      this.reformattedDate = moment(this.givenDate).format('MM/DD/YYYY');
    },

    resetAddForm() {
      // Reset input values
      this.givenTitle = '';
      this.givenDescription = '';
      this.givenPriority = 'low';
      this.givenDate = null;
      this.reformattedDate = moment().format('MM/DD/YYYY');
    },

    addItem() {
      // validate for empty
      if (this.givenTitle == '' || this.givenDescription == '') return;

      // validate for uniqueness
      const isTitleValid = this.titleRule[0](this.givenTitle);
      if (isTitleValid !== true) return;

      // if all validation passes then we can add the new entry
      const newItem = {
        Title: this.givenTitle,
        Description: this.givenDescription,
        Deadline: this.reformattedDate,
        Priority: this.givenPriority,
        isComplete: false,
      };

      //Add new entry to table and close dialog
      this.items.push(newItem);
      this.dialog = false;

      // Reset input values
      this.givenTitle = '';
      this.givenDescription = '';
      this.givenPriority = 'low';
      this.givenDate = null;

      // display toaster
      toastr.options.positionClass = 'toast-bottom-right';
      toastr.success('Task was Successfully Added');
    },

    deleteItem(index) {
      this.items.splice(index, 1);
      toastr.options.positionClass = 'toast-bottom-right';
      toastr.success('Task was successfully deleted');
    },

    populateUpdateItem(item) {
      // Set the values for the dialog based on the selected item
      this.givenTitle = item.Title;
      this.givenDescription = item.Description;
      this.reformattedDate = item.Deadline;
      this.givenPriority = item.Priority;
    },

    editItem() {
      //find the index of the given item
      //const index = items.indexOf(givenTitle);
      const index = this.items.findIndex(
        (item) => item.Title === this.givenTitle
      );

      // Update the item with the new values
      this.items[index].Description = this.givenDescription;
      this.items[index].Deadline = this.reformattedDate;
      this.items[index].Priority = this.givenPriority;

      // Reset the form and close the dialog
      this.resetAddForm();
      this.dialog = false;

      // Display toaster
      toastr.options.positionClass = 'toast-bottom-right';
      toastr.success('Task was successfully updated');
    },
  },
  watch: {
    // Watch for changes in givenDate and format it when it changes
    givenDate: {
      handler: 'reformatDate',
      immediate: true, // Format initially as well
    },
  },
};
</script>

<style></style>
