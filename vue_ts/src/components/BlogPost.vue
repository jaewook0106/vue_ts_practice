<template>
  <div class="blogpost">
    <h2>{{ post.title }}</h2>
    <p>{{ post.author }}</p>
    <p class="meta">{{ dateSet }}</p>
    <button type="button" @click="delEvent(idxData)">삭제</button>
  </div>
</template>

<script lang = "ts">
import { Component, Prop, Vue, Emit } from 'vue-property-decorator';

export interface Post {
  title: string;
  author: string;
  datePosted: Date;
}

@Component
export default class BlogPost extends Vue {
  @Prop() private post!: Post;
  @Prop() private idxData!: number;
  //comeputed
  get dateSet(): string {
    return `${this.post.datePosted.getFullYear()} / ${this.post.datePosted.getMonth()} / ${this.post.datePosted.getDate()}`;
  }

  //method
  @Emit('delEmit')
  public delEvent(idxData: number): void {
  }
}


</script>

<style lang="scss" scoped>
div.blogpost {
	h2 {
		text-decoration: underline;
	}
	p.meta {
		font-style: italic;
	}
}
 
</style>
