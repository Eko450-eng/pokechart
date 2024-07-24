<script lang="ts">
	let types = [
		{ name: 'Normal', immunes: ['Ghost'], weaknesses: ['Rock', 'Steel'], strengths: [] },
		{
			name: 'Fire',
			immunes: [],
			weaknesses: ['Fire', 'Water', 'Rock', 'Dragon'],
			strengths: ['Grass', 'Ice', 'Bug', 'Steel']
		},
		{
			name: 'Water',
			immunes: [],
			weaknesses: ['Water', 'Grass', 'Dragon'],
			strengths: ['Fire', 'Ground', 'Rock']
		},
		{
			name: 'Electric',
			immunes: ['Ground'],
			weaknesses: ['Electric', 'Grass', 'Dragon'],
			strengths: ['Water', 'Flying']
		},
		{
			name: 'Grass',
			immunes: [],
			weaknesses: ['Fire', 'Grass', 'Poison', 'Flying', 'Bug', 'Dragon', 'Steel'],
			strengths: ['Water', 'Ground', 'Rock']
		},
		{
			name: 'Ice',
			immunes: [],
			weaknesses: ['Fire', 'Water', 'Ice', 'Steel'],
			strengths: ['Grass', 'Ground', 'Flying', 'Dragon']
		},
		{
			name: 'Fighting',
			immunes: ['Ghost'],
			weaknesses: ['Poison', 'Flying', 'Psychic', 'Bug', 'Fairy'],
			strengths: ['Normal', 'Ice', 'Rock', 'Dark', 'Steel']
		},
		{
			name: 'Poison',
			immunes: ['Steel'],
			weaknesses: ['Poison', 'Ground', 'Rock', 'Ghost'],
			strengths: ['Grass', 'Fairy']
		},
		{
			name: 'Ground',
			immunes: ['Flying'],
			weaknesses: ['Grass', 'Bug'],
			strengths: ['Fire', 'Electric', 'Poison', 'Rock', 'Steel']
		},
		{
			name: 'Flying',
			immunes: [],
			weaknesses: ['Electric', 'Rock', 'Steel'],
			strengths: ['Grass', 'Fighting', 'Bug']
		},
		{
			name: 'Psychic',
			immunes: ['Dark'],
			weaknesses: ['Psychic', 'Steel'],
			strengths: ['Fighting', 'Poison']
		},
		{
			name: 'Bug',
			immunes: [],
			weaknesses: ['Fire', 'Fighting', 'Poison', 'Flying', 'Ghost', 'Steel', 'Fairy'],
			strengths: ['Grass', 'Psychic', 'Dark']
		},
		{
			name: 'Rock',
			immunes: [],
			weaknesses: ['Fighting', 'Ground', 'Steel'],
			strengths: ['Fire', 'Ice', 'Flying', 'Bug']
		},
		{ name: 'Ghost', immunes: ['Normal'], weaknesses: ['Dark'], strengths: ['Psychic', 'Ghost'] },
		{ name: 'Dragon', immunes: ['Fairy'], weaknesses: ['Steel'], strengths: ['Dragon'] },
		{
			name: 'Dark',
			immunes: [],
			weaknesses: ['Fighting', 'Dark', 'Fairy'],
			strengths: ['Psychic', 'Ghost']
		},
		{
			name: 'Steel',
			immunes: [],
			weaknesses: ['Fire', 'Water', 'Electric', 'Steel'],
			strengths: ['Ice', 'Rock', 'Fairy']
		},
		{
			name: 'Fairy',
			immunes: [],
			weaknesses: ['Fire', 'Poison', 'Steel'],
			strengths: ['Fighting', 'Dragon', 'Dark']
		}
	];

    let attacking = true;
    function changeMode(){
        attacking = !attacking;
    }
    
</script>

<div class="container">
	<div class="row">
        <div class="box-container">
            <button on:click={changeMode}>Toggle</button>
        </div>
		{#each types as defender}
			<div class="box-container">
				<p>{defender.name}</p>
			</div>
		{/each}
	</div>
	<div class="col">
		{#each types as attacker}
			<div class="row">
				<div class="box-container">
					<p class="col-item">{attacker.name}</p>
				</div>
				{#each types as defender}
					{#if attacker.weaknesses.includes(defender.name)}
						<div class="box-container w">
							<img class="box" src="images/{attacking ? defender.name.toLowerCase() : attacker.name.toLowerCase()}.png" alt={defender.name} />
						</div>
					{:else if attacker.strengths.includes(defender.name)}
						<div class="box-container s">
							<img class="box" src="images/{attacking ? defender.name.toLowerCase() : attacker.name.toLowerCase()}.png" alt={defender.name} />
						</div>
					{:else if attacker.immunes.includes(defender.name)}
						<div class="box-container i">
							<img class="box" src="images/{attacking ? defender.name.toLowerCase() : attacker.name.toLowerCase()}.png" alt={defender.name} />
						</div>
					{:else}
						<div class="box-container">
							<img class="box" src="images/{attacking ? defender.name.toLowerCase() : attacker.name.toLowerCase()}.png" alt={defender.name} />
						</div>
					{/if}
				{/each}
			</div>
		{/each}
	</div>
</div>

<style lang="scss">
	* {
		margin: 0;
		padding: 0;
	}

	.container {
		background-color: #1e1e2e; 
        color: white;
	}

	.box-container {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 5rem;
		aspect-ratio: 1/1;
		border: 0.5px solid black;
	}

	.box {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 3rem;
		aspect-ratio: 1/1;
	}

	.i {
		background-color: gray;
	}
	.w {
		background-color: red;
	}
	.s {
		background-color: green;
	}

	.col {
		display: flex;
		flex-direction: column;
	}

	.col::first-of-type() {
		margin-top: 1rem;
	}

	.col-item {
		padding: 1rem;
	}

	.row {
		display: flex;
		flex-direction: row;
		margin-left: 6rem;
		border: 1px solid black;
	}

	.row::first-of-type() {
		margin-left: 6rem;
	}
</style>
