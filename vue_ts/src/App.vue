<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js + aTypeScript App"/> -->
    <BlogPost v-for="(posts, idx) in bolgPosts" :idxData = "idx" :post="posts" :key="idx" @delEmit="testEmit"/>
    <div class="wrap_btn">
      <input type="text" v-model="titleValue" placeholder="제목">
      <input type="text" v-model="nameValue" placeholder="이름">
      <input type="text" v-model="brithValue" placeholder="생년월일 예시 2019. 1. 6">
      <button type="button" @click="addEvent">추가</button>
    </div>
  </div>
  
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
// import HelloWorld from './components/HelloWorld.vue';
import BlogPost, { IPost } from './components/BlogPost.vue';


@Component({
  components: {
    // HelloWorld,
    BlogPost
  },
})
export default class App extends Vue {
  private testArr: Array<number> = [1,2,3,4,5]
  private titleValue: string = '';
  private nameValue: string = '';
  private brithValue: string = '';
  private bolgPosts: IPost[] = [
		{
			title: 'Look I am blogging!',
			author: 'Edward',
			datePosted: new Date(2019, 1, 6)
		},
  ];
  private text: string = 'abc';

  mounted() {
    console.log(this.bolgPosts)
    console.log(this.testArr.splice(1, 1))
  }

  public testEmit(id: number): void {
    console.log('id', id);
    
    this.bolgPosts.splice(id, 1);
    console.log(this.bolgPosts)
  }

  public addEvent(): void {
    if(this.titleValue.length > 0 && this.nameValue.length > 0 && this.brithValue.length > 0){

      // interface IAddType {
      //   title: string;
      //   author: string;
      //   datePosted: Date;
      // }
      interface IObjPost {
        [key:string]: any
      }
      const objAdd:IObjPost = {};
      const dateArr:Array<string> = this.brithValue.split('.');
      console.log(dateArr);
      objAdd.title = this.titleValue;
      objAdd.author = this.nameValue;
      objAdd.datePosted = new Date(Number(dateArr[0]), Number(dateArr[1]), Number(dateArr[2]));
      this.bolgPosts.push(objAdd as IPost);

      this.titleValue = '';
      this.nameValue = '';
      this.brithValue = '';

    } else {
      alert('입력을 잘못했습니다.');
    }
   

  }
  
 
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.wrap_btn{
  margin:50px 0
}
</style>
