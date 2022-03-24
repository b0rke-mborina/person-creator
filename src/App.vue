<template>
	<v-app>
		<v-app-bar app color="primary" dark>
			<h1 class="display-1">person-creator</h1>
			<v-spacer></v-spacer>
			<span class="mr-2">Web app</span>
		</v-app-bar>
		<v-main>
			<router-view/>
		</v-main>
	</v-app>
</template>
<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
