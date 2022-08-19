<script>
import { blur, slide, fly, scale, fade } from 'svelte/transition';
</script>

<div class="modal-container" in:blur out:fade>
 <div class="modal-content" transition:blur>
  <slot><!-- optional fallback --></slot>
 </div>
</div>



