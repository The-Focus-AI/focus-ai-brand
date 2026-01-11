---
name: update
description: Update the local focus-ai-brand plugin by pulling the latest changes from git
---

# Update Focus.AI Brand Plugin

Pull the latest changes for this plugin from the git repository.

## Instructions

1. Change to the plugin directory:
   ```bash
   cd ${CLAUDE_PLUGIN_ROOT}
   ```

2. Pull the latest changes:
   ```bash
   git pull
   ```

3. Report the result to the user, including:
   - Whether any updates were pulled
   - The latest commit message if updated
   - Remind them to restart Claude Code if there were significant changes
