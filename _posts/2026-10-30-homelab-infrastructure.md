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

- 3 Mini PC winblu
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

---

# Architettura attuale

L'infrastruttura attuale è basata su un cluster Proxmox VE a tre nodi utilizzato per ospitare servizi Linux self-hosted e per attività di studio e sperimentazione.

## Diagramma architetturale

```mermaid
flowchart TB

    INTERNET[Internet]
    TAILSCALE[Tailscale VPN]

    INTERNET --> TAILSCALE

    subgraph MGMT["Management Network"]
        PVE01[pve-01<br/>Proxmox VE]
        PVE02[pve-02<br/>Proxmox VE]
        PBS03[pbs-03<br/>Proxmox Backup Server]
    end

    TAILSCALE --> PVE01
    TAILSCALE --> PVE02
    TAILSCALE --> PBS03

    subgraph SERVICE["Erogazione Network"]
        WD4TB[WD Elements 4TB<br/>Primary Storage]
        NFS[NFS Export]
    end

    PBS03 --> WD4TB
    WD4TB --> NFS

    NFS --> PVE01
    NFS --> PVE02

    subgraph WORKLOADS["Hosted Services"]
        NEXTCLOUD[CT100 Nextcloud LXC]
        DB[(MariaDB)]
    end

    PVE01 --> NEXTCLOUD
    NEXTCLOUD --> DB
    NFS --> NEXTCLOUD

    subgraph ROADMAP["Planned Backup Strategy"]
        USB1TB[USB HDD 1TB]
        PBSREPO[Backup Repository]
    end

    PBS03 -. Future .-> USB1TB
    USB1TB -. Future .-> PBSREPO
    NEXTCLOUD -. Scheduled Backup .-> PBSREPO

## Cluster

Il cluster è composto dai seguenti nodi:

- pve-01
- pve-02
- pbs-03

I nodi vengono amministrati tramite l'interfaccia centralizzata di Proxmox VE.

---

## Networking

L'ambiente utilizza due reti distinte:

### Management Network

Utilizzata per:

- gestione dei nodi
- amministrazione del cluster
- comunicazioni Proxmox

### Erogazione Network

Rete dedicata ai servizi e allo storage.

Questa rete è stata realizzata sfruttando la seconda scheda di rete disponibile sul nodo pbs-03.

---

## Storage

Il nodo pbs-03 ospita un disco esterno WD da 4 TB.

Lo storage viene condiviso tramite NFS agli altri nodi del laboratorio.

Questo approccio consente di centralizzare i dati dei servizi mantenendo la semplicità dell'infrastruttura.

---

## Nextcloud

Il servizio Nextcloud è attualmente ospitato all'interno di un container LXC eseguito sul nodo pve-01.

I dati dell'applicazione vengono archiviati sullo storage condiviso esportato tramite NFS dal nodo pbs-03.

---

## Accesso Remoto

L'accesso all'intera infrastruttura è protetto tramite Tailscale.

Questa soluzione consente l'accesso remoto ai servizi e ai sistemi di amministrazione senza esporre direttamente il laboratorio su Internet.

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

## Evoluzioni pianificate

Una delle prossime attività previste consiste nell'introduzione di una soluzione di backup dedicata mediante Proxmox Backup Server.

L'obiettivo è collegare un secondo disco USB da 1 TB al nodo pbs-03 e utilizzarlo come repository indipendente per i backup.

Questa soluzione consentirà di mantenere separati:

- i dati di produzione ospitati sul disco WD da 4 TB
- i backup dei servizi del laboratorio
riducendo il rischio di perdita simultanea dei dati in caso di guasto del supporto di storage principale.

- Ulteriori attività di automazione e monitoraggio
