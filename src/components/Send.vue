<template>
	<div class="container-send">
		<div class="wrapper">
			<h2 class="title">Envoyer des token</h2>
			<form>
				<div class="container-input">
					<input
						type="text"
						id="adresse"
						class="input text-sm rounded-lg block w-full p-2.5"
						placeholder="Adresse du destinataire"
						required
					/>
                </div>
                <div class="container-input2">
                    <input
						type="text"
						id="montant"
						class="input2 text-sm rounded-lg block w-full p-2.5"
						placeholder="Montant"
						required
					/>
					<button type="submit" class="text-black gold-bg text-center">Envoyer</button>
				</div>
			</form>
			
		</div>
	</div>
</template>

<style scoped>
	.container-send {
		margin-bottom: 2em;
		display: flex;
		justify-content: center;
	}
	.wrapper{
		display: flex;
		flex-direction: column;
		align-items: start;
	}
	.title {
		color: #ffffff;
		font-weight: 400;
		font-size: 20px;
		margin-bottom: 0.5em;
	}
	.container-input {
		display: flex;
		justify-content: space-between;
		align-items: center;
		width: 40vw;
	}
    .container-input2 {
		display: flex;
		justify-content: space-between;
		align-items: center;
		width: 30vw;
        margin-top: 1em;
	}
	.input {
		width: 30vw;
	}

    .input2 {
		width: 15vw;
	}
	.input:focus {
    outline: none !important;
    border:2px solid #fbbf24;
	margin: -2px;
    }
    
	.icon {
		height: 20px;
	}
</style>
