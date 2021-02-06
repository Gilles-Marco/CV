<script>
import { onMount } from "svelte"
import { watchResize } from "svelte-watch-resize"

import AppbarButton from "./AppbarButton.svelte"

    export let selected = 0;

    let buttons = [
        {
            text: "Presentation",
            link: "#presentation"
        },
        {
            text: "Projects",
            link: "#projects"
        },
        {
            text: "Career",
            link: "#career"
        },
        {
            text: "Degrees",
            link: "#degrees"
        },
        {
            text: "Contact",
            link: "#contact"
        }
    ]

    let slider;
    let overlay;
    let appBarButtons = []

    function moveSlider(target){
        let button = appBarButtons[target]

        if(button === undefined) return;

        let buttonRect = button.getBoundingClientRect()
        slider.style.left = buttonRect.x+"px"
        slider.style.width = buttonRect.width+"px"
        slider.style.margin = "0"
        overlay.style.left = buttonRect.x+"px"
        overlay.style.width = buttonRect.width+"px"
        overlay.style.margin = "0";
    }

    function handleClick(event, index){
        selected = index;
    }

    function handleResize(){
        moveSlider(selected);
    }

    $: moveSlider(selected);

    onMount(async ()=>{
        setTimeout(()=>{
            moveSlider(selected)
        }, 100)
        
    })
</script>

<style type="text/scss">

%over-button {
    transition: left 0.5s ease-out, width 0.5s ease-out;
    height: 100%;
    width: 0;
    pointer-events: none;
    position: absolute;
}

.appbar {
    $width-slider: 2px;

    @apply flex flex-row justify-center lg:space-x-8 md:space-x-4 space-x-2;

    position: fixed !important; /* Sometimes something tries to overwrite position value by 'relative' */
    background-image: linear-gradient(to bottom left,  rgba(245, 245, 245, 0.6), rgba(245, 245, 245, 0.4));
    backdrop-filter: blur(2px);
    height: 3.5em;
    width: 100%;
    border-bottom: solid 2px #EEE;
    box-shadow: 0px 1px 25px -10px rgba(125, 125, 125, 0.5);

    div {
        @apply flex flex-row;
    }

    .slider {
        @extend %over-button;
        border-bottom: solid $width-slider rgba(224, 45, 45, 0.897);
    }

    .wrapper {
        cursor: pointer;
        user-select: none;
    }

    .overlay {
        @extend %over-button;
        background-image: linear-gradient(to top, rgba(255, 195, 195, 0.3), rgba(255, 255, 255, 0));
    }
}

</style>

<div class="appbar" use:watchResize={handleResize}>
    <div>
        {#each buttons as button, index}
            <div class="wrapper" class:underline={selected==index} on:click={(event) => handleClick(event, index)} bind:this="{appBarButtons[index]}">
                <AppbarButton  {...button}/>
            </div>
        {/each}
    </div>
    <div class="slider" bind:this={slider}/>
    <div class="overlay" bind:this={overlay}/>
</div>