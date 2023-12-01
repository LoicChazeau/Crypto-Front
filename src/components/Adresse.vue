<template>
	<div class="container-adresse">
		<div class="wrapper">
			<h2 class="title">Saisissez l'adresse de votre wallet</h2>
			<form  @submit.prevent="transferTokens">
				<div class="container-input">
					<input
						type="text"
						v-model="Adress"
						id="adresse"
						class="input text-sm rounded-lg block w-full p-2.5"
						placeholder="Adresse wallet"
						required
					/>
					<button type="submit" class="text-white gold-bg text-center " >
						<img class="icon" src="../../public/fleche.svg" alt="fleche" />
					</button>
				</div>
				{solde}
			</form>
			
		</div>
	</div>
</template>
<script>
	import Web3 from "web3";
	import { toWei } from "web3-utils";

	export default {
		data() {
			return {
				solde:0,
				Address:""
			};
		},
		methods: {
			async transferTokens() {
				const contractAddress = "0x6d5C183b957a6335e82bB97C02159db2ffa0f505";
				const contractAbi = [
					{
						anonymous: false,
						inputs: [
							{
								indexed: true,
								internalType: "address",
								name: "owner",
								type: "address",
							},
							{
								indexed: true,
								internalType: "address",
								name: "spender",
								type: "address",
							},
							{
								indexed: false,
								internalType: "uint256",
								name: "value",
								type: "uint256",
							},
						],
						name: "Approval",
						type: "event",
					},
					{
						anonymous: false,
						inputs: [
							{
								indexed: true,
								internalType: "address",
								name: "from",
								type: "address",
							},
							{
								indexed: true,
								internalType: "address",
								name: "to",
								type: "address",
							},
							{
								indexed: false,
								internalType: "uint256",
								name: "value",
								type: "uint256",
							},
						],
						name: "Transfer",
						type: "event",
					},
					{
						inputs: [
							{
								internalType: "address",
								name: "_spender",
								type: "address",
							},
							{
								internalType: "uint256",
								name: "_value",
								type: "uint256",
							},
						],
						name: "approve",
						outputs: [
							{
								internalType: "bool",
								name: "success",
								type: "bool",
							},
						],
						stateMutability: "nonpayable",
						type: "function",
					},
					{
						inputs: [
							{
								internalType: "address",
								name: "_to",
								type: "address",
							},
							{
								internalType: "uint256",
								name: "_value",
								type: "uint256",
							},
						],
						name: "transfer",
						outputs: [
							{
								internalType: "bool",
								name: "success",
								type: "bool",
							},
						],
						stateMutability: "nonpayable",
						type: "function",
					},
					{
						inputs: [
							{
								internalType: "address",
								name: "_from",
								type: "address",
							},
							{
								internalType: "address",
								name: "_to",
								type: "address",
							},
							{
								internalType: "uint256",
								name: "_value",
								type: "uint256",
							},
						],
						name: "transferFrom",
						outputs: [
							{
								internalType: "bool",
								name: "success",
								type: "bool",
							},
						],
						stateMutability: "nonpayable",
						type: "function",
					},
					{
						inputs: [
							{
								internalType: "string",
								name: "_name",
								type: "string",
							},
							{
								internalType: "string",
								name: "_symbol",
								type: "string",
							},
							{
								internalType: "uint8",
								name: "_decimals",
								type: "uint8",
							},
							{
								internalType: "uint256",
								name: "_totalSupply",
								type: "uint256",
							},
						],
						stateMutability: "nonpayable",
						type: "constructor",
					},
					{
						inputs: [
							{
								internalType: "address",
								name: "",
								type: "address",
							},
							{
								internalType: "address",
								name: "",
								type: "address",
							},
						],
						name: "allowance",
						outputs: [
							{
								internalType: "uint256",
								name: "",
								type: "uint256",
							},
						],
						stateMutability: "view",
						type: "function",
					},
					{
						inputs: [
							{
								internalType: "address",
								name: "",
								type: "address",
							},
						],
						name: "balanceOf",
						outputs: [
							{
								internalType: "uint256",
								name: "",
								type: "uint256",
							},
						],
						stateMutability: "view",
						type: "function",
					},
					{
						inputs: [],
						name: "decimals",
						outputs: [
							{
								internalType: "uint8",
								name: "",
								type: "uint8",
							},
						],
						stateMutability: "view",
						type: "function",
					},
					{
						inputs: [],
						name: "name",
						outputs: [
							{
								internalType: "string",
								name: "",
								type: "string",
							},
						],
						stateMutability: "view",
						type: "function",
					},
					{
						inputs: [],
						name: "symbol",
						outputs: [
							{
								internalType: "string",
								name: "",
								type: "string",
							},
						],
						stateMutability: "view",
						type: "function",
					},
					{
						inputs: [],
						name: "totalSupply",
						outputs: [
							{
								internalType: "uint256",
								name: "",
								type: "uint256",
							},
						],
						stateMutability: "view",
						type: "function",
					},
				];


				const web3 = new Web3(window.ethereum);
				const contract = new web3.eth.Contract(contractAbi, contractAddress);
				const result = await contract.methods.balanceOf(this.Address).send({ from: accounts[0] });
				this.solde = result
			}

		}
	}
</script>
<style scoped>
	.container-adresse {
		margin-bottom: 2.5em;
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
