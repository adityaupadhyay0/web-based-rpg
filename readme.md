
Software Requirements Specification (SRS)

Project Title: Legends of Etheria – A Web-Based 2D RPG GameBackend Technology: Go (Golang)Frontend Technology: HTML5 Canvas, JavaScript (Phaser.js)Database: PostgreSQL + Redis (Caching + Session Store)Architecture: Microservices (Event-Driven, Pub/Sub, REST + WebSocket)

1. Introduction

1.1 Purpose:This document defines the complete Software Requirements Specification for the "Legends of Etheria" project, a multiplayer, persistent-world web-based 2D RPG. It details the features, architecture, and technical design necessary for development and deployment.

1.2 Scope:

Browser-based 2D tile-based RPG game.

Massive Multiplayer Online (MMO) experience.

Persistent world with real-time mechanics.

Character development, quest progression, and social gameplay.

Admin tools for world and user management.

1.3 Audience:This document is intended for project stakeholders, software architects, developers, testers, and DevOps engineers.

1.4 Definitions, Acronyms, and Abbreviations:

RPG: Role-Playing Game

NPC: Non-Player Character

XP: Experience Points

PvP/PvE: Player vs Player/Environment

GM: Game Master

2. Functional Requirements

2.1 User Account System

Registration, login, OAuth2 support

Email verification, password reset

User profiles and character lists

2.2 Character System

Create multiple characters per user

Character classes (Mage, Knight, Rogue, etc.)

Skill trees and leveling up (XP system)

2.3 World Interaction

Tile-based movement (client-side & server-authoritative)

Map zones and seamless zone loading

Environmental interactions (NPCs, items, doors, etc.)

2.4 Combat System

Real-time PvE and PvP combat

Turn-based or cooldown-based abilities

Health, mana, stamina, and stats system

2.5 Inventory and Items

Inventory management (add, use, drop)

Equipment slots (weapons, armor, accessories)

Crafting system (future release)

2.6 Quest Engine

Quest creation, assignment, and tracking

Multiple objective types (fetch, kill, escort)

Rewards system (XP, items, currency)

2.7 Multiplayer & Communication

Real-time WebSocket communication

Chat system: local, global, private, guild

Emotes and status updates

2.8 Economy and Trade

Currency system (gold, silver)

Shop vendors (buy/sell items)

Player-to-player trading

2.9 Admin/GM Panel

Role-based access

Live world editing (spawns, events, weather)

User moderation tools (ban, mute, teleport)

2.10 Analytics and Logs

Real-time metrics (active users, server load)

Gameplay logs and error reports

3. Non-Functional Requirements

Performance: Low latency < 100ms gameplay response

Scalability: Horizontal scaling for services & game zones

Security: JWT for auth, XSS/SQLi protections, rate limiting

Usability: Intuitive UI with keyboard & mouse support

Availability: 99.9% uptime with load balancing

Maintainability: Modular codebase, versioned APIs

4. System Architecture

4.1 Overview

Event-driven architecture using a message queue (NATS or RabbitMQ)

WebSockets for real-time communication

REST for data management APIs

Microservices containerized via Docker

4.2 Services:

Auth Service: Handles login, registration, sessions

Character Service: Character management & data

World Service: Map data, movement, triggers

Combat Service: Battle logic and stat management

Inventory Service: Item ownership, usage

Quest Service: Quest tracking and logic

Chat Service: Real-time messaging

Admin Service: Admin tools and world management

4.3 Database

PostgreSQL for structured data

Redis for caching, sessions, pub/sub

Blob Storage (optional): For assets like tilesets, sprites

4.4 Interservice Communication

gRPC or REST between services

Event bus for pub/sub actions

5. Data Models (Simplified)

User

ID, Email, Username, PasswordHash, CreatedAt

Character

ID, UserID, Name, Class, Level, XP, Stats, InventoryID

Item

ID, Name, Type, Description, Usable, EquipSlot, Stats

Quest

ID, Title, Objectives[], Rewards[], Prerequisites[]

