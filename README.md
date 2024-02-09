# K6 Repository

This repository houses performance testing scripts using [k6](https://k6.io/) for various APIs. The project adopts a well-organized directory structure to ensure a clear and modular codebase.

## Directory Structure

```plaintext
|-- K6
    |-- config
    |   |-- checks.js
    |   |-- scenarios.js
    |-- data
    |   |-- environments.json
    |-- helpers
    |   |-- dataManager.js
    |   |-- dateUtils.js
    |   |-- randomData.js
    |-- reports
        |-- summary-dashboard.html
    |-- requests
    |   |-- <application>.js
    |-- tests
    |   |-- <application>.js
```

## Usage

1. **Configuration Files (`config/`):**
   - `scenarios.js`: Configures scenarios and thresholds, which can be called on CLI environment options.
   - `checks.js`: Sets custom checks for the tests.

2. **Data Files (`data/`):**
   - `environments.json`: JSON file containing environment data.

3. **Helper Scripts (`helpers/`):**
   - `randomData.js`: Contains helper functions for generating random data.
   - `dateUtils.js`: Contains helper functions for generating dates data.
   - `dataManager.js`: Includes data management functions for .jsons in data folder.

4. **Reports folder (`reports/`):**
   - `summary-dashboard.html`: A standard report generated on test runs.

5. **Request Scripts (`requests/`):**
   - `<application>.js`: JS file containing requests and assertions for the requests of the API.

6. **Test Scripts (`tests/`):**
   - `<application>.js`: Scripts for performance testing.

   Customize or add test scripts based on your testing requirements.

## How to run a script?
Through the CLI, there're options that must be passed as parameter when running a script, e.g.:

```
k6 run -e SCENARIO=<scenario> -e THRESHOLD=<threshold> -e ENVIRONMENT=<environment> <testName.js>
```

You should select the scenario (if not, 1 VU will execute 1 loop), threshold *(optional)* and environment which the test will use.

If Elastic Search is configured to receive the data of the tests run this command:

```
k6-elastic run -e SCENARIO=<scenario> -e THRESHOLD=<threshold> -e ENVIRONMENT=<environment> <testName.js> -o output-elasticsearch 
```

If you want to generate localdashboard and see it in real time run this command:

```
k6-dashboard run -e SCENARIO=<scenario> -e THRESHOLD=<threshold> -e ENVIRONMENT=<environment> -o "dashboard=open&report=<report_path>/summary-dashboard.html" <testName.js>
```

**Scenarios and thresholds* are setted up at config/scenarios.js.

**Environment* settings are setted up at data/environments.json.

## How to run a script in docker?
This repo contains 2 files to configure Docker.
1. **Dockerfile**: xk6 instalation in a docker container.
2. **Docker-compose**: All configuration for create Kibana, Elastic, Grafana and K6.
3. **.env**: File with variables for the docker-compose.

First at all, you must have docker in your local. Then build the docker-compose with:
```
docker-compose up -d
```
Wait 2 min and now you have Elastic with Kibana and Grafana Dashboard.
Now you can launch k6 with this command:
```
docker-compose run --rm k6 run /home/k6/tests/<application>.js
```
This comand run a K6 test with the output-elasticsearch setted in the docker-compose. 

## Links
[Official Documentation](https://k6.io/docs/)  
[K6 Libraries](https://jslib.k6.io/)  
[Executors](https://k6.io/docs/using-k6/scenarios/executors/)  
[Thresholds/Metrics(built-in)](https://k6.io/docs/using-k6/metrics/reference/)  
[Checks/Assertions](https://k6.io/docs/using-k6/checks/)  
[How to: environment variables](https://k6.io/docs/using-k6/environment-variables/)  
[K6 chaiJS](https://k6.io/docs/javascript-api/jslib/k6chaijs/)  
[Elasticsearch report configuration](https://k6.io/docs/results-output/real-time/elasticsearch/)  
[Elastic Output: xk6-output-elasticsearch](https://github.com/elastic/xk6-output-elasticsearch)  
[Local Dashboard: xk6-dashboard](https://github.com/grafana/xk6-dashboard)  
[Best practices](https://k6.io/docs/using-k6-browser/recommended-practices/)