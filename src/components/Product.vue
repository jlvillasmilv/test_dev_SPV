<template>
	<div class="card">
		<div class="card-image">
			<figure class="image is-1by1">
				<img  :alt="pd.name" :src="pd.img" >
			</figure>
		</div>
		<div class="card-content">
			<div class="media">
				<div class="media-left">
					<div class="media-content">
						<p class="title is-6"><strong>{{pd.name}}</strong></p>
						<p class="subtitle is-6">$ {{pd.price}}</p>
						<p class="subtitle is-6">Available  {{ pd.available }}</p>
						<p class="subtitle is-6">Best_seller  {{ pd.best_seller }}</p>
						<p class="subtitle is-6">Categories  {{ pd.categories }}</p>
					</div>
				</div>

			</div>
			<div class="content">
				<p class="subtitle">{{pd.description}}</p>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		props: {
			pd: { type: Object, required: true }
		},

	}
</script>

<style type="text/css">
	
</style>