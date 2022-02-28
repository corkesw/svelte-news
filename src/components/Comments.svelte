<script>
  import Comment from "./Comment.svelte";
  import { onMount } from "svelte";

  import { user } from "../stores";

  import { getComments } from "../utils/api";
  export let articleId;
  export let viewComments;
  export let commentChange;

  let userValue;
  user.subscribe((value) => {
    userValue = value;
  });

  let err = false;
  let comments = [];

  $: console.log(articleId);
  $: console.log(viewComments, comments);

  onMount(() => {
    console.log("opants");
    commentChange = false;
    err = false;
    getComments(articleId)
      .then((res) => {
        comments = res;
        console.log(comments);
      })
      .catch((error) => {
        viewComments = false;
        err = true;
      });
  });
</script>

<div>
  {#if err && viewComments}
    <p class="errormessage">{err}</p>
  {/if}

  {#if viewComments && comments.length > 0}
    {#each comments as comment}
      <div class="comment" key={comment.comment_id}>
        <p>{comment.body}</p>
        <p class="article--details">by {comment.author}</p>
        <p class="article--details">
          on{" "}
          {`${new Date(comment.created_at).getDate()}/${
            new Date(comment.created_at).getMonth() + 1
          }/${new Date(comment.created_at).getFullYear()}`}
        </p>
        <Comment
          bind:commentChange
          bind:userValue
          {comment}
          bind:viewComments
        />
        <hr />
      </div>
    {/each}
  {/if}

  <p>comments@@@</p>
</div>

<style>
  .comment {
    color: white;
  }
</style>
