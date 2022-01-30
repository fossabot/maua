# Maua
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fmaua-maua-maua%2Fmaua.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Fmaua-maua-maua%2Fmaua?ref=badge_shield)


## 👷 ⛏️ WIP 🛠️ 👷

Maua is a Python library (and command line interface) for synthesizing images, video, and audio using deep learning.

While many research groups publish code to reproduce results of their papers, it is often still time intensive to set up the environment correctly and figure out how to run the algorithms on your own data. The goal of Maua is to collect these methods in one place to make it easy to use them as creative tools. The primary design goal is composability. Combining different methods in unique ways exponentially expands the space of possible results--and so the creative freedom.

Maua is still under construction for now and so the API and functionality are subject to change.

## Installation

Deep learning is very compute hungry, this means that a decent GPU is practically a requirement. If you have an NVIDIA GPU with the driver installed: set up [Miniconda](https://docs.conda.io/en/latest/miniconda.html) on your machine and run the commands below.

```bash
git clone --recursive https://github.com/maua-maua-maua/maua.git
cd maua
conda create -n maua python=3.8 pytorch torchvision torchaudio cudatoolkit=11.3 cudatoolkit-dev=11.3 cudnn mpi4py Cython pip=21.3.1 -c nvidia -c pytorch -c conda-forge
conda activate maua
pip install -r requirements.txt
```

Currently installation has only been tested on a Ubuntu 20.04 machine with NVIDIA GPUs. Other configurations are also be possible but might be more involved. If you're running into problems, feel free to open an issue!

## Usage

### Command line

Use --help to find the options available
```bash
python -m maua --help
python -m maua dalle --help
python -m maua diffusion v --help
```

#### Examples

Generate images with classifier-free guided diffusion:
```bash
python -m maua diffusion cfg "A street art mural of a dapper turtle with wings"
```

Generate images by finetuning RuDALL-E on a set of images:
```bash
python -m maua dalle ru finetune --input_dir /path/to/directory/of/images/
```

Upscale images using RealESRGAN:
```bash
python -m maua super image upscale /path/to/image.png /path/to/image2.png /path/to/image3.png --model_name RealESRGAN-pbaylies-hr-paintings
```

### Python

All of the command line functions are also available for import within python.

#### Examples

High resolution diffusion:
```python
from maua.diffusion.guided import guided_diffusion as diffusion
# or 
# from maua.diffusion.cfg import classifier_free as diffusion
# or 
# from maua.diffusion.v import v_diffusion as diffusion
from maua.super.image import upscale

images = [diffusion("A street art mural of a dapper turtle with wings") for i in range(5)]

for pil_image in upscale(images, model_name='latent-diffusion'):
    pil_image.save(f"output/{i}.png")
```

## Thanks

Thank you to everyone that makes their work available to the community. Maua incorporates open source code from all of the internet, without the work of these amazing people this wouldn't be possible. Below is a (probably very) incomplete list of people whose code has directly or indirectly contributed to Maua:

@crowsonkb, @ProGamerGov, @lucidrains, @dvschultz, @eps696, @l4rz, @caillonantoine, @ben-hayes, @adrienchaton, @sportsracer48, @afiaka87, @aydao, @rosinality, @genekogan, @dribnet, @alexjc, @htoyryla, @neverix, @sniklaus, @xinntao, @cszn, @JingyunLiang, @kentsyx, @kakaobrain, @yu45020, @twitter@advadnoun, @twitter@danielrussruss, @twitter@ai_curio

## Citations

Maua relies on many innovations coming directly from the research community. It's safe to say that if you use Maua in any way for research related purposes you should be citing some papers. For now, please do a quick web-search based on the file path (these are generally named after the method). A full list of papers to cite will be compiled and documented clearly in the future.

## License

The main license for this repository is GPL-v3. However, due to the wide variety of sources of code, different components might fall under different licenses. Efforts are still underway to ensure all parts of the Maua library are licensed and attributed correctly. If there are any issues with licensing please make an issue and they will be rectified ASAP!

The code is provided free of charge for the purpose of enabling people to make art and explore deep learning synthesis. Due to the aformentioned licensing, commercial use of Maua may be tricky. You will need to make sure that you are adhering to the licensing terms of all the submodules!

In general, output does not fall under the license of the code. Copyrights of model weights and model outputs are still a major gray area so use these commercially at your own risk! As a rule of thumb, try to consider if what you are making really is transformative. If you've simply scraped someone's social media page and trained a model to mimic them, you need to give them credit and should not use the model or outputs commercially without discussing with them.


[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fmaua-maua-maua%2Fmaua.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Fmaua-maua-maua%2Fmaua?ref=badge_large)