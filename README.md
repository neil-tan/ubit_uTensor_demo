# Background Reading
[Simple Neural Network on MCU](https://blog.hackster.io/simple-neural-network-on-mcus-a7cbd3dc108c)

[An End-to-End Tutorial Running Convolution Neural Network on MCU with uTensor](https://towardsdatascience.com/simple-cnn-on-mcu-with-utensor-372265ecc5b4)


# Set up
We typically use MacOS for development. You will need to install utensor-cli (aka. the code generator) and mbed-cli.

For utensor-cli, I recommend doing the following:
- use pyenv to manage your python versions
- use pipenv `pipenv install -d --skip-lock` to install utensor-cli
- switch utensor-cli to the correct branch, see the section below.

# Code Generation
Using the code-generator [ubit branch](https://github.com/uTensor/utensor_cgen/tree/ubit)
```
utensor-cli convert mnist_for_mc.pb --transform-methods='dropout|>linear_reoder|>quantize|>conv_pool|>FakeGatherV2|>inline|>biasAdd|>remove_id_op|>refcnt' --output-nodes mul_6
```


# Build Instruction
```
mbed import https://github.com/neil-tan/ubit_uTensor_demo
cd ubit_uTensor_demo
# connect your board
mbed compile -m auto -t GCC_ARM --profile=uTensor/build_profile/release.json -f
```

# TODO
- Patch the main.cpp to use the correct dimensions and tensor-names
- Verify the output
- Switch to uBit toolchain, Yotta