# Changing the Repository URL in Git

If you need to update the URL of your Git repository, follow these commands:

1. **Remove the existing remote named 'origin':**
   ```bash
   git remote remove origin
   ```
   This command removes the remote named 'origin' from your repository configuration.

2. **Add the new repository URL as the remote 'origin':**
   ```bash
   git remote add origin <Your complete URL here>
   ```
   Replace `<Your complete URL here>` with the URL of the new repository. This sets the new URL as the remote named 'origin.'

3. **Verify the new remote URL:**
   ```bash
   git remote -v
   ```
   This command displays the configured remote repositories. Ensure that the 'origin' remote now points to the new URL.

4. **Set the upstream branch to track changes from 'origin/dev/main':**
   ```bash
   git branch --set-upstream-to=origin/dev/main
   ```
   This sets the upstream branch to track changes from the 'dev/main' branch on the 'origin' remote.

5. **Stash your changes (if needed):**
   ```bash
   git stash
   ```
   Use this command to temporarily save your local changes in case they conflict with incoming changes from the new repository URL.

6. **Pull the latest changes from the new URL:**
   ```bash
   git pull
   ```
   Finally, run this command to fetch and merge the latest changes from the updated repository URL. This ensures your local branch is synchronized with the remote.

These commands are useful when you need to switch the remote URL of your Git repository and align your local branch with the changes from the new repository location.