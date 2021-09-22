# svelte-monetization

> A minimal and lightweight wrapper for the Web Monetization API.

## Installation

```bash
$ npm install svelte-monetization
```

## Usage

### Add Svelte Monetization to your project

```svelte
<script>
  import Monetization from "svelte-monetization";

  function handleProgress(event) {
    console.log(event.detail);
  }
</script>

<!-- Set up your payment pointer in your App.svelte -->
<svelte:head>
  <meta
    name="monetization"
    content="$coil.xrptipbot.com/701298d5-481d-40ff-9945-336671ab2c42" />
</svelte:head>

<Monetization
  let:isMonetized
  let:isLoading
  on:progress={handleProgress}>
  {#if isLoading}
    <div>Loading message here</div>
  {:else if isMonetized}
    <div>Monetized/premium content here</div>
  {:else}
    <div>Show ads here</div>
  {/if}
</Monetization>
```

### Events

You can also listen to [Web Monetization browser events](https://webmonetization.org/docs/api#browser-events) via Component events.

- `start`

  Fires when Web Monetization has started actively paying.

- `progress`

  Fires when a payment comes in.

- `stop`

  Used to determine when Web Monetization has stopped.

- `pending`

  Used to determine when Web Monetization is enabled

## Use case examples

- Hide existing ads when Web Monetization is enabled
- Content that can be viewed only when Web Monetization is enabled
- Total amount of payment stored for each user in database etc, utilized for premium content

## License

This plugin is released under the [MIT License](LICENSE.md).
