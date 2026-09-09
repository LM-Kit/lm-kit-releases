# LM-Kit releases

Official release downloads for LM-Kit products. Every release on this repository is one product
version: the tag names the product and the version (`one/v2026.9.0`), the title names the
product, and every asset name starts with the product. Nothing is built here. The assets are
produced, signed and checked by each product's release pipeline and published as one complete set.

| Product | What it is | Tag prefix | Releases |
|---|---|---|---|
| [LM-Kit One](https://lm-kit.com/products/lm-kit-one) | A local AI server: OpenAI-compatible inference, agents, document intelligence, RAG and search on your own hardware | `one/v` | [All LM-Kit One releases](https://github.com/LM-Kit/lm-kit-releases/releases?q=one%2Fv&expanded=true) |

## LM-Kit One

Each release ships the same version for every target, plus a checksum file.

| Target | Asset | Notes |
|---|---|---|
| Windows x64, Windows Arm64 | `LM-Kit-One-<version>-win-<arch>.msi`, and the portable `.zip` | Authenticode-signed |
| Linux x64, Linux Arm64 | `LM-Kit-One-<version>-linux-<arch>.tar.gz` | Self-contained: extract and run |
| macOS Apple Silicon | `LM-Kit-One-<version>-osx-arm64.pkg` | Developer ID-signed, notarized |
| Container, linux/amd64 and linux/arm64 | `lmkitone/lm-kit-one:<version>` on Docker Hub, `ghcr.io/lm-kit/lm-kit-one:<version>` on GitHub Container Registry | One tag serves both architectures |
| Checksums | `LM-Kit-One-<version>-SHA256SUMS.txt` | SHA-256 of every asset above |

### Install

**Windows.** Run the installer. For an unattended install as a Windows service:

```
msiexec /i LM-Kit-One-<version>-win-x64.msi INSTALLMODE=service /qn
```

**Linux.** The archive is rooted at the payload, so it extracts straight into its install directory:

```bash
sudo mkdir -p /opt/lmkit-one
sudo tar -xzf LM-Kit-One-<version>-linux-x64.tar.gz -C /opt/lmkit-one
/opt/lmkit-one/lmkit
```

**macOS.** Open the `.pkg`.

**Container.** The API answers on port 5189 and the admin panel on `https://localhost:7221/admin`;
add `--gpus all` for an NVIDIA GPU:

```bash
docker run -d --name lmkit -p 5189:5189 -p 7221:7221 \
  -v lmkit-state:/data/state -v lmkit-models:/data/models \
  lmkitone/lm-kit-one:<version>
```

After a host install, the admin panel is at `http://localhost:5189/admin`. The first visit creates
the operator account. Everything else, from choosing a model to running as a service or behind a
reverse proxy, is in the guides.

### Verify a download

```bash
sha256sum --ignore-missing -c LM-Kit-One-<version>-SHA256SUMS.txt
```

On Windows, `Get-FileHash .\LM-Kit-One-<version>-win-x64.msi` in PowerShell prints the hash to
compare against the checksum file.

### Documentation

- Guides: [docs.lm-kit.com/lm-kit-one](https://docs.lm-kit.com/lm-kit-one). A running server also
  serves them at `/guides`.
- Product page: [lm-kit.com/products/lm-kit-one](https://lm-kit.com/products/lm-kit-one)

## Support and security

Questions go to [support@lm-kit.com](mailto:support@lm-kit.com). To report a vulnerability, follow
[SECURITY.md](SECURITY.md) and never open a public issue for it.

## License

LM-Kit products are commercial software distributed under the LM-Kit End User License Agreement;
see [LICENSE.md](LICENSE.md). Downloading or running a release means accepting it.
