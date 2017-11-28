---
title: Instalar a CLI do Azure com o Docker
description: "Como instalar um contêiner do Docker com a CLI do Azure 2.0"
keywords: CLI do Azure, Instalar CLI do Azure, docker do azure, imagem do docker do azure,
author: sptramer
ms.author: sttramer
manager: routlaw
ms.date: 10/30/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: azurecli
ms.service: multiple
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: 76ecf2c9cd0e6e694a31ac160112d1348863f118
ms.sourcegitcommit: 905939cc44764b4d1cc79a9b36c0793f7055a686
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="install-azure-cli-20-with-docker"></a><span data-ttu-id="be64d-104">Instalar CLI do Azure 2.0 com o Docker</span><span class="sxs-lookup"><span data-stu-id="be64d-104">Install Azure CLI 2.0 with Docker</span></span>

<span data-ttu-id="be64d-105">Você pode usar o Docker para instalar um contêiner do Linux autônomo com a CLI do Azure 2.0 pré-instalada.</span><span class="sxs-lookup"><span data-stu-id="be64d-105">You can use Docker to install a standalone Linux container with the Azure CLI 2.0 pre-installed.</span></span> <span data-ttu-id="be64d-106">Permite que você inicie rapidamente com um ambiente no qual pode experimentar a CLI para decidir se é ideal para você ou permite que use isso como uma imagem de base.</span><span class="sxs-lookup"><span data-stu-id="be64d-106">This lets you get started quickly with an environment where you can try out the CLI to decide if it's right for you, or allows you to use this as a base image.</span></span>

## <a name="install-with-docker"></a><span data-ttu-id="be64d-107">Instalar com o Docker</span><span class="sxs-lookup"><span data-stu-id="be64d-107">Install with Docker</span></span>

<span data-ttu-id="be64d-108">Instalar a CLI usando `docker run`.</span><span class="sxs-lookup"><span data-stu-id="be64d-108">Install the CLI using `docker run`.</span></span>

   ```bash
   docker run -it azuresdk/azure-cli-python:<version>
   ```

