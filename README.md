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
`packaging/homebrew/`, by a script that downloads the published macOS zip,
hashes it, and — where the release carries a `SHA256SUMS` — refuses to emit a
cask whose hash disagrees with it. That check is against the checksum file
itself, not against its signature, and it is skipped rather than failed if the
file cannot be fetched.

So the cask carries no signature of its own, and what a Homebrew user trusts is
this repository's git history and Apple's notary. The `SHA256SUMS.asc` on each
release is the one artifact that survives a compromise of either, and verifying
it is worth doing by hand.
