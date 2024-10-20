# Stable Diffusion on Mac M1

- Update dotfiles to add python@2.10 and virtualenv

## Trying things out

- `--seed $RANDOM`
- `--from-file`: prompts from a file (one per line?)
- `--skip_grid`: outputs ony in `outputs/txt2img-samples/samples/`
- `--f`: downsampling factor
- [x] `--n_samples` : number of images in a batch, doesn't work well, might as well loop
- [x] `--ddim_steps` : 50 default, not sure, 50 timesteps? 60 does not work
- [x] `--W` and `--H` : even 768 squared seems too much

```bash
cd stable-diffusion
source venv/bin/activate
time python scripts/txt2img.py --from-file ../prompts/prompt-1.txt --skip_grid --n_samples 1 --n_iter 1 --plms --seed $RANDOM
mv outputs/txt2img-samples/samples "../output/samples-$(date +samples-%Y-%m-%dT%H.%M.%S)"
```

### Tone down warning

```python
# Add this to txt2img.py
#-------------------
# Tone down "Some weights of the model checkpoint ..."
from transformers import logging
# logging.set_verbosity_warning()
logging.set_verbosity_error()
#-------------------
```

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

- [Repo](https://github.com/bfirsh/stable-diffusion.git)
- [Stable Diffusion on M1](https://replicate.com/blog/run-stable-diffusion-on-m1-mac)
- [imaginAIry](https://github.com/brycedrennan/imaginAIry)
