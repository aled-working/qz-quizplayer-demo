<script>
    import artery from '$lib/assets/linked-cat-IMG-artery.jpg';
    import leaf from '$lib/assets/linked-cat-IMG-leaf.jpg';
    import nutrient from '$lib/assets/linked-cat-IMG-nutrient.jpg';

/* youtube  https://www.youtube.com/watch?v=aZzGvfnw8Zw */
// https://medium.com/codex/things-ive-learned-building-a-drag-drop-component-with-svelte-2ad9169f1aff
//https://svelte.dev/examples/animate

const dummyLinked = {
    /* correctAnswer: {
        qCat00: 'op02',
        qCat01: 'op04',
        qCat02: 'op01',
        qCat03: 'op05',
        qCat04: 'op03',
        qCat05: 'op00',
    }, */
    correctAnswer: {
        op00:'Artery',
        op02:'Leaf',
        op04:'Nutrient',
    },
    type: 'linked',
    qText: 'Which ones match?',

    qCategories: [
        { 
            qCatText: 'Artery ',
            qCatId: 'qCat00',
            qCatImg: artery
        },
        { 
            qCatText: 'Leaf',
            qCatId: 'qCat01',
            qCatImg: leaf,
        },
        { 
            qCatText: 'Nutrient',
            qCatId: 'qCat02',
            qCatImg: nutrient
        },
],
    options: [
        { 
            opText: 'A green part of a plant attached to the stem, where gases enter and leave the plant',
            opId: 'op01'
        },
        { 
            opText: 'A substance that is essential for an organism to grow and live',
            opId: 'op02'
        },
        { 
            opText: 'A muscular tube that transports blood from the heart to all parts of the body.',
            opId: 'op03'
        },
]
} // end dummy data


let whichCat = false
let studentAnswer = {}

function checkAnswer(){
    //used all the cats?
    if (Object.keys(studentAnswer).length !== Object.keys(dummyLinked.correctAnswer).length) return

    //compare
    let numCorrectMatches = Object.keys(studentAnswer).filter( key => studentAnswer[key] === dummyLinked.correctAnswer[key]).length

    // announce
    if (numCorrectMatches === Object.keys(dummyLinked.correctAnswer).length) {
        console.log('WOOHOO')
    }else{
        console.log('NOT QUITE RIGHT')
    }
}




</script>

<div class="qWrap center column">

    <h1>{dummyLinked.qText}</h1>

<!-- categories -->

<div class="categories center">
    {#each dummyLinked.qCategories as qCat}
    <div 
        id={qCat.qCatId}
        class={ qCat.isUsed 
                ? 'qCat usedCat faint'
                : qCat === whichCat 
                    ? 'qCat selected' 
                    : 'qCat'}
        draggable="true"
        on:pointerdown={()=>{whichCat = qCat }}
    >
    <img src={qCat.qCatImg} alt="">
    <!-- <h1 
        class='btn'>{qCat.qCatText}
    </h1> -->
</div>
{/each}
</div>



<div class="faint">Tap an image, then tap its description</div>



<!-- options -->

<div class="optionsForLinking center">
    {#each dummyLinked.options as option}
        
        <div 
        id={option.opId} 
        class='option big bold rounded center column'
        on:pointerdown={
            ()=>{
                if (!whichCat) return
                studentAnswer[option.opId] = whichCat.qCatText
                whichCat.isUsed = true
                checkAnswer()
                whichCat = false // reset
            } }
        >
        {option.opText}

        {#if (studentAnswer[option.opId] )}
        <h1 
        
        class='btn'
        on:pointerdown={()=> {
            // delete studentAnswer[option.opId] 
            // console.log('option.opId was',option.opId);
            // console.log('studentAnswer',studentAnswer);
            }}
        >
        {studentAnswer[option.opId]}
        </h1>
     {/if}   
    </div>
    {/each}
</div>
</div>


<style>
.qWrap{
    gap: 2rem
    }
.categories{
    gap: 2rem;
    flex-wrap: wrap;
    max-width: 50rem;
    cursor: grab;
}
.qCat h1{
    font-size:2rem;
    transition: all .5s ease;
    overflow: hidden;
}

.optionsForLinking{
    gap: 1rem;
    align-items: flex-start;
    padding: 0 2rem;
    max-width: 60rem;
    flex-wrap:wrap;

}
.optionsForLinking .option{
    border: 2px dashed #ffffff33;
    padding: .5rem;
    width: 15rem
}
.optionsForLinking .option:hover{
    border: 2px solid yellow
}
.selected h1 {
    background: yellow
}
.qCat img{
    width: 8rem;
    height: 8rem;
    border-radius: 50%;
    transition: all .5s ease;
    border:.5rem solid white;
}
.qCat .btn img{
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    border:none
}
.qCat:hover img
{
    scale: 1.7;
    /* border: .5rem solid yellow; */
}
.qCat.selected img
{
    scale: 1.7;
    border: .5rem solid yellow;
}
.usedCat img{
    scale: 0.8;
    border: .5rem solid yellow;
}


</style>