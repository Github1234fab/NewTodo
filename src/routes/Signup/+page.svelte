<script>
        import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";
        import { collection, addDoc } from "firebase/firestore";
        import { db } from "../../lib/firebase.js";

        let email = "";
        let password = "";
        let eyeOpen = false;

        const auth = getAuth();

        //fonction pour toggle l'icon Eye
        function eyeOpenToggle() {
                eyeOpen = !eyeOpen;
                console.log(eyeOpen);
        }

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
                <div class="wrapper-inputs">
                        <div class="wrapper-input">
                                <label for="E-mail">E-mail</label>
                                <input
                                        type="email"
                                        bind:value={email}
                                        id="E-mail"
                                        name="E-mail"
                                        placeholder="Your E-mail"
                                />
                        </div>
                        <div class="wrapper-input">
                                {#if eyeOpen}
                                        <label for="Password">Password </label>
                                        <input
                                                type="text"
                                                bind:value={password}
                                                name="Password"
                                                id="Password"
                                                placeholder="Your Password"
                                        />
                                {:else}
                                        <label for="Password">Password </label>
                                        <input
                                                type="password"
                                                bind:value={password}
                                                name="Password"
                                                id="Password"
                                                placeholder="Your Password"
                                        />
                                {/if}

                                <div class="wrapper-eye">
                                        <button on:click={eyeOpenToggle} class="eye"><i class="fa-regular fa-eye"></i></button>
                                </div>
                        </div>
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
                background-color: rgba(26, 26, 152, 0.709);
                border-radius: 20px;
                width: 25%;
                height: 80%;
        }
        .wrapper-inputs {
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                gap: 30px;
                width: 100%;
                margin-top: 50px;
        }
        .wrapper-input {
                display: flex;
                justify-content: baseline;
                align-items: baseline;
                gap: 8px;
                flex-direction: column;
        }
        .wrapper-eye {
                display: flex;
                justify-content: flex-start;
                align-items: flex-start;
                gap: 8px;
                flex-direction: column;
                margin-top: 20px;
        }
        .eye {
                background-color: transparent;
                border: none;
                color: white;
                font-size: 1rem;
                cursor: pointer;
                margin-top: 0;
              border: 1px solid white;
              cursor: pointer;
        }
        input {
                padding: 0.5rem;
                font-weight: 700;
                border-radius: 0.25rem;
                border: 1px solid pink;
                background-color: transparent;
                color: rgb(229, 228, 228);
        }
        input::placeholder {
                color: rgba(98, 173, 238, 0.864);
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
                font-weight: 600;
                margin-top: 40px;
        }
        p {
                color: white;
                font-weight: 300;
        }
        a {
                color: white;
        }

        @media (max-width: 768px) {
                form {
                        width: 70%;
                }
        }
</style>
