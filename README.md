# 🌐 ASP.NET Core Web App on Azure

Welcome to **Anjani Netala's** ASP.NET Core Web Application, deployed on Microsoft Azure using GitHub Actions CI/CD.  
This project was created as part of a learning exercise to understand Azure App Services and automated deployment.

> 👩‍💻 Name: Anjani Netala  
> 🧾 Student ID: 500238659  
> 🌍 Live Site: [anjani500659webapp.azurewebsites.net](https://anjani500659webapp.azurewebsites.net)

---

## 🚀 Technologies Used

- ASP.NET Core 8.0
- Razor Pages
- HTML5 & CSS3
- GitHub Actions
- Azure App Service (Linux)
- Azure CLI

---

## 🛠️ Features

- Responsive and modern UI layout
- Custom header and footer
- Student info and welcome message
- GitHub-based CI/CD pipeline
- Azure Web App hosting

---

## 🔁 Deployment Pipeline (CI/CD)

This project uses **GitHub Actions** to automatically build and deploy changes to Azure whenever new code is pushed to the `master` branch.

### ✅ Workflow File: `.github/workflows/azure-webapp.yml`

```yaml
name: Deploy ASP.NET Core app to Azure Web App

on:
  push:
    branches:
      - master

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Setup .NET
        uses: actions/setup-dotnet@v3
        with:
          dotnet-version: '8.0.x'

      - name: Restore dependencies
        run: dotnet restore

      - name: Build
        run: dotnet build --configuration Release

      - name: Publish
        run: dotnet publish --configuration Release --output ./publish

      - name: Deploy to Azure Web App
        uses: azure/webapps-deploy@v2
        with:
          app-name: anjani500659webapp
          publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
          package: ./publish
