<script lang="ts">
	import { Graphics, Text } from 'pixi-svelte';
	import { getContext } from '../game/context';

	const context = getContext();
	const canvas = $derived(context.stateLayoutDerived.canvasSizes());
	let characterY = $state(0.22);
	let multiplier = $state(1.00);
</script>

<Graphics
	draw={(graphics) => {
		const width = canvas.width;
		const height = canvas.height;

		// Ciel parisien
		graphics.rect(0, 0, width, height);
		graphics.fill(0x87ceeb);

		// Sol
		graphics.rect(0, height * 0.86, width, height * 0.14);
		graphics.fill(0x426b3a);

		// Tour Eiffel stylisée
		const cx = width / 2;
		const top = height * 0.12;
		const bottom = height * 0.86;

		graphics.poly([
			cx, top,
			cx - width * 0.18, bottom,
			cx - width * 0.11, bottom,
			cx, top + height * 0.12,
			cx + width * 0.11, bottom,
			cx + width * 0.18, bottom,
		]);

		graphics.stroke({
			width: Math.max(5, width * 0.008),
			color: 0x3a302b,
			alpha: 1,
		});
	}}
/>

<Text
	x={canvas.width / 2}
	y={canvas.height * 0.06}
	anchor={{ x: 0.5, y: 0 }}
	text="EIFFEL TOWER"
	style={{
		fontFamily: 'Arial',
		fontSize: Math.max(28, canvas.width * 0.04),
		fontWeight: '700',
		fill: 0xffffff,
	}}
/>

<Graphics x={canvas.width / 2} y={canvas.height * characterY} draw={(graphics) => { graphics.circle(0, 0, 22); graphics.fill(0xffd2a6); }} />
<Graphics x={canvas.width / 2} y={canvas.height * characterY + 22} draw={(graphics) => { graphics.roundRect(-14, 0, 28, 42, 8); graphics.fill(0xe63946); }} />

<Graphics x={canvas.width / 2} y={canvas.height * characterY + 32} draw={(g) => { g.moveTo(-12, 4); g.lineTo(-38, 20); g.moveTo(12, 4); g.lineTo(38, 20); g.stroke({ width: 8, color: 0xffd2a6 }); }} />
<Text text={`${multiplier.toFixed(2)}x`} />
