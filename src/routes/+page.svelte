<script>
	import Layout from "$lib/+layout.svelte";

	let clicks = 0;

	async function SummonEmu(trigger) {
		if (trigger == "click" && event.pointerType != "mouse") return;

		let body = document.querySelector("body");
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

		body.appendChild(img);
		body.appendChild(audio);

		audio.play();

		setTimeout(() => {
			audio.pause();

			audio.currentTime = 0;
			audio.src = audio.src;

			body.removeChild(img);
			body.removeChild(audio);
		}, 3000);
	}
</script>

<Layout>
	<div
		class="top-0 right-0 bottom-0 left-0 absolute"
		on:click={event => SummonEmu("click", event)}
		on:touchstart={event => SummonEmu("touch", event)}
	></div>

	<div class="mt-[75px]">
		<div class="w-fit bg-[#ffffff] px-2 mx-auto rounded-lg">
			<p class="text-[30px] text-[#5a6dfa]">EmuOtori</p>
		</div>

		<p id="score" class="text-[40px] text-[#ffffff] mt-[25px]">0</p>

		<div class="w-fit bg-[#ffffff] mt-[325px] px-2 mx-auto rounded-lg">
			<p class="text-[19px] text-[#5a6dfa]">Click Everywhere To Summon Emu!</p>
		</div>
	</div>
</Layout>
