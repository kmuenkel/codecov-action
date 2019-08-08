<!-- <p align="center"><img  src="./codecov-logo.png"  /></p> -->

# Codecov GitHub Action
### Easily upload coverage reports to Codecov from GitHub Actions 

## Usage

Inside your `.github/workflows/workflow.yml` file:

```yaml
steps:
- uses: actions/checkout@master
- uses: actions/codecov-action@v1
  with:
    token: ${{secrets.CODECOV_TOKEN}} #for private repos
    file: ./coverage.xml #optional
    flags: unittests #optional
    name: codecov-1 #optional
```
>**Note**: This assumes that you've set your Codecov token inside settings > secrets as `CODECOV_TOKEN`. If not, you can get an upload token for your specific repo on codecov.io. A token is *not* required for public repositories. 

### Example `workflow.yml` with Codecov Action

```yaml
name: Example workflow for Codecov
on: [push]
jobs:
  run:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
   
    - name: Setup Python  
      uses: actions/setup-python@master
      with:
        version: 3.7

    - name: Generate coverage report
      run: |
        pip install pytest
        pip install pytest-cov
        pytest --cov=./ --cov-report=xml

    - name: Upload coverage to Codecov  
      uses: codecov/codecov-action@v1
      with:
        token: ${{secrets.CODECOV_TOKEN}}
        file: ./coverage.xml
        flags: unittests
        name: codecov-1 
```

## Arguments

| Input  | Description |
| :---:     |     :---:   | 
| `token`  | Used to authorize coverage report uploads  |
| `file`  | Location of the coverage report |
| `flags`  | Flag upload under a certain group name |
| `name`  | Custom defined name for the upload |


## License 

The code in this project is released under the [MIT License](LICENSE)
