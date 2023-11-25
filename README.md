# YOLOv8  with SEGMONTO

Example notebook for using the Ultralytics API (YOLOv8) and YALTAi for image-based object prediction from segmonto segmentation.

Here's an example of a bash script used on the Geneva HPC servers:

```
#!/bin/env bash

#SBATCH --partition=shared-gpu
#SBATCH --time=09:00:00
#SBATCH --output=journal-%j.out
#SBATCH --mem=25000
#SBATCH --gres=gpu:3,VramPerGpu:24GB
#SBATCH --cpus-per-task=12
module load cuDNN/8.6.0.163-CUDA-11.8.0 GCCcore/10.3.0 Python/3.9.5 OpenSSL/1.1.1q

source ~/gallicorpora_yolov8/.env/bin/activate

#srun python3.9 -m venv ~/gallicorpora_yolov8/venv

echo "Creation virtualenv"

#source ~/gallicorpora_yolov8/venv/bin/activate
#/home/users/h/humeau/gallicorpora_yolov8/venv/bin/python3.9 -m pip install --upgrade pip

#mkdir $HOME/gallicorpora_yolov8/tmp

#TMPDIR=$HOME/gallicorpora_yolov8/tmp pip install -U ultralytics comet-ml

echo "Installation finished"

echo "I: CUDA_VISIBLE_DEVICES: ${CUDA_VISIBLE_DEVICES}"

echo "====="

srun nvidia-smi

echo "====="


echo "Yolov8 training"
srun python3  ~/gallicorpora_yolov8/run_yolov.py
echo "Training finish !"

deactivate
#rm -fr ~/gallicorpora_yolov8/venv
#rm -fr $HOME/gallicorpora_yolov8/tmp
echo "clean uninstall"
#rm -fr $HOME/gallicorpora_yolov8/tmp
echo "clean uninstall"  
```

-------

*The computations were performed at University of Geneva using Baobab HPC service.*



