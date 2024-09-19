<template>
	<pre
		v-pre
		class="language-javascript"
	><code ref="codeBlock">const message = 'Hello, World!';
console.log(message);</code></pre>
</template>

<script setup>
import { onMounted, ref } from "vue";
import Prism from "prismjs";
import "prismjs/themes/prism.css";
import "prismjs/components/prism-javascript";

const codeBlock = ref(null);

onMounted(() => {
	Prism.highlightElement(codeBlock.value);
});
</script>

<style></style>
