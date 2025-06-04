
# 📚 Node-RED EPUB to PDF Workflow for reMarkable & Kavita

This repository contains a Node-RED flow designed to automate the process of delivering EPUB and PDF files to your reMarkable tablet via email.

## ✨ Features

- Accepts EPUB and PDF files via email
- Converts EPUB files to PDF using `epub_to_remarkable`
- Routes files based on subject line:
  - `Send to reMarkable` → pushed to reMarkable via Aviary
  - `Send to eReader` → saved to Kavita directory
- Uses FileBrowser to store temporary files
- Automatically deletes temporary files after processing
- Fully self-hosted using Docker

## 🛠 Requirements

You’ll need the following services running locally (Docker recommended):

| Service | GitHub | Port | Notes |
|--------|--------|------|-------|
| Node-RED | https://github.com/node-red/node-red | `1880` | Core automation |
| epub_to_remarkable | https://github.com/suntorytimed/epub_to_remarkable | `5004` | Converts EPUB to PDF |
| Aviary | https://github.com/rmitchellscott/aviary | `8011` | Pushes PDF to reMarkable *(API-generated token used if pairing fails)* |
| FileBrowser | https://github.com/filebrowser/filebrowser | `8087` | Stores and deletes files |

> ⚠️ FileBrowser must be run with `FB_NOAUTH=true` in this example. If you're exposing this to the internet, configure authentication and update your flow.

---

## ⚠ Notes

- I was unable to get Aviary to pair with my reMarkable via the standard method, so I used https://github.com/ddvk/rmapi to generate the rmapi.conf.
- Some of the code in this flow (e.g., function nodes) was **generated or assisted by AI tools**. Please use caution and review logic before deploying in production environments.

---

## 📥 Email Integration

The flow is triggered by incoming emails via IMAP. Example setup:

- Gmail with filters to move emails to:
  - Folder `ReMarkable` if subject is `Send to reMarkable`
  - Folder `Kavita Books` if subject is `Send to eReader`

## 📂 Files in This Repo

- `remarkable_epub_flow.json`  
  The sanitised Node-RED flow file ready to import into your local Node-RED instance.

## 🚀 Getting Started

1. Clone this repo
2. Start your supporting services (Node-RED, Aviary, FileBrowser, epub_to_remarkable)
3. Import the flow into Node-RED
4. Update folder names, server IPs, and authentication as needed
5. Send an email with a book attached and one of the two subject lines to trigger the flow

## 🙌 Credits

- [suntorytimed/epub_to_remarkable](https://github.com/suntorytimed/epub_to_remarkable)
- [rmitchellscott/aviary](https://github.com/rmitchellscott/aviary)
- [filebrowser/filebrowser](https://github.com/filebrowser/filebrowser)
- [node-red/node-red](https://github.com/node-red/node-red)

## 📧 Contact

Open an issue or submit a pull request for improvements or fixes. Happy automating!
