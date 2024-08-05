<script>
	let enteredPassword = "";
	let passwordValidity = "short";
	let passwordsArray = [];
	$: if (enteredPassword.trim().length < 5) {
		passwordValidity = "Too short";
	} else if (enteredPassword.trim().length > 10) {
		passwordValidity = "Too long";
	} else {
		passwordValidity = "valid";
	}
	function addToPasswordsArray() {
		if (passwordValidity === "valid") {
			passwordsArray = [...passwordsArray, enteredPassword];
		}
	}
	function removeFromArray(index) {
		passwordsArray = passwordsArray.filter((pw, idx) => {
			return idx !== index;
		});
	}
</script>

<h1>Assignment</h1>

<p>Solve these tasks.</p>

<ol>
	<li>Add a password input field and save the user input in a variable.</li>
	<li>
		Output "Too short" if the password is shorter than 5 characters and "Too
		long" if it's longer than 10.
	</li>
	<li>
		Output the password in a paragraph tag if it's between these boundaries.
	</li>
	<li>Add a button and let the user add the passwords to an array.</li>
	<li>Output the array values (= passwords) in a unordered list (ul tag).</li>
	<li>Bonus: If a password is clicked, remove it from the list.</li>
</ol>

<div class="form-control">
	<label for="enteredPassword">Password Field</label>
	<input type="password" bind:value={enteredPassword} id="enteredPassword" />
</div>
<button on:click={addToPasswordsArray}>Add password</button>

{#if passwordValidity === "Too short"}
	<p>Password is too short</p>
{:else if passwordValidity === "Too long"}
	<p>Password is too long</p>
{:else}
	<p>Password is valid: {enteredPassword}</p>
{/if}
<ul>
	{#each passwordsArray as password, i}
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<li on:click={removeFromArray.bind(this, i)}>
			<p>{password}</p>
		</li>
	{/each}
</ul>
<p>please start adding some passwords</p>
