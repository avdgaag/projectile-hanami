# Projectile Hanami

## Summary

Projectile Hanami is an [Emacs][] minor mode, based on [Projectile][], for navigating [Hanami][] projects. With Projectile Hanami, you can:

* navigate through entities, repositories, actions, views and templates are different apps in your project;
* quickly jump to some important standard files;
* run `hanami server`
* run `hanami console`
* run Rake tasks

Projectile Hanami is based on [Projectile Rails][], but is not a complete port of all its functionality.

## Installation

This guide assumes you have [Projectile][] already set up.

Since this package is still under heavy development and testing, it is not yet available through one of the popular package managers. You can try it out by cloning the repository and adding it to your `load-path`:

```elisp
(add-to-list 'load-path "/path/to/repo")
(require 'projectile-hanami)
```

To have Projectile Hanami loaded whenever Projectile is loaded, you can add it as a hook:

```elisp
(add-hook 'projectile-mode-hook 'projectile-hanami-on)
```

...but, this will most likely conflict with Projectile Rails. If you use both [Ruby on Rails][] _and_ Hanami, you will probably want something _slightly_ more sophisticated. I use the following snippet:

```elisp
(defun projectile-rails-or-hanami-on ()
  "Activate either `projectile-rails-mode` or `projectile-hanami-mode`."
  (if (projectile-hanami-applicable-p)
    (projectile-hanami-mode +1)
    (projectile-rails-on)))

(add-hook 'projectile-mode-hook 'projectile-rails-or-hanami-on)
```

Since Projectile Rails cannot distinguish between Rails and Hanami projects, and Hanami _can_, we use Projectile Hanami's detection mechanism and fall back to Projectile Rails in case of no match.

## Usage

### Customization

You can define the Projectile Hanami keybinding prefix:

```elisp
;; Defaults to C-c e
(setq projectile-hanami-keymap-prefix (kbd "C-c p C-q"))
```

To override how Hanami commands are invoked:

```elisp
;; Defaults to `bundle exec hanami`
(setq projectile-hanami-cmd "/path/to/hanami")
```

### Commands

Command                                   | Keybinding           | Description
------------------------------------------|----------------------|---------------------------------------------------------------------------
projectile-hanami-find-initializer        | <kbd>C-c e i</kbd>   | Use `projectile-completion-system` to find initializers across apps.
projectile-hanami-find-lib                | <kbd>C-c e l</kbd>   | Use `projectile-completion-system` to find project lib files.
projectile-hanami-find-controller         | <kbd>C-c e c</kbd>   | Use `projectile-completion-system` to find controller actions across apps.
projectile-hanami-find-view               | <kbd>C-c e v</kbd>   | Use `projectile-completion-system` to find views across apps.
projectile-hanami-find-template           | <kbd>C-c e t</kbd>   | Use `projectile-completion-system` to find templates across apps.
projectile-hanami-find-presenter          | <kbd>C-c e p</kbd>   | Use `projectile-completion-system` to find presenters across apps.
projectile-hanami-find-stylesheet         | <kbd>C-c e s</kbd>   | Use `projectile-completion-system` to find stylesheets across apps.
projectile-hanami-find-javascript         | <kbd>C-c e j</kbd>   | Use `projectile-completion-system` to find javascripts across apps.
projectile-hanami-find-config             | <kbd>C-c e g</kbd>   | Use `projectile-completion-system` to find config files across apps.
projectile-hanami-find-routes             | <kbd>C-c e u</kbd>   | Use `projectile-completion-system` to find routes files across apps.
projectile-hanami-find-entity             | <kbd>C-c e e</kbd>   | Use `projectile-completion-system` to find entities.
projectile-hanami-find-repository         | <kbd>C-c e r</kbd>   | Use `projectile-completion-system` to find repositories.
projectile-hanami-find-mailer             | <kbd>C-c e m</kbd>   | Use `projectile-completion-system` to find mailers.
projectile-hanami-find-mailer-template    | <kbd>C-c e T</kbd>   | Use `projectile-completion-system` to find mailer templates.
projectile-hanami-find-application        | <kbd>C-c e a</kbd>   | Use `projectile-completion-system` to find main application files.
projectile-hanami-goto-related-controller | <kbd>C-c e C</kbd>   | Find the controller action related to the current view or template.
projectile-hanami-goto-related-template   | <kbd>C-c e T</kbd>   | Find the template related to the current view or controller action.
projectile-hanami-goto-related-view       | <kbd>C-c e V</kbd>   | Find the view related to the current template or controller action.
projectile-hanami-goto-entity             | <kbd>C-c e E</kbd>   | Find the entity for the current repository.
projectile-hanami-goto-repository         | <kbd>C-c e R</kbd>   | Find the repository for the current entity.
projectile-hanami-goto-mapping            | <kbd>C-c e g m</kbd> | Find the project's `lib/config/mapping.rb` file
projectile-hanami-goto-rakefile           | <kbd>C-c e g r</kbd> | Find the project's Rakefile.
projectile-hanami-goto-gemfile            | <kbd>C-c e g g</kbd> | Find the project's Gemfile.
projectile-hanami-rake                    | <kbd>C-c e ! r</kbd> | Run a project Rake task.
projectile-hanami-console                 | <kbd>C-c e ! c</kbd> | Run `hanami console`
projectile-hanami-server                  | <kbd>C-c e ! s</kbd> | Run `hanami server`

[Emacs]: http://www.gnu.org/software/emacs/emacs.html
[Projectile]: https://github.com/bbatsov/projectile
[Hanami]: https://hanamirb.org
[Projectile Rails]: https://github.com/asok/projectile-rails
