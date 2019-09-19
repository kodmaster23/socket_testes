<template>
  <q-page class="flex flex-center">

    <button @click="connectSocket()">PLAY!</button>

<ul>
  <li>new messages:</li>
  <li v-for="msg in msgs">
   {{ msg}}
  </li>
</ul>
  </q-page>
</template>

<style>
</style>

<script>
   import Echo from 'laravel-echo';

   const client = require('pusher-js');
   export default {
      name: 'PageIndex',
      data() {
         return {
            "msgs": []
         }
      },
      mounted() {

      },
      methods: {
         connectSocket(){
            console.log("entrou");
            const echo = new Echo({
               authEndpoint: 'https://demo.estardigital.cidatec.com.br/api/broadcasting/auth',
               broadcaster: 'pusher',
               key: "estar",
               wsHost: 'demo.estardigital.cidatec.com.br',
               wsPort: 6001,
               wssPort: 6001,
               enabledTransports: ['ws','wss'],
               disableStats: false,
               auth: {
                  headers: {
                     Authorization: "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjYzNzMwODZkMTA2YjY2ODkyYTE0NjQ0YjU5NjNlYjVkOTcyMzdjMGNmMWMzYmZkNGE0ZThlZWQzNzBlZjYxNWNkZTBiODYxZDhlMDNjYzgzIn0.eyJhdWQiOiIyIiwianRpIjoiNjM3MzA4NmQxMDZiNjY4OTJhMTQ2NDRiNTk2M2ViNWQ5NzIzN2MwY2YxYzNiZmQ0YTRlOGVlZDM3MGVmNjE1Y2RlMGI4NjFkOGUwM2NjODMiLCJpYXQiOjE1Njg5MTY1MzMsIm5iZiI6MTU2ODkxNjUzMywiZXhwIjoxNjAwNTM4OTMzLCJzdWIiOiIzNCIsInNjb3BlcyI6W119.qDzs9sbXKo26UOk6kajosj3Wz72v3vNyx1v6C3KSiTG1sFALAxo-fhBzjGgSmO8Bn0evftplnXVhe8j4hsDjYNYVv7EBK3XI-LbP_FWg-YaYwPHv_tDO0hMUno_bsIcu_ueBGFVHAS9S7LG0WoCpcxVnnVeAyAYeMyhl0NkVW_NLjaNUTaWD8yBIbhwBy25LOczE76eeUYlvwp5H-nVqhdjGHnJjwSISJocO5B5FBIBZOxpMNfKMrlB4hv5WJOBrrdyGzXCBz0klJEeGTbisYMrhA9HskM4NCd6Q0KuGSNVXHbdHW1azkzDOipaTgo4EKHKTRt8c4qa4hKldYub8IHCsrVY__t_7_UCqR5MqWZkaVI41a7RGrpdI6pOL_aKAhZLrzbhYhKJnWuJopzjtf5qN_YnMXNpSxgPVef3KSm1YTy1wiBXfiGk6aAje1eytaOup8gyqNPWbfeCaE9PnA4CZumhICMFuRVqiE8ZJLxU3a3bOd-bmY_dKE5gzLIixvq3QObrIfOFLgejHB18fsYbHumuWeysX6uTO5KdUKyrmUGQEfM32Wc-c6MbMcttp_8kbds2aCIlUHLhJYOimd7ITBMbdsnKPOBmxCsx-RRIINW4ac4F6rMwhDTvjEUdmu0mmwbGsRAVhbClOWCtSoBRKYiMxibdKPYcGyQzFmAc",
                     Accept:'application/json',
                     AccessingFrom: "backoffice"
                  },
               },
            });
            echo.private('agent_11')
               .listen('.new.vehicle.status', (e) => {
                  this.msgs.push(e.msg);
               });
            console.log("saiu2");
         }
      }
   }
</script>
