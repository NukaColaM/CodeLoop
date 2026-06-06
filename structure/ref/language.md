# Architectural vocabulary

Use these terms consistently in `structure` reports.

## Terms

**Module**: anything with an interface and implementation: function, class, package, or file.

**Interface**: everything callers must know: types, signatures, invariants, error modes, ordering, configuration.

**Implementation**: code hidden behind the interface.

**Depth**: behavior behind the interface relative to interface size.

**Deep module**: small interface, substantial implementation, high caller leverage.

**Shallow module**: interface nearly as complex as implementation; callers must understand too much.

**Seam**: interface location where behavior can change or be swapped. One adapter is hypothetical; two adapters make the seam real.

**Leverage**: functionality callers get for a small interface investment.

**Locality**: knowledge, changes, and bugs concentrated in one place.

## Tests

**Deletion test**: if deleting a module removes complexity, it was pass-through. If complexity spreads across callers, it earned its keep. If complexity moves to every caller, deepen it.

**Interface test**: if you cannot explain how to use the module in one sentence without caveats, the interface is too large or the module is too shallow.
