# Resource-Shared Single-PE NTT Polynomial Multiplier for CRYSTALS-Kyber

Reproducibility artifact for *Constant-Time BRAM-Free Single-PE NTT-based Polynomial Multiplier for CRYSTALS-Kyber on FPGA*.

## Requirements

* **FPGA:** Xilinx Artix-7 xc7a35tcpg236-1
* **Tool:** Vivado 2024.2 (free WebPACK licence covers xc7a35t)
* **Software:** Python ≥ 3.8, bash (tested on Ubuntu 24.04, Python 3.12)

## Repository Structure

| Path | Content |
|---|---|
| `rtl/` | Verilog: `shared_pe/`, `per_phase_baseline/`, `pipelined_barrett/`, `common/` |
| `tb/` | Testbenches: functional, constant-time, Barrett, power |
| `scripts/` | Verification, synthesis, power, TVLA, masking, shuffling, reporting, figures |
| `data/` | Test vectors, archived TVLA data, expected manuscript results |
| `reports/raw/` | Archived Vivado 2024.2 reports and simulator logs |
| `docs/` | Architecture, verification, reproducibility, security evaluation |

## Quick Start

```bash
git clone <repository-url> && cd <repository>
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
source <Vivado-install-dir>/2024.2/settings64.sh
./reproduce_all.sh --quick
```

## Reproduction Modes

| Command | What it does |
|---|---|
| `./reproduce_all.sh --quick` | RTL simulations + software analyses; no Vivado P&R (~6 min) |
| `./reproduce_all.sh --full` | Everything including Vivado synthesis/implementation/power (~45 min) |
| `./reproduce_all.sh --from-reports` | Re-analyse archived reports only; no Vivado/xsim needed (~3 min) |
| `./reproduce_all.sh --clean` | Remove generated outputs |

Output is written to `results/` including `REPRODUCIBILITY_REPORT.md`.

## Expected Results

| Metric | Shared PE | Pipelined | Per-phase |
|---|--:|--:|--:|
| LUT | 907 | 908 | 1250 |
| FF | 357 | 336 | 474 |
| DSP48E1 | 3 | 3 | 12 |
| Cycles | 27 269 | 30 853 | 27 269 |
| Fmax | 74.5 MHz | 120.5 MHz | 72.5 MHz |
| Latency | 365.9 µs | 256.1 µs | 376.3 µs |

Full traceability: [docs/manuscript_result_mapping.md](docs/manuscript_result_mapping.md).

## Citation

See [CITATION.cff](CITATION.cff).

## License

MIT — see [LICENSE](LICENSE).
