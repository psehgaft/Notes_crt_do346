# Notes_crt_do346 — Migrating Virtual Machines to OpenShift with MTV

Study notes and hands-on exercises for Red Hat course DO346: migrating virtual
machines from VMware vSphere, Red Hat Virtualization (RHV), OVA files, and
OpenShift Virtualization itself into OpenShift Virtualization, using the
Migration Toolkit for Virtualization (MTV) — Red Hat's supported distribution
of the upstream Forklift project.

## What this repository contains

| Path | Description |
| ---- | ----------- |
| `notes.md` | Step-by-step walkthrough: installing the MTV Operator, creating providers, storage maps and network maps, building migration plans, and migrating VMs from each source type, with both Web Console and `oc` CLI instructions. |
| `exercises/` | Hands-on exercises and quizzes. |
| `crds/mtv-operator.yaml` | Sample operator-install manifests used by the walkthrough. |

### Exercises

- `Migrating _VMs_vSphere_to_OpenShift_CNV_with_MTV.md` — full vSphere-to-OpenShift migration guide, from source provider to migrated VM.
- `exercise_1_warm_migration.md` — warm migration: the VM keeps running during most of the data transfer.
- `exercise_2_ova_import.md` — importing a VM from an OVA file.
- `exercise_3_multus_networking.md` — migrating a VM onto a specific Multus secondary network.
- `exercise_4_cli_only_migration.md` — a complete migration using only the `oc` CLI.
- `exercise_5_monitoring_and_logs.md` — monitoring `PlanMigration` resources and collecting MTV logs for troubleshooting.
- `mtv_quiz_50_questions.md` — 50 multiple-choice questions with explanations.
- `Qs-2.md` — exam questions on networking and storage in OpenShift Virtualization.

## Prerequisites

To follow the walkthrough and exercises you need:

- An OpenShift 4.12+ cluster with cluster-admin privileges.
- OpenShift Virtualization installed and configured.
- Access to a source virtualization environment (vSphere, RHV, or OVA files).
- The `oc` CLI installed and authenticated against the cluster.

## Usage

1. Read `notes.md` for the end-to-end migration flow: install the MTV
   Operator, define your source and target providers, map storage and
   networks, create a migration plan, and start it.
2. Work through the exercises in `exercises/` in order — they build from a
   basic warm migration to CLI-only migration and troubleshooting.
3. Use the quizzes (`mtv_quiz_50_questions.md`, `Qs-2.md`) to check your
   understanding before the exam.

A migration plan is started by annotating the plan, for example:

```bash
oc annotate plan <plan-name> forklift.konveyor.io/start=true -n openshift-mtv
```

## License

This repository is licensed under the GNU General Public License v3.0 —
see `LICENSE` for details.
