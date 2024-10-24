# PetStore API Testing with Postman and Gihub Action

This repository contains a collection of API tests for the Pet Store API using Postman and Newman. It is designed to automate the process of API testing, ensuring that each endpoint works as expected. The setup integrates with GitHub Actions for continuous testing, providing a streamlined CI/CD workflow.

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Setup Instructions](#setup-instructions)
- [Running Tests Locally](#running-tests-locally)
- [Automated Testing with GitHub Actions](#automated-testing-with-github-actions)
- [Data-Driven Testing](#data-driven-testing)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

## Introduction

The **PetStore API Testing** project uses Postman collections to define test cases for various endpoints of a Pet Store API. The tests are executed using [Newman](https://www.npmjs.com/package/newman), a command-line runner for Postman collections, allowing you to automate API testing both locally and through GitHub Actions.

## Features

- **Comprehensive API Tests**: Includes tests for CRUD operations on Pet Store entities.
- **Automated Testing with GitHub Actions**: Automatically runs tests on every push or pull request to the `main` branch.
- **Data-Driven Testing**: Supports running tests with multiple data sets for broader test coverage.
- **Easy Setup**: Simple to clone, install dependencies, and run tests locally or through CI/CD.

## Setup Instructions

Follow these steps to set up the project and run the tests:

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/kazalbrur/PetStore_API_Testing_Postman_newman.git
   cd PetStore_API_Testing_Postman_newman
   ```

2. **Install Node.js**:
   Ensure you have Node.js installed on your system. If not, download it from [Node.js official website](https://nodejs.org/).

3. **Install Newman**:
   Install Newman globally using npm:
   ```bash
   npm install -g newman
   ```

## Running Tests Locally

To run the Postman collection locally using Newman, execute the following command:

```bash
newman run PetStoreAPI_Tests.postman_collection.json
```

This command runs all the test cases defined in the `PetStoreAPI_Tests.postman_collection.json` file. You can customize the run by adding options like `--reporters` for HTML or JSON reports.

## Automated Testing with GitHub Actions

This repository is set up with GitHub Actions to automatically run tests on every push or pull request to the `main` branch. The GitHub Actions workflow file is located at `.github/workflows/api-test.yml`.

### Workflow Overview

The GitHub Actions workflow:
- Checks out the code.
- Sets up Node.js and installs Newman.
- Runs the Postman collection using Newman.

To view the results of the workflow:
1. Go to the **Actions** tab in the GitHub repository.
2. Select the **API Testing** workflow.
3. View logs and results of the test runs.

## Data-Driven Testing

The **DataFiles** directory can be used to store data files (JSON/CSV) for data-driven testing. Update the collection to use these files for parameterized tests using the `data` option in Newman:

```bash
newman run PetStoreAPI_Tests.postman_collection.json --iteration-data DataFiles/testData.json
```

This command will run the tests using multiple sets of data, as defined in `testData.json`.

## Project Structure

```
PetStore_API_Testing_Postman_newman/
│
├── .github/
│   └── workflows/
│       └── api-test.yml           # GitHub Actions workflow for automated testing
│
├── DataFiles/
│   └── testData.json              # Example data file for data-driven tests
│
├── Documentation/
│   └── guide.md                   # Documentation and setup guide
│
├── PetStoreAPI_Tests.postman_collection.json  # Postman collection with API tests
│
├── README.md                      # Project overview and instructions (this file)
│
└── package.json                   # Node.js package file (if needed for scripts)
```

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Make your changes and commit them with a descriptive message.
4. Submit a pull request to the `main` branch for review.

## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/kazalbrur/PetStore_API_Testing_Postman_newman/blob/main/LICENSE) file for details.
