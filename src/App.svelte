<script>
  import { Router, Link, Route } from "svelte-navigator";
  import Articles from "./components/Articles.svelte";
  import Article from "./components/Article.svelte";
  import Header from "./components/Header.svelte";
  import Nav from "./components/Nav.svelte";
  import Login from "./components/Login.svelte";
  import { user } from "./stores";
  let topic;
  let sortBy = "title";
  let order = "asc";
  let page = 1;

  let userValue;
  user.subscribe((value) => {
    console.log(value);
    userValue = value;
  });
</script>

<Router primary={false}>
  <Header />
  <Nav />

  <main>
    <Route path="/articles">
      <Articles bind:topic bind:sortBy bind:order bind:page />
    </Route>
    <Route path="/">
      <Articles bind:topic bind:sortBy bind:order bind:page />
    </Route>
    <Route path="articles/:chosenTopic" let:params>
      <Articles chosenTopic={params.chosenTopic} />
    </Route>
    <Route path="article/:articleId" let:params>
      <Article articleId={params.articleId} />
    </Route>
    <Route path="/login"><Login /></Route>
  </main>
</Router>

<style>
 :global(body){
  margin: 0;
  font-family: 'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

:global(code) {
  font-family: source-code-pro, Menlo, Monaco, Consolas, 'Courier New',
    monospace;
}


:global(body) {
  background-color: #000000;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100%25' height='100%25' viewBox='0 0 1600 800'%3E%3Cg %3E%3Cpolygon fill='%23020122' points='1600 160 0 460 0 350 1600 50'/%3E%3Cpolygon fill='%23040244' points='1600 260 0 560 0 450 1600 150'/%3E%3Cpolygon fill='%23050266' points='1600 360 0 660 0 550 1600 250'/%3E%3Cpolygon fill='%23070388' points='1600 460 0 760 0 650 1600 350'/%3E%3Cpolygon fill='%230904AA' points='1600 800 0 800 0 750 1600 450'/%3E%3C/g%3E%3C/svg%3E");
  background-attachment: fixed;
  background-size: cover;
}

:global(.errormessage) {
  background-color: red;
  color: white;
  display: inline;
  font-size: 0.7rem;
}

:global(.errormessage.comment ){
  display: inline-block;
}

:global(:global){
  font-size: 1rem;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  padding: 10px;
}

:global(.uploading ){
  background-color: orangered;
  color: white;
  display: inline;
  font-size: 0.7rem;
}

:global(.success ){
  background-color: green;
  color: white;
  display: inline;
  font-size: 0.7rem;
}

/* Spinner */

.spinner {
  margin: 0px auto 0px auto;
  width: 25vw;
}

.artilcesspinner {
  z-index: 1 !important;
}

.lds-facebook {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-facebook div {
  display: inline-block;
  position: absolute;
  left: 8px;
  width: 16px;
  background: #fff;
  animation: lds-facebook 1.2s cubic-bezier(0, 0.5, 0.5, 1) infinite;
}
.lds-facebook div:nth-child(1) {
  left: 8px;
  animation-delay: -0.24s;
}
.lds-facebook div:nth-child(2) {
  left: 32px;
  animation-delay: -0.12s;
}
.lds-facebook div:nth-child(3) {
  left: 56px;
  animation-delay: 0;
}
@keyframes lds-facebook {
  0% {
    top: 8px;
    height: 64px;
  }
  50%,
  100% {
    top: 24px;
    height: 32px;
  }
}

/* media queries */

@media screen and (min-width:600px) {
  .applayout {
    display: grid;
    grid-template-columns: 150px auto;
    grid-template-rows: 60px 40px auto;
    grid-template-areas: 
      "appheader appheader"
      "appnav appnav"
      "appmain appmain";
  }

  .appheader {
    grid-area: appheader;
  }

  .appnav {
    grid-area:appnav;
  }

  .appmenu {
    grid-area: appmenu;
  }

  .appmain {
    grid-area: appmain;
  }

  }

  @media screen and (max-width: 600px) {
  
    /* The side navigation menu */
  .sidenav {
      color: white;
      height: 100%; /* 100% Full-height */
      width: 0; /* 0 width - change this with JavaScript */
      position: fixed; /* Stay in place */
      z-index: 1; /* Stay on top */
      top: 0; /* Stay at the top */
      left: 0;
      background-color: rgb(10,4,167); /* Black*/
      opacity: 97%;
      overflow-x: hidden; /* Disable horizontal scroll */
      padding-top: 60px; /* Place content 60px from the top */
      transition: 0.5s; /* 0.5 second transition effect to slide in the sidenav */
    }
  
    /* The navigation menu links */
  .sidenav a {
      padding: 8px 8px 8px 32px;
      text-decoration: none;
      display: block;
      transition: 0.3s;
    }
  
    .menuopentrue {
      width: 40%;
    }
  
    .closemenu {
      position: relative;
      top: -30px;
      left: 20px;
    }
  }

@media screen and (max-width:600px) {
  .desktop {
    display:none;
  }
  
}

.styledbutton {
	box-shadow:inset 0px -3px 7px 0px #29bbff;
	background:linear-gradient(to bottom, #2dabf9 5%, #0688fa 100%);
	background-color:#2dabf9;
	border-radius:3px;
	border:1px solid #0b0e07;
	display:inline-block;
	cursor:pointer;
	color:#ffffff;
	font-size:15px;
	padding:2px;
  margin: 0px;
	text-decoration:none;
	text-shadow:0px 1px 0px #263666;
}
.styledbutton:hover {
	background:linear-gradient(to bottom, #0688fa 5%, #2dabf9 100%);
	background-color:#0688fa;
}
/* button:active {
	position:relative;
	top:1px;
} */

.styledbutton:disabled {
  box-shadow:inset 0px -3px 7px 0px #7f8181;
	background:linear-gradient(to bottom, #7f8181 5%, #d2d5d8 100%);
	background-color:#363738;
	border-radius:3px;
	border:1px solid #0b0e07;
	display:inline-block;
	cursor:pointer;
	color:#4b4a61;
	font-family:Arial;
	font-size:15px;
	padding:2px;
  margin: 0px;
	text-decoration:none;
	text-shadow:0px 1px 0px #263666;
}
</style>
