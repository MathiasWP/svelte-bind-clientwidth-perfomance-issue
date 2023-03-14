# showcase of performance issue with bind:clientWidth in Svelte

Note that this also applies to:
- clientHeight
- offsetWidth
- offsetHeight

There seems to be a linear performance decrease when it comes to using bind:clientWidth (or any of the other similar properties).
Every binding adds around the same overhead in execution time.

It's difficult to give an exact number, but rendering stops feeling instant (200ms) at around only 30 elements that use bind:clientWidth (or others), while we can go in the thousands without the binding and have no performance issues.

this is kinda bad