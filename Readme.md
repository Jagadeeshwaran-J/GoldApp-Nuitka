
# 🪙 Gold Detection Project (.EXE Packaging)

This repository contains a complete solution for detecting **gold bars and coins** using a deep learning model. The project is securely packaged into a Windows `.exe` executable using **Nuitka**, providing performance, security, and ease of deployment.

---

## 📁 Final Folder Structure (Client Delivery)

```
GoldProject_Final/
├── Gold_detector.exe              # Compiled executable
├── config.yaml                    # Detection and runtime settings
├── data.yaml                      # Input/output data schema
├── Model_encrypt.pt               # AES-encrypted model file
├── instantclient_23_8/           # Oracle DB connectivity dependencies
```

---

## 🧠 Project Overview

- 🔍 Detects gold **bars** and **coins** using a YOLO-like or RT-DETR model
- 🔐 Model is AES-encrypted (`Model_encrypt.pt`)
- 🧾 Results are validated against an Oracle database
- 💻 Converted to `.exe` with Nuitka for secure, standalone execution

---

## ⚙️ Setup Instructions (Developer Side)

### 1. 🧪 Create and Activate Virtual Environment
```bash
python -m venv .venv
.venv\Scripts\activate
```

### 2. 📦 Install Dependencies
```bash
pip install -r requirements.txt
pip install nuitka
```

### 3. 🔨 Convert Python Script to `.exe`
Use this command (or `build_gold_exe.bat`):
```bash
python -m nuitka Gold_detector.py ^
  --standalone ^
  --enable-plugin=torch ^
  --enable-plugin=numpy ^
  --include-data-files=config.yaml=config.yaml ^
  --include-data-files=data.yaml=data.yaml ^
  --include-data-files=Model_encrypt.pt=Model_encrypt.pt ^
  --include-data-dir=instantclient_23_8=instantclient_23_8 ^
  --output-dir=dist
```

Output:  
`dist/Gold_detector.dist/Gold_detector.exe`

---

## ▶️ How to Run the Executable (Client Side)

```bash
cd GoldProject_Final
Gold_detector.exe
```

Sample Output:
```
Gold bars detected: 4
Gold coins detected: 10
DB Validation: MATCHED
Result saved: output/result.json
```

---

## 🔐 AES Encryption Usage

| Component         | Protection Method                           |
|------------------|----------------------------------------------|
| Model file        | Encrypted with AES and decrypted in memory  |
| Key used          | Hardcoded inside `.exe` (`NcsSoftSolutions`)|
| Source code       | Fully compiled to C binary via Nuitka       |

This ensures your model and business logic remain protected during distribution.

---

## 🧾 What to Deliver to Client

| File / Folder         | Description                                 |
|-----------------------|---------------------------------------------|
| `Gold_detector.exe`   | Compiled executable                         |
| `config.yaml`         | Runtime parameters                          |
| `data.yaml`           | Schema for detection input/output           |
| `Model_encrypt.pt`    | AES-encrypted model file                    |
| `instantclient_23_8/` | Required Oracle DB drivers and libraries    |

🛑 **Do NOT include:**
- `.venv/` – Used only during development
- `*.py` – All source code is compiled
- `*.bat` or build scripts

---

## 📦 Why Use `.venv`?

| Reason                    | Explanation                                                        |
|---------------------------|--------------------------------------------------------------------|
| Isolation                 | Keeps project dependencies separate from system Python            |
| Consistency               | Ensures same environment for development and Nuitka compilation   |
| Clean deployment          | Not required after `.exe` build, so not shipped to client         |

---

## ✅ Pros and Cons of This Packaging Method

### ✅ Pros:
- ✅ Source code is compiled and obfuscated
- ✅ Model is encrypted and secure
- ✅ Single-folder delivery (portable)
- ✅ Oracle client bundled (no install needed)

### ⚠️ Cons:
- ⏳ Slightly longer build time than PyInstaller
- 🧪 `.exe` size can be large due to embedded libraries
- 🔍 Debugging issues post-compilation can be harder

---

## 🛠 Troubleshooting

| Issue                              | Solution                                                         |
|------------------------------------|------------------------------------------------------------------|
| EXE closes immediately             | Run from Command Prompt to view errors                           |
| Oracle connection error            | Confirm `instantclient_23_8/` is in same folder                  |
| Model not detected                 | Ensure `Model_encrypt.pt` is not corrupted                       |
| Antivirus flags EXE                | Zip before sharing or sign binary using a certificate            |

---

## 📃 License

```
© 2025 NCS Soft Solutions Pvt. Ltd.  
This project is proprietary and confidential. Do not distribute without permission.
```

---

## 🙋‍♂️ Contact

**Author**: Jagadeeshwaran.J  
**Company**: NCS Soft Solutions Pvt. Ltd.  
**Email**: jagadeeshwaran@example.com

---

## 📌 GitHub Usage

1. Commit all files except `.venv/`, `.pyc`, `__pycache__/`, and `*.py`
2. Push using:
```bash
git init
git remote add origin https://github.com/yourname/gold-project.git
git add .
git commit -m "Initial commit"
git push -u origin main
```

---

## 📥 Download & Usage

Clients can download the `.zip` file or receive via physical media. No installation required. Just **unzip and double-click** `Gold_detector.exe`.

---
