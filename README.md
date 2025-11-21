# pyspark-tdd-scaffold
example project demonstrating test driven pyspark structured streaming development with local testing capability

we are using [deltalake medallion architecture](https://databricks.com/it/glossary/medallion-architecture) in this example, but the considerations and benefits apply more generally

### Landing Mechanism

this codebase assumes files arrive in a landing layer (s3 bucket), i.e. push based ingestion.

optionally we can modify this into a pull based ingestion design by changing the bronze layer logic to pull data (e.g. from a kafka topic)

## Dev Environment setup

We use a devcontainer to provide a baseline linux development runtime.

### Mac BootStrap

Here are some simple bootstrap instructions to get you started.

bash
```
brew install docker
brew install colima
colima start --cpu 4 --memory 8
```

After these, you should be able to build and start the devcontainer in vscode.

## Project Layout

each sub directory contains an `__init__.py`, which configures them as packages to facilitate importing and [test scope isolation](https://docs.pytest.org/en/7.1.x/how-to/fixtures.html)

`deltalake` contains the processing code
`tests` contains the tests

```
.
├── deltalake
│   ├── bronze
│   │   └── *.py
│   ├── silver
│   │   └── *.py
│   └── gold
│   │   └── *.py
├── tests
│   ├── bronze
│   │   └── *_test.py    
│   ├── silver 
│   │   └── *_test.py
│   ├── gold 
│       └── *_test.py          
└── integration    

```
## Considerations

### Unit Testing

*code should be modularised so that new functionality can be validated by `unit tests` in isolation*

- easy for someone unfamiliar with project/repo to start contributing indepedently
- easy to verify test cases against specification
- pytest `fixture` scopes should be set to `module`
  
### Integration Testing

*repo should be logically laid out so that pipeline can be validated end-to-end by `integration tests`*

- easy for reviewers to rule out any regression in functionality
- pytest `fixture` scopes should be set to `module`
  
  
## Package management

```
uv sync --extra dev
```

## Reference dataset

loosely basing off of the iFlix dataset here (just referencing the data shape)

https://www.kaggle.com/datasets/aungpyaeap/movie-streaming-datasets-iflix


## Run Tests

Run a single test
```
uv run pytest tests/bronze/play_test.py
```

Run all the tests
```
uv run pytest tests/
```

When these tests run, they will create a bunch of files under `./spark-warehouse` directory, the files are cleaned up after tests completion but you can modify the tests so that the artifacts remain if you are curious about the workings of the delta log and relevant parquet files.