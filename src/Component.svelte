<script>
  import { onDestroy, onMount, createEventDispatcher } from 'svelte'
  const dispatch = createEventDispatcher()
  
  let isLoading = true
  let isMonetized = true
  
  const monetizationEventCb = (ev) => {
      const eventName = ev.type.replace('monetization', '')
      dispatch(eventName, ev.detail)
  
      if (ev.type === 'monetizationstart') {
          isLoading = false
          isMonetized = true
      }
  }
  
  onMount(() => {
      if (!document.monetization) {
          isLoading = false
          isMonetized = false
          return
      }
  
      const { state } = document.monetization
  
      if (state === 'stopped') {
          isLoading = false
          isMonetized = false
      }
  
      document.monetization.addEventListener('monetizationstart', monetizationEventCb)
      document.monetization.addEventListener('monetizationstop', monetizationEventCb)
      document.monetization.addEventListener('monetizationprogress', monetizationEventCb)
      document.monetization.addEventListener('monetizationpending', monetizationEventCb)
  })
  
  onDestroy(() => {
      if (!document.monetization) return
  
      document.monetization.removeEventListener('monetizationstart', monetizationEventCb)
      document.monetization.removeEventListener('monetizationstop', monetizationEventCb)
      document.monetization.removeEventListener('monetizationprogress', monetizationEventCb)
      document.monetization.removeEventListener('monetizationpending', monetizationEventCb)
  })
  </script>
  
  <slot {isLoading} {isMonetized} />