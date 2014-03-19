#Shadow Dom

The Shadow Dom allows for encapsulation on the dom level.

* Insertion Points, add the shadow dom in where you want it to be added.
* Re-projection, shadow DOM subtree may have shadow roots of their own.
* Fallback Content, if nothing is distributed to an insertion point.
* Multiple Shadow Subtrees

The most recently applied shadow DOM subtree has the best shot of getting fresh children for its <content> insertion points.
Once it's had its way, the next most recent shadow DOM subtree—if even allowed to—can rummage through the remaining children.
Cycle repeats until either the current shadow DOM subtree has no \<shadow\> element, or we've processed the oldest DOM subtree for this element.


##CSS

Shadow Dom specifies a ::distributed pseudo-selector.

### Events in Shadow DOM

To ensure that the elements of the shadow DOM subtree are not exposed outside of the subtree, there's a fair bit of work that happens while dispatching an event from inside of the subtree.
