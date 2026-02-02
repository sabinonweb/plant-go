#🌱 PlantGO – Solana NFT Program
===============================

PlantGO is a Solana smart contract that powers a gamified plant discovery ecosystem.It allows users to mint plant-based NFT cards with dynamic rarity logic, ownership tracking, and on-chain supply control.

This program handles:

*   🌿 Plant-based NFT minting
    
*   🎖 Dynamic rarity distribution
    
*   🏆 First discovery rewards
    
*   🧠 Quiz-based NFT rewards
    
*   📊 On-chain supply counters
    
*   🔐 Ownership verification via PDA
    

📦 What This Program Does
-------------------------

This Solana program:

1.  Creates NFT mint accounts (SPL Token mint).
    
2.  Mints NFTs to users.
    
3.  Determines rarity dynamically based on:
    
    *   First discovery
        
    *   New species
        
    *   Supply caps
        
    *   Quiz participation
        
4.  Prevents duplicate ownership using Program Derived Accounts (PDAs).
    
5.  Tracks plant-specific NFT supply counters on-chain.
    

All instructions are serialized using **Borsh**.

🧠 Rarity System
----------------

NFTs are not randomly minted. They follow deterministic on-chain logic.

### Card Types

Rarity TypeDescriptionGenesisFragmentCommon NFTAstralShardRare NFTMythicCrestEpic NFTPrimordialRelicFirst discoverer of known plantAuroraSeedFirst discoverer of new speciesCodexOfInsightQuiz participation rewardAscendantSealQuiz winner reward

### 🌟 Rarity Logic Flow

#### First Discovery Rules

*   If plant is **new species** AND first on-chain → AuroraSeed
    
*   If plant is **known species** AND first on-chain → PrimordialRelic
    

#### Supply-Based Distribution

*   Epic capped at MAX\_EPIC = 20
    
*   Rare capped at MAX\_RARE = 50
    
*   After caps → Common (GenesisFragment)
    

#### Quiz NFTs

*   Quiz winner → AscendantSeal
    
*   Quiz participant → CodexOfInsight
    

🏗 Architecture Overview
------------------------

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   Frontend (Web / Mobile)        ↓Serialize Instruction (Borsh)        ↓Solana Program (Rust)        ↓SPL Token Program        ↓Mint NFT to User ATA   `

🔐 Program Derived Accounts (PDAs)
----------------------------------

### Ownership PDA

Prevents duplicate NFT ownership per user per plant per rarity.

**Seeds:**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   [plant_name, user_wallet, card_type]   `

### Plant Counter PDA

Tracks total mint supply per plant.

**Seeds:**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   ["plant_counter", plant_name]   `

📚 Instructions
---------------

### CreateMint

Creates a new SPL Token mint.

#### Required Accounts

*   Mint account (new)
    
*   Mint authority
    
*   Payer
    
*   Rent sysvar
    
*   System program
    
*   SPL Token program
    

#### Frontend Payload

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   {  "nft_title": "Aurora Seed",  "nft_symbol": "PGA",  "nft_uri": "ipfs://Qm..."}   `

### MintNFT

Mints an NFT to the user's associated token account.

#### Required Accounts

*   User wallet
    
*   Common mint
    
*   Rare mint
    
*   Epic mint
    
*   Aurora mint
    
*   Primordial mint
    
*   Mint authority
    
*   Associated token account
    
*   Payer
    
*   Rent sysvar
    
*   System program
    
*   SPL Token program
    
*   Ownership PDA
    
*   Plant Counter PDA
    

#### Frontend Payload

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   {  "card_type": "GenesisFragment",  "plant_name": "Sunflower",  "is_new_species": false,  "quiz_winner": false}   `

🛠 How to Run the Blockchain Part
---------------------------------

### 1️⃣ Install Dependencies

#### Install Solana CLI

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   sh -c "$(curl -sSfL https://release.solana.com/stable/install)"   `

Verify installation:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   solana --version   `

#### Install Rust

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   curl https://sh.rustup.rs -sSf | sh   `

### 2️⃣ Build the Program

From the project root:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   cargo build-sbf   `

The compiled binary will be generated at:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   target/deploy/plant_program.so   `

### 3️⃣ Start Local Validator

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   solana-test-validator   `

In another terminal:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   solana config set --url localhost   `

