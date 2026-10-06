# homebrew-tap

Homebrew casks for [Azzurro](https://azzurro.blue/) and
[rPGP](https://rpgp.app/).

    brew tap jzbz/tap
    brew install --cask azzurro
    brew install --cask rpgp

or, without tapping first:

    brew install --cask jzbz/tap/azzurro
    brew install --cask jzbz/tap/rpgp

One tap rather than one per app: a tap is only a repository with a `Casks/`
directory, nothing in it is per-project, and a second one would be a second
thing to tap for no gain.

Each cask is generated from a template kept in the app's own repository, under
`packaging/homebrew/`, by a script that writes nothing until the release checks
out. It downloads the published macOS zip and the release's `SHA256SUMS` and
`SHA256SUMS.asc`, requires exactly one good signature over the sums by the
release key, named by its full fingerprint, and then requires the zip's one line
in them to match the zip's hash. A file that cannot be fetched, a missing line
or a mismatch stops it, and no cask comes out.

So the hash in each cask was checked against the release key's signature when
the cask was written, but the cask carries no signature of its own: what a
Homebrew user trusts is this repository's git history and Apple's notary. The
`SHA256SUMS.asc` on each release is the one artifact that survives a compromise
of either, and verifying it is worth doing by hand.
