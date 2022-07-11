<template>
	<header>
		<router-link to="/">
			<h1><span>Vue</span> Movies Kinopoisk</h1>
		</router-link>
	</header>
	<main>
		<router-view></router-view>
	</main>
</template>

<style lang="scss">
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: 'Fira Sans',sans-serif;
		&::selection {
			background: transparentize(#42b883,0.5);
		}
}
body {
	background: #1f1f1f;
}
a {
	text-decoration: none;
}

header {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 10px 15px;
	background: #2c3d4e;
	box-shadow: 0 0 6px rgba(0,0,0,0.1);
}
h1 {
	color:#fff;
	font-size: 28px;
	span {
		color:#42b883
	}
}
</style>
