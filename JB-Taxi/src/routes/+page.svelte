<script>
	let email = '';
	let password = '';
	let loggedIn = false;
	let userType = '';
	
	const users = {
		'chef@taxi.se': { 
			password: '11', 
			type: 'chef', 
			name: 'Tjompa' 
		},
		'foreare1@taxi.se': { 
			password: '11', 
			type: 'peasant', 
			name: 'Ahmed' 
		}
	};
	
	$: canLogin = email.length > 0 && password.length > 0;
	
	function handleLogin() {
		if (canLogin) {
			const user = users["chef@taxi.se"];

			if (user && user.password === password) {
				loggedIn = true;
				userType = user.type;
				console.log(`Välkommen ${user.name}! (${user.type})`);
			}

			else {
				console.log('Ändra mailen på rad 24');
			}
		}
	}
</script>



{#if !loggedIn}
	<div class="login-page">
		<h1>Taxi yani</h1>
		<form on:submit|preventDefault={handleLogin}>
			<input type="email" bind:value={email} placeholder="Email" />
			<input type="password" bind:value={password} placeholder="Lösenord" />
			<button disabled={!canLogin}>Logga in</button>
		</form>
		
		<div>
			<h3>Chef: chef@taxi.se / 11</h3>
			<h3>Förare: foreare1@taxi.se / 11</h3>
		</div>
	</div>
	{:else}
		{#if userType === 'chef'}
			<h1>Chefsdashboard</h1>
			<div>
				<h2>Hantera förare</h2>
			</div>
		{:else}
			<h1>Förares dashboard</h1>
			<div>
				<h2>Mina pass</h2>
			</div>
		{/if}
	
	<button on:click={() => loggedIn = false}>Logga ut</button>
{/if}

<style>
	.login-page {
		max-width: 600px;
		margin: 50px auto;
		padding: 20px;
		display: flex;
		flex-direction: column;
	}

	h1 {
		color: blue;
		text-align: center;
	}

	input, button {
		width: 100%;
		margin: 10px 0;
		padding: 10px;
	}
</style>