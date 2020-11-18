# CRDT-LWW
A Swift implementation of Last-Writer-Wins Element Set. 


CRDT
---


Conflict-free replicated data type


## CRDT Charactistics

- Associativity (a+(b+c)=(a+b)+c), so that grouping doesn't matter.
- Commutativity (a+b=b+a), so that order of application doesn't matter.
- Idempotence (a+a=a), so that duplication doesn't matter.

## Types

- Operation-based CRDTs
- State-based CRDTs

## Known CRDT

- G-Counter (Grow-only Counter)
- Pn-Counter (Positive-Negative Counter)
- G-Set (Grow-only Set)
- 2P-Set (Two-Phase Set)
- LWW-Element-Set (Last-Write-Wins-Element-Set)
- OR-Set (Observed-Removed Set)oSequence CRDTs
- Sequence CRDTs

## Reference

- Live Demo of https://github.com/edvorg/lww-element-set
- https://github.com/cedricblondeau/go-lww-element-set

## Examples

```
let bikes = CRDTLWW<String>()
bikes.add(CRDTNode("BMW", 1))  // add a BMW with timestamp 1
bikes.add(CRDTNode("DUCATI", 1))  // add a DUCATI with timestamp 1
bikes.add(CRDTNode("HONDA", 1))  // add a HONDA with timestamp 1
bikes.remove(CRDTNode("BMW", 2)) // remove a BMW with timestamp 2
bikes.result() // returns (DUCATI, 1), (HONDA, 1)
bikes.query("DUCATI") // returns (DUCATI, 1)
bikes.query("BMW") // returns nil
bikes.count() // returns 2
```

Things to optimize:

- CRDTLWW.result() is expensive and can be cached and optimized.
- CRDTLWW might not contain full set of history because it's
  overridden by last timestamp.
- Test cases need to be improved.
- If the timestamp are the same for multiple elements, the result order
  could be undermined because of using Dictionary. Consider building an
ordered dictionary in Swift if needed.(just like concurrentHashmap in java)
