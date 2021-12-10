<template>
  <div class="demo-ctn">
    <div class="inner">
      <h3>Demo Styles</h3>
      <CodeContainer
        id="js1"
        :content="jsContent"
        language="javascript"
        code-title="My Javascript code snippet"
        :dark="true"
      />
      <CodeContainer
        id="php1"
        :content="phpContent"
        language="php"
        code-title="My PHP code snippet"
        :dark="true"
      />
      <CodeContainer
        id="curl1"
        :content="cUrlContent"
        language="shell"
        code-title="My cUrl code snippet"
        :dark="true"
      />
      <CodeContainer
        id="go1"
        :content="golangContent"
        language="go"
        code-title="My Golang code snippet"
        :dark="true"
      />
      <CodeContainer
        id="dart1"
        :content="dartContent"
        language="dart"
        code-title="My Dart code snippet"
        :dark="true"
      />
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      jsContent:
`const Omni = require('@omni/server-sdk')

const omni = new Omni({
  apiKey: Omni_API_key,
  apiSecret: Omni_API_SECRET,
  applicationId: "4h4jh4jk4h44 4h4jkhfgf4g4fg44 44h4jh 44 jhk4h4",
  privateKey: Omni_APPLICATION_PRIVATE_KEY_PATH
})`,
      phpContent:
`<?php
$a = array('a' => 1, 'b' => 2, 3 => 'c');

echo "$a[a] {\${a[3] /* } comment */} {$a[b]} \\$a[a]}";

function hello($who) {
  return "Hello $who!";
}
?>`,
      cUrlContent:
`# start the server in HTTPS mode
cd web
sudo node ../server.js 443 'yes' >> ../node.log &

# here is how to stop the server
for pid in \`ps aux | grep 'node ../server.js' | awk '{print $2}'\` ; do
  sudo kill -9 $pid 2> /dev/null
done`,
      golangContent:
`cpackage main

import "fmt"

// Send the sequence 2, 3, 4, ... to channel 'ch'.
func generate(ch chan<- int) {
  for i := 2; ; i++ {
    ch <- i  // Send 'i' to channel 'ch'
  }
}`,
      dartContent:
`import 'dart:math' show Random;

void main() {
  print(new Die(n: 12).roll());
}`
    }
  }
}
</script>

<style scoped>
 .inner {
   max-width: 800px;
   margin: 0 auto;
   font-family: Arial, Helvetica, sans-serif;
 }
</style>
