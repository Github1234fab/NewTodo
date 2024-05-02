<script>
        import { signInWithEmailAndPassword } from "firebase/auth";
            import { auth } from '../../lib/firebase.js';

        let email = "";
        let password = "";

        //fonction pour se connecter avec un email et un mot de passe. Si la connexion est réussie, on redirige l'utilisateur vers la page d'application

        const login = async () => {
                try {
                        const userCredential = await signInWithEmailAndPassword(auth, email, password);
                        // Signed in
                        const user = userCredential.user;
                        console.log("Logged in with email:", email);
                          window.location.href = "/Application"; 
                } catch (error) {
                        const errorCode = error.code;
                        const errorMessage = error.message;
                        console.log("Failed to log in:", errorMessage);
                }
        };
</script>

<section class="auth-section">
        <form on:submit|preventDefault={login}>
                <label for="Email">Email</label>
                <input type="email" bind:value={email} name="Email" id="Email" />
                <label for="Password">Password </label>
                <input type="password" bind:value={password} name="Password" id="Password" />

                <button type="submit">Log In</button>
                <p>
                        Are U sure you have an account? <br />
                        If you haven't an account, go to <a href="/Signup"> Sign Up</a>
                </p>
        </form>
        <a href="/Application">Application</a>

</section>
