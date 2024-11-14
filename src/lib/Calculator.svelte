<script>
    import { onMount } from 'svelte';
    let input = "";
    let lastInputIsOperator = false; 

    function append(value) {
        if (typeof value === "number" || value === ".") {
            input += value;
            lastInputIsOperator = false; 
        } else if (!lastInputIsOperator) {
            input += value;
            lastInputIsOperator = true; 
        }
    }

    function calculate() {
        try {
            input = eval(input);
            lastInputIsOperator = false;
        } catch (error) {
            input = "Xato";
        }
    }

    function clearInput() {
        input = "";
        lastInputIsOperator = false; 
    }

    function handleKeydown(event) {
        const key = event.key;

        if (/\d/.test(key)) {
            append(Number(key));
        } else if (key === '+' || key === '-' || key === '*' || key === '/') {
            append(key);
        } else if (key === 'Enter') {
            calculate();
        } else if (key === 'Escape' || key === 'c') {
            clearInput();
        } else if (key === '.') {
            append('.');
        }
    }

    onMount(() => {
        window.addEventListener('keydown', handleKeydown);
        return () => window.removeEventListener('keydown', handleKeydown);
    });
</script>

<div class="w-3/12 my-20 mx-auto p-5 rounded-lg text-right bg-blue-800 bg-opacity-80 shadow-md">
    <div class="display text-2xl mb-2.5 p-2.5 border border-yellow-50 rounded bg-gray-200 text-blue-900">
        {input || "0"}
    </div>
    <div class="buttons grid grid-cols-4 gap-2.5">
        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append(1)}>1</button>
        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append(2)}>2</button>
        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append(3)}>3</button>
        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append("+")}>+</button>

        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append(4)}>4</button>
        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append(5)}>5</button>
        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append(6)}>6</button>
        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append("-")}>-</button>

        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append(7)}>7</button>
        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append(8)}>8</button>
        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append(9)}>9</button>
        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append("*")}>×</button>

        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append(0)}>0</button>
        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append(".")}>.</button>
        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => calculate()}>=</button>
        <button class="p-2 text-xl cursor-pointer rounded bg-blue-500 text-white hover:bg-blue-600 active:bg-blue-700 transition-transform duration-200 ease-in-out transform hover:scale-105" on:click={() => append("/")}>÷</button>

        <button class="p-2 text-xl cursor-pointer rounded bg-yellow-500 text-white hover:bg-yellow-600 active:bg-yellow-700 transition-transform duration-200 ease-in-out transform hover:scale-105 col-span-4" on:click={() => clearInput()}>C</button>
    </div>
</div>