MapTile

ID, Type, Properties, ZoneID, InteractableID

ChatMessage

ID, SenderID, Channel, Content, Timestamp

6. Game Client (Frontend)

Technologies:

Phaser.js game engine

HTML5 + CSS for interface

WebSocket + REST API client

Modules:

UI/UX: Health bars, menus, chat, maps

GameRenderer: Tiles, animations, overlays

InputManager: Keyboard and mouse input

SyncEngine: Updates from server

7. DevOps and Deployment

Dockerized microservices

CI/CD pipeline via GitHub Actions

Reverse proxy via NGINX

Load balancing with HAProxy or cloud load balancer

Monitoring: Prometheus, Grafana

Central logging: Loki or ELK stack

8. Roadmap and Future Extensions

Player housing system

Mounts and travel mechanics

Seasonal events and world bosses

Companion AI / Pets

Mobile support via PWA or wrapper (Capacitor.js)

Blockchain integration (optional)

9. Pre-Documentation Artifacts

9.1 Vision Document

High-level game concept and philosophy

Business goals, target audience, monetization

Success criteria and KPIs (e.g., 10k DAUs in 3 months)

9.2 Feasibility Study

Technical, Operational, Economic, Legal analyses

Server and infrastructure cost estimates

9.3 Project Charter

Goals, constraints, stakeholders and responsibilities

Budget, timeline overview, risk register summary

9.4 Use Case Document

Key use cases with actors and flows:

Player: Register → Create Character → Play → Save Progress

Admin: Add Quest → Monitor Players

Player: Trade Item → Chat with Guild

9.5 User Stories & Epics

Epic: Player Progression

As a player, I want to level up by gaining XP.

As a player, I want to unlock new skills.

Epic: Social Interaction

As a player, I want to chat with my guild.

As a player, I want to form parties.

Epic: Administration

As an admin, I want to teleport players.

As an admin, I want to trigger world events.

9.6 Game Design Document (GDD)

World lore, zone maps, NPC behavior

Character classes, combat balance charts

Art style guide: sprites, animations, UI mockups

9.7 Software Architecture Document

Detailed system and component diagrams

Data flow diagrams (DFDs) and deployment views

9.8 API Specification

OpenAPI/Swagger definitions for REST endpoints

WebSocket message schemas and auth flow

9.9 Test Plan

Unit, integration, E2E test strategies

Load testing approach (1000+ concurrent users)

Security and compliance test cases

9.10 Risk Management Plan

Identified risks with probability and impact

Mitigation strategies (backups, failovers, chat moderation)

9.11 Milestone Plan

Phase 1 (4 weeks): Core systems (Auth, World, Movement)

Phase 2 (6 weeks): Combat, Inventory, Chat

Phase 3 (4 weeks): Admin tools, Testing

Phase 4 (2 weeks): Beta, Bug fixes, Launch

Document Version: Final v1.0Author: Aditya UpadhyayLast Updated: June 21, 2025















