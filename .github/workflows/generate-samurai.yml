name: Generate Snake
on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:

# Avoid two runs stepping on each other's push to the output branch.
concurrency:
  group: generate-snake
  cancel-in-progress: true

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5
    steps:
      - name: Generate snake
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: Matheusin9
          # "Sunset" (light) + "Neon night" (dark) — a warm gradient that pops
          # on GitHub's light theme, and a purple-to-cyan gradient that pops
          # on the dark theme, each with a snake color chosen for contrast
          # against its own palette instead of the default green/black.
          outputs: |
            dist/github-contribution-grid-snake.svg?color_snake=%231b6ca8&color_dots=%23ebedf0,%23ffd8a8,%23ffb677,%23ff8c42,%23ff5757
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark&color_snake=%2300e0ff&color_dots=%23161b22,%233a2e50,%236a4c93,%23b185db,%23ff6ec7

      - name: Push snake to output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
