<script>
	import Layout from "$lib/+layout.svelte";
	import Footer from "$lib/+footer.svelte";

	let clicks = 0;

	async function SummonEmu(trigger, event) {
		if (trigger == "click" && event.pointerType != "mouse") return;

		let body = document.querySelector("body");
		let score = document.getElementById("score");
		let img = document.createElement("img");
		let audio = document.createElement("audio");

		let size = 100 + Math.floor(Math.random() * 100);
		let angle = Math.floor(Math.random() * 360);
		let coord_y = 2 + Math.floor(Math.random() * 50);
		let coord_y_from = ["top", "bottom"][Math.floor(Math.random() * 2)];
		let coord_x = 2 + Math.floor(Math.random() * 50);
		let coord_x_from = ["left", "right"][Math.floor(Math.random() * 2)];

		clicks++;

		img.src = "./pictures/emuotori.png";
		img.style = `width: ${size}px; ${coord_y_from}: ${coord_y}%; ${coord_x_from}: ${coord_x}%; position: absolute; transform: rotate(${angle}deg); user-select: none; pointer-events: none;`;
		img.alt = "Emu Otori";

		audio.src = "./audios/emuotori.mp3";
		audio.volume = 0.4;

		score.innerHTML = clicks;

		body.appendChild(img);
		body.appendChild(audio);

		audio.play();

		setTimeout(() => {
			audio.pause();

			audio.currentTime = 0;
			audio.src = "";

			body.removeChild(img);
			body.removeChild(audio);
		}, 3000);
	}
</script>

<Layout>
	<div
		class="top-0 bottom-0 left-0 right-0 absolute"
		on:click={event => SummonEmu("click", event)}
		on:touchstart={event => SummonEmu("touch", event)}
	>
		<div
			class="w-fit h-auto bg-[#ffffff] px-[10px] mt-[75px] mx-auto rounded-lg"
		>
			<p class="text-[25px] text-[#5a6dfa]">EmuOtori</p>
		</div>

		<div class="w-full h-auto">
			<p id="score" class="text-[30px] text-[#ffffff] mt-[25px]">0</p>
		</div>

		<div
			class="w-fit h-auto bg-[#ffffff] text-center mt-[325px] px-[10px] mx-auto rounded-lg"
		>
			<p class="text-[19px] text-[#5a6dfa]">Click Anywhere To Summon Emu!</p>
		</div>

		<Footer />
	</div>
</Layout>
