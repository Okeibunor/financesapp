<template>
  <div class="p-5">
      <button class="bg-blue-500 text-white px-5 py-3 rounded" id="launch-btn">Connect Bank Account</button>
  </div>
</template>

<script>
  export default {
    mounted(){
        const copyToClipboard = text => {
          const elm = document.createElement('textarea');
          elm.value = text;
          document.body.appendChild(elm);
          elm.select();
          document.execCommand('copy');
          document.body.removeChild(elm);
        };
        const config = {
          key: "live_pk_yG716FaHwK5J7KX3thLl",
          onSuccess (response) {
            copyToClipboard(response.code);
            console.log(JSON.stringify(response));
            alert(JSON.stringify(response));
            /**
             response : { "code": "code_xyz" }
             you can send this code back to your server to get this
             authenticated account and start making requests.
             */
          },
          onClose () {
            console.log('user closed the widget.')
          }
        };
        const connect = new Connect(config);
        connect.setup();
        const launch = document.getElementById('launch-btn');
        launch.onclick = function () {
          connect.open();
        };
    }
  }
</script>

<style lang="css" scoped>
  .p-5 {
      padding: 5em;
  }
</style>
