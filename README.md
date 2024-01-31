# poc-sbom-javascript

In this Proof of Concept (POC), we'll leverage GitHub Actions and npm to generate and verify the Software Bill of Materials (SBOM) for a straightforward JavaScript application.

### What is a SBOM?

> A “software bill of materials” (SBOM) has emerged as a key building block in software security and software supply chain risk management. A SBOM is a nested inventory, a list of ingredients that make up software components. [CISA](https://www.cisa.gov/sbom)

### Demo: How to use it?

This repo has a very simple JavaScript application that used Express to create a simple server that returns a "Hello World" message.

This project has some dependencies that are defined in the [package.json](package.json) and in the [package-lock.json](package-lock.json). The source code can be found in the [index.js](index.js) file.

The package.json contains some scripts that will help us to generate the SBOMs:
- `generate-sbom:cyclonedx` will generate the SBOM in the CycloneDX format.
- `generate-sbom:spdx` will generate the SBOM in the SPDX format.
- `generate-sbom` will generate the SBOM in the CycloneDX and SPDX formats.

The SBOMs will be generated in the `./sbom` folder:
- `./sbom/cyclonedx.json` is the SBOM in the CycloneDX format, [see](sbom/cyclonedx.json).
- `./sbom/spdx.spdx` is the SBOM in the SPDX format, [see](sbom/spdx.json).


Additionally, the project is equipped with a GitHub Action that verifies changes in dependencies and ensures the Software Bill of Materials (SBOMs) are up to date. You can find the GitHub Action defined in the [.github/workflows/ci.yml](.github/workflows/ci.yml) file. The validation process involves removing dynamic elements, such as timestamps and serial numbers, from the SBOMs and comparing the existing files with the new ones generated during the `npm run generate-sbom` execution.

**Test the results**

The most simple way to see this difference is by checking these PRs:
- Passing: [#3](https://github.com/UlisesGascon/poc-sbom-javascript/pull/3)
- Failing: [#2](https://github.com/UlisesGascon/poc-sbom-javascript/pull/2)

### Resources

- [npm-sbom documentation](https://docs.npmjs.com/cli/v10/commands/npm-sbom)
- [The Software Package Data Exchange (SPDX)](https://spdx.dev/)
- [CycloneDX](https://cyclonedx.org/)