# Colocation of state

The general idea is to split up where state lives.  If all state lives in the root (i.e. a reducer that is at the root), then whenever any state changes, everything will re-render. Instead, keep state as close to where it belongs as possible.

Imagine you have a multi-step wizard.  As I type text into an input on the current step, the nav shouldn't be re-rendering. Each individual step in the wizard should have its own state that is separate from the global/generic wizard's state.
