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

</script>



<h1>{dummyMulti.qText}</h1>
<div class="faint">Pick one</div>
<div class='options center'>{#each dummyMulti.options as option, id}
    <button><h1>{option.optionText}</h1> </button>
{/each}</div>





<style>
    .options {gap: .5rem}
</style>