.
├── .github/                           # GitHub workflows and PR templates
│   ├── ISSUE_TEMPLATE/               # Issue templates
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── workflows/
│       ├── ci.yml                    # Build, test, lint
│       ├── cd.yml                    # Deploy to staging/prod
│       └── security-scans.yml        # SAST/Dependabot checks
│
├── architecture/                      # Architecture Decision Records & Diagrams
│   ├── ADR/                           # Markdown ADRs
│   ├── diagrams/                      # PlantUML, draw.io files
│   └── README.md
│
├── docs/                              # High‑level project docs
│   ├── SRS/                           # Software Requirements Specification
│   ├── GDD/                           # Game Design Document (lore, balance)
│   ├── API/                           # OpenAPI + WebSocket schemas
│   ├── SECURITY.md                    # Threat model & hardening guides
│   ├── STYLE_GUIDE.md                 # Coding conventions (Go & JS)
│   └── CONTRIBUTING.md                # How to contribute & code of conduct
│
├── frontend/                          # Phaser.js game client (monorepo style)
│   ├── apps/                          
│   │   └── game/                      # Primary game app
│   │       ├── public/                # index.html, favicons, robots.txt
│   │       ├── src/
│   │       │   ├── assets/            # Sprites, sounds, music
│   │       │   │   ├── tilesets/
│   │       │   │   ├── characters/
│   │       │   │   ├── ui/
│   │       │   │   └── audio/
│   │       │   ├── engine/            # Phaser scenes & systems
│   │       │   ├── ui/                # React/Preact overlays (menus, HUD)
│   │       │   ├── store/             # Pinia/Redux state management
│   │       │   ├── services/          # REST & WS clients, typings
│   │       │   └── utils/             # Helpers & polyfills
│   │       ├── tests/                 # Jest & Playwright for E2E
│   │       ├── tsconfig.json
│   │       ├── package.json
│   │       └── vite.config.ts
│   ├── libs/                          # Shared UI components & hooks
│   └── README.md
│
├── backend/                           # Go microservices (monorepo style)
│   ├── cmd/                           # Entrypoints per service
│   │   ├── auth/main.go
│   │   ├── world/main.go
│   │   ├── combat/main.go
│   │   └── ...                        
│   ├── services/                      # Service folders with clean architecture
│   │   ├── auth/
│   │   ├── character/
│   │   ├── world/
│   │   ├── combat/
│   │   ├── inventory/
│   │   ├── quest/
│   │   ├── chat/
│   │   ├── admin/
│   │   ├── analytics/
│   │   └── billing/                   # (Future: microtransactions)
│   ├── libs/                          # Reusable Go libraries
│   │   ├── config/                    # Viper/Env loader & schema
│   │   ├── logger/                    # Zap + structured logging
│   │   ├── middleware/                # HTTP, WS, auth middleware
│   │   ├── eventbus/                  # NATS/RabbitMQ client wrapper
│   │   ├── observability/             # Metrics (Prometheus), tracing (Jaeger)
│   │   └── security/                  # JWT, rate‑limiter, sanitizer
│   ├── proto/                         # .proto definitions & generated code
│   ├── tests/                         # Integration & contract tests
│   ├── go.mod
│   └── go.sum
│
├── infra/                             # Infrastructure as Code
│   ├── kubernetes/                    # Helm charts & Kustomize overlays
│   │   ├── base/
│   │   └── overlays/
│   │       ├── dev/
│   │       ├── staging/
│   │       └── prod/
│   ├── terraform/                     # Cloud provisioning (GCP/AWS/Azure)
│   ├── docker/                        # Dockerfiles & build scripts
│   ├── nginx/                         # Reverse proxy & SSL config
│   └── README.md
│
├── tools/                             # Developer utilities & CLIs
│   ├── migrate/                       # DB migration runner (Go CLI)
│   ├── seeder/                        # Initial data seeder
│   ├── asset-packer/                  # Sprite atlas generator
│   ├── ws-debugger/                   # WebSocket testing CLI
│   └── codegen/                       # API client & proto codegen
│
├── database/                          # Data schemas & seeds
│   ├── migrations/                    # SQL scripts per service
│   │   ├── auth/
│   │   ├── world/
│   │   └── ...
│   ├── seed/                          # YAML/JSON initial data
│   └── schema-diagrams/               # ERD & relationship charts
│
├── tests/                             # Cross‑cutting test suites
│   ├── e2e/                           # Full system E2E (Cypress/Playwright)
│   ├── performance/                   # k6 or JMeter load tests
│   ├── security/                      # OWASP ZAP scripts
│   └── chaos/                         # Chaos Monkey experiments
│
├── mods/                              # Community mod support (future)
│   ├── docs/                          # Modding API docs
│   └── sample-mod/                    # Template mod project
│
├── benchmarks/                        # Benchmarks & profiling scripts
│
├── .env                               # Local environment vars
├── .env.example
├── .gitignore
├── Makefile                           # Common tasks: build, lint, test, deploy
├── README.md
└── LICENSE
