# Stable Difusion on Mac M1

- Update dotfiles to addd python@2.10 and virtualenv

## Trying things out

 - `--seed $RANDOM`
 - `--n_samples` : number of images in a batch
 - `--ddim_steps` : 50 default, not sure, 50 timesteps?
## Setup

```bash

git clone -b apple-silicon-mps-support https://github.com/bfirsh/stable-diffusion.git
cd stable-diffusion
mkdir -p models/ldm/stable-diffusion-v1/

virtualenv venv
# app_data_dir=/Users/daniel/Library/Application Support/virtualenv)

source venv/bin/activate

pip install -r requirements.txt

brew install Cmake protobuf rust

mv ~/Downloads/sd-v1-4.ckpt models/ldm/stable-diffusion-v1/model.ckpt

python scripts/txt2img.py \
  --prompt "a red juicy apple floating in outer space, like a planet" \
  --n_samples 1 --n_iter 1 --plms

# Your output's in outputs/txt2img-samples/. That's it.
```

## References

- [Stable Diffusion on M1](https://replicate.com/blog/run-stable-diffusion-on-m1-mac)