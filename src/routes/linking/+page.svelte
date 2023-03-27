<script>

/* youtube  https://www.youtube.com/watch?v=aZzGvfnw8Zw */
// https://medium.com/codex/things-ive-learned-building-a-drag-drop-component-with-svelte-2ad9169f1aff
//https://svelte.dev/examples/animate

const dummyLinked = {
    correctAnswer: {
        qCat00: 'op02',
        qCat01: 'op04',
        qCat02: 'op01',
        qCat03: 'op05',
        qCat04: 'op03',
        qCat05: 'op00',
    },
    type: 'linked',
    qText: 'Which ones match?',

    qCategories: [
        { 
            qCatText: 'Heart',
            qCatId: 'qCat00'
        },
        { 
            qCatText: 'Root',
            qCatId: 'qCat01'
        },
        { 
            qCatText: 'Leaf',
            qCatId: 'qCat02'
        },
        { 
            qCatText: 'Digestion',
            qCatId: 'qCat03'
        },
        { 
            qCatText: 'Nutrient',
            qCatId: 'qCat04'
        },
        { 
            qCatText: 'Skeleton',
            qCatId: 'qCat05'
        },
],
    options: [
        { 
            opText: 'A framework of bones that hold together a plant or animal',
            opId: 'op00'
        },
        { 
            opText: 'A green part of a plant attached to the stem, where gases enter and leave the plant',
            opId: 'op01'
        },
        { 
            opText: 'A large muscle that pumps blood around the body',
            opId: 'op02'
        },
        { 
            opText: 'A substance that is essential for an organism to grow and live',
            opId: 'op03'
        },
        { 
            opText: 'The part of a plant which attaches it to the ground, and allows the plant to absorb water and nutrients',
            opId: 'op04'
        },
        { 
            opText: 'The process of breaking down food into nutrients that can be absorbed by the body',
            opId: 'op05'
        },
]
} // end dummy data


let userAnswer = {}
let whichCat = false
let qWrapClass = ''

function start(cat){
    whichCat = cat
    qWrapClass = 'started'
//console.log('start', cat, whichCat);
}
function match(option){
    if (!whichCat) return
    // collect user answers until complete, then check against dummyLinked.correctAnswer
    userAnswer[whichCat] = option
    let numCats = dummyLinked.qCategories.length
    let numUserAnswersSoFar = Object.keys(userAnswer).length

    console.log('numUserAnswersSoFar',numUserAnswersSoFar);
    if (numUserAnswersSoFar === numCats) {
        console.log('checking');
        let numCorrect = 0
        Object.keys(userAnswer).forEach(k=> {if(userAnswer[k] === dummyLinked.correctAnswer[k])
                {numCorrect +=1; console.log('numCorrect', numCorrect)}})
        if (numCorrect === numCats)     console.log('SUCCESS');   
        if (numCorrect !== numCats)     console.log('NOT QUITE');   

    }
}
function cancel(){
console.log('cancel');
}



</script>

<div class={`qWrap center column ${qWrapClass}`}>

    <h1>{dummyLinked.qText}</h1>


<div class="categories center">
    {#each dummyLinked.qCategories as qCat}
        <div 
        id={qCat.qCatId}
        draggable="true"
        on:pointerdown={()=>start(qCat.qCatId)}
        >
        <h1 
        class='btn'>{qCat.qCatText}
        </h1>
    </div>
    {/each}
</div>

<div class="faint">Drag each onto its match below</div>

<div class="optionsForLinking center">
    {#each dummyLinked.options as option}
        <div 
        id={option.opId} 
        class='option big bold rounded center'
        on:pointerdown={()=>match(option.opId)}
        >
        {option.opText}
    </div>
    {/each}
</div>
</div>


<style>
    .qWrap{
        gap: 2rem
    }
    .categories{
    gap: .3rem;
    flex-wrap: wrap;
    max-width: 50rem;
    cursor: grab;
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

</style>