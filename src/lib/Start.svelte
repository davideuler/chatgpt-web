<script lang="ts">
    import { get } from 'http';
  import { chatsStorage, apiKeyStorage } from './Storage.svelte'
  const redirect = (url, asLink = true) =>
  asLink ? (window.location.href = url) : window.location.replace(url);

  $: apiKey = $apiKeyStorage
  let api_key = localStorage.getItem("scan_key");

  if(api_key!== undefined && api_key!=null){
    let chat = $chatsStorage.find((chat) => chat.id === 1) 
    if(chat !== undefined){
      redirect("/chat/#/chat/1");
    }else {
      redirect("/chat/#/chat/new");
    }
  }

</script>