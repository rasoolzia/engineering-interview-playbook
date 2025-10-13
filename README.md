# Engineering Interview Playbook

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/rasoolzia/engineering-interview-playbook?style=social)](https://github.com/rasoolzia/engineering-interview-playbook)
[![GitHub forks](https://img.shields.io/github/forks/rasoolzia/engineering-interview-playbook?style=social)](https://github.com/rasoolzia/engineering-interview-playbook)

## About the Project

**Engineering Interview Playbook** is an open-source collection of real-world programming and technical interview questions, organized by topic and available in **English** and **Persian (Farsi)**.

The goal is simple: help developers prepare better for job interviews at tech companies — from startups to big tech.

Questions are organized by category (Frontend, Backend, Algorithms, System Design, and more) with separate JSON files for English and Persian. This structure improves maintainability and powers a fast, visual, and interactive user experience on the website.

See it in action: [https://playbook.mrzd.ir](https://playbook.mrzd.ir)

This repo will eventually power an interactive web app where users can:

- Browse questions by category
- Filter by difficulty (Easy / Medium / Hard)
- Switch between English and Persian
- Search keywords
- View code snippets and follow-up questions

## Current Structure (Category-based JSON files)

We chose the **per-category** approach (one file per topic per language) because:

- Fewer files → easier to manage
- One fetch per category → better performance in the future app
- Clear separation of languages → easier translation and review
- Still granular enough for contributions
