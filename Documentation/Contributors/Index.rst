.. include:: ../Includes.txt


.. _contributing:

============
Contributing
============

Target group: **Contributors**

Thank you for considering contributions! You can contact us with any questions.

.. _contribute_docs:

Documentation
=============

You are welcome to help improve this guide. Just click on "Edit me on GitHub"
on the top right to submit your change request.

.. _contribute_feedback:

Feedback
========

Any problems? You miss a feature? There is an incompatibility? You have strategic input?

Please open an issue
`at our Github repository <https://github.com/dmind-gmbh/extension-cookieman/issues>`__
after you have read the documentation.

.. _contribute_code:

Code (Templates, JavaScript, PHP)
=================================

We are happy to receive pull requests.

Branches
~~~~~~~~~~

We use one branch for each stable TYPO3 API version. This model is not followed by many extensions.
This allows us to
focus on that API only and not worry about compatibility constructs or inabilities to incorporate any new
TYPO3 feature. So absolutely no `if (TYPO3_VERSION ...)` in cookieman.

Also it simplifies testing, as each version might need a different setup.
As our acceptance testing boots up the corresponding TYPO3 with a bootstrap_package and introduction
distribution and there are some specialities in each version combination, this just feels natural to us.

The downside is that currently `TER <https://extensions.typo3.org/extensions/cookieman>`__ only shows our
supported version
range on the list but not on the detail page.

After switching branches, you might need a `git clean -fdX -e '!.idea'` to remove any ignored files which were
created by another version's build (in this example excluding the IDE settings, .idea).

Releases
~~~~~~~~~~

Releases follow `semver <https://semver.org/>`. Including with composer via `dmind/cookieman: ^2.0` shall never
break any documented feature or the input or output of any function marked with @api in the code.
Be sure to shoot us an angry message if we messed up!

We usually release for all supported TYPO3 APIs at the same time and use consecutive patch versions (e.g.
2.2.3, 2.2.4, 2.2.5), each supporting one. We might deviate if feature sets change in the future.

Run locally
~~~~~~~~~~

:command:`ddev start && ddev launch` will install a TYPO3 with example content and cookieman.
This installs helper extensions that automatically enable a certain theme and some TypoScript setup to facilitate
development.
The admin user is "admin", password "adminadmin".

The ddev custom command :command:`ddev install-git-hooks` installs CGL checkers as pre-commit hooks (only tested on Linux
so far - the script runs under the container environment so good chances that this would work for other OSs as
well).

To throw away the database and restart cleanly, run :command:`ddev rm -ORU && git clean -fdX -e '!.idea' && ddev start`

Composer scripts
~~~~~~~~~~

Have a look at the `composer.json`'s `script` section. This is the main entry point for any commands needed
during development. Use :command:`ddev composer` from outside the container or just :command:`composer` from inside.

- :command:`ddev composer cookieman:...` enables an official cookieman theme. The "customtheme" shall resemble an integrator
  following our documentation.
- :command:`ddev composer cookieman:build` generates minified JS/CSS.
- :command:`ddev composer cookieman:test` runs all important tests. You do not strictly have to run tests before opening a
  pull request - they are also run post-commit on
  `Github actions <https://github.com/dmind-gmbh/extension-cookieman/actions>`__.
- :command:`ddev composer fix:cgl` tries to fix CGL problems.
- :command:`ddev composer build:docs` [+ any parameters, defaults to "makehtml"] builds documentation using the official
  `TYPO3 docs team docker image <https://docs.typo3.org/m/typo3/docs-how-to-document/master/en-us/RenderingDocs/Quickstart.html>`__
  (experimental feature, feedback is welcome). Unfortunately, the parameter :command:`--help` is masked by composer.
  :command:`composer build:docs -- --help` should work, but it doesn't.
