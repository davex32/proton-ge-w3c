# Proton-GE W3Champions / Warcraft III Compatibility Fork

A focused GE-Proton fork for **Warcraft III 3.0**, **Battle.net**, **W3Champions**, and **FLO** on Linux.

This branch is based on **GE-Proton11-7** and keeps the upstream GE-Proton patch stack while adding a small set of Wine compatibility fixes needed for the Warcraft III / W3Champions environment.

## Download 
You can download the pre-built Proton build from the [Releases Page](https://github.com/davex32/proton-ge-w3c/releases/tag/GE-Proton11-7-W3C)


## Base

- Upstream: [GloriousEggroll/proton-ge-custom](https://github.com/GloriousEggroll/proton-ge-custom)
- Base release: **GE-Proton11-7**
- Compatibility branch: `wc3-ge-proton11-7`

This is an unofficial compatibility fork and is not affiliated with Blizzard, W3Champions, Valve, or GloriousEggroll.

## W3Champions compatibility fixes

The custom Wine patches live in:

```text
patches/w3c/
```

and are applied from `patches/protonprep-valve-staging.sh`.

### Shared-memory process queries

`0001-w3c-shared-query-reserve.patch`

Adds an opt-in shared-memory fast path for the high-frequency process memory queries performed by W3Champions against Warcraft III.

Enable it with:

```text
W3C_SHARED_QUERY=1
```

The implementation is deliberately restricted to the verified 64-bit W3Champions -> Warcraft III process pair and falls back to the normal Wine query path when the shared mapping cannot be used.

### Schannel missing-byte accounting

`0002-w3c-schannel-missing-count.patch`

Corrects Schannel missing-byte reporting used by the Battle.net / W3Champions networking path.

### Thread-input graph fixes

`0003-wine-thread-input-detach-graphfix.patch`

`0004-wine-thread-input-destroy-repartition.patch`

Preserve and repartition Wine thread-input graph connectivity when queues detach or are destroyed. These changes address input-state corruption seen across Warcraft III / W3Champions transitions.

### Job-object limit reporting

`0005-w3c-job-object-limit-query.patch`

Reports configured job-object limit flags in the form expected by W3Champions.

### UDP socket compatibility

`0006-w3c-ipv6-v6only-compat.patch`

Adds the socket behavior needed by the W3Champions / FLO UDP setup path:

- Windows-compatible `IPV6_V6ONLY` query behavior
- `IP_ECN` compatibility for IPv4 UDP sockets

This fixes FLO socket setup failures such as **WSAENOPROTOOPT / OS Error 10042**.

## Already provided by GE-Proton

The GE-Proton11-7 base already contains several fixes needed by this setup, so they are intentionally not duplicated in `patches/w3c/`, including:

- Warcraft III certificate-related compatibility
- AF_UNIX support used by the client stack
- cross-process selected-cursor sharing
- the normal GE-Proton Wine, DXVK, VKD3D-Proton, ProtonFixes, and runtime patch stack

## Building

Prepare the source tree:

```bash
./patches/protonprep-valve-staging.sh
```

Configure a build directory:

```bash
mkdir -p ../proton-ge-wc3-build
cd ../proton-ge-wc3-build
../proton-ge-w3c/configure.sh --build-name=GE-Proton11-7-W3C
```

Build:

```bash
make redist -j"$(nproc)"
```

The resulting archive is:

```text
GE-Proton11-7-W3C.tar.gz
```

## Usage

For W3Champions, enable the shared-query optimization in the launcher environment:

```text
W3C_SHARED_QUERY=1
```

When running GE-Proton outside Steam, use an **umu**-based launcher such as current Lutris or Heroic so Proton runs with its intended runtime environment.

## Patch layout

```text
patches/w3c/
├── 0001-w3c-shared-query-reserve.patch
├── 0002-w3c-schannel-missing-count.patch
├── 0003-wine-thread-input-detach-graphfix.patch
├── 0004-wine-thread-input-destroy-repartition.patch
├── 0005-w3c-job-object-limit-query.patch
└── 0006-w3c-ipv6-v6only-compat.patch
```

## Upstream projects

- [GE-Proton](https://github.com/GloriousEggroll/proton-ge-custom)
- [Valve Proton](https://github.com/ValveSoftware/Proton)
- [Wine](https://gitlab.winehq.org/wine/wine)
- [W3Champions](https://www.w3champions.com/)

## Support

If this fork is useful to you:

<a href="https://ko-fi.com/davexmachina" target="_blank">
  <img src="https://storage.ko-fi.com/cdn/kofi2.png" alt="Support me at ko-fi.com" height="46">
</a>
