# tetragon-lab

```
dpkg --print-architecture
```

OUTPUT: amd64

```
curl -L --remote-name-all https://github.com/cilium/tetragon/releases/download/tetragon-cli/tetragon-linux-amd64.tar.gz.sha256sum
```

Valid Packages: <br/>
https://github.com/cilium/tetragon/releases/tag/tetragon-cli

```
sha256sum --check tetragon-linux-amd64.tar.gz.sha256sum
```

OUTPUT: <b>OK</b>

```
sudo tar -C /usr/local/bin -xzvf tetragon-linux-amd64.tar.gz
```

```
rm tetragon-linux-amd64.tar.gz{,.sha256sum}
```
