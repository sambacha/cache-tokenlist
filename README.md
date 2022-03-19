## cache-tokenlists

- Caches fetched tokenlists. 
- Updates when etag changes
- Uses cache regardless if endpoint unreachable.
- Uses write-file-atomic for safe updates.

```
const Cache = require('cache-tokenlist');
const assert = require('assert');

const cache = new Cache('/path/to/cache');

//////////////
// callbacks
//////////////

// get
cache.get('https://https://gateway.ipfs.io/ipns/tokens.uniswap.org', function(err, json) {
  assert.ok(!err);
  assert.ok(json.length > 0);
});

// get with forced update
cache.get('https://https://gateway.ipfs.io/ipns/tokens.uniswap.org', { force: true }, function(err, json) {
  assert.ok(!err);
  assert.ok(json.length > 0);
});

// clear the cache
cache.clear(function(err) {
  assert.ok(!err);
});

//////////////
// promise
//////////////

// get
const json = await cache.get('https://https://gateway.ipfs.io/ipns/tokens.uniswap.org')
assert.ok(json.length > 0);

// get with forced update
const json2 = await cache.get('https://https://gateway.ipfs.io/ipns/tokens.uniswap.org', { force: true })
assert.ok(json2.length > 0);

// clear the cache
await cache.clear();
```


## License

MIT