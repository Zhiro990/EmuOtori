<script>
	import Layout from "$lib/+layout.svelte";
	import Footer from "$lib/+footer.svelte";

	let clicks = 0;
	let playaudio = false;

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

		img.src = "./pictures/emuotori.webp";
		img.style = `width: ${size}px; ${coord_y_from}: ${coord_y}%; ${coord_x_from}: ${coord_x}%; position: absolute; transform: rotate(${angle}deg); user-select: none; pointer-events: none;`;
		img.alt = "Emu Otori";

		audio.src = "./audios/emuotori.mp3";
		audio.volume = playaudio ? 0.4 : 0;

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

	function ChangeAudioSetting() {
		let audiosettingbuttonimg = document.getElementById("audio-setting-button-img");

		audiosettingbuttonimg.src = "./pictures/audio-" + (playaudio ? "off" : "on") + ".svg";

		playaudio = !playaudio;
	}
</script>

<Layout>
	<div
		class="top-0 bottom-0 left-0 right-0 absolute"
		on:click={event => SummonEmu("click", event)}
		on:touchstart={event => SummonEmu("touch", event)}
	>
		<div
			class="w-fit h-auto bg-[#ffffff] px-[20px] py-[5px] mt-[75px] mx-auto rounded-lg select-none"
		>
			<p class="font-bold text-[21px] text-[#5a6dfa]">EmuOtori</p>
		</div>

		<div class="w-full h-auto mb-[390px] md:mb-[330px] select-none">
			<p id="score" class="text-[30px] text-[#ffffff] mt-[25px]">0</p>
		</div>

		<Footer />

		<div
			id="audio-setting"
			class="w-full md:w-fit h-fit flex mt-[12.5px] md:mt-0 items-center space-x-[15px] md:top-[20px] right-[25px] absolute"
		>
			<input
				type="range"
				id=""
				class=""
			/>

			<button
				id="audio-setting-button"
				class="size-fit"
				on:click={ChangeAudioSetting}
			>
				<img
					id="audio-setting-button-img"
					src="./pictures/audio-off.svg"
					class="size-[35px] md:size-[40px] select-none"
					alt="Audio Setting"
				/>
			</button>
		</div>
	</div>
</Layout>
