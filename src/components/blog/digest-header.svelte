<script lang="ts">
  import Modal from "../modal.svelte";
  import TwitterFollowButton from "../t-button.svelte";
  import Signup from "../signup.svelte";
  let isNewsLetterFormShown: boolean = false;

  const handleClose = () => {
    isNewsLetterFormShown = false;
  };
</script>

<style lang="postcss">
  header {
    @apply mb-0 !important;
  }

  header h1 + p {
    @apply text-p-medium;
  }
</style>

<header class="mb-0">
  <h1>DevX Digest</h1>
  <p>Our newsletter where we cover everything about Developer Experience</p>
  <p class="mt-micro text-base">
    <button class="btn-primary" on:click={() => (isNewsLetterFormShown = true)}
      >Signup for the Newsletter</button
    >
    <TwitterFollowButton trackingContext="Digest" class="btn-secondary" />
  </p>
</header>

<Modal isOpen={isNewsLetterFormShown} on:close={handleClose}>
  <Signup type="newsletter" />
</Modal>
