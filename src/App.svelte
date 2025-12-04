{#if showDecrypt}
<div>
  <h1>{decrypt}</h1>
  <input bind:value={inputD} type="text" placeholder="Text to decrypt">
  <button on:click={switchToEncrypt}>Back</button>
  {#if showCopyD}
    <button on:click={copyD}>Copy</button>
  {/if}
</div>
{/if}

{#if !showDecrypt}
<div>
  <h1>{encrypt}</h1>
  <input bind:value={inputE} type="text" placeholder="Text to encrypt">
  <button on:click={switchToDecrypt}>Next</button>
  {#if showCopyE}
    <button on:click={copyE}>Copy</button>
  {/if}
</div>
{/if}

<script>
  // define variables
  let showDecrypt = false;

  let inputE = "";
  let inputD = "";

  const defaultEncryptText = "Encrypted text will appear here...";
  const defaultDecryptText = "Decrypted text will appear here...";

  $: encrypt = inputE ? btoa(inputE) : defaultEncryptText;
  $: decrypt = inputD ? atob(inputD) : defaultDecryptText;


  // button functions
  function switchToDecrypt() {
    showDecrypt = true;
    inputE = "";
  }

  function switchToEncrypt() {
    showDecrypt = false;
    inputD = "";
  }


  // copy functions
  function copyE() {
    navigator.clipboard.writeText(encrypt);
  }

  function copyD() {
    navigator.clipboard.writeText(decrypt);
  }


  // don't show copy button if input is empty
  $: showCopyE = inputE.length > 0;
  $: showCopyD = inputD.length > 0;
</script>