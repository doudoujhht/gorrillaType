<script lang="ts">
    import * as english from "../languages/english.json"

    let userText = "";
    function getRandomWords (words):String{
        const randomWords = new Set();
        while(randomWords.size < 30){
            randomWords.add(words[Math.floor(Math.random() * words.length)])
        }
        return [...randomWords].join(" ");
    }

    let words = getRandomWords(english.words)
    const handleInput = (e) => {
        // I want to know if a key was a letter or not
        // if it was a letter, I want to add it to the userText
        // if it was a backspace, I want to remove the last letter from the userText
        // if it was a space, I want to add a space to the userText
        if (e.key === "Backspace"){
            userText = userText.slice(0, -1)

        }
        else if (e.key === " "){
            userText += " "

        }
        else{
            userText += e.key;
        }

    }

</script>
<svelte:body on:keydown={handleInput}/>

<main class="bg-background h-[90vh] flex flex-col items-center justify-center" >
<!--    <Choices/>-->
    <div class="text-icon text-3xl">
        {#each words as word , index}
            {#if userText.length>index && userText[index] === words[index]}
                <span class="text-primary">{word}</span>
            {:else if userText.length > index && userText[index] !== words[index]}
                <span class="text-secondary">{word}</span>
            {:else}
                <span class="text-default">{word}</span>
            {/if}
        {/each}
    </div>

</main>