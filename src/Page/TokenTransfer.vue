<script setup>
import Header from '../components/Header.vue'
import Footer from '../components/Footer.vue'
import Adresse from '../components/Adresse.vue'
import Send from '../components/Send.vue'
</script>

<template>
	<div class="container-page">
    <Header />  
    <Adresse />
    <Send />
    
		<h1>Transfert de Tokens</h1>
		<form @submit.prevent="transferTokens">
			<label>Adresse du destinataire:</label>
			<input type="text" v-model="recipientAddress" />
			<label>Montant de transfert:</label>
			<input type="text" v-model="transferAmount" />
			<button type="submit">Transférer</button>
		</form>
		<br />
		<p>Adresse à Loic <br>0x4Da0Cf30D8931259A65bf2F74b6807Df8CEdB1f6</p>
		<p v-if="transactionHash">Transaction hash: {{ transactionHash }}</p>
	</div>

  <Footer />
</template>

<style scoped>
	.container-page {
		height: 100vh;
	}
</style>

<script>
	import Web3 from "web3";
	import { toWei } from "web3-utils";

	export default {
		data() {
			return {
				recipientAddress: "",
				transferAmount: "",
				transactionHash: "",
			};
		},
		methods: {
			async transferTokens() {
				console.log(this.recipientAddress)
				console.log(this.transferAmount)

				// Connect to Ethereum network
				const web3 = new Web3(window.ethereum);

				// Get the user's accounts
				const accounts = await web3.eth.requestAccounts();

				// Set contract address and ABI
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

				// Load the contract
				const contract = new web3.eth.Contract(contractAbi, contractAddress);

				// Format transfer amount
				const transferAmountWei = toWei(this.transferAmount, "ether");

				// Perform the transfer
				const result = await contract.methods.transfer(this.recipientAddress, transferAmountWei).send({ from: accounts[0] });

				// Update transaction hash
				this.transactionHash = result.transactionHash;
				console.log(this.transactionHash)
			},
		},
	};
</script>
