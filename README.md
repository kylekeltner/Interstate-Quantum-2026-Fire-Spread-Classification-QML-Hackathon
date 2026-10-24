# LA County Quantum Geo fire simulation

**Run `LA_County_Quantum_Geo.ipynb`. This one notebook contains the model code and
the supplied LA County land-cover map.** It installs its scientific Python
dependencies and rebuilds all intermediate results. No previous notebook,
data folder, presentation PDF, satellite image, API key, or account for a
quantum computer is needed.

## View the saved figures

The notebook includes saved maps, charts, tables, and compact animations from
the verified default run. The first maps appear near the top, before the setup
code. Open the notebook normally to view them; a new simulation is not required.
On GitHub, select **Preview**, not **Code** or **Raw**. In VS Code, use **Open
With → Jupyter Notebook** if the file opens as JSON text.

The long encoded literal in the bundled-data cell is the compressed KML input.
It is not a result or an error. That cell is collapsed in compatible notebook
editors; GitHub may still show its source. Live sliders require Run All, while
saved PNG figures and GIF previews can be viewed without executing Python.
The bundled GIFs contain every hourly frame at a smaller display size; Run All
regenerates the full-resolution animations and refreshes the overview maps.

## Run from GitHub with Google Colab

1. Upload `LA_County_Quantum_Geo.ipynb` to your GitHub repository. The other
   files in this package are optional documentation and local setup aids.
2. Open [Google Colab](https://colab.research.google.com/), choose **File → Open
   notebook → GitHub**, and paste the GitHub URL of the notebook. You can also
   upload the notebook directly to Colab.
3. Use a **CPU** runtime with Python **3.12 or 3.13**, then choose **Runtime →
   Run all**. The first cell installs the tested package versions. If it asks
   you to restart after upgrading a package already in memory, choose
   **Runtime → Restart session**, then **Run all** again.
4. Wait for **Completed** at the bottom. Use the final download controls or
   Colab's Files panel to download GIFs, the workbook, or the complete ZIP.
   Download results before the temporary runtime ends.

GitHub itself shows a static notebook preview; it does not run the code or
interactive animation. Colab supplies Python and the notebook host, so readers
do not need to install them on their computer.

Sources: [Colab FAQ](https://research.google.com/colaboratory/faq.html),
[runtime versions](https://research.google.com/colaboratory/runtime-version-faq.html),
[GitHub notebook previews](https://docs.github.com/en/repositories/working-with-files/using-files/working-with-non-code-files#working-with-jupyter-notebook-files).

## Run locally

Use **64-bit Python 3.12 or 3.13**, internet access for the first installation,
and JupyterLab or VS Code with its Python and Jupyter extensions. An isolated
virtual environment avoids changing packages used by other projects.

Windows PowerShell:

```powershell
py -3.13 -m venv .venv
.venv\Scripts\python -m pip install jupyterlab ipykernel
.venv\Scripts\python -m jupyterlab LA_County_Quantum_Geo.ipynb
```

Linux/macOS (with Python 3.12 or 3.13 and its venv support installed):

```bash
python3.12 -m venv .venv
.venv/bin/python -m pip install jupyterlab ipykernel
.venv/bin/python -m jupyterlab LA_County_Quantum_Geo.ipynb
```

Select that environment's Python kernel and **Run All**. The notebook installs
the scientific packages itself; `requirements.txt` is also provided for an
optional preinstallation. It checks versions on every run. If setup updates
an already-imported package, restart the kernel once and run all cells again.
Python and the notebook host must exist before a notebook can execute.

Allow several minutes for setup and computation, longer on slower CPUs.
8 GB RAM and 3 GB free disk are recommended, including packages and outputs.
No GPU is used. Current pins
target Python 3.12–3.13; other Python versions stop with an explanation.

## Outputs and model

Everything is written to `quantum_geo_run/` beside the working notebook:

- `fire_outputs/48h_three_simulations/three_simulations_48h_county.gif`
- `fire_outputs/48h_three_simulations/three_simulations_48h_detail.gif`
- `fire_outputs/48h_three_simulations/quantum_data/hourly_quantum_snapshots.xlsx`
- Hourly CSVs, 48 four-qubit kernel/distance bundles, complex feature states,
  hourly confusion matrices, arrival rasters, and provenance manifests.
- `quantum_geo_results.zip`, containing the complete result set.

The notebook preserves the original seeded ignition, 90 m grid, 48-hour
display, and calculations through hour 72 for the final 24-hour forecast.
The reference, classical KNN, and quantum-kernel KNN use the same connected-cell
propagation solver. Water and unknown cells block all three; diagonals cannot
cut blocked corners. Each animation has 49 frames, hours 0–48, with each
simulation's own reached footprint and future-danger colors.

Each hour supplies 40 random points in each of five baseline future-danger
zones (200/hour, 9,600 total). Geographic training/test blocks remain disjoint.
The four-qubit danger experiment learns reference future-danger categories.
A separate static fuel-score head feeds the corrected physical simulation.
The notebook explains both targets and exports their evaluation results.

The provided scored KML is embedded as compressed data and checked against its
SHA-256 before use. The baseline is recomputed on each run; stale outputs are
never used as inputs. The original Quantum Geo presentation is cited as a
method reference and its packaging-time hash is recorded; it is not required
to run. Direct scientific dependency versions are pinned and each execution
records installed versions. Seeds and settings are fixed, but results are not
guaranteed bit-for-bit across platforms: floating-point differences can change
SVM boundary votes, nearest neighbors, and rounded fuel classes at some cells.
No quantum advantage or increased accuracy is assumed.

These are synthetic scenario forecasts, not official NFDRS ratings or
validated evacuation guidance. Green means no modeled arrival within the
forecast window, not a declaration of safety.

## Sharing

You can share just the `.ipynb`. Include this README for convenient instructions.
The supplied `.gitignore` excludes generated results and local environments.
Keep the saved figure outputs when uploading if readers should see results
without running code. This packaged copy retains PNG figures and compact GIF
previews, while omitting installation logs and inactive widget state.
