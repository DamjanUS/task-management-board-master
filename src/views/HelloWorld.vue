<template>
  <div class="hello">
    <draggable class="flex" v-model="taskCategories">
      <taskCategory
        v-for="category in taskCategories"
        :key="category.id"
        :category="category"
        @input="
          (event) => {
            category.tasks = event;
          }
        "
      >
      </taskCategory>
    </draggable>
    <PButton style="padding: 5px; border: 2px solid black;" @click="storeData()">Storage</PButton>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import taskCategory from '@/components/taskCategory.vue'
import PButton from '@/components/PButton.vue'

export default {
  mounted(){
    const myJSONTwo = JSON.parse(localStorage.getItem('storeArray1'))
    if(myJSONTwo == null) return;
    this.taskCategories = myJSONTwo
    
  },
  data() {
    return {
      available: true,
      taskCategories: [
        {
          id: 1,
          name: "categoryOne",
          tasks: [
            {
              id: 1,
              title: "January",
              description: "workmonth1",
              completed: false,
              dueDate: new Date(2024, 12, 21, 7, 15),
            },
          ],
        },
        {
          id: 2,
          name: "categoryTwo",
          tasks: [
            {
              id: 2,
              title: "February",
              description: "workmonth2",
              completed: false,
              dueDate: new Date(2024, 9, 17, 11, 25),
            },
            {
              id: 3,
              title: "March",
              description: "workmonth3",
              completed: false,
              dueDate: new Date(2023, 8, 21, 21, 55),
            },
          ],
        },
        {
          id: 3,
          name: "categoryThree",
          tasks: [
            {
              id: 3,
              title: "April",
              description: "workmonth3",
              completed: false,
              dueDate: new Date(2025, 8, 19, 19, 55),
            },
          ],
        },
      ],
    };
  },
  name: "HelloWorld",
  props: {
    msg: String,
  },
  methods: {
    storeData() {
      const myJSON = JSON.stringify(this.taskCategories)  
      localStorage.setItem("storeArray1",myJSON)
    }
  },
  components: {
    draggable,
    taskCategory,
    PButton
  },
};
</script>


<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.flex {
  display: flex;
  flex-direction: row;
}
</style>
