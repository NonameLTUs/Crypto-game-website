<template>
  <div>
    <span>web3 active {{ isLoggedIn }}</span>
  </div>
</template>

<script>
  import Web3 from 'web3'
  import GameABI from '@/../../crypto-game/build/contracts//Game.json'
  const GameAddress = "0x0"
  var GameInstance = null
  var web3 = window.web3 !== undefined ? new Web3(window.web3.currentProvider) : null
  // var infuraWeb3 = new Web3(new Web3.providers.WebsocketProvider(config.InfuraWeb3))

  export default {
    name: "Game",
    data() {
      return {
        defaultAccount: null,
        loggedIn: false,
        BN: this.isWeb3Present ? web3.utils.BN : null
      }
    },
    computed: {
      isLoggedIn() {
        return this.defaultAccount !== null
      },
      isWeb3Present() {
        return web3 !== null
      }
    },
    methods: {
      watchWeb3Accounts() {
        setInterval(() => {
          web3.eth.getCoinbase().then(defaultAddress => {
            if (this.defaultAccount !== defaultAddress) {
              this.defaultAccount = defaultAddress

              if (defaultAddress === null) {
                console.log('web3 not found');
              } else {
                console.log('web3 found')
              }

              this.reset();
            }
          })
        }, 500)
      },
      reset() {

      }
    },
    created() {
      if (this.isWeb3Present) {
        // GameInstance = new web3.eth.Contract(GameABI.abi, GameAddress)
        this.watchWeb3Accounts()
      } else {
        console.log("Ethereum Client not found");
      }
    }
  }
</script>