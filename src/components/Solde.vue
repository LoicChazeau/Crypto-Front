<template>
	<div class="container-solde">
		<div class="wrapper">
			<h2 class="title">Solde de votre compte</h2>
				<div class="box-solde">
					<div class="solde">10 000 $</div>
                </div>		
		</div>
	</div>
</template>

<style scoped>
	.container-solde {
		margin-bottom: 2em;
		display: flex;
		justify-content: center;
	}
	.wrapper{
		/* display: flex; */
		flex-direction: column;
		align-items: start;
	}
	.title {
		color: #ffffff;
		font-weight: 400;
		font-size: 20px;
		margin-bottom: 0.5em;
	}
    .box-solde {
        width: 37.5vw;
        height: 10vh;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .solde {
        background-color: #4B5563;
        width: 10vw;
        border-radius: 7.5px;
        padding: 12.5px;
        font-size: 20px;
        font-weight: 500;
    }
</style>
