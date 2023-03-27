<script>
    import logo from '$lib/assets/logo.png';
  </script>


<main class='center column'>
<nav>nav</nav>
<slot />

</main>
<footer class='center column'>
    <div>12 questions created for KS3 learners by</div>
    <div><img src={logo} alt=""></div>
    
</footer>


<style>
    main{
        inset:0;
        min-height: 90vh; 
        background: radial-gradient(64.57% 64.57% at 50% 35.43%, #009BC7 0%, #007A9C 92.65%);
        
        color:white;
        position: relative;
        gap: 2rem;
    }
    nav{
        position: absolute;
        top:0;
        padding: 1rem;
    }
    footer{
        color: var(--pearson-blue);
        min-height: max-content; 
        padding: 4rem;
        gap: 2rem
    }

</style>