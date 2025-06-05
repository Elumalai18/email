name: CI

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Run build
        run: |
          echo "Build running..."
          # Add your build commands here
          
      - name: Send email on success
        if: success()
        uses: dawidd6/action-send-mail@v3
        with:
          server_address: smtp.example.com
          server_port: 587
          username: ${{ secrets.SMTP_USERNAME }}
          password: ${{ secrets.SMTP_PASSWORD }}
          subject: Build Passed
          body: Your build succeeded!
          to: your-email@example.com
          from: github-actions@example.com

      - name: Send email on failure
        if: failure()
        uses: dawidd6/action-send-mail@v3
        with:
          server_address: smtp.example.com
          server_port: 587
          username: ${{ secrets.SMTP_USERNAME }}
          password: ${{ secrets.SMTP_PASSWORD }}
          subject: Build Failed
          body: Your build failed! Please check.
          to: your-email@example.com
          from: github-actions@example.com
