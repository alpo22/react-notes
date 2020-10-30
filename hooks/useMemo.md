## useMemo (not _React.memo_)

> Memoize a value. This is NOT React.memo.

Memoize (cache) a value. Ask yourself, _"is this really expensive to calculate?"_  If so, memoize it so its not recalculated on re-render (unless its dependencies change).

    const numDec = 100; // number of decimals
    const pi = useMemo(() => computePi(numDec), [numDec]);

It runs while the page is rendering, so may appear slow the first time.
