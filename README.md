# Game Cheat Detection Lab

Behavioural anomaly detection for aimbot-style cheating, demonstrated on **synthetic** player telemetry.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/sarahz101/game-cheat-detection-lab/blob/main/cheat_detection_lab.ipynb)

## What this is
Cheat software leaves behavioural fingerprints: aim-assist cheats are unnaturally fast, accurate and consistent, while human players vary. This notebook simulates player telemetry (casual players, skilled legitimate players, blatant cheaters and subtle cheaters) and compares two detectors:

1. a **rule-based baseline** using robust statistics (median and MAD), and
2. an **Isolation Forest**, an unsupervised ML model that never sees the cheater labels.

The question it explores: *can we catch subtle cheaters without wrongly flagging legitimately skilled players?*

## Results (from the included run, seed 42)
| Detector | Precision | Recall | Cheaters caught | Innocents flagged |
|---|---|---|---|---|
| Rule-based baseline | 1.00 | 0.62 | 25/40 | 0 |
| Isolation Forest | 0.95 | 0.90 | 36/40 | 2 |

The baseline catches every blatant cheater but only 40% of subtle ones. The Isolation Forest catches 84% of the subtle cheaters, at the cost of two false positives, and no skilled legitimate player was flagged. The precision-recall trade-off section shows how a review team could choose its own threshold.

## Run it
- **No install needed:** click the Colab badge above and choose *Runtime > Run all*.
- **Locally:** `pip install -r requirements.txt`, then open `cheat_detection_lab.ipynb` in Jupyter.

## Limitations
- All data is synthetic, so this demonstrates a method and is not a validated anti-cheat system.
- The contamination rate was set close to the true cheater rate, which a real system would not know.
- The model is evaluated on the data it was fitted on, which is normal for unsupervised detection but not enough for deployment.
- Detection should lead to human review, not automatic bans, because false positives harm real players.

## Next steps
- Use real or open telemetry from a game server I control.
- Model aim trajectories over time with sequence models (e.g. LSTMs).
- Add a single-player integrity track (licence-check bypass and tamper detection).
- Explain *why* a player was flagged.

## Reference
Alayed, H., Frangoudes, F. and Neuman, C. (2013) ‘Behavioral-based cheating detection in online first person shooters using machine learning techniques’, in *2013 IEEE Conference on Computational Intelligence in Games (CIG)*. Niagara Falls, ON: IEEE, pp. 1–8. doi: 10.1109/CIG.2013.6633617.
