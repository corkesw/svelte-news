<script>
  import { Link } from "svelte-navigator";

  import { getArticles } from "../utils/api";

  export let topic;
  export let sortBy;
  export let order;
  export let page;

  let articles = [];
  $: console.log(articles);
  $: console.log(order)

  $: if (topic !== "" || sortBy !== "" || order !== "" || page !== "") {
    getArticles({ topic, sortBy, order, page })
      .then((res) => {
        articles = res.articles;
      })
      .catch((err) => console.log(err));
  }
</script>

<p class="sortby">
  Sort :
  <button
    class={`sortauthor ${sortBy} styledbutton`}
    type="button"
    on:click={() => {
      sortBy = "author";
      page = 1;
    }}
  >
    Author
  </button>
  <button
    class={`sortcreated_at ${sortBy} styledbutton`}
    type="button"
    on:click={() => {
        sortBy = "created_at";
        page = 1;
      }}
  >
    Date
  </button>
  <button
    class={`sorttitle ${sortBy} styledbutton`}
    type="button"
    on:click={() => {
        sortBy = "title";
        page = 1;
      }}
  >
    Title
  </button>
  {#if !topic}
    <button
      class={`sorttopic ${sortBy} styledbutton`}
      type="button"
      on:click={() => {
        sortBy = "topic";
        page = 1;
      }}
    >
      Topic
    </button>
  {/if}
  <button
    class={`sortvotes ${sortBy} styledbutton`}
    type="button"
    on:click={() => {
        sortBy = "votes";
        page = 1;
      }}
  >
    Votes
  </button>
  <button
    class={`sortcomment_count ${sortBy} styledbutton`}
    type="button"
    on:click={() => {
        sortBy = "comment_count";
        page = 1;
      }}
  >
    Comments
  </button>
  <span class="order__span">
    Order:
    {#if order === "desc"}
      <button
        class="order__button"
        type="button"
        on:click={() => {
            order = "asc";
          }}
      >
        Desc
      </button>
    {:else}
      <button
        class="order__button"
        type="button"
        on:click={() => {
            order = "desc";
          }}
      >
        Asc
      </button>
    {/if}
  </span>
</p>

<div>
  <p>Articles</p>
  {#each articles as article}
    <Link class="article--link" to={`/article/${article.article_id}`}>
      <div class="article__div">
        <p class={`article--title ${article.topic}`}>
          {article.title}
        </p>
        <p class="article--details">
          Topic: {article.topic.toUpperCase()} Author:{" "}
          {article.author}{" "}
        </p>
        <p class="article--details">
          Date posted:{" "}
          {`${new Date(article.created_at).getDate()}/${
            new Date(article.created_at).getMonth() + 1
          }/${new Date(article.created_at).getFullYear()}`}
          <span class="desktop">
            {" "}
            Votes: {article.votes} Comments: {article.comment_count}
          </span>
        </p>
      </div>
    </Link>
  {/each}
</div>

<style>
  .articles {
    /* background-color: #094074; */
    padding-top: 1px;
  }

  .article__div {
    border: 2px solid black;
    border-radius: 10px;
    padding: 3px;
    margin: 4px auto;
    background-color: #fbfbfb;
    color: black;
    width: 85vw;
    text-decoration: none;
  }

  .centre {
    text-align: center;
  }

  p.article--title {
    font-size: large;
    font-weight: bold;
    text-decoration: none;
    padding: 5px 0px;
    margin: 2px auto;
  }

  /* .cooking {
  background-color: rgb(241, 255, 241);
}

.coding {
  background-color: rgb(232, 239, 241);
}

.football {
  background-color: rgb(248, 231, 234);
} */

  p.article--details {
    font-size: small;
    margin: 0px 0px 5px 0px;
  }

  .article--link:link {
    text-decoration: none;
    color: green;
  }

  .article--link:visited {
    text-decoration: none;
    color: red;
  }

  .article--link .article__div:hover {
    color: #dc851f;
    background-color: #6a687a;
  }

  div .comment {
    padding: 0px;
    margin: 0px;
  }

  .comment--form {
    padding: 0px;
    margin: 0px;
  }

  #comment {
    word-wrap: break-word;
    word-break: break-all;
    height: 80px;
    width: 83.8vw;
    margin: auto;
    position: relative;
    left: 0px;
  }

  .charsleft {
    margin-left: 5px;
  }
  .charsleft.amber {
    font-size: 0.7rem;
    background-color: orangered;
    color: white;
  }

  .charsleft.green {
    font-size: 0.7rem;
  }

  .charsleft.red {
    font-size: 0.7rem;
    background-color: red;
    color: white;
  }

  .sortby {
    color: white;
    display: flex;
    flex-wrap: wrap;
    width: 75vw;
    margin: auto;
    margin-top: 10px;
    margin-bottom: 5px;
    align-items: center;
    justify-content: space-between;
  }

  .sortby button {
    margin: 0px, 5px;
    padding: 2px;
  }

  .order__span {
    align-items: center;
  }

  @media screen and (min-width: 600px) {
    .sortby {
      height: 2rem;
      display: block;
      width: 85vw;
      margin: 0px auto;
      margin-top: 10px;
      margin-bottom: 5px;
      align-items: center;
      justify-content: left;
    }

    .sortby button {
      padding: 2px;
    }

    .order__span {
      margin-left: 25px;
    }
  }

  .sortauthor.author,
  .sortcreated_at.created_at,
  .sorttitle.title,
  .sorttopic.topic,
  .sortvotes.votes,
  .sortcomment_count.comment_count,
  .order__button {
    background: linear-gradient(
      to bottom,
      rgb(9, 4, 170) 5%,
      rgb(9, 4, 170) 100%
    );
    background-color: rgb(9, 4, 170);
    box-shadow: inset 0px -3px 7px 0px rgb(9, 4, 170);
    color: white;
  }

  .order__button {
    border: 1px solid #0b0e07;
    display: inline-block;
    cursor: pointer;
    color: #ffffff;
    font-size: 15px;
    padding: 2px;
    margin: 0px;
    text-decoration: none;
    text-shadow: 0px 1px 0px #263666;
  }

  .pagination {
    margin: 15px auto;
    width: 50vw;
    color: white;
  }

  .pagination button {
    margin: 0px, 5px;
    padding: 2px;
  }

  .deletedtrue {
    color: red;
  }
  /* AddArticle.jsx */

  .article__form {
    display: grid;
    grid-template-columns: 20vw 65vw;
    grid-template-rows: 2rem 2rem 30rem;
    grid-template-areas:
      "topiclabel topicinput"
      "titlelabel titleinput"
      "articlelabel articleinput"
      "addarticlespacer articlesubmit";
  }

  .topiclabel {
    grid-area: topiclabel;
    margin: 5px;
  }

  .topicinput {
    grid-area: topicinput;
    margin: 5px;
  }

  .input-with-hint {
    height: 2rem;
    width: 40vw;
  }
  .titlelabel {
    grid-area: titlelabel;
    margin: 5px;
  }

  .titleinput {
    grid-area: titleinput;
    width: 60vw;
  }
  .articlelabel {
    grid-area: articlelabel;
    margin: 5px;
  }

  .articleinput {
    grid-area: articleinput;
    width: 60vw;
  }

  .addarticlespacer {
    grid-area: addarticlespacer;
  }

  .articlesubmit {
    width: 60px;
    grid-area: articlesubmit;
  }

  .nologin {
    text-decoration: none;
  }
</style>
