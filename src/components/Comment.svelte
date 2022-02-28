<script>
  import { incVote, deleteComment } from "../utils/api";
  export let commentChange;
  export let userValue;
  export let comment;
  export let viewComments;

  let err = false;
  let isDeleted = false;

  const handleClick = () => {
    comment.votes++;
    err = false;
    incVote("comments", comment.comment_id).catch((error) => {
      comment.votes--;
      err = true;
    });
  };

  const handleDelete = () => {
    err = false;
    deleteComment(comment_id)
      .then(() => {
        isDeleted = true;
        commentChange = true;
      })
      .catch((error) => {
        err = true;
      });
  };
</script>

<div class={`deleted${isDeleted}`}>
  <button disabled={isDeleted === true} on:click|once={handleClick} type="button">
    Votes: {comment.votes}
  </button>
  <button
    disabled={isDeleted === true}
    on:click={() => {
      viewComments = false;
    }}
  >
    Hide comments
  </button>
  {#if comment.author === userValue}
    <button disabled={isDeleted === true} type="button" onClick={handleDelete}>
      Delete
    </button>
  {/if}
  {#if err}
    <span
      ><br />
      <p class="errormessage">Connection error, please try again later</p></span
    >
  {/if}
  {#if isDeleted}
    <p>Deleting...</p>
  {/if}
</div>
