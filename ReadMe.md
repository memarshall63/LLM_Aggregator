# LLM API Aggregator

This project is an API that aggregates responses from multiple Language Model (LLM) providers, including OpenAI, Anthropic, and Google.

## Features

- Concurrent requests to multiple LLM APIs
- Rate limiting for each LLM provider
- Google Cloud Storage integration for storing responses
- FastAPI-based RESTful API
- Swagger documentation
- Dockerized application

## Setup

1. Clone the repository:
   ```
   git clone https://github.com/yourusername/llm-api-aggregator.git
   cd llm-api-aggregator
   ```

2. Create a `config.ini` file in the root directory with the following content:
   ```ini
   [API_KEYS]
   OPENAI_API_KEY = your_openai_api_key
   ANTHROPIC_API_KEY = your_anthropic_api_key
   GOOGLE_API_KEY = your_google_api_key

   [STORAGE]
   GCS_BUCKET_NAME = your_gcs_bucket_name
   GCS_SERVICE_ACCOUNT_KEY = path/to/your/service_account_key.json

   [LLM]
   TIMEOUT = 30
   MAX_RETRIES = 3

   [RATE_LIMIT]
   CALLS = 10
   PERIOD = 60
   ```

   Note: If you're using Application Default Credentials, you can omit the `GCS_SERVICE_ACCOUNT_KEY` setting.

3. Set up Google Cloud Storage:
   - Create a Google Cloud project if you haven't already
   - Enable the Google Cloud Storage API
   - If not using Application Default Credentials, create a service account and download the JSON key file

4. Build the Docker image:
   ```
   docker build -t llm-api-aggregator .
   ```

5. Run the Docker container:
   ```
   docker run -p 8000:8000 llm-api-aggregator
   ```

6. Access the API at `http://localhost:8000` and the Swagger documentation at `http://localhost:8000/docs`

## Usage

Send a POST request to `/api/v1/process` with a JSON body:

```json
{
  "prompt": "Your prompt here"
}
```

The API will return responses from all LLM providers and the blob name where the response is stored in Google Cloud Storage.

## Running Tests

To run the tests, use the following command:

```
pytest
```

## Contributing

Please read CONTRIBUTING.md for details on our code of conduct, and the process for submitting pull requests.

## License

This project is licensed under the MIT License - see the LICENSE.md file for details.
