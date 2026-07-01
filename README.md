# Cluster Files - Release Repository

This repository contains the build workflow scripts, license, and instructions to download, install, and configure **Cluster Files** and **Cluster Auto** on Android.

---

## 📥 How to Download & Install

1. Navigate to the **Releases** section on the right side of this GitHub repository page.
2. Download the latest `cluster-files-release.apk`.
3. Transfer the APK to your phone and install it (make sure you allow installation from "Unknown Sources" in your browser/file explorer if prompted).

---

## ⚙️ How to Configure Root Directory Access

This setup explains how to configure and use **Cluster Files** and **Cluster Auto** to unlock root directory access on your Android phone.

### 📦 Required Applications
To browse root directories, you must install the following two apps on your phone:
1. **Cluster Files** (`com.zk.clfiles`) - The main file manager application.
2. **Cluster Auto** (`com.zk.clAuto`) - The background bridge manager daemon application.

### ⚙️ Prerequisites (Android Setup)
1. **Enable Developer Options**:
   * Open Android **Settings** -> **About Phone**.
   * Locate the **Build Number** and tap it 7 times until you see a message saying *"You are now a developer"*.
2. **Enable USB Debugging**:
   * Go back to **Settings** -> **System** -> **Developer Options**.
   * Scroll down and toggle **USB Debugging** to **ON**.
   * *(Optional)* If using wireless debugging, also turn **Wireless Debugging** to **ON**.

### 🚀 Starting the Daemon Service

#### Option A: Rooted Devices (100% Unrestricted Root Access)
If your phone is rooted (using Magisk, KernelSU, or APatch):
1. Open the **Cluster Auto** app on your phone.
2. Tap **Start via Root** (or **Start** under root settings).
3. Grant **Superuser (Root)** access when prompted.
4. *Access Level:* You will have 100% full read/write permission to every directory on the system (including protected paths like `/data/data` and `/dev/__properties`).

#### Option B: Non-Rooted Devices (Shell-Level Access via ADB)
If your phone is not rooted, you can start the service using a computer via ADB:
1. Connect your phone to your computer with a USB cable.
2. Open a terminal / command prompt on your computer.
3. Run the following command to dynamically locate and execute the starter binary:
   ```bash
   adb shell $(pm path com.zk.clAuto | cut -d: -f2 | sed 's/base.apk/lib\/arm64\/libshizuku.so/')
   ```
4. *Access Level:* The helper will run under the `shell` user (UID 2000). You will be able to browse the system root (`/`), read/write to `/data/local/tmp`, and view system file configurations, but you will not have permission to read restricted root-only system directories.

### 🔒 Authorization Settings
By default, the following applications are **automatically pre-authorized** to connect to the daemon:
* `com.zk.clfiles` (Cluster Files)
* `com.zk.clandro` (CL-Andro)
* `com.zk.clbrowser` (CL-Browser)

You do **not** need to manually toggle permission switches inside the Cluster Auto app for these applications. Once the daemon is started, simply open **Cluster Files** and click on **Root Directory** to begin browsing.
