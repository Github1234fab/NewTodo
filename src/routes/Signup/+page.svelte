<script>
        import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";
        import { collection, addDoc } from "firebase/firestore";
        import { db } from "../../lib/firebase.js";

        let email = "";
        let password = "";

        const auth = getAuth();

        //fonction pour créer un utilisateur avec un email et un mot de passe. Si la création est réussie, on ajoute l'utilisateur à la collection "users" dans Firestore

        const signup = async (event) => {
                event.preventDefault();

                try {
                        const userCredential = await createUserWithEmailAndPassword(auth, email, password);
                        const user = userCredential.user;
                        console.log("User signed up successfully:", user);

                        // Ajouter l'utilisateur à la collection "users" dans Firestore
                        const usersCollection = collection(db, "users");
                        await addDoc(usersCollection, {
                                email: user.email,
                        });
                        window.location.href = "/Application";
                } catch (error) {
                        const errorCode = error.code;
                        const errorMessage = error.message;
                        console.log("Error code:", errorCode);
                        console.log("Error message:", errorMessage);
                        console.log("no sign");
                }
        };
</script>

<section class="signUp-section">
        <h1>SignUp</h1>
        <form on:submit={signup}>
                <div class="wrapper-input">
                        <label for="E-mail">E-mail</label>
                        <input type="email" bind:value={email} id="E-mail" name="E-mail" placeholder="Your E-mail" />
                </div>
                <div class="wrapper-input">
                        <label for="Password">Password </label>
                        <input
                                type="password"
                                bind:value={password}
                                id="Password"
                                name="Password"
                                placeholder="
minimum of 6 characters"
                        />
                </div>

                <button type="submit">Sign Up</button>
                <p>
                        You haven't an account? <br />
                        Please, sign up or <a href="/Signin">sign in</a>
                </p>
        </form>
</section>

<style>
        .signUp-section {
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
                background-color: rgba(0, 0, 255, 0.709);
                border-radius: 20px;
                width: 25%;
                height: 50%;
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
                font-weight: 700;
                border-radius: 0.25rem;
                border: 1px solid pink;
                background-color: transparent;
                color: rgb(229, 228, 228);
        }
        input::placeholder{
                color: rgba(98, 173, 238, 0.585);
                font-weight: 100;
        }
        label {
                margin-left: -90px;
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
        }
        a {
                color: white;
        }
</style>
