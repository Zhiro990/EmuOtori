<script>
	import Layout from "$lib/+layout.svelte";
	import Footer from "$lib/+footer.svelte";

	let clicks = 0;

	async function Click() {
		let main = document.querySelector("main");
		let score = document.getElementById("score");
		let img = document.createElement("img");
		let audio = document.createElement("audio");

		let size = 100 + Math.floor(Math.random() * 100);
		let angle = Math.floor(Math.random() * 360);
		let y = 1 + Math.floor(Math.random() * 68);
		let x = 1 + Math.floor(Math.random() * 53);

		clicks++;

		img.src = "./pictures/emuotori.png";
		img.style = `width: ${size}px; top: ${y}%; left: ${x}%; position: absolute; transform: rotate(${angle}deg); pointer-events: none;`;
		img.alt = "Emu Otori";

		audio.src = "./audios/emuotori.mp3";
		audio.volume = 0.4;

		score.innerHTML = clicks;

		main.appendChild(img);
		main.appendChild(audio);

		audio.play();

		setTimeout(() => {
			audio.pause();

			audio.currentTime = 0;
			audio.src = audio.src;

			main.removeChild(img);
			main.removeChild(audio);
		}, 3000);
	}
</script>

<Layout>
	<div class="w-full h-auto pt-[75px]">
		<p id="score" class="text-[21px] text-[#ffffff]">0</p>
		<button
			class="w-[75px] h-[75px] bg-[#ffffff] text-[#5a6dfa] mt-[300px] md:mt-[70%] shadow-2xl rounded-full"
			on:click={Click}
		>
			Click
		</button>
	</div>
	<Footer />
</Layout>
