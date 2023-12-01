<template>
	<div class="container-adresse">
		<div class="wrapper">
			<h2 class="title">Saisissez l'adresse de votre wallet</h2>
			<form>
				<div class="container-input">
					<input
						type="text"
						id="adresse"
						class="input text-sm rounded-lg block w-full p-2.5"
						placeholder="Adresse wallet"
						required
					/>
					<button type="submit" class="text-white gold-bg text-center ">
						<img class="icon" src="../../public/fleche.svg" alt="fleche" />
					</button>
				</div>
			</form>
			
		</div>
	</div>
</template>

<style scoped>
	.container-adresse {
		margin-bottom: 3em;
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
		font-size: 16px;
		margin-bottom: 0.5em;
	}
	.container-input {
		display: flex;
		justify-content: space-between;
		align-items: center;
		width: 37.5vw;
	}
	.input {
		width: 30vw;
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
