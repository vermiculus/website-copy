As the first exercise after 'hello, world', this is a good opportunity
to call attention to a few [style conventions][bbatsov-style]:
- lisp-case function names
- code layout (indentation and trailing parens)
- docstring formatting (using UPCASE for parameter names)

To re-iterate the general mentor guidelines, though: style is a
suggestion, not a rule.  Submissions *should* be consistent within
themselves, however.

### Reasonable Solutions
There are a few common approaches:

```elisp
;; using 'concat'
(defun two-fer (&optional name)
  (concat "One for " (or name "you") ", one for me."))

;; using 'format'
(defun two-fer (&optional name)
  "Return a message using NAME or a default."
  (format "One for %s, one for me." (or name "you")))

;; setting state
(defun two-fer (&optional name)
  (unless name
    (setq name "you"))
  (concat "One for " name ", one for me."))
```
...or any combination of these.

One approach that is valuable to think about is where the message is
duplicated:

```elisp
(defun two-fer (&optional name)
  (if name
      (concat "One for " name ", one for me.")
    "One for you, one for me."))
```

This minimizes runtime performace cost, but obviously increases
maintenance costs by violating DRY.  Prefer to see understanding of
`or` or `setq` before moving on.

### Unreasonable Solutions

You might see someone try to pay lip-service:

```elisp
(defun two-fer (&optional name)
  (cl-case name
    ("Alice" "One for Alice, one for me.")
    ("Bob" "One for Bob, one for me.")
    (otherwise "One for you, one for me.")))
```

This completely side-steps the exercise and doesn't set them up to
succeed later on.

### Other Notes

- You may see forms like `(if name name "you")`.  These are probably
  ok to approve: they still show understanding that this form still
  evaluates to a value.  It's worth a note, though.

[bbatsov-style]: https://github.com/bbatsov/emacs-lisp-style-guide
