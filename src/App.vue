<template>
   <!-- Content -->
   <div class="px-3 py-10 md:px-10 pt-16">
      <div class="w-full sm:w-1/2 lg:w-1/3 mx-auto">
         <!-- Todo spinner -->
         <TodoSpinner v-if="loading" />

         <template v-else>
            <!-- Todo form -->
            <TodoForm />

            <!-- Todo items -->
            <TodoItems v-if="$store.state.todos.length" />

            <!-- Todo empty -->
            <TodoEmpty v-else />
         </template>
      </div>
   </div>
   <!--/ Content -->
</template>

<script>
import TodoItems from "@/components/TodoItems.vue";
import TodoForm from "@/components/TodoForm.vue";
import TodoSpinner from "@/components/TodoSpinner.vue";
// import TodoItem from '@/components/TodoItem.vue';
import TodoEmpty from "@/components/TodoEmpty.vue";

export default {
   name: "App",

   components: {
      TodoSpinner,
      TodoItems,
      TodoForm,
      // TodoItem,
      TodoEmpty,
   },

   data() {
      return {
         loading: false,
      };
   },

   created() {
      this.loading = true
      this.$store.dispatch('getTodos').finally(() => {
         this.loading = false
      })
   },
};
</script>
