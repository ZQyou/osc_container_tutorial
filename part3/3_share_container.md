# Share Your Container
A survey result from Nature, 2016 shows that most scientists can not reproduce
someone else's result (60-80%) and their own result (40-60%).

## Upload to OSC
```shell
$ scp -r samtools_1.9.sif USER@owesn.osc.edu:./
```

## Upload to Container Library
### Create a project
1. Go to https://cloud.sylabs.io/
2. Click __Share__ icon
3. Enter your project name, i.e. samtools
4. Select __Public__
5. Click __Next__ to initialize the project

### Push your image with Singularity client
```shell
$ singularity push samtools_1.7 library://USER/default/samtools:1.7
```

### Mange your projects

## Sign and Verify Containers
### Create your keys
```shell
$ singularity keys newpair
Enter your name (e.g., John Doe) : Zhi-Qiang You
Enter your email address (e.g., john.doe@example.com) : <your login email>
Enter optional comment (e.g., development keys) : osc
Generating Entity and OpenPGP Key Pair... Done
Enter encryption passphrase :
```
Use `list` sub-command to show all of the keys you have created or saved
locally.`
```shell
$ singularity keys list
Public key listing (/users/PZS0710/zyou/.singularity/sypgp/pgp-public):

0) U: Zhi-Qiang You (osc) <my login email>
   C: 2019-05-13 22:33:52 -0400 EDT
   F: 7C079E3B2F84042D4D418D025C8FC5FAF32D582B
   L: 4096
   --------
```
Use `push` to upload your key to the Keystore
```shell
$ singularity keys push <the finger print>
```

### Sign and verify your container
```shell
$ singularity sign samtools_1.7.sif
$ singularity verify samtools_1.7.sif
Verifying image: samtools_1.7.sif
Data integrity checked, authentic and signed by:
        Zhi-Qiang You (osc) <my login email>, KeyID 5C8FC5FAF32D582B

```
You can also verify this image without a local key.
```shell
$ rm  ~/.singularity/sypgp/*
$ singularity verify samtools_1.7.sif
INFO:    key missing, searching key server for KeyID: 5C8FC5FAF32D582B...
INFO:    key retrieved successfully!
Store new public key 7C079E3B2F84042D4D418D025C8FC5FAF32D582B? [Y/n] y
Data integrity checked, authentic and signed by:
        Zhi-Qiang You (osc) <my login email>, KeyID 5C8FC5FAF32D582B
```
