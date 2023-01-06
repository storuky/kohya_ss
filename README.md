# Kohya's dreambooth and finetuning

This repository now includes the solutions provided by Kohya_ss in a single location. I have combined both solutions under one repository to align with the new official Kohya repository where he will maintain his code from now on: https://github.com/kohya-ss/sd-scripts.

A note accompanying the release of his new repository can be found here: https://note.com/kohya_ss/n/nba4eceaa4594

## Installation

Open a regular Powershell terminal and type the following inside:

```powershell
git clone https://github.com/bmaltais/kohya_ss.git
cd kohya_ss

python -m venv --system-site-packages venv
.\venv\Scripts\activate

pip install torch==1.12.1+cu116 torchvision==0.13.1+cu116 --extra-index-url https://download.pytorch.org/whl/cu116
pip install --upgrade -r requirements.txt
pip install -U -I --no-deps https://github.com/C43H66N12O12S2/stable-diffusion-webui/releases/download/f/xformers-0.0.14.dev0-cp310-cp310-win_amd64.whl

cp .\bitsandbytes_windows\*.dll .\venv\Lib\site-packages\bitsandbytes\
cp .\bitsandbytes_windows\cextension.py .\venv\Lib\site-packages\bitsandbytes\cextension.py
cp .\bitsandbytes_windows\main.py .\venv\Lib\site-packages\bitsandbytes\cuda_setup\main.py

accelerate config

```

### Optional: CUDNN 8.6

This step is optional but can improve the learning speed for NVidia 4090 owners...

Due to the filesize I can't host the DLLs needed for CUDNN 8.6 on Github, I strongly advise you download them for a speed boost in sample generation (almost 50% on 4090) you can download them from here: https://b1.thefileditch.ch/mwxKTEtelILoIbMbruuM.zip

To install simply unzip the directory and place the cudnn_windows folder in the root of the kohya_diffusers_fine_tuning repo.

Run the following command to install:

```
python .\tools\cudann_1.8_install.py
```

## Upgrade

When a new release comes out you can upgrade your repo with the following command:

```powershell
cd kohya_ss
git pull
.\venv\Scripts\activate
pip install --upgrade -r requirements.txt
```

Once the commands have completed successfully you should be ready to use the new version.

## Launching the GUI

To run the GUI you simply use this command:

```
gui.cmd
```

## Dreambooth

You can find the dreambooth solution spercific [Dreambooth README](README_dreambooth.md)

## Finetune

You can find the finetune solution spercific [Finetune README](README_finetune.md)

## LoRA

You can create LoRA network by running the dedicated GUI with:

```
python lora_gui.py
```

or via the all in one GUI:

```
python kahya_gui.py
```

Once you have created the LoRA network you can generate images via auto1111 by installing the extension found here: https://github.com/kohya-ss/sd-webui-additional-networks

## Change history

* 2023/01/06 (v19.4):
    - Add new Utility to Extract a LoRA from a finetuned model
* 2023/01/06 (v19.3.1):
    - Emergency fix for dreambooth_ui no longer working, sorry
    - Add LoRA network merge too GUI. Run `pip install -U -r requirements.txt` after pulling this new release.
* 2023/01/05 (v19.3):
    - Add support for `--clip_skip` option
    - Add missing `detect_face_rotate.py` to tools folder
    - Add `gui.cmd` for easy start of GUI
* 2023/01/02 (v19.2) update:
    - Finetune, add xformers, 8bit adam, min bucket, max bucket, batch size and flip augmentation support for dataset preparation
    - Finetune, add "Dataset preparation" tab to group task specific options
* 2023/01/01 (v19.2) update:
    - add support for color and flip augmentation to "Dreambooth LoRA"
* 2023/01/01 (v19.1) update:
    - merge kohys_ss upstream code  updates
    - rework Dreambooth LoRA GUI
    - fix bug where LoRA network weights were not loaded to properly resume training
* 2022/12/30 (v19) update:
    - support for LoRA network training in kohya_gui.py.
* 2022/12/23 (v18.8) update:
    - Fix for conversion tool issue when the source was an sd1.x diffuser model
    - Other minor code and GUI fix
* 2022/12/22 (v18.7) update:
    - Merge dreambooth and finetune is a common GUI
    - General bug fixes and code improvements
* 2022/12/21 (v18.6.1) update:
    - fix issue with dataset balancing when the number of detected images in the folder is 0

* 2022/12/21 (v18.6) update:
    - add optional GUI authentication support via: `python fine_tune.py --username=<name> --password=<password>`