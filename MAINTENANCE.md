# Lichtblick package maintenance

This repository builds the source revision recorded in `lichtblick.lock`.
The repository URL, branch, and commit SHA are verified before every build.

When the pinned source changes:

1. update `LICHTBLICK_SHA` to the reviewed branch head;
2. increment the Debian revision in `.xgc2/product.yml`;
3. update each distribution-specific `release.apt_versions` value; and
4. require the packaging CI matrix to pass before release.

Do not add uncommitted source patches or generated build outputs to this
repository.
