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

#### Logging and visualization with Aim

[Aim](https://github.com/aimhubio/aim) is an easy-to-use and performant open-source ML experiment tracker.
Aim logs your training runs, enables a beautiful UI to compare them and an API to query them programmatically.

---

To log metaseq training metrics and hparams with an Aim, you simply need to pass an extra flag like so:
```shell
metaseq train --aim_repo .
```

| Arguments | Description |
| --- | --- |
| `aim_repo` | Defines the path to store collected training logs. If set to "." logs will be stored at cwd(current working directory). |
| `aim_run_hash` | Training run hash. If skipped creates or continues run based on "save_dir". Otherwise, stores training metadata in specified run. |

---

Run `aim up --repo ./path/to/logs` to run Aim UI to visualize, explore and compare metaseq trainings.

| Arguments | Description |
| --- | --- |
| `-h` &#124; `--host <host>` | Specify host address to run UI on. |
| `-p` &#124; `--port <port>` | Specify port to listen to. |
| `--repo <repo_path>`        | Path to stored logs - parent directory of `.aim` repo. _Current working directory by default_. |

Complete list of arguments see in [official docs](https://aimstack.readthedocs.io/en/latest/refs/cli.html#up).

