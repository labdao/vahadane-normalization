# pathology-image-tiling-and-correction

## Running this app locally
Run the app locally with: `uvicorn tileImageAndCorrect:app --reload --host "0.0.0.0"`

## Building the container image

1. Clone this repository
1. Inside the directory for this repository, run:

    ```shell
    docker build -t vahadane_norm_and_tile .
    ```

## Running the container
Run the app in Docker via:

    docker run -d -p 8000:8000 vahadane_norm_and_tile:latest

and it should be running at http://localhost:8000 (or replace `localhost` with the IP/DNS name of whichever computer is running the container)

## Processing data with Postman

1. In Postman, craft a request with the following properties:

    | Postman parameter | Value |
    | --- | --- |
    | Request Type | `POST` |
    | Body Type | `form-data` |
    | key type (dropdown) | File |
    | key name (textbox) | `files` |
    | key value | (select an image) |
  
1. Press the "Send" button
1. The result should be a .zip file, so when the result is ready (it will look like random letters and numbers in the bottom half of the screen), press "Save Response" on the right side of the screen. Save the zip file.

## Processing data with bacalhau 
You can learn more about bacalhau in the [docs](https://docs.bacalhau.org/getting-started/installation).

the examples images have been pinned to IPFS using Pinata:
```
QmTr26AJDQMyxEJacL2ph7N71SAgRJaqj4USt4bMiE4Jff
QmX4kSU5W5Lnjjx9ZhBezonMdKQiy3zbJfkSLfUE4cTDMd
QmQr9LBQhmCUzRXkZZeN5nVZriavubLpBffFv5WkBFNUFU
```

Install bacalhau via: 
```
curl -sL https://get.bacalhau.org/install.sh | bash
```

To process the first of the example images using bacalhau, run: 
```
bacalhau docker run \                                         
  -v QmTr26AJDQMyxEJacL2ph7N71SAgRJaqj4USt4bMiE4Jff:/inputs/test.png \
  ghcr.io/openlab-apps/vahadane_norm_and_tile:main python main.py /inputs/test.png 
```

You can download the results by calling ``` bacalhau get ``` on the job id you have received.
