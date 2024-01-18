<script>
  import { account } from "../../store";
  import { browser } from "$app/environment";
  let address;
  if (browser) {
    address = localStorage.getItem("walletAccount");
  }
</script>

<main>
  <h1>ERC4337 예제</h1>

  {#if address?.length > 0}
    <p>현재 연결된 계정: {address}</p>
  {:else}
    <p>MetaMask 계정에 연결 중...</p>
  {/if}
</main>

<style>
  main {
    text-align: center;
    margin: 2rem;
  }
</style>
