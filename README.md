# showcase of performance issue with `bind:clientWidth` in Svelte

Note that this also applies to:
- `bind:clientHeight`
- `bind:offsetWidth`
- `bind:offsetHeight`

There seems to be a linear performance decrease when it comes to using `bind:clientWidth` (or any of the other similar properties).
Every new element with binding adds around the same overhead in execution time.

It's difficult to give an exact number, but rendering stops feeling instant _(200ms)_ at around only 30 elements that use `bind:clientWidth` (or others), while we can go into the thousands without the binding and have no performance issues.

this is kinda bad

## demo
https://user-images.githubusercontent.com/48158184/225107486-3cd4300d-1317-4cff-97cd-7db89e8ae104.mov
