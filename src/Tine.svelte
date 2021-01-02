<script>
    export let note;
    export let sampler;

    let tine;
    let isTouched = false;

    let playSound = () => {
        sampler.triggerAttackRelease([note.freq], 4)
    };

    let mouseDown = false
</script>

<style>
    .tine {
        user-select: none;
        background: peachpuff;
        height: 100px;
        display: flex;
        align-items: end;
        width: 30px;
        justify-content: center;
        padding-bottom: 7px;
        color: tomato;
        font-weight: bold;
        border-radius: 0 0 15px 15px;
    }

    .active {
        background: olive;
    }
</style>

<svelte:body
    on:touchmove={(e) => {
        e.preventDefault();
        const touch = e.touches[0];
        const element = document.elementFromPoint(touch.pageX, touch.pageY);
        let prevTouched = isTouched;
        isTouched = element === tine;

        if (prevTouched && !isTouched) {
            playSound();
        }
    }}
    on:mousedown={() => {
        mouseDown = true
    }}
    on:mouseup={() => {
        mouseDown = false
    }}   
/>

<div
    class={`tine ${isTouched ? 'active' : ''}`}
    bind:this={tine}
    on:mousedown={() => {
        isTouched = true;
    }}
    on:mouseenter={() => {
        if(mouseDown){
            isTouched = true
        }
    }}
    on:touchstart={() => {
        isTouched = true;
    }}
    on:mouseup={() => {
        isTouched = false;
    }}
    on:touchend={() => {
        isTouched = false;
    }}
    on:mouseleave={() => {
        if (isTouched) {
            isTouched = false;
            playSound();
        }
    }}>
    {note.name}
</div>
