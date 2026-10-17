# EShop Project — Copilot Custom Instructions

## Project Context
- This is an **EShop e-commerce system** used as a **System Under Test (SUT)** for software testing coursework.
- The system specification is defined in `README.md` (Vietnamese).
- Students must design test cases using **Domain Testing** and **Boundary Value Analysis** techniques, then execute them against the SUT to find bugs.

## System Architecture
| Component       | Technology                  | Default URL             |
| --------------- | --------------------------- | ----------------------- |
| Backend API     | Node.js + Express + SQLite  | `http://localhost:3000`  |
| Frontend Web    | React + Vite + Tailwind CSS | `http://localhost:5173`  |
| Web Admin       | React + Vite + Tailwind CSS | `http://localhost:5174`  |
| Mobile App      | React Native + Expo         | LAN IP of host machine  |

## Testing Guidelines
- Always reference the **System Requirements Specification** in `README.md` as the single source of truth for expected behavior.
- The SUT is **intentionally seeded with bugs** — differences between specification and implementation are bugs to report.
- Test case IDs should follow the format: `TC-<FR>-<Technique>-<Number>` (e.g., `TC-FR01-DT-001` for Domain Testing, `TC-FR01-BVA-001` for Boundary Value Analysis).
- Bug reports must include: Bug ID, Title, Severity, Steps to Reproduce, Expected Result, Actual Result, Screenshot.

## Language
- All test documentation, bug reports, and analysis should be written in **Vietnamese**.
- Use technical terms in English where appropriate (e.g., Domain Testing, Boundary Value Analysis, equivalence class).
