# RFdiffusionRC

This repo provides usage instructions for setting up [RFdiffusion](https://www.bakerlab.org/members/) on [Penn State's Roar Collab (RC) HPC system](https://www.icds.psu.edu/access-roar-and-roar-collab-online/).



### Installation
1. under $PWD, make two dirs: env and model. Under env, mkdir SE3nv.
2. under the same dir as env and model, do `git clone https://github.com/RosettaCommons/RFdiffusion.git`
3. `cd models` and then do  
```
wget http://files.ipd.uw.edu/pub/RFdiffusion/6f5902ac237024bdd0c176cb93063dc4/Base_ckpt.pt
wget http://files.ipd.uw.edu/pub/RFdiffusion/e29311f6f1bf1af907f9ef9f44b8328b/Complex_base_ckpt.pt
wget http://files.ipd.uw.edu/pub/RFdiffusion/60f09a193fb5e5ccdc4980417708dbab/Complex_Fold_base_ckpt.pt
wget http://files.ipd.uw.edu/pub/RFdiffusion/74f51cfb8b440f50d70878e05361d8f0/InpaintSeq_ckpt.pt
wget http://files.ipd.uw.edu/pub/RFdiffusion/76d00716416567174cdb7ca96e208296/InpaintSeq_Fold_ckpt.pt
wget http://files.ipd.uw.edu/pub/RFdiffusion/5532d2e1f3a4738decd58b19d633b3c3/ActiveSite_ckpt.pt
wget http://files.ipd.uw.edu/pub/RFdiffusion/12fc204edeae5b57713c5ad7dcb97d39/Base_epoch8_ckpt.pt
```
4. `module load anaconda3/2021.05`
5. `cd ../env/SE3nv` and `conda create --prefix $PWD` to install a local conda env
6. activate the installed conda env by `source activate /storage/group/RISE/toShare/RFdiffusion/env/SE3nv`
7. install pip locally by `conda install pip`
8. install dependencies for SE3Transformer using pip `pip install jedi omegaconf hydra-core icecream pyrsistent `
9. install dgl for SE3Transformer using pip `pip install dgl==1.0.2+cu116 -f https://data.dgl.ai/wheels/cu116/repo.html`
10. install SE3Transformer by going into `RFdiffusion/env/SE3Transformer` dir, `cd ../../RFdiffusion/env/SE3Transformer/` and then `pip -q install .`
11. install additional dependencies for RFdiffusion: `pip install torch opt_einsum e3nn`
12. Go to  the root dir of `RFdiffusion` repo using `cd ../../` and then `pip install .` to install RFdiffusion



### Testing

1. To make sure it's working, asking for a GPU or a CPU session by on RC
2. For some reason, the models should be in a specific directory: `cp -r /storage/group/RISE/toShare/RFdiffusion/models /storage/group/RISE/toShare/RFdiffusion/env/SE3nv/lib/python3.11/site-packages/rfdiffusion/inference/../../models`
3. Also, the input pdbs should be in a similar place `cd /storage/group/RISE/toShare/RFdiffusion/env/SE3nv/lib/python3.11/site-packages/rfdiffusion/inference/../../` and `mkdir examples`
4.  `cd examples` and `cp -r /storage/group/RISE/toShare/RFdiffusion/RFdiffusion/examples/input_pdbs .`
5. go to `RFdiffusion/scripts` and run `./run_inference.py 'contigmap.contigs=[150-150]' inference.output_prefix=test_outputs/test inference.num_designs=10`


Links: 

[RFdiffusion github](https://github.com/RosettaCommons/RFdiffusion#getting-started--installation)

[RFdiffusion google colab notebook](https://colab.research.google.com/github/sokrypton/ColabDesign/blob/v1.1.1/rf/examples/diffusion.ipynb)
