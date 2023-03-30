<script>
    import logo from '$lib/assets/logo.png';
  </script>


<main class='center column'>

<div class="questionArea center column">
    <slot />
</div>

</main>
<footer class='center column'>
    <div>12 questions created for KS3 learners by</div>
    <div><img src={logo} alt=""></div>
    <nav class='center'>
        <a href="/">start</a>
        <a href="/multiple-choice">multiple choice</a>
        <a href="/linking">linking</a>
        <a href="/linking-with-images">linking, with images</a>
        <a href="/scrambled">scrambled</a>
    </nav>
    
</footer>


<style>
    main{
        inset:0;
        
        background: radial-gradient(64.57% 64.57% at 50% 35.43%, #009BC7 0%, #007A9C 92.65%);
        
        color:white;
        position: relative;
        /* gap: 2rem; */
    }
    .questionArea{
        gap: 2rem;
        min-height: 70vh; 
        padding: 4rem 0;
    }
    nav{
        /* position: absolute;
        top:0; */
        padding: 1rem;
        gap: 1rem
    }
    footer{
        color: var(--pearson-blue);
        min-height: max-content; 
        padding: 4rem;
        gap: 2rem
    }

</style>