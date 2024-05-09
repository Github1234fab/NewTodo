<script>
        import { addDoc, collection, onSnapshot, deleteDoc, doc, query, where } from "firebase/firestore";
        import { db, auth } from "../../lib/firebase.js";
        import { onMount } from "svelte";

        let produit = "";
        let snap;
        let inputData;

        //écouteur d'évènemenent sur la base de données. Dès qu'un utilisateur est connecté, on récupère les données de l'utilisateur

        auth.onAuthStateChanged((user) => {
                if (user) {
                        const q = query(collection(db, "todos"), where("userId", "==", user.uid));
                        onSnapshot(q, (snapshot) => {
                                snap = snapshot.docs.sort((a, b) => {
                                        const produitA = a.data().produit.toUpperCase(); // ignore upper and lowercase
                                        const produitB = b.data().produit.toUpperCase(); // ignore upper and lowercase
                                        if (produitA < produitB) {
                                                return -1;
                                        }
                                        if (produitA > produitB) {
                                                return 1;
                                        }
                                        return 0; // names must be equal
                                });
                                console.log(user.uid);
                        });
                } else {
                        snap = null;
                }
        });

        // fonction pour ajouter un produit dans la base de données, avec un id généré aléatoirement et l'id de l'utilisateur connecté

        async function handleSubmit(event) {
                event.preventDefault();
                console.log(db);

                inputData = {
                        produit: produit.trim(),
                        id: crypto.randomUUID(),
                        userId: auth.currentUser.uid,
                };

                await addDoc(collection(db, "todos"), inputData);
                console.log(inputData);

                produit = "";
                console.log(produit);
        }

        //fonction pour supprimer un produit de la base de données en fonction de son id

        async function handleClick(id) {
                const docRef = doc(db, "todos", id);
                await deleteDoc(docRef);
                console.log("Document successfully deleted!");
        }
</script>

<div class="app-section">
        <form on:submit={handleSubmit}>
                <div class="wrapper-input">
                        <label for="Produits">Your products</label>
                        <input type="text" bind:value={produit} id="produits" />
                </div>
                <button type="submit">Add</button>
        </form>
        <h2>Your list</h2>
        {#if snap}
                <ul>
                        {#each snap as doc}
                                <li>
                                        {doc.data().produit}
                                        <button class="delete" on:click={() => handleClick(doc.id)}>x</button>
                                </li>
                        {/each}
                </ul>
        {/if}
</div>

<style>
        .app-section {
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                height: 100vh;
                background: linear-gradient(160deg, rgb(3, 3, 53), rgb(21, 21, 158));
                color: rgb(255, 255, 255);
                gap: 30px;
        }
        .wrapper-input {
                display: flex;
                flex-direction: column;
                justify-content: baseline;
                align-items: baseline;
                gap: 8px;
        }
        form {
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                gap: 30px;
                padding: 1rem 2rem;
                border-radius: 20px;
                margin-top: -50px;
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
                border-radius: 8px;
                cursor: pointer;
                background-color: #1277dd;
                border: none;
                font-size: 1rem;
                font-weight: 300;
                margin-left: 10px;
        }
        .delete {
                text-decoration: none;
                color: white;
                width: auto;
                height: 40px;
                padding: 0.5rem 1rem;
                border-radius: 100%;
                cursor: pointer;
                background-color: transparent;
                border: none;
                font-size: 1rem;
                font-weight: 900;
                margin-left: 10px;
                color: red;
        }

        ul {
                display: flex;
                flex-direction: column;
                width: 90%;
                padding: 1rem 2rem;
                max-height: 400px;
                flex-wrap: wrap;
                border: 1px solid pink;
                border-radius: 10px;
                gap: 20px;
        }
        ul > * {
                flex: 1 1 10%;
        }
        li {
                color: white;
        }
        h2 {
                color: white;
                font-size: 1rem;
                font-weight: 400;
                margin-left: -760px;
        }
</style>
