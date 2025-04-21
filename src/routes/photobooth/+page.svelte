<div class="photoboothPage"></div>
<div class="container">
	<div class="description">
		<h1 class="pageTitle">Photobooth</h1>
		<p>
			Capture unforgettable moments with our professional photobooth services. Our photo booth
			packages include a range of customizable options, from traditional photo booths to digital
			photo booths. Our photo booth packages are perfect for weddings, birthdays, corporate events,
			and more.
		</p>
		<ul>
			<li>Digital Share Photo booth with ability to to print</li>
			<li>360 Photo Booth</li>
			<li>Video guest card for weddings or guest reactions</li>
		</ul>
	</div>
</div>

<style>
	.photoboothPage {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;

		min-height: 100vh;

		background:
			linear-gradient(to right bottom, rgba(0, 0, 0, 0.85), rgba(0, 0, 0, 0.25)),
			linear-gradient(to left top, rgba(0, 0, 0, 0.85), rgba(0, 0, 0, 0.25)),
			url('../../lib/images/photoBoothBg.webp') center center / cover fixed;
		z-index: -1;
	}
	.container {
		position: relative;
		z-index: 250;
	}
</style>
