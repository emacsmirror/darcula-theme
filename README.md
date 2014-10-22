darcula-theme-emacs
===================

Emacs theme inspired by IntelliJ's Darcula.

Distributed on [MELPA](http://melpa.milkbox.net/), use by installing the `darcula-theme` package and then

```elisp
(load-theme 'darcula t)
;;(set-frame-font "Inconsolata-16") ;; your preferred main font face here
```

If you're on emacs `<24.4` you'll need to add the following magical workaround to your `.emacs`:

```elisp
;; WORKAROUND https://github.com/alezost/alect-themes/#emacs-2431-and-earlier
(defun face-spec-recalc-new (face frame)
  "Improved version of `face-spec-recalc'."
  (while (get face 'face-alias)
    (setq face (get face 'face-alias)))
  (face-spec-reset-face face frame)
  (let ((theme-faces (get face 'theme-face)))
    (if theme-faces
        (dolist (spec (reverse theme-faces))
          (face-spec-set-2 face frame (cadr spec)))
      (face-spec-set-2 face frame (face-default-spec face))))
  (face-spec-set-2 face frame (get face 'face-override-spec)))
(defadvice face-spec-recalc (around new-recalc (face frame) activate)
  "Use `face-spec-recalc-new' instead."
  (face-spec-recalc-new face frame))
```

Note that semantic highlighting in the below example is only achievable in Scala when using [ENSIME](https://github.com/ensime/ensime-server) with the following semantic highlighting overlays:

```elisp
(setq ensime-sem-high-faces
      ;; NOTE: Inconsolata doesn't have italics
      ;; FURTHER NOTE: these are overlays, not faces
      '((var . (:foreground "#9876aa" :underline (:style wave :color "yellow")))
        (val . (:foreground "#9876aa"))
        (varField . (:slant italic))
        (valField . (:foreground "#9876aa" :slant italic))
        (functionCall . (:foreground "#a9b7c6"))
        (operator . (:foreground "#cc7832"))
        (param . (:foreground "#a9b7c6"))
        (class . (:foreground "#4e807d"))
        (trait . (:foreground "#4e807d" :slant italic))
        (object . (:foreground "#6897bb" :slant italic))
        (package . (:foreground "#cc7832"))))
```

![example](darcula-example.jpg)
