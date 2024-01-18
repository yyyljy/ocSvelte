<script>
  import { page } from "$app/stores";

  const connectWallet = async () => {
    // MetaMask가 설치되어 있지 않으면 에러 처리
    if (typeof window.ethereum === "undefined") {
      console.error("MetaMask를 찾을 수 없습니다. 먼저 설치하세요.");
      return;
    }

    // MetaMask에 연결
    window.ethereum
      .request({ method: "eth_requestAccounts" })
      .then((result) => {
        accounts = result;
      })
      .catch((error) => {
        console.error(
          "MetaMask 계정에 연결하는 중 오류가 발생했습니다.",
          error
        );
      });
  };
</script>

<header>
  <nav>
    <svg viewBox="0 0 2 3" aria-hidden="true">
      <path d="M0,0 L1,2 C1.5,3 1.5,3 2,3 L2,0 Z" />
    </svg>
    <ul>
      <li aria-current={$page.url.pathname === "/" ? "page" : undefined}>
        <a href="/">Home</a>
      </li>
      <li aria-current={$page.url.pathname === "/ERC4337" ? "page" : undefined}>
        <a href="/erc4337">ERC4337</a>
      </li>
      <li
        aria-current={$page.url.pathname.startsWith("/CCIP")
          ? "page"
          : undefined}
      >
        <a href="/ccip">CCIP</a>
      </li>
      <li
        aria-current={$page.url.pathname.startsWith("/QRMAZE")
          ? "page"
          : undefined}
      >
        <a href="/qrmaze">QRMAZE</a>
      </li>
    </ul>
    <svg viewBox="0 0 2 3" aria-hidden="true">
      <path d="M0,0 L0,3 C0.5,3 0.5,3 1,2 L2,0 Z" />
    </svg>
  </nav>
</header>

<style>
  header {
    display: flex;
    justify-content: space-evenly;
  }

  nav {
    display: flex;
    justify-content: center;
    --background: rgba(255, 255, 255, 0.7);
  }

  svg {
    width: 2em;
    height: 3em;
    display: block;
  }

  path {
    fill: var(--background);
  }

  ul {
    position: relative;
    padding: 0;
    margin: 0;
    height: 3em;
    display: flex;
    justify-content: center;
    align-items: center;
    list-style: none;
    background: var(--background);
    background-size: contain;
  }

  li {
    position: relative;
    height: 100%;
  }

  li[aria-current="page"]::before {
    --size: 6px;
    content: "";
    width: 0;
    height: 0;
    position: absolute;
    top: 0;
    left: calc(50% - var(--size));
    border: var(--size) solid transparent;
    border-top: var(--size) solid var(--color-theme-1);
  }

  nav a {
    display: flex;
    height: 100%;
    align-items: center;
    padding: 0 0.5rem;
    color: var(--color-text);
    font-weight: 700;
    font-size: 0.8rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    text-decoration: none;
    transition: color 0.2s linear;
  }

  a:hover {
    color: var(--color-theme-1);
  }
</style>
