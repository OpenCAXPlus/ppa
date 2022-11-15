# ppa
The ppa for OpenCAXPlus

Follow the tutorial [here](https://assafmo.github.io/2019/05/02/ppa-repo-hosted-on-github.html)
## To install from this repo

```sh
curl -s --compressed "https://opencaxplus.github.io/ppa/KEY.gpg" | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/opencaxplus.gpg >/dev/null
sudo curl -s --compressed -o /etc/apt/sources.list.d/OpenCAXPlus.list "https://opencaxplus.github.io/ppa/OpenCAXPlus.list"
sudo apt update
```

## To update the repo content
```sh
# Packages & Packages.gz
dpkg-scanpackages --multiversion . > Packages
gzip -k -f Packages

# Release, Release.gpg & InRelease
apt-ftparchive release . > Release
gpg --default-key B7273D58819A588B132C77E416637014136D42BD -abs -o - Release > Release.gpg
gpg --default-key B7273D58819A588B132C77E416637014136D42BD --clearsign -o - Release > InRelease

# Commit & push
git add -A
git commit -m update
git push
```
