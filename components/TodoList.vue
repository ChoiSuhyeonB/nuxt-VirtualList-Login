<template>
  <section>
    <!-- <ul v-if="$store.state.items">
      <li v-for="(todoItem, index) in $store.state.items" :key="index">
        <i class="checkBtn fas fa-check" aria-hidden="true"></i>
        {{ todoItem.name }}
        <span
          class="removeBtn"
          type="Button"
          @click="removeTodo(todoItem.id, index)"
        >
          <i class="far fa-trash-alt" aria-hidden="true"></i>
        </span>
      </li>
    </ul> -->

    <!-- <infinite-loading
      spinner="spiral"
      @infinite="infiniteScroll"
    ></infinite-loading> -->

    <RecycleScroller
      class="scroller"
      page-mode
      v-if="$store.state.items"
      :items="this.$store.state.items"
      :item-size="30"
      v-slot="{ item }"
      key-field="id"
    >
      <div class="list">
        {{ item.name }}
        <span class="removeBtn" type="Button" @click="removeTodo(item.id)">
          <i class="far fa-trash-alt" aria-hidden="true"></i>
        </span>
      </div>
    </RecycleScroller>
  </section>
</template>

<script lang="ts">
import { Component, Vue, Prop, Emit } from "nuxt-property-decorator";

//@ts-ignore
// import VueVirtualScroller from "vue-virtual-scroller";
// import { RecycleScroller } from "vue-virtual-scroller";
// @Component({
//   components: {
//     RecycleScroller
//   }
// })
@Component
export default class TodoList extends Vue {
  //props:['propsdata']

  //@Prop() propsdata: string[] | undefined;
  //@Prop() page: any | undefined;
  //임시 배열 변수 Data입니다.
  Data: string[] = [""];
  //computed
  get url() {
    // return "/api/todolist/" + this.$store.state.page;
    return "/api/todolist/";
  }
  // public async infiniteScroll($state: {
  //   loaded: () => void;
  //   complete: () => void;
  // }) {
  //   setTimeout(async => {
  //     //this.page = this.page + 10;
  //     this.$store.commit("changePage", this.$store.state.page + 10);
  //     this.Data = [];
  //     this.$axios
  //       .get(this.url)
  //       .then(res => {
  //         if (res && res.data.length > 1) {
  //           res.data.forEach((todoItem: any) => this.Data.push(todoItem));
  //           this.Data.forEach((todoItem: any) =>
  //             this.$store.commit("pushTodoItems", todoItem)
  //           );

  //           $state.loaded();
  //         } else {
  //           $state.complete();
  //         }
  //       })
  //       .catch(err => {
  //         console.log(err);
  //       });
  //   }, 1000);
  // }

  public removeTodo(todoItem: string): void {
    this.$emit("removeTodo", todoItem);
  }
}
</script>

<style scoped>
ul {
  /* 리스트에 점을 없애준다. */
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
  margin-left: 10px;
}
li {
  display: flex;
  min-height: 30px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 20px;
}
.checkBtn {
  line-height: 45px;
  color: rgb(7, 177, 126);
  margin-left: 30px;
  margin-right: 70px;
}
.removeBtn {
  color: rgb(245, 9, 213);
  margin-left: 10px;
}

/* vue-virtual-scroller css */
.scroller {
  height: 100%;
  width: 50%;
  margin-left: auto;
  margin-right: auto;
  background: lightcyan;
  margin-top: 20px;
  margin-bottom: 20px;
  padding: 1px;
  font-size: 1rem;
  display: flex;
  border-radius: 10px;
}

.list {
  width: 100%;
  border-radius: 10px;
  margin: 0;
  padding-right: 40px;
  background: white;
}
.list:hover {
  background: rgb(235, 231, 231);
}
</style>
