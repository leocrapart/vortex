<script>
  import { onMount } from "svelte";

  let canvas;

  const particle_size = 10;
  const canvas_width = 500;
  const canvas_height = canvas_width;
  $: px = 10 + delta;
  $: py = 10 + delta;

  let cx = canvas_width / 2;
  let cy = canvas_height / 2;

  const radius = canvas_width / 3;
  const circle_start_angle = 0;
  const circle_end_angle = 2 * Math.PI;

  let delta = 0;
  let seconds = 0;
  const fps = 30;

  onMount(() => {
    const ctx = canvas.getContext("2d");

    // center
    ctx.fillStyle = "black";
    ctx.fillRect(cx, cy, particle_size, particle_size);

    // circle
    ctx.beginPath();
    ctx.arc(cx, cy, radius, circle_start_angle, circle_end_angle);
    ctx.stroke();

    const interval = setInterval(() => {
      delta += 1;
      // particle blue mooving
      ctx.fillStyle = "blue";
      ctx.fillRect(px, py, particle_size, particle_size);

      // eraser
      ctx.fillStyle = "white";
      ctx.fillRect(px - 5, py - 5, particle_size, particle_size);
    }, 1000 / fps);

    const interval_2 = setInterval(() => {
      seconds += 1;
    }, 1000);

    return () => {
      clearInterval(interval);
      clearInterval(interval_2);
    };
  });
</script>

<div>{seconds} s</div>
<div>{delta} frames</div>
<div>{fps} fps</div>

<canvas bind:this={canvas} width={canvas_width} height={canvas_height} />
