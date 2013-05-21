Topic: "Exporting variables for Eshell"
Date: 2012-10-18
Category: emacs

Usually when I'm working in Emacs it is running as a daemon. A lot of
times when I'm doing patch work and commits it'll want to dump me into
an editor set by my shell settings. More times than not this is
problematic because my editor may be set to nano or vim and rendering
in the eshell is ugly. So far all emacs/eshell sessions I wanted to
make sure my EDITOR/VISUAL environment variables were defined with
'emacsclient -n' in order to push all commit changes into a new buffer
window to be edited.

To remedy this I use a eshell hook to automatically set my environment
variables while in the shell without messing with anything I may have
set outside of emacs.

    (add-hook 'eshell-mode-hook
              '(lambda nil
                 (eshell/export "EDITOR=emacsclient -n")
                 (eshell/export "VISUAL=emacsclient -n")))

Pretty straight forward and keeps my eshell editing happy.
