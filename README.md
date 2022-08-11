# run-terraform-test-suite
Github action for running Go tests on AWS Terraform fixtures

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| go-version | the version of Go used for the provided test suites | `string` | n/a | yes |
| terraform-version | the version of Terraform used for the provided fixtures | `string` | n/a | yes |
| fixtures-directory | path to the fixtures to run the test suites against | `string` | n/a | yes |
| test-files-directory | path to the test suites to run against the fixtures | `string` | n/a | yes |
| aws-access-key-id | your AWS Access Key ID for the fixtures | `string` | n/a | yes |
| aws-secret-access-key | your AWS Secret Access Key for the fixtures | `string` | n/a | yes |

## Usage

```
  Tests:
    name: Test Fixtures
    runs-on: "ubuntu-latest"
    steps:
      - name: Run tests
        uses: synapsestudios/run-terraform-test-suite@main
        with:
          go-version: 1.18.3
          terraform-version: 1.2.2
          fixtures-directory: "fixtures/terraform-aws-bastion-server"
          test-files-directory: "test"
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

### Run a test directory against a set of fixture directories

```
  Tests:
    name: Test Fixtures
    runs-on: "ubuntu-latest"
    strategy:
        matrix:
            param: [ 'fixtures/terraform-aws-bastion-server', 'fixtures/terraform-aws-bastion-server-2]
    steps:
      - name: Run tests
        uses: synapsestudios/run-terraform-test-suite@main
        with:
          go-version: 1.18.3
          terraform-version: 1.2.2
          fixtures-directory: ${{ matrix.param }}
          test-files-directory: "test"
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

### Run a set of test directories against a fixture directory

```
  Tests:
    name: Test Fixtures
    runs-on: "ubuntu-latest"
    strategy:
        matrix:
            param: [ 'tests/test-suite-1', 'tests/test-suite-2]
    steps:
      - name: Run tests
        uses: synapsestudios/run-terraform-test-suite@main
        with:
          go-version: 1.18.3
          terraform-version: 1.2.2
          fixtures-directory: "fixtures/terraform-aws-bastion-server"
          test-files-directory: ${{ matrix.param }}
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

### Run array of test directories against a set of fixture directories

```
  Tests:
    name: Test Fixtures
    runs-on: "ubuntu-latest"
    strategy:
        matrix:
            fixtures: [ 'fixtures/terraform-aws-bastion-server', 'fixtures/terraform-aws-bastion-server-2],
            tests: [ 'tests/test-suite-1', 'tests/test-suite-2' ]
    steps:
      - name: Run tests
        uses: synapsestudios/run-terraform-test-suite@main
        with:
          go-version: 1.18.3
          terraform-version: 1.2.2
          fixtures-directory: ${{ matrix.fixtures }}
          test-files-directory: $${{ matrix.tests }}
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```