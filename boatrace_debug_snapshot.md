# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-22T11:40:01.325168+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×51 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-10-22T11:37:39]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×30  [2026-10-22T11:10:46]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 STRATEGY_CI_FAIL  ×37  [2026-10-22T11:02:25]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-22T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-22T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-22T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=185<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1269 actual=0.3333 gap=-0.2064`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=33 pred=0.3210 actual=0.2121 gap=+0.1089`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-10-22T06:00:13]
- key: `ORPHAN_SCAN|151 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1833 actual=0.0000 gap=+0.1833`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-22T06:00:13]
- key: `ROI_STAT|S00: n=185 hit%=28.1% hit_CI[Bonf]=[19.7,38.4]% ROI=0.76 ROI_boot95=[0.55,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-22T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=175 hit%=36.0% hit_CI[Bonf]=[26.4,46.9]% ROI=0.98 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-22T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=84 hit%=52.4% hit_CI[Bonf]=[37.2,67.2]% ROI=0.96 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=44.8% ROI=1.16 (コスト 8,300/回収 9,630)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=47 hit%=34.0% ROI=0.72 (コスト 11,200/回収 8,120)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=92 hit%=42.4% ROI=1.19 (コスト 20,800/回収 24,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=63 hit%=33.3% ROI=0.86 (コスト 15,100/回収 13,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift ≥+30%: n=53 hit%=24.5% ROI=0.77 (コスト 13,900/回収 10,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|bt=win: n=444 pred=0.4790 actual=0.3581 error=+0.1209 (+25%) brier=0.2430 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|S00(win): n=185 pred=0.4406 hit=0.2811 cal_err=+0.1595 brier=0.2371 BSS=-0.17 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.39MB / last modified 2026-10-22T11:39:29.881199+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
n
2026-10-22 11:38:26,929 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-10-22 11:38:26,933 [INFO] run_cycle: fetched 04/3 [scan]: 154 combos
2026-10-22 11:38:27,054 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-22 11:39:04,135 [INFO] run_cycle: === run_cycle 11:39:04 ===
2026-10-22 11:39:04,136 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-22 11:39:04,136 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-22 11:39:04,166 [INFO] predictor: Models loaded OK
2026-10-22 11:39:16,606 [INFO] scraper: odds3t: 120/120 parsed
2026-10-22 11:39:17,754 [INFO] scraper: odds3f: 20/20 parsed
2026-10-22 11:39:18,844 [INFO] scraper: odds2t: 30/30 parsed
2026-10-22 11:39:18,845 [INFO] scraper: odds2f: 15/15 parsed
2026-10-22 11:39:19,924 [INFO] scraper: odds_win: 6/6 parsed
2026-10-22 11:39:19,924 [INFO] scraper: fetch_race 03/2: boats=6 odds=191/191
2026-10-22 11:39:19,927 [INFO] predictor: CALIBRATION_MODE=on
2026-10-22 11:39:19,927 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-22 11:39:19,938 [INFO] run_cycle: fetched 03/2 [final]: 156 combos
2026-10-22 11:39:22,376 [WARNING] scraper: beforeinfo parse failed: jcd=11 rno=4
2026-10-22 11:39:22,377 [WARNING] run_cycle: fetch None: 11/4
2026-10-22 11:39:26,048 [INFO] scraper: odds3t: 120/120 parsed
2026-10-22 11:39:27,122 [INFO] scraper: odds3f: 20/20 parsed
2026-10-22 11:39:28,212 [INFO] scraper: odds2t: 30/30 parsed
2026-10-22 11:39:28,213 [INFO] scraper: odds2f: 15/15 parsed
2026-10-22 11:39:29,420 [INFO] scraper: odds_win: 6/6 parsed
2026-10-22 11:39:29,420 [INFO] scraper: fetch_race 16/3: boats=6 odds=191/191
2026-10-22 11:39:29,423 [INFO] predictor: CALIBRATION_MODE=on
2026-10-22 11:39:29,423 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-22 11:39:29,427 [INFO] run_cycle: fetched 16/3 [scan]: 156 combos
2026-10-22 11:39:29,534 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 64
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 64
  }
]
```

