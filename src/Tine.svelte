<script>
    export let note;
    let c4 = new Audio("C4.wav");

    let tine;
    let isTouched = false;

    let playSound = () => {
        c4.currentTime = 0;
        c4.play();
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
        padding: 10px;
        color: tomato;
        font-weight: bold;
        border-radius: 0 0 10px 10px;
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
    {note}
</div>
