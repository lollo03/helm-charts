# PhotoPrism Helm Chart (Simple Deployment)

This Helm chart deploys [PhotoPrism®](https://www.photoprism.app/), a server-based application for browsing, organizing, and sharing your personal photo collection.

> **Note:** This chart is designed for a **simple, self-contained deployment**. It is ideal for **personal use, testing, or for users getting started with PhotoPrism on Kubernetes**. It uses the built-in SQLite database and is not configured for high availability or very large-scale libraries.

## Chart Design and Limitations

To maintain simplicity, this chart makes the following design choices:

*   **SQLite Database:** It uses the embedded SQLite database that comes with PhotoPrism. The database file is stored on the `storage` persistent volume. This avoids the complexity of managing a separate database instance.
*   **No External Database Support:** This chart does not support connecting to an external MariaDB or MySQL database.
*   **Single Replica:** The deployment is limited to a single pod with a `Recreate` update strategy. 

If you require high performance for a very large library, high availability, or external database support, consider a more advanced Helm chart or deployment method.

## Installing the Chart

**IMPORTANT:** You must set a secure `config.adminPassword` during installation.

## Persistence

This chart provisions two `PersistentVolumeClaim`s to store data:

1.  **Originals Volume:** Stores your original photo and video files. You should set this large enough to hold your entire library.
2.  **Storage Volume:** Stores PhotoPrism's internal data, including the **SQLite database file**, thumbnails, and sidecar files.