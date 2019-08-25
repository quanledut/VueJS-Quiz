<template>
  <b-nav>
    <b-nav-item disabled>
      <b>Fancy Quiz App</b>
    </b-nav-item>
    <b-nav-item disabled>
      Counter: {{currentIndex}}/{{total}}
    </b-nav-item>
  </b-nav>
</template>

<script>
	export default {
		props: {
			total: Number,
			currentIndex: Number
		}
	}
</script>