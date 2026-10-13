# OCI storage cleanup — 2026-10

## Context

OCI Always Free Ampere A1 allocation is now 2 OCPUs / 12 GB RAM (Oracle quietly cut it from the old 4/24 legend — verified 2026-10-08). Block storage is 200 GB total. Storage on the OCI hosts (Grasshopper workstation, Kali node) has accumulated junk from failed Android emulation attempts, old Docker images, and abandoned experiments.

## Plan

1. Inventory: `du -sh /*` and `docker system df` on each OCI host.
2. Identify trash: old QEMU images, failed AVD directories, stale Docker layers, abandoned project dirs.
3. Move candidates here (this branch) before deleting locally.
4. Delete local copies only after the GitHub commit is confirmed.
5. Reclaim: `docker system prune -af` for unused images/containers.

## Redroid migration (related)

The Android emulation path is switching from QEMU/TCG (12x slowdown, no KVM on OCI) to redroid — containerized Android that runs on the host kernel via binder/ashmem, no KVM needed. See the redroid implementation log in Grasshopper for the full design.

## Status

- [ ] Inventory run
- [ ] Trash identified
- [ ] Moved to this repo
- [ ] Local copies deleted
- [ ] Docker pruned
