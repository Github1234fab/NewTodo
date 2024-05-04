<script>
        import { signInWithEmailAndPassword } from "firebase/auth";
        import { auth } from "../../lib/firebase.js";

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

<section class="signIn-section">
        <h1>Sign In</h1>
        <form on:submit|preventDefault={login}>
                <div class="wrapper-input">
                        <label for="Email">Email</label>
                        <input type="email" bind:value={email} name="Email" id="Email" />
                </div>
                <div class="wrapper-input">
                        <label for="Password">Password </label>
                        <input type="password" bind:value={password} name="Password" id="Password" />
                </div>
                <button type="submit">Log In</button>
                <p>
                        Are U sure you have an account? <br />
                        If you haven't an account, <br />go to <a href="/Signup"> Sign Up</a>
                </p>
        </form>
</section>

<style>
        .signIn-section {
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                height: 100vh;
                background: linear-gradient(160deg, rgb(3, 3, 53), rgb(21, 21, 158));
                color: rgb(255, 255, 255);
                gap: 30px;
        }

        form {
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                gap: 30px;
                background-color: rgba(26, 26, 152, 0.709);
                width: 45%;
                height: 60%;
                border-radius: 20px;
        }

        .wrapper-input {
                display: flex;
                flex-direction: column;
                justify-content: baseline;
                align-items: baseline;
                gap: 8px;
        }

        input {
                padding: 0.5rem;
                border-radius: 0.25rem;
                border: 1px solid pink;
                background-color: transparent;
                color: rgb(229, 228, 228);
                font-weight: 700;
        }
        button {
                text-decoration: none;
                color: white;
                padding: 0.5rem 1rem;
                border-radius: 0.25rem;
                cursor: pointer;
                background-color: #1277dd;
                border: none;
                font-size: 1rem;
                font-weight: 300;
        }
        p {
                color: rgba(255, 255, 255, 0.775);
                font-weight: 200;
                margin-top: 40px;
        }
        a {
                color: white;
        }

        @media (max-width: 768px) {
                form {
                        width: 90%;
                }
        }
</style>
