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

### Training results logging and visualization with Aim

[Aim](https://github.com/aimhubio/aim) is an easy-to-use and performant open-source ML experiment tracker.
Aim logs your training runs, enables a beautiful UI to compare them and an API to query them programmatically.


#### 1. Logging training results with Aim

To log metaseq training metrics and hparams with Aim, you simply need to pass an extra flag:
```shell
metaseq-train --aim_repo .
```

[TODO real train cmd]

| Arguments | Description |
| --- | --- |
| `aim_repo` | Defines the path to store collected training logs. If set to "." logs will be stored at cwd(current working directory). |
| `aim_run_hash` | Training run hash. If skipped creates or continues run based on "save_dir". Otherwise, stores training metadata in the specified run. |

#### 2. Running Aim UI to visualize the results

Once training is started, open Aim UI to see the tracked results:

`aim up --repo ./path/to/logs`

| Arguments | Description |
| --- | --- |
| `--repo <repo_path>`        | Path to stored logs - parent directory of `.aim` repo. _Current working directory by default_. |
| `-h` &#124; `--host <host>` | Specify host address to run UI on. |
| `-p` &#124; `--port <port>` | Specify port to listen to. |

_Complete list of Aim CLI usage guide find at [official docs](https://aimstack.readthedocs.io/en/latest/refs/cli.html#up)._

The following message will be printed, meaning Aim UI is up and running:

```
Running Aim UI on repo `<Repo#-5930451821203570655 path=/.aim read_only=None>`
Open http://127.0.0.1:43800
Press Ctrl+C to exit
```

#### 3. Exploring results with Aim UI

Open your browser and navigate to http://<host>:<port> (http://127.0.0.1:43800 by default) in your browser.

Aim UI home page will appear:

[TODO img]

Click on Metrics Explorer icon to start exploring metrics:

[TODO img]

Select metrics to explore from the top left dropdown `+ Metrics` and click `Search`:

[TODO img]

See Aim full documentation and usage guide at [aimstack.readthedocs.io](https://aimstack.readthedocs.io)
