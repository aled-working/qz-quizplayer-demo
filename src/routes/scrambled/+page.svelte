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


let word = ''
let answered = false
let isCorrect = false
let isWrong = false
let correctObj = null

let scrambled = dummyMulti.correctAnswer.optionText.split('')
function shuffle(what){
    return what.sort(() => Math.random() - 0.5)
}
scrambled = shuffle(scrambled)
if (scrambled.join('')===dummyMulti.correctAnswer.optionText) scrambled = shuffle(scrambled) // shuffle again if result is actually the word

function handleTap(i){
    word = word + scrambled[i]
    checkAnswer()
}
function checkAnswer(){
    
    let correctWord = dummyMulti.correctAnswer.optionText
    if (word.length >= correctWord.length) {
        answered=true
    } else { return }

    if (word===dummyMulti.correctAnswer.optionText) {
        isCorrect = true
        console.log('WOOHOO')
    }else{
        isWrong = true
        console.log('NOT QUITE RIGHT')
    }
}
function deleteLast(){
    console.log('deleteLast');
    let current = word.split('')
    let trashed = current.pop()
    word = current.join('')
    isCorrect = false
    isWrong = false
}
</script>



<div class="faint">Which word means...</div>
<h1>{dummyMulti.qText}</h1>
<div class='options center'>
    {#each scrambled as letter, i}
    <div 
    class={`btn ${isCorrect || isWrong ? 'faint' : ''}`}
    on:pointerdown={()=>{handleTap(i)}}
    ><h1>{letter}</h1> </div>
{/each}</div>


<div class={`options center ${word ? '' : 'trans' }`}>

    <!-- <div class={`btn ${answered ? 'answered' : ''} ${isCorrect ? 'correct' : ''}` }>
        <h1 >{word} 
            <span class="badge badge-wrong">&#x2718;</span>
            <span class="badge badge-correct">&#10003;</span>
        </h1>
    </div> -->
    <h1 class="btn">
        {#if isWrong}<span class="badge badge-wrong">&#x2718;</span>{/if}
        {#if isCorrect}<span class="badge badge-correct">&#10003;</span>{/if}
        {word} 
    </h1>

        {#if !isWrong && !isCorrect}
    <h1 class='btn faint' on:click={()=>deleteLast()}>x</h1>
    {/if}
    
</div>






<style>
    .options {gap: .5rem}
</style>