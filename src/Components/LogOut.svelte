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
<section class="header">
        <a class="home-link" href="/">ToDo</a>
  
<button on:click={handleSignOut}>log out</button>
</section>



<style>
.header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 1rem;
        background-color: navy;
        color: white;
}

button {
        font-family: "Fredoka";
        background-color: #1277dd;
        color: white;
        border: none;
        padding: 0.5rem 1rem;
        border-radius: 0.25rem;
        cursor: pointer;
    
}
.home-link{
        text-decoration: none;
        color: white;
        font-size: 1.5rem;
        font-weight: 700;
        font-family: "Fredoka";
}
</style>