<span data-ttu-id="be64d-109">Confira nossas [marcas do Docker](https://hub.docker.com/r/azuresdk/azure-cli-python/tags/) para versões disponíveis.</span><span class="sxs-lookup"><span data-stu-id="be64d-109">See our [Docker tags](https://hub.docker.com/r/azuresdk/azure-cli-python/tags/) for available versions.</span></span>

<span data-ttu-id="be64d-110">A CLI está instalada na imagem como o comando `az` no `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="be64d-110">The CLI is installed on the image as the `az` command in `/usr/local/bin`.</span></span>

> [!NOTE]
> <span data-ttu-id="be64d-111">Se você quiser acompanhar as chaves SSH do seu ambiente de usuário, use `-v ${HOME}:/root` para montar $HOME como `/root`.</span><span class="sxs-lookup"><span data-stu-id="be64d-111">If you want to pick up the SSH keys from your user environment, you can use `-v ${HOME}:/root` to mount $HOME as `/root`.</span></span>

> ```bash
> docker run -it -v ${HOME}:/root azuresdk/azure-cli-python:<version>
> ```

### <a name="update-with-docker"></a><span data-ttu-id="be64d-112">Atualizar com o Docker</span><span class="sxs-lookup"><span data-stu-id="be64d-112">Update with Docker</span></span>

<span data-ttu-id="be64d-113">Atualizar com o Docker requer obter a nova imagem e recriar qualquer contêiner existente.</span><span class="sxs-lookup"><span data-stu-id="be64d-113">Updating with Docker requires both pulling the new image and re-creating any existing containers.</span></span> <span data-ttu-id="be64d-114">Por esse motivo, você deve evitar o uso de um contêiner que hospeda a CLI como um armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="be64d-114">For this reason you should try and avoid using a container which hosts the CLI as a data store.</span></span>

1. <span data-ttu-id="be64d-115">Atualizar sua imagem local com `docker pull`.</span><span class="sxs-lookup"><span data-stu-id="be64d-115">Update your local image with `docker pull`.</span></span>

   ```bash
   docker pull azuresdk/azure-cli-python
   ```

2. <span data-ttu-id="be64d-116">Obter os contêineres atuais usando a imagem CLI.</span><span class="sxs-lookup"><span data-stu-id="be64d-116">Get the containers currently using the CLI image.</span></span>

   ```bash
   docker container ls -a --filter 'ancestor=azuresdk/azure-cli-python'
   ```

   ```output
   CONTAINER ID        IMAGE                              COMMAND             CREATED             STATUS                        PORTS               NAMES
   34a868beb2ab        azuresdk/azure-cli-python:latest      "/bin/sh -c bash"   8 minutes ago       Exited (0) 8 minutes ago                       inspiring_benz
   ```

  > [!NOTE]
  > <span data-ttu-id="be64d-117">Se você instalou uma versão específica da imagem, você precisará adicionar `:<version>` ao final do nome da imagem.</span><span class="sxs-lookup"><span data-stu-id="be64d-117">If you installed a specific version of the image, you will need to add `:<version>` to the end of the image name.</span></span>

3. <span data-ttu-id="be64d-118">Interromper e recriar os contêineres.</span><span class="sxs-lookup"><span data-stu-id="be64d-118">Halt and recreate the containers.</span></span>

   ```bash
   docker stop inspiring_benz
   docker rm inspiring_benz
   docker run azuresdk/azure-cli-python
   ```

### <a name="uninstall-with-docker"></a><span data-ttu-id="be64d-119">Desinstalar com o Docker</span><span class="sxs-lookup"><span data-stu-id="be64d-119">Uninstall with Docker</span></span>

<span data-ttu-id="be64d-120">Se você decidiu desinstalar a CLI do Azure, lamentamos sua saída.</span><span class="sxs-lookup"><span data-stu-id="be64d-120">If you ever decide to uninstall the Azure CLI, we're sorry to see you go.</span></span> <span data-ttu-id="be64d-121">Antes de desinstalar, use o comando `az feedback` para nos fornecer algumas razões por ter escolhido desinstalar e como poderíamos melhorar a experiência da CLI.</span><span class="sxs-lookup"><span data-stu-id="be64d-121">Before you uninstall, use the `az feedback` command to give us some reasons why you chose to uninstall and how we could improve the CLI experience.</span></span> <span data-ttu-id="be64d-122">Queremos assegurar que a CLI do Azure não tenha bugs e seja amigável o máximo possível.</span><span class="sxs-lookup"><span data-stu-id="be64d-122">We want to make sure that the Azure CLI is as bug-free and user-friendly as we can make it.</span></span> <span data-ttu-id="be64d-123">Você também pode [registrar um problema do github](https://github.com/Azure/azure-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="be64d-123">You can also [file a github issue](https://github.com/Azure/azure-cli/issues).</span></span>

<span data-ttu-id="be64d-124">Para desinstalar corretamente a imagem do Docker da CLI, precisará remover qualquer contêiner que o executa e excluir a imagem do local.</span><span class="sxs-lookup"><span data-stu-id="be64d-124">To properly uninstall the CLI Docker image you need to remove any containers running it, and then delete the local image.</span></span>

1. <span data-ttu-id="be64d-125">Obtenha os contêineres que executam a imagem azure-cli.</span><span class="sxs-lookup"><span data-stu-id="be64d-125">Get the containers running the azure-cli image.</span></span>

   ```bash
   docker container ls -a --filter 'ancestor=azuresdk/azure-cli-python'
   ```

   ```output
   CONTAINER ID        IMAGE                              COMMAND             CREATED             STATUS                        PORTS               NAMES
   34a868beb2ab        azuresdk/azure-cli-python:latest      "/bin/sh -c bash"   8 minutes ago       Exited (0) 8 minutes ago                       inspiring_benz
   ```
  > [!NOTE]
  > <span data-ttu-id="be64d-126">Se você instalou uma versão específica da imagem, você precisará adicionar `:<version>` ao final do nome da imagem.</span><span class="sxs-lookup"><span data-stu-id="be64d-126">If you installed a specific version of the image, you will need to add `:<version>` to the end of the image name.</span></span>

2. <span data-ttu-id="be64d-127">Exclua todos os contêineres com a imagem da CLI.</span><span class="sxs-lookup"><span data-stu-id="be64d-127">Delete any containers with the CLI image.</span></span>

   ```bash
   docker rm 34a868beb2ab
   ```

3. <span data-ttu-id="be64d-128">Remova a imagem da CLI instalada localmente.</span><span class="sxs-lookup"><span data-stu-id="be64d-128">Remove the locally installed CLI image.</span></span>

   ```bash
   docker rmi azuresdk/azure-cli-python
   ```
