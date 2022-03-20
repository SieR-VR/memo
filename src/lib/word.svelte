<script lang="ts">
    export let word: string;

    function onDragStart(event: DragEvent): void {
        let dataTransfer = event.dataTransfer;
        dataTransfer.setData("text", word);
        
        dataTransfer.setDragImage(event.target as HTMLDivElement, 0, 0);
    }
</script>

<div draggable="true" class="word-card" on:dragstart={onDragStart}>
    <div class="word">{word}</div>
</div>

<style>
    @import url('./style.css');

    @keyframes floating {
        0% {
            transform: translateY(0);
        }
        50% {
            transform: translateY(5px);
        }
        100% {
            transform: translateY(0);
        }
    }

    @keyframes shake {
        0% { transform: translate(1px, 1px) rotate(0deg); }
        10% { transform: translate(-1px, -2px) rotate(-1deg); }
        20% { transform: translate(-3px, 0px) rotate(1deg); }
        30% { transform: translate(3px, 2px) rotate(0deg); }
        40% { transform: translate(1px, -1px) rotate(1deg); }
        50% { transform: translate(-1px, 2px) rotate(-1deg); }
        60% { transform: translate(-3px, 1px) rotate(0deg); }
        70% { transform: translate(3px, 1px) rotate(-1deg); }
        80% { transform: translate(-1px, -1px) rotate(1deg); }
        90% { transform: translate(1px, 2px) rotate(0deg); }
        100% { transform: translate(1px, -2px) rotate(-1deg); }
    }

    .word-card {
        background-color: #ffffff;
        border: 3px solid #367aff;
        border-radius: 5px;

        box-shadow: 0px 0px 5px 0px rgba(0, 0, 0, 0.75);

        display: flex;
        min-width: 70px;
        height: 40px;

        margin: 10px;
        padding: 0 10px;

        justify-content: center;
        align-items: center;

        animation: floating 3s ease-in-out infinite;
    }

    .word-card:hover {
        animation: shake 0.5s ease-in-out infinite;
    }

    .word {
        font-family: 'Nanum Handwriting';
        font-size: 30px;
    }
</style>