<div class="heroContainer">
	<div class="heroContent">
		<h1>Nuric Productions</h1>
		<p>Elevating Your Events with Premier Entertainment Solutions</p>
	</div>
</div>

<style>
	@property --textGradientX {
		syntax: '<percentage>';
		inherits: false;
		initial-value: 0%;
	}
	@property --textGradientY {
		syntax: '<percentage>';
		inherits: false;
		initial-value: 100%;
	}

	@keyframes textGradientShine {
		0% {
			--textGradientX: 100%;
			--textGradientY: 0%;
		}
		25% {
			--textGradientX: 100%;
			--textGradientY: 100%;
		}
		50% {
			--textGradientX: 0%;
			--textGradientY: 100%;
		}
		75% {
			--textGradientX: 0%;
			--textGradientY: 0%;
		}
		100% {
			--textGradientX: 100%;
			--textGradientY: 0%;
		}
	}

	.heroContainer {
		font-family: 'Roboto', sans-serif;
		display: grid;
		place-items: center;
		height: calc(100vh - 350px);
	}
	.heroContent {
		text-align: right;
		width: calc(100% - 4rem);
		max-width: 700px;
		h1 {
			font-size: clamp(2.5rem, 7vw, 6rem);
			font-weight: 800;
			text-transform: uppercase;
			background:
				radial-gradient(
					ellipse farthest-corner at right bottom,
					#fedb37 0%,
					#fdb931 16%,
					#9f7928 30%,
					#8a6e2f 40%,
					transparent 80%
				),
				radial-gradient(
					ellipse farthest-corner at var(--textGradientX) var(--textGradientY),
					#fff 0%,
					#f9fca1 25%,
					#d8a520 50%,
					#b1740e 75%,
					#a36406 100%
				);
			margin: 0;
			background-clip: text;
			-webkit-text-fill-color: transparent;
			color: #fff;
			animation: textGradientShine 12s ease-in-out infinite;
		}
		p {
			font-size: clamp(1.8rem, 4vw, 3.5rem);
			text-wrap: balance;
		}
	}
</style>
