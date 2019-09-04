<template>
  <div class="hello">
    <h2>
      本工具修改自<a  class="logo"  href="https://www.mytokenpocket.vip/"><img src="https://dapp.mytokenpocket.vip/TokenPocket-logo-h.png"></a> 
      <span class="title"><a href="https://eos-key.mytokenpocket.vip/" target="_blank">EOS公钥私钥生成器</a></span>
    </h2>
    <p>本工具用来随机生成一组EOSIO公钥私钥，生成过程可断网离线操作，<a href="https://github.com/eosio-key/eos-key" target="_blank">代码已开源</a>。</p>
    <p><strong>请一定注意记录并保管好您的私钥信息</strong></p>
    <button @click="generate">生成公钥和私钥</button>
    <div v-if="privateKey">
      <p>私钥:       {{privateKey}}</p><br/>
      <p>EOS公钥:    {{'EOS'+rawpublicKey}}</p>
      <p>FIBOS公钥:  {{'FO'+rawpublicKey}}</p>
      <p>ENU公钥:    {{'ENU'+rawpublicKey}}</p>
      <p>GOC公钥:    {{'GOC'+rawpublicKey}}</p>
    </div>
    <a class="ribbon" target="_blank" href="https://github.com/eosio-key/eos-key"><img style="position: absolute; top: 0; left: 0; border: 0; width: 100px" src="https://s3.amazonaws.com/github/ribbons/forkme_left_gray_6d6d6d.png" alt="Fork me on GitHub"></a>
  </div>
</template>

<script>
import ecc from 'eosjs-ecc';

export default {
  name: 'HelloWorld',
  data () {
    return {
      privateKey: '',
      rawpublicKey: ''
    }
  },
  methods: {
    generate() {
      ecc.randomKey().then(privateKey => {
        this.privateKey = privateKey;
        const publicKey = ecc.privateToPublic(privateKey);
        this.rawpublicKey = publicKey.slice(3)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

h2 {
  margin-bottom: 80px;
}

.logo {
  display: inline-block;
  vertical-align: middle;
}

.logo img {
  width: 300px;
  float: left;
}

.title {
  display: inline-block;
  vertical-align: middle;
}

strong {
  color: red;
}

button {
  color: #fff;
  background-color: #007bff;
  display: inline-block;
  font-weight: 400;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  border: 1px solid #007bff;
  padding: .375rem .75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: .25rem;
  transition: color .15s 
}

p {
  word-wrap: break-word;
}


@media (max-width: 760px) {
  .ribbon {
    display: none;
  }
}
</style>
