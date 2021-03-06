# FoldingAtHomeContainer

This container will run the Folding@Home client in a Docker container, on a GPU.

To run this container on your Nvidia GPU you will need the [NVIDIA Container
Toolkit](https://github.com/NVIDIA/nvidia-docker) installed alongside your
Docker engine.

## Scope

My goal for this project is to make it as easily as possible for users to run
Folding@Home on a GPU. My initial effort will be focused on making this simple
to run on Amazon ECS. However, this container should run equally well on any
conatainer platform, provided there is a GPU available. It will still run
without a GPU just fine, but you will see warnings if you do not remove the GPU
slot from the config.xml.

Secondly, this container should be as simple and obvious as possible. As of now
this means a barely configured FAHClient and NVIDIA GPUs only. There is no
support for teams, passkeys, or any other inputs really.

## Non-Goals

I am not working making this container infinitely customizable. If you want to
customize the container to add passkeys or teams, or any other support; feel
free to fork or launch a new container _FROM raykrueger/folding-at-home_ in
your own Dockerfile, and copying in your own config.xml.

Windows and Mac are not supported. Mainly because Mac and Windows do not have
GPU support for linux containers.

## Testing Locally (on Linux)

Once you've installed the NVIDIA Docker Tool kit, you can run this locally.

    docker run --gpus=all --rm -it raykrueger/folding-at-home

To build and test local...

    git clone https://github.com/raykrueger/FoldingAtHomeContainer.git
    cd FoldingAtHomeContainer
    docker build -t folding-at-home
    docker run --gpus=all --rm -it folding-at-home

## Running on Amazon ECS

To run this container on Amazon ECS I've built a CDK app that you can
download here
[https://github.com/raykrueger/FoldingOnECS](https://github.com/raykrueger/FoldingOnECS).
