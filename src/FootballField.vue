<template>
	<div class="field-and-players__wrapper">
		<div class="perspective-wrapper">
			<div class="football-field__wrapper">
				<ul class="football-field__stripes">
					<li class="football-field__stripe" v-for="stripe in 7"></li>
				</ul>
				<div class="football-field__inner-content">
					<div class="football-field__middle-line">
						<div class="football-field__circle"></div>
					</div>
					<div class="back-rectangle__wrapper">
						<div class="back-rectangle__goalkeeper"></div>
					</div>
				</div>
				<span class="dummy-rect-1"></span>
				<span class="dummy-rect-2"></span>
			</div>
		</div>
		<div class="football-players__wrapper">
			<slot></slot>
		</div>
	</div>
</template>
<style lang="scss">
.field-and-players__wrapper {
	--grass: #6d9332;
	--white-lines: #b5d684;
	--stripe-lines: #6d9430;
	position: relative;
	flex: 1;
	&.is-blurred::before {
		content: "";
		position: fixed;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(black, 0.4);
		backdrop-filter: blur(20px);
		z-index: 3;
	}
}
.football-players__wrapper {
	position: absolute;
	top: 0;
	width: 100%;
	height: 100%;
	padding-top: 0px;
	display: flex;
	flex-direction: column;
	flex: 1;
	align-items: stretch;
	z-index: 2;
	> ul {
		display: flex;
		align-items: flex-end;
		justify-content: space-around;
		flex: 1;
		li {
			flex: 1;
		}
	}
}
.perspective-wrapper {
	perspective: 30cqw;
	@media (orientation: portrait) {
		perspective: 65cqw;
	}
}
.football-field {
	&__wrapper {
		padding: 8px;
		display: flex;
		aspect-ratio: 11/10;
		background-color: var(--grass);
		transform: rotateX(5deg);
		border-radius: 6px;
		border-bottom-left-radius: 0px;
		border-bottom-right-radius: 0px;
		@media (orientation: portrait) {
			aspect-ratio: 9/16;
		}
		&::after {
			content: "";
			position: absolute;
			bottom: -10px;
			left: 0px;
			height: 10px;
			width: 100%;
			background-color: #283f0a;
			transform: rotate(180deg) rotateX(365deg);
		}
		.dummy-rect-1,
		.dummy-rect-2 {
			position: absolute;
			bottom: -10px;
			left: -8.5px;
			height: 10px;
			width: 10px;
			background-color: var(--bg-color);
			transform: skewX(20deg);
			z-index: 2;
		}
		.dummy-rect-2 {
			left: auto;
			right: -8.5px;
			transform: skewX(-20deg);
		}
	}
	&__inner-content {
		position: relative;
		display: flex;
		container-type: size;
		border: solid 2px var(--white-lines);
		flex: 1;
		border-radius: 4px;
		border-bottom-left-radius: 0px;
		border-bottom-right-radius: 0px;
	}
	&__middle-line {
		opacity: 0;
		position: absolute;
		width: 100%;
		height: 2px;
		background-color: var(--white-lines);
		top: calc(50% - 1px);
	}
	&__circle {
		position: absolute;
		top: 50%;
		left: 50%;
		translate: -50% -50%;
		width: 20cqh;
		height: 20cqh;
		border-radius: 100%;
		border: solid 2px var(--white-lines);
	}
	&__stripes {
		display: flex;
		position: absolute;
		top: 0px;
		left: 0px;
		width: 100%;
		height: 100%;
		z-index: 1;
		> li {
			flex: 1;
		}
		> li:nth-child(2n) {
			background-color: rgba(black, 0.05);
		}
	}
}

.back-rectangle {
	&__wrapper {
		position: absolute;
		bottom: 0px;
		width: 60cqw;
		height: 30cqh;
		left: 50%;
		transform: translateX(-50%);
		border: solid 2px var(--white-lines);
		border-bottom: none;
		background-color: var(--grass);
	}
	&__goalkeeper {
		position: absolute;
		bottom: 0px;
		width: 22cqw;
		height: 12cqh;
		left: 50%;
		transform: translateX(-50%);
		border: solid 2px var(--white-lines);
		border-bottom: none;
	}
}
</style>
