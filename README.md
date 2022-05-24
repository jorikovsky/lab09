sudo apt install gpg
gpg --list-secret-keys --keyid-format LONG
gpg --full-generate-key

gpg --list-secret-keys --keyid-format LONG

GPG_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep ssb | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}')

GPG_SEC_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep sec | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}')
gpg --armor --export ${GPG_KEY_ID} | cat

git config user.signingkey ${GPG_SEC_KEY_ID}
git config gpg.program gpg

git tag -s v0.1.0.0
git tag -v v0.1.0.0
git show v0.1.0.0
git push origin main --tags
