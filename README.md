# librechat_test

This is a test repository for LibreChat, with the purpose to test it and try out its Agent functionalities. The Repo is organizred as followed:
* The project index points to all files we want to put into version control, here we change files
* LibreChat is added as a submodule. The Submodule points to the productive state of LibreChat. Dont update the submodule!

We will edit files in the project root and move them into the LibreChat folder.

# Running LibreChat

1. Clone the Repository with `git clone git@github.com:gebauerm/librechat_test.git --recurse submodules`. This will also load the LibreChat Repository as a [submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules) into `./LibreChat`. We will keep configuration files in the parent repository.
2. Change into the LibreChat Folder. Create the following folders:
    * Meili_data_v1.12
    * data-node
    * images
    * uploads
    * logs
3. Create an _.env_ file from _.env.example_ and uncomment the liness 68 and 69, to:

            UID=1000
            GID=1000

4. Start LibreChat by typing `docker compose up`. This will start serveral containers, with Docker Compose. Docker Compose is a light orchestration tool for containers. LibreChat is a collection of multiple containers communicating with each other. In case you have issues with the configuration and run into errors, you can test your configurations faster by restarting the LibreChat Container. This can be done by `docker container restart LibreChat`



# Add a LLM Provider to LibreChat

## Mistral

1. Create a copy of the file `./LibreChat/.env.example` and plance the copy at `./LibreChat/.env`

2. We will provide you with an API Key. Take this key and paste it into the newly created .env file under `MISTRAL_API_KEY=<key>`
Move the following files into the LibreChat folder:
* librechat.yaml
* docker-compose.override.yml

Otherwise head to the [documentation](https://www.librechat.ai/docs/configuration/librechat_yaml/ai_endpoints/mistral)

## Azure OpenAI


