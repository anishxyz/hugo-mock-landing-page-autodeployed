### CI/CD Steps

1. **Workflow Trigger**
   - The workflow runs whenever changes are pushed to the `main` branch of the repository.

2. **Job Setup**
   - A single job named "deploy" is defined to run on an Ubuntu 22.04 runner.

3. **Check Out Source Repository**
   - This step uses the `actions/checkout` action to fetch your repository code.
   - Includes submodules (which often contain Hugo themes).
   - Fetches the complete git history (for Hugo's .GitInfo and .Lastmod features).

4. **Initialize Hugo Environment**
   - Uses the `peaceiris/actions-hugo` action to set up Hugo version 0.144.1.
   - Enables extended features (required for SCSS/SASS processing and other advanced features).

5. **Compile Hugo Static Files**
   - Runs the Hugo command to build your website with several flags:
     - `-D`: Include draft content
     - `--gc`: Run garbage collection during the build
     - `--minify`: Minify the output HTML, CSS, JS, etc. to reduce file sizes

6. **Publish to GitHub Pages**
   - Uses the `peaceiris/actions-gh-pages` action to:
     - Create or update a `gh-pages` branch with the built website
     - Use GitHub's automatically generated token for authentication
     - Set the commit author to the GitHub Actions bot
     - (Optional) Set up a custom domain via CNAME if uncommented