### 4️⃣ Deploy the Program

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   solana program deploy target/deploy/plant_program.so   `

You will receive a **Program ID**.

Save this Program ID — the frontend must use it when sending transactions.

# plant-go-frontend

Plant identification and gamified learning mobile application built with Flutter.

## Quick Start

### Prerequisites
- Flutter SDK 3.7.0+
- Android Studio or Xcode
- Firebase account

### Installation

```bash
git clone <repository-url>
cd plantgo-frontend
flutter pub get
```

Configure Firebase by adding `google-services.json` (Android) and `GoogleService-Info.plist` (iOS) to their respective directories.

```bash
flutter run
```

## Features

### Plant Scanner
Real-time plant identification using camera with WebSocket streaming to Go backend. Supports both live video streaming and single image scanning.

**Backend Endpoints:**
- WebSocket: `ws://localhost:8080/scan/video`
- HTTP: `POST http://localhost:8080/scan/image`

**Protocol:**
```json
// Client -> Server
{
  "type": "frame",
  "data": {
    "image": "base64_encoded_image",
    "timestamp": 1640995200000
  }
}

// Server -> Client
{
  "type": "prediction",
  "data": {
    "prediction": "Rose",
    "confidence": 0.85
  }
}
```

### Plant Riddles
Progressive plant-themed challenges with backend integration. Fallback to mock data when backend unavailable.

**Endpoints:**
- `GET /riddles/level/{levelIndex}` - Riddle by level
- `GET /riddles/active` - Active riddles
- `GET /riddles` - All riddles

### Interactive Map
Geolocation-based plant discovery using Flutter Map and Firebase Firestore. Add plants with photos and GPS coordinates.

### User Authentication
Firebase Authentication with email/password, Google Sign-In, and guest mode support.

### Progress Tracking
Streak tracking, achievements, course completion, and profile management with Firebase Firestore persistence.

## Architecture

Clean Architecture with three layers:

```
Presentation (UI + BLoC)
    ↓
Domain (Use Cases + Entities)
    ↓
Data (Repositories + API)
```

**State Management:** flutter_bloc  
**Dependency Injection:** GetIt + Injectable  
**Networking:** Dio + Retrofit  
**Database:** Firebase (Auth, Firestore)

## Project Structure

```
lib/
├── api/              REST API services
├── core/             Dependency injection, services
├── data/             Models, repository implementations
├── domain/           Entities, use cases, repository interfaces
├── presentation/     Screens, blocs, widgets
├── services/         App-specific services
└── configs/          App configuration
```

## Configuration

### Backend URL
Configure in `lib/core/constants/app_constants.dart`:
```dart
static const String baseUrl = 'http://your-ip:8080';
```

Can be changed at runtime via Settings screen.

### Firebase
Config files required:
- Android: `android/app/google-services.json`
- iOS: `ios/Runner/GoogleService-Info.plist`

## Development

### Code Generation
```bash
flutter pub run build_runner build --delete-conflicting-outputs
```

### Analysis
```bash
flutter analyze
flutter format .
```

### Testing
```bash
flutter test
```

## Key Dependencies

| Package | Purpose |
|---------|---------|
| flutter_bloc ^8.1.6 | State management |
| dio ^5.7.0 | HTTP client |
| retrofit ^4.4.1 | Type-safe API |
| firebase_core ^2.24.2 | Firebase integration |
| camera ^0.10.5+5 | Camera access |
| flutter_map ^6.1.0 | Map display |
| get_it ^7.7.0 | Dependency injection |

See [pubspec.yaml](pubspec.yaml) for complete list.

## Known Issues

- Some cubits use mock data pending full backend integration
- Info-level analyzer warnings (avoid_print, deprecated_member_use) present but non-critical

## Recent Changes

### v1.0.0 (2026-01-01)
- Fixed dependency conflict (retrofit_generator -> v9.2.0)
- Removed duplicate service files
- Fixed linting warnings
- Consolidated documentation



#plant-go-backend
# Project plantgo-backend

## Getting Started

### Prerequisites
- [Docker](https://www.docker.com/)
- [Make (optional)](https://www.gnu.org/software/make/)

## MakeFile

Run bckend on docker with containerized DB
```bash
make docker-run
```

Live reload the application:
```bash
make watch
```

Shutdown DB Container
```bash
make docker-down
```

DB Integrations Test:
```bash
make itest
```

Run build make command with tests
```bash
make all
```

Build the application
```bash
make build
```

Run the application
```bash
make run
```

Run the test suite:
```bash
make test
```

Clean up binary from the last build:
```bash
make clean
```

## Swagger UI for API Documentation

Test the API endpoints here :
```bash
http://localhost:8080/swagger/index.html
```

## Wanna interact with db ?

Connect to db
```bash
docker exec -it plantgo-backend-plantgo_postgres-1 psql -U gogo -d plantgo_db
```

## Swagger UI Docs

Endpoints interaction 
```bash
swag init -g ./cmd/api/main.go -o ./cmd/api/docs
`
