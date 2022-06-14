## Getting started with Training

## Prerequisites
Complete all of the setup as mentioned in [the setup doc](setup.md).

### Launching a small-scale baseline run
```
opt-baselines \
  -n 2 -g 8 \
  -p test_v0 \
  --model-size 125m \
  --azure \
  --checkpoints-dir "INSERT_YOUR_CHECKPOINT_DIR" \
  --no-save-dir  # Remove this if you want to print out full save-dir path
```
#### Bring up tensorboard for the run
```
tensorboard serve --logdir="INSERT_TENSORBOARD_LOGDIR"  --bind_all --port=6018
```

#### Training results logging and visualization with Aim

[Aim](https://github.com/aimhubio/aim) helps to log metaseq training runs for visualization and in-depth comparison.

**Bring up Aim for the project**

To log metaseq training metrics and hparams with Aim, you simply need to pass an extra flag `--aim-repo /path/to/log/dir`.

Example:
```shell
metaseq-train --task streaming_language_modeling \
  data-bin/pile-00 \
  --vocab-filename data-bin/pile-00/bpe-vocab.json \
  --merges-filename data-bin/pile-00/bpe-merges.txt \
  --criterion cross_entropy \
  --batch-size 8 \
  --save-dir /checkpoints/lm_transformer_pile-00 \
  --arch transformer_lm --share-decoder-input-output-embed \
  --dropout 0.1 \
  --optimizer adam --weight-decay 0.01 --clip-norm 0.0 \
  --lr 0.0005 --lr-scheduler inverse_sqrt --warmup-updates 4000 --warmup-init-lr 1e-07 \
  --tokens-per-sample 1024 --sample-break-mode none --fp16 \
  --aim-repo /path/to/log/dir
```

Once the training is started, open Aim UI to see the results:

`aim up --repo ./path/to/logs`

The following message will be outputted, meaning Aim UI is up and running:

```
Running Aim UI on repo `<Repo#-5930451821203570655 path=/.aim read_only=None>`
Open http://127.0.0.1:43800
Press Ctrl+C to exit
```

Open your browser and navigate to `http://<host>:<port>/metrics` to visualize and explore tracked metrics.
Select metrics to explore from the top left dropdown `+ Metrics` and click `Search`

![Metrics Explorer](https://user-images.githubusercontent.com/13848158/173547055-d88cacec-588c-4762-88a6-53d74279fa61.jpg)

- metaseq Aim arguments:

| Arguments | Description |
| --- | --- |
| `aim_repo` | Defines the path to store collected training logs. If set to "." logs will be stored at cwd(current working directory). |
| `aim_run_hash` | Training run hash. If skipped creates or continues run based on "save_dir". Otherwise, stores training metadata in the specified run. |

- aim up arguments:

| Arguments | Description |
| --- | --- |
| `--repo <repo_path>`        | Path to stored logs - parent directory of `.aim` repo. _Current working directory by default_. |
| `-h` &#124; `--host <host>` | Specify host address to run UI on. |
| `-p` &#124; `--port <port>` | Specify port to listen to. |

_See Aim full documentation at [aimstack.readthedocs.io](https://aimstack.readthedocs.io)._

