<script>
  import { useParams } from "svelte-navigator";
  import { getArticle, getComments, incVote } from "../utils/api";
  import CommentAdd from "./CommentAdd.svelte";
  const params = useParams();
  let articleId = $params.articleId;
  let article = {};
  let error = false;
  let loading = true;
  let votes;
  let voteErr = false;
  let viewComments = false;
  let commentErr = false;
  let comments = [];
  let addComment = true;
  let commentChange = false
  let commentAdded = false

  const handleVoteClick = () => {
    voteErr = false;
    votes = votes + 1;
    incVote("articles", articleId)
      .then((res) => {
        console.log(res);
      })
      .catch((err) => {
        voteErr = true;
        votes = votes - 1;
      });
  };

  const handleCommentClick = () => {
    commentErr = false;
    getComments(articleId)
      .then((res) => {
        comments = res;
      })
      .catch((err) => {
        commentErr = true;
      });
  };

  $: if (articleId !== 0) {
    error = false;
    loading = true;
    getArticle(articleId)
      .then((res) => {
        article = res;
        loading = false;
        votes = res.votes;
      })
      .catch((err) => (error = true));
  }
</script>

{#if error}
  <p class="errormessage">Article not found</p>
{:else if loading}
  <div class="spinner">
    <div class="lds-facebook">
      <div />
      <div />
      <div />
    </div>
  </div>
{:else}
  <section class="article__div">
    <p class="article--title">{article.title}</p>
    <p class="article--details">
      Topic: {article.topic} Author: {article.author}
    </p>
    <p class="article--details">
      Date posted:{" "}
      {`${new Date(article.created_at).getDate()}/${
        new Date(article.created_at).getMonth() + 1
      }/${new Date(article.created_at).getFullYear()}`}
    </p>
    <p>{article.body}</p>
    <button class="styledbutton" type="button" on:click|once={handleVoteClick}>
      Votes: {votes}
    </button>
    {#if voteErr}
      <p class="errormessage">Connection offline!</p>
    {/if}

    {#if viewComments}
      <button class="styledbutton" type="button" on:click={handleCommentClick}>
        Hide Comments
      </button>
    {:else}
      <button
        className="styledbutton"
        type="button"
        on:click={handleCommentClick}
      >
        Comments
      </button>
    {/if}
  </section>
{/if}

{#if addComment}
  <button
    class="styledbutton"
    on:click={() => {
      // setAddComment(true);
      // commentAdded.reset();
    }}
  >
    Add comment
  </button>
{/if}
{#if commentErr}
  <span>
    <br />
    <p class="errormessage comment">Offline!</p>
  </span>
{/if}

<CommentAdd bind:commentAdded bind:commentChange bind:articleId bind:addComment bind:viewComments />

<!-- <Comments
                article_id={article_id}
                setViewComments={setViewComments}
                viewComments={viewComments}
                commentChange={commentChange}
                setCommentChange={setCommentChange}
              />
               -->