## Phase別通知記録 (24h)
{'final': 24, 'result': 15, 'scan': 25}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 60
  FINAL_MISSING: 51
  ANOMALY_SCAN_FINAL_RATIO: 21
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 42 | 13 | 12,600 | 10,020 | -2,580 | 0.795 |
| S01_NAKAANA1 | 47 | 15 | 9,400 | 7,160 | -2,240 | 0.762 |
| S02_TETSUBAN | 14 | 9 | 2,800 | 3,780 | +980 | 1.35 |

## 直近アラート (24h・新しい順)
```
[11:39:29] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1364}
[11:38:27] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1362}
[11:37:39] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1344}
[11:35:22] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1363}
[11:33:33] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1356}
[11:32:28] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1352}
[11:31:40] FINAL_MISSING: {"deadline": "2026-10-22T09:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102214020901", "sid": "S00"}
[11:31:40] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1336}
[11:30:35] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1335}
[11:29:42] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1334}
```

## 本日残レース: 131件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 37件 締切済
- 通知発射: scan=7 nid / final=6 nid / result=2 nid
- predictions: 3 / うち結果DB記録済: 2
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 2件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 147R | win | 1 | 0.4111 | 3.9 | 1.60 | 200 | scan=3.2 drift=+21.9% | 11:21:21 |
| S01_NAKAANA1 | 041R | win | 1 | 0.5735 | 3.7 | 2.12 | 200 | scan=- drift=- | 10:49:30 |
| S01_NAKAANA1 | 142R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=- drift=- | 08:59:18 |
| S01_NAKAANA1 | 1211R | win | 1 | 0.5174 | 3.5 | 1.81 | 200 | scan=3.2 drift=+9.4% | 20:03:19 |
| S00 | 205R | win | 1 | 0.5334 | 8.5 | 4.53 | 300 | scan=- drift=- | 19:53:18 |
| S01_NAKAANA1 | 204R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=3.5 drift=+5.7% | 19:27:44 |
| S01_NAKAANA1 | 129R | win | 1 | 0.5123 | 4.7 | 2.41 | 200 | scan=3.1 drift=+51.6% | 18:52:30 |
| S00 | 202R | win | 1 | 0.3177 | 8.4 | 2.67 | 300 | scan=10.5 drift=-20.0% | 18:31:19 |
| S01_NAKAANA1 | 128R | win | 1 | 0.4989 | 3.1 | 1.55 | 200 | scan=3.3 drift=-6.1% | 18:23:43 |
| S01_NAKAANA1 | 012R | win | 1 | 0.5990 | 3.2 | 1.92 | 200 | scan=3.0 drift=+6.7% | 15:52:30 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 63 | +28.3% | -42.2% | +495.8% | 10 | 3 | 40 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 470.1s |
| **Latency** (scan→final max) | 650.9s |
| **Traffic** (notifications 24h) | 64 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 600円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 442 | 0.4802 | 0.3575 | +0.1227 | 🟡+26% | 0.2437 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 184 | 0.4429 | 0.2826 | 0.2384 | 🔴-0.18 | 0.761 |
| S01_NAKAANA1 | win | 175 | 0.4936 | 0.3600 | 0.2431 | 🔴-0.05 | 0.979 |
| S02_TETSUBAN | win | 83 | 0.5345 | 0.5181 | 0.2569 | 🔴-0.03 | 0.946 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 7 | 0.1833 | 0.0000 | 🔴+0.1833 |
| 0.20-0.30 | 7 | 0.2288 | 0.2857 | 🔴-0.0570 |
| 0.30-0.50 | 155 | 0.4155 | 0.3290 | 🔴+0.0864 |
| 0.50+ | 265 | 0.5436 | 0.3849 | 🔴+0.1587 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 191 | 0.782 |
| win | <5.0 | ✅learned | 342 | 0.747 |
| win | <10.0 | ✅learned | 150 | 0.457 |
| win | <20.0 | ✅learned | 42 | 0.244 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-10-22T11:40:01.325168+09:00_