# librechat_test

This is a test repository for LibreChat, with the purpose to test it and try out its Agent functionalities. The Repo is organizred as followed:
* The project index points to all files we want to put into version control, here we change files
* LibreChat is added as a submodule. The Submodule points to the productive state of LibreChat. Dont update the submodule! In this folder we start LibreChat

We will edit files in the project root and move them into the LibreChat folder.

# Track Guide

## Running LibreChat

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



## Add a LLM Provider to LibreChat

### Mistral

1. Create a copy of the file `./LibreChat/.env.example` and plance the copy at `./LibreChat/.env`

2. We will provide you with an API Key. Take this key and paste it into the newly created _.env_ file under `MISTRAL_API_KEY=<key>`.
Move the following files into the LibreChat folder:
* librechat.yaml
* docker-compose.override.yml

Otherwise head to the [documentation](https://www.librechat.ai/docs/configuration/librechat_yaml/ai_endpoints/mistral)

3. Select a Mistral Model from the top left.
![model](./doc/model_selection.png)


## Azure OpenAI


## Add an MCP Server

### Example with archivX

In this example we will connect an archivX MCP Server to LibreChat.
Wit this MCP Server we will be able to download and search papers on ArchivX.
We will use [Smithery](https://smithery.ai/) to find a suiting mcp server.

[Smithery](https://smithery.ai/) provides a lot of MCP Servers that can be started, right with LibreChat. We will use [Academa](https://smithery.ai/server/@IlyaGusev/academia_mcp) from smithery. Smithery offers direct integration with LibreChat.

__I recommend to use the json representation and put it under the mcpServer Section in LibreChat__

To achieve this do the following:

1. Go tp the Json Section of [academia](https://smithery.ai/server/@IlyaGusev/academia_mcp). The contents of the json is what you need.

![smithery_academia](./doc/smithery.png)

2. Open `librechat.yaml` and add the following lines __under__ _mcpServers_. Mind the yaml structre.

          mcpServers:
            academia_mcp:
                command: npx
                args:
                - -y
                - "@smithery/cli@latest"
                - run
                - "@IlyaGusev/academia_mcp"
                - --key
                - <key from Smithery>

The key you need is written in the json-format within smithery. Paste in the correct key.
If you paid attention you will see that the content matches the one written in the json at [academia](https://smithery.ai/server/@IlyaGusev/academia_mcp).

3. Restart LibreChat with `docker container restart LibreChat`
4. Open LibreChat and go to _"MCP Server"_
![mcp](./doc/mcp.png). There click on "academia_mcp".
5. Search for a the paper "Attention is all you need" and ask to download it. A Link should appear that should direct you to a pdf.


### Browse more MCP Server

No you are set to experiment.
Add more MCP Servers by using the json configurations.
Explore [Smithery](https://smithery.ai/).
