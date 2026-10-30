---
title: Homelab Infrastructure
date: 2026-10-29 18:00:00 +0100
categories: [Projects]
tags: [Proxmox, Linux, Nextcloud, MariaDB, Tailscale, Homelab]
---

# Homelab Infrastructure

## Introduzione

Questo progetto nasce dalla volontà di approfondire in modo pratico tecnologie legate alla virtualizzazione, ai sistemi Linux, allo storage e ai servizi self-hosted.

Nel tempo l'infrastruttura si è evoluta da una semplice installazione di Nextcloud su Raspberry Pi a un ambiente basato su un cluster Proxmox VE a tre nodi, utilizzato quotidianamente per attività di studio, sperimentazione e gestione di servizi personali.

L'obiettivo principale è quello di mantenere un ambiente realistico in cui testare tecnologie e procedure simili a quelle utilizzate negli ambienti enterprise, acquisendo esperienza diretta nella gestione di infrastrutture virtualizzate.

---

# Obiettivi del progetto

- Approfondire l'utilizzo di Proxmox VE
- Migliorare le competenze di amministrazione Linux
- Sperimentare servizi self-hosted
- Studiare soluzioni di storage e virtualizzazione
- Testare procedure di migrazione e aggiornamento
- Disporre di un ambiente accessibile da remoto in sicurezza

---

# Evoluzione del progetto

## Fase 1 - Raspberry Pi e Nextcloud

Il progetto è iniziato con l'installazione di Nextcloud su Raspberry Pi.

### Componenti

- Raspberry Pi 3B+
- Nextcloud
- Database SQLite
- HDD esterno USB

Questa configurazione ha rappresentato il punto di partenza per comprendere il funzionamento di Linux, dei servizi web e dei sistemi di storage.

---

## Fase 2 - Migrazione SQLite → MariaDB

Con la crescita del servizio è stato eseguito il passaggio da SQLite a MariaDB.

### Obiettivi della migrazione

- Migliorare affidabilità e scalabilità
- Allineare l'architettura alle best practice suggerite da Nextcloud
- Acquisire esperienza nella gestione dei database

### Attività svolte

- Installazione e configurazione MariaDB
- Backup preventivo del sistema
- Conversione del database
- Verifica dell'integrità dei dati
- Validazione del servizio

---

## Fase 3 - Realizzazione del Cluster Proxmox

Successivamente l'infrastruttura è stata ridisegnata introducendo una piattaforma di virtualizzazione.

### Componenti

- 3 Mini PC
- Proxmox VE
- Switch Ethernet a 8 porte
- Storage dedicato

### Obiettivi

- Centralizzare la gestione dei servizi
- Approfondire la virtualizzazione
- Disporre di un ambiente più flessibile ed espandibile

---

## Fase 4 - Migrazione di Nextcloud su Proxmox

Una volta completata l'infrastruttura Proxmox, il servizio Nextcloud è stato migrato all'interno del cluster.

### Soluzione adottata

- Container LXC
- Database MariaDB
- Storage dedicato

### Attività svolte

- Creazione del container
- Configurazione Linux
- Migrazione applicativa
- Migrazione dei dati
- Test funzionali post-migrazione

---

## Fase 5 - Accesso remoto tramite Tailscale

Per consentire l'amministrazione remota e l'accesso ai servizi in sicurezza è stata introdotta una rete VPN basata su Tailscale.

### Vantaggi

- Accesso remoto sicuro
- Nessuna esposizione diretta dei servizi a Internet
- Gestione semplificata della connettività
- Accesso da dispositivi multipli

---

# Architettura attuale

## Compute

- Cluster Proxmox VE composto da 3 nodi
- Gestione centralizzata tramite interfaccia Proxmox
- Container LXC
- Macchine virtuali dedicate ai test

## Networking

- Switch Ethernet 8 porte unmanaged
- Connettività LAN dedicata
- 2 subnet divise in management ed erogazione
- Accesso remoto tramite Tailscale

## Storage

- HDD esterno da 4 TB 
- Archiviazione dati e servizi del laboratorio

## Servizi principali

- Nextcloud
- MariaDB
- Tailscale
- Servizi Linux di laboratorio

---

# Tecnologie utilizzate

## Virtualizzazione

- Proxmox VE
- LXC Containers

## Sistemi Operativi

- Linux
- Raspberry Pi OS
- Debian

## Database

- MariaDB
- SQLite

## Networking

- Ethernet
- TCP/IP
- VPN
- Tailscale

## Storage

- Storage locale
- HDD USB 4 TB
- HDD USB 2TB

---

# Principali sfide affrontate

Durante lo sviluppo del progetto sono state affrontate diverse problematiche tecniche, tra cui:

- Migrazione sicura dei dati Nextcloud
- Conversione del database SQLite in MariaDB
- Pianificazione della migrazione verso Proxmox
- Gestione dello storage condiviso
- Configurazione dei container LXC
- Accesso remoto sicuro tramite VPN
- Validazione dei servizi dopo ogni migrazione

---

# Risultati ottenuti

Il progetto si è evoluto da una semplice installazione domestica di Nextcloud a una piattaforma infrastrutturale basata su virtualizzazione e servizi Linux.

L'ambiente viene utilizzato come laboratorio permanente per approfondire:

- Virtualizzazione
- Linux Administration
- Networking
- Storage
- Self-hosting
- Troubleshooting infrastrutturale

e rappresenta uno spazio di apprendimento continuo in cui sperimentare nuove tecnologie e nuove soluzioni architetturali.

---

# Prossimi sviluppi

Le attività pianificate per le prossime evoluzioni del laboratorio comprendono:

- Ottimizzazione dello storage
- Introduzione di nuove VM e container
- Studio di soluzioni di backup dedicate
- Approfondimento delle funzionalità avanzate di Proxmox VE
- Ulteriori attività di automazione e monitoraggio
