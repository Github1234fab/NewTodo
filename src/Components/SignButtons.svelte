<script>

        import caddie from "../assets/pngegg (27).png"
</script>

<section class="buttons-container">
     <div class="wrapper-buttons">
                <a href="/Signin">Sign in</a>
                <a href="/Signup">Sign up</a>
                </div>
                <img class="caddie" src={caddie} alt="illustration d'un Caddie">


</section>

<style>
        .buttons-container {
                display: flex;
                flex-direction: column;
                justify-content: center;
                align-items: center;
                padding: 1rem;
                width: 50%;
                margin: auto auto;
                gap: 50px;
        }
        .wrapper-buttons{
                display: flex;
                justify-content: center;
                align-items: center;
                gap: 30px;
        }
a{
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
.caddie{
        width: auto;
        height: 200px;
          margin-left: -50px;
}
   
</style>
