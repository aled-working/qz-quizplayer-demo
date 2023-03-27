<script>
const dummyLinked = {
    answer: {
        q00: 'op05',
        q01: 'op04',
        q02: 'op03',
        q03: 'op02',
        q04: 'op01',
        q01: 'op00',
    },
    type: 'linked',
    qText: 'Which ones match?',
    qImg: null,

    qCategories: [
        { 
            qCatText: 'Heart',
            qCatImg: null,
            qCatId: 'qCat00'
        },
        { 
            qCatText: 'Root',
            qCatImg: null,
            qCatId: 'qCat01'
        },
        { 
            qCatText: 'Leaf',
            qCatImg: null,
            qCatId: 'qCat02'
        },
        { 
            qCatText: 'Digestion',
            qCatImg: null,
            qCatId: 'qCat03'
        },
        { 
            qCatText: 'Nutrient',
            qCatImg: null,
            qCatId: 'qCat04'
        },
        { 
            qCatText: 'Skeleton',
            qCatImg: null,
            qCatId: 'qCat05'
        },
],
    options: [
        { 
            opText: 'A framework of bones that hold together a plant or animal',
            opImg: null,
            opId: 'op00'
        },
        { 
            opText: 'A green part of a plant attached to the stem, where gases enter and leave the plant',
            opImg: null,
            opId: 'op01'
        },
        { 
            opText: 'A large muscle that pumps blood around the body',
            opImg: null,
            opId: 'op02'
        },
        { 
            opText: 'A substance that is essential for an organism to grow and live',
            opImg: null,
            opId: 'op03'
        },
        { 
            opText: 'The part of a plant which attaches it to the ground, and allows the plant to absorb water and nutrients',
            opImg: null,
            opId: 'op04'
        },
        { 
            opText: 'The process of breaking down food into nutrients that can be absorbed by the body',
            opImg: null,
            opId: 'op05'
        },
]
} // end dummy data

function allowDrop(ev) {
  ev.preventDefault();
  console.log('allowDrop',ev)
}

function drag(ev) {
    console.log('drag',ev)
    ev.preventDefault();
}

function drop(ev) {
  ev.preventDefault();
  console.log('drop',ev)
}

</script>


<h1>{dummyLinked.qText}</h1>


<div class="categories center">
    {#each dummyLinked.qCategories as qCat}
        <div 
        id={qCat.qCatId}
        draggable="true"
        on:dragstart={ev => drag(ev) }
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
        on:drop={ev => drop(ev)}
        on:dragover={ev => allowDrop(ev) }
        >{option.opText}
    </div>
    {/each}
</div>

<style>
.categories{
    gap: .3rem;
    flex-wrap: wrap;
    max-width: 50rem;

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