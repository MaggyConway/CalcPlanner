<template>
	<div id="app">
		<home />
	</div>
</template>

<script>
import Home from './components/Home.vue'

export default {
	name: 'App',
	components: {
		Home
  }
}
</script>

<style>
* {
	margin: 0;
	padding: 0;
	-webkit-box-sizing: border-box;
		-moz-box-sizing: border-box;
				box-sizing: border-box;
	outline: none;
}
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	/* color: #2c3e50; */
	/* margin-top: 60px; */
}
</style>