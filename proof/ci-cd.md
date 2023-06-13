# CI/CD

# What is CI/CD?
> In software engineering, CI/CD is the combined practices of continuous integration (CI) and continuous delivery. 
[Wikipedia CI/CD](https://en.wikipedia.org/wiki/CI/CD)

![CICD Image](https://user-images.githubusercontent.com/93530655/199507551-dc179c00-2907-4b91-bdb2-671c3baf4c51.png)
***
## CI
To integrate new code into my project seamlessly, I use different branches. Whenever I need to add a new feature or fix an issue, I create a separate branch.
Once the feature is complete or the problem is fixed, I merge the branch back into the "Main Branch."

After pushing a branch or completing a merge, I rely on SonarCloud for code quality and test coverage analysis. SonarCloud is a helpful tool that
performs static code analysis on the code I've written and provides insights into code coverage for my project. You can check out my project
on SonarCloud by [clicking here](https://sonarcloud.io/organizations/dpils-s/projects). If you want to learn more about SonarCloud, you can refer to [SonarCloud here](https://docs.sonarcloud.io/).


<details>
  <summary>Example CI workflow (used in front-end)</summary>
  
   ``` yml
  # This workflow will build and Test a Vue + JavaScripr project
# For more information see: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-net

name: Continuous Integration && SonarCloud

on:
  push:
    branches:
      - main
      - master
  pull_request:
    branches:
      - main
      - master

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: 16

      - name: Install dependencies
        run: npm ci

      - name: Build
        run: npm run build

      - name: Test coverage
        run: npm run test:coverage

      - name: SonarCloud Scan
        uses: sonarsource/sonarcloud-github-action@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} 
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }} 
        with:
          args:
            -Dsonar.projectKey=Dpils-s_Rider-maps
            -Dsonar.organization=dpils-s

  ```
  
  </details>
  
  ## CD
To continuously deliver the project I use [Docker](https://docs.docker.com/get-started/). After a successful merge into main, the CD pipeline creates 
a docker image from the main branch, and publishes it on [Dockerhub](https://hub.docker.com/repository/docker/artjomf/maps/general).

<details>
  <summary>Example CD workflow (used in front-end)</summary>
  
  ``` yml
name: Continuous Delivery

on:
  push:
    branches:
      - main

jobs:
  build_and_deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2

    - name: Set up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: 16

    - name: Install dependencies
      run: npm ci

    - name: Build Docker image
      run: docker build -t ${{ secrets.DOCKER_HUB_USERNAME }}/maps .

    - name: Login to Docker Hub
      uses: docker/login-action@v1
      with:
        username: ${{ secrets.DOCKER_HUB_USERNAME }}
        password: ${{ secrets.DOCKER_HUB_ACCESS_TOKEN }}

    - name: Push Docker image
      run: |
        docker tag ${{ secrets.DOCKER_HUB_USERNAME }}/maps artjomf/maps:${{ github.sha }}
        docker push ${{ secrets.DOCKER_HUB_USERNAME }}/maps:${{ github.sha }}
        docker tag ${{ secrets.DOCKER_HUB_USERNAME }}/maps:${{ github.sha }} artjomf/maps:latest
        docker push ${{ secrets.DOCKER_HUB_USERNAME }}/maps:latest
  ```
</details>
