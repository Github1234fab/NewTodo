<script>
  import { auth } from "../lib/firebase.js";
  
  async function handleSignOut() {
    try {
      await auth.signOut();
      console.log("User signed out");
      window.location.href = "/SeeYouLater";
    } catch (error) {
      console.error("Error signing out: ", error);
    }
  }
</script>

<header>
        <h1>ToDo</h1>
        <nav>
                <ul>
                        <li><a href="/Signin">Sign in</a></li>
                        <li><a href="/Signup">Sign up</a></li>
                        <button on:click={handleSignOut}>log out</button>
                </ul>
        </nav>
</header>

<style>
        header {
                display: flex;
                justify-content: space-between;
                align-items: center;
                padding: 1rem;
                background-color: #333;
                color: white;
                
        }

        nav ul {
                display: flex;
                list-style: none;
        }

        nav ul li {
                margin-left: 1rem;
        }

        nav ul li a {
                color: white;
                text-decoration: none;
        }
</style>
