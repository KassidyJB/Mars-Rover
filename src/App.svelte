<script>
  import { Router, Route } from "svelte-routing";
  import About from "./routes/About.svelte";
  import Rovers from "./routes/Search.svelte";
  import LearnMore from "./routes/LearnMore.svelte";
</script>

<Router>
  <nav>
    <a href="/About">About</a>
    <a href="/Rovers">Photo Search</a>
    <a href="/LearnMore">Learn More</a>
  </nav>

  <div>
    <Route path="/About" component={About} />
    <Route path="/Rovers" component={Rovers} />
    <Route path="/LearnMore" component={LearnMore} />
  </div>
</Router>

<main>
  <h1>Welcome to the Mars Rover Project!</h1>

  <div>
  <p><a href= "/About">+About</a>  /  <a href= "/Search">+Photo Search</a>  /   <a href= "/LearnMore">+Learn More</p>
  </div>

  <p class="read-the-docs">
  This is the Home page. 
  Click one of the tab options above for more!
  </p>
</main>


