<script>
  import { user } from "../stores";

  import { postComments } from "../utils/api";

  export let addComment;
  export let articleId;
  export let viewComments;
  export let commentChange;
  export let commentAdded;

  let userValue;
  user.subscribe((value) => {
    console.log(value);
    userValue = value;
  });

  let newCommentInput = "";
  let charactersLeftInForm = 200;
  let err = false;

  //   const { user } = useContext(UserContext);

  const handleCommentSubmit = (e) => {
    err = false;
    postComments(newCommentInput, userValue, articleId)
      .then(() => {
        newCommentInput = "";
        commentChange = true;
        commentAdded.loading(true);
        viewComments = true;
      })
      .catch((error) => {
        err = true;
        console.log(err);
      });
  };
</script>

<div>
  {#if addComment}
    <form class="comment--form" on:submit|preventDefault={handleCommentSubmit}>
      <label for="comment" />
      <textarea
        required
        placeholder="max 200 chars"
        value={newCommentInput}
        type="text"
        maxLength="200"
        id="comment"
        name="comment"
        on:change={(e) => {
          newCommentInput = e.target.value;
          charactersLeftInForm = 200 - e.target.value.length;
        }}
      />
      <button
        class="styledbutton"
        on:click={(e) => {
          newCommentInput = "";
          charactersLeftInForm = 200;
          err = false;
        }}>Clear</button
      >
      <button
        type="button"
        class="styledbutton"
        on:click={() => {
          addComment = !addComment;
          charactersLeftInForm = 200;
          err = false;
        }}
      >
        Hide
      </button>
      <button class="comment--submit styledbutton">Submit</button>
      <!-- <span>
        {charactersLeftInForm <= 25 ? <span className="charsleft red">{charactersLeftInForm} characters left</span> : null}
        {charactersLeftInForm <= 50 && charactersLeftInForm >25 ? <span className="charsleft amber">{charactersLeftInForm} characters left</span> : null}
        {charactersLeftInForm < 200 && charactersLeftInForm >50 ? <span className="charsleft green">{charactersLeftInForm} characters left</span> : null}
        </span> -->
    </form>
  {/if}
</div>

<!-- {addingComment.on && !err ?<p className="uploading">Uploading comment...</p> : null}
      {commentAdded.on? <p className="success">Success!</p>: null}
      {err ? (
        <p className="errormessage">{err}</p>
      ) : null}
     -->
