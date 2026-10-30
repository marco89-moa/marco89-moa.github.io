---
title: Homelab Infrastructure
date: 2026-10-30 18:00:00 +0100
categories: [Projects]
tags: [Proxmox, Linux, Nextcloud, Homelab]
---

# Homelab Infrastructure

## Overview

Questo progetto nasce con l'obiettivo di approfondire tecnologie di virtualizzazione, sistemi Linux, storage e servizi self-hosted attraverso la realizzazione di un laboratorio infrastrutturale personale.

Nel tempo il laboratorio si è evoluto da una semplice installazione Nextcloud su Raspberry Pi a una piattaforma basata su un cluster Proxmox a tre nodi.

---

## Architettura attuale

### Compute

- Cluster Proxmox VE a 3 nodi
- Mini PC dedicati alla virtualizzazione
- Container LXC e macchine virtuali

### Networking

- Switch Ethernet 8 porte
- Accesso remoto tramite Tailscale

### Storage

- HDD esterno da 4 TB
- Storage condiviso per i servizi del laboratorio

### Servizi

- Nextcloud
- MariaDB
- Tailscale

---

## Evoluzione del progetto

### Fase 1

Installazione iniziale di Nextcloud su Raspberry Pi con database SQLite.

### Fase 2

Migrazione del database da SQLite a MariaDB.

### Fase 3

Realizzazione di un cluster Proxmox VE composto da due nodi più uno per Proxmox Backup Server.

### Fase 4

Migrazione del servizio Nextcloud verso un container LXC.

### Fase 5

Accesso remoto sicuro tramite Tailscale.

---

## Obiettivi

- Approfondire Proxmox VE
- Migliorare le competenze Linux
- Studiare storage e virtualizzazione
- Sperimentare servizi self-hosted
- Realizzare un ambiente di apprendimento continuo
