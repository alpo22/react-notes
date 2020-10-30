---


---

<h2 id="useimperativehandle">useImperativeHandle</h2>
<blockquote>
<p>Expose a Component’s inner functions so can call them</p>
</blockquote>
<p>Allows you to pass in a <code>ref</code> to a component, then in the component you can expose some of its functions by adding them to that ref, so the parent can call them.<br>
E.g. you have a <code>&lt;Textarea&gt;</code> component, and elsewhere on the screen there is a button that when clicked makes the <code>&lt;Textarea&gt;</code> scroll to its top.<br>
Used rarely, pairs with <code>forwardRef</code>.<br>
<a href="https://reactjs.org/docs/hooks-reference.html#useimperativehandle">https://reactjs.org/docs/hooks-reference.html#useimperativehandle</a></p>
<h3 id="forwardref">forwardRef</h3>
<p>Allows component to take a <code>ref</code> as a prop and pass it down further to its child.<br>
Simple example: <a href="https://gist.github.com/jamesreggio/142215754ad06f375bd87657c6227ed8">https://gist.github.com/jamesreggio/142215754ad06f375bd87657c6227ed8</a><br>
Not sure why you couldnt just pass down the ref as a prop though, call it <code>myRef</code>…</p>

