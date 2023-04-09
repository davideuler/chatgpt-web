<script lang="ts">
    import { get } from 'http';
  import { apiKeyStorage } from './Storage.svelte'

  $: apiKey = $apiKeyStorage
</script>

<article class="message">
  <div class="message-body" on:load={(event) => {
    //apiKeyStorage.set("12345")
  }}>
    <strong><a href="https://github.com/ihopeit/brain-assistant">Brain Assistant</a></strong>
    is a simple one-page web interface to the Brain Assistant Login API. To use it, you need to login by Wechat.
    All messages are stored in your browser's local storage, so everything is
    <strong>private</strong>. You can also close the browser tab and come back later to continue the conversation.
  </div>
</article>
<article class="message" class:is-danger={!apiKey} class:is-warning={apiKey}>
  <div class="message-body">
    
    <script lang="javascript">
      api_key = localStorage.getItem("scan_key");
      if (api_key === undefined || api_key === null) {
        // redirect to login page
        window.location.href = "/v1/login"
      }else{
        localStorage.setItem("apiKey", '"' + api_key + '"');
        console.log("api_key set");
      }

    </script>

    点击左侧<a href={'#/chat/new'}>创建会话</a>来开始一个会话

    <form
      class="field has-addons has-addons-right"
      on:submit|preventDefault={(event) => {
        if (event.target && event.target[0].value) {
        apiKeyStorage.set(event.target[0].value)
        }
      }}
    >
      
    </form>

  </div>
</article>
{#if apiKey}
  <article class="message is-info">
    <div class="message-body">
      Select an existing chat on the sidebar, or
      <a href={'#/chat/new'}>create a new chat</a>
    </div>
  </article>
{/if}
