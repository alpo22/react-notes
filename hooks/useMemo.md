## useMemo (not _React.memo_)

> Memoize a value. This is NOT React.memo.

Memoize (cache) a value. Ask yourself, _"is this really expensive to calculate?"_  If so, memoize it so its not recalculated on re-render (unless its dependencies change).

    const sortedData = useMemo(() => ...sort and return the raw data..., [rawData]);

It runs while the page is rendering, so may appear slow the first time.

A practical example is a component that accepts some raw data as a prop, sorts it, then displays it.  The _sorted data_ could be memoized so that it is not re-sorted on re-render.  It will still get re-sorted if the `rawData` prop changes, but we don't want to re-sort if this component's other state changes, or the parent updates causing this component to re-render.
