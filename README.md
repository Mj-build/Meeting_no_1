# Subproject for skills building 
This repo provides the team members an opportunity to learn the framework, the interconnectivity and testing the teams transferable skills 
through building a mini project that encompasses the aforementioned.

_regualar standups will be held to check team member progress_

# Arcitechture & Language stack 
* Information regarding the stack we are testing in this mini project is in [Multi_Era_RPG_Specifications.pdf](https://github.com/user-attachments/files/28322685/Multi_Era_RPG_Specifications.pdf)

# 🎮 Adaptive Combat Arena

> Unreal Engine 5.4 Combat System Project

---

# 🛠️ Development Setup Guide

## 📌 Overview

This guide explains how all team members must set up their development environment for the Adaptive Combat Arena project.

⚠️ All steps must be followed exactly to prevent build failures, Git conflicts, and Unreal asset corruption.

---

# 🧱 1. Core Requirements

- Unreal Engine 5.4
- Visual Studio 2022
- Git
- Git LFS

---

# 💻 2. Visual Studio Setup

## Install

winget install Microsoft.VisualStudio.2022.Community

## Workloads

- Game development with C++
- Desktop development with C++

## Components

- MSVC v143 (v14.38)
- Windows SDK
- CMake tools
- ATL + MFC

## Config

Development Editor | Win64

---

# 📦 3. Clone Repo

 git clone git@github.com:Mj-build/Meeting_no_1.git

---

# 📥 4. Pull LFS

 git lfs pull

---

# ⚙️ 5. Generate Files

Right click .uproject → Generate VS files

---

# 🧪 6. Build

Open .sln → Build Solution

---

# 🎮 7. Launch

Open .uproject

---

# 🌿 8. Workflow

 git checkout -b feature/name
 git add .
 git commit -m "feat"
 git push

---

# 🚨 Rules

- Same UE version
- Use LFS
- No binaries commit
- Pull before work

---

# ✅ Summary

Clone → LFS → Generate → Build → Develop
