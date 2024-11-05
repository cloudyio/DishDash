<script lang="ts">
    let data = null;

    async function RollFood() {
        const response = await fetch('https://www.themealdb.com/api/json/v1/1/random.php');
        data = await response.json();
        console.log(data);
    }
</script>

<div class="bg-[#2e2e2e] text-[#fdffff] h-screen ">
    <div class="flex pt-40 justify-center">
        <div class="flex flex-col items-center">
            <h1 class="font-bold text-6xl flex-col flex justify-center">Dish Dash</h1>
            <h2 class="text-xl">Find a random meal to cook up</h2>
            <button
                class="inline-block cursor-pointer mt-5 text-lg h-16 w-50 rounded-md bg-gray-800 px-4 py-3 text-center font-semibold text-white transition duration-200 ease-in-out hover:bg-gray-900" 
                on:click={() => RollFood()}>
                Find me a meal!
            </button>
        </div>
    </div>

    {#if data && data.meals && data.meals.length > 0}
    <div class="mt-10 text-center flex justify-center">
        <div class="flex flex-col items-center max-w-md">
            <h2 class="text-2xl font-bold mb-4">{data.meals[0].strMeal}</h2>
            <p class="text-lg mb-2"><strong>Category:</strong> {data.meals[0].strCategory}</p>
            <p class="text-lg mb-2"><strong>Area:</strong> {data.meals[0].strArea}</p>
        </div>
        <img class="w-full max-w-md mx-4 rounded-lg mb-4" src={data.meals[0].strMealThumb} alt="{data.meals[0].strMeal}" />
    </div>

    <div class="mt-6 flex bg-[#2e2e2e]">
        <div class="mr-10 ">
            <h3 class="text-xl font-semibold mb-2">Ingredients</h3>
            <ul class="list-none p-0">
                {#each Array(12) as _, i}
                    {#if data.meals[0][`strIngredient${i + 1}`]}
                        <li class="text-lg mb-1">
                            {data.meals[0][`strMeasure${i + 1}`]} {data.meals[0][`strIngredient${i + 1}`]}
                        </li>
                    {/if}
                {/each}
            </ul>
        </div>
        <div>
            <h3 class="text-xl font-semibold mb-2">Instructions</h3>
            <p class="text-lg mb-2">{data.meals[0].strInstructions}</p>
        </div>
    </div>
    {/if}
</div>
