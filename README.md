# nnDetection finetuning — The Missing Piece

Code and pretrained checkpoints for our paper:

> **The Missing Piece: A Case for Pre-Training in 3D Medical Object Detection**
> Katharina Eckstein, Constantin Ulrich, Michael Baumgartner, Jessica Kächele,
> Dimitrios Bounias, Tassilo Wald, Ralf Floca, Klaus H. Maier-Hein
> MICCAI 2025 · [doi:10.1007/978-3-032-04965-0_58](https://doi.org/10.1007/978-3-032-04965-0_58)
> · [arXiv:2509.15947](https://arxiv.org/abs/2509.15947)

## Where the code lives

This repository is a placeholder. The finetuning code is **not** kept here —
it has been integrated into nnDetection itself, on its own branch:

👉 **https://github.com/MIC-DKFZ/nnDetection/tree/finetuning**

Start with [`docs/finetuning.md`](https://github.com/MIC-DKFZ/nnDetection/blob/finetuning/docs/finetuning.md)
on that branch: it covers the supported backbone/detector combinations, the
CLI flags for loading pretrained weights, and a worked example command per
checkpoint.

It adds, on top of the standard nnDetection workflow:

- **ResEnc** (nnU-Net residual encoder) and **Primus** (ViT)
  backbones for Retina U-Net and Deformable DETR
- loading pretrained encoders from a checkpoint's `nnssl_adaptation_plan`,
  including architecture reconciliation (`--transfer_learning`,
  `--load_adapt_plan`)
- support for MultiTalent-style checkpoints with multiple per-dataset stems
- two-phase (freeze/unfreeze) warmup finetuning

## Pretrained checkpoints

All six backbones from the paper are on the Hugging Face Hub, collected in
[The Missing Piece: Pre-trained nnDetection Backbones](https://huggingface.co/collections/MIC-DKFZ/the-missing-piece-pre-trained-nndetection-backbones-6ab62e4d50b7219ef37d1d50):

| Checkpoint | Pretraining | Backbone |
|---|---|---|
| [`ResEncL-MissingPiece-MAE`](https://huggingface.co/MIC-DKFZ/ResEncL-MissingPiece-MAE) | Masked Autoencoder | ResEnc |
| [`ResEncL-MissingPiece-MG`](https://huggingface.co/MIC-DKFZ/ResEncL-MissingPiece-MG) | Models Genesis | ResEnc |
| [`ResEncL-MissingPiece-S3D`](https://huggingface.co/MIC-DKFZ/ResEncL-MissingPiece-S3D) | Spark 3D | ResEnc |
| [`ResEncL-MissingPiece-VoCo`](https://huggingface.co/MIC-DKFZ/ResEncL-MissingPiece-VoCo) | Volume Contrastive | ResEnc |
| [`ResEncL-MissingPiece-MultiTalent`](https://huggingface.co/MIC-DKFZ/ResEncL-MissingPiece-MultiTalent) | MultiTalent (supervised) | ResEnc |
| [`RetinaUNet-MissingPiece-MultiTalent`](https://huggingface.co/MIC-DKFZ/RetinaUNet-MissingPiece-MultiTalent) | MultiTalent (supervised) | nnDetection ConvBackbone |

Each repository holds the weights, a standalone `adaptation_plan.json`, and a
model card listing the papers to cite for that checkpoint. Every checkpoint
also carries those citations internally, and they are printed to the training
log when the weights are loaded.

```bash
pip install huggingface_hub
hf download MIC-DKFZ/ResEncL-MissingPiece-MAE checkpoint_final.pth \
    --local-dir ./checkpoints/ResEncL-MissingPiece-MAE
```

## Citation

```bibtex
@inproceedings{eckstein2025missingpiece,
  title     = {The Missing Piece: A Case for Pre-Training in 3D Medical Object Detection},
  author    = {Eckstein, Katharina and Ulrich, Constantin and Baumgartner, Michael
               and K{\"a}chele, Jessica and Bounias, Dimitrios and Wald, Tassilo
               and Floca, Ralf and Maier-Hein, Klaus H.},
  booktitle = {Medical Image Computing and Computer Assisted Intervention -- MICCAI 2025},
  year      = {2025},
  publisher = {Springer},
  doi       = {10.1007/978-3-032-04965-0_58}
}
```

## Contact

Questions are welcome at katharina.eckstein@dkfz-heidelberg.de.
