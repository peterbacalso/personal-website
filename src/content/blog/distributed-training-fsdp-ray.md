---
title: "Distributed Training Across Heterogeneous GPUs with FSDP2 and Ray"
description: "Building and testing distributed ML training across mixed GPU clusters using PyTorch FSDP2, Ray Train, and Kubernetes."
pubDate: 2026-05-11
tags: ["ml", "systems", "distributed-training"]
---

> **Work in Progress** — This post is still being written. I'll be documenting the design, implementation, and lessons learned from building a distributed training pipeline.

## Motivation

Most LLM models these days don't fit in commercial GPUs. I have a measly 8GB VRAM on my old RTX 1070, which means training anything meaningful requires distributed training across multiple GPUs.

The vast majority of training clusters use NVIDIA hardware, so I built this pipeline as a way to test whether I can provision an efficient training cluster with heterogeneous GPUs and orchestrate it properly.

## Experimental Goals

This is a rigorous experiment testing distributed ML training using:
- **PyTorch FSDP2** — fully sharded data parallelism
- **Ray Train** — distributed training orchestration
- **Kubernetes + KubeRay** — heterogeneous GPU cluster management
- **Vast.ai spot instances** — cost-effective GPU provisioning

## POC Experiments

I'm planning to verify this pipeline across several dimensions:

### Cluster & Scheduling
1. KubeRay heterogeneous groups — pools, placement, tier isolation
2. Kueue fair scheduling — concurrent submissions, quota enforcement
3. RayJob lifecycle — submit / monitor / cancel / no orphaned pods

### Backend Strategy
4. FSDP2 multi-node — NCCL rendezvous across K8s pods
5. FSDP2 + CPU offload — graceful degradation vs. OOM
6. DeepSpeed ZeRO-3 — checkpoint consolidation across shards
7. ZeRO-Infinity (if NVMe) — load model exceeding total GPU VRAM

### Strategy Selection
8. Auto-selection — correct backend chosen per model size
9. Fallback — FSDP2 OOM → retry with ZeRO-3

### Researcher Interface
10. End-to-end submission — plain Python in, job ID + MLflow out
11. Fault tolerance — kill worker mid-run, checkpoint resumes
12. MLflow logging — metrics correct, not duplicated across workers

---

More details coming soon.
