name: Build and Publish Training Dashboard

on:
  push:
    branches: [ main ]

jobs:
  build_and_publish:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v4

    - name: Setup Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.10'

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Run training dashboard generator
      run: |
        python src/generate_all_advanced.py

    - name: Upload outputs as artifact
      uses: actions/upload-artifact@v4
      with:
        name: dashboard-outputs
        path: outputs_advanced/

    - name: Deploy HTML Dashboard to GitHub Pages
      uses: peaceiris/actions-gh-pages@v6
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./outputs_advanced
        publish_branch: gh-pages
<!--
**kaskis7070/Kaskis7070** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
