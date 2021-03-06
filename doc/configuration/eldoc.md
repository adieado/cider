# ElDoc

Eldoc is a buffer-local minor mode that helps with looking up Lisp
documentation. When it is enabled, the echo area displays some useful
information whenever there is a Lisp function or variable at point;
for a function, it shows the argument list, and for a variable it
shows the first line of the variable's documentation string.

CIDER provides a Clojure backend for ElDoc that works out-of-the box, as
long as `eldoc-mode` is enabled.

![Eldoc](../images/eldoc.png)

## Enabling ElDoc

`global-eldoc-mode` is enabled by default in Emacs 25.1, so you don't really have
to do anything to enable it.

It will in both source and REPL buffers.

## Configuring ElDoc

* CIDER also would show the eldoc for the symbol at point. So in `(map inc ...)`
when the cursor is over `inc` its eldoc would be displayed. You can turn off this
behaviour by:

```el
(setq cider-eldoc-display-for-symbol-at-point nil)
```

* CIDER respects the value of `eldoc-echo-area-use-multiline-p` when
displaying documentation in the minibuffer. You can customize this variable to change
its behaviour.

| eldoc-echo-area-use-multiline-p | Behaviour |
| ------------- | ------------- |
| `t`  | Never attempt to truncate messages. Complete symbol name and function arglist or variable documentation will be displayed even if echo area must be resized to fit.|
| `nil`  | Messages are always truncated to fit in a single line of display in the echo area.  |
| `truncate-sym-name-if-fit` or anything non-nil | Symbol name may be truncated if it will enable the function arglist or documentation string to fit on a single line. Otherwise, behavior is just like `t` case. |

* CIDER will try to add expected function arguments based on the current context
(for example for the `datomic.api/q` function where it will show the expected
inputs of the query at point), if the variable `cider-eldoc-display-context-dependent-info`
is non-nil:

```el
(setq cider-eldoc-display-context-dependent-info t)
```
