<script>
  import { account } from "../../store";
  let address;
  account.subscribe((value) => {
    address = value;
  });
</script>

<main>
  <h1>CCIP 예제</h1>

  {#if address.length > 0}
    <p>현재 연결된 계정: {address}</p>
  {:else}
    <p>MetaMask 계정에 연결 중...</p>
  {/if}
</main>

<style>
  /* 기본 스타일링 */
  main {
    text-align: center;
    margin: 2rem;
  }
</style>
