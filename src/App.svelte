<script>
  import { Router, Route } from "svelte-routing";
  import LearnMore from "./routes/LearnMore.svelte";
  import About from "./routes/About.svelte";
  import Rovers from "./routes/Rovers.svelte";
</script>

<Router>
  <nav>
    <a href="/Learn More">Learn More</a>
    <a href="/About">About</a>
    <a href="/Search">Photo Search</a>

  </nav>

  <div>
    <Route path="/LearnMore" component={LearnMore} />
    <Route path="/About" component={About} />
    <Route path="/Rovers" component={Rovers} />
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

