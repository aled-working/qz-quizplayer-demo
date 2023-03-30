<script>

    const dummyMulti={
        correctAnswer: {
            optionText: 'Leaf',
            optionId: 'option02'
    },
        type: 'linked',
        qText: 'A green part of a plant attached to the stem, where gases enter and leave the plant',
        options: [
        { 
            optionText: 'Heart',
            optionId: 'option00'
        },
        { 
            optionText: 'Root',
            optionId: 'option01'
        },
        { 
            optionText: 'Leaf',
            optionId: 'option02'
        },
        { 
            optionText: 'Digestion',
            optionId: 'option03'
        },
        { 
            optionText: 'Nutrient',
            optionId: 'option04'
        },
        { 
            optionText: 'Skeleton',
            optionId: 'option05'
        },
    ]
    }

let answered = false
let isCorrect = false
let isWrong = false
let clicked = null
let correctObj = null
let word //// ????
function handleTap(clickedId){
    clicked = clickedId
    console.log('clickedId',clickedId);
    word= dummyMulti.options.find(op=> op.optionId === clickedId).optionText //// jeez
    //     {#if dummyLinked.options.find(op=> op.userCat===whichCat)}
    checkAnswer()
}
function checkAnswer(){
    answered = true
    // correctObj = dummyMulti.correctAnswer
    if (word === correctObj.optionText) {
        console.log('WOOHOO')
    }else{
        console.log('NOT QUITE RIGHT')
    }
    // handle wrong
    return
}

</script>



<h1>{dummyMulti.qText}</h1>
<div class="faint">Pick one</div>

<div class={`options center ${answered ? 'answered' : ''}`}>
    {#each dummyMulti.options as option, id}
    <h1 
    class={`btn ${clicked===option.optionId ? 'clicked':''} ${dummyMulti.correctAnswer.optionId===option.optionId ? 'correct':''}`}
    on:click={()=>handleTap(option.optionId)}
    >
    <span class="badge badge-wrong">&#x2718;</span>
    <span class="badge badge-correct">&#10003;</span>
    {option.optionText}
</h1> 
{/each}</div>





<style>
    .options {gap: .5rem}

    .badge {
        display: none;
        position: absolute;
        left:.5rem;
        top: 50%;
        translate: 0 -50%;
        place-items: center;
        width:3rem;
        height:3rem;
        border-radius: 50%;
        box-shadow: var(--base-deeper-color) 0px 20px 30px -10px;
        scale: 1;
        animation: popIn .2s ease  ;      
    }
    @keyframes popIn {
        from {scale: 1.5}
        to {scale: 1}
    }

    /******** STATES ********/
.answered{ pointer-events: none;}
.answered .btn{ opacity: .5;}
.answered .correct{
    background-color: var(--correct-color);
    border-color:var(--text-color);
    color:white;
    border: 5px solid currentColor;
    opacity: 1;
}
.clicked:not(.correct){
        background-color: var(--wrong-color);
        border-color: var(--wrong-color);
        color:var(--text-color);
        opacity: 1;
    }
.clicked {padding-left: 3rem;}
/* .clicked  .badge{ display: grid}    */
.clicked .badge-wrong {display: block;}
.correct .badge-wrong {display: none}
.clicked.correct .badge-correct {display: block}


</style>