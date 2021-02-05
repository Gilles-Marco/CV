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
    let appBarButtons = []

    function moveSlider(target){
        let button = appBarButtons[target]

        if(button === undefined) return;

        let buttonRect = button.getBoundingClientRect()
        slider.style.left = buttonRect.x+"px"
        slider.style.width = buttonRect.width+"px"
        slider.style.margin = "0"
    }

    function handleEnter(event, index){
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

.appbar {
    $width-slider: 2px;

    @apply fixed flex flex-row justify-center lg:space-x-8 md:space-x-4 space-x-2;

    background-color: lightgreen;
    height: 3.5em;
    width: 100%;

    div {
        @apply flex flex-row;
    }

    .slider {
        @apply mx-8;

        margin-left: 0;
        margin-right: 0;
        pointer-events: none;
        position: absolute;
        height: 100%;
        width: 0;
        border-bottom: solid $width-slider red;
        transition: left 0.5s ease-out, width 0.5s ease-out;
    }
}

</style>

<div class="appbar" use:watchResize={handleResize}>
    <div>
        {#each buttons as button, index}
            <div class="wrapper" on:mouseenter={(event) => handleEnter(event, index)} bind:this="{appBarButtons[index]}">
                <AppbarButton  {...button}/>
            </div>
        {/each}
    </div>
    <div class="slider" bind:this={slider}/>
</div>