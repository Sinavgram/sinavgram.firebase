# Sınavgram Firebase Infrastructure

**Sınavgram Firebase** contains the Firebase infrastructure configuration and service definitions used by the Sınavgram educational platform.

This repository preserves the Firebase-related configuration of the project, including Cloud Firestore security rules, database indexes, Firebase Storage rules, Hosting configuration, and authentication provider settings.

It is published as part of the Sınavgram project retirement and open-source release.

> **Project Status: Archived / Retired**
>
> This repository is provided for historical reference, infrastructure preservation, and educational purposes. The original production infrastructure and its data are not included.

## Overview

Sınavgram uses Firebase services to support several backend-related application features.

This repository contains the configuration files required to describe and manage parts of that infrastructure.

Unlike the main application and backend repositories, this repository focuses specifically on Firebase service configuration rather than application logic.

## Firebase Services

| Service | Purpose |
|---|---|
| Cloud Firestore | Database security rules and index definitions |
| Firebase Storage | File and image storage access rules |
| Firebase Hosting | Static content hosting |
| Firebase Authentication | Authentication provider configuration |
| Firebase Remote Config | Remote configuration support |

### Cloud Firestore

The repository includes Firestore security rules and index definitions.

**Current configuration includes:**
- Public read access for questions.
- Authenticated question submission and updates.
- Public read access for course-related documents.
- User-specific access restrictions for user documents.
- Additional authenticated-user access rules.
- Composite indexes for question queries.

Database location configured in `firebase.json`:

```text
europe-west3
```

### Firebase Storage

Storage rules define access permissions for uploaded files.

Configured storage paths include:

| Path | Access |
|---|---|
| `/avatars/{userId}` | Public read, owner-only write |
| `/question_images/{imageId}` | Public read, authenticated write |
| Other paths | Authenticated read and write |

These rules represent the configuration preserved in this repository, not a guarantee that the original production storage remains available.

### Firebase Authentication

The Firebase configuration includes support for:

- Email and password authentication.
- Google Sign-In.

Provider settings are defined in `firebase.json`.

### Firebase Hosting

Firebase Hosting is configured to use the `public/` directory as its deployment root.

The configuration excludes Firebase configuration files, hidden files, and `node_modules` from deployment.

### Firebase Remote Config

The Firebase configuration references a Remote Config template.

Remote Config support is part of the preserved infrastructure configuration. The original production configuration and values are not guaranteed to be available in this repository.

## Repository Structure

```text
sinavgram.firebase/
│
├── public/                  # Firebase Hosting public directory
│
├── .firebaserc              # Firebase project association
├── .gitattributes
├── .gitignore
│
├── firebase.json            # Firebase service configuration
│
├── firestore.rules          # Cloud Firestore security rules
├── firestore.indexes.json   # Firestore index definitions
│
└── storage.rules            # Firebase Storage security rules
```

## Getting Started

### Requirements

- Node.js
- npm
- Firebase CLI
- A Google account
- A Firebase project

### 1. Clone the repository

```bash
git clone https://github.com/Sinavgram/sinavgram.firebase.git

cd sinavgram.firebase
```

### 2. Install Firebase CLI

```bash
npm install -g firebase-tools
```

### 3. Authenticate

```bash
firebase login
```

### 4. Configure your Firebase project

The repository contains a `.firebaserc` file referencing the original Sınavgram Firebase project.

For independent development, use your own Firebase project instead of deploying to the original project.

You can associate your project using:

```bash
firebase use --add
```

Review `firebase.json` and ensure all referenced configuration files are available before deployment.

### 5. Deploy Firebase configuration

**Firestore rules**

```bash
firebase deploy --only firestore:rules
```

**Firestore indexes**

```bash
firebase deploy --only firestore:indexes
```

**Storage rules**

```bash
firebase deploy --only storage
```

**Hosting**

```bash
firebase deploy --only hosting
```

**All configured services**

```bash
firebase deploy
```

Deployment requires an appropriately configured Firebase project and the necessary permissions.

## Security Considerations

The security rules included in this repository reflect the original project's configuration and should not automatically be considered suitable for a new production deployment.

In particular:

- Authenticated users can write to the questions collection.
- The Firestore catch-all rule allows authenticated users to read and write otherwise unmatched documents.
- Authenticated users can upload question images.
- Storage access outside explicitly defined paths requires authentication.

Review and adapt these rules before deploying them to a new Firebase project.

Never assume that historical production security rules represent current security best practices.

## Data Availability

**This repository does not contain Sınavgram's production data.**

The public release includes infrastructure configuration files, not a production database backup or storage archive.

The following resources are not distributed:

- Cloud Firestore production documents.
- User accounts and authentication records.
- Uploaded profile pictures.
- Uploaded question images.
- Production user-generated content.
- Original production credentials.
- Private Firebase configuration values.

The repository preserves the configuration structure without exposing the original production data.

## Project Retirement

Sınavgram is being retired, and its source code and infrastructure configuration are being made publicly available.

This repository is part of that preservation effort.

The original Firebase infrastructure is not intended to be provided as a reusable hosted service.

Please note:

- No active development is planned.
- No production infrastructure availability is guaranteed.
- No production data is distributed.
- Historical configuration may require modifications to work with a new Firebase project.
- Issues and support requests may not receive a response.

## Related Repositories

The following repositories contain other components of the Sınavgram project:

| Repository | Description |
|---|---|
| [sinavgram](https://github.com/Sinavgram/sinavgram) | Latest Flutter mobile application |
| [sinavgram.old](https://github.com/Sinavgram/sinavgram.old) | Legacy Flutter application |
| [sinavgram.backend.old](https://github.com/Sinavgram/sinavgram.backend.old) | Legacy Python/Flask backend |
| [sinavgram.firebase](https://github.com/Sinavgram/sinavgram.firebase) | Firebase infrastructure configuration |

## License

No explicit open-source license has been specified for this repository.

Public availability does not automatically grant permission to redistribute or commercially use the contents. Please refer to the repository's license information before reusing the configuration or other materials.

## Author

**Mehmet Alper Kocaoğlu**

- GitHub: [@mehmetalper04](https://github.com/mehmetalper04)
- Organization: [Sinavgram](https://github.com/Sinavgram)

---

*Preserving the infrastructure behind Sınavgram.*

*The project may be retired, but its source code remains available for exploration and learning.*
