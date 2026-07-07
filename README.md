# Pomodoro

This project is a web-based Pomodoro app created using Python.

This projeject is a demo of AI-enabled software development and token optimization. Not intended for production and actual public use.

## Installation

We need `uv` and `venv` installed for this project.

### uv

`uv` is an extremely fast Python package and project manager, written in Rust. Open  [this link](https://docs.astral.sh/uv/#installation) for the installation information.


### venv

`venv` is a module included with Python (version 3.3 and later) used to create isolated Python virtual environments.

After `uv` is available on your system, install `venv` to create a virtual environment for this work project. Go to the root of your project and run this command:
```bash
uv venv
```

Then, activate virtual environment:
```bash
source .venv/bin/activate
```

Note: to deactivate virtual environment:
```bash
deactivate
```

## Scanning with Graphify

Make sure `.graphifyignore` exists.

Run this in the root folder:
```
graphify .
```

This will create a `graphify-out/` directory and the `graph.json` file.

To create HTML graph, run:
```
graphify cluster-only .
```

To create a HTML report based on `graph.json` file, run:
```
uvx --from graphifyy graphify export callflow-html
```