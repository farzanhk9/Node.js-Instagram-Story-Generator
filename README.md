#!/usr/bin/env bash
# File: bootstrap_insta_story_node.sh
# Usage: bash bootstrap_insta_story_node.sh [project-name]
set -euo pipefail
NAME="${1:-insta-story}"
[ -d "$NAME" ] && { echo "Directory '$NAME' exists"; exit 1; }
mkdir -p "$NAME"/{.github/workflows,examples}
cd "$NAME"

# ---------------- package.json ----------------
cat > package.json <<'EOF'
{
  "name": "insta-story",
  "version": "0.1.0",
  "type": "module",
  "description": "Instagram Story generator (1080x1920) with Node.js + canvas CLI.",
  "bin": {
    "insta-story": "story.js"
  },
  "scripts": {
    "start": "node story.js --help",
    "build": "echo 'No build step required'",
    "lint": "echo 'Add ESLint if needed'",
    "test": "node -e \"console.log('OK')\""
  },
  "author": "Your Name",
  "license": "MIT",
  "dependencies": {
    "canvas": "^2.11.2",
    "stackblur-canvas": "^2.7.0",
    "yargs": "^17.7.2"
  }
}
EOF

# ---------------- .gitignore ----------------
cat > .gitignore <<'EOF'
node_modules/
*.log
.DS_Store
story.jpg
story.png
dist/
EOF

# ---------------- LICENSE ----------------
cat > LICENSE <<'EOF'
MIT License

Copyright (c) 2025

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
(see full MIT text as usual)
EOF

# ---------------- README.md ----------------
cat > README.md <<'EOF'
# Insta Story (Node.js)

A configurable **Instagram Story** (1080×1920) generator using Node.js, `canvas`, and CLI options.

## Features
- Gradient or photo background (optional blur)
- Title, subtitle, CTA button (fonts, sizes, colors, positions)
- Logo placement (4 corners, scale, margin)
- Safe paddings for story
- Pure image output (`.jpg` or `.png`)

## Quick Start
```bash
npm i
node story.js --title "Big Sale!" --subtitle "Up to 40% off" --cta "Shop now" \
  --bgType gradient --gradColors "#1e3c72,#2a5298" --output story.jpg


