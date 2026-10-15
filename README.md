# BeKampus

BeKampus is a web platform for discovering events and communities connected to the National University of Colombia (UNAL), Bogotá campus.

It brings student, academic, cultural, and sports activities into one place. Visitors can browse public events without an account; authentication and appropriate permissions are required for actions such as registering for an event or managing an organization.

## Project status

The initial scope focuses on UNAL Bogotá. Events may have different eligibility rules, including events open to the public. A verified organizer is not necessarily an organization or event officially endorsed by the University.

## Documentation

- [Product definition](docs/PRODUCT.md): users, scope, product rules, and MVP boundaries.
- [Requirements](docs/REQUIREMENTS.md): functional requirements and quality constraints.
- [Architecture](docs/ARCHITECTURE.md): current technical principles and domain boundaries.

## Local development

Use the scripts and setup instructions in the root `package.json` and the relevant application or package manifests. Keep these instructions aligned with the actual Turborepo setup; do not document commands that have not been verified.

## Working principles

1. Track implementation work in GitHub Issues and GitHub Projects, not in a duplicate Markdown task list.
2. Link changes to Issues with clear acceptance criteria.
3. Enforce authorization on the server and, where appropriate, at the data layer.
4. Update documentation in the same pull request when product behavior or a technical decision changes.
5. Close work only after its acceptance criteria and relevant checks pass.
