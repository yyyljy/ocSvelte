<script>
  import welcome from "$lib/images/svelte-welcome.webp";
  import welcome_fallback from "$lib/images/svelte-welcome.png";
  import wallet from "$lib/images/wallet.png";
  import { account } from "../store";
  import { browser } from "$app/environment";

  if (browser && !account?.length && localStorage.getItem("walletAccount")) {
    account.set(localStorage.getItem("walletAccount"));
  }

  let login = () => {
    if (typeof window.ethereum === "undefined") {
      console.error("MetaMask를 찾을 수 없습니다. 먼저 설치하세요.");
      return;
    }

    window.ethereum
      .request({ method: "eth_requestAccounts" })
      .then((result) => {
        account.set(result);
        localStorage.setItem("walletAccount", result);
      })
      .catch((error) => {
        console.error(
          "MetaMask 계정에 연결하는 중 오류가 발생했습니다.",
          error
        );
      });
  };
</script>

<svelte:head>
  <title>Home</title>
  <meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
  <span class="welcome">
    <picture>
      <source srcset={welcome} type="image/webp" />
      <img src={welcome_fallback} alt="Welcome" />
    </picture>
  </span>
  <button class="btn" on:click={login}>
    <img class="wallet" src={wallet} alt="wallet" />
  </button>
  <p>{$account ? `Address:` + $account : ""}</p>
</section>

<style>
  section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    flex: 0.6;
  }

  .welcome {
    display: block;
    position: relative;
    width: 100%;
    height: 0;
    padding: 0 0 calc(100% * 495 / 2048) 0;
  }

  .welcome img {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    display: block;
  }

  .wallet {
    width: 100%;
    height: 100%;
  }

  .btn {
    width: 15%;
    border: 0px;
    background-color: transparent;
  }
</style>
