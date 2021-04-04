# dexcom-share-outside-us

This JavaScript module provides an [Async Iterator API][] for reading
blood glucose readings from Dexcom's Share servers.

This version was forked from [dexcom-share](https://www.npmjs.com/package/dexcom-share) by Nathan Rajlich.

Dexcom has separate databases for US and non-US customers and the only changes I made were to add the alternative endpoints for non-US customers
and a parameter to specify whether to use an US or non-US account. These changes were also submitted as PR to the original repository but unfortunately,
it seems to be abandoned.

### Example

```js
const dexcom = require('dexcom-share')

async function main() {
  const iterator = dexcom({
    username: 'DEXCOM_SHARE_USERNAME',
    password: 'DEXCOM_SHARE_PASSWORD',
	outsideUs: true // new in this fork!
  })

  for await (const reading of iterator) {
    console.log(reading)
    /*
    { DT: '/Date(1515095827000-0800)/',
      ST: '/Date(1515095827000)/',
      Trend: 4,
      Value: 123,
      WT: '/Date(1515095827000)/',
      Date: 1515095827000 }
    */
  }
}

main().catch(err => {
  console.error(err)
  process.exit(1)
})
```

[Async Iterator API]: https://github.com/tc39/proposal-async-iteration
