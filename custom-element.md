#Make a web component custom element

###Example
Making a new element named vs-swatch which must have a - per draft spec.
```
var Swatch = document.registerElement('vs-swatch');
document.body.appendChild(new Swatch());
document.getElementsByTagName("vs-swatch")[0].setAttribute("color", "red")
```

#### Exetend Custom Elements


```
var p = Object.create(TickTockClock.prototype);
p.popOutBirdie = function() { … }
p.chime = function() {
  this.popOutBirdie();
  TickTockClock.prototype.chime.call(this);
};
var CuckooClock = document.registerElement('cuckoo-clock', {prototype: p});
var c = new CuckooClock();
c.tick();         // inherited from tick-tock-clock
c.chime();        // specialized by cuckoo-clock
c.popOutBirdie(); // specific to cuckoo-clock

```

### Psuedo Selector for Custom Elements
```
<style>
tick-tock-clock:unresolved {
  content: '??:??';  
}
</style>
<tick-tock-clock></tick-tock-clock> <!-- will show ??:?? -->
